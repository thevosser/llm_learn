---
topic_id: tool-use
type: concept
title: "Tool Use: How a Model Asks Your Code to Do Something"
hook: "The model never runs anything. It asks, and your code decides whether to say yes."
category: llm-mechanics
---

## The concept

A chat model only does one thing: predict the next chunk of text. It has
no ability to reach out to a database, call an API, or check the current
time — none of that is part of what "generate text" means. Tool use is the
protocol that lets a model participate in that kind of action anyway,
without ever actually gaining the ability to do it itself.

Here's the mechanism: your request to the model includes a list of
available "tools" — each one just a name, a description, and a schema for
what arguments it takes (this is exactly the schema-enforced structured
output from the previous lesson, applied specifically to "decide whether
to call a function"). When the model decides a tool would help, instead of
writing a plain-text answer it writes a structured request: which tool,
with which arguments. That's it — that's the model's entire contribution.
Your code is the one that actually receives that request, decides whether
to run it, executes it for real, and sends the result back. The model then
gets a fresh turn to write an actual answer using that real result.

The model isn't "calling a function" in any literal sense. It's writing
text that says, in effect, "I'd like `get_weather` called with
`{"city": "Austin"}`" — and every single part of what happens after that
sentence is up to your code, including whether it happens at all.

## Try this

Same question — "What's the weather in Austin right now?" — asked of a
model with and without tool access:

<!-- interactive.js renders here -->

## Why it matters

This is the seam underneath every AI product that appears to "do" things —
search the web, check a calendar, send an email, query a database. None of
that is the model reaching out into the world; it's the model asking, your
code deciding, and the answer coming back through the same channel. It's
also the literal building block for the next two lessons: an agent loop is
just this same tool-use exchange happening repeatedly until the model
decides it's done, and multi-agent orchestration is several of those loops
talking to each other.
