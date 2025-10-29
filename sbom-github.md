---
title: Adding SBOMs to your GitHub and Maven Central Releases with Jreleaser
---


# Adding SBOMs to your GitHub and Maven Central Releases with Jreleaser

## Motivation
Software Bill of Materials (SBOMs) are critical to modern software development and supply chain management. 
An SBOM is a complete inventory of all the components and dependencies of a software product. 
It provides a detailed list of all the open-source and third-party components used in a software product, their versions and any known vulnerabilities.
SBOMs are essential for ensuring the security and integrity of software products, as they enable developers and security teams to identify and remediate vulnerabilities in a timely manner.
In this blog post, we will discuss how to add SBOMs to your GitHub and Maven Central releases and JReleaser, and why it is essential.

## Requirements

You need a project, a GitHub repository, and releases done with JReleaser.
Also, you need an SBOM producer that supports your build system. 
Here we show how to do it with maven and cyclonedx-maven-plugin.

## Goal 

This blog post provides a step-by-step guide on adding SBOMs to your GitHub and Maven Central releases using Maven and JReleaser.
We will cover the requirements for adding SBOMs, the benefits of doing so, and the steps involved in generating and adding an SBOM to your GitHub and Maven Central release.
By the end of this post, you will clearly understand how to add SBOMs to your software releases and why it is crucial to do so.

## Steps

1. Add a plugin to your pom.xml. If you have a different build system, you can find the appropriate plugin here: [https://cyclonedx.org/docs/bom-tools/](https://cyclonedx.org/docs/bom-tools/)

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.cyclonedx</groupId>
         <artifactId>cyclonedx-maven-plugin</artifactId>
         <version>2.9.1</version>
         <executions>
           <execution>
             <goals>
               <goal>makeAggregateBom</goal>
             </goals>
             <phase>package</phase>
           </execution>
         </executions>
       </plugin>
     </plugins>
   </build>
   ```

   This will generate a bom.xml file in the target directory. We use the `makeAggregateBom` goal to have a single sbom for all the modules of our project.

2. (GitHub) Add the bom.xml and bom.json to your release script.
   If you have the JReleaser YAML file, you can add the bom.xml to the files section of the release section. This only affects the GitHub release.

   ```yaml
   files:
     Active: ALWAYS
     artifacts:
       - path: target/bom.xml
       - path: target/bom.json
   ```

   This adds the bom.xml and bom.json to the release assets.

3. (Maven Central) JReleaser automatically uploads the SBOMs to Maven Central from version 1.6.0, if there is file matching the SBOM file name convention.
   Warning: If using the `jreleaser/release-action` action, be aware that even if you use the latest version of the action it can pull different versions of JReleaser, it must be >= 1.6.0. 
   See example from `maven-lockfile` release action:

   ```yml
     - name: Run JReleaser
       uses: jreleaser/release-action@f69e545b05f149483cecb2fb81866247992694b8
       with:
         version: 1.15.0
         arguments: full-release 
       env:
         JRELEASER_GITHUB_TOKEN: ${{ secrets.JRELEASER_GITHUB_TOKEN }}
         [...]
   ```

4. Make a release  :)
   The final result looks like this on GitHub: https://github.com/chains-project/maven-lockfile/releases/tag/v5.3.5 and like this on Maven Central: https://repo1.maven.org/maven2/io/github/chains-project/maven-lockfile/5.3.5/.

## Conclusion
In conclusion, adding SBOMs to your GitHub and Maven Central releases is a simple and effective way to improve the security and integrity of your software products. Following the steps outlined in this blog post, you can easily generate and add an SBOM to your GitHub and Maven Central release using Maven and JReleaser. With an SBOM, you can identify and remediate vulnerabilities in your software products on time, reducing the risk of security breaches and ensuring the trust of your users. We hope this post has helped guide you through adding SBOMs to your GitHub and Maven Central releases, and we encourage you to continue exploring ways to improve the security and quality of your software products.
