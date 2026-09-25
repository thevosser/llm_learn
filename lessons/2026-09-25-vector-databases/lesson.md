---
topic_id: vector-databases
type: concept
title: "Vector Databases: When Exact Search Gets Too Slow"
hook: "sqlite-vec checks every vector. A dedicated vector database learns to skip most of them."
category: data-storage
---

## The concept

`sqlite-vec` computes vector search by comparing the query against every
stored vector — an exact, linear scan. For a few thousand vectors that's
essentially instant. As the collection grows into the millions, checking
every single one on every query stops being fast enough, no matter how
efficient the underlying comparison is, simply because there are that
many comparisons to make.

Dedicated vector databases (pgvector, Qdrant, and others) solve this with
approximate-nearest-neighbor indexing — commonly an algorithm called HNSW
(Hierarchical Navigable Small World). Instead of comparing against every
vector, HNSW builds a graph-like structure over the stored vectors ahead
of time that lets a search jump straight toward the likely neighborhood of
the best matches and skip the vast majority of vectors entirely. The
tradeoff is right in the name: *approximate* — it's no longer guaranteed
to find the mathematically exact closest match, just a very good one,
in exchange for being dramatically faster at scale.

This is the same fixed-price-vs-metered-shaped tradeoff that keeps
showing up throughout this project: exact and simple (sqlite-vec) versus
faster-but-approximate-and-more-complex (a dedicated vector database) —
and the right choice depends entirely on how large the collection actually
gets, not on which one sounds more sophisticated.

## Try this

Searching a collection of stored vectors for the nearest match, at small
and at large scale:

<!-- interactive.js renders here -->

## Why it matters

This is exactly the sqlite-vec lesson's own tradeoff one level further:
sqlite-vec was already the simpler choice over hand-rolled application-
code comparison; a dedicated vector database is the next simpler-to-
faster tradeoff step up, worth taking only once the collection has
actually grown large enough that exact linear scan is the bottleneck —
not by default, and not preemptively.
