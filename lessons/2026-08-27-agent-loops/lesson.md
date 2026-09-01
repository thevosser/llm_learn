---
topic_id: agent-loops
type: concept
title: "Agent Loops: Tool Use, on Repeat"
hook: "An agent doesn't have new abilities. It just gets to go again."
category: llm-mechanics
---

## The concept

An "agent" sounds like it should be a different kind of thing from a chat
model — something with more capability, more autonomy. Mechanically, it
isn't. An agent loop is exactly the tool-use exchange from the last
lesson, just allowed to repeat: after a tool result comes back, instead of
stopping, the model gets another turn where it can call another tool, or
another, until it decides it has enough to write a final answer.

The "loop" part is doing all the work here, and it lives entirely in your
code, not the model. Your program keeps re-calling the model with the
growing conversation (original question, plus every tool call and result
so far) until the model's response is a plain answer instead of another
tool request — then the loop exits. Strip away the framing and it really
is just a `while` loop: `while model wants to use a tool: run the tool,
add the result, ask again`.

This is also exactly why agents can go wrong in a specific way regular
chat can't: nothing inherently stops the loop. A model that keeps deciding
"one more tool call would help" keeps the loop going — which is why real
agent code always adds a hard cap on iterations, not because the model is
untrustworthy, but because an unbounded loop is a bug waiting to happen
regardless of what's driving it.

## Try this

Watch a single question turn into a multi-step loop — step through what
the model sees and does at each turn:

<!-- interactive.js renders here -->

## Why it matters

Every "AI agent" product is this loop with a specific tool set and a
system prompt around it — there's no separate "agent mode" inside the
model itself. Once this clicks, agent frameworks stop looking like magic
and start looking like what they are: a while loop, a growing
conversation, and a stopping condition. It's also the direct setup for the
next lesson — multi-agent orchestration is just several of these loops
delegating pieces of a task to each other.
