---
topic_id: temperature-and-sampling
type: concept
title: "Temperature: Turning the Randomness Dial"
hook: "Temperature doesn't make a model smarter or dumber. It makes it more or less willing to gamble."
category: llm-mechanics
---

## The concept

At each step, a chat model doesn't produce one fixed "next word" — it
produces a full probability distribution over every possible next token,
some far more likely than others. What actually gets picked and appended
to the output is a separate, additional step: sampling from that
distribution. Temperature is the setting that controls how that sampling
behaves.

At temperature 0, sampling almost always just takes the single
highest-probability token every time — the output becomes close to
deterministic, and running the same prompt twice tends to produce
identical or near-identical results. As temperature rises, the
distribution gets flattened out: tokens that were only moderately likely
get picked more often, and the output gets more varied — and, past a
certain point, more likely to wander into something incoherent, since
low-probability tokens are low-probability for a reason.

There's no universally "better" setting — it's a tradeoff, not a quality
dial. Low temperature is right for anything that has one correct or
consistent answer (code, factual lookups, structured extraction) where
variety is a bug, not a feature. Higher temperature is right for anything
that benefits from range — brainstorming, creative writing, generating
multiple distinct options to choose from.

## Try this

Same prompt — "write an opening line for a story about a lighthouse" —
run at increasing temperature settings:

<!-- interactive.js renders here -->

## Why it matters

This is the other big lever alongside the specificity/format work from
the prompt-engineering-basics lesson — wording controls *what* you're
asking for, temperature controls *how much room* the model has in
answering it. Picking a low temperature for a factual task or a
structured-output request isn't caution for its own sake; it's closing
off a source of variance you don't want in an answer that's supposed to
be consistent.
