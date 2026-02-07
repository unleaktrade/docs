---
description: How facilitators connect counterparties and earn rewards.
---

# Facilitator Perspective

This page describes the RFQ lifecycle **from the facilitator’s point of view**.

A facilitator is an optional party that helps connect makers and takers. They may source liquidity, route interest, or coordinate off-chain relationships around an RFQ.

Facilitators do not control RFQ state or outcomes. Their on-chain impact is limited to being designated and, if matched, claiming a share of the taker fee after settlement.

***

## When a Facilitator Is Set

A facilitator can be designated in two places:

* **RFQ-level** (set by the maker).
* **Quote-level** (set by the taker when committing a quote, or updated later).

The facilitator is eligible for a reward **only if**:

* the RFQ specifies a facilitator address, and
* the selected quote specifies the **same** facilitator address.

***

## What You Do (And Don’t Do)

As a facilitator, you may:

* introduce takers to an RFQ or help makers attract interest,
* coordinate off-chain communications,
* agree on commercial terms outside the protocol.

You do **not**:

* open, select, or settle RFQs,
* bypass deadlines,
* change protocol outcomes.

***

## How Rewards Work

On successful settlement:

* the taker pays a fixed fee,
* the treasury receives the fee minus any facilitator share,
* the facilitator share is retained in the RFQ vault.

You claim the share by calling `withdraw_reward` **after settlement**. Claims are only valid if the RFQ and the selected quote both point to your address.

By default, the facilitator fee is **1000 bps (10%)** of the taker fee unless configured otherwise.

***

## Timing and Restrictions

Facilitator updates follow RFQ state rules:

* The maker can set or clear the RFQ facilitator while the RFQ is in **Draft**, **Open**, **Committed**, or **Revealed**.
* A taker can set or clear the quote facilitator while the RFQ is in **Draft**, **Open**, **Committed**, **Revealed**, or **Selected**.

Once settlement completes, the facilitator is fixed and only reward claims remain.
