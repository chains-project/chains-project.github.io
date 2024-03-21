  # The CHAINS software supply chain recommendations

Based on our readings and research, we came to the following conclusions.

-- The Chains team

## Strongly recommends

* CHAINS strongly recommends designing, implementing and enforcing reproducible builds
* CHAINS strongly recommends the usage of dependency pinning, via hashes.
  * In NPM, this means using [lockfiles](https://docs.npmjs.com/cli/v10/configuring-npm/package-lock-json).
  * In Maven, this mean strict versions in the pom + [Maven lockfile](https://github.com/chains-project/maven-lockfile/).
* CHAINS strongly recommends the usage of automated dependency bots such as Renovate and Dependabot.

## Encourages

* CHAINS encourages transparency logs over releases and packages using verifiable data structures
* CHAINS recommends using functional package managers in CI (Guix, NIX)

