---
topic_id: structured-outputs
type: concept
title: "Getting an LLM to Return Real JSON, Reliably"
hook: "'Return only JSON' in the prompt is a suggestion. There's a stronger way to ask."
category: llm-mechanics
---

## The concept

The moment your code does `json.loads(response)` on a model's output, you've
introduced a new failure mode: what happens the one time in fifty it wraps
the JSON in a sentence, adds a markdown code fence, or trails off mid-object?
That single malformed reply can crash a loop that was otherwise working
fine.

There are two levels of asking for structured output, and they're not
equally reliable:

- **Asking nicely in the prompt** ("respond with only this JSON shape,
  nothing else") works most of the time, because the model is genuinely
  trying to comply. But it's still just an instruction the model is
  following, not a guarantee — nothing stops it from adding a stray
  sentence before or after, especially under a slightly unusual input.
- **Schema-enforced structured output** is a different mechanism: instead
  of hoping the model follows formatting instructions, the API constrains
  the response generation itself so it's mechanically guaranteed to match
  a schema you define — no stray prose possible, because the format isn't
  optional at that point.

The first approach is fine for a quick script where you can eyeball
failures. The second is what you want the moment something else is
automatically consuming that output without a human checking each result —
which is exactly the situation any tool-using or multi-step agent is in
constantly.

## Try this

Below is a comparison: the same request sent as a plain "please return
JSON" prompt vs. a schema-enforced structured request, showing where each
one is prone to breaking.

<!-- interactive.js renders here -->

## Why it matters

This is the exact seam between "the model talked" and "your code can act
on what it said." Every tool-using agent, form-filler, or classifier
depends on this seam holding — which is exactly why it's worth
understanding solidly before building anything that parses model output
inside a loop, rather than discovering the failure mode the first time a
pipeline crashes on a Tuesday.
