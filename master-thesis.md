# Master Thesis Topics

1. [Reproducible Builds for non-compiled languages like JavaScript](#reproducible-builds-for-non-compiled-languages-like-javascript)
2. [Detection and Mitigation of GitHub action smells](#detection-and-mitigation-of-github-action-smells)

### Reproducible Builds for non-compiled languages like JavaScript

Reproducible builds can create trust in the build process of distributed software artifacts through independent verifiers.
If multiple people are able to build the same artifact it is likely that the build has not been tampered with.
The [reproducible builds](https://reproducible-builds.org/) project has made significant progress in the reproducibility of binary artifacts. But what about non-compiled languages such as JavaScript?
In the world of JavaScript it is common to either bundle a codebase (e.g. using the popular [webpack](https://reproducible-builds.org/)) or transpile down from a related language (e.g. from [TypeScript](https://www.typescriptlang.org/)).
These transformations are similar to compilation and may not be reproducible.
Here too, an attack on the build system could be used to attack systems stealthily, and reproducible builds could aid in detection.

In this project we will study the reproducibility of JavaScript build processes in one or more areas (npm packages, client-side bundling, transpiling, GitHub Actions, etc.) to understand the state of reproducibility in JavaScript and, depending on findings, propose fixes.

Related work:
1. [Reproducible Builds: Increasing the Integrity of Software Supply Chains](https://arxiv.org/abs/2104.06020)
1. [Prototype of reproducing GitHub actions](https://github.com/ericcornelissen/reproducing-actions)
1. [Reproducible Central](https://github.com/jvm-repo-rebuild/reproducible-central)

### Detection and Mitigation of GitHub action smells

[GitHub Actions](https://docs.github.com/en/actions) is the continuous integration and continuous delivery (CI/CD) solution offered by GitHub.
It supports "[expressions](https://docs.github.com/en/actions/writing-workflows/choosing-what-your-workflow-does/evaluate-expressions-in-workflows-and-actions)" which are parts of the workflow that are filled in at runtime.
The values may come from other parts of the CI/CD workflow or directly from the GitHub website.
A problem with this is that an attacker controlled value used in the wrong way can lead to compromise of the CI/CD workflow.
In this project we will look into automatically fixing such misconfigurations in GitHub Actions workflow definitions.

Related work:

Academic

1. [ARGUS: A Framework for Staged Static Taint Analysis of GitHub Workflows and Actions](https://www.usenix.org/conference/usenixsecurity23/presentation/muralee)
1. [Automatic Security Assessment of GitHub Actions Workflows](https://dl.acm.org/doi/abs/10.1145/3560835.3564554)
1. [Characterizing the Security of Github CI Workflows](https://www.usenix.org/conference/usenixsecurity22/presentation/koishybayev)
1. [Ambush From All Sides: Understanding Security Threats in Open-Source Software CI/CD Pipelines](https://ieeexplore.ieee.org/document/10061526)
1. [Mitigating Security Issues in GitHub Actions](https://orbi.umons.ac.be/bitstream/20.500.12907/48447/1/Hassan2024-EnCyCriSSVM.pdf)
1. [ActionsRemaker: Reproducing GitHub Actions](http://cdn.zhuhaonan.com/files/icse-23-actionsremaker.pdf)
1. [Quantifying Security Issues in Reusable JavaScript Actions in GitHub Workflows](https://orbi.umons.ac.be/handle/20.500.12907/48468)
1. [A Preliminary Study of GitHub Actions Dependencies](https://ceur-ws.org/Vol-3483/paper7.pdf)
1. [On the outdatedness of workflows in the GitHub Actions ecosystem](https://www.sciencedirect.com/science/article/pii/S0164121223002224)

Industry

1. https://github.com/CycodeLabs/raven
1. https://github.com/boostsecurityio/poutine
1. https://boostsecurityio.github.io/lotp/
1. https://github.com/AdnaneKhan/ActionsTOCTOU

Prototype:
- [Prototype implementation of detection](https://github.com/ericcornelissen/ades)
- [Issue for automatic repair of CI violations](https://github.com/ericcornelissen/ades/issues/42)
