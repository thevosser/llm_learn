---
topic_id: prompt-engineering-basics
type: concept
title: "Prompt Engineering Isn't Magic Words"
hook: "The best prompts read like clear instructions to a literal new hire, not incantations."
category: llm-mechanics
---

## The concept

"Prompt engineering" sounds like it should mean finding the secret phrase
that unlocks better answers. In practice, almost all of the actual leverage
comes from three boring things:

1. **Say exactly what you want, including the format.** "Summarize this"
   gets you a summary in whatever shape the model feels like. "Summarize
   this in 3 bullet points, each under 15 words" gets you something you can
   actually use without editing. Models aren't bad at guessing what you
   meant — they're just not obligated to guess right, so don't make them.
2. **Show, don't just tell (few-shot examples).** One or two examples of
   the input/output pattern you want usually does more work than a whole
   paragraph describing the pattern in the abstract. This is the same
   reason job training uses worked examples instead of just a rulebook.
3. **Separate instructions from the content being acted on.** "Here are
   your instructions: X. Here is the text to apply them to: Y" is more
   reliable than blending the two — the model is less likely to follow an
   instruction that accidentally looks like part of the data, and vice
   versa.

None of this is about tricking the model — it's the same reason clearer
tickets get better work out of a new coworker. The model isn't reading your
mind either way; the question is just how much of the ambiguity you're
leaving for it to guess at.

## Try this

Below is a side-by-side: the same request written two ways — vague, and
specific-with-format — so you can compare what each is likely to produce.

<!-- interactive.js renders here -->

## Why it matters

This is the fastest lever you have. Before reaching for a bigger model, a
fine-tune, or extra tooling, tightening the prompt itself usually closes
most of the gap between "technically answered" and "actually usable" —
and it costs nothing to try.
