---
description: >-
  What every instruction costs on-chain, who pays it, and what you get back —
  for makers, takers, and facilitators.
---

# The Cost of UnleakTrade

{% hint style="info" %}
Every action in an RFQ is a Solana instruction. This page breaks down what each one costs, which on-chain accounts it creates, and which of those costs come back to you.
{% endhint %}

[**Bonds & Fees**](bonds-and-fees.md) explains *why* the economics exist and when bonds are refunded or slashed. This page looks at the same lifecycle from the wallet's point of view: instruction by instruction, account by account.

***

## The Three Kinds of Cost

Everything you ever pay falls into one of three buckets:

* **Bonds** — refundable USDC guarantees. Locked while you have an open obligation, returned in full when you honor it. Bonds are never a payment; see [**Bonds & Fees**](bonds-and-fees.md) for the refund and slashing rules.
* **The protocol fee** — the only non-refundable protocol charge. Denominated in the RFQ's quote token, paid by the selected taker, and charged **only on successful settlement**. It is paid **on top of** the quote amount, so the maker always receives the full quoted amount.
* **Network costs** — what Solana itself charges: a transaction fee per signature (currently 5,000 lamports, about 0.000005 SOL), plus a **rent-exempt deposit** for every new on-chain account an instruction creates. The deposit is proportional to the account's size and goes to no one — it simply sits in the account, and it is returned only if that account is later closed.

{% hint style="warning" %}
Most protocol accounts are **permanent by design** — they form the auditable history of every RFQ. Their rent deposits (a few thousandths of a SOL each) are therefore locked for good. The exceptions are called out below.
{% endhint %}

The SOL figures below assume Solana's current rent parameters and are rounded; the byte sizes are exact, taken from the on-chain program.

***

## What You Pay as a Maker

### Creating a draft — `init_rfq`

* **Creates:** the RFQ account (496 bytes, ≈ 0.0043 SOL deposit) and the RFQ's USDC bonds escrow, a token account (≈ 0.002 SOL deposit). You pay both, plus one transaction fee.
* **Token movements:** none. Your bond is *not* posted at draft time.
* **Comes back?** Cancelling the draft (`cancel_rfq`) closes the RFQ account and refunds its deposit to you. The escrow token account stays open, so its smaller deposit does not return.

### Publishing — `open_rfq`

* **Creates:** the RFQ's slashed-bonds tracker (123 bytes, ≈ 0.0017 SOL deposit), the permanent record used by the [Transparency ledger](../user-guide/transparency.md).
* **Token movements:** your **maker bond is locked** — `bond_amount` USDC moves from your wallet into the bonds escrow.
* **Worth knowing:** the RFQ carries a single `bond_amount`. The same value you post as maker is what every committing taker must post too — you are setting the skin-in-the-game for both sides.

### Editing and routing — `update_rfq`, `set_rfq_facilitator`

* **Transaction fee only.** No accounts are created and no tokens move. `update_rfq` works while the RFQ is a draft; the facilitator can be set or cleared up to the moment a quote is selected.

### Selecting a quote — `select_quote`

* **Creates:** the Settlement account (520 bytes, ≈ 0.0045 SOL deposit), the base-token vault owned by the RFQ, and your own quote-token account if you do not have one yet (≈ 0.002 SOL each). You pay all of these.
* **Token movements:** your **base amount is escrowed** — the full `base_amount` moves into the RFQ's vault, ready to be delivered the moment the taker funds.

### Exits — `cancel_rfq`, `close_expired`, `close_incomplete`

* **`cancel_rfq`** (draft only): closes the RFQ account and **refunds its rent deposit to you**. Nothing else to unwind — no bond was posted.
* **`close_expired`** (no valid reveals): refunds your full bond from the escrow. Bonds of takers who committed but never revealed are transferred to the protocol treasury in the same transaction.
* **`close_incomplete`** (selected taker never funded): refunds your full bond **and** your escrowed base amount, closes the Settlement account (**its deposit comes back to you**), and slashes the unrevealed takers' bonds plus the selected taker's bond to the treasury.

{% hint style="info" %}
`close_expired` and `close_incomplete` may also create the treasury's USDC token account if it does not exist yet — a one-time ≈ 0.002 SOL deposit paid by whoever triggers it first.
{% endhint %}

***

## What You Pay as a Taker

### Committing — `commit_quote`

* **Creates:** your Quote account (278 bytes, ≈ 0.0028 SOL deposit) and a commit guard (49 bytes, ≈ 0.0012 SOL deposit) — a small permanent account keyed by your commit hash that makes every commitment unique and unreplayable.
* **Token movements:** your **taker bond is locked** — the RFQ's `bond_amount` in USDC moves from your wallet into the bonds escrow.
* **Worth knowing:** the transaction also carries a built-in ed25519 signature-verification instruction for the liquidity-guard attestation. It rides in the same transaction, and its signature counts toward the transaction fee like any other — so committing pays for two signatures (about 0.00001 SOL) instead of one.

