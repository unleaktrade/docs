---
description: A simple way to reason about how UnleakTrade works.
---

# Mental Model

{% hint style="info" %}
This page provides a **mental model** for understanding UnleakTrade.
{% endhint %}

Instead of describing instructions or states, it explains the protocol as a sequence of **conceptual locks**, **decisions**, and **guarantees**.\
If you keep this model in mind, every RFQ flow will feel intuitive.

***

## Think in Layers, Not Transactions

UnleakTrade is best understood as **layers of commitment**, not as individual transactions.

Each layer:

* restricts what participants can do,
* increases the cost of inaction,
* and reduces optionality over time.

The protocol moves from _flexibility_ to _finality_.

***

## Layer 1 - Intent (No Risk)

At the beginning, everything is optional:

* The maker defines an RFQ.
* Takers decide whether they care.
* No funds are locked.
* No penalties exist.

Nothing meaningful can go wrong here.

**Mental shortcut:**

> _This layer exists to express intent, not commitment._

***

## Layer 2 - Interest (Bonded, Still Private)

When the RFQ opens:

* The maker posts a bond.
* Takers commit quotes by posting bonds.
* Prices are still hidden.

At this stage:

* participants are signaling seriousness,
* but not revealing strategy,
* and not committing trade capital.

**Mental shortcut:**

> _Bonds replace trust, privacy replaces exposure._

***

## Layer 3 - Information (Reveal Is Mandatory)

Once the reveal phase begins:

* Quotes must become real.
* Hidden intent turns into concrete information.
* Non-reveals are penalized.

From here on:

* doing nothing has consequences,
* but capital is still not locked.

**Mental shortcut:**

> _If you spoke up, you must now speak clearly._

***

## Layer 4 - Decision (Irreversibility Begins)

When valid quotes exist:

* the maker must either select or accept a penalty,
* exactly one quote can be chosen.

This is the first **irreversible decision**:

* choosing commits the maker,
* not choosing is punished.

**Mental shortcut:**

> _Silence (no-show) is no longer acceptable._

***

## Layer 5 - Capital Lock (Asymmetric Commitment)

After selection:

* the maker escrows the base asset,
* the taker escrows nothing yet,
* the taker gets a time window to execute.

This asymmetry is intentional:

* the maker shows full intent,
* the taker gets execution flexibility,
* deadlines prevent abuse.

**Mental shortcut:**

> _One side commits capital, the other commits time._

***

## Layer 6 - Finalization (Only Two Outcomes)

From here, there are only two possible endings:

### Settlement

* the taker executes in time,
* assets are exchanged,
* bonds are refunded,
* fees are paid.

### Exit

* a deadline is missed,
* penalties apply,
* capital is returned or seized,
* the RFQ is closed.

There is no third option.

**Mental shortcut:**

> _Everything ends, and it ends cleanly._

***

## How Bonds Fit the Model

{% hint style="info" %}
Bonds are not payments.\
They are **pressure points**.
{% endhint %}

Each bond answers a question:

* _Will you reveal if you commit?_
* _Will you select if quotes exist?_
* _Will you settle if selected?_

{% hint style="success" %}
If the answer is “yes”, the bond comes back.
{% endhint %}

{% hint style="warning" %}
If the answer is “no”, the bond is gone.
{% endhint %}

All slashed bonds go to the protocol, never to counterparties.

***

## One Sentence Summary

If you remember only one thing:

> **UnleakTrade gradually replaces optionality with obligation, and obligation with finality — using time and bonds.**

Everything else is just mechanics.

***

## How to Use This Page

* Read this page once.
* Keep it in mind while reading RFQ States.
* Come back when a flow feels complex.

It is the conceptual backbone of the protocol.
