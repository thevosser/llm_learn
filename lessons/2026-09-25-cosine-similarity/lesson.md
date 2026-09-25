---
topic_id: cosine-similarity
type: concept
title: "Cosine Similarity: Comparing Direction, Not Distance"
hook: "Two vectors can point almost the same way and still have wildly different lengths."
category: llm-mechanics
---

## The concept

Once two pieces of text are embedded as vectors, "how similar are they"
becomes a math question: how do you compare two lists of numbers?
Cosine similarity answers it by looking at the *angle* between the two
vectors, not their length. Two vectors pointing in nearly the same
direction score close to 1 (very similar) regardless of whether one is
much longer than the other; two vectors pointing in unrelated directions
score close to 0, and opposite directions score close to -1.

The "ignores magnitude" part is the whole point, not an accident. A short
sentence and a long paragraph about the exact same idea will typically
produce vectors of different lengths (magnitude often correlates loosely
with text length or word frequency effects) — if similarity were measured
by raw distance between the vectors' endpoints, that length difference
alone would make them look less similar than they actually are, purely
for reasons that have nothing to do with meaning. Measuring the angle
instead sidesteps that entirely: what matters is which direction the
vector points, not how far out it reaches.

This is why cosine similarity, not raw Euclidean distance, is the default
comparison for embeddings in nearly every practical system — it matches
what embeddings are actually meant to represent (a direction encoding
meaning) rather than treating vector length as if it carried information
it usually doesn't.

## Try this

Two pairs of vectors — compare what happens when magnitude differs versus
when direction differs:

<!-- interactive.js renders here -->

## Why it matters

This is the concrete mechanism underneath every "how similar are these
two things" step in vector search, RAG retrieval, and metadata-filtered
retrieval — all of them are, underneath, running this same angle
comparison. Understanding that it's measuring direction, not raw
distance, also explains why embedding a one-word query against a
paragraph-length document isn't automatically a mismatch just because
their lengths differ wildly.
