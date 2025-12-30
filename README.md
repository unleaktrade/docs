---
description: Structured on-chain price discovery for negotiated trades
---

# RFQ

RFQs (Requests For Quote) provide a controlled way to discover prices and execute large or sensitive trades on-chain.\
Instead of trading immediately, participants follow a time-bounded workflow that enforces commitments, selection, and settlement.

This section documents how RFQs work, how participants interact with them, and how the protocol enforces correct behavior.

***

### How to Navigate This Section

The RFQ documentation is organized to move from **concepts** to **actions**, and from **system behavior** to **participant perspective**.

You can read it top-down, or jump directly to the section most relevant to you.

#### Start here if you are new

* **Overview** explains what an RFQ is and why it exists.
* **Lifecycle** introduces the phases and states at a high level.

#### Go deeper if you use RFQs

* **Happy Path** shows how a trade successfully completes.
* **Failure & Exit Paths** explains how RFQs close when things go wrong.

#### Focus on your role

* **Maker Perspective** explains obligations and risks for RFQ creators.
* **Taker Perspective** explains timing and incentives for liquidity providers.

***

### What RFQs Are Designed For

RFQs are particularly useful when:

* trade sizes are large,
* liquidity is fragmented,
* price discovery matters more than speed,
* participants want clear rules and enforcement.

The protocol ensures that every RFQ:

* progresses through explicit phases,
* can always be closed,
* and ends in a deterministic final state.
