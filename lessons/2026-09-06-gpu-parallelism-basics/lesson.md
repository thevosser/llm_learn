---
topic_id: gpu-parallelism-basics
type: concept
title: "Why Matrix Multiplies Scale Across Thousands of Cores"
hook: "A GPU isn't a faster CPU - it's thousands of slow, simple cores doing the same operation at once."
category: high-performance-computing
---

## The concept

A CPU core is built to run one complicated sequence of instructions as
fast as possible, with branches, caching, and out-of-order execution all
optimized for a single stream of logic. A GPU core is the opposite bet:
each one is much simpler and slower on its own, but there are thousands
of them, and they're built to all do the *same* simple operation on
different pieces of data at the same instant.

That bet only pays off when the work is actually shaped that way — and a
matrix multiply, which is most of what happens inside a transformer
model, is exactly that shape. Every output entry in the result matrix is
an independent dot product of one row and one column; none of those dot
products need to know about any other one while it's being computed.
Splitting a huge matrix multiply into thousands of small independent dot
products and handing one to each core is what makes GPUs dramatically
faster than CPUs for this specific kind of math, even though any single
GPU core is individually much weaker than a CPU core.

The catch that shows up as you scale up: keeping thousands of cores fed
with data becomes the new bottleneck. A core sitting idle waiting for
its input to arrive from memory wastes exactly as much time as a core
that's slow to compute — which is why memory bandwidth, not raw core
count, is often what actually limits how fast a real model runs.

## Try this

Same matrix multiply, split across a growing number of cores — watch
where the real speedup comes from, and where it stalls:

<!-- interactive.js renders here -->

## Why it matters

This is the mechanical floor underneath everything else in this
high-performance-computing track: data-vs-model-parallelism is about
splitting work that's too big for one GPU's memory across several GPUs;
inference-batching-and-throughput is about keeping those cores fed with
enough work at once to justify the overhead of dispatching it. Neither
makes sense without this as the starting mental model of what a GPU is
actually good at.
