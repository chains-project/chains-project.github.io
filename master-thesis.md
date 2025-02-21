---
title: Open Master Thesis Topics in Project Chains
---

# Master Thesis Topics in Project Chains

Project Chains hosts master's students for their theses, here are available topics. See [main page](/) for completed theses.

### Empirical study of vulnerability tracking processes in vulnerability reports
Contact: Yekatierina Churakova
<p>Description:
Vulnerability scanning tools play a crucial role in the identification and collection of vulnerabilities across different systems and platforms. Having reliable and accurate report, which lists all associated vulnerabilities for the dependencies list, is crucial for supply-chain security. [SBOM](https://cyclonedx.org/capabilities/sbom/) and [VEX](https://cyclonedx.org/capabilities/vex/) productions tools (e.g. [Trivy](https://trivy.dev/), [Grype](https://github.com/anchore/grype), [DepScan](https://github.com/owasp-dep-scan/dep-scan) etc.) are used for this purpose. Every tool has a number of vulnerability database integrations to provide the most distinct report. However, vulnerability databases often use diverse naming conventions, IDs, and tracking systems, making it difficult to reveal information about a specific vulnerability. The inconsistency and fragmentation in vulnerability reporting is hapening, where different references to different vulnerability databases may use different identifiers for the same vulnerability, making it difficult to trace and assess risks consistently.
In this project we will explore the area of vulnerability tracking and aims to address the vulnerability naming problems. The thesis will be focused on studying the approach for mapping various vulnerability identifiers across different databases to their corresponding Common Vulnerabilities and Exposures (CVE) IDs. The aim is to improve vulnerability tracking, propose a way to solve the naming problem, and enhance the accuracy of vulnerability reports.

Related works:
1. [Impacts of Software Bill of Materials (SBOM) Generation on Vulnerability Detection](https://www.cs.montana.edu/izurieta/pubs/SCORED2024.pdf)
2. [Minimum Requirements for Vulnerability Exploitability eXchange (VEX) ](https://www.cisa.gov/sites/default/files/2023-04/minimum-requirements-for-vex-508c.pdf)
3. [Enhancing the Container Image Scanning Tool - GRYPE](https://ieeexplore.ieee.org/document/10200828)
4. [Understanding the Quality of Container Security Vulnerability Detection Tools](https://arxiv.org/pdf/2101.03844)


<h3 >Empirical Study of Compilation Reproducibility in Solidity</h3>
Contact: Aman Sharma
<p>Description:
The reproducibility of software builds is a critical aspect of secure software development This concept has been pushed forward in the context of Solidity, the programming language
used for writing smart contracts on the Ethereum blockchain, with the notion of "verified contracts".
In this thesis, you will conduct an empirical study on the reproducibility of compilation in Solidity. You will recompile verified Solidity contracts and analyze the
consistency of the results. The datasets for this study will be sourced from Etherscan and Sourcify.
This research will contribute to the understanding of software integrity in the growing field of technology and could potentially inform best practices for
Solidity development.</p>
<ol>
<li ><p><a href="http://arxiv.org/pdf/2104.06020">Reproducible Builds: Increasing the Integrity of Software Supply Chains</a></p>
</li>
<li ><p><a href="https://etherscan.io/">Etherscan</a></p>
</li>
<li ><p><a href="https://sourcify.dev/">Sourcify</a></p>
</li></ol>

<h3 >Zero-knowledge software bills of materials</h3>

Contact: Javier Ron

<p>Description: Software bills of materials (SBOMs) are complete lists of software components [1], these can be helpful in tracing vulnerabilities, license compliance, etc. However, revealing an SBOM publicly also means revealing said vulnerabilities to malicious actors. Furthermore, some proprietary software developers advocate for access control for SBOM distribution [2].
Zero-knowledge proofs allows a party to convey that a statement is true without disclosing any additional information. [3]
You will design, develop, and evaluate a zero-knowledge SBOM system, which allows developers to disclose limited, but verifiable SBOM information to authorized users.</p>
<ol>
<li ><p>The Minimum Elements For a Software Bill of Materials https://www.ntia.doc.gov/files/ntia/publications/sbomminimumelementsreport.pdf</p>
</li>
<li ><p>An Empirical Study on Software Bill of Materials: Where We Stand and the Road Ahead http://arxiv.org/abs/2301.05362</p>
</li>
<li ><p>Zero-knowledge proof https://en.wikipedia.org/wiki/Zero-knowledgeproof</p>
</li>
<li ><p><a href="https://arxiv.org/abs/2307.02088">Trust in Software Supply Chains: Blockchain-Enabled SBOM and the AIBOM Future 2024</a></p>
</li></ol>

<h3 >Study of non-reproducible builds in the Java ecosystem</h3>
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
<li ><p><a href="https://reproducible-builds.org/">https://reproducible-builds.org/</a></p>
</li>
<li ><p><a href="https://dl.acm.org/doi/10.1145/3643764">AROMA:
Automatic Reproduction of Maven Artifacts</a></p>
</li></ol>

<h3 >Dynamic Integrity Verification &amp; Repair for Java Applications</h3>
Contact: Martin Monperrus
<p>Description:
Attackers constantly try to tamper with the code of software applications in production.
Chang and Attalah have proposed a technique to not only detect modifications and also repairing the code after attacks by a network of small security
units called guards. These guards can be programmed to perform tasks such as checksumming the program code, and they work in concert to create mutual protection.
In this thesis, you will devise, implement and evaluate such as an approach in the context of modern Java software with dependencies. An open question is how to set up guard inside or around dependency code.</p>
<ol>
<li ><p><a href="https://link.springer.com/chapter/10.1007/3-540-47870-1_10">Protecting Software Code by Guards</a></p>
</li>
<li ><p><a href="https://dl.acm.org/doi/abs/10.1145/353323.353383">Reflection as a mechanism for software integrity verification</a></p>
</li>
<li ><p><a href="https://dl.acm.org/doi/abs/10.1145/3274694.3274732">Practical integrity protection with oblivious hashing</a></p>
</li></ol>

<h3 >Dynamic Introspection of Dependencies in Java Applications</h3>
<p>Contact: Aman Sharma</p>
<p>Description: We aim to design and develop a prototype for dynamic introspection of dependencies in Java applications. This would enable real-time tracking and decision based on the dependency execution context. By leveraging Java's instrumentation capabilities, the proposed system will monitor and identify the active dependencies at any given
point during program execution. The focus will be on minimizing performance
overhead to ensure that the introspection process does not significantly impact the application's responsiveness or efficiency, while integrating seamlessly with any existing Java application.
Rigorous evaluation against various benchmarks will be one to assess its accuracy,
performance, and usability.</p>

<h3 >Automatic Backporting of Java Libraries to Older Bytecode Versions</h3>
Contact: Aman Sharma
<p>Description:
With the rapid evolution of Java, libraries often get updated to new bytecode versions. This causes compatibility issues and breakages for
applications that are still running on older versions of Java. To address this, a possible solution is to automatically backport Java libraries to older bytecode
versions. This thesis will focus on designing and implementing an automated tool for backporting Java libraries. The tool should be capable of translating new bytecode
instructions to their older equivalents, maintaining the functional behavior of the library while ensuring compatibility with older Java versions. An open question is
how to handle new language features and APIs that do not have direct equivalents in older versions.</p>
<ol>
<li ><p><a href="https://ieeexplore.ieee.org/abstract/document/9540328/">Back to the past–analysing backporting practices in package dependency networks</a></p>
</li>
<li ><p><a href="https://inria.hal.science/hal-01355859/file/icsme_hal.pdf">Recommending code changes for automatic backporting of Linux device drivers</a></p>
</li>
<li ><p><a href="https://arxiv.org/abs/2405.07204">Transforming C++11 Code to C++03 to Support Legacy Compilation Environments</a></p>
</li></ol>

<h3 > Reproducible Just-in-Time (JIT) Compilation</h3>
<p>Contact: Martin Monperrus</p>
<p>This thesis will explore the concept of reproducible JIT compilation, focusing on the challenges and solutions for ensuring consistent and repeatable execution of 
program compilation across different runs. By analyzing the factors that contribute to variability in JIT compilation, such as optimization heuristics, runtime conditions,
and system configurations, you will propose methodologies to achieve reproducibility. The study will involve the design and implementation of a framework that 
captures and standardizes the JIT compilation process, enabling developers to reproduce the same JIT compilation results reliably. Through empirical evaluation, the thesis will 
assess the impact of reproducible JIT compilation on software reliability, debugging, and performance, ultimately contributing to the development of more robust and 
trustworthy software systems.</p>
<ol>
<li > [Recompilation for debugging support in a JIT-compiler](https://doi.org/10.1145/634636.586100) </li>
<li > [https://github.com/rschwietzke/jmh-C2-compile](https://github.com/rschwietzke/jmh-C2-compile) </li>
<ol>






