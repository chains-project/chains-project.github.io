# Adding SBOMs to your GitHub Releases with Jreleaser

## Motivation
Software Bill of Materials (SBOMs) are critical to modern software development and supply chain management. 
An SBOM is a complete inventory of all the components and dependencies of a software product. 
It provides a detailed list of all the open-source and third-party components used in a software product, their versions and any known vulnerabilities.
SBOMs are essential for ensuring the security and integrity of software products, as they enable developers and security teams to identify and remediate vulnerabilities in a timely manner.
In this blog post, we will discuss how to add SBOMs to your GitHub releases and JReleaser, and why it is essential.

## Requirements

You need a project, a GitHub repository, and releases done with JReleaser.
Also, you need an SBOM producer that supports your build system. 
Here we show how to do it with maven and cyclonedx-maven-plugin.

## Goal 

This blog post provides a step-by-step guide on adding SBOMs to your GitHub releases using Maven and JReleaser.
We will cover the requirements for adding SBOMs, the benefits of doing so, and the steps involved in generating and adding an SBOM to your GitHub release.
By the end of this post, you will clearly understand how to add SBOMs to your software releases and why it is crucial to do so.

## Steps

1. Add a plugin to your pom.xml. If you have a different build system, you can find the appropriate plugin here: https://cyclonedx.org/docs/bom-tools/

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.cyclonedx</groupId>
         <artifactId>cyclonedx-maven-plugin</artifactId>
         <version>2.7.9</version>
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

2. Add the bom.xml and bom.json to your release script.
   If you have the JReleaser YAML file, you can add the bom.xml to the files section of the release section.

   ```yaml
   files:
     Active: ALWAYS
     artifacts:
       - path: target/bom.xml
       - path: target/bom.json
   ```

   This adds the bom.xml and bom.json to the release assets.

3. Make a release  :)
   The final result looks like this: https://github.com/chains-project/maven-lockfile/releases/tag/v3.0.0

## Conclusion
In conclusion, adding SBOMs to your GitHub releases is a simple and effective way to improve the security and integrity of your software products. Following the steps outlined in this blog post, you can easily generate and add an SBOM to your GitHub release using Maven and JReleaser. With an SBOM, you can identify and remediate vulnerabilities in your software products on time, reducing the risk of security breaches and ensuring the trust of your users. We hope this post has helped guide you through adding SBOMs to your GitHub releases, and we encourage you to continue exploring ways to improve the security and quality of your software products.

