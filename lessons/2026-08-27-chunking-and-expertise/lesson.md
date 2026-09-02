---
topic_id: chunking-and-expertise
type: concept
title: "Chunking: Why Experts Remember More"
hook: "A chess master doesn't have a better memory than you. They see fewer, bigger pieces."
category: learning-science
---

## The concept

Chunking is grouping several individual pieces of information into one
larger, meaningful unit that then occupies a single slot in working
memory instead of many. It's the direct escape hatch from the
three-to-five-item working-memory limit covered in the cognitive-load
lesson — not by expanding capacity, but by shrinking how many "items"
the same information counts as.

The classic demonstration is chess: shown a real mid-game board for a few
seconds, a novice sees roughly twenty individual pieces to track — bumping
straight into the working-memory ceiling almost immediately. A grandmaster
looking at the exact same board sees a handful of *recognized patterns* —
"that's a standard formation," "that's a familiar attacking setup" — and
reconstructs the position accurately from just a few chunks. Tellingly,
this expert advantage disappears almost completely when the pieces are
arranged randomly instead of in a realistic game position — the
grandmaster's memory isn't fundamentally better, their years of exposure
just built a library of recognizable patterns that only fire on
patterns that actually occur in real play.

This is exactly why the same page of code looks like a wall of symbols to
a beginner and a handful of familiar shapes — a loop, a guard clause, a
standard error-handling pattern — to someone experienced: the same
information, chunked very differently depending on what's already been
built up through practice.

## Try this

The same information, viewed as a beginner would see it versus how
someone experienced in the domain would see it:

<!-- interactive.js renders here -->

## Why it matters

This connects directly across this project's two categories rather than
staying abstract to either one: the tokenizer-playground lesson showed
that a model also breaks text into small pieces (tokens) instead of whole
words — but a model's chunking is fixed by its tokenizer and never
changes. A human's chunking gets coarser and more efficient with real
practice in a domain. Same underlying idea — group small pieces into
meaningful larger units — showing up on both the LLM-mechanics and the
learning-science side of this project.
