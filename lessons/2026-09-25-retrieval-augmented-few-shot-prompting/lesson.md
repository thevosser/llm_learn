---
topic_id: retrieval-augmented-few-shot-prompting
type: concept
title: "Retrieval-Augmented Few-Shot: Picking Examples That Actually Fit"
hook: "The same three examples don't help every prompt equally. Retrieval picks the ones that do."
category: llm-mechanics
---

## The concept

The prompt-engineering-basics lesson covered few-shot examples as one of
the strongest levers for shaping output — showing the model a couple of
input/output pairs usually does more work than describing the pattern in
prose. The examples in that lesson were static: the same two or three,
hardcoded into every prompt regardless of what's actually being asked.

Retrieval-augmented few-shot prompting swaps RAG's retrieve step onto
that exact same mechanism, but retrieves *examples* instead of *facts*.
Instead of always showing the same three hardcoded examples, embed the
current input, search a stored library of past examples for the ones
closest to it, and use those as the few-shot examples in the prompt this
time. A request that's stylistically or topically close to certain stored
examples gets shown *those* examples specifically, rather than whatever
three happened to be picked once and hardcoded forever.

This is the same retrieval mechanism as fact-based RAG end to end —
embed, search, retrieve, insert into the prompt — just pointed at a
library of style or voice examples instead of a library of reference
documents. The "augmented generation" step doesn't care what kind of text
it's reading; it's still just more context in the prompt either way.

## Try this

Generating a post in a specific style, with static examples versus
retrieved examples matched to the current topic:

<!-- interactive.js renders here -->

## Why it matters

This is the exact mechanism behind a "shapes" library for bot voice or
rhetorical style: instead of hardcoding a handful of example posts into
every generation prompt regardless of topic, retrieval finds the stored
examples whose style or topic is closest to the current situation and
uses those specifically — the same RAG retrieval step already covered,
repointed at a completely different kind of stored content.
