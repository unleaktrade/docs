---
description: >-
  Introduces the RFQ concept, core actors, and design principles. This page
  gives you the mental model needed to understand everything else.
---

# Overview

## What is an RFQ?

An RFQ (Request For Quote) is an on-chain workflow that allows a **maker** to request liquidity and multiple **takers** to compete by submitting quotes.

Instead of trading immediately, the RFQ introduces a **structured negotiation**:

* takers first commit interest without revealing prices,
* then reveal concrete quotes,
* then the maker selects one quote,
* and finally the trade can be settled.

This structure enables competitive pricing while keeping the process fully enforceable on-chain.

***

## Why RFQs?

RFQs are designed for situations where:

* trade sizes are large,
* price discovery matters,
* immediate execution is not ideal,
* and participants need protection against non-cooperative behavior.

By combining **time windows**, **explicit actions**, and **bond-based incentives**, the RFQ ensures that:

* participants act honestly,
* inactivity is penalized,
* and every RFQ eventually reaches a final state.

***

## Core Actors

### Maker

The maker is the party requesting liquidity.

The maker:

* defines the RFQ parameters,
* opens the RFQ and posts a bond,
* selects a quote if valid offers exist,
* escrows the base asset once a quote is selected.

The maker controls _when_ the RFQ is opened and _which_ quote is selected, but is constrained by deadlines.

### Taker

A taker is a party responding to an RFQ.

A taker:

* commits a quote by posting a bond,
* reveals the quote later,
* may be selected as counterparty,
* completes settlement if selected.

Multiple takers can participate in the same RFQ, but only one can be selected.

### Facilitator

A facilitator is an optional party that helps connect makers and takers.\
They can assist with sourcing liquidity, routing interest, or coordinating off-chain relationships around an RFQ.

Facilitators do not control RFQ state transitions or outcomes.

On-chain, facilitators can be designated:

* by the maker at the RFQ level, and
* by a taker on a specific quote.

If the selected quote’s facilitator matches the RFQ’s facilitator, the facilitator can claim a share of the taker fee after settlement.

### Protocol

The protocol enforces the rules of the RFQ.

It:

* enforces deadlines (TTLs),
* holds bonds and escrows,
* executes settlement,
* collects protocol fees,
* receives all slashed bonds.

The protocol does not arbitrate or decide outcomes — it only enforces them.

***

## States and Phases (High-Level)

An RFQ progresses through a series of **states**, each representing a **phase** of the workflow:

* Draft
* Open (commit window)
* Committed (reveal window)
* Revealed (selection window)
* Selected (settlement window)
* Settled, or a failure state

An RFQ **never changes state automatically**.\
It only progresses when a user performs a valid action at the right time.

Deadlines define _when actions are allowed_, not _when they happen_.

***

## Terms (Quick Definitions)

* **Bond**: a refundable guarantee that is only lost when obligations are violated.
* **Fee**: a non-refundable payment charged only on successful settlement.
* **TTL (time-to-live)**: a defined time window for each phase; once it expires, certain actions are no longer valid.

***

## Bonds and Incentives (High-Level)

RFQs rely on bonds to enforce correct behavior:

* The maker posts a **maker bond** when opening an RFQ.
* Each taker posts a **taker bond** when committing a quote.

Bonds are:

* refunded when obligations are respected,
* slashed when obligations are violated.

{% hint style="info" %}
**Important invariant:**\
All slashed bonds go **100% to the protocol treasury**.\
They are never redistributed to counterparties.

This keeps incentives simple and predictable.
{% endhint %}

***

## How to Read This Documentation

This documentation is organized progressively:

1. **Lifecycle pages** explain _what happens_ to an RFQ over time.
2. **Perspective pages** explain _what matters_ depending on whether you are a maker or a taker.
3. Economic rules are described conceptually, without implementation details.

You do not need to understand the underlying program to follow the logic — the focus is on behavior, incentives, and outcomes.

***

## What’s Next?

The next section explains the RFQ lifecycle itself:

* how phases follow one another,
* how deadlines structure the flow,
* and how an RFQ reaches a final state.

👉 Continue to [**RFQ Lifecycle**](lifecycle/README.md).
