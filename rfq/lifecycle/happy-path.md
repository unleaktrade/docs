---
description: How an RFQ successfully progresses from creation to settlement.
---

# Happy Path

This page describes the normal, successful flow of an RFQ, from the moment it is created to the moment a trade is settled.

It focuses on **what is expected to happen when all participants act correctly and on time**, without covering failure cases or exits.

***

## From Intent to Trade

An RFQ is designed to gradually move from **intent** to **commitment**.

Early phases are flexible and competitive, allowing multiple takers to participate.\
Later phases become stricter, locking decisions and capital until the trade is completed.

The happy path follows this progression step by step.

***

## Draft — RFQ Creation

The process begins when the maker creates an RFQ.

At this stage:

* The maker defines trade parameters (assets, size, constraints, deadlines).
* The RFQ is not visible to takers.
* No bonds, escrows, or fees are involved.

{% hint style="success" %}
This phase exists purely for preparation.
{% endhint %}

The RFQ only moves forward once the maker decides to open it.

***

## Open — Commit Phase

The maker opens the RFQ and makes it public.

At this point:

* The maker posts a **maker bond**.
* The commit window becomes active.
* The RFQ is visible to all takers.

During the commit phase:

* Takers may commit quotes.
* Each commitment locks a **taker bond**.
* Quotes are not revealed yet, only commitment hashes are submitted.

{% hint style="success" %}
This phase allows takers to signal interest without exposing prices.
{% endhint %}

***

## Committed — Reveal Phase

Once at least one taker has committed, the RFQ enters the reveal phase.

At this point:

* The commit phase is over.
* The reveal window becomes active.

During the reveal phase:

* Committed takers may reveal their quotes.
* Reveals must match their earlier commitments.
* The maker does not act yet.

Only revealed quotes can later be selected.

{% hint style="success" %}
This phase transforms hidden interest into real, verifiable prices.
{% endhint %}

***

## Revealed — Selection Phase

As soon as at least one valid quote has been revealed, the RFQ enters the selection phase.

At this point:

* All valid revealed quotes are available.
* The selection window becomes active.

During this phase:

* The maker reviews the revealed quotes.
* Exactly one quote can be selected.
* Takers wait for the maker’s decision.

{% hint style="info" %}
This is the decision point of the RFQ.
{% endhint %}

***

## Selected — Settlement Window

When the maker selects a quote:

* A single taker becomes the counterparty.
* The maker **escrows the base asset** into the protocol.
* A settlement window becomes active.

Important characteristics of this phase:

* The maker’s capital is now locked.
* The selected taker may complete settlement **at any time until the deadline**.

{% hint style="success" %}
This phase balances commitment (maker) with execution flexibility (taker).
{% endhint %}

***

## Settled — Trade Completion

Settlement completes when the selected taker finalizes the trade within the allowed time window.

At settlement:

* Base assets are transferred to the taker.
* Quote assets are transferred to the maker.
* Maker and taker bonds are refunded.
* Protocol fees are collected.
* Any penalties from earlier phases are finalized.

{% hint style="info" %}
The RFQ reaches its successful terminal state.
{% endhint %}

***

## Closing Note

The happy path illustrates the intended use of RFQs:

* competitive price discovery,
* explicit selection,
* and deterministic settlement.

{% hint style="warning" %}
Not every RFQ will follow this path.\
When commitments are missing, deadlines are missed, or settlement is not completed, the RFQ exits through well-defined failure paths.
{% endhint %}

👉 Continue to [**Failure & Exit Paths**](failure-and-exit-paths.md) to understand how those cases are handled.
