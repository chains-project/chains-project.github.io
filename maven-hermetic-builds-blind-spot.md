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

Nothing exotic: JUnit 5 as a test dependency, Surefire as the runner. Building it, however, pulls down artifacts that appear nowhere in this file:

| GAV | Why |
|---|---|
| `org.apache.maven.surefire:surefire-junit-platform:3.2.5` | The JUnit-Platform *provider* Surefire selects at test-execution time |
| `org.apache.maven.surefire:common-java5:3.2.5` | The provider's own dependency |
| `org.junit.platform:junit-platform-launcher:1.9.3` | A **second**, older copy — alongside the `1.10.2` already pulled in by `junit-jupiter` |
| `org.junit.platform:junit-platform-engine:1.9.3`, `-commons:1.9.3`, `opentest4j:1.2.0` | Same story: shadow versions, pinned independently by Surefire |

That's not a rounding error. The build ends up with two different versions of `junit-platform-launcher` — one your dependency graph knows about, one it doesn't.

## Why: this isn't in the declared graph at all

Surefire doesn't declare its test-framework provider as a Maven dependency. `maven-surefire-plugin`'s own POM lists exactly three dependencies (`maven-surefire-common`, `maven-core`, `maven-plugin-annotations`) — no provider anywhere. Instead, code inside the plugin inspects the test classpath at *execution time*, detects `org.junit.jupiter`, and makes a live, imperative resolver call for `org.apache.maven.surefire:surefire-junit-platform`, at Surefire's own version, independent of whatever JUnit version you declared.

That's the root cause, and it's why every tool that only walks the declared POM graph is structurally blind to it — there's no edge in the graph to find.

## None of the native mechanisms see it

We checked, directly, against this exact reproduction:

- **`mvn dependency:tree`** — 0 matches for any of the 7 artifacts above.
- **`mvn dependency:resolve-plugins`** — 0 matches. It resolves the plugin's own *declared* dependencies (`surefire-api`, `surefire-logger-api`, ...), but the provider isn't among them.
- **`mvn dependency:go-offline`** — 0 matches. Its own documentation promises "resolve everything needed to build offline." Then, using the exact repo it just populated:
  ```
  mvn --offline test
  ...
  [ERROR] The following artifacts could not be resolved:
  org.apache.maven.surefire:surefire-junit-platform:jar:3.2.5 (absent):
  Cannot access central in offline mode and the artifact has not been
  downloaded from it before.
  ```
  A tool whose entire job is "make this buildable offline" ships a repo that isn't.

This isn't a Surefire-specific quirk, either. `maven-failsafe-plugin` shares the same provider-selection code and shows the identical blind spot. `maven-compiler-plugin`'s `annotationProcessorPaths` (how tools like Error Prone get attached) resolves outside the main dependency graph too — [MCOMPILER-503](https://issues.apache.org/jira/browse/MCOMPILER-503) is the upstream ticket. `quarkus-maven-plugin` resolves "deployment" extension JARs the same way. `protobuf-maven-plugin`, combined with `os-maven-plugin`, resolves an OS-specific `protoc` binary whose exact coordinate can't even be known without evaluating a Maven extension first. The pattern — a plugin that calls straight into the resolver from its own Mojo code instead of declaring what it needs — is common enough that it has its own [maven-lockfile issue](https://github.com/chains-project/maven-lockfile/issues/1568).

## Where maven-lockfile comes in

Today, `mvn lockfile:generate` has the same blind spot as everything above — it also only walks the declared graph. We're changing that: a [draft in progress](https://github.com/chains-project/maven-lockfile/pull/1623) adds a `DynamicResolutionSpy`, a Maven core extension that taps `EventSpy`, the same extension point Maven itself uses to observe every artifact resolution in a session — regardless of which plugin triggered it, with no per-plugin logic required. Attach it via `.mvn/extensions.xml`, and it records what it sees; `generate` merges that recording into `lockfile.json` alongside the normal dependency graph, complete with a real SHA-256 checksum for each artifact — including all 7 GAVs above, verified end-to-end against this exact reproduction.

That matters for `freeze` too. `lockfile:freeze` takes a generated lockfile and produces `pom.lockfile.xml` — a fully version-pinned POM meant to make a build reproducible without relying on Maven's live dependency resolution. A lockfile that's missing Surefire's provider is a lockfile that can describe a build it cannot actually reproduce offline. Once the dynamically-resolved artifacts are captured with real checksums at generation time, they become exactly the kind of pre-verified, pre-fetchable record an airgapped mirror needs — closing the gap between "the build passed `lockfile:validate`" and "the build actually runs with no network."

The broader point generalizes past Surefire: `dependency:tree`, `resolve-plugins`, `go-offline`, and trusted-checksums schemes all share this blind spot, because they all read the same declared graph. Anything that resolves imperatively, from inside a plugin's own code, needs a different kind of observation — not a smarter reading of the POM, but watching what the resolver actually does.
