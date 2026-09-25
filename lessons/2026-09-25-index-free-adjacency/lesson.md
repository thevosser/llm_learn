---
topic_id: index-free-adjacency
type: concept
title: "Index-Free Adjacency: The Trick Behind Fast Graph Traversal"
hook: "A pointer to the next node beats looking up where the next node is, every single hop."
category: data-storage
---

## The concept

Index-free adjacency is the specific storage-engine technique that makes
graph database traversal fast, and the underlying idea is genuinely
simple: each node stores direct physical pointers to its connected nodes,
so moving from one node to an adjacent one is just following a pointer —
no lookup, no index search, no query planning required to find "what's
connected to this."

Contrast that with a relational join, which conceptually has to look up
matching rows via an index (or a full scan) at *every single hop* — even
a well-optimized index lookup is still a lookup, an operation with its own
cost, repeated once per hop. Index-free adjacency skips that lookup
entirely: the connection isn't found, it's already sitting right there as
a direct reference, the moment you're standing on the node.

If this sounds familiar from a completely different context: it's
conceptually the same idea as following a `next` pointer in a C linked
list — direct address in hand, no searching required to get to the next
element — just made persistent (saved to disk, not just in memory),
safe under concurrent access from multiple queries at once, and wrapped
in a real query language instead of raw pointer arithmetic.

## Try this

Moving from one node to the next, with and without index-free adjacency:

<!-- interactive.js renders here -->

## Why it matters

This is the mechanical reason graph traversal cost scales so much more
gently with hop count than the relational-join alternative from the
graph-databases lesson — it isn't a query-optimizer trick or clever
caching, it's a fundamentally different, cheaper physical operation
(follow a pointer) standing in for a fundamentally more expensive one
(look something up) at every single step of the traversal.
