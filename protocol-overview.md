---
description: How UnleakTrade coordinates OTC trades on-chain.
---

# Protocol Overview

{% hint style="info" %}
UnleakTrade is an on-chain protocol for negotiating and settling OTC trades through **structured, time-bounded workflows**.
{% endhint %}

Instead of relying on off-chain negotiation or trusted intermediaries, the protocol defines a deterministic process where:

* prices are discovered competitively,
* commitments are enforced economically,
* and every interaction ends in a clear outcome.

This page describes **how the protocol is structured**, independently of any specific RFQ flow.

***

## What the Protocol Actually Does

At its core, UnleakTrade does three things:

1. **Coordinates price discovery**
2. **Enforces commitments and deadlines**
3. **Finalizes settlement or exits deterministically**

{% hint style="info" %}
All three happen fully on-chain.
{% endhint %}

The protocol does **not**:

* match orders automatically,
* optimize execution prices,
* or arbitrate disputes.

It enforces a process, nothing more, nothing less.

***

## Core Protocol Responsibilities

### Coordination

The protocol defines _who can act, when, and how_.

It:

* structures interactions into explicit phases,
* restricts actions based on time and state,
* prevents participants from skipping steps.

{% hint style="success" %}
This coordination layer is what replaces brokers, chats, and manual OTC workflows.
{% endhint %}

### Enforcement

The protocol enforces behavior using **bonds and deadlines**.

It ensures that:

* committed quotes must be revealed,
* valid quotes must be acted upon,
* selected trades must be completed on time.

{% hint style="warning" %}
**Violations are penalized automatically.**

There is no discretion and no negotiation.
{% endhint %}

### Finalization

Every protocol interaction reaches a terminal state.

For RFQs, this means:

* either the trade settles successfully,
* or the RFQ exits through a defined failure path.

In both cases:

* funds are redistributed deterministically,
* bonds are either refunded or slashed,
* the protocol state is closed.

{% hint style="info" %}
Nothing remains pending indefinitely.
{% endhint %}

***

## Protocol Components (Concrete View)

UnleakTrade is composed of a small number of tightly scoped components.

### RFQ Engine

The RFQ engine defines:

* the lifecycle of an RFQ,
* its states and deadlines,
* and the rules governing maker and taker actions.

RFQs are the **primary interface** through which users interact with the protocol.

### Escrow & Settlement Logic

The protocol controls escrow only when strictly necessary.

Specifically:

* the maker’s asset is escrowed **after quote selection**,
* no quote-asset escrow exists,
* settlement is finalized explicitly by the selected taker.

{% hint style="info" %}
This minimizes locked capital while preserving settlement guarantees.
{% endhint %}

### Economic Layer

The economic layer enforces behavior through:

* maker bonds,
* taker bonds,
* and protocol fees.

Key properties:

* bonds are refundable guarantees, not payments,
* slashed bonds always go **100% to the protocol**,
* fees are charged **only on successful settlement**.

{% hint style="info" %}
This keeps incentives simple and predictable.
{% endhint %}

## Participants and Authority

The protocol recognizes three roles:

* **Makers**, who initiate negotiations and select quotes
* **Takers**, who compete by submitting and revealing quotes
* **The protocol**, which enforces rules and outcomes

No role has special authority:

* makers cannot bypass deadlines,
* takers cannot avoid penalties,
* the protocol cannot override rules.

{% hint style="info" %}
Authority is entirely rule-based.
{% endhint %}
