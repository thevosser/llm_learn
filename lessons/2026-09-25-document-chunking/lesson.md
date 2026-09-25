---
topic_id: document-chunking
type: concept
title: "Document Chunking: One Vector, One Idea"
hook: "Embed a whole book as one vector, and you get the blurry average of everything in it."
category: llm-mechanics
---

## The concept

An embedding model doesn't have a size limit that stops you from feeding
it an entire document at once, but doing so produces a specific problem:
one vector has to represent everything in that text at once. A document
covering five different subtopics gets squashed into a single point in
vector space that's roughly the average of all five — similar to all of
them a little, a strong match for none of them.

Chunking fixes this by splitting long source text into smaller pieces
*before* embedding, so each resulting vector represents one focused idea
instead of a blurry blend of several. A query about just one of those
five subtopics can now match tightly against the one chunk that's
actually about it, instead of weakly matching the whole document's
smeared-together vector.

The practical tradeoff is chunk size itself: too large, and you're back
to the blurry-average problem on a smaller scale. Too small, and a chunk
might not contain enough context to be useful on its own once retrieved —
a sentence fragment handed to a chat model with no surrounding context can
be less useful than a well-sized paragraph would have been.

## Try this

The same five-topic document, embedded whole versus split into
per-topic chunks:

<!-- interactive.js renders here -->

## Why it matters

This is a direct prerequisite for making RAG actually work well in
practice, not just in theory — the retrieval-augmented-generation lesson
assumed you already have well-matched chunks to retrieve; this is the
step that makes those chunks exist in the first place. Get chunking wrong
(too big, too small, or split in the wrong places) and RAG's retrieval
step degrades quietly, the same way a wrong nomic-embed-text prefix does —
no error, just retrieval that doesn't quite find the right thing.
