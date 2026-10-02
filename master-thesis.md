---
title: Open Master Thesis Topics in Project Chains
---

# Master Thesis Topics in Project Chains

Project Chains hosts master's students for their theses, here are available topics. See [main page](/) for completed theses.

### Verifiable Testing of Software

Description: This thesis investigates the application of zero-knowledge virtual machines (zkVMs) to create cryptographically verifiable proofs of test execution for software systems. Traditional software testing provides confidence in program correctness, but offers no cryptographic guarantees that tests were actually executed or passed. By leveraging zkVM technology, it becomes possible to generate succinct proofs that specific test cases were run against particular code versions and produced passing results, without revealing sensitive test data or execution traces. The research will involve: (1) implementing a testing framework integrated with zkVM platforms such as RISC Zero or SP1, (2) evaluating the computational overhead and proof generation time for various test suites, (3) designing efficient proof aggregation schemes to handle large test suites, and (4) exploring use cases such as CI/CD pipelines where verifiable test evidence could replace trust in build servers. The work will assess the practicality of zkVM-based testing for real-world software projects, measuring the trade-offs between proof size, generation cost, and verification speed.

Related Work:

[1] [RISC Zero: A zero-knowledge verifiable general computing platform](https://www.risczero.com/)

[2] [SP1: A performant, 100% open-source, contributor-friendly zkVM](https://github.com/succinctlabs/sp1)

[3] [Jolt: SNARKs for Virtual Machines via Lookups](https://eprint.iacr.org/2023/1217)

### Trust Assumptions and Threats in Build Attestation Systems

Description: 
Build attestations are cryptographically verifiable statements that describe how, when, and by whom a software artifact was produced. They are used for strengthening software supply chain security by ensuring that binaries and container images can be traced back to a documented build process. While standards like SLSA and tools such as Sigstore, Tekton Chains, and GitHub's native attestations promise to ensure trust in build outputs, there is no systematic assessment of their capabilities and limitations. This thesis will examine which trust assumptions different build attestation systems make, what attacker models they use, and how well current implementations satisfy their security goals. The work should evaluate potential attack vectors and propose recommendations for more robust, verifiable provenance.

### Server Integrity and Provenance Checking with Checksum Databases

Description: The primary objective is to develop a robust system for ensuring the integrity of server files and configurations through the use of checksum 
algorithms. The problem addressed is the increasing vulnerability of servers to unauthorized changes, data corruption, and potential security breaches, which can compromise sensitive information and disrupt services. The 
project aims to create a comprehensive checksum database that regularly scans server files, generates checksums, and compares them against a baseline to detect any unauthorized modifications. Expectations include the successful
implementation of a user-friendly interface for monitoring integrity status, the ability to generate alerts for discrepancies, and a detailed report system for auditing purposes. Ultimately, the project seeks to enhance server 
security and reliability, providing a valuable tool for system administrators in maintaining the integrity of their digital environments.

Related Work:

[1] [A study on the use of checksums for integrity verification of web downloads](https://dl.acm.org/doi/pdf/10.1145/3410154)

### Package manager with capabilities

Description: All package managers have the same semantics, all dependencies run with the same privileges as the main application. Malicious code in dependencies have a full open avenue to infect the main target application.
In this project, you will design and develop a package system with capabilities. For example, one dependency could have the right to read disk but not the other one. A clean first principle dependency calculus will be designed. Compartmentalization will be used for every dependency. To populate the package registry, there would be an automated port from an existing registry.

Related Work:

[1] [Package management systems](https://ieeexplore.ieee.org/iel5/52/6155129/06155145.pdf)

### Everything authenticated data structures

There are millions of legacy applications built with no builtin integrity. We cannot afford rewriting all of them. Yet, we need to improve their integrity. In this project,you will design and develop an automated code transformation system that automatically ports legacy data structures to authenticated data structures. For example, one could transform all linked list to authenticated linked lists. One could transform an existing non auditable banking application into a auditable one.

Related Work:

[1] [Efficient data structures for tamper-evident logging](https://www.usenix.org/event/sec09/tech/full_papers/crosby.pdf)

[2] [Custos: Practical tamper-evident auditing of operating systems using trusted execution](https://par.nsf.gov/servlets/purl/10146530)

### Structured and Standardized Model Cards for ML/AI Models

Model cards document the properties, intended use, limitations, and ethical considerations of AI/ML models to support transparency and responsible deployment. However, they are typically written in unstructured or free-form formats, leading to inconsistent content, missing information, and limited machine-readability. This lack of standardization hinders automated analysis, comparison across models, and integration with governance and auditing tools. In this Master's thesis, you will design modelcard.json, a standardized, machine-readable schema for representing model card information in a structured format. You will analyze a representative set of existing model cards to identify common fields and variations, derive a unified schema, and implement validation tools to enforce consistency. Finally, you will evaluate how the schema enables automated tasks such as comparison, completeness checking, and compliance assessment. The study aims to improve transparency and interoperability in the AI model supply chain and contribute toward a common documentation standard for trustworthy AI systems.

Related Work:

[1] [Implementing AI Bill of Materials (AI BOM) with SPDX 3.0](https://www.linuxfoundation.org/research/ai-bom)

[2] [Model Cards for Model Reporting](https://dl.acm.org/doi/10.1145/3287560.3287596)

[3] [Datasheets for datasets](https://dl.acm.org/doi/10.1145/3458723)

### Automatic Hardening of Agentic Skills

Description: AI coding agents like Claude Code are extended through "skills": markdown instruction files distributed via open registries such as skills.sh. Skills play the same role as packages in ecosystems like npm or PyPI, but with key differences. By default, skills often execute with broad user privileges and can access the local filesystem and network. Recent studies report widespread vulnerabilities across public skill registries, with confirmed malicious skills performing credential theft, exfiltration, and ransomware delivery. Existing defenses such as community "skill scanners" have been reported to be brittle, failing on simple obfuscated payloads. A core challenge is that skills use natural language to instruct agents to execute code, allowing dynamic interpretation and resolution at runtime. This makes traditional static analysis insufficient and deny-list approaches ineffective. 
In this thesis, you will investigate security properties of agent skills as a supply chain artifact and design techniques for automatic hardening of skill configurations. This may include capability-based permission models restricting what skills can access, evaluation of sandboxing approaches at different granularities, or detection methods combining static analysis with semantic understanding of skill intent.

Related Work:

[1] [Agent Skills in the Wild: An Empirical Study of Security Vulnerabilities at Scale](https://arxiv.org/pdf/2601.10338)

[2] [Socket Brings Supply Chain Security to skills.sh (blog post)](https://socket.dev/blog/socket-brings-supply-chain-security-to-skills)

### Privacy-Preserving Transparency for Open-Source Funding with Zero-Knowledge Proofs

Description: Open-source software is increasingly funded by companies and foundations, yet the funding landscape lacks transparency: who funds whom is rarely disclosed, and existing donation platforms reveal either everything or nothing. Companies often prefer not to advertise which projects they fund—whether for competitive reasons, to avoid influencing maintainer decisions, or simply for internal policy. At the same time, the broader community benefits from knowing that a project is sustainably funded and that funding is diversified. This thesis explores how zero-knowledge (ZK) proofs can reconcile these conflicting goals. The core idea is to make funders and recipients publicly visible (i.e., a company funds some open-source project, a maintainer receives funds) while keeping the individual funding edges private (i.e., which company funds which project is not revealed). A ZK proof would allow any party to verify global properties of the funding graph—such as total funding for a project, number of distinct funders, or that no single funder exceeds a dominance threshold—without learning any individual edge. The research will involve: (1) formalizing the privacy and transparency requirements for open-source funding as a graph property problem, (2) designing ZK circuits for relevant aggregate statements (e.g., sum, set membership, graph connectivity), (3) prototyping a system using existing ZK toolkits (e.g., circom, gnark, or SP1) and evaluating its practicality for realistic funding graphs, and (4) analyzing what disclosure policies are achievable and what trade-offs exist between privacy, verifiability, and usability. This is a software engineering and cryptography topic, not a blockchain or cryptocurrency topic: the system would be usable with traditional payment infrastructure and no on-chain settlement is required.

Related Work:

[1] [Groth16: On the Size of Pairing-Based Non-interactive Arguments](https://eprint.iacr.org/2016/260)

[2] [thanks.dev: open-source funding transparency platform](https://thanks.dev/)

[3] [2024 Open Source Software Funding Report (Linux Foundation)](https://www.linuxfoundation.org/research/open-source-funding-2024)

### Configurable Dependency Resolution: Adding Resolver Algorithms in Build Toolchains

Description: Every major build ecosystem ships its own dependency resolution algorithm tightly coupled to its build toolchain. Maven uses a nearest-wins strategy over a dependency tree. Go modules pioneered Minimal Version Selection (MVS). Despite the fact that all of these systems ultimately solve the same abstract problem — selecting a consistent, compatible set of package versions from a version graph — dependency resolution is conceptually separable from the build tool itself. Given a manifest (e.g., `package.json`, `pom.xml`, `Cargo.toml`), a registry, and an algorithm, the output is a resolved lock set that can in principle be handed to any native build tool for fetching and building.

This thesis investigates what happens when you decouple the resolver from the build tool: applying the resolution algorithm of ecosystem A to the dependency manifest of ecosystem B, then using the native build tool of B to build from the foreign-resolved lock set. For example, using Maven's nearest-wins strategy to resolve an npm project's `package.json`, then invoking `npm install` against those resolved versions. The study will cover multiple cross-pairings across npm, Maven, Cargo, Go, and PyPI.

Related Work:

[1] [Dependency Resolution Algorithms in Different Ecosystems](dependency-resolution/index.md)

[2] [Minimal Version Selection](https://research.swtch.com/vgo-mvs)

[3] [ecosyste-ms/package-manager-resolvers — A reference for dependency resolution algorithms and strategies across different package managers](https://github.com/ecosyste-ms/package-manager-resolvers)

[4] [Dependency Solving Is Still Hard, but We Are Getting Better at It](https://arxiv.org/abs/2011.07851)

[5] [PubGrub: Next-Generation Version Solving](https://nex3.medium.com/pubgrub-2fb6470504f)

[6] [Package Managers à la Carte: A Formal Model of Dependency Resolution](https://arxiv.org/abs/2602.18602)

[7] [The stages of package installation](https://nesbitt.io/2026/04/27/the-stages-of-package-installation.html)

### Beyond Declared Dependencies: The Limits of Hermetic Build Tools

Tools like [Hermeto](https://github.com/hermetoproject/hermeto) promise hermetic container builds by prefetching all declared dependencies before network isolation kicks in. In theory, the build runs against a closed, auditable set of inputs. In practice, the hermetic guarantee is layered and partial: Hermeto addresses the *declared dependency layer* — what appears in lockfiles like `package-lock.json`, `Cargo.lock`, or `requirements.txt` — but leaves the *toolchain and native dependency layer* to the user. Nix offers a theoretically stronger model: content-addressed derivations, sandboxed builds, and a store that captures the full dependency closure including compilers and system libraries. An ecosystem of automated translation tools — `dream2nix`, `poetry2nix`, `cargo2nix` [2] — attempts to generate these derivations from standard lockfiles, but the two models rest on different assumptions about what a hermetic boundary even means.

This thesis investigates the *hermetic gap*: the delta between what a tool declares as its dependency set and what a build actually consumes. The central question is whether Nix's stronger closure model translates into a meaningfully tighter boundary in practice, and what classes of dependencies — undeclared system libraries, toolchain leakage, native extension bindings, implicit platform assumptions — fall outside the boundary regardless of which model is used.

Related Work:

[1] [Hermeto — prefetch CLI for hermetic container builds](https://github.com/hermetoproject/hermeto)

[2] [dream2nix — automated Nix derivation generation from package manager metadata](https://github.com/nix-community/dream2nix)

[3] [Zheng, Adams, Hassan — On Build Hermeticity in Bazel-Based Build Systems, IEEE Software 2025](https://mcislab.github.io/publications/2025/ieeesw-shenyu.pdf)

[4] [Lamb & Zacchiroli — Reproducible Builds: Increasing the Integrity of Software Supply Chains, IEEE Software 2021](https://arxiv.org/pdf/2104.06020)

[5] [SLSA — Supply-chain Levels for Software Artifacts framework](https://slsa.dev/)

[6] [The Design Space of Lockfiles Across Package Managers, Empirical Software Engineering 2025](https://arxiv.org/abs/2505.04834)

[7] [The Dependency Your Build Downloads That No Maven Tool Will Show You](https://chains.proj.kth.se/maven-hermetic-builds-blind-spot.html)
