---
topic_id: desirable-difficulty
type: concept
title: "Why the Broken Starter Code Is on Purpose"
hook: "If a lesson feels effortless, check whether you're actually building anything."
category: learning-science
---

## The concept

There's a category of difficulty in learning that actively helps, which
is a strange claim on its face — isn't the point to make things clear and
easy? "Desirable difficulty" is the research term for exactly this: certain
kinds of friction, introduced deliberately, produce deeper and more
durable learning than a smooth, frictionless presentation of the same
material, even though the smooth version feels more pleasant and more
"successful" while it's happening.

The mechanism is the same one from the retrieval-practice lesson, applied
one level up: struggling to produce or fix something yourself forces real
engagement that watching a clean, correct example doesn't. A fully working
script you just read requires nothing from you but attention — you can
follow every line without ever testing whether you actually understand
it. A script with something subtly wrong or incomplete forces you to
actually reason about what it's doing, form a hypothesis about the fix,
and test that hypothesis — which is a different and much stronger kind of
engagement than passive reading, even on the exact same material.

The "desirable" part matters, though — this isn't an argument for
maximum difficulty. Difficulty that's just confusing (bad instructions,
missing context, an error with no clues) doesn't help; it just frustrates.
The useful kind is difficulty that's productive: you have enough to work
with, the gap is real but closeable, and closing it yourself is what does
the work a worked example can't.

## Try this

Same code concept, presented two ways — compare what each actually
demands of you:

<!-- interactive.js renders here -->

## Why it matters

This validates a rule that's already written into
`curator/agent_instructions.md`: every code lesson should include "a
short starter snippet with something incomplete or slightly broken... —
never a fully working script to just read." That wasn't an arbitrary
style choice — it's this exact principle, already correctly built into
how this project generates lessons. Worth protecting deliberately as more
lessons get added: the temptation to hand over a clean, complete example
"to be helpful" is exactly the temptation this research says to resist.
