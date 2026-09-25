---
topic_id: nomic-embed-text-model
type: concept
title: "nomic-embed-text: A Local Model That Wants to Know Your Intent First"
hook: "Embed the same sentence two different ways, and it wants a different vector back."
category: llm-mechanics
---

## The concept

`nomic-embed-text` is a real, commonly used embedding model you can run
entirely locally through Ollama — no API key, no network call, just a
model producing the vectors from the embeddings-vs-chat lesson on your
own machine. Mechanically it does exactly what any embedding model does:
text in, fixed-length vector out.

The detail that makes it worth its own lesson is a training choice, not a
mechanical one: it was trained with **task prefixes** baked in —
`search_document: ` prepended to text you're storing for later retrieval,
`search_query: ` prepended to a question you're about to search with. The
model was trained to treat these two framings slightly differently, which
means the *same sentence* embedded once as a "document" and once as a
"query" doesn't produce the identical vector, even though nothing about
the sentence itself changed.

Skipping the prefix, or using the wrong one, doesn't crash anything — it
just quietly produces vectors that don't line up as well as they should,
which shows up as "vector search results feel a little off" rather than
an obvious error, and is exactly the kind of subtle bug prefix
requirements like this can cause if you're not aware they exist.

## Try this

Embedding the same sentence into the vector space, with two different
prefixes:

<!-- interactive.js renders here -->

## Why it matters

This is a concrete, specific example of a broader rule: an embedding
model's training determines the exact rules for using it correctly, and
those rules aren't always visible from the API surface alone — mixing up
`search_document` and `search_query` won't throw an error, it'll just
degrade retrieval quality in a way that's easy to misdiagnose as
"the vector search itself doesn't work well" when the real cause is one
missing prefix.
