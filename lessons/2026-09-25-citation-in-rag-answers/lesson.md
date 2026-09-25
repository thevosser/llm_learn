---
topic_id: citation-in-rag-answers
type: concept
title: "Citation in RAG: Making the Answer Checkable"
hook: "A RAG answer without a citation is just a hallucination with better source material."
category: llm-mechanics
---

## The concept

A RAG pipeline hands a chat model real, retrieved text and asks it to
answer using that text — which solves the hallucination problem from
earlier for the *facts themselves*, but doesn't automatically solve a
related problem: how do you know the model actually used the retrieved
text, rather than quietly falling back on its own training-data instincts
partway through the answer? Nothing about the RAG architecture forces the
model to stay grounded in what it was given.

Citation closes that gap by adding one more instruction to the prompt:
name which retrieved source (a document title, a chunk ID, a page number)
supported each part of the answer. This doesn't change what the model is
mechanically capable of — it's still just generating text — but it
creates something checkable. A confident answer with no citation asks you
to trust it. A confident answer with a citation lets you go verify: open
that specific source, and see for yourself whether it actually says what
the model claims it does.

This also surfaces failures that would otherwise stay invisible: if a
model is asked to cite its source and the citation doesn't actually
support the claim (or doesn't exist at all), that's a much clearer signal
something went wrong than a plausible-sounding uncited answer ever would
be.

## Try this

The same RAG answer, with and without a citation requirement:

<!-- interactive.js renders here -->

## Why it matters

This is a structured-output problem wearing a RAG costume — "always
include a source reference in your answer" is exactly the kind of format
requirement the structured-outputs lesson covered, just applied to make a
specific failure mode (ungrounded RAG answers) visible instead of
invisible. It costs one more sentence in the prompt and turns "trust me"
into "check this yourself."
