---
topic_id: environment-variables-and-secrets
type: concept
title: "Why Secrets Don't Belong in Your Code"
hook: "Delete the line with the API key. The key is still in your git history forever."
category: dev-fundamentals
---

## The concept

The tempting shortcut when you're wiring up an API for the first time is
to just paste the key straight into the code: `API_KEY = "sk-abc123..."`.
It runs immediately, no extra setup — and it's a bad habit for a specific,
concrete reason, not just a vague "best practice" one.

The moment that line gets committed to git, the key is in the repository's
history permanently. Deleting the line in a later commit doesn't remove
it — the old commit still exists, still contains the key, and anyone with
access to the repo (or its history, if it's ever made public, forked, or
shared) can find it. This is exactly the same shape of problem discussed
earlier this project around GitHub PATs: a secret embedded anywhere
persistent is a secret that's effectively permanent until it's manually
revoked.

The fix is to keep the secret's actual value completely outside the code:
an **environment variable**. The code just reads
`os.environ["API_KEY"]` (or the equivalent in any language) — the actual
value lives somewhere else entirely: a `.env` file that's explicitly
excluded from git via `.gitignore`, or a platform's secret-manager UI (the
Console vault credentials, GitHub Actions secrets, a hosting provider's
environment settings). The code becomes portable — the same script works
on your laptop, a teammate's machine, or a server, each with its own key
injected at runtime — and rotating a leaked key means updating one value
somewhere, not changing and redeploying code.

## Try this

Same script, two ways of getting the API key into it:

<!-- interactive.js renders here -->

## Why it matters

This is the exact mechanism behind the GitHub PAT and Anthropic API key
discussions from earlier in this project — "where does the secret live"
isn't a side detail, it's the whole security model. Every credential this
project touches (the GitHub token, a future email-service key, an
Anthropic API key for the curator agent) follows this same pattern: never
in the code, always injected at runtime from somewhere the code doesn't
control.
