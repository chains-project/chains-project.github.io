---
title: The official CHAINS software supply chain recommendations
---


# The official CHAINS software supply chain recommendations

Based on our readings and research, we came to the following conclusions.

-- The Chains team

## CHAINS Recommends

CHAINS recommendations are meant to be directly applicable, with state of the art solutions.

- CHAINS recommends designing, implementing and enforcing [reproducible builds](https://arxiv.org/pdf/2104.06020)
- CHAINS recommends the usage of dependency pinning, via hashes.
  - In NPM, this means using [lockfiles](https://docs.npmjs.com/cli/v10/configuring-npm/package-lock-json).
  - In Maven, this means strict versions in the pom + [Maven lockfile](https://github.com/chains-project/maven-lockfile/).
- CHAINS recommends the usage of automated dependency bots such as [Renovate](<[url](https://github.com/apps/renovate)>) and Dependabot. Chains recommends activating auto-merge of dependency updates, together with a strong test suite.
- CHAINS recommends the usage of static vulnerability scanners on all commits of the main branch. This contributes to protecting against insider attacks (eg [xz](https://research.swtch.com/xz-timeline)).
- CHAINS recommends disabling dynamic evaluation of code (aka eval) in production
  - In NodeJS, this is `--disallow-code-generation-from-strings` [doc](https://nodejs.org/api/cli.html#--disallow-code-generation-from-strings)
- CHAINS recommends taking care of Github organization permissions:
  -  Do not use default "Allow all actions and reusable workflows"
  -  Do not use "Require approval for all external contributor" for CI workflows
  -  Do no use default "Read and write permissions" for token permissions
  -  Tokens should all have expiration dates
- CHAINS recommends having Github tag rulesets to enforce immutable Git tags
 
## CHAINS Encourages

These items are harder to achieve than the recommendations above, because of lack of maturity.

- CHAINS encourages transparency logs over releases/packages
- CHAINS encourages pushing build attestations on high-integrity ledgers such Sigstore/Rekor
- CHAINS encourages using functional package managers in CI (Guix, NIX)
- CHAINS encourages automated publication of SBOMs as part of the release process ([tutorial for Github release](https://chains.proj.kth.se/sbom-github.html))
- CHAINS encourages source-based package registries, such as Go. This increases transparency and auditability, and reduces the attack surface of malicious tampering.

## CHAINS says DONT

- DOn't use caching in your builds, strictly forbidden in your release builds ([caching attack](https://adnanthekhan.com/2024/05/06/the-monsters-in-your-build-cache-github-actions-cache-poisoning/))


