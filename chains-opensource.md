---
title: Open-source contributions of the Chains project
---

Our contributions to the infrastructure.

* Maven
  * [maven-lockfile: build integrity in Maven with lockfiles](https://github.com/chains-project/maven-lockfile/)
  * [JSON output for mvn dependency:tree (merged)](https://github.com/apache/maven-dependency-plugin/pull/391) [issue](https://issues.apache.org/jira/browse/MDEP-799) 
  * [Deterministic Maven SBOM for build-info-go (merged)](https://github.com/jfrog/build-info-go/pull/258)
  * [Expiration for deployment keys on Maven Central](https://community.sonatype.com/t/add-support-for-expiration-for-access-tokens-in-nexus/12501)
* Pypi
  * [add verifiable cryptographic signature to email event in "security history" log](https://github.com/pypi/warehouse/issues/15974)
* Go
  * [Bug identified and reproduced related to the trimpath flag (issue 67011)](https://github.com/golang/go/issues/67011)
* Github
  * [search on Github for all commits signed by a given GPG or SSH key](https://github.com/orgs/community/discussions/112411)
  * [fix outdated Github workflow template](https://github.com/actions/starter-workflows/pull/2347)
  * [keep github action logs forever for transparency and auditability of published software packages](https://github.com/orgs/community/discussions/123969)
  * [link to attestation in NPM automated notification emails](https://github.com/orgs/community/discussions/122114)
  * [Github SBOMs are not compatible with Grype](https://github.com/orgs/community/discussions/131104)   
* Docker
  * [Search docker images by checksums sha256](https://github.com/docker/roadmap/issues/663)
* npm
  * [[RRFC] Locally computed integrity values in the lockfile](https://github.com/npm/rfcs/issues/757)

Applications:
* Key contributions to make [go-ethereum / geth reproducible](https://github.com/ethereum/go-ethereum/issues/28987)
  * [enabling reproducible builds: Detached HEAD state (merged)](https://github.com/ethereum/go-ethereum/pull/30320)
  * [enabling reproducible builds: Travis CI bug (merged)](https://github.com/ethereum/go-ethereum/pull/30319)
  * [enabling reproducible builds: vcs.modified=true on downloadable artefacts](https://github.com/ethereum/go-ethereum/issues/30324)
* Diffoscope
  * [Bug Report: Different output of diffoscope on different operating system](https://lists.reproducible-builds.org/pipermail/diffoscope/2024-August/002788.html)
  * [Bug Report: Propose fix for disabling syntax highlighting in the diff](https://lists.reproducible-builds.org/pipermail/diffoscope/2024-August/002783.html)
  * [Bug Report: Propose fix for correctly identifying line endings difference in file](https://lists.reproducible-builds.org/pipermail/diffoscope/2025-January/002811.html)
* Reproducible-Central
  * [Use HTTPS to clone in buildspec](https://github.com/jvm-repo-rebuild/reproducible-central/pull/768)

Under our radar (not opened by us but relevant)
* [sandboxed build scripts at rust](https://github.com/rust-lang/rust-project-goals/issues/108)
