---
topic_id: cost-per-task-vs-cost-per-token
type: concept
title: "The Metric That Should Actually Drive Orchestration Decisions"
hook: "The cheapest model per token can be the most expensive way to finish a task."
category: high-performance-computing
---

## The concept

Cost-per-token is the number that's easy to compare across models,
which is exactly why it's the number people default to optimizing. But
it isn't the number that determines what a task actually costs to
finish — cost-per-task is, and the two can point in opposite directions.

A cheap model that gets a task right on the first try in 500 tokens can
easily cost less overall than an even cheaper model that needs three
retries and a longer prompt each time to get there, because retries
don't just add tokens linearly - they add the tokens of every failed
attempt plus the tokens spent diagnosing and re-prompting after each one.
The same logic applies to picking between a fast, weaker model and a
slower, stronger one for a step in a pipeline: if the weaker model's
mistakes get caught downstream and cost a full re-run to fix, the
"expensive" model was actually cheaper end to end.

This matters most in orchestration, where a single pipeline might call a
model hundreds or thousands of times. A per-call saving that looks
tiny in isolation, multiplied by a bad retry rate across that many
calls, can dwarf the savings from a cheaper base rate — which is exactly
why the metric you optimize for changes the architecture you'd build.

## Try this

Same task, two model choices - see where the sticker price and the
actual cost diverge:

<!-- interactive.js renders here -->

## Why it matters

This is the metric orchestrating-agents-at-scale actually needs:
"concurrency limits and rate limits" from that topic are about what you
*can* run at once, but cost-per-task is what tells you whether you
*should* — it's the number that decides whether fanning a task out to
many cheap agents or running it through one capable one is the better
design for a given pipeline, which is precisely the tradeoff a real
orchestration project has to make.
