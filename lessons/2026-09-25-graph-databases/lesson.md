---
topic_id: graph-databases
type: concept
title: "Graph Databases: Relationships as First-Class Citizens"
hook: "Instead of re-deriving a connection every time, a graph database just... has it."
category: data-storage
---

## The concept

A graph database stores data as nodes (things) and edges (relationships
between things) where the edges are stored directly, as real pointers
from one record to another — not derived at query time by matching keys
across tables the way a relational join works. A "follows" or
"purchased" relationship isn't a foreign key column to be joined on; it's
a stored, traversable connection sitting right there in the data.

This directly targets the exact weak spot from the relational-databases
lesson: multi-hop, connectivity-shaped questions. "Which customers are
connected to customer X through a chain of shared purchases, three steps
removed" stops requiring three chained joins and becomes a graph
traversal instead — follow the stored edges outward from X, three hops,
and see what's reachable. The cost of one more hop in a graph traversal
tends to stay far more manageable than the cost of one more join in a
relational query, specifically because the connections are already there
to follow rather than needing to be re-derived from scratch each time.

The tradeoff runs the other way for exactly the questions relational
databases excel at: set-based aggregation across many independent
records ("total sales last month") isn't naturally what a
relationship-traversal engine is optimized for. Graph databases are a
different shape, not a strictly better one.

## Try this

The same "friends of friends of friends" question, run as relational
joins versus graph traversal:

<!-- interactive.js renders here -->

## Why it matters

This sets up the next two lessons directly: index-free adjacency is the
storage-engine trick that makes graph traversal fast in the first place,
and relational algebra vs. graph query languages is about how differently
these two shapes get *expressed* as queries, not just how they're stored.
