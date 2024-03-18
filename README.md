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

# Consistent Hardening and Analysis of Software Supply Chains

CHAINS is a research project at [KTH Royal Institute of Technology](https://kth.se), it is about hardening the software supply chain, incl. dependency engineering as well as reproducible, executable and verifiable builds and SBOMs. 
We primarily look at Maven, NPM, and the software supply chain of crypto.
The project is funded by the [Swedish Foundation for Strategic research (SSF)](https://strategiska.se/pressmeddelande/de-fick-bidragen-i-future-software-systems/). We are recruiting software engineers, postdocs, and interns, [get in touch!](mailto:baudry@kth.se,monperrus@kth.se,musard@kth.se,mekstedt@kth.se) 

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

(chronological order)

- [The Multibillion Dollar Software Supply Chain of Ethereum](http://arxiv.org/pdf/2202.07029), IEEE Computer, 2022
- [Diverse Double-Compiling to Harden Cryptocurrency Software](http://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-323901), Master's thesis Niklas Rosencrantz, 2023
- [Silent Spring: Prototype Pollution Leads to Remote Code Execution in Node.js](https://arxiv.org/pdf/2207.11171), Usenix Security 2023
- [Challenges of Producing Software Bill Of Materials for Java](https://arxiv.org/abs/2303.11102), IEEE Security & Privacy, 2023
- [GitBark: A Rule-Based Framework for Maintaining Integrity in Source Code Repositories](https://urn.kb.se/resolve?urn=urn:nbn:se:kth:diva-340648), Master's thesis Elias Bonnici, 2023
- [Highly Available Blockchain Nodes With N-Version Design](https://arxiv.org/abs/2303.14438), IEEE Transactions on Dependable and Secure Computing, 2024
- [BUMP: A Benchmark of Reproducible Breaking Dependency Updates](http://arxiv.org/pdf/2401.09906), Proceedings of IEEE SANER, 2024

Posts:
- [Dependency Resolution in Different Ecosystems](dependency-resolution/index.md)
- [The CHAINS software supply chain recommendations](recommendations-chains.md)
- [An overview of Reproducible Builds Summit 2023](reproducible-builds-2023/index.md)
- [Software supply chain art](software-supply-chain-art.md)
- [Software supply chain attacks on crypto infrastructure](software-supply-chain-attacks-crypto.md)
- [NIX and the supply chain, debrief of NixCon 2022](nixcon-2022.md)
- [SBOMs for your GitHub Releases](sbom-github.md)

## Team

* Principal Investigators: [Musard Balliu](https://people.kth.se/~musard/), [Benoit Baudry](https://softwarediversity.eu/), [Mathias Ekstedt](https://www.kth.se/profile/mekstedt/), [Martin Monperrus](https://www.monperrus.net/martin/)
* PhD students: [Sofia Bobadilla](https://www.kth.se/profile/sofbob?l=en), [Eric Cornelissen](https://ericcornelissen.dev/), [Javier Ron](https://www.kth.se/profile/javierro), [Aman Sharma](https://algomaster99.github.io/), [Mikhail Shcherbakov](https://www.kth.se/profile/mshc), [Liu Yuxin](https://www.kth.se/profile/yuxinli), [Frank Reyes](https://www.kth.se/profile/frankrg/?l=en), [Yekatierina Churakova](https://www.kth.se/profile/yekchu?l=en)
* Research engineers & assistants: [Yogya Gamage](https://www.kth.se/profile/yogya/?l=en), [Raphina Liu](), [Elias Lundell](https://www.kth.se/profile/ellundel/) 
* Master's students: [Arvid Siberov](TODO), [Christofer Vikström](TODO), [Daniel Williams](TODO), [Felix Qvarfordt](TODO), [Vivi Andersson](TODO), [Oliver Schwalbe Lehtihet]()

Chains alumni: [Arvid Siberov](https://siberov.se), [Linus Östlund](https://www.kth.se/profile/linusost/), [Gabriel Skoglund](https://www.kth.se/profile/gabsko), [César Soto-Valero](https://www.cesarsotovalero.net/), [Martin Wittlinger](https://github.com/MartinWitt/)


## Events & Talks
- April 26 2024: [3rd KTH Workshop on the Software Supply Chain](software-supply-chain-workshop-3.md)
- October 2023: A Runtime Integrity Tool for Java Dependencies (Aman Sharma et al.). Poster at [SecDev 2023](https://secdev.ieee.org/2023/accepted-posters/)
- August 18 2023: The Software Supply Chain and its Security Implications. Benoit Baudry at [CTF Midnight sun](https://conf.midnightsunctf.com/speakers/benoit-bauldry)
- June 5 2023: Keynote "The Software Supply Chain". Benoit Baudry at the [French Conference for Software Research](https://gdrgpl2023.sciencesconf.org/resource/page/id/4). Speaker: Benoit Baudry
- May 25 2023: [The Security Implications of the Software Supply Chain](https://youtu.be/EsUGeWnGZfg). Keynote at the [CDIS Spring Conference](https://www.kth.se/cdis/events/conferences). Speaker: Benoit Baudry
- Apr 21 2023: [2nd Workshop on the Software Supply Chain @ KTH](https://chains.proj.kth.se/software-supply-chain-workshop-2). Keynote Speakers: [Christian Collberg](http://collberg.cs.arizona.edu/), [Stefano Zacchiroli](https://upsilon.cc/~zack/)
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

- June 17 2022: [Framtidens Forskning](https://framtidensforskning.se/2022/06/17/forsorjningskedjan-for-programvaror-avgorande-for-sakerheten/) (In Swedish)

## Repositories

See [https://github.com/chains-project/](https://github.com/orgs/chains-project/repositories?type=source)

## Master / Internship topics

* <https://www.kth.se/profile/musard/page/master-thesis-in-security-and-privacy?l=en>
* <https://softwarediversity.eu/topics/>
* <https://www.monperrus.net/martin/topics>.

