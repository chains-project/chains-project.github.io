---
title: The Different Types of Reproducible Builds
---

# The Different Types of Reproducible Builds

Reproducible builds are a set of software development practices to support an independently-verifiable path from source to binary code. 
Why its matter:

- **Security**: It allows verification that no vulnerabilities or backdoors were introduced during compilation
- **Trust**: It enables multiple parties to validate that binaries match the published source code
- **Quality Assurance**: It provides consistency in testing and deployment environments
- **Long-term Maintenance**: It makes it possible to recreate development environments years later

## Kinds of reproducible builds

**Same-environment reproducibility**: Ensures that building the same source code with the same build environment produces identical binary outputs, byte-for-byte. 

**Different-environment reproducibility**: Ensures that building the same source code within different build environments produces identical binary outputs, byte-for-byte. A classical example is changing the operating system.

**Package-registry reproducibility**: Ensures that it is possible to rebuild an artefact published on a package registry (say NPM or Maven Central) given only the package registry data as input. A weaker version of this is to take the package registry data and some additional information required to rebuild, this is what [reproducible-central](https://github.com/jvm-repo-rebuild/reproducible-central) does for Maven.

**Time-travel reproducibility**: Ensures that building the source code of the past (possibly years before) is still possible, producing identical binary outputs. The challenge is that dependencies evolve over time, and disappear.

**Functional reproducibility**: Focuses on ensuring that builds produce binaries with identical functionality, even if there are minor, non-functional differences in the output files (like timestamps or build paths). Typically, verifiers apply some kind normalization / canonicalization on the build output to achieve this.

**Compiler reproducibility**: Ensures that building the same source code with different compiler binares produces identical binary outputs, byte-for-byte. This is the essence of [diverse-double compiling](https://dwheeler.com/trusting-trust/).


