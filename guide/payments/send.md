---
layout: guide
title: Sending bitcoin
description: An introduction to how sending bitcoin works.
nav_order: 2
parent: Payments
permalink: /guide/payments/send/
main_classes: -no-top-padding
# image: /assets/images/guide/payments/send/header.svg
---

# Sending bitcoin

Sending bitcoin can be a very straightforward or complex flow in a Bitcoin application. People may be sending bitcoin to a known contact, moving it between their wallets on different devices, or making a purchase through a [payment processor](https://bitcoin.design/guide/getting-started/software/#payment-processors).

Let us look at the main transaction options senders need to configure when moving bitcoin:

- **Amount** — How much to send
- **Recipient address** — Where to send the bitcoin
- **Coin selection** — Which coins/inputs to use (optional)
- **Fee settings** — Prioritize fast confirmation or low cost (optional)

You do not need to follow the order below. Feel free to tailor the configuration's order for the payment to what best serves your users. For example, you may make users set the amount before they enter the address.

## Get the recipient address

<div class="center" markdown="1">
{% include image.html
   image = "/assets/images/guide/payments/send/get-recipient-address.svg"
   alt-text = "Graphic showing chat messages between the sender and receiver. The sender sends a bitcoin address and the receiver agrees to pay."
   width = 400
   height = 400
   layout = "float-right-desktop"
%}

To send a payment on the Bitcoin blockchain, the sender needs to obtain an address from the recipient. Since Bitcoin [addresses](https://bitcoin.design/guide/glossary/#address) are long and seemingly random, they are best shared by copying and pasting in plain text, as a [payment link](https://bitcoin.design/guide/foundations/wallet-interoperability/#payment-links), or as a scannable [QR Code](https://bitcoin.design/guide/foundations/wallet-interoperability/#qr-codes).

The receiver does this by generating a new address in their wallet application, then sharing it with the sender. If the sender and receiver are physically close to each other, scanning the receiver's address as a QR Code will be easy. Still, if they are not, they can send the address as text in any regular communication tool like email, SMS, etc.
</div>

## Inputting an address

<div class="center" markdown="1">
{% include image.html
   image = "/assets/images/guide/payments/send/input-address.svg"
   alt-text = "Address input field prompting the sender to paste the address"
   width = 400
   height = 400
   layout = "float-right-desktop"
%}

Once you have gotten the address, its time to enter the payment details. Bitcoin transactions are irreversible, so both the sender and receiver should take great care in correctly sharing and inputting addresses.

**QR Code** -- Access will need to be granted to your application to enable scanning of QR Codes. Once the camera detects a valid address in the QR Code, it should automatically fill the address field.

**Copy Paste** -- When the sender receives the address or payment link as text, your application can detect a valid address in the clipboard and prompt the sender to press a button to paste it.

</div>

**Do's**

- Indicate clearly if the address is valid or not
- Show the full address if possible to help the sender visually verify it is correct
- If space is a constraint, truncate the address in the middle so that both the beginning and end are visible

**Don'ts**

- Prevent the transaction to be sent if the address is invalid

## Inputing an amount

<div class="center" markdown="1">
{% include image.html
   image = "/assets/images/guide/payments/send/input-amount.svg"
   alt-text = "Amount input field with bitcoin, local currency and selections for fractions of the total wallet balance"
   width = 400
   height = 400
   layout = "float-right-desktop"
%}

Unless the sender needs to transfer a specific amount of bitcoin, they should have the ability to switch between other currencies when inputting the amount. It is common practice to provide bitcoin, satoshi, and the sender's preferred fiat currency as options.

Applications sometimes also allow the sender to select fractions of their total available balance by providing a "max" or "use full balance" button. These fractions can be handy when the sender needs to make transfers from their hot wallet to a more secure hardware wallet.
</div>

**Do's**

- Allow senders to switch which denomination they are inputting the amount with
- State the total balance available (subtracting the required fee)
- Allow selecting max amount or fractions for easier fund management
- Payment links and QR Codes can contain an amount. When they do, your application should populate the amount field automatically
- Indicate if an amount entered is more than the available balance

## Transaction fee

<div class="center" markdown="1">
{% include image.html
   image = "/assets/images/guide/payments/send/select-fee-rate.svg"
   alt-text = "Fee selection component with high, medium, low urgency options"
   width = 400
   height = 400
   layout = "float-right-desktop"
%}

The application can automatically estimate a fee and set it for the sender. This would typically prioritize the transaction to be included in a block as soon as possible. Since the fee rate may vary if the network is busy, you can give senders more fine-grained fee controls so they can choose to optimize for faster confirmation or lower fees.

When allowing the sender to set fees, it is essential to communicate the estimated cost in their preferred currency and the estimated time until first confirmation. Be mindful that the way Bitcoin fees get calculated may not map to the sender's traditional financial experience. If you allow adjustment of fees, consider providing details on how it gets calculated.

Human error with fee selection can lead to costly mistakes, and fee estimations are imperfect. Carefully consider if and how you expose transaction fees to senders.
</div>

**Variations**
- Automatically set the fee-rate
- Allow sender to choose from presets
- Allow sender to enter a custom fee rate (advanced)

**Do's**

- If the sender does not have advanced knowledge about bitcoin fees but wants control over the fee-rate, provide presets to select how urgent the transaction is (e.g. low, medium, high priority)
- When using presets clearly communicate estimated confirmation time and costs related to each of the fee rate options
- When allowing users to enter their own fee rate warn the sender if they enter an amount far beyond the recommended fee-rate for the next block

## Reviewing and approving the payment

<div class="center" markdown="1">
{% include image.html
   image = "/assets/images/guide/payments/send/review-payment.svg"
   alt-text = "Approval screen with details of the transaction and confirmation button"
   width = 400
   height = 400
   layout = "float-right-desktop"
%}

A valid transaction that is broadcasted to the network cannot be reversed, so it is critical that the sender is given a chance to double check the payment details (amount, recipient address, total fee, etc) before submitting the transaction.

If your application allows setting spending limits, and the current transaction exceeds it, make sure they go through some security check (biometric, enter PIN, 2FA password, etc). This technique can also be employed if the transaction is attempting to use the max wallet balance.
</div>

**Do's**

- Allow the sender to review payment details like address, amount, and fees and adjust if necessary before submitting the transaction
- Show the amount being sent and the fee information in both bitcoin and the senders preferred currency

## Transaction processing and confirmation

{% include image.html
   image = "https://i.imgur.com/idV0Mt7.png"
   retina = "https://i.imgur.com/idV0Mt7.png"
   alt-text = "Notifications after the transaction is broadcasted"
   width = 1600
   height = 800
%}

Once the transaction is valid, it is now in the memory pool and is available for including in a block by miners. When in the memory pool, the sender can see the wallet's transaction as unconfirmed or pending.

After broadcasting a transaction, the process of propagation and validation is quite fast, so showing these states may be infeasible. You may inform the sender that their transaction is pending a confirmation, the estimated time to confirm given the current fee market, and once it has gotten its first confirmation.

**Do's**
- Clearly indicate the state of the outgoing transaction
- Show the amount of confirmations the transaction has
- Provide information on transaction/block ID for receipt purposes

**Don'ts**
- Show the transaction as confirmed until it has received ***at least*** one confirmation, but preferably six