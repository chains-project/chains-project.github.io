---
title: Pushing Sigstore Attestations to Maven Central on Release
---

# Pushing Sigstore Attestations to Maven Central on Release

## Requirements

You need a project, a GitHub repository, and releases done with GitHub Actions. You also need a sigstore plugin that supports your build system.
Here we show how to do it with maven and sigstore-maven-plugin.

## Steps

1. Add a plugin to your pom.xml. If you have a different build system, you can find the appropriate plugin here: [https://docs.sigstore.dev/language_clients/language_client_overview/](https://docs.sigstore.dev/language_clients/language_client_overview/).

   ```xml
   <properties>
     <sigstore.skip>true</sigstore.skip>
   </properties>
   ```

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>dev.sigstore</groupId>
         <artifactId>sigstore-maven-plugin</artifactId>
         <version>1.3.0</version>
         <configuration>
           <skip>${sigstore.skip}</skip>
         </configuration>
         <executions>
           <execution>
             <id>sign</id>
             <goals>
               <goal>sign</goal>
             </goals>
           </execution>
         </executions>
       </plugin>
     </plugins>
   </build>
   ```

   This will create a `<filename>.sigstore.json` with the attestation during the `sign` build step. We add the optional property `sigstore.skip` to make the default to not sign (for easier local development). Signing is then enabled during deployment builds using the maven argument: `-Dsigstore.skip=false`.

2. (GitHub) Add the `id-token` permission to your release job in GitHub Actions.

   ```yaml
   jobs:
     build:
       name: Build and release
       permissions:
         id-token: write
       [...]
   ```

   This enables OIDC authentication for the release job, which is required for signing artifacts with sigstore. For additional details, see the documentation for [sigstore-maven-plugin](https://github.com/sigstore/sigstore-java/tree/main/sigstore-maven-plugin).

3. (Maven Central) JReleaser automatically uploads the `<filename>.sigstore.json` files to Maven Central.

4. Make a release :) The final result looks like this on Maven Central: https://repo1.maven.org/maven2/io/github/chains-project/maven-lockfile/5.8.2/.

