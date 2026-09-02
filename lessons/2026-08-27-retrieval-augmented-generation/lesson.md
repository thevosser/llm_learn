---
topic_id: retrieval-augmented-generation
type: concept
title: "RAG: Giving a Chat Model Something Real to Read First"
hook: "RAG doesn't make the model smarter. It gives it better source material."
category: llm-mechanics
---

## The concept

Retrieval-augmented generation (RAG) is what you get from combining two
mechanisms already covered separately: embeddings-based search, and chat
generation. The recipe is simple: take the user's question, embed it into
that vector space from the embeddings-vs-chat lesson, find the
nearest-matching chunks of real text from your own documents (not the
model's training data — your actual notes, your actual docs), and hand
those chunks to the chat model as part of the prompt, along with an
instruction to answer using them.

The point of doing this connects directly to the previous lesson: a chat
model answering purely from its own training data is exactly where
hallucination risk lives, especially for anything specific to you — your
notes, your company's internal docs, anything that was never in its
training data at all, by definition. RAG sidesteps that entirely. The
model isn't recalling anything from fuzzy training-data memory; it's
reading real text you just handed it in the prompt, the same way you'd
answer a question far more accurately with the source document open in
front of you than from memory alone.

It's worth being precise about what RAG is not: it doesn't change the
model's weights, doesn't make it "know more" in any lasting sense, and
the very next question with no relevant retrieved chunks gets answered
exactly like a plain chat model would — confidently, and with the same
hallucination risk as before.

## Try this

Same question about your own notes, asked two ways:

<!-- interactive.js renders here -->

## Why it matters

This is the direct, practical fix for the hallucination problem on
anything the model couldn't possibly know from training — your own
content. It's also just the embeddings-vs-chat lesson's search mechanism
and the tool-use lesson's "give the model real data" pattern, combined
into one specific, extremely common architecture. Nothing new to learn
mechanically — just those two pieces working together.
