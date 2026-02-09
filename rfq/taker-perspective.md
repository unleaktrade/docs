---
description: How takers participate, compete, and settle RFQs.
---

# Taker Perspective

This page describes the RFQ lifecycle **from the taker’s point of view**.

It focuses on when a taker should act, what obligations are created at each step, and when capital or bonds are at risk.

***

## The Taker’s Role

As a taker, you respond to an RFQ created by a maker.

You:

* decide whether to participate,
* compete with other takers on price,
* may be selected as the counterparty,
* and complete settlement if selected.

If you work with a facilitator, you can designate them on your quote so they can claim a share of the taker fee when the trade settles. You can set or clear the quote facilitator while the RFQ is in **Draft**, **Open**, **Committed**, **Revealed**, or **Selected**.

Your actions are optional at every step, but once you act, **deadlines matter**.

***

## Evaluating an Open RFQ

When an RFQ is open:

* you can inspect its parameters,
* evaluate size, assets, and deadlines,
* decide whether it fits your strategy.

At this stage:

* you have no obligations,
* no capital is locked,
* and there is no penalty for ignoring the RFQ.

***

## Commit Phase: Signaling Interest

If you decide to participate, your first action is to **commit a quote**.

When you commit:

* you post a **bond**,
* you submit a commitment (_hash_),
* your quote **details remain private**.

{% hint style="success" %}
This action signals serious intent to participate.
{% endhint %}

From this point on:

* you are expected to reveal your quote later,
* failure to do so may result in losing your bond.

***

## Reveal Phase: Making the Quote Real

During the reveal phase:

* you may reveal your committed quote,
* the reveal must match your earlier commitment,
* your quote becomes visible to the maker.

{% hint style="warning" %}
Revealing is critical:

* only revealed quotes can be selected,
* failing to reveal puts your bond at risk.
{% endhint %}

{% hint style="info" %}
If you reveal correctly and on time, you remain eligible.
{% endhint %}

***

## Waiting for Selection

Once quotes are revealed:

* you wait for the maker’s decision,
* you do not lock any trade capital yet,
* you are not required to take any action.

{% hint style="success" %}
If your quote is **not selected**:

* you can later recover your bond,
* your participation ends without further risk.
{% endhint %}

{% hint style="info" %}
If your quote **is selected**, your role changes.
{% endhint %}

***

## Selected: Optional but Time-Bounded Execution

When your quote is selected:

* you become the sole counterparty,
* the maker escrows the base asset,
* a settlement window begins.

Important characteristics:

* your quote asset is **not escrowed**,
* you may complete settlement at **any time until the deadline**,
* you control _when_ to execute within that window.

{% hint style="warning" %}
This gives you flexibility, but not indefinitely.
{% endhint %}

***

## Completing Settlement

To complete settlement:

* you transfer the quote asset to the maker,
* the trade executes atomically,
* bonds are refunded,
* protocol fees are paid.

{% hint style="success" %}
If you complete settlement on time:

* the trade succeeds,
* your bond is returned,
* no penalties apply.
{% endhint %}

***

## Failing to Settle

{% hint style="warning" %}
If you do **not** complete settlement before the deadline:

* the RFQ closes as _incomplete_,
* your taker bond is slashed,
* the maker recovers their escrowed asset.
{% endhint %}

All penalties go to the protocol.

***

## Taker Risks and Guarantees

As a taker, you risk:

* your **bond**, if you fail to reveal,
* your **bond**, if you are selected but do not settle.

You are protected against:

* makers who never open RFQs,
* makers who never select (bond penalty applies to them),
* counterparties disappearing without consequences.

{% hint style="info" %}
Your capital is only at risk **after** you choose to act.
{% endhint %}

***

## Closing Note

From the taker’s perspective, RFQs are about timing:

* commit only when serious,
* reveal on time,
* settle when selected.

{% hint style="success" %}
Used correctly, RFQs allow you to compete for large trades with clear rules, predictable risk, and enforced outcomes.
{% endhint %}
