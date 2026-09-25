---
topic_id: sqlite-vec
type: concept
title: "sqlite-vec: Vector Search Without a Separate Server"
hook: "Your vector database might just be a file next to your code."
category: llm-mechanics
---

## The concept

Once you've decided to store embeddings and search them, you need
somewhere to actually put the vectors and something to compute similarity
between them. `sqlite-vec` is a loadable extension for SQLite — the same
single-file, no-server database used all over this project's own
discussions — that adds a real vector table type (`vec0`) and a `MATCH`
operator for nearest-neighbor distance queries, directly inside ordinary
SQL.

Without it, storing vectors in SQLite still technically works: you'd
store each vector as a serialized blob, then pull every row back into
your application code and compute cosine similarity yourself, in a loop,
outside the database. That works for small datasets but puts all the
comparison work in your application, in whatever language it's written
in, computed one row at a time.

With `sqlite-vec`, that same comparison happens inside the database
engine itself, as part of the query — `MATCH` and `vec0` express
"find the nearest vectors" as SQL, next to whatever ordinary columns
(dates, categories, IDs) you'd normally filter on. No separate vector
database server to run, deploy, or keep in sync — just SQLite, doing one
more thing SQLite already knows how to do.

## Try this

Finding the 3 nearest stored vectors to a query vector, two ways:

<!-- interactive.js renders here -->

## Why it matters

This is a direct, concrete instance of the fixed-price-vs-metered
tradeoff from the cloud-cost-basics lesson, applied to infrastructure
instead of billing: running a dedicated vector database server is more
capable at large scale, but it's an extra service to deploy, monitor, and
keep available. For a project sized like this one's own daily-lesson
tool, `sqlite-vec` is the same "keep it simple, one fewer moving part"
bet this whole site was already built around.
