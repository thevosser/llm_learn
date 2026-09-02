---
topic_id: fine-tuning-vs-prompting
type: concept
title: "Fine-Tuning vs. Prompting: Two Ways to Change Behavior"
hook: "One changes what you say to the model. The other changes the model."
category: llm-mechanics
---

## The concept

When a model isn't doing what you want, there are two structurally
different ways to fix it. Prompting means changing your instructions —
clearer wording, better examples, a stricter format request — with zero
change to the model itself. It's what the prompt-engineering-basics
lesson was entirely about: cheap, instant, and fully reversible by just
writing a different prompt next time.

Fine-tuning means actually continuing the model's training on your own
examples, adjusting its underlying weights so the desired behavior
becomes baked in rather than something you have to re-explain every
single request. That sounds strictly better — no more repeating
instructions — but it comes at real cost: you need an actual training
dataset (often hundreds or thousands of good examples), a training run
that costs real money and time, and undoing a bad fine-tune isn't a
one-line prompt edit, it's training again.

In practice, almost everything should start with prompting, because
iteration is nearly free — you can test ten different phrasings in ten
minutes. Fine-tuning earns its cost in narrower cases: extremely
high-volume, well-defined, repetitive behavior where the token cost of
re-explaining the same instructions on every single request (at scale)
outweighs the upfront cost of training it in once.

## Try this

Same goal — get consistent, correctly-formatted JSON output every time —
handled two ways:

<!-- interactive.js renders here -->

## Why it matters

This is a direct extension of the "try the cheap lever first" idea from
structured-outputs and prompt-engineering-basics: prompting (and
schema-enforced structured output) solves the overwhelming majority of
"the model isn't doing X" problems well before fine-tuning would even be
worth considering. Reaching for fine-tuning before exhausting prompting is
one of the more common expensive mistakes in practice.
