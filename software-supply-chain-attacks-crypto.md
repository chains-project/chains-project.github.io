# Software supply chain attacks on crypto

In this article, we discus attacks on cryptocurrency and digital asset infrastructures and focus on software supply chain attacks.
We first list high-profile attacks that have been made public and we discuss possible mitigations.

Authors: Martin Monperrus & the [CHAINS team](https://chains.proj.kth.se/)  
Creation date: Nov 30 2022  
Status: keeps being updated over time  
Ref URL: <https://chains.proj.kth.se/software-supply-chain-attacks-crypto.html>

## Software Attacks

### event-stream attack (Maintainer change), 2018

`event-stream` npm package by Dominic Tarr was compromised because of a maintainer change.
Dominic Tarr stopped maintaining the repository long before the attack. The bad actor reached out
to the developer in 2018 to help him out. However, he added **malicious code to steal bitcoins**
from applications and then released the malicious `event-stream` on npm. See
[issue](https://github.com/dominictarr/event-stream/issues/116) for more details. References:

- [A bad link in the cryptochain](https://www.kaspersky.com/blog/copay-supply-chain-attack/24786/)
- [Widely used open source software contained bitcoin-stealing backdoor](https://arstechnica.com/information-technology/2018/11/hacker-backdoors-widely-used-open-source-software-to-steal-bitcoin/)

### Colourama attack (typosquatting), 2018

End-user transaction attack through Pypi typosquatting by monitoring the clipboard for crypto addresses.

"A malicious package was slipped into Pypi. "Called “Colourama,” the package looked similar to Colorama, which is one of the top-20 most-downloaded legitimate modules in the Python repository. The doppelgänger Colourama package contained most of the legitimate functions of the legitimate module, with one significant difference: Colourama added code that, when run on Windows servers, installed a Visual Basic script to constantly monitor the server’s clipboard for signs a user is about to make a cryptocurrency payment."

- [Two new supply-chain attacks come to light in less than a week
  ](https://arstechnica.com/information-technology/2018/10/two-new-supply-chain-attacks-come-to-light-in-less-than-a-week/)

### Hardware wallet Ledger NaNoX, 2020

"A single connection controlled by the non-secure processor allows it to reset the display. Hence, malicious code running on the non-secure processor can turn off the display even while it’s running on battery only. This might be leveraged as part of an elaborate social engineering attack where the infected Ledger Nano X shuts off its display while malware on a computer convinces the user to press a series of buttons to approve a malicious transaction (e.g., “Your Ledger Nano X stopped responding, please hold both buttons to restart the device”).

- <https://blog.kraken.com/post/5590/kraken-security-labs-supply-chain-attacks-against-ledger-nano-x/>

### Sushiswap attack (weakly protected repo), 2021

"On Friday, September 17, 2021, Miso suffered a supply chain exploit, whereupon the fund wallet address was fixed"

- [$3 million cryptocurrency heist stemmed from a malicious GitHub commit](https://blog.sonatype.com/3-million-cryptocurrency-heist-malicious-github-commit?hsLang=en-us)

### Onus attack (through Log4J), 2021

"The attackers were able to make off with the data before an update patching the Log4j vulnerability was available and demanded $5 million in ransom for the stolen information. [...] The attackers waited until 25 December 2021 for payment from ONUS, and when they did not receive the ransom, the attackers put the information of close to 2 million customers up for sale"

- [Vietnamese Crypto Trading Platform Hit with Log4j](https://redskyalliance.org/xindustry/vietnamese-crypto-trading-platform-hit-with-log4j)

### Cryptomining attack (compromised docker images), 2022

"The Sysdig Threat Research Team (TRT) ... surfaced more than 1,600 malicious Docker images containing cryptominers, backdoors, and other nasty malware disguised as legitimate popular software."

- [Container Supply Chain Attacks Cash In on Cryptojacking](https://www.darkreading.com/attacks-breaches/container-supply-chain-attacks-cashing-in-on-cryptojacking)
- [Detecting cryptomining attacks “in the wild”](https://sysdig.com/blog/detecting-cryptomining-attacks-in-the-wild/)

### DyDx attack (NPM account compromised), 2022

The NPM account of DyDx was compromised.

- https://www.mend.io/resources/blog/popular-cryptocurrency-exchange-dydx-has-had-its-npm-account-hacked/

### Crypto Wallet Address Replacement Attacks, 2023

"At around 17:49 UTC on 9 February 2023, Phylum’s automated risk detection platform began alerting us to a long series of suspicious publications which appear to be a revived attempt to deliver the same crypto wallet clipboard replacing malware. This time, however, the attacker changed the obfuscation technique and radically increased the volume of attacks."

- <https://blog.phylum.io/phylum-discovers-revived-crypto-wallet-address-replacement-attack>

### 3CX attack (installer compromised), 2023

The hackers compromised a Windows installer and targeted a few, very specific companies in the cryptocurrency business. Not clear how they managed to infect the installer file.

- [The Massive 3CX Supply-Chain Hack Targeted Cryptocurrency Firms (Wired)](https://www.wired.com/story/3cx-supply-chain-attack-north-korea-cryptocurrency-targets/)
- [Not just an infostealer: Gopuram backdoor deployed through 3CX supply chain attack (Kaspersky)](https://securelist.com/gopuram-backdoor-deployed-through-3cx-supply-chain-attack/109344/)

### Minecraft mods attack (package manager compromised), June 2023

"Participants posting in the forum said the malware used in the attack, dubbed Fracturiser, runs on Windows and Linux systems. It’s delivered in stages that are initiated by Stage 0, which begins once someone runs one of the infected mods. Each stage downloads files from a command-and-control server and then calls for the next stage. Stage 3, believed to be the final stage in the sequence, creates folders and scripts, makes changes to the system registry, and goes on to perform the following:
Propagate itself to all JAR (Java archive) files on the filesystem, Steal cookies and login information for multiple Web browsers, Replace cryptocurrency addresses in the clipboard with alternate ones, Steal Discord credentials, Steal Microsoft and Minecraft credentials"

Reference: [Dozens of popular Minecraft mods found infected with Fracturiser malware (arstechnica.com)](https://arstechnica.com/information-technology/2023/06/dozens-of-popular-minecraft-mods-found-infected-with-fracturiser-malware/)

### Fake ledger attack (fake app on app store) 2023

Microsoft’s official App Store served up a Fake Ledger App on Microsoft App Store.

Reference: <https://decrypt.co/204506/fake-ledger-app-microsoft-app-store-zachxbt>

### Math.random() caused weak randomness until 2014 (prng issue) disclosed in 2023

BitcoinJS was widely used in early 2010s and the use of Math.random() potentially affects millions of cryptocurrency wallets that were generated in the 2011-2015 timeframe.

The main bug: the random number generator is seeded with Math.random() and the current time, granting at most ~40 bits of entropy. On-chain metadata discloses the creation time for any wallet hence all wallets created in the 2011-2015 time window on all major browsers, had problems.

Reference:

- [Randstorm](https://www.unciphered.com/randstorm)
- [Randstorm: You Can’t Patch a House of Cards](https://www.unciphered.com/blog/randstorm-you-cant-patch-a-house-of-cards)

### Ledge NPM account compromised (package attack), 2023

Ledger got their NPM account compromised.
A malicious version of a commonly used web3 connector `@ledgerhq/connect-kit` was pushed to NPM.
Many client dapps pulled the malicious version due to the absence of pinning and exact version matching, resulting in fund draining.

Reference

- <https://techcrunch.com/2023/12/14/supply-chain-attack-targeting-ledger-crypto-wallet-leaves-users-hacked/>
- <https://www.ledger.com/blog/a-letter-from-ledger-chairman-ceo-pascal-gauthier-regarding-ledger-connect-kit-exploit>

### Trust Wallet accounts drained (supply chain misuse), Jan 2024

Secbit has discovered that Trust Wallet did not correctly use a dependency (`trezor-crypto`), resulting in low entropy seed phrase generation.

Ref: <https://secbit.io/blog/en/2024/01/19/trust-wallets-fomo3d-summer-vuln/>

### Attack through AI generated code, Nov 2024

@r_cky0 [reported](https://x.com/r_cky0/status/1859656430888026524) that ChatGPT generated code containing links to scamming website, incl. executable key exfiltration.

Ref: <https://x.com/r_cky0/status/1859656430888026524>

## Hardware attacks

It is possible to tamper with hardware devices used in crypto, typically a hardware wallet. Who would do that: an employee at the company that designed the wallet, the factory that produced it, and everyone involved in shipping it. Ref: <https://vitalik.ca/general/2021/01/11/recovery.html>. Such a real hardware supply chain attack has happened on Trezor wallets (2022): <https://www.kaspersky.com/blog/fake-trezor-hardware-crypto-wallet/48155/>

## Counter-measures

### Cryptography

- "To mitigate fake devices and evil-maid attacks, we sign a public key generated on the secure chip of each device during the factory setup using our own private key. The BitBoxApp verifies the challenge is signed by a certified attestation key When you connect the BitBox02 to the host device, the BitBoxApp automatically checks that it is connected to an authentic device produced and programmed by Shift Crypto with a challenge-response mechanism. The BitBoxApp sends the BitBox02 a challenge (random number) that needs to be signed by the attestation key on the device." [How we mitigate supply chain attacks](https://shiftcrypto.ch/blog/supply-chain-attacks/)

### Old hardware

Old hardware, predating crypto, cannot contain a backdoor that has been designed for stealing crypto. Some suggest using old hardware one already has at home, such as a GameBoy, see <https://blockworks.co/news/gameboy-cold-wallet>

### Diversity

Compromising one software component is hard, compromising many is much harder.
It is a good idea to use [software diversity](https://arxiv.org/pdf/2005.11776.pdf) and hardware diversity to protect crypt funds.

Casa is a company providing key protection, their architecture distributes multiple keys across different hardware devices. Ref: [Supply chain attacks: What you need to know to protect your assets](https://blog.keys.casa/supply-chain-attacks-what-you-should-know/)

"To avoid fragility to malware, software bugs, and hardware faults, a diversity of hardware and software should be relied upon within the sets of components that are redundantly performing the same functions. This applies to hardware wallets, software which runs on the hardware wallets, the networked devices, and their operating systems." [Custody Protocols Using Bitcoin Vaults, Swambo et al. 2020](https://arxiv.org/pdf/2005.11776.pdf)

[Edit this page](https://github.com/chains-project/chains-project.github.io/edit/main/software-supply-chain-attacks-crypto.md)
