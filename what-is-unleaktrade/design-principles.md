---
description: The core beliefs behind UnleakTrade’s architecture.
---

# Design Principles

{% hint style="info" %}
UnleakTrade’s design is grounded in several key principles.
{% endhint %}

## Deterministic outcomes

Every RFQ reaches a final state, either a successful settlement or a well-defined exit path. There’s no ambiguity about what comes next, and no RFQ can stall indefinitely.

## Confidential competitiveness

Takers compete in a way that protects price intentions until the reveal phase, enabling fair, blind bidding without front-running or early disclosure.

## Economic accountability

Bonds (posted by maker and taker) are central to enforcing honest behavior. Obligations like revealing or settling aren’t optional:t hey carry on-chain consequences!

## Protocol fee alignment

Fees are only charged on **successful settlements**, ensuring the protocol earns revenue only when value is created.

## Simple, predictable incentives

Slashed bonds never flow to other market participants; they go **100% to the protocol treasury**, keeping incentive structures straightforward and predictable.

{% hint style="success" %}
These principles make UnleakTrade reliable, transparent, and aligned with both retail and institutional participants.
{% endhint %}
