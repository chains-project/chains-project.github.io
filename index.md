---
name: ""
title: CHAINS Research Project at KTH
---

```
 .d8888b.  888    888        d8888 8888888 888b    888  .d8888b.  
d88P  Y88b 888    888       d88888   888   8888b   888 d88P  Y88b 
888    888 888    888      d88P888   888   88888b  888 Y88b.      
888        8888888888     d88P 888   888   888Y88b 888  "Y888b.   
888        888    888    d88P  888   888   888 Y88b888     "Y88b. 
888    888 888    888   d88P   888   888   888  Y88888       "888 
Y88b  d88P 888    888  d8888888888   888   888   Y8888 Y88b  d88P 
 "Y8888P"  888    888 d88P     888 8888888 888    Y888  "Y8888P"  
```

CHAINS is a research project at [KTH Royal Institute of Technology](https://kth.se), it is about hardening the software supply chain, incl. dependency engineering as well as reproducible, executable and verifiable builds and SBOMs. 
We primarily look at Maven, NPM, and the software supply chain of crypto.
The project is funded by the [Swedish Foundation for Strategic research (SSF)](https://strategiska.se/pressmeddelande/de-fick-bidragen-i-future-software-systems/).

To get notified about project news, subscribe to the [Chains mailing list](https://maillist.sys.kth.se/mailman/listinfo/eecs.kth.se_chains-info).

```xml
    <dependency>
      <groupId>com.martiansoftware</groupId>
      <artifactId>jsap</artifactId>
      <version>2.1</version>
    </dependency>
    <dependency>
      <groupId>org.slf4j</groupId>
      <artifactId>slf4j-api</artifactId>
      <version>1.7.36</version>
    </dependency>
    <dependency>
      <groupId>commons-io</groupId>
      <artifactId>commons-io</artifactId>
      <version>2.11.0</version>
    </dependency>
```    


## Papers & Theses

(reverse chronological order, newest first)

* 2026
  - [The Design Space of Lockfiles Across Package Managers](https://link.springer.com/article/10.1007/s10664-025-10789-w), Empirical Software Engineering, 2026.
* 2025
  - [Dirty-Waters-Action: Automated Feedback toward Cleaning Software Supply Chains](http://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-373821), Master's thesis Diogo Gaspar, 2026
  - [NodeShield: Runtime Enforcement of Security-Enhanced SBOMs for Node.js](https://doi.org/10.1145/3719027.3765136), ACM CCS, 2025.
  - [GoLeash: Mitigating Golang Software Supply Chain Attacks with Runtime Policy Enforcement](http://arxiv.org/pdf/2505.11016), Technical report 2505.11016, arXiv, 2025.
  - [Canonicalization for Unreproducible Builds in Java](https://ieeexplore.ieee.org/abstract/document/11223991/), IEEE Transactions on Software Engineering, 2025.
  - [Implementing in-toto SBOM Attestations in an Enterprise Context](http://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-363613), Master's thesis Christofer Vikström, 2025.
  - [Dirty-Waters: Detecting Software Supply Chain Smells](https://dl.acm.org/doi/abs/10.1145/3696630.3728578), ACM FSE Companion, 2025.
  - [Software Bills of Materials in Maven Central](https://ieeexplore.ieee.org/abstract/document/11025737), Proceedings of MSR, 2025.
  - [On-Chain Analysis of Smart Contract Dependency Risks on Ethereum](https://arxiv.org/abs/2503.19548), Technical report 2503.19548, arXiv, 2025.
  - [Vexed by VEX tools: Consistency evaluation of container vulnerability scanners](https://arxiv.org/abs/2503.14388), 18th International Symposium on Foundations & Practice of Security, 2025.
  - [Maven-Hijack: Software Supply Chain Attack Exploiting Packaging Order](http://arxiv.org/pdf/2407.18760), In Proceedings of ACM Workshop on Software Supply Chain Offensive Research and Ecosystem Defenses (SCORED), 2025. ([webpage](https://chains.proj.kth.se/maven-hijack.html))
  - [Towards Zero-Knowledge Software Bill of Materials](http://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-369919), Master’s thesis Tom Sorger, 2025.
  - [Diverse Double-Compiling in a CI/CD Pipeline](http://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-369921), Master’s thesis Ludvig Christensen, 2025.
  - [Detecting Semantic Changes in Dependency Updates Using Dynamic Analysis](http://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-367525), Master’s thesis Leonard Sebastian Husmann, 2025.
* 2024
  - [Code-Reuse Attacks in Managed Programming Languages and Runtimes](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-354771), PhD Thesis Mikhail Shcherbakov, 2024.
  - [Automatic Program Repair For Breaking Dependency Updates With Large Language Models](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-354835), Master's thesis Federico Bonno, 2024.
  - [Investigation of the Software Supply Chain of JavaScript Cryptocurrency Wallets](https://daisy.dsv.su.se/divaexport/fil?id=282465), Master's thesis Raphina Yi Liu, 2024.
  - [Geth Rebuild: Strengthening Ethereum Client Integrity through Reproducible Builds](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-355285), Master's thesis Vivi Andersson, 2024.
  - [From Blueprint to Reality: Evaluating the Feasibility of Air-gapped Maven Builds](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-359186), Master's thesis Oliver Schwalbe Lehtihet, 2024.
  - [The Embedding and Retrieval of Software Supply Chain Information in Java Applications](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-354837), Master's thesis Daniel Williams, 2024.
  - [Measuring the Vulnerability Lifecycle in the Software Supply Chain via SBOM Scans](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-354504), Master's thesis Felix Qvarfordt, 2024.
  - [GoSurf: Identifying Software Supply Chain Attack Vectors in Go](https://dl.acm.org/doi/abs/10.1145/3689944.3696166), Proceedings of ACM Workshop on Software Supply Chain Offensive Research and Ecosystem Defenses (SCORED), 2024.
  - [Breaking-Good: Explaining Breaking Dependency Updates with Build Analysis](https://ieeexplore.ieee.org/abstract/document/10795312), Proceedings of IEEE SCAM, 2024.
  - [SBOM.EXE: Countering Dynamic Code Injection based on Software Bill of Materials in Java](https://arxiv.org/abs/2407.00246), arXiv, 2024.
  - [GHunter: Universal Prototype Pollution Gadgets in JavaScript Runtimes](https://www.usenix.org/conference/usenixsecurity24/presentation/cornelissen), Usenix Security, 2024.
  - [Unveiling the Invisible: Detection and Evaluation of Prototype Pollution Gadgets with Dynamic Taint Analysis](https://dl.acm.org/doi/abs/10.1145/3589334.3645579), Proceedings of WWW, 2024.
  - [Mitigating CI/CD threats through an extended access control model](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-346918), Master's thesis Arvid Siberov, 2024.
  - [BUMP: A Benchmark of Reproducible Breaking Dependency Updates](https://ieeexplore.ieee.org/abstract/document/10589737), Proceedings of IEEE SANER, 2024.
  - [Highly Available Blockchain Nodes With N-Version Design](https://ieeexplore.ieee.org/abstract/document/10372117/), IEEE Transactions on Dependable and Secure Computing, 2024.
* 2023
  - [GitBark: A Rule-Based Framework for Maintaining Integrity in Source Code Repositories](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-340648), Master's thesis Elias Bonnici, 2023.
  - [Challenges of Producing Software Bill Of Materials for Java](https://www.computer.org/csdl/magazine/sp/2023/06/10235318/1Q41lK4HmYU), IEEE Security & Privacy, 2023.
  - [Silent Spring: Prototype Pollution Leads to Remote Code Execution in Node.js](https://www.usenix.org/conference/usenixsecurity23/presentation/shcherbakov), Usenix Security, 2023.
  - [Diverse Double-Compiling to Harden Cryptocurrency Software](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-323901), Master's thesis Niklas Rosencrantz, 2023.
* 2022
  - [The Multibillion Dollar Software Supply Chain of Ethereum](https://ieeexplore.ieee.org/abstract/document/9903894), IEEE Computer, 2022.


## Repositories

See [https://github.com/chains-project/](https://github.com/orgs/chains-project/repositories?type=source)

## Posts

- [CHAINS contributions to open-source](chains-opensource.md)
- [Dependency Resolution in Different Ecosystems](dependency-resolution/index.md)
- [The CHAINS software supply chain recommendations](recommendations-chains.md)
- [An overview of Reproducible Builds Summit 2023](reproducible-builds-2023/index.md)
- [Software supply chain art](software-supply-chain-art.md)
- [Software supply chain attacks on crypto infrastructure](software-supply-chain-attacks-crypto.md)
- [NIX and the supply chain, debrief of NixCon 2022](nixcon-2022.md)
- [SBOMs for your GitHub Releases](sbom-github.md)
- [Sigstore Attestations for your GitHub Releases](maven-sigstore.md)
- [Software suply chain CWEs](cwe-software-supplu-chain.md)
- [CHAINS checklist](chains-repo-checklist.md)

## Team

* Principal Investigators: [Musard Balliu](https://people.kth.se/~musard/), [Benoit Baudry](https://softwarediversity.eu/), [Mathias Ekstedt](https://www.kth.se/profile/mekstedt/), [Martin Monperrus](https://www.monperrus.net/martin/)
* Post-doctoral researchers: [Mohammad M. Ahmadpanah](https://smahmadpanah.github.io/), [Larissa Schmid](https://www.kth.se/profile/lgschmid)
* PhD students: [Sofia Bobadilla](https://www.kth.se/profile/sofbob?l=en), [Eric Cornelissen](https://ericcornelissen.dev/), [Javier Ron](https://www.kth.se/profile/javierro), [Aman Sharma](https://algomaster99.github.io/), [Yuxin Liu](https://www.kth.se/profile/yuxinli), [Frank Reyes](https://www.kth.se/profile/frankrg/?l=en), [Yekatierina Churakova](https://www.kth.se/profile/yekchu?l=en), [Carmine Cesarano](https://carminecesarano.github.io/) (visiting), [Yogya Gamage](https://scholar.google.se/citations?user=m_67-NAAAAAJ), [Vivi Andersson](TODO), [Serena Cofano](https://scholar.google.com/citations?user=Udd1jsMAAAAJ&hl=en) (visiting)
* Research engineers & assistants: [Raphina Liu](https://scholar.google.se/citations?user=h1uxQNcAAAAJ), [Elias Lundell](https://www.eliaslundell.se/), [Monica Jin](https://www.kth.se/profile/mjin/), [Diogo Torres Correia](https://www.kth.se/profile/diogotc)
* Master's students: [Christian Stjernberg](https://christian.stjernberg.com), Daniel Lai Wikström

Chains alumni: [Deepika Tiwari](https://deee92.github.io/), [Arvid Siberov](https://siberov.se), [Linus Östlund](https://www.kth.se/profile/linusost/), [Gabriel Skoglund](https://www.kth.se/profile/gabsko), [César Soto-Valero](https://www.cesarsotovalero.net/), [Martin Wittlinger](https://github.com/MartinWitt/), [Felix Qvarfordt](https://www.linkedin.com/in/felix-qvarfordt-4b1196a3/), [Daniel Williams](https://www.linkedin.com/in/d-willi/), [Oliver Schwalbe Lehtihet](https://www.linkedin.com/in/oliver-schwalbe-lehtihet/), [Federico Bono](https://www.linkedin.com/in/federico-bono/), [Elias Bonnici](https://www.linkedin.com/in/elias-bonnici-999330189/), [Christofer Vikström](TODO), [Mikhail Shcherbakov](https://www.kth.se/profile/mshc), [Leonard Husmann](https://www.linkedin.com/in/leonard-husmann/), [Tom Sorger](https://tomsorger.com/), [Ludvig Christensen](https://github.com/ludvigch)


## Events & Talks

- Jan 13 2026: Talk: "[Software supply chain attacks and defenses for Web3](http://arxiv.org/pdf/2511.12274)", Martin Monperrus, Nanyang Technological University
- Dec 17 2025, [Konflux Secure Software Factory and Hermeto](https://www.meetup.com/kth-software-research-meetup/events/312366391/?eventOrigin=group_upcoming_events) [[slides](https://drive.google.com/file/d/1mzbVse8GUr51OzQ4xDE5ol80nqg8HTHK/view)], Adam Kaplan (Red Hat)
- June 17 2025: [The Academic Nordic Blockchain Workshop 2025](academic-nordic-blockchain-2025.md)
- April 25 2025: [4th KTH Workshop on the Software Supply Chain](software-supply-chain-workshop-4.md)
- April 27 2025: Talk: "[Software supply chain attacks and defenses for Web3](http://arxiv.org/pdf/2511.12274)", Martin Monperrus, University of Zurich
- Jan 30 2025 Consistent Hardening and Analysis of Software Supply Chains, Talk at Umeå University, Martin Monperrus
- Jan 8 2025, OSS Remediation Ops: From Project-Centric Strategies to Ecosystem-wide Analysis, [Lyuye Zhang](https://lyuyezhang.github.io/), Nanyang Technological University, Singapore
- Oct 18 2024 GoSurf: Identifying Software Supply Chain Attack Vectors in Go, Talk at SCORED, Carmine Cesarano and Vivi Andersson
- May 23 2024: [Chains talk at Dataföreningen](https://dfs.se/pa_gang/prata-eu-cyber-resilience-act-med-oss-16-2/)
- April 26 2024: [3rd KTH Workshop on the Software Supply Chain](software-supply-chain-workshop-3.md)
- Nov 26 2023: [The Chains SBOM orchestra at SCORED](https://github.com/chains-project/sbom-orchestra/), Chains Team, [SCORED 2023](https://scored.dev), Copenhagen
- October 2023: A Runtime Integrity Tool for Java Dependencies (Aman Sharma et al.). Poster at [SecDev 2023](https://secdev.ieee.org/2023/accepted-posters/)
- August 18 2023: The Software Supply Chain and its Security Implications. Benoit Baudry at [CTF Midnight sun](https://conf.midnightsunctf.com/speakers/benoit-bauldry)
- June 5 2023: Keynote "The Software Supply Chain". Benoit Baudry at the [French Conference for Software Research](https://gdrgpl2023.sciencesconf.org/resource/page/id/4). Speaker: Benoit Baudry
- May 25 2023: [The Security Implications of the Software Supply Chain](https://youtu.be/EsUGeWnGZfg). Keynote at the [CDIS Spring Conference](https://www.kth.se/cdis/events/conferences). Speaker: Benoit Baudry
- Apr 21 2023: [2nd Workshop on the Software Supply Chain @ KTH](https://chains.proj.kth.se/software-supply-chain-workshop-2). Keynote Speakers: [Christian Collberg](https://collberg.cs.arizona.edu/), [Stefano Zacchiroli](https://upsilon.cc/~zack/)
- Apr 18 2023: [Highly Available Blockchain Nodes With N-Version Design](https://www.meetup.com/kth-software-research-meetup/events/292824632/). Speaker: Javier Ron
- Mar 31 2023: [Verifiable source-only bootstrap from scratch](TBA). Speaker: an
- Mar 08 2023: [SBOM for Alpine Linux](https://www.meetup.com/fr-FR/kth-software-research-meetup/events/291758976/). Speaker: [Hans Thorsen Lamm](https://www.linkedin.com/in/hans-thorsen-b76411244/?originalSubdomain=se).
- Jan 19 2023: [Talk: The software supply chain of crypto](https://www.meetup.com/decentralized-camp/events/290035869/) Decentralization meetup Stockholm, Speaker: Martin Monperrus
- Dec 08 2022: [Software bloat in PyPI](https://www.meetup.com/kth-software-research-meetup/events/288920697/). Speaker: [Georgios Drosos](https://www.linkedin.com/in/georgios-petros-drosos-498063173/) (Athens University of Economics and Business)
- Nov 15 2022: [Building Robust Software Supply Chains](https://docs.google.com/presentation/d/1CvrbdWn4qndZE1x6-VManWwL5mZXdJGZ-N0n6PPOXvU/edit#slide=id.g18d8483ced4_2_54) at [STEW'22](https://www.swedsoft.se/2022/08/29/program-biljettslapp-stew-2022/). Speaker: Benoit Baudry
- Sep 30 2022: [1st Workshop on the Software Supply Chain @ KTH](https://chains.proj.kth.se/software-suppply-chain-workshop-1)
- Sep 20 2022: [Open-source security analysis @SAP](https://www.meetup.com/fr-FR/kth-software-research-meetup/events/288225155/). Speakers: [Henrik Plate](https://www.linkedin.com/in/henrikplate/) (SAP), [Serena Elisa Ponta](https://scholar.google.it/citations?user=DFVwF6sAAAAJ&hl=en) (SAP)
- Jun 14 2022: [Building Robust Software Supply Chains](https://www.dropbox.com/s/lkf6v6k3fngpke2/software-supply-chain-baudry-xp2022.pdf?dl=0) at [XP'22](https://www.agilealliance.org/xp2022/). Speaker: Benoit Baudry

## Press

- [Bygger mer robusta programvarukedjorn](https://framtidensforskning.se/2024/06/12/bygger-mer-robusta-programvarukedjor/), in Framtidens Forskning (June 12 2024, In Swedish)
- [Försörjningskedjan för programvaror avgörande för säkerheten](https://framtidensforskning.se/2022/06/17/forsorjningskedjan-for-programvaror-avgorande-for-sakerheten/), in Framtidens Forskning (June 17 2022, In Swedish)


## Master / Internship topics

* [CHAINS master's thesis topics](master-thesis.md)
* <https://www.kth.se/profile/musard/page/master-thesis-in-security-and-privacy?l=en>
* <https://softwarediversity.eu/topics/>
* <https://www.monperrus.net/martin/topics>.

