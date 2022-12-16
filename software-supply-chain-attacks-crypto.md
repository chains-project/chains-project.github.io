# Software supply chain attacks on crypto infrastructure

In this article, we discus attacks on cryptocurrency and digital asset infrastructures.
We focus on software supply chain attacks.
We first list high-profile attacks that have been made public and the discuss possible mitigations.

Authors: Martin Monperrus \& the [CHAINS team](https://chains.proj.kth.se/)


## Attacks

(Work in progress)

### Attack via Maintainer change

`event-stream` npm package by Dominic Tarr was compromised because of a maintainer change.
Dominic Tarr stopped maintaing the repository long before the attack. The bad actor reached out
to the developer in 2018 to help him out. However, he added **malicious code to steal bitcoins**
from application and then released the malicious `event-stream` on npm. See
https://github.com/dominictarr/event-stream/issues/116 for more details.

### DyDx attack through NPM

The NPM account of DyDx was compromised: <https://www.mend.io/resources/blog/popular-cryptocurrency-exchange-dydx-has-had-its-npm-account-hacked/>

## Sushiswap attack

"On Friday, September 17 2021, Miso suffered a supply chain exploit, whereupon the fund wallet address was fixed"
<https://blog.sonatype.com/3-million-cryptocurrency-heist-malicious-github-commit?hsLang=en-us>

## Onus attack through Log4J

"The attackers were able to make off with the data before an update patching the Log4j vulnerability was available and demanded $5 million in ransom for the stolen information. [...] The attackers waited until 25 December 2021 for payment from ONUS, and when they did not receive the ransom, the attackers put the information of close to 2 million customers up for sale"
<https://redskyalliance.org/xindustry/vietnamese-crypto-trading-platform-hit-with-log4j>

## Cryptomining through compromised docker images

"The Sysdig Threat Research Team (TRT) ... surfaced more than 1,600 malicious Docker images containing cryptominers, backdoors, and other nasty malware disguised as legitimate popular software."
<https://www.darkreading.com/attacks-breaches/container-supply-chain-attacks-cashing-in-on-cryptojacking>
[Detecting cryptomining attacks “in the wild”](https://sysdig.com/blog/detecting-cryptomining-attacks-in-the-wild/)

## Ledger NaNoX

"A single connection controlled by the non-secure processor allows it to reset the display. Hence, malicious code running on the non-secure processor can turn off the display even while it’s running on battery only. This might be leveraged as part of an elaborate social engineering attack where the infected Ledger Nano X shuts off its display while malware on a computer convinces the user to press a series of buttons to approve a malicious transaction (e.g., “Your Ledger Nano X stopped responding, please hold both buttons to restart the device”).

 <https://blog.kraken.com/post/5590/kraken-security-labs-supply-chain-attacks-against-ledger-nano-x/>
 
## End-user transaction attack through Pypi typosquatting

Typosquatting to monitor the clipboard for crypto addresses.

"A malicious package was slipped into Pypi. "Called “Colourama,” the package looked similar to Colorama, which is one of the top-20 most-downloaded legitimate modules in the Python repository. The doppelgänger Colourama package contained most of the legitimate functions of the legitimate module, with one significant difference: Colourama added code that, when run on Windows servers, installed a Visual Basic script to constantly monitors the server’s clipboard for signs a user is about to make a cryptocurrency payment."
<https://arstechnica.com/information-technology/2018/10/two-new-supply-chain-attacks-come-to-light-in-less-than-a-week/>

## Copay attack through event-stream

"The flatmap-stream library was modified to leak private keys (basically, cryptowallet passwords) from applications relying both on event-stream and copay-dash libraries."
[A bad link in the cryptochain](https://www.kaspersky.com/blog/copay-supply-chain-attack/24786/)
[Widely used open source software contained bitcoin-stealing backdoor](https://arstechnica.com/information-technology/2018/11/hacker-backdoors-widely-used-open-source-software-to-steal-bitcoin/)


## Hardware wallets

"If you buy a hardware wallet, you are trusting a number of actors that were involved in producing it - the company that designed the wallet, the factory that produced it, and everyone involved in shipping it who could have replaced it with a fake. Hardware wallets are potentially a magnet for such attacks: the ratio of funds stolen to number of devices compromised is very high."
Vitalik Buterin, <https://vitalik.ca/general/2021/01/11/recovery.html>
