---
topic_id: context-windows-tokens
type: concept
title: "What 'Context Window' Actually Means"
hook: "It's not memory. It's how much the model can literally see in one breath."
category: llm-mechanics
---

## The concept

A "context window" is the maximum number of tokens — input and output
combined — a model can process in a single request. That's the whole
definition, but the implications trip people up constantly.

The big one: **there is no memory between separate requests.** When a
chatbot "remembers" what you said five messages ago, that's not the model
recalling anything — the app is silently resending the entire conversation
so far, every single time, as part of the next request's input. If
something isn't in that resent text, it doesn't exist to the model anymore.
That's also why long conversations get slower and more expensive as they
go: you're not sending one message, you're resending the whole
conversation-so-far plus one new message, every turn.

This connects directly to tokens (from the tokenizer playground, if you've
poked at that): the context window is measured in tokens, not words or
characters, and it's a hard ceiling — go over it and the request either
gets rejected or the oldest content silently falls off the front. A "128K
context window" sounds enormous until you remember a full novel is
roughly 100K-150K tokens — plenty of real work (a large codebase, a long
document, hours of chat history) can actually bump into that ceiling.

## Try this

Below is a small simulation: watch a conversation grow turn by turn and
see when older messages start getting pushed out of a fixed-size context
window.

<!-- interactive.js renders here -->

## Why it matters

This is the practical reason techniques like summarization, RAG
(retrieval instead of resending everything), and "compaction" exist —
they're all just different strategies for fitting more effective history
into a window that has a hard limit. It also explains the very real
experience of "it forgot what I told it earlier": often, it didn't forget
so much as the app stopped sending that part back.
