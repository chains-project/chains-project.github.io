---
title: "The Dependency Your Build Downloads That No Maven Tool Will Show You"
---

# The Dependency Your Build Downloads That No Maven Tool Will Show You

For hermetic and airgapped Maven builds, the first question is always: what do I need to pre-fetch? The obvious answer is "run `dependency:tree`, or `go-offline`, and mirror everything it lists." That answer is wrong, and the gap it leaves is invisible until you actually try to build offline.

## A two-line reproduction

```xml
<dependencies>
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>5.10.2</version>
    <scope>test</scope>
  </dependency>
</dependencies>

<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-surefire-plugin</artifactId>
      <version>3.2.5</version>
    </plugin>
  </plugins>
</build>
```

Nothing exotic: JUnit 5 as a test dependency, Surefire as the runner. Building it, however, pulls down 8 artifacts that appear nowhere in this file. There's exactly **one** genuinely dynamic resolution — Surefire picking its test-framework provider — and everything else is that one artifact's own, perfectly ordinary POM ancestry and dependency tree, invisible only because the root of that tree was never in anyone's graph to begin with:

```
maven-surefire-plugin:3.2.5                    (declared in the POM)
  │
  │  at test-execution time: detects org.junit.jupiter on the test
  │  classpath, resolves its provider directly - no POM edge for this step
  ▼
org.apache.maven.surefire:surefire-junit-platform:3.2.5  (jar)   ← the one dynamic resolution
  │
  ├─ parent POM ─▶ org.apache.maven.surefire:surefire-providers:3.2.5  (pom)
  │                  defines the dependencyManagement that pins the
  │                  unversioned junit-platform-launcher dependency below
  │
  ├─ dependency ─▶ org.apache.maven.surefire:common-java5:3.2.5        (jar)
  │
  └─ dependency ─▶ org.junit.platform:junit-platform-launcher:1.9.3    (jar)
                      │  (no version in surefire-junit-platform's own POM;
                      │   inherited from surefire-providers above)
                      │
                      ├─ dependency ─▶ org.junit.platform:junit-platform-engine:1.9.3 (jar)
                      │                   ├─ dependency ─▶ org.junit.platform:junit-platform-commons:1.9.3 (jar)
                      │                   └─ dependency ─▶ org.opentest4j:opentest4j:1.2.0                (jar)
                      │
                      └─ superseded at runtime by ─▶ org.junit.platform:junit-platform-launcher:1.10.2 (jar)
                           Surefire's own classpath assembly prefers this version for the actual
                           test run - but 1.9.3 is still resolved and downloaded via the POM chain
                           above, and neither version is ever declared by junit-jupiter, so
                           dependency:tree shows neither one.
```

Eight nodes, eight artifacts a hermetic mirror needs on disk: the provider jar, its parent POM, its direct dependency, two versions of `junit-platform-launcher`, and the three artifacts that hang off `1.9.3`. That's not a rounding error — the build ends up with two different versions of the same launcher jar, one your dependency graph knows about, one it doesn't, plus a parent POM that exists purely to serve a dependency the graph never had.

## Why: this isn't in the declared graph at all

Surefire doesn't declare its test-framework provider as a Maven dependency. `maven-surefire-plugin`'s own POM lists exactly three dependencies (`maven-surefire-common`, `maven-core`, `maven-plugin-annotations`) — no provider anywhere. Instead, code inside the plugin inspects the test classpath at *execution time*, detects `org.junit.jupiter`, and makes a live, imperative resolver call for `org.apache.maven.surefire:surefire-junit-platform`, at Surefire's own version, independent of whatever JUnit version you declared. Once that one call happens, Maven resolves everything under it — the parent POM, the dependencies — through its completely ordinary, static resolution machinery. It's one dynamic entry point dragging in a normal seven-artifact static subtree behind it.

That's the root cause, and it's why every tool that only walks the *declared* POM graph is structurally blind to the whole subtree — there's no edge in anyone's graph pointing at the root.

## None of the native mechanisms see it

We checked, directly, against this exact reproduction — each command against its own throwaway local repo, via `-Dmaven.repo.local`, so nothing pre-cached from an earlier step hides the gap:

