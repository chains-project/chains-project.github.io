  # The CHAINS software supply chain recommendations

Based on our readings and research, we came to the following conclusions.

-- The Chains team

## CHAINS Recommends

* CHAINS recommends designing, implementing and enforcing [reproducible builds](https://arxiv.org/pdf/2104.06020)
* CHAINS recommends the usage of dependency pinning, via hashes.
  * In NPM, this means using [lockfiles](https://docs.npmjs.com/cli/v10/configuring-npm/package-lock-json).
  * In Maven, this mean strict versions in the pom + [Maven lockfile](https://github.com/chains-project/maven-lockfile/).
* CHAINS recommends the usage of automated dependency bots such as [Renovate]([url](https://github.com/apps/renovate)) and Dependabot.
* CHAINS recommends the usage of static vulnerability scanners on all commits of the main branch. This contributes to protect against insider attacks (eg [xz](https://research.swtch.com/xz-timeline)).
  
## CHAINS Encourages

* CHAINS encourages transparency logs over releases/packages
* CHAINS recommends using functional package managers in CI (Guix, NIX)
* CHAINS encourages automated publication of SBOMs as part the release process ([tutorial for Github release](https://chains.proj.kth.se/sbom-github.html))

