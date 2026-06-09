---
title: 'Microservices: More Than Just Code'
description: 'What microservices really solve, what they break, and why they are as much a people problem as a technical one.'
pubDate: 'Jul 02 2025'
---

Microservices are everywhere and often misunderstood. This post explores what they
really solve, what they often break, and why they're as much a people problem as a
technical one. I'll also share how I approached service design in OpenOrderFlow, an
event-driven backend system built from the ground up.

Ask a team why they moved to microservices, and you'll hear things like:

> "Decoupling."
>
> "Independent deployability."
>
> "Scale."

Ask them again six months later, and the tone usually shifts:

> "Too many dependencies."
>
> "Hard to trace bugs across services."
>
> "No one knows who owns what."

Microservices aren't a shortcut to better architecture. They're a choice — one that
trades some problems for others. In OpenOrderFlow, I tried to explore this tradeoff
intentionally.

## What is OpenOrderFlow? (short version)

OpenOrderFlow is an event-driven backend system modeled after platforms like Swiggy
or Uber Eats, but built generically, so that any kind of business (restaurants,
retail, services) could plug in, offer items, and fulfill customer orders.

It's built with Kafka, Spring Boot, PostgreSQL, Redis, Docker, and more. But the real
focus is on architecture, boundaries, and autonomy — not just tech.

It's not a monolith split into pieces. It's a system designed around ownership and flow.

## Microservices in OpenOrderFlow

Each domain in OpenOrderFlow — Orders, Inventory, Customer, Business, Partner,
Delivery, Notification, Payment — is its own service, with its own databases (yes, one
DB per core-domain), logic, and Kafka event contracts.

There's no "shared auth service" or "platform utility dump." Every service is built to
own its domain, its truth, and its consequences.

## What Microservices Actually Solve

At their best, microservices offer:

- Smaller, easier-to-reason codebases
- Independent deployments
- Isolated failures
- Independent scalability
- Clearer ownership over models and logic

In OpenOrderFlow, for example, only the InventoryService needs to know about inventory
logic.

If an order comes in, the OrderService emits an event — it doesn't reach across a
network call to ask for permission.

That's the point: services should expose decisions, not internals.

## What Microservices Break (or at Least Complicate)

Microservices also create their own gravity:

- Ownership becomes ambiguous without design discipline
- Debugging is harder — tracing a single request becomes a distributed puzzle
- Schema evolution, deployment sequencing, contract testing — all get trickier
- Teams drift into accidental monoliths if boundaries aren't respected

Honestly, OpenOrderFlow would've been simpler as a monolith. But that's not what I
wanted to explore. I wanted the friction. I wanted to feel the problems architecture is
supposed to solve.

## The Socio-Technical Truth

This is the part we don't talk about enough.

Microservices aren't just about services — they're about people. They reflect how teams
are structured, how decisions are made, and how responsibilities are divided.

If a service is a boundary in code, it should also be a boundary in ownership,
communication, and accountability.

Without that alignment, your system is just a distributed illusion of control.

Conway's Law isn't theoretical. If two teams can't talk clearly, their services won't
either.

In OpenOrderFlow, I had the unusual freedom to act as all the teams. It reminded me how
architecture isn't just tech design — it's social design.

## What They Unlock (Technically)

When done well, microservices also unlock real technical wins:

- Faster iteration and releases
- Safe, incremental deployments
- Scaling hot paths independently
- Language and stack flexibility (if you can handle the ops)
- Isolation of faults — no more platform-wide outages from one null pointer

But those wins are only possible if you're intentional — about design, communication,
and trust.

## My Approach in OpenOrderFlow

- Services are organized around real business domains: orders, inventory, business,
  customer, delivery
- Kafka is used for async flows — like inventory validation, partner assignment, and
  delivery status
- REST is used only where sync is unavoidable — e.g., customer authentication
- Events are modeled explicitly — not just JSON blobs thrown over a wall
- No shared logic, no vague "core services" — every service owns its models and its
  contracts

## EDA: A World of Its Own

Underneath all this is another layer — Event-Driven Architecture.

It's not just about using Kafka. It's about thinking in terms of events, flows, state,
and reactions instead of just requests and responses and also handling idempotency,
states of the system designed as a Finite State Machine, modeling event schemas and a
lot more.

OpenOrderFlow is deeply rooted in that mindset — but that's a topic too big to squeeze
in here. Maybe, I'll write about that separately.

## Conclusion

Building OpenOrderFlow wasn't about proving that microservices are good or bad. It was
about asking the harder questions:

> Who owns what?
>
> Where do decisions live?
>
> What does this system look like when it's 10x bigger and 3x messier?

Microservices don't automatically give you better architecture. But if you design with
care — and accept the cost — they can give you something more valuable: a system that
mirrors your thinking, not your tech debt.
