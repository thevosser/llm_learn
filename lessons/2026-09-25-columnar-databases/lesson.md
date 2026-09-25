---
topic_id: columnar-databases
type: concept
title: "Columnar Databases: Built to Scan, Not to Fetch"
hook: "Getting one full record fast and summing one column across a billion rows fast are different engineering problems."
category: data-storage
---

## The concept

A row-oriented database (the relational shape covered earlier) stores
each record's fields together, physically adjacent on disk — grab
customer #4821, and every field of that one record (name, email,
signup date, balance) comes back together in one read. That's exactly
right for "fetch this one specific record," which is the overwhelmingly
common operation in transactional systems.

A columnar database flips that layout: it stores all values for one
column together, across every row, rather than grouping by record. Ask
for the average order value across ten million orders, and a columnar
store only has to read the one `order_value` column's worth of data —
it never has to load names, emails, or shipping addresses it doesn't
need, because those live in entirely separate physical blocks it can
simply skip. A row store answering the same aggregation question has to
read every full record just to get at the one field it actually needs
from each.

This is a genuine tradeoff, not a strict upgrade: fetching one complete
record back out of a columnar store means reassembling it from many
separate column blocks, which is slower than a row store's single
contiguous read. Row stores win at "get me this one record." Column
stores win at "summarize this one field across everything." This is
exactly the OLTP-vs-OLAP split (transactional workloads vs. analytical
ones) that shapes a lot of real database architecture decisions.

## Try this

Two operations against the same order data — fetch one order, and
average order value across ten million orders:

<!-- interactive.js renders here -->

## Why it matters

Recognizing which shape a workload actually is — lots of single-record
lookups (row store territory) versus aggregating one or two fields across
huge numbers of records (column store territory) — is the actual decision,
the same way it was for graph vs. relational. Neither one is "the good
database"; each is built for a specific access pattern.
