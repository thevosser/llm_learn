---
topic_id: quantization-and-model-compression
type: concept
title: "Trading Precision for Speed: What Quantization Actually Does"
hook: "Cutting a model's numbers from 16 bits to 4 bits sounds like it should break everything - usually it barely dents accuracy."
category: high-performance-computing
---

## The concept

Every weight in a model is a number, and by default those numbers are
stored with a lot of precision - 16 or 32 bits each, capable of
representing an enormous range of values very finely. Quantization asks
a blunt question: does a weight of 0.5023841 actually need to be stored
that precisely, or would 0.5 do almost as well?

For most weights in a large model, the answer is "almost as well" is
good enough, because the model's output depends on millions of weights
working together - a small rounding error in any one of them gets
averaged out by all the others. Storing weights in 8 or even 4 bits
instead of 16 shrinks the model's memory footprint by 2-4x and lets a
GPU move and multiply that data faster, since less data means less
memory bandwidth spent per weight - directly attacking the bottleneck
from gpu-parallelism-basics.

The tradeoff isn't free: precision loss compounds in specific spots
(very large or very small weights, and models already fine-tuned to a
narrow task) more than others, which is why quantization is a spectrum
to tune per use case, not a single on/off switch. Going too aggressive
(down to 1-2 bits) does start visibly degrading output quality, which is
exactly why 4-8 bit is the common sweet spot in practice rather than
going as low as possible.

## Try this

Same model, three precision levels - see where the tradeoff actually
lands:

<!-- interactive.js renders here -->

## Why it matters

This is a second, independent lever on top of the parallelism levers
from gpu-parallelism-basics and inference-batching-and-throughput: those
make better use of the hardware you have, while quantization changes how
much hardware the model needs in the first place. In an orchestration
system running many agents at once (orchestrating-agents-at-scale), a
quantized model directly means more concurrent work fits in the same
GPU memory - a real, practical version of the "high-performance +
orchestration" bridge you were after.
