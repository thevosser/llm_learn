---
topic_id: vector-search
type: concept
title: "Vector Search: Finding Meaning Instead of Matching Words"
hook: "Search for 'canine' and find documents that only ever say 'dog.'"
category: llm-mechanics
---

## The concept

Vector search is the practical payoff of everything the last two lessons
set up: embed a query into the same vector space as a collection of
stored documents, then find whichever stored vectors are closest to it by
cosine similarity. The stored documents whose vectors point in the most
similar direction to the query's vector are the "search results" — no
keyword matching involved at any point.

This is a fundamentally different search mechanism from traditional
keyword search, which looks for the literal characters you typed. Keyword
search for "canine" will not find a document that only ever uses the word
"dog" — the strings don't match, full stop. Vector search can, because
"canine" and "dog" get embedded into nearby points in the vector space
(they mean similar things), even though they don't share a single letter
in common. That's the entire value proposition: retrieval based on
meaning, not spelling.

It's also worth being honest about the tradeoff: keyword search is
exact and predictable — you know exactly why a result matched (the string
appeared). Vector search is fuzzier by design — a result can match for
reasons that aren't obvious from reading the query, which is powerful
when it works and occasionally confusing when a result seems unrelated at
first glance but scored close for a genuine semantic reason.

## Try this

The same query, run as keyword search versus vector search, against a
document that never uses the literal query word:

<!-- interactive.js renders here -->

## Why it matters

This is the retrieval mechanism that makes RAG possible at all — "find
relevant text, then hand it to a chat model" only works because vector
search can locate relevant text that doesn't share vocabulary with the
question. It's also exactly why the "structured lookup vs. vector search"
distinction later in this set matters: this power to match on meaning is
wasted, and sometimes actively wrong, for a question that has one single
correct literal answer sitting in a database field somewhere.
