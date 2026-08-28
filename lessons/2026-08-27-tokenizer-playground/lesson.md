---
topic_id: tokenizer-playground
type: code
title: "Tokens Aren't Words — Prove It Yourself"
hook: "A whitespace split isn't a tokenizer. Watch it undercount."
category: llm-mechanics
---

## The concept

The context-windows lesson established that models measure everything in
tokens, not words — but "token" stayed a bit abstract there. Today you get
to poke at it directly.

The cheapest possible stand-in for a tokenizer is `text.split()` — break on
whitespace, count the pieces. It's tempting to treat that as "close enough"
to a real token count. It isn't, and the gap is bigger than people expect.
Real tokenizers (the kind actual models use) usually split punctuation off
as its own token, and often break a single unfamiliar word into several
sub-word pieces. A whitespace split does neither, so it systematically
undercounts anything with punctuation or uncommon words in it — exactly
the content that tends to eat the most context window in practice.

## Try this

The code box below has a deliberately naive `naive_token_count()` — it
just splits on whitespace. Run it as-is, then:

1. Change `text` to something with a lot of punctuation in it.
2. Notice the count doesn't move even though a real tokenizer would see
   more tokens (each `.` `,` `!` `?` `'` typically counts as its own).
3. Extend `naive_token_count()` so it also counts each of those
   punctuation marks as a separate token, and re-run. Watch the number
   climb closer to what a real tokenizer would report for the same text.

```python
text = "Well, that's not exactly right -- is it?"

def naive_token_count(s):
    # crude: just split on whitespace
    return len(s.split())

print(f"Text: {text}")
print(f"Naive count (whitespace split): {naive_token_count(text)}")

# Your turn: extend naive_token_count() so punctuation like . , ! ? '
# each count as their own token too, closer to how a real tokenizer
# would see this text. Then try a sentence with a made-up word in it -
# a whitespace-based counter has no way to represent a word getting
# split into multiple sub-word tokens, no matter how you extend it.
```

<!-- interactive.js renders here -->

## Why it matters

"Just count the words" is a mental shortcut that quietly breaks the
moment real text shows up — contractions, punctuation-heavy writing, code
snippets, or anything with names and jargon the model split into pieces.
Every one of those makes the real token count higher than a word count
would suggest, which is exactly the direction that gets a request
unexpectedly close to a context-window limit.
