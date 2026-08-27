---
topic_id: git-branching
type: concept
title: "Branches Aren't Copies — They're Pointers"
hook: "The thing that makes branching cheap is the same thing that makes merge conflicts confusing."
category: dev-fundamentals
---

## The concept

The mental model that trips people up: a branch feels like it should be a
full copy of the project, frozen at some point in time. It isn't. A branch
is just a movable label pointing at one commit. Creating a branch costs
almost nothing — Git isn't copying any files, it's writing a few bytes that
say "here's where `git-branching` points right now."

Commits themselves are the real structure: each one points back at its
parent, so the whole history is a chain (technically a graph, once branches
fork and merge). When you "make a commit on a branch," what actually
happens is: a new commit gets created pointing at the old commit, and the
branch label moves forward to point at the new one. Switching branches just
moves which label you're currently standing on.

This is why merging can get messy: two branches are two different chains of
commits that both grew out of the same starting point. A **merge** finds
that common ancestor and combines both sets of changes into a new commit
with two parents. A **rebase** does something different — it takes your
branch's commits and replays them one by one on top of the other branch, as
if you'd written them there in the first place, producing a single straight
line instead of a fork. Same end content is possible either way; the
difference is whether the history remembers the fork happened.

## Try this

Below is a small before/after comparison: pick "merge" or "rebase" on the
same two diverging branches and see how the resulting commit graph differs.

<!-- interactive.js renders here -->

For a much deeper hands-on drill — actually typing the commands and
watching a real graph move — Learn Git Branching
(learngitbranching.js.org) is worth 15 minutes on its own. Treat today's
comparison as the "why," and that site as the "muscle memory."

## Why it matters

Pull requests are just "hey, merge my branch into yours" with a review step
attached. Once branches-as-pointers clicks, PRs, merge conflicts, and
"rebase vs. merge" arguments on a team stop being mysterious — they're all
just different ways of asking the same question: how do these two chains
of commits get reconciled into one.
