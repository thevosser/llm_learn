---
topic_id: relational-algebra-vs-graph-query-languages
type: concept
title: "Relational Algebra vs. Graph Query Languages: Two Ways to Ask About Connections"
hook: "SQL derives a relationship through a join. Cypher just says 'follow this path.'"
category: data-storage
---

## The concept

Underneath every relational database is relational algebra: data modeled
as independent sets of tuples (rows), with relationships between them
expressed only at query time, via operations like join that match rows
across tables based on shared key values. A relationship in this model
isn't a thing that's stored — it's a thing that gets *derived*, freshly,
by the join operation, every time a query asks for it.

Graph query languages (Cypher, and the newer standardized GQL) start from
a different premise entirely: structural pattern-matching and
variable-length paths are treated as native, first-class parts of the
query language itself, not something built up from more primitive
set operations. A Cypher query can express "find a path of any length
from A to B following 'follows' edges" directly, as a single readable
pattern — the equivalent relational-algebra expression would require an
unbounded, awkward chain of joins that can't even be written cleanly for
an unknown number of hops in standard SQL.

This is the query-language expression of the same graph-vs-relational
split from earlier lessons, one level up: it's not just that graph
databases *store* connections more directly (index-free adjacency) — the
*language* you use to ask about those connections is built around paths
and patterns as a native concept, rather than simulating them through
repeated joins.

## Try this

The same "any-length path between two people" question, expressed in
each paradigm:

<!-- interactive.js renders here -->

## Why it matters

This closes the loop across the whole database-storage set: graph
databases store relationships differently (index-free adjacency), scale
differently on multi-hop questions (graph-databases lesson), and are
*asked about* differently at the query-language level too. All three are
the same underlying difference in how relationships are treated — derived
at query time versus native and first-class — showing up at three
different layers of the system.
