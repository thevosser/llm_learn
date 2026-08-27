---
topic_id: cloud-cost-basics
type: concept
title: "Why Cloud Bills Don't Look Like Your Netflix Bill"
hook: "A $5/month droplet and a $5/month AWS habit are not the same kind of $5."
category: cloud-infra
---

## The concept

There are two fundamentally different ways cloud providers charge you, and
mixing them up in your head is where "why is my bill $400" surprises come
from.

**Fixed-price hosting** (a DigitalOcean droplet, a Railway service) works
like rent: you pick a box with a certain amount of CPU/RAM/disk, and you
pay that price whether you use 2% of it or 100% of it. The ceiling is
completely predictable — it cannot go over the sticker price — but you're
also paying for idle capacity sitting there unused most of the time.

**Metered/usage-based billing** (AWS, GCP, Azure, and most of their
individual services) works like a utility bill: you're charged for exact
consumption — requests served, data transferred out, compute-seconds
used, storage-hours. Nothing sits idle costing you money, but there's no
inherent ceiling either. A workload that's normally cheap can spike hard
if traffic spikes, a loop retries endlessly, or a public bucket gets
scraped — the bill follows usage wherever it goes.

Neither is "better" — they're a tradeoff between predictability and
efficiency, and the right one depends entirely on the shape of the
workload: something with steady, well-understood usage favors fixed-price;
something spiky or unpredictable favors metered, because you'd otherwise
be paying fixed-price for peak capacity you rarely use.

## Try this

Below is a toggle from the cloud-providers lesson's family: switch between
"steady, predictable small workload" and "spiky, unpredictable workload"
and see which billing model comes out cheaper in each case.

<!-- interactive.js renders here -->

## Why it matters

This is directly relevant to the daily-curator decision on this very
project: a small job that runs once a day for a few minutes is exactly the
"steady, predictable, low usage" shape — which is why a fixed-price
droplet is a completely reasonable choice here, even though a
metered/managed service could technically also do it for pennies. Knowing
which category a workload falls into is the whole decision, most of the
time.
