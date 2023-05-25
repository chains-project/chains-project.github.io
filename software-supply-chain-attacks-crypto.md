# Software supply chain attacks on crypto

In this article, we discus attacks on cryptocurrency and digital asset infrastructures and focus on software supply chain attacks.
We first list high-profile attacks that have been made public and the discuss possible mitigations.

Authors: Martin Monperrus & the [CHAINS team](https://chains.proj.kth.se/)  
Creation date: Nov 30 2022  
Status: keeps being updated over time  
Ref URL: <https://chains.proj.kth.se/software-supply-chain-attacks-crypto.html>  

## Attacks

### event-stream attack (Maintainer change), 2018

`event-stream` npm package by Dominic Tarr was compromised because of a maintainer change.
Dominic Tarr stopped maintaining the repository long before the attack. The bad actor reached out
to the developer in 2018 to help him out. However, he added **malicious code to steal bitcoins**
from application and then released the malicious `event-stream` on npm. See
[issue](https://github.com/dominictarr/event-stream/issues/116) for more details. References:

* [A bad link in the cryptochain](https://www.kaspersky.com/blog/copay-supply-chain-attack/24786/)
* [Widely used open source software contained bitcoin-stealing backdoor](https://arstechnica.com/information-technology/2018/11/hacker-backdoors-widely-used-open-source-software-to-steal-bitcoin/)

### Colourama attack (typosquatting), 2018

End-user transaction attack through Pypi typosquatting by monitoring the clipboard for crypto addresses.

"A malicious package was slipped into Pypi. "Called “Colourama,” the package looked similar to Colorama, which is one of the top-20 most-downloaded legitimate modules in the Python repository. The doppelgänger Colourama package contained most of the legitimate functions of the legitimate module, with one significant difference: Colourama added code that, when run on Windows servers, installed a Visual Basic script to constantly monitors the server’s clipboard for signs a user is about to make a cryptocurrency payment."
<https://arstechnica.com/information-technology/2018/10/two-new-supply-chain-attacks-come-to-light-in-less-than-a-week/>

### Hardware wallet Ledger NaNoX, 2020

"A single connection controlled by the non-secure processor allows it to reset the display. Hence, malicious code running on the non-secure processor can turn off the display even while it’s running on battery only. This might be leveraged as part of an elaborate social engineering attack where the infected Ledger Nano X shuts off its display while malware on a computer convinces the user to press a series of buttons to approve a malicious transaction (e.g., “Your Ledger Nano X stopped responding, please hold both buttons to restart the device”).

### Sushiswap attack (weakly protected repo), 2021

"On Friday, September 17 2021, Miso suffered a supply chain exploit, whereupon the fund wallet address was fixed"
<https://blog.sonatype.com/3-million-cryptocurrency-heist-malicious-github-commit?hsLang=en-us>

### Onus attack (through Log4J), 2021

"The attackers were able to make off with the data before an update patching the Log4j vulnerability was available and demanded $5 million in ransom for the stolen information. [...] The attackers waited until 25 December 2021 for payment from ONUS, and when they did not receive the ransom, the attackers put the information of close to 2 million customers up for sale"
<https://redskyalliance.org/xindustry/vietnamese-crypto-trading-platform-hit-with-log4j>

### Cryptomining attack (compromised docker images), 2022

"The Sysdig Threat Research Team (TRT) ... surfaced more than 1,600 malicious Docker images containing cryptominers, backdoors, and other nasty malware disguised as legitimate popular software."

* [Container Supply Chain Attacks Cash In on Cryptojacking](https://www.darkreading.com/attacks-breaches/container-supply-chain-attacks-cashing-in-on-cryptojacking)
* [Detecting cryptomining attacks “in the wild”](https://sysdig.com/blog/detecting-cryptomining-attacks-in-the-wild/)

 <https://blog.kraken.com/post/5590/kraken-security-labs-supply-chain-attacks-against-ledger-nano-x/>
 
### DyDx attack (NPM account compromised), 2022

The NPM account of DyDx was compromised: <https://www.mend.io/resources/blog/popular-cryptocurrency-exchange-dydx-has-had-its-npm-account-hacked/>

### Crypto Wallet Address Replacement Attacks, 2023
"At around 17:49 UTC on 9 February 2023, Phylum’s automated risk detection platform began alerting us to a long series of suspicious publications which appear to be a revived attempt to deliver the same crypto wallet clipboard replacing malware. This time, however, the attacker changed the obfuscation technique and radically increased the volume of attacks."
<https://blog.phylum.io/phylum-discovers-revived-crypto-wallet-address-replacement-attack>

### 3CX attack (installer compromised), 2023

The hackers compromised a Windows installer and targeted a few, very specific compagnies in the cryptocurrency business. Not clear how they managed to infect the installer file.

* [The Massive 3CX Supply-Chain Hack Targeted Cryptocurrency Firms (Wired)](https://www.wired.com/story/3cx-supply-chain-attack-north-korea-cryptocurrency-targets/)
* [Not just an infostealer: Gopuram backdoor deployed through 3CX supply chain attack (Kaspersky)](https://securelist.com/gopuram-backdoor-deployed-through-3cx-supply-chain-attack/109344/)
 
## Discussion

### Hardware wallet attacks

* Tamper with the device:
  * who: an employee at the company that designed the wallet, the factory that produced it, and everyone involved in shipping it Ref! <https://vitalik.ca/general/2021/01/11/recovery.html>
  * Real hardware supply chain attack on Trezor wallets (2022): <https://www.kaspersky.com/blog/fake-trezor-hardware-crypto-wallet/48155/>

* Mitigations:
  * "To mitigate fake devices and evil-maid attacks, we sign a public key generated on the secure chip of each device during the factory setup using our own private key. The BitBoxApp verifies the challenge is signed by a certified attestation key When you connect the BitBox02 to the host device, the BitBoxApp automatically checks that it is connected to an authentic device produced and programmed by Shift Crypto with a challenge-response mechanism. The BitBoxApp sends the BitBox02 a challenge (random number) that needs to be signed by the attestation key on the device."  [How we mitigate supply chain attacks](https://shiftcrypto.ch/blog/supply-chain-attacks/)
  * Use old hardware you already have at home, such as a GameBoy, see <https://blockworks.co/news/gameboy-cold-wallet>



[Edit this page](https://github.com/chains-project/chains-project.github.io/edit/main/software-supply-chain-attacks-crypto.md)
