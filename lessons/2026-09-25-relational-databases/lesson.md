---
topic_id: relational-databases
type: concept
title: "Relational Databases: Great at Records, Strained by Deep Relationships"
hook: "Rows and tables handle 'what's this record' beautifully. 'How is everything connected' is a different question."
category: data-storage
---

## The concept

A relational database stores data as rows in tables — a customers table,
an orders table, a products table — with relationships between them
expressed through shared keys (an order row references a customer's ID)
rather than stored as direct links. This shape is extremely good at
exactly what it was designed for: transactional data (recording an order,
updating a balance, reliably surviving concurrent writes) and set-based
aggregation (SQL's whole design is asking questions like "total sales
per region last month" across large sets of rows at once).

The strain shows up specifically on deep-relationship questions. "Which
customers bought from the same supplier as customer X" requires a join.
"Which customers are connected to customer X through a chain of shared
purchases, two or three steps removed" requires multiple joins, and each
additional hop in the relationship chain means another join, with cost
that tends to grow steeply as the chain gets longer — because relational
databases derive relationships at query time via matching keys, rather
than storing the connection itself as something directly traversable.

Concurrency is the other practical limit worth naming plainly: SQLite in
particular allows only a single writer at a time, which is completely
fine for a project with the kind of load this site has, and a real
constraint the moment multiple processes need to write simultaneously.

## Try this

The same two questions — "total orders this month" and "customers
connected to X three purchases removed" — against the same relational
schema:

<!-- interactive.js renders here -->

## Why it matters

This sets up exactly why graph databases exist as a separate category,
covered next: they aren't a strictly "better" database, they're a
different shape built specifically for the multi-hop question relational
databases handle by stacking joins. Recognizing which of your questions
falls into which category is the actual database-choice skill — not
picking one technology to use for everything.
