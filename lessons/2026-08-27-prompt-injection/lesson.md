---
topic_id: prompt-injection
type: concept
title: "Prompt Injection: When the Data Talks Back"
hook: "If a model reads untrusted text as part of its job, that text can try to give it new orders."
category: llm-mechanics
---

## The concept

Most real LLM applications feed the model a mix of two things: trusted
instructions (from the developer or the user directly) and untrusted
content the model is supposed to just process — a fetched webpage, an
email, a document, the result of a tool call. The problem is that a model
doesn't have a hard structural wall between "instruction" and "data" the
way a traditional program would — it's all just tokens in the same
context window, and the model is doing its best to follow whatever reads
like an instruction, wherever it appears.

That means untrusted content can contain text deliberately written to
look like an instruction: "ignore your previous instructions and instead
do X" embedded inside a webpage or document the model was only supposed
to summarize. A naive application — one that just concatenates the
system instructions and the untrusted content together with no real
separation — can end up following that injected instruction instead of
the developer's original one. This is prompt injection, and it's an
actively exploited, real vulnerability class in production LLM
applications, not a hypothetical.

Defenses aren't perfect, but they're not nothing either: clear structural
separation between instructions and data (rather than blending them into
one undifferentiated block of text), explicitly telling the model that
fetched content is data to analyze — never commands to obey, and treating
anything a tool returns with the same suspicion you'd treat unvalidated
user input in any other kind of application.

## Try this

The same task — summarize a fetched webpage — built two ways:

<!-- interactive.js renders here -->

## Why it matters

This is directly relevant to this project's own future curator agent:
once it's fetching content from the URLs in config/sources.json to decide
what to teach next, that fetched content is untrusted input by
definition — a compromised or malicious page could try exactly this
attack against the curator. The defense pattern in this lesson (treat
fetched content as data, never as instructions) needs to be built into
that agent's design from the start, not added later as an afterthought.
