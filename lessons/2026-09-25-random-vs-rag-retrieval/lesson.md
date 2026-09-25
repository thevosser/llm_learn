---
topic_id: random-vs-rag-retrieval
type: concept
title: "Random Selection vs. RAG Retrieval: Relevance Costs Variety"
hook: "The most relevant example isn't always the most interesting choice."
category: llm-mechanics
---

## The concept

Once you have a library of stored examples (posts, shapes, past
responses), there are two structurally different ways to pick which ones
to use: pull one at random, or retrieve the ones semantically closest to
the current situation via RAG. It's tempting to assume "closest match" is
strictly better, but the tradeoff runs in both directions.

Random selection is simple, requires no embeddings or search
infrastructure at all, and has a real property RAG retrieval doesn't:
it preserves variety. A system that always retrieves the single closest
match to a recurring situation will tend to surface the same handful of
examples over and over — technically the most relevant choice every
time, but repetitive and predictable in a way that can flatten out
whatever made the content interesting in the first place.

RAG retrieval trades that variety away deliberately, in exchange for
semantic relevance: it costs real infrastructure (embeddings, a vector
search step) and it narrows the space of what gets chosen down to
"whatever's most similar," which is exactly the right tradeoff when
relevance matters more than variety — and exactly the wrong one when the
whole point was unpredictability or drift.

## Try this

Picking which "shape" (a rhetorical template) to use for a bot's next
post, two ways:

<!-- interactive.js renders here -->

## Why it matters

This isn't a case where one approach is simply better — it's a real
design decision with a real cost either way, worth making deliberately
rather than defaulting to RAG just because it's the more sophisticated-
sounding option. A system generating varied, surprising content (like a
"shapes" library meant to keep bot behavior from feeling repetitive) may
specifically want random selection's variety over RAG's relevance.
