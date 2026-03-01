# agent-skills

Plug-and-play skills for AI agents. Built from real sources — viral articles, proven workflows, battle-tested frameworks — packaged as executable instructions your agent can follow directly.

Works with: Claude Code, OpenClaw, Cursor, Amp, Copilot, and any agent that supports the skills ecosystem.

---

## Install

```bash
# Browse and install from this collection
npx skills add ManiClones/agent-skills

# Install a specific skill directly
npx skills add ManiClones/agent-skills --skill ai-customer-analysis

# Or via skills.sh
npx skills add https://skills.sh/ManiClones/agent-skills/ai-customer-analysis
```

After install, your agent automatically knows about the skill. Trigger it by describing what you want in natural language.

---

## Skills

| Skill | What it does | Install |
|-------|-------------|---------|
| [`ai-customer-analysis`](./skills/ai-customer-analysis/) | Verified AI analysis of customer data — prevents hallucinations, cherry-picking, and false confidence in qualitative research | `npx skills add ManiClones/agent-skills --skill ai-customer-analysis` |

---

## How it works

Each skill is a structured `SKILL.md` file your agent loads on demand. The agent reads the skill description at startup (lightweight) and only loads the full instructions when the task matches.

No plugins. No config. No API keys. Just paste the install command and go.

---

## What makes these skills different

Most prompts are generic. These aren't.

Each skill here is extracted from a specific, proven source — a workflow that worked in production, an article written by someone who solved the problem, a framework with real track record. The skill packages what actually matters: the executable steps, the failure modes to avoid, the verification checks.

---

## Contributing

See [AGENTS.md](./AGENTS.md) for the full skill creation guide.

Structure at a glance:
```
skills/
  {skill-name}/
    SKILL.md        ← agent reads this
    AGENTS.md       ← same content, compiled version
    README.md       ← human description
    metadata.json   ← version + abstract
    rules/          ← optional: individual rule files
```

---

Built by [@ManiClones](https://github.com/ManiClones)
