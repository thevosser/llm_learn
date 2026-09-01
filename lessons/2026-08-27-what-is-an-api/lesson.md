---
topic_id: what-is-an-api
type: concept
title: "What 'Calling an API' Actually Means"
hook: "It's not magic. It's a very structured letter, mailed to a program you don't control."
category: dev-fundamentals
---

## The concept

"Call the API" gets used so casually it's easy to skip past what's
actually different about it. Calling a function in your own code and
calling an API are both "ask something to do work and give you back an
answer," but the mechanics underneath are not the same at all.

Call your own function, and everything happens in the same process, in
the same memory, effectively instantly — you wrote it, you control every
line, and if something goes wrong it's your bug to fix directly.

Call an API, and a request travels out over the network — usually as
HTTP — to a completely different program, frequently one running on
someone else's server that you have no access to or control over. That
request has to follow an agreed-upon shape: a URL, a method
(GET to fetch something, POST to send something), often a JSON body, and
usually some form of authentication (this is exactly where the API keys
and PATs from earlier lessons come in — they're how the other program
verifies the request is allowed). The response comes back the same way,
over the network, formatted the way that API decided to format it.

That round trip is where a whole category of failure appears that a local
function call doesn't have: the network can be slow or drop entirely, the
other server can be down, rate limits can reject a request that would've
been totally fine seconds earlier, and authentication can be wrong or
expired. None of that is a bug in your code — it's the nature of asking a
program you don't control, over a network you don't control, to do
something for you.

## Try this

Same task — "get today's weather" — two ways:

<!-- interactive.js renders here -->

## Why it matters

Every LLM call in this project, the GitHub push that publishes each
lesson, and the email step still to come are all, mechanically, this same
pattern: a structured request out, a response back, new failure modes
along the way that a local function call would never have. Once "API
call" stops being a vague catch-all and becomes this specific, concrete
shape, error messages like timeouts, 401s, and rate limits stop being
mysterious — they're just which part of that round trip went wrong.
