---
description: How makers create, control, and complete RFQs.
---

# Maker Perspective

This page describes the RFQ lifecycle **from the maker’s point of view**.

It focuses on the decisions a maker makes, when the maker becomes committed, and what risks the maker takes at each stage.

***

## The Maker’s Role

{% hint style="info" %}
As a maker, you initiate the RFQ.
{% endhint %}

You control:

* when the RFQ is opened,
* which quote is selected,
* whether the trade moves forward.

At the same time, the protocol enforces **deadlines and commitments** that prevent the RFQ from stalling indefinitely.

***

## Before Opening: Full Flexibility

Before opening the RFQ:

* you define all trade parameters,
* you can revise or cancel freely,
* no capital is locked.

{% hint style="success" %}
There is no risk at this stage.\
Nothing happens until you decide to open the RFQ.
{% endhint %}

***

## Opening the RFQ: First Commitment

When you open the RFQ:

* you post a **bond**,
* the RFQ becomes visible to takers,
* the commit window starts.

{% hint style="warning" %}
At this point:

* you can no longer cancel freely,
* you are signaling serious intent to trade,
* but you have not yet committed any trade capital.
{% endhint %}

Your role during this phase is passive: you wait for takers to respond.

***

## Commit & Reveal Phases: Observing the Market

During the commit and reveal phases:

* takers express interest and then reveal concrete quotes,
* you cannot yet select a counterparty,
* you do not lock any trade assets.

Your only responsibility is to remain attentive to the process.

{% hint style="info" %}
If no valid market forms, the RFQ can close without penalty to you.
{% endhint %}

***

## Selection: The Key Decision

Once valid quotes are revealed, you enter the most important phase.

{% hint style="info" %}
As the maker:

* you must decide whether to select a quote,
* exactly one quote can be selected,
* selection must happen before the deadline.
{% endhint %}

{% hint style="warning" %}
If you **do not select a quote in time**:

* the RFQ is closed as _ignored_,
* your **bond is slashed**,
* the penalty goes to the protocol.
{% endhint %}

{% hint style="success" %}
**Selection is therefore a real obligation**, not a suggestion.
{% endhint %}

***

## After Selection: Capital Commitment

When you select a quote:

* you escrow the **base asset** into the protocol,
* your trade intent becomes irreversible.

From this moment:

* your capital is locked,
* you cannot change counterparties,
* you must wait for the selected taker to complete settlement.

{% hint style="info" %}
This is the strongest commitment you make as a maker.
{% endhint %}

***

## Waiting for Settlement

After selection:

* the taker has until the settlement deadline to complete the trade,
* you cannot force early execution,
* you are protected by deadlines and penalties.

If settlement completes in time:

* the trade is executed,
* your bond is refunded.

If settlement does **not** complete:

* your escrowed base asset is returned,
* your bond is refunded,
* the taker is penalized.

***

## Maker Risks and Guarantees

As a maker, your risks are tightly scoped:

You risk:

* your **bond**, if you fail to select a quote after valid reveals,
* temporary illiquidity of your base asset after selection.

You are protected against:

* takers who do not reveal,
* takers who do not settle,
* RFQs getting stuck indefinitely.

{% hint style="info" %}
All penalties are enforced automatically by the protocol.
{% endhint %}

***

## Closing Note

From the maker’s perspective, an RFQ is a controlled commitment process:

* flexible at the start,
* decisive at selection,
* protected through settlement.

Understanding when you become committed - and when you are still free - is key to using RFQs effectively.

👉 Continue to [**Taker Perspective**](taker-perspective.md) to see how the same lifecycle looks from the other side of the trade.
