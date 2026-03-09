---
name: x-post-by-articleskills
description: >-
  This is a command-line instruction to install a specific skill package named "10-things-i-wish-i-knew-before-using-openclaw" from the GitHub repository `ManiClones/agent-skills` using the `npx skills add` command. It is intended for users of the Skills CLI tool who want to access a curated list of 1
---

# X post by @ArticleSkills

> Source: https://x.com/ziwenxu_/status/2031064835962667318  
> Created: 2026-03-09

## Overview
This is a command-line instruction to install a specific skill package named "10-things-i-wish-i-knew-before-using-openclaw" from the GitHub repository `ManiClones/agent-skills` using the `npx skills add` command. It is intended for users of the Skills CLI tool who want to access a curated list of 10 lessons learned before using OpenClaw. The target audience is users of AI agent tools, particularly those exploring or evaluating OpenClaw. The outcome enabled is immediate access to a structured knowledge resource without manual research.

## Why This Works
The approach leverages the existing Skills CLI ecosystem to distribute bite-sized, high-value knowledge as installable packages. This bypasses the friction of searching for, copying, or saving external content. By packaging insights as a CLI-installable skill, it ensures version control, easy updates, and integration into existing agent workflows. The use of Twitter (X) as the distribution channel capitalizes on the platform’s viral knowledge-sharing culture among AI tool adopters.

## Core Framework
### Installation Command
- Command: `npx skills add ManiClones/agent-skills --skill 10-things-i-wish-i-knew-before-using-openclaw`
- Package source: `ManiClones/agent-skills` (GitHub repository)
- Skill identifier: `10-things-i-wish-i-knew-before-using-openclaw`
- Tool dependency: `skills` CLI (must be installed and configured)
- Execution method: `npx` (executes package without global installation)

### Knowledge Structure
- Format: 10-item list
- Topic: Lessons learned prior to using OpenClaw
- Delivery format: Installable skill package (implied to be structured as markdown, JSON, or CLI-displayed text)

## Content Strategy & Categories
### Content Type
- Format: “10 Things I Wish I Knew Before…” — a proven viral knowledge format in AI/tech communities
- Category: Pre-use guidance / onboarding checklist / anti-frustration guide
- Structure: Numerical list (exactly 10 items)
- Tone: Reflective, experiential, cautionary

### Content Source
- Authorship: Implied to be authored by @ManiClones (mentioned in tweet)
- Origin: Personal experience with OpenClaw
- Curation: Packaged by @ziwenxu_ for distribution via Skills CLI

## Implementation & Operations
### Workflow
1. User sees tweet with command
2. User runs `npx skills add ManiClones/agent-skills --skill 10-things-i-wish-i-knew-before-using-openclaw` in terminal
3. Skills CLI fetches and installs the skill package from the specified repo
4. Skill becomes available via `skills list` or direct invocation
5. User accesses content via CLI interface

### Tool Dependency
- Requires `skills` CLI to be installed on user’s system
- Requires internet connection to fetch from GitHub
- Requires Node.js environment (since `npx` is used)

### Scaling Strategy
- Scalable via repository branching: new skills can be added as new folders/files in `ManiClones/agent-skills`
- No team or operational overhead beyond maintaining the repo and updating the skill content

## Distribution & Growth
### Channel
- Primary: Twitter (X) — via @ziwenxu_ tweet
- Secondary: GitHub repository `ManiClones/agent-skills` (hosting the skill package)

### Algorithmic Leverage
- Uses viral knowledge format (“10 Things I Wish I Knew…”)
- Tags and mentions (@ManiClones, @ziwenxu_) to trigger network effects
- Low-friction action (single command) encourages sharing and adoption

### Funnel Architecture
1. Awareness: Tweet seen by AI tool users
2. Interest: Curiosity about OpenClaw lessons
3. Action: Run single npx command
4. Adoption: Skill installed and consumed
5. Sharing: User reposts command or recommends skill

## Key Numbers & Metrics
- **Number of lessons:** 10 (explicitly stated in skill name)
- **Command length:** 1 line (exact command provided)
- **Repository owner:** ManiClones (exact username)
- **Skill identifier:** 10-things-i-wish-i-knew-before-using-openclaw (exact string)

## Mistakes to Avoid
- Not having the `skills` CLI installed — command will fail
- Typing the command incorrectly (e.g., misspelling `ManiClones`, `agent-skills`, or the skill name)
- Assuming the skill is available without running the install command
- Expecting graphical interface — skill is CLI-only
- Believing the content is hosted on a website — it is only accessible via CLI after install

## Tools & Resources
- **Skills CLI**: Tool used to install and manage skills (context: likely a CLI framework for AI agent knowledge packages)
- **npx**: Node.js package runner used to execute the skills command without global install
- **GitHub**: Hosting platform for `ManiClones/agent-skills` repository
- **OpenClaw**: AI agent tool referenced in the skill’s content (not a tool used to install, but the subject of the lessons)

## Business Models & Partnerships
- No revenue model, pricing, or partnership structure mentioned
- No indication of monetization, subscriptions, or affiliate links
- Purely a free knowledge-sharing initiative

## Metadata
- **Source:** x.com
- **Type:** playbook
- **Depth:** intermediate
- **Source length:** ~22 words