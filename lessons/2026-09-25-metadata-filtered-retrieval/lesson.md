---
topic_id: metadata-filtered-retrieval
type: concept
title: "Metadata-Filtered Retrieval: Vector Search Inside a Fence"
hook: "Search by meaning, but only within the documents you're actually allowed to be searching."
category: llm-mechanics
---

## The concept

Plain vector search finds the closest matches across an entire
collection of stored vectors, with no concept of which ones should even
be eligible in the first place. Metadata-filtered retrieval adds an
ordinary SQL-style filter — `WHERE doc_type = 'invoice'`,
`WHERE bot_id = 42` — evaluated *alongside* the vector similarity search,
so results have to satisfy both conditions: closest by meaning, *and*
inside the right subset.

This matters because "closest by meaning across everything" is often not
the actual question being asked. A support system with both internal
engineering docs and public help-center articles embedded in the same
table doesn't want a customer's question pulling from internal docs just
because they happened to score as semantically close — the metadata
filter (`doc_type = 'public'`) needs to exclude those candidates before
similarity ranking ever gets to decide between what's left.

Combining both in one query (rather than filtering in application code
after the fact) also matters for correctness at the edges: filtering
after retrieval means you might retrieve the top 5 matches, then discard
3 of them for failing the filter, and end up with only 2 real results —
filtering as part of the same query avoids ever wasting a retrieval slot
on a candidate that was never eligible to begin with.

## Try this

The same query, run as vector search alone versus vector search combined
with a metadata filter:

<!-- interactive.js renders here -->

## Why it matters

This is exactly the mechanism behind the facebots-style "bot voice"
retrieval use case: filtering to one specific `bot_id`'s past posts
*before* ranking by similarity to the current situation, so a bot's
generated posts and reactions only ever draw on that one bot's own voice,
never a different bot's, no matter how semantically similar another bot's
post might otherwise score.
