---
topic_id: hallucination
type: concept
title: "Hallucination Isn't a Bug in the Usual Sense"
hook: "The model isn't lying to you. It never had a concept of 'true' to lie about in the first place."
category: llm-mechanics
---

## The concept

A chat model's entire job, mechanically, is producing plausible next
tokens given everything before it. Nowhere in that objective is there a
step that checks the output against reality — there's no internal
fact-database lookup, no "am I sure about this" flag being consulted.
Plausible-sounding and true happen to line up most of the time, because
the training data mostly contains true things stated in normal,
plausible-sounding ways. But "plausible" and "true" are not the same
property, and the gap between them is where hallucination lives.

When a model has strong, well-represented training data on a topic, this
gap rarely shows up — the most plausible continuation usually is the
correct one. When it doesn't — an obscure fact, a question about
something past its training cutoff, a made-up-sounding name it's never
actually seen — the model still does the exact same thing it always
does: produce the most plausible-sounding continuation it can. That
continuation can be completely fabricated and still come out fluent,
confident, and specific, because nothing about *how* fluently or
confidently something is generated tracks whether it's grounded in
anything real.

This is also why asking a model "are you sure?" doesn't reliably fix
anything — the model can generate a confident-sounding reassurance just
as easily as it generated the original fabrication, for exactly the same
reason: fluency was never coupled to accuracy in the first place.

## Try this

Same kind of question, asked about something well-represented in
training data versus something obscure or fabricated-sounding:

<!-- interactive.js renders here -->

## Why it matters

This is the actual reason retrieval-augmented generation and tool use
exist as patterns — both are ways of giving the model something real to
work from (a fetched document, a live API result) instead of relying on
its own fuzzy training-data memory for anything that needs to actually be
correct. Recognizing which category a question falls into — safely inside
what the model reliably knows, or in hallucination-risk territory — is
the practical skill this lesson is really about.
