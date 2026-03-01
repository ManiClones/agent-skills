# Rule: Anchor to Exact Words

## The Problem
AI paraphrases. Paraphrase introduces interpretation. Interpretation introduces bias.
"The user said they found onboarding confusing" is not the same as "I had no idea what to do after I signed up."

## The Rule
Before drawing any conclusion from a data source, quote the customer verbatim.
Do not paraphrase. Do not summarize. Quote first, conclude second.

## Enforcement Prompt
After generating initial insights:
> "For each insight, show me the exact words the customer used — not a paraphrase. If you cannot produce a direct quote, remove the insight."

## Why This Matters
The quote IS the data. The insight is just your interpretation of the quote.
If the interpretation is disconnected from the actual words, the insight is fiction.
