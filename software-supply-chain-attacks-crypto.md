---
title: Software supply chain attacks on crypto and web3
---

# Software supply chain attacks on crypto and web3

In this post, we discus attacks on cryptocurrency and digital assets infrastructures that are based on software supply chain attacks.
We aim to be the most comprehensive list, with all high-profile attacks that have been made public.

Authors: [Martin Monperrus](mailto:monperrus@kth.se)  
Creation date: Nov 30 2022  
Status: updated over time, last update 2025 
Ref URL: <https://chains.proj.kth.se/software-supply-chain-attacks-crypto.html>

## Software Attacks

### 1. event-stream attack (Maintainer change), 2018

`event-stream` npm package by Dominic Tarr was compromised because of a maintainer change.
Dominic Tarr stopped maintaining the repository long before the attack. The bad actor reached out
to the developer in 2018 to help him out. However, he added **malicious code to steal bitcoins**
from applications and then released the malicious `event-stream` on npm. See
[issue](https://github.com/dominictarr/event-stream/issues/116) for more details. References:

- [A bad link in the cryptochain](https://www.kaspersky.com/blog/copay-supply-chain-attack/24786/)
- [Widely used open source software contained bitcoin-stealing backdoor](https://arstechnica.com/information-technology/2018/11/hacker-backdoors-widely-used-open-source-software-to-steal-bitcoin/)

### 2. Colourama attack (typosquatting), 2018

End-user transaction attack through Pypi typosquatting by monitoring the clipboard for crypto addresses.

"A malicious package was slipped into Pypi. "Called “Colourama,” the package looked similar to Colorama, which is one of the top-20 most-downloaded legitimate modules in the Python repository. The doppelgänger Colourama package contained most of the legitimate functions of the legitimate module, with one significant difference: Colourama added code that, when run on Windows servers, installed a Visual Basic script to constantly monitor the server’s clipboard for signs a user is about to make a cryptocurrency payment."

- [Two new supply-chain attacks come to light in less than a week
  ](https://arstechnica.com/information-technology/2018/10/two-new-supply-chain-attacks-come-to-light-in-less-than-a-week/)

### 3. Hardware wallet Ledger NaNoX, 2020

"A single connection controlled by the non-secure processor allows it to reset the display. Hence, malicious code running on the non-secure processor can turn off the display even while it’s running on battery only. This might be leveraged as part of an elaborate social engineering attack where the infected Ledger Nano X shuts off its display while malware on a computer convinces the user to press a series of buttons to approve a malicious transaction (e.g., “Your Ledger Nano X stopped responding, please hold both buttons to restart the device”).

- <https://blog.kraken.com/post/5590/kraken-security-labs-supply-chain-attacks-against-ledger-nano-x/>

### 4. Sushiswap attack (weakly protected repo), 2021

"On Friday, September 17, 2021, Miso suffered a supply chain exploit, whereupon the fund wallet address was fixed"

- [$3 million cryptocurrency heist stemmed from a malicious GitHub commit](https://blog.sonatype.com/3-million-cryptocurrency-heist-malicious-github-commit?hsLang=en-us)

### 5. Onus attack (through Log4shell), 2021

"The attackers were able to make off with the data before an update patching the Log4j vulnerability was available and demanded $5 million in ransom for the stolen information. [...] The attackers waited until 25 December 2021 for payment from ONUS, and when they did not receive the ransom, the attackers put the information of close to 2 million customers up for sale"

- [Vietnamese Crypto Trading Platform Hit with Log4j](https://redskyalliance.org/xindustry/vietnamese-crypto-trading-platform-hit-with-log4j)

### 6. Cryptomining attack campaign (compromised docker images), 2022

"The Sysdig Threat Research Team (TRT) ... surfaced more than 1,600 malicious Docker images containing cryptominers, backdoors, and other nasty malware disguised as legitimate popular software."

- [Container Supply Chain Attacks Cash In on Cryptojacking](https://www.darkreading.com/attacks-breaches/container-supply-chain-attacks-cashing-in-on-cryptojacking)
- [Detecting cryptomining attacks “in the wild”](https://sysdig.com/blog/detecting-cryptomining-attacks-in-the-wild/)

### 7. DyDx attack (NPM account compromised), 2022

The NPM account of dYdX, a popular decentralized cryptocurrency exchange, was compromised in 2022. The attackers gained access to dYdX's NPM account and published malicious versions of their legitimate packages. The compromised packages contained malware designed to steal cryptocurrency from users.

The attack targeted the @dydxprotocol scoped packages on the NPM registry. Once discovered, dYdX quickly revoked the compromised credentials and removed the malicious packages from NPM. 

- [Popular Cryptocurrency Exchange dYdX Has Had Its NPM Account Hacked](https://www.mend.io/blog/popular-cryptocurrency-exchange-dydx-has-had-its-npm-account-hacked/)

### 8. Crypto Wallet Address Replacement Attacks, 2023

"At around 17:49 UTC on 9 February 2023, Phylum’s automated risk detection platform began alerting us to a long series of suspicious publications which appear to be a revived attempt to deliver the same crypto wallet clipboard replacing malware. This time, however, the attacker changed the obfuscation technique and radically increased the volume of attacks."

- <https://blog.phylum.io/phylum-discovers-revived-crypto-wallet-address-replacement-attack>

### 9. 3CX attack (installer compromised), 2023

The hackers compromised a Windows installer and targeted a few, very specific companies in the cryptocurrency business. It is unknown how they managed to infect the installer file.

- [The Massive 3CX Supply-Chain Hack Targeted Cryptocurrency Firms (Wired)](https://www.wired.com/story/3cx-supply-chain-attack-north-korea-cryptocurrency-targets/)
- [Not just an infostealer: Gopuram backdoor deployed through 3CX supply chain attack (Kaspersky)](https://securelist.com/gopuram-backdoor-deployed-through-3cx-supply-chain-attack/109344/)

### 10. Minecraft mods attack (package manager compromised), June 2023

"Participants posting in the forum said the malware used in the attack, dubbed Fracturiser, runs on Windows and Linux systems. It’s delivered in stages that are initiated by Stage 0, which begins once someone runs one of the infected mods. Each stage downloads files from a command-and-control server and then calls for the next stage. Stage 3, believed to be the final stage in the sequence, creates folders and scripts, makes changes to the system registry, and goes on to perform the following:
Propagate itself to all JAR (Java archive) files on the filesystem, Steal cookies and login information for multiple Web browsers, Replace cryptocurrency addresses in the clipboard with alternate ones, Steal Discord credentials, Steal Microsoft and Minecraft credentials"

Reference: [Dozens of popular Minecraft mods found infected with Fracturiser malware (arstechnica.com)](https://arstechnica.com/information-technology/2023/06/dozens-of-popular-minecraft-mods-found-infected-with-fracturiser-malware/)

### 11. Fake Ledger app attack (Microsoft App Store), 2023

A malicious actor published a fake Ledger hardware wallet application on Microsoft's official App Store, impersonating the legitimate Ledger cryptocurrency wallet software. 

Blockchain investigator ZachXBT identified and reported the fake app in December 2023. The malicious application remained available in the Microsoft App Store for some time despite multiple user reports, highlighting weaknesses in the app review process for official app marketplaces. This incident demonstrates how threat actors can leverage trusted distribution channels to target cryptocurrency users specifically.

References:
- [Fake Ledger App Found on Microsoft App Store (zachxbt)](https://decrypt.co/204506/fake-ledger-app-microsoft-app-store-zachxbt)
- [Ledger Warning About Fake Apps](https://support.ledger.com/article/fraudulent-ledger-live-applications)

Reference: <https://decrypt.co/204506/fake-ledger-app-microsoft-app-store-zachxbt>

### 12. Math.random() caused weak randomness until 2014 (prng issue) disclosed in 2023

BitcoinJS was widely used in early 2010s and the use of Math.random() potentially affects millions of cryptocurrency wallets that were generated in the 2011-2015 timeframe.

The main bug: the random number generator is seeded with Math.random() and the current time, granting at most ~40 bits of entropy. On-chain metadata discloses the creation time for any wallet hence all wallets created in the 2011-2015 time window on all major browsers, had problems.

Reference:

- [Randstorm: You Can’t Patch a House of Cards](https://www.unciphered.com/blog/randstorm-you-cant-patch-a-house-of-cards)

### 13. Ledger NPM account compromised (package attack), 2023

Ledger got their NPM account compromised.
A malicious version of a commonly used web3 connector `@ledgerhq/connect-kit` was pushed to NPM.
Many client dapps pulled the malicious version due to the absence of pinning and exact version matching, resulting in fund draining.

Reference

- <https://techcrunch.com/2023/12/14/supply-chain-attack-targeting-ledger-crypto-wallet-leaves-users-hacked/>
- <https://www.ledger.com/blog/a-letter-from-ledger-chairman-ceo-pascal-gauthier-regarding-ledger-connect-kit-exploit>


### 14. Trust Wallet accounts drained (supply chain misuse), Jan 2024

Secbit has discovered that Trust Wallet did not correctly use a dependency (`trezor-crypto`), resulting in low entropy seed phrase generation. This vulnerability allowed attackers to predict private keys and drain user wallets.

The issue stemmed from improper initialization of the random number generator in the trezor-crypto library. Without sufficient entropy sources, the wallet generated predictable seed phrases that could be brute-forced much more easily than properly randomized ones.

According to security researchers, multiple victims reported losing funds, with the total damage estimated to be in the millions of dollars.

Ref: <https://secbit.io/blog/en/2024/01/19/trust-wallets-fomo3d-summer-vuln/>
Ref: <https://x.com/r_cky0/status/1859656430888026524>

### 16. @solana/web3.js attack, Dec 2024

The @solana/web3.js package, which averages over 350,000 weekly downloads on npm, has been compromised with a backdoor.
The goal is to leak private keys to a remote server.
The root causes is social engineering/phishing attack targeting the maintainers of the library.

> According to Mert Mumtaz, CEO of Helius Labs, the damage from this attack is roughly $130K.
> A fast response and detection by the Solana team was really important in making the download window of those versions to a minimum of 5 hours.

Ref: 
* <https://www.mend.io/blog/the-solana-web3-js-incident-another-wake-up-call-for-supply-chain-security/>
* <https://x.com/blockaid_/status/1864069590147277261>

More fake and malicious solana packages:
* solanacore, see <https://platform.safedep.io/community/malysis/01JGVKW3NNZFJMSX4F9JN40CNN>
* walletcore-gen, see <https://twitter.com/npm_malware/status/1876328153880342680>

### 17. Malicious NPM package web3-parser Jan 2025

Malicious infostealing package that exfiltrates secrets and data, package originally published in May of 2022, so has been around for almost 3 years! 

References:
* <https://sourcecodered.com/malicious-web3-parser-npm-package/>
* <https://github.com/advisories/GHSA-66c6-q6m3-5pmx>
* <https://security.snyk.io/vuln/SNYK-JS-WEB3PARSER-8660797>

### 18. Bybit attack / Safe Javascript compromised - Feb 2025

The AWS account of a Safe developer was first compromised, the attacked uploaded malicious Javascript targeting a single wallet. The multisig signers signed a compromised transaction involving an [exploit contract](https://etherscan.io/address/0xbdd077f651ebe7f7b3ce16fe5f2b025be2969516) called with DELEGATE_CALL. This resulted in a $1.5B (billion!) theft on the cold wallet of the Bybit crypto exchange.

Notes:
- This hack exploits a multisig cold wallet **without exploiting any smart contract vulnerability**. 
- The attacker knew that the attacked would be discovered and remediated fast, so instead of targeting multiple small wallets, they target one of the largest ever, 
- A few minutes after the attack, the attacked replaced the compromised JS file with the original one, in order to delete traces.
- The Bybit operator did blind signing. Better UX is needed, readable/interpretable transactions is high priority.
 
Overall, a perfectly executed attack.

References:
- (best wrap up): <https://research.checkpoint.com/2025/the-bybit-incident-when-research-meets-reality/>
- (official) <https://www.bybit.com/en/press/post/bybit-confirms-security-integrity-amid-safe-wallet-incident-no-compromise-in-infrastructure-blt9986889e919da8d2>

### 19. set-utils attack on Pypi (March 2025)

The Socket Research Team identified a malicious PyPI package named 'set-utils' that targets Ethereum developers by stealing private keys. Masquerading as a utility for Python sets, it imitates popular libraries like 'python-utils' and 'utils' to deceive users into installation. Once integrated, 'set-utils' intercepts Ethereum account creation processes, exfiltrating private keys by embedding them within blockchain transactions via the Polygon RPC, making detection challenging. Since its release on January 29, 2025, the package has been downloaded over 1,000 times.

Sources: 
- <https://socket.dev/blog/new-pypi-malware-exfiltrates-ethereum-private-keys>

### 20. changed-files attack, suspected to target Coinbase

On March 14, 2025, an attack on Github Action tj-actions/changed-files was detected by StepSecurity's researchers, who reported the incident to the maintainers of the tj-actions organization. Unit 42 collected evidence that Coinbase was the target, but the attack was not successful.

Sources: 

* <https://www.stepsecurity.io/blog/harden-runner-detection-tj-actions-changed-files-action-is-compromised>
* <https://unit42.paloaltonetworks.com/github-actions-supply-chain-attack/>

### 21.  semantic‑types to steal Solana keys

The threat actor embedded a covert key‑stealing payload inside the Python package semantic‑types and made five other packages (solana-keypair, solana-publickey, solana‑mev‑agent‑py, solana‑trading‑bot, and soltrade) depend on it.  Once imported, the malware monkey-patches Solana key-generation methods by modifying functions at runtime without altering the original source code. Each time a keypair is generated, the malware captures the private key. It then encrypts the key using a hardcoded RSA‑2048 public key and encodes the result in Base64. The encrypted key is embedded in a spl.memo transaction and sent to Solana Devnet, where the threat actor can retrieve and decrypt it to gain full access to the stolen wallet.

Source: <https://socket.dev/blog/monkey-patched-pypi-packages-steal-solana-private-keys>


## Hardware supply chain attacks

It is possible to tamper with hardware devices used in crypto, typically a hardware wallet. Who would do that: an employee at the company that designed the wallet, the factory that produced it, and everyone involved in shipping it. Ref: <https://vitalik.ca/general/2021/01/11/recovery.html>. Such a real hardware supply chain attack has happened on Trezor wallets (2022): <https://www.kaspersky.com/blog/fake-trezor-hardware-crypto-wallet/48155/>


