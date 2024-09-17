# Master Thesis Topics in Project Chains

Project Chains hosts master's students for their theses, here are available topics. See [main page](/) for completed theses.

### Reproducible Builds for non-compiled languages like JavaScript

Contact: Eric Cornelissen

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

Contact: Eric Cornelissen

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


<h3 id="uid42">Empirical Study of Compilation Reproducibility in Solidity</h3>

Contact: Aman Sharma

<p>Description:
The reproducibility of software builds is a critical aspect of secure software development This concept has been pushed forward in the context of Solidity, the programming language
used for writing smart contracts on the Ethereum blockchain, with the notion of "verified contracts".
In this thesis, you will conduct an empirical study on the reproducibility of compilation in Solidity. You will recompile verified Solidity contracts and analyze the
consistency of the results. The datasets for this study will be sourced from Etherscan and Sourcify.
This research will contribute to the understanding of software integrity in the growing field of technology and could potentially inform best practices for
Solidity development.</p>
<ol>
<li id="uid43"><p><a href="http://arxiv.org/pdf/2104.06020">Reproducible Builds: Increasing the Integrity of Software Supply Chains</a></p>
</li>
<li id="uid44"><p><a href="https://etherscan.io/">Etherscan</a></p>
</li>
<li id="uid45"><p><a href="https://sourcify.dev/">Sourcify</a></p>
</li></ol>

<h3 id="uid46">Zero-knowledge software bills of materials</h3>

Contact: Javier Ron

<p>Description: Software bills of materials (SBOMs) are complete lists of software components [1], these can be helpful in tracing vulnerabilities, license compliance, etc. However, revealing an SBOM publicly also means revealing said vulnerabilities to malicious actors. Furthermore, some proprietary software developers advocate for access control for SBOM distribution [2].
Zero-knowledge proofs allows a party to convey that a statement is true without disclosing any additional information. [3]
You will design, develop, and evaluate a zero-knowledge SBOM system, which allows developers to disclose limited, but verifiable SBOM information to authorized users.</p>
<ol>
<li id="uid47"><p>The Minimum Elements For a Software Bill of Materials https://www.ntia.doc.gov/files/ntia/publications/sbomminimumelementsreport.pdf</p>
</li>
<li id="uid48"><p>An Empirical Study on Software Bill of Materials: Where We Stand and the Road Ahead http://arxiv.org/abs/2301.05362</p>
</li>
<li id="uid49"><p>Zero-knowledge proof https://en.wikipedia.org/wiki/Zero-knowledgeproof</p>
</li>
<li id="uid50"><p><a href="https://arxiv.org/abs/2307.02088">Trust in Software Supply Chains: Blockchain-Enabled SBOM and the AIBOM Future 2024</a></p>
</li></ol>

<h3 id="uid51">Study of non-reproducible builds in the Java ecosystem</h3>
<p>Description: Build Reproducibility means that a software build
always results in a bit-by-bit identical output provided the source code
and build environment is also the exact same [1]. This property is a
good safeguard against compromised build process threat [2] and
hence it is an important safeguard for software supply chain security.
In Java
ecosystem,&nbsp;<a href="https://github.com/jvm-repo-rebuild/reproducible-central">Reproducible
Central</a>&nbsp;attempts to reproduce Maven/Gradle/sbt artifacts
on&nbsp;<a href="https://mvnrepository.com/">Maven Central</a>. It does so&nbsp;by
building the artifact from source and then comparing it with the
artifact in Maven registry. If it is bit-by-bit identical, then the
maven package is said to be reproducible, else the package is
non-reproducible. In this thesis, you will create a taxonomy of reasons
for non-reproducible builds of Maven packages.</p>
<ol>
<li id="uid52"><p><a href="https://reproducible-builds.org/">https://reproducible-builds.org/</a></p>
</li>
<li id="uid53"><p><a href="https://dl.acm.org/doi/10.1145/3643764">AROMA:
Automatic Reproduction of Maven Artifacts</a></p>
</li></ol>

<h3 id="uid54">Diverse-double compilation for Java</h3>

Contact: Martin Monperrus

