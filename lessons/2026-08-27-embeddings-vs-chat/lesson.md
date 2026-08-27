---
topic_id: embeddings-vs-chat
type: concept
title: "Embeddings vs. Chat Models: Two Different Jobs"
hook: "One of these models answers you. The other just tells you what's similar to what."
category: llm-mechanics
---

## The concept

"LLM" gets used as one catch-all term, but the models behind a chatbot and
the models behind a search box are usually doing genuinely different jobs.

A **chat model** (GPT-4-class, Claude, etc.) takes in text and predicts the
next token, over and over, to generate new text. Its output is more text —
an answer, a summary, a poem. It's built to converse.

An **embedding model** takes in text and outputs a fixed-length list of
numbers — a vector, often a few hundred to a few thousand dimensions long.
That vector doesn't "mean" anything on its own. What matters is distance:
text with similar meaning produces vectors that land close together in
that space, and unrelated text produces vectors that land far apart. An
embedding model doesn't generate anything — it maps meaning to a point in
space so meaning can be *compared*.

That's the core split: chat models produce language, embedding models
produce coordinates. It's why "search my notes for anything about
tax deductions" is an embeddings problem (find nearby points) and "explain
what a tax deduction is" is a chat problem (generate an explanation).
They're often used together — this pairing is exactly what powers RAG
(retrieval-augmented generation): embed a question, find the nearest
stored chunks of text by vector distance, then hand those chunks to a
chat model to actually write the answer.

## Try this

Below is a tiny side-by-side: type the same short phrase into both a
"chat" framing and a "search" framing and see how the task — and the kind
of model you'd reach for — changes.

<!-- interactive.js renders here -->

## Why it matters

This is the split that explains why "just add a vector database" and
"just add a bigger chat model" solve different problems. It's also the
foundation for the next lesson in this sequence — tool use — since a lot
of "the model looked something up" behavior is really an embedding search
happening behind the scenes, with a chat model narrating the result.
