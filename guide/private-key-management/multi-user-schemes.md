---
layout: guide
title: Shared
nav_order: 3
parent: Private key management
permalink: /guide/private-key-management/multi-user-schemes/
main_classes: -no-top-padding
---

{% include picture.html
   image = "/assets/images/guide/private-key-management/shared.jpg"
   retina = "/assets/images/guide/private-key-management/shared@2x.jpg"
   mobile = "/assets/images/guide/private-key-management/shared-mobile.jpg"
   mobileRetina = "/assets/images/guide/private-key-management/shared-mobile@2x.jpg"
   alt-text = "Shared schemes header illustration"
   width = 1600
   height = 600
   layout = "full-width"
%}

# Shared schemes

While multi-key setups can be used for personal use, if several people need to share funds multiple keys become a necessity. You will often see this referred to as *multi-sig* setups, stemming from the fact that multiple keys need to sign a transaction for it to be valid.

The use-cases for shared schemes include spouses managing a joint account, groups, organizations or companies managing their funds, as well as inheritance planning. It can also be used for governance of an organization, with transactions used not to transfer funds but to record, or vote, for decisions. 

## Multi-key

As we saw with multi-key setups for personal use, a multi-key wallet has several controlling keypairs attached, so called co-signers. The number of keys and required co-signers will depend on the use case. With spouses sharing a *joint account*, a simple 1-of-2 multi-key setup might suffice, meaning there are two keys but only one is required to sign for a transaction to be valid. At the other end of a spectrum a company might require a more complex 3-of-5 setup, requiring three of the five co-signers to approve any transaction. 

Just like with personal schemes, external signing devices can be used to hold one or several of the keys used for a shared multi-key setup. While this can increase security if managed correctly, the same caveat applies in terms of adding significant complexity. 

{% include image.html
   image = "/assets/images/guide/private-key-management/schemes/shared-multi-key.jpg"
   retina = "/assets/images/guide/private-key-management/schemes/shared-multi-key@2x.jpg"
   alt-text = "Shared multi-key illustration"
   caption = "Several users can control the wallet with a combination of the keys."
   width = 800
   height = 400
%}

#### Pros 
- Allows several people to access and control a bitcoin wallet
- Can tailor requirements for multiple co-signers and access
- High security, if setup well

#### Cons 
- Has significant complexity and op-sec burden for multiple private keys, each of which might need a good manual backup scheme

### How it works 
A software wallet-application or coordination software initiates a multi-sig wallet, choosing the number of total keys, and the number required to sign transactions. One user then adds private keys from other users' wallets generated elsewhere to the multisig, after which the software wallet can complete the creation process. For any future transaction from the multi-sig wallet the required amount of co-signers need to sign (using Partially Signed Bitcoin Transactions - PSBT from [BIP174]({{ 'https://github.com/bitcoin/bips/blob/master/bip-0174.mediawiki'}})) before any transaction is valid.

### Best practice

**When to use** 
- When funds need to be accessed by several people or an organization
- When users are likely to be very knowledgeable or be guided through setup and use

**When not to use** 
- (No other option currently for shared access scenarios)

**Variations** 
- The number of required co-signers and attached keypairs
- Key storage devices

**Do's** 
- Make sure the multi-key setup itself is backed up properly, including x-pubs for all the participating keys, fingerprint and derivation.

**Products that use this scheme** 
Few tailor-made products exist for shared wallets, but any wallet-application that supports multi-key setups can be used to initiate a shared wallet. 
- [Revault](https://revault.dev) - in development
- [Electrum](https://electrum.org)
- [Bluewallet](https://bluewallet.io)
- [Specter](https://specter.solutions)
- [Armory](https://btcarmory.com)
- [Guarda](https://guarda.com)

---

Next up, common [principles]({{ '/guide/private-key-management/principles/' | relative_url }}) we should strive to follow.