<p>Description:
Java is a key programming language for enterprise applications. As such, the Java compiler is an ideal target for a trusting trust attack. This thesis aims to investigate the feasibility of diverse-double compilation (DDC) to mitigate this problem You will design, implement and evaluate DDC for Java.</p>
<ol>
<li id="uid55"><p><a href="https://dl.acm.org/doi/pdf/10.1145/358198.358210?trk=public_post_comment-text">Reflections on Trusting Trust</a></p>
</li>
<li id="uid56"><p><a href="http://ieeexplore.ieee.org/document/1565233/">Countering trusting trust through diverse double-compiling</a></p>
</li>
<li id="uid57"><p><a href="http://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-323901">Diverse Double-Compiling to Harden Cryptocurrency Software (Master's thesis KTH 2023)</a></p>
</li></ol>
<p>(a related crazy idea is to do diverse-double compilation for a JIT compiler)</p>

<h3 id="uid58">Diverse-double compilation in a CI/CD Pipeline</h3>
<p>Description:
C is a fundamental programming language for system-level software. Given its widespread use, the C compiler is a prime
target for trusting trust attacks. This thesis aims to explore the systematic use of diverse-double compilation (DDC) in a modern Continuous Integration/Continuous Deployment (CI/CD) pipeline. You will design, implement and evaluate DDC in a CI/CD environment.</p>
<ol>
<li id="uid59"><p><a href="https://dl.acm.org/doi/pdf/10.1145/358198.358210?trk=public_post_comment-text">Reflections on Trusting Trust</a></p>
</li>
<li id="uid60"><p><a href="http://ieeexplore.ieee.org/document/1565233/">Countering trusting trust through diverse double-compiling</a></p>
</li>
<li id="uid61"><p><a href="http://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-323901">Diverse Double-Compiling to Harden Cryptocurrency Software (Master's thesis KTH 2023)</a></p>
</li></ol>

<h3 id="uid62">Dynamic Integrity Verification &amp; Repair for Java Applications</h3>

Contact: Martin Monperrus

<p>Description:
Attackers constantly try to tamper with the code of software applications in production.
Chang and Attalah have proposed a technique to not only detect modifications and also repairing the code after attacks by a network of small security
units called guards. These guards can be programmed to perform tasks such as checksumming the program code, and they work in concert to create mutual protection.
In this thesis, you will devise, implement and evaluate such as an approach in the context of modern Java software with dependencies. An open question is how to set up guard inside or around dependency code.</p>
<ol>
<li id="uid63"><p><a href="https://link.springer.com/chapter/10.1007/3-540-47870-1_10">Protecting Software Code by Guards</a></p>
</li>
<li id="uid64"><p><a href="https://dl.acm.org/doi/abs/10.1145/353323.353383">Reflection as a mechanism for software integrity verification</a></p>
</li>
<li id="uid65"><p><a href="https://dl.acm.org/doi/abs/10.1145/3274694.3274732">Practical integrity protection with oblivious hashing</a></p>
</li></ol>

<h3 id="uid66">Dynamic Introspection of Dependencies in Java Applications</h3>
<p>Description: We aim to design and develop a prototype for dynamic introspection of dependencies in Java applications. This would enable real-time tracking and decision based on the dependency execution context. By leveraging Java's instrumentation capabilities, the proposed system will monitor and identify the active dependencies at any given
point during program execution. The focus will be on minimizing performance
overhead to ensure that the introspection process does not significantly impact the application's responsiveness or efficiency, while integrating seamlessly with any existing Java application.
Rigorous evaluation against various benchmarks will be one to assess its accuracy,
performance, and usability.</p>

<h3 id="uid67">Automatic Backporting of Java Libraries to Older Bytecode Versions</h3>

Contact: Aman Sharma

<p>Description:
With the rapid evolution of Java, libraries often get updated to new bytecode versions. This causes compatibility issues and breakages for
applications that are still running on older versions of Java. To address this, a possible solution is to automatically backport Java libraries to older bytecode
versions. This thesis will focus on designing and implementing an automated tool for backporting Java libraries. The tool should be capable of translating new bytecode
instructions to their older equivalents, maintaining the functional behavior of the library while ensuring compatibility with older Java versions. An open question is
how to handle new language features and APIs that do not have direct equivalents in older versions.</p>
<ol>
<li id="uid68"><p><a href="https://ieeexplore.ieee.org/abstract/document/9540328/">Back to the past–analysing backporting practices in package dependency networks</a></p>
</li>
<li id="uid69"><p><a href="https://inria.hal.science/hal-01355859/file/icsme_hal.pdf">Recommending code changes for automatic backporting of Linux device drivers</a></p>
</li>
<li id="uid70"><p><a href="https://arxiv.org/abs/2405.07204">Transforming C++11 Code to C++03 to Support Legacy Compilation Environments</a></p>
</li></ol>
