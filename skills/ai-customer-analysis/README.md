# AI Customer Analysis — Verified Insight Protocol

Analyze customer interviews, surveys, and transcripts with AI — without the hallucinations, cherry-picking, and false confidence that corrupt most AI-assisted qualitative research.

## The Problem

You get one output. It reads confidently. You build your next product decision on top of it. You never see what's missing.

Run the same customer transcripts through two models and you get completely different narratives, different "evidence," and different product recommendations — at the same confidence level. The model doesn't analyze your data. It generates the most statistically likely answer, which is almost always what you already believe, formatted as insight.

## What This Skill Prevents

| Failure Mode | What Happens Without This Skill |
|-------------|--------------------------------|
| Invented evidence | Model fabricates or misattributes quotes |
| False/generic insights | "Customers want simplicity" — true of every product |
| Signal without direction | Observations with no actionable decision |
| Contradictory insights | Real tensions in your data averaged into false consensus |

## Install

```bash
npx skills add ManiClones/agent-skills --skill ai-customer-analysis
```

## Trigger

```
"Analyze these customer transcripts using the ai-customer-analysis skill"
"I have 12 customer interview transcripts — help me find real insights"
"What are customers actually asking for in these survey responses?"
```

## Output Format

Every insight produces 5 required fields:
- **INSIGHT** — specific, directional, actionable
- **EVIDENCE** — exact quote with participant ID + timestamp
- **SEGMENT** — which customer type, not "customers in general"
- **CONTRADICTIONS** — a customer who disagrees, with source
- **DECISION** — specific action or explicit non-action

No insight ships without all 5 fields.
