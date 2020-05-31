# Tsunami Wallet

* This is a fork of Samourai Wallet - Add credit goes to the original developers for a great model to work off *

Tsunami wallet aims to provide enhanced privacy on Ethereum. The main objectives are to improve privacy in an adversarial environment.
The end goal is to enable someone to create a transaction with no possible link with the origin, even from highly sophisticated adversaries.

The main leaks of privacy it aims to improve upon are:
- IP address & timing lookup linkability
- Address linkability


### IP address linkability

Ethereum does not have a feasible SPV mode available at this time. Mobile users hoping to connect to the Ethereum network are required to do so though a node provider.
This node provider will have access to a few key datapoints the user:
1. The IP address of the user
2. The addresses & contracts the user is interested in

To prevent IP address leaks, all network connections through Tsunami Wallet are through TOR. This provides one level of privacy, in that the IP address of the user is never disclosed to the node operator.

The next problem is timing analysis. If a node operator sees a Tor IP looking up the balance of 3 different addresses at almost the same time, they could make the assumption that the three addresses may be linked in some way.

It is for this reason that Tsunami wallet has two distict wallets. A regular ethereum wallet, and a "private" ethereum wallet.

Care needs to be taken to not request balances of either wallet at the same time.

### Address privacy
For address link-ability, ZK proofs are used, and attempts are make to prevent the user from accidentally making transactions that can leak privacy.
Initially, the Aztec protocol was used, but until Aztec 2.0 is launched, it is not feasible for address privacy.
The current version uses Tornado.cash for address privacy. Tornado.cash only allows for fixed deposit amounts.

The main method that a user can link a Tornado deposit to a Tornado withdrawal are:
1. Sending a transaction outside Tornado from the deposit address to the withdrawal address (or vice versa)
2. Depositing a specific amount and withdrawing the exact same amount to the withdrawal address
3. Depositing and withdrawing at almost the same time

Tsunami wallet has features in place to try to block users from making these mistakes. This means:
1. Tsunami wallet will never let you directly transfer from your private addresses to your non-private address
2. Tsunami wallet uses multiple withdrawal addresses for private balances, as opposed to a single address
3. It enforces a randomized time before it allows you to redeem a Tornado.cash note

Tornado Cash notes are encrypted using the wallets private key and saved to the devices local storage.
Eventually, they will be backed up somewhere. As it stands, if the user un-installs the wallet, all notes will be lost.

### Build:

Import as Android Studio project. Should build "as is". PGP signed tagged releases correspond to builds that were issued via Google Play.


### License:

[Unlicense](https://github.com/Samourai-Wallet/samourai-wallet-android/blob/master/LICENSE)

