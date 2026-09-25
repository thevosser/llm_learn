---
topic_id: structured-lookup-vs-vector-search
type: concept
title: "Structured Lookup vs. Vector Search: Don't Embed What You Can Just Ask"
hook: "Vector search finds the closest match. Sometimes you need the exact, only-correct answer."
category: data-storage
---

## The concept

Vector search is built to answer "what's semantically closest to this,"
which is exactly the wrong question to ask for a fact that has one single
correct answer sitting in a database field somewhere. "Have these two
bots interacted before?" isn't a fuzzy, meaning-based question — it's a
yes-or-no fact that either is or isn't true, recorded (or derivable)
directly in structured data. Running that through vector search would
mean embedding the question, embedding some record of past interactions,
and hoping the closest match happens to be correct — an unnecessary,
probabilistic detour around a question a plain `SELECT` could answer with
certainty.

The distinguishing test is simple: does this question have an exact,
unambiguous answer defined by specific fields in your data (an ID match, a
date comparison, a boolean flag), or is it fundamentally about *meaning*
or *similarity* where there's no single "correct" match, only better and
worse ones? The first category is a job for ordinary structured
lookup — SQL `WHERE` clauses, exact key matches. The second is what vector
search was actually built for.

Reaching for vector search on a structured-lookup question doesn't just
waste effort — it introduces a real failure mode that a plain SQL query
never has: the "closest match" from an embedding comparison can be
wrong with total confidence, in exactly the way a `WHERE bot_a_id = ? AND
bot_b_id = ?` query structurally cannot be.

## Try this

Answering "have bot A and bot B interacted before?" two ways:

<!-- interactive.js renders here -->

## Why it matters

This is the reverse warning to vector search's own lesson: knowing when
*not* to reach for the fuzzy, meaning-based tool is just as important as
knowing how to use it. A system correctly built with both RAG for
open-ended questions and structured SQL lookups for exact facts is doing
something more disciplined than a system that runs everything through
embeddings because that's the pattern that was already set up.
