---
topic_id: polyglot-persistence
type: concept
title: "Polyglot Persistence: Different Jobs, Different Databases"
hook: "The right number of database types for a system is 'exactly as many as it has actual pain points.'"
category: data-storage
---

## The concept

Polyglot persistence is the practice of using different database types
for different jobs within the same system — relational for transactional
records, vector for semantic search, graph for relationship traversal,
columnar for analytics — rather than forcing every kind of data and every
kind of question through a single database shape. Given the last several
lessons, this might sound like the obvious endpoint: why wouldn't you use
the exactly-right tool for each job?

The reason it's not automatically the right call is operational cost,
and it's real: every additional database type in a system is another
piece of infrastructure to run, monitor, back up, secure, and keep
compatible as the rest of the system changes. A system with four database
types has four times the surface area for something to go quietly out of
sync, four sets of operational knowledge required, and four things that
can independently break at 2am.

The right trigger for adding a new database type isn't "this would be
theoretically more optimal" — it's a specific, concrete pain point that's
actually being felt: joins that have become unmanageably slow and deep
(reach for graph), vector search that's outgrown exact linear scan
(reach for a dedicated vector database), an analytics query that's
choking a transactional system (reach for columnar). Add the complexity
when the pain justifies it, not preemptively.

## Try this

A system's storage choices at two different points in its life:

<!-- interactive.js renders here -->

## Why it matters

This is the exact "keep it simple, add complexity only when it's earned"
principle this whole learning site was built around, applied to database
architecture instead of site architecture — the same reasoning that kept
this project on a single SQLite-backed GitHub Pages site instead of
standing up a database server on day one.
