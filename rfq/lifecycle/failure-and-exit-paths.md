---
description: How an RFQ closes when a trade does not complete.
---

# Failure & Exit Paths

{% hint style="warning" %}
Not every RFQ results in a successful trade.\
The protocol explicitly defines how an RFQ exits when progress stops or obligations are not met.
{% endhint %}

This page describes the **intentional failure paths** of an RFQ, how they occur, and what outcomes they produce.

***

## Designed for Safe Failure

Failure is not an exception in the RFQ model.

Deadlines, bonds, and explicit actions ensure that:

* RFQs never remain stuck,
* participants can always exit,
* and misbehavior or inactivity is penalized predictably.

Every failure path ends with the RFQ in a final, closed state.

***

## Expired — No Valid Market Formed

{% hint style="info" %}
An RFQ expires when no usable market ever emerges.
{% endhint %}

This happens in two situations:

* **No Commitments**
  * The commit window ends.
  * No taker committed a quote.
* **No Valid Reveals**
  * Commitments exist.
  * The reveal window ends with no valid revealed quotes.

### **Outcome**

* The maker bond is refunded.
* All faulty taker bonds are slashed.
* Slashed bonds are transferred entirely to the protocol.
* The RFQ is closed permanently.

{% hint style="success" %}
This path ensures a clean exit when there is no real liquidity.
{% endhint %}

***

## Ignored — Maker Did Not Select

An RFQ is ignored when:

* At least one valid quote was revealed,
* but the maker did not select any quote before the selection deadline.

{% hint style="info" %}
This represents a failure to act after receiving valid offers.
{% endhint %}

### **Outcome**

* The maker bond is slashed.
* Slashed bonds go entirely to the protocol.
* Takers who revealed valid quotes can later recover their own bonds.
* The RFQ is closed.

{% hint style="success" %}
This path discourages makers from requesting quotes without following through.
{% endhint %}

***

## Incomplete — Settlement Not Completed

An RFQ becomes incomplete when:

* The maker selected a quote and escrowed the base asset,
* but the selected taker did not complete settlement before the settlement deadline.

### **Outcome**

* The maker recovers the escrowed base asset.
* The maker bond is refunded.
* The selected taker bond is slashed.
* Slashed bonds go entirely to the protocol.
* The RFQ is closed.

{% hint style="success" %}
This path enforces seriousness after a counterparty has been selected.
{% endhint %}

***

## Bonds and Penalties

Across all failure paths:

* Bonds are refunded only to participants who respected their obligations.
* Bonds are slashed only when obligations are violated.
* **All slashed bonds go 100% to the protocol treasury.**
* Slashed bonds are never redistributed to counterparties.

{% hint style="success" %}
This keeps incentives simple and predictable.
{% endhint %}

***

## Closing Note

Failure and exit paths are a core part of the RFQ design.

They ensure that:

* every RFQ can be closed,
* time is never wasted indefinitely,
* and honest participants are protected.

***

With the lifecycle covered, the next sections focus on **how the system looks from each participant’s point of view**.
