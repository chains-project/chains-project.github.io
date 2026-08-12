---
title: "The Dependency Your Build Downloads That No Maven Tool Will Show You"
---

# The Dependency Your Build Downloads That No Maven Tool Will Show You

For hermetic and airgapped Maven builds, the first question is "what do I need to pre-fetch?" The obvious answer is "run `dependency:tree`, or `go-offline`, and mirror everything it lists." That answer is wrong, and the gap it leaves is invisible until you actually try to build offline.

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

Building this minimal POM, however, pulls down 8 artifacts that appear nowhere in this file.
The reason for this is **dynamic dependency resolution**.
Surefire picks its test-framework provider and its dependencies.

```
maven-surefire-plugin:3.2.5                    (declared in the POM)
  │
  │  at test-execution time: detects junit-platform-commons on the test
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


## Why: this isn't in the declared graph at all

Surefire doesn't declare its test-framework provider as a Maven dependency. `maven-surefire-plugin`'s own POM lists exactly three dependencies (`maven-surefire-common`, `maven-core`, `maven-plugin-annotations`) — no provider anywhere.
Instead, [code inside the plugin](https://github.com/apache/maven-surefire/blob/surefire-3.2.5/maven-surefire-common/src/main/java/org/apache/maven/plugin/surefire/AbstractSurefireMojo.java#L1105-L1113) inspects the test classpath at *execution time* and makes a live, imperative resolver call for `org.apache.maven.surefire:surefire-junit-platform`, at Surefire's own version, independent of whatever JUnit version you declared.

1. [`createProviders`](https://github.com/apache/maven-surefire/blob/surefire-3.2.5/maven-surefire-common/src/main/java/org/apache/maven/plugin/surefire/AbstractSurefireMojo.java#L1105-L1113) builds the candidate provider list and picks the first applicable one.
2. [`JUnitPlatformProviderInfo.isApplicable()`](https://github.com/apache/maven-surefire/blob/surefire-3.2.5/maven-surefire-common/src/main/java/org/apache/maven/plugin/surefire/AbstractSurefireMojo.java#L2953-L2955) is the detection — it returns true when [`getJUnit5Artifact()`](https://github.com/apache/maven-surefire/blob/surefire-3.2.5/maven-surefire-common/src/main/java/org/apache/maven/plugin/surefire/AbstractSurefireMojo.java#L2183-L2190) finds `org.junit.platform:junit-platform-commons` on the project's test classpath, which is exactly what our one declared `junit-jupiter` dependency drags in.
3. [`JUnitPlatformProviderInfo.getProviderClasspath()`](https://github.com/apache/maven-surefire/blob/surefire-3.2.5/maven-surefire-common/src/main/java/org/apache/maven/plugin/surefire/AbstractSurefireMojo.java#L2972-L2979) then passes the string literal `"surefire-junit-platform"` — plus Surefire's own version, not yours — straight into [`SurefireDependencyResolver.getProviderClasspath`](https://github.com/apache/maven-surefire/blob/surefire-3.2.5/maven-surefire-common/src/main/java/org/apache/maven/plugin/surefire/SurefireDependencyResolver.java#L186-L200), which synthesizes a `Dependency` on the spot and hands it to Aether.

That last call is the dynamic edge: a coordinate that exists only as an argument in Java code, never as an entry in any POM. Once that one call happens, Maven resolves everything under it — the parent POM, the dependencies — through its completely ordinary, static resolution machinery. It's one dynamic entry point dragging in a normal seven-artifact static subtree behind it.

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

For comparison, an actual `mvn test -Dmaven.repo.local=sandbox2` run resolves all 8 — inspect `sandbox2/` afterward and every artifact from the diagram is there, `surefire-providers` POM included.

This isn't a Surefire-specific quirk, either:

- **`maven-failsafe-plugin`** — shares the same provider-selection code, and shows the identical blind spot.
- **`maven-compiler-plugin`** — `annotationProcessorPaths`, how tools like Error Prone get attached, resolves outside the main dependency graph. [MCOMPILER-503](https://issues.apache.org/jira/browse/MCOMPILER-503) is the upstream ticket.
- **`quarkus-maven-plugin`** — resolves "deployment" extension JARs the same way.
- **`protobuf-maven-plugin`** — combined with `os-maven-plugin`, resolves an OS-specific `protoc` binary whose exact coordinate can't even be known without evaluating a Maven extension first.

## [maven-lockfile](https://github.com/chains-project/maven-lockfile)

[maven-lockfile](https://github.com/chains-project/maven-lockfile) is a Maven plugin that pins every dependency of a build to an exact version and checksum in a `lockfile.json`, so the same build always resolves the same artifacts.
Our goal is to record these dynamically-resolved artifacts in the lockfile too, with their checksums, so that a lockfile is a complete pre-fetch list and hermetic, offline builds actually work.