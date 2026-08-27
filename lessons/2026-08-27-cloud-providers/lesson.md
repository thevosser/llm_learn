---
topic_id: cloud-providers
type: concept
title: "Cloud Providers, Compared"
hook: "Why 'just use AWS' isn't always the right answer anymore."
category: cloud-infra
---

## The concept

For years, "cloud" basically meant three names: AWS, Azure, and Google Cloud.
They're still the biggest players, and they're built for huge companies running
thousands of servers. That's exactly why they can feel overwhelming for a
one-person project: you're wading through the same console built for a
company with a whole ops team.

There's a second tier of providers built specifically for solo developers and
small projects: things like DigitalOcean, Railway, and Fly.io. They trade
away some of the deep customization the big three offer, in exchange for
being simple enough to actually get something running in an afternoon.

The real question isn't "which cloud is best" — it's "how much complexity
does this specific project actually need." A personal site serving a few
static pages needs almost none. A system handling sensitive data across many
regions needs a lot.

## Try this

Below is a tiny interactive comparison. Toggle between "small personal
project" and "enterprise system" and see how the reasoning for which
provider fits changes.

<!-- interactive.js renders here -->

## Why it matters

You'll hit this decision every time you start a new project. Knowing the
real tradeoff, control and depth versus simplicity and speed, means you can
pick deliberately instead of defaulting to whatever's most famous.
