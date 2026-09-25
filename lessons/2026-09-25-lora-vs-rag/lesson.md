---
topic_id: lora-vs-rag
type: concept
title: "LoRA vs. RAG: Baking It In vs. Looking It Up"
hook: "One of these changes the model permanently. The other never touches it at all."
category: llm-mechanics
---

## The concept

This is the fine-tuning-vs-prompting distinction from earlier, made
concrete with two specific, commonly paired techniques. LoRA
(Low-Rank Adaptation) is a fine-tuning method — it adjusts the model's
weights (efficiently, via small additional trained matrices, rather than
retraining the whole model from scratch) so a particular style or skill
becomes permanently baked in. Once trained, that behavior shows up by
default, with no special prompt needed to invoke it.

RAG does none of that. It retrieves facts or examples at query time and
inserts them into the prompt — the model's weights never change, and if
you stop retrieving, the model goes right back to behaving exactly as it
did before, with zero memory of anything it was ever shown via RAG.

The practical split: RAG is the right tool for facts and examples that
change often, or that are specific to one query at a time (today's
documents, this particular bot's past posts) — retraining a model every
time your source data changes would be absurd. LoRA is the right tool for
a style, tone, or skill you want present *by default*, on every request,
without having to retrieve and re-inject it each time — worth the
upfront training cost specifically because it doesn't need repeating.

## Try this

Getting a model to consistently write in one bot's specific voice, two
ways:

<!-- interactive.js renders here -->

## Why it matters

The two aren't actually competitors — they solve different problems and
often get combined: a LoRA-trained base tone plus RAG-retrieved
specific-post examples layered on top. Confusing which one to reach for is
usually a category error the same way choosing fine-tuning over prompting
was in the earlier lesson — pick based on "does this need to change
per-request" (RAG) or "should this be true by default, every time"
(LoRA), not on which one sounds more sophisticated.
