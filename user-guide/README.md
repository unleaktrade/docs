---
description: Get set up with the UnleakTrade app in a couple of minutes.
---

# Getting Started

{% hint style="info" %}
The UnleakTrade app lives at [**app.unleak.trade**](https://app.unleak.trade). This guide walks you through it screen by screen.
{% endhint %}

You do not need to install anything: the app runs in your browser and reads the chain directly over the selected network's RPC — your wallet is only asked to approve signatures and transactions.

***

## Connect Your Wallet

The first screen you see is the connect gate. UnleakTrade supports every modern Solana wallet — Phantom, Solflare, Backpack, Glow, and any other wallet that follows the Wallet Standard is discovered automatically.

<figure><img src="../.gitbook/assets/user-guide/connect.png" alt="The UnleakTrade connect screen with the Select Wallet button"><figcaption>The connect gate — pick any Wallet Standard wallet.</figcaption></figure>

Press **Select Wallet**, choose your wallet from the list, and approve the connection in the wallet popup.

***

## Sign In With a Signature

Right after connecting, your wallet asks you to **sign a short message**. This is UnleakTrade's sign-in:

* it proves the wallet is really yours and unlocked,
* it is a plain message signature — **not a transaction**, so it costs nothing and moves nothing,
* it lasts for the browser tab: refreshing keeps you signed in, closing the tab signs you out.

{% hint style="success" %}
If you close the wallet popup by accident, use the **Cancel** button on the signing screen and connect again — nothing is lost.
{% endhint %}

***

## Find Your Way Around

Once signed in you land on the dashboard. The navigation bar gives you everything:

* **Marketplace** — every RFQ on the network, grouped by state.
* **My Activity** — the RFQs you posted, the quotes you made, and your rewards, in one place.
* **Transparency** — the protocol's public ledger of fees and slashed bonds.
* **Create RFQ** — the four-step wizard for posting your own request.
* **The control rail** — the guard-status pill (the liquidity guard's live health), notifications, and the network switcher.

***

## Pick Your Network

The network switcher in the navigation bar selects the Solana cluster: **Devnet** for trying things out with test tokens, **Mainnet Beta** (the switcher marks it with an amber warning; the protocol is **not live on mainnet yet**, so there is nothing to trade there today), and **Localnet** for developers running a local validator. Your choice is remembered on this device. Switching networks also signs you out: a sign-in signature from one network is never reused on another, so the app asks you to sign in again.

{% hint style="warning" %}
Everything on Devnet is play money. It is the perfect place to walk through this guide end to end.
{% endhint %}

To post an RFQ or submit a quote on Devnet you need **Unleak USDC (uUSDC)** for the bond: a test token with no real-world value, sent to the wallet you registered on the [waitlist](https://unleak.trade/waitlist) once your registration is activated. Connect that same wallet in the app.

***

## Works on Any Screen

The app is fully responsive — every flow in this guide works the same on a phone, with bottom sheets replacing popovers.

<figure><img src="../.gitbook/assets/user-guide/marketplace-mobile.png" alt="The marketplace on a phone-sized screen" width="290"><figcaption>The marketplace on a phone.</figcaption></figure>

***

👉 Continue to [**Browsing the Marketplace**](browsing-the-marketplace.md).