### Revealing and routing — `reveal_quote`, `set_quote_facilitator`

* **Transaction fee only.** Revealing recomputes your commitment hash on-chain and publishes your quoted amount; nothing is created and no tokens move.

### Funding the trade — `complete_settlement`

This is the instruction where the real value moves, and the only place the protocol fee is charged.

* **You need in your wallet:** the **quote amount plus the total fee**, in the quote token. The fee is paid on top — the maker receives the full quote amount, undiminished.
* **Creates:** the RFQ's fees tracker (153 bytes, ≈ 0.002 SOL deposit — the permanent fee record shown in Transparency), plus any missing token accounts along the way: your base-token account, the treasury's quote-token account, and the RFQ's fee escrow. You pay these one-time deposits.
* **Token movements, all in one transaction:**
  * the full quote amount goes to the maker,
  * the treasury's share of the fee goes to the treasury,
  * any facilitator share moves into the RFQ's fee escrow, reserved for the facilitator to claim,
  * the maker's base amount is released from the vault **to you**,
  * **both bonds are refunded** — yours and the maker's,
  * bonds of takers who never revealed are slashed to the treasury.

### Reclaiming your bond — `refund_quote_bonds`

* If you revealed honestly but were not selected, this returns your **full bond** once the funding window has passed. Transaction fee only (plus, rarely, the one-time treasury token-account deposit noted above).
* Your Quote account itself stays on-chain as part of the RFQ's history; its deposit is not returned.

***

## What You Pay as a Facilitator

Being named as a facilitator costs nothing — the maker sets the RFQ-level address and the taker sets the quote-level address, each paying only their own transaction fee.

### Claiming — `withdraw_reward`

* **Creates:** your reward tracker (121 bytes, ≈ 0.0017 SOL deposit), the permanent record of the claim, and your quote-token account if you do not have one yet.
* **Token movements:** your share moves from the RFQ's fee escrow into your wallet.
* **Worth knowing:** the claim only succeeds when the RFQ and the winning quote name the **same** facilitator address and the computed share is greater than zero. On very small fees the share can round down to zero — in that case there is nothing to claim, so skip the transaction.

***

## The Fee, Worked Through

The protocol fee is set by the maker as `taker_fee_bps`, in basis points of the settled quote amount (10,000 bps = 100%, capped at 10,000):

* **Total fee** = quote amount × `taker_fee_bps` ÷ 10,000, rounded down — but never less than 1 unit when the rate is non-zero.
* **Facilitator share** = total fee × `facilitator_fee_bps` ÷ 10,000, rounded down. The rate is snapshotted from the protocol config when the RFQ is created — **1000 bps (10%)** by default.
* **Treasury share** = total fee − facilitator share.

A concrete example, with a 500,000 USDC quote and a 50 bps fee:

* total fee = 500,000 × 50 ÷ 10,000 = **2,500 USDC**, paid by the taker on top of the quote,
* facilitator share (at the default 10%) = **250 USDC**, held in escrow until claimed,
* treasury share = **2,250 USDC**,
* the taker funds **502,500 USDC** in total; the maker receives the full **500,000 USDC**.

{% hint style="success" %}
If the RFQ fails — expired, ignored, or incomplete — **no fee is charged at all**. Only bond penalties apply, and those never exceed the bonds themselves.
{% endhint %}

***

## Accounts & Rent at a Glance

Who pays each deposit, and whether it ever comes back:

* **RFQ** (496 bytes) — paid by the maker at `init_rfq`. Refunded only if the draft is cancelled; permanent once published.
* **Bonds escrow & vaults** (token accounts, ≈ 0.002 SOL each) — paid by whoever first needs them; never closed.
* **Slashed-bonds tracker** (123 bytes) — paid by the maker at `open_rfq`; permanent.
* **Quote** (278 bytes) and **commit guard** (49 bytes) — paid by the taker at `commit_quote`; permanent.
* **Settlement** (520 bytes) — paid by the maker at `select_quote`. Refunded to the maker if the trade closes incomplete; permanent after a successful settlement.
* **Fees tracker** (153 bytes) — paid by the taker at `complete_settlement`; permanent.
* **Reward tracker** (121 bytes) — paid by the facilitator at `withdraw_reward`; permanent.

{% hint style="info" %}
The permanence is deliberate: these accounts are what the [Transparency](../user-guide/transparency.md) view and any outside auditor read. A few thousandths of a SOL buys a tamper-proof public record of every trade.
{% endhint %}

***

## Cost Summary

* If you behave, your only true costs are **network costs** — and, for the winning taker, the **protocol fee**.
* Bonds always come back to honest participants, on success *and* on failure.
* The maker never pays the protocol fee; it is charged to the selected taker, on top of the quote.
* Rent deposits are small, one-time, and mostly permanent — the price of a complete on-chain audit trail.

👉 For when bonds are refunded versus slashed, continue to [**Bonds & Fees**](bonds-and-fees.md). For what happens economically on each failure path, see [**Failure & Exit Paths**](lifecycle/failure-and-exit-paths.md).