```
mvn -B org.apache.maven.plugins:maven-dependency-plugin:3.10.0:tree           -Dmaven.repo.local=sandbox
mvn -B org.apache.maven.plugins:maven-dependency-plugin:3.10.0:resolve-plugins -Dmaven.repo.local=sandbox
mvn -B org.apache.maven.plugins:maven-dependency-plugin:3.10.0:go-offline     -Dmaven.repo.local=sandbox
mvn -B --offline test -Dmaven.repo.local=sandbox   # using the repo go-offline just populated
```

- **`dependency:tree`** — 0 matches for any of the 8 artifacts above.
- **`dependency:resolve-plugins`** — 0 matches. It resolves the plugin's own *declared* dependencies (`surefire-api`, `surefire-logger-api`, ...), but the provider isn't among them.
- **`dependency:go-offline`** — 0 matches. Its own documentation promises "resolve everything needed to build offline." Then, `mvn --offline test` against the exact repo it just populated:
  ```
  [ERROR] The following artifacts could not be resolved:
  org.apache.maven.surefire:surefire-junit-platform:jar:3.2.5 (absent):
  Cannot access central in offline mode and the artifact has not been
  downloaded from it before.
  ```
  A tool whose entire job is "make this buildable offline" ships a repo that isn't.

For comparison, an actual `mvn test -Dmaven.repo.local=sandbox2` run resolves all 8 — inspect `sandbox2/` afterward and every artifact from the diagram is there, `surefire-providers` POM included.

This isn't a Surefire-specific quirk, either. `maven-failsafe-plugin` shares the same provider-selection code and shows the identical blind spot. `maven-compiler-plugin`'s `annotationProcessorPaths` (how tools like Error Prone get attached) resolves outside the main dependency graph too — [MCOMPILER-503](https://issues.apache.org/jira/browse/MCOMPILER-503) is the upstream ticket. `quarkus-maven-plugin` resolves "deployment" extension JARs the same way. `protobuf-maven-plugin`, combined with `os-maven-plugin`, resolves an OS-specific `protoc` binary whose exact coordinate can't even be known without evaluating a Maven extension first. The pattern — a plugin that calls straight into the resolver from its own Mojo code instead of declaring what it needs — is common enough that it has its own [maven-lockfile issue](https://github.com/chains-project/maven-lockfile/issues/1568).

## Where maven-lockfile comes in

Today, `mvn lockfile:generate` has the same blind spot as everything above — it also only walks the declared graph. We're changing that: a [draft in progress](https://github.com/chains-project/maven-lockfile/pull/1623) adds a `DynamicResolutionSpy`, a Maven core extension that taps `EventSpy`, the same extension point Maven itself uses to observe every artifact resolution in a session — regardless of which plugin triggered it, with no per-plugin logic required. Attach it via `.mvn/extensions.xml`, and it records what it sees; `generate` merges that recording into `lockfile.json` alongside the normal dependency graph, complete with a real SHA-256 checksum for each artifact — verified end-to-end against this exact reproduction, capturing all 7 jars in the diagram above. (The parent POM is a known follow-up: the extension currently records binary artifacts only, on the assumption that a POM is already visible through some declared parent/BOM chain — an assumption this exact case disproves, since `surefire-providers.pom` is only ever reachable through the dynamic root.)

That matters for `freeze` too. `lockfile:freeze` takes a generated lockfile and produces `pom.lockfile.xml` — a fully version-pinned POM meant to make a build reproducible without relying on Maven's live dependency resolution. A lockfile that's missing Surefire's provider is a lockfile that can describe a build it cannot actually reproduce offline. Once the dynamically-resolved artifacts are captured with real checksums at generation time, they become exactly the kind of pre-verified, pre-fetchable record an airgapped mirror needs — closing the gap between "the build passed `lockfile:validate`" and "the build actually runs with no network."

The broader point generalizes past Surefire: `dependency:tree`, `resolve-plugins`, `go-offline`, and trusted-checksums schemes all share this blind spot, because they all read the same declared graph. Anything that resolves imperatively, from inside a plugin's own code, needs a different kind of observation — not a smarter reading of the POM, but watching what the resolver actually does.
