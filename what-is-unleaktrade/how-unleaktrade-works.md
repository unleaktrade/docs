---
description: A conceptual (high-level) overview of the RFQ mechanism.
---

# How UnleakTrade Works?

At a high level, trading on UnleakTrade follows this flow:

1. **Maker publishes an RFQ** — aggressive trade parameters and bond posted.
2. **Takers commit blind quotes** — bonds lock to signal real intent.
3. **Takers reveal quotes** — reveal concrete price/size info.
4. **Maker selects one quote** — base asset is escrowed.
5. **Settlement completes** — selected taker executes trade; fees paid (treasury receives the fee minus any facilitator share).
6. **Or an exit path activates** — if any deadlines expire without action, the RFQ exits through a safe failure mode.

Every step is done via guided interactions with the smart contract, and all time windows and enforcement rules are deterministic.

{% hint style="success" %}
This controlled cadence ensures participants interact fairly, with clear expectations and automated settlement.
{% endhint %}
