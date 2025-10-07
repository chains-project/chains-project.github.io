---
title: Open Master Thesis Topics in Project Chains
---

# Master Thesis Topics in Project Chains

Project Chains hosts master's students for their theses, here are available topics. See [main page](/) for completed theses.

### Audit Trail of Contributors in Dependencies
Contact: Larissa Schmid

Open-source projects rely on a community of maintainers and contributors, which is a strength but also introduces potential security risks. New contributors, in particular, can represent a vector for vulnerabilities, as demonstrated by incidents such as the compromise of the event-stream package. For projects that depend on such packages, it is critical to monitor changes in maintainers and contributors to make informed decisions about whether to continue trusting a dependency. Audit trails provide verifiable records of who made changes, when they were made, and how they were reviewed and integrated. Maintaining such records helps verify the trustworthiness of new contributors and allows reconstruction of events if a package is compromised. In this master's thesis, you will design and implement a tool that automatically generates audit trails for new contributors in the dependencies of a project. The tool will track commit history, ownership changes of packages, the introduction of new dependencies, and the presence of release signatures along with their traceability to known maintainers. 

Related Work:
[1] [OpenSSF Scorecard: On the Path Toward Ecosystem-Wide Automated Security Metrics](ieeexplore.ieee.org/abstract/document/10163720)

[2] [Decomposing and Measuring Trust in Open-Source Software Supply Chains](dl.acm.org/doi/abs/10.1145/3639476.3639775)

### Comparative Analysis of Software Composition Analysis Tools
Contact: Larissa Schmid

Software Composition Analysis (SCA) tools scan a project's dependencies to identify known security vulnerabilities, thereby supporting software supply chain security. Although numerous SCA tools have been developed, they differ significantly in functionality, capabilities, and the ecosystems they support. To date, there is no comprehensive evaluation that systematically compares these tools. This Master’s thesis aims to collect a representative set of SCA tools, analyze and compare their features, and evaluate them on a shared dataset. The study will provide practical insights into how SCA tools perform across different ecosystems and their relative strengths and limitations. 

Related Work: 
[1] [Software composition analysis for vulnerability detection: An empirical study on Java projects](dl.acm.org/doi/abs/10.1145/3611643.3616299)
[2] [Understanding Similarities and Differences Between Software Composition Analysis Tools](ieeexplore.ieee.org/abstract/document/10645968)
[3] [Adversarial Analysis of Software Composition Analysis Tools](https://link.springer.com/chapter/10.1007/978-3-031-75764-8_9)

### Empirical Study of API Difference Tools for Java Dependencies
Contact: Frank Reyes Garcia

Java applications rely extensively on external libraries, which are frequently updated and modified. As these libraries evolve, changes to their public APIs can introduce breaking changes, binary incompatibilities, or subtle behavioral issues that may impact client projects.
Detecting and understanding these API changes is critical for maintaining software reliability and facilitating safe dependency updates.
Several tools such as [roseau](https://github.com/alien-tools/roseau/tree/main?tab=readme-ov-file), [japicmp](https://siom79.github.io/japicmp/), [Revapi](https://revapi.org/), and [Clirr](https://clirr.sourceforge.net/) have been developed to analyze and report API differences between library versions.
This thesis will conduct a comprehensive comparative study of leading API diff tools, applying them to a diverse set of real-world open-source Java projects.
The evaluation will focus on each tool’s ability to detect and classify different types of API changes (e.g., breaking, non-breaking, additions, deprecations).
The outcome will be a benchmark and critical analysis of existing API diff tools and a dataset of API changes in real-world Java libraries.

Related Work:

[1] [API evolution and compatibility: A data corpus and tool evaluation](https://www.jot.fm/issues/issue_2017_04/article2.pdf)

[2] [Understanding the Impact of APIs Behavioral Breaking Changes on Client Applications](https://dl.acm.org/doi/10.1145/3643782)

### How prevalent is Maven Class Hijacking?
Contact: Aman Sharma, Frank Reyes Garcia

Maven Class Hijacking [1] is a supply chain attack where a legitimiate Java class deep in the dependency tree can act malicious by shadowing a legitimate Java class that one declares directly.
We want to explore how prevalent the condition "infection dependency precedes the gadget dependency" is.
In this thesis, we will construct a dataset of Maven projects to answer the above question.
The two criteria of the dataset can be 1) duplication of fully qualified names of class across two different dependencies.
2) dependencies that could become infectious by analyzing social engineering proxies such as no commits in the past 10 years.
In the paper [1], we also recommend a mitigation for this attack.
We would like to know how prevalent this mitigation is and in what cases it can break the build leading to a false-positive. 

[1] [Maven-Hijack: Software Supply Chain Attack Exploiting Packaging Order](https://arxiv.org/abs/2407.18760)

Related Work:

[2] [Will Dependency Conflicts Affect My Program's Semantics?](https://ieeexplore.ieee.org/document/9350237)

[3] [DevPhish: Exploring Social Engineering in Software Supply Chain Attacks on Developers](http://arxiv.org/abs/2402.18401)



### Ahead of Time Compilation Cache Analysis
Contact: Aman Sharma

[JEP 483](https://openjdk.org/jeps/483) introduced a performance optimization technique to improve startup time.
It allowed creating an "AOT" cache which stores the compiled versions of commonly loaded classfiles.
In this thesis, we will explore the commonly loaded classfile by implementing an AOT Cache reader.
Next, we can analyze how are synthetically generated classfiles handled.
Another question to investigate is if this cache can be repurposed as an allowlist of classes similar to the concept of BOMI in SBOM.exe [1].

[1] [SBOM.EXE: Countering Dynamic Code Injection based on Software Bill of Materials in Java](https://arxiv.org/abs/2407.00246)


<h3 >Trust Assumptions and Threats in Build Attestation System</h3>
Contact: Larissa Schmid
<p>Description:
Build attestations are cryptographically verifiable statements that describe how, when, and by whom a software artifact was produced. They are used for strengthening software supply chain security by ensuring that binaries and container images can be traced back to a documented build process. While standards like SLSA and tools such as Sigstore, Tekton Chains, and GitHub's native attestations promise to ensure trust in build outputs, there is no systematic assessment of their capabilities and limitations. This thesis will examine which trust assumptions different build attestation systems make, what attacker models they use, and how well current implementations satisfy their security goals. The work should evaluate potential attack vectors and propose recommendations for more robust, verifiable provenance. </p>

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
<li > <a href="https://doi.org/10.1145/634636.586100">Recompilation for debugging support in a JIT-compiler</a> </li>
<li > <a href="https://github.com/rschwietzke/jmh-C2-compile">https://github.com/rschwietzke/jmh-C2-compile</a> </li>
<ol>






