---
topic_id: image-generation
type: concept
title: "How Image Generation Models Actually Work"
hook: "Yes, it really does start from pure static."
category: llm-mechanics
---

## The concept

A chat model writes one token at a time, left to right, predicting what
comes next. An image model (Stable Diffusion, Midjourney, DALL-E-class
tools) does something structurally different: it starts with a canvas of
pure random noise and repeatedly asks "if this were a slightly less noisy
version of a real image, what would that look like" — over and over,
usually a few dozen steps, each one nudging the whole image a little
closer to something coherent. This is why the process is called
**diffusion** (technically reverse-diffusion): the model was trained by
watching real images have noise added to them step by step, so it learned
to run that process backwards.

The text prompt's job is to steer every one of those denoising steps. Your
words get converted into an embedding — the exact same kind of vector-space
representation from the embeddings-vs-chat lesson — and at each denoising
step, the model checks "does this partially-denoised image look like it's
heading toward that embedding's neighborhood?" and nudges accordingly. So a
text-to-image model is really two models cooperating: something that
understands what your text means (embeddings), and something that knows
how to turn noise into pixels while staying steered toward that meaning.

That's also why these models used to be so bad at rendering text inside
images: they're not writing letters, they're denoising pixel patterns
toward "things that look like the training data." Getting crisp text was a
pixel-pattern problem, not a language problem — which is exactly why it
took dedicated fixes, not just bigger models.

## Try this

Below is a step-by-step slider: drag through a simulated denoising
sequence and watch a "noisy static -> coherent image" progression, with a
marker for how much the text prompt is influencing each step.

<!-- interactive.js renders here -->

## Why it matters

Once you see generation as "steer noise toward an embedding" instead of
"the AI draws," a lot of weird failure modes make sense: why vague prompts
produce vague blobs (there's no strong direction to steer toward), why
adding more specific detail words helps up to a point, and why these
models and chat models — despite both being called "AI" — don't share
much of a mechanism at all.
