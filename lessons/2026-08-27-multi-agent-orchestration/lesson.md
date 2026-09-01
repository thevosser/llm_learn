---
topic_id: multi-agent-orchestration
type: concept
title: "Multi-Agent Orchestration: One Loop, or Several Talking to Each Other?"
hook: "A team of specialists isn't smarter than one generalist — it just forgets less."
category: llm-mechanics
---

## The concept

Take the agent loop from the last lesson and ask: what happens as the task
gets bigger? A single loop handling everything keeps appending every tool
call and result to one growing conversation. That works fine for a short
task, but it has a real cost: the context keeps growing, and everything
that's ever happened in the loop stays in view (and gets re-sent, and
re-billed) on every single turn — including tool results that were only
relevant three steps ago.

Multi-agent orchestration is the fix for that specific problem, not a
different kind of intelligence. Instead of one loop doing everything, a
**coordinator** agent breaks the task into pieces and delegates each piece
to its own separate agent loop — each with its own smaller context and
often its own narrower tool set. When a sub-agent finishes, it doesn't
hand back its entire conversation history — just a summarized result. The
coordinator's own context only grows by that summary, not by everything
the sub-agent did to produce it.

The tradeoff is real, not free: now there's coordination overhead (who
does what, in what order, what happens if a sub-agent fails) and more
total model calls happening. It's worth it exactly when a single loop's
context would otherwise balloon out of control — not by default for every
task.

## Try this

Same overall job — research three topics and write a combined summary —
handled two different ways:

<!-- interactive.js renders here -->

## Why it matters

This is the actual reason "multi-agent" systems exist, and it's a much
narrower reason than the marketing around them suggests: context
management, not smarter reasoning. Recognizing that means you can tell
when a task genuinely needs multiple agents (it's ballooning one loop's
context) versus when it's just adding coordination overhead to something a
single loop could have handled fine.
