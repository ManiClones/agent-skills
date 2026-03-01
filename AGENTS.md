# agent-skills

This file provides guidance to AI coding agents (Claude Code, Cursor, Copilot, etc.) when working with code in this repository.

## Repository Overview

A collection of agent skills built from real sources — viral articles, proven workflows, and battle-tested frameworks. Each skill is packaged as executable instructions your agent can follow directly.

## Creating a New Skill

### Directory Structure

```
skills/
  {skill-name}/           # kebab-case directory name
    SKILL.md              # Required: skill definition (agent reads this)
    AGENTS.md             # Required: same as SKILL.md or full compiled version
    README.md             # Required: human-readable description
    metadata.json         # Required: version, org, abstract, references
    rules/                # Optional: individual rule files (one per rule)
      _template.md        # Template for new rules
      rule-name.md        # Individual rules
```

### Naming Conventions

- **Skill directory**: `kebab-case` (e.g., `ai-customer-analysis`, `influencer-deal-structure`)
- **SKILL.md**: Always uppercase, always this exact filename
- **Rules**: `kebab-case.md` (e.g., `verification-gate.md`, `hook-selection.md`)

### SKILL.md Format

```markdown
---
name: {skill-name}
description: {One sentence describing when to use this skill. Include trigger phrases like "analyze customer data", "structure influencer deals", etc.}
source: {original article URL if applicable}
---

# {Skill Title}

{Brief description of what the skill does and when to use it.}

## How It Works

1. {Step one}
2. {Step two}
3. {Step three}

## Usage

Invoke by telling your agent:
> "{natural language trigger phrase}"

## Rules

{Core rules the agent must follow — the executable content}

## Output

{What the agent should produce when this skill runs}

## Troubleshooting

{Common failure modes and fixes}
```

### metadata.json Format

```json
{
  "version": "1.0.0",
  "organization": "ManiClones",
  "date": "Month Year",
  "abstract": "One paragraph describing what the skill does, what problem it solves, and who it is for.",
  "source": "https://original-article-url.com",
  "references": [
    "https://reference1.com",
    "https://reference2.com"
  ]
}
```

### Best Practices

- **Keep SKILL.md under 500 lines** — use `rules/` subdirectory for detailed content
- **Write specific descriptions** — the description is what the agent uses to decide when to activate the skill
- **One rule per file** in `rules/` — makes it easy to update individual rules without touching the whole skill
- **Source everything** — link to the original article or framework the skill is based on
- **Test before shipping** — paste the SKILL.md raw URL into Claude Code and verify it works

### Installation (for users)

```bash
# Install all skills from this repo
npx skills add ManiClones/agent-skills

# Install a specific skill
npx skills add ManiClones/agent-skills --skill {skill-name}

# Or via skills.sh shorthand
npx skills add https://skills.sh/ManiClones/agent-skills/{skill-name}
```

### After Creating a Skill

1. Update `README.md` — add skill to the skills table
2. Commit with message: `feat({skill-name}): add {one-line description}`
3. The skill is immediately available via `npx skills add ManiClones/agent-skills`

## Repository Maintained By

ManiClones / PHNTM — https://github.com/ManiClones
