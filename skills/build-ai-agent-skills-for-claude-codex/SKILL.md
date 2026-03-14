---
name: build-ai-agent-skills-for-claude-codex
description: >-
  Operational playbook for building, deploying, and managing AI agent skills using the open skills standard. Use when creating, debugging, or optimizing skills for Claude, Codex, or other AI agents. Use when user asks about skill structure, triggering accuracy, skills.sh CLI, progressive disclosure, meta-messages, or enterprise skill deployment.
---

# the complete guide to building skills for claude/codex

> Source: https://x.com/i/article/2020822118695665664
> Created: 2026-03-14

## Overview
This skill helps you build, test, and deploy AI agent skills using the open skills standard — transforming generic AI interactions into specialized, 24/7 automated employees. Use this when you need to encode expert knowledge into AI agents for document creation, workflow automation, or MCP-enhanced workflows. It enables consistent, high-quality outputs that outperform basic prompting, reduces repetitive manual work, and scales organizational knowledge across teams. The skill standard is adopted by Anthropic, OpenAI, Microsoft, and tools like Vercel’s skills.sh CLI, supporting 35+ AI agents including Claude Code, Cursor, Codex, and Windsurf.

## Instructions
1. **Identify your use case** — Select one of these three categories with 2–3 concrete scenarios:
   - **Document & asset creation**: e.g., generate professional web interfaces, presentations, or designs (e.g., frontend-design skill).
   - **Workflow automation**: e.g., multi-step processes like building new skills (e.g., skill-creator skill).
   - **MCP enhancement**: e.g., automate GitHub pull request reviews using Sentry error data.

2. **Define success criteria** — Set measurable targets:
   - Triggering accuracy: Skill must load on 90% of relevant queries.
   - Tool efficiency: Complete workflows in X tool calls (compare to baseline).
   - Error rate: Zero failed API calls per workflow.
   - Consistency: Same task yields similar outputs across sessions.

3. **Write effective descriptions** — Structure the YAML `description` field using:
   - Trigger phrases users actually say.
   - Mention relevant file types (e.g., `.pdf`, `.xlsx`).
   - Clearly state the problem solved (e.g., “Automatically applies corporate branding to Word documents”).

4. **Structure your SKILL.md file**:
   - Use YAML frontmatter for metadata (name, description, allowed-tools).
   - Use Markdown body for step-by-step instructions, examples, and best practices.
   - Organize critical instructions under `## CRITICAL` headers.
   - Keep instructions concise with bullet points.

5. **Implement progressive disclosure**:
   - **Level 1 (always loaded)**: YAML frontmatter (name, description) injected into system prompt.
   - **Level 2 (loaded when relevant)**: SKILL.md body content loaded only when agent determines relevance.
   - **Level 3 (loaded as needed)**: Files in `scripts/`, `references/`, and `assets/` directories accessed only when explicitly referenced.

6. **Use the two-message pattern**:
   - Send user-visible messages (`isMeta: false`) for conversation transparency.
   - Send meta messages (`isMeta: true`) containing full skill instructions — never shown to users.

7. **Test iteratively**:
   - Test triggering: Does the skill load on correct queries? Avoid false positives.
   - Test functionality: Does it produce correct outputs consistently?
   - Test performance: Is it better than the baseline (no skill)? Measure time, errors, and output quality.

8. **Use the skills.sh CLI**:
   - Install: Run `npm install -g skills.sh`.
   - Use: `skills.sh install <skill-name>` to install from marketplace.
   - Detects 35+ AI agents (Claude Code, Cursor, Codex, Open Code, Windsurf, etc.).
   - Provides popularity rankings, categorized browsing, and search.

9. **Apply advanced patterns**:
   - **Context-aware tool selection**: Dynamically choose tools based on context (e.g., use Google Drive for `.docx`, Dropbox for `.pdf`).
   - **Domain-specific intelligence**: Embed specialized knowledge (e.g., financial compliance rules, accessibility guidelines).
   - **Iterative refinement**: For quality-critical outputs, use feedback loops (e.g., generate → review → revise → finalize).

10. **Enforce security and trust**:
    - Only use skills from trusted sources: Anthropic-created, self-created, or verified partner skills.
    - Review community skills before installation.
    - Restrict capabilities via YAML: `allowed-tools: [“pdf-fill”, “excel-formula”]`.
    - Understand environment restrictions:
      - `claude.ai`: Restricted packages, limited network.
      - `claude code`: Full network access, local to user’s machine.
      - `api`: Runs in code execution container with configurable permissions.

11. **For teams and organizations**:
    - Identify high-value workflows where team members repeatedly explain processes to AI.
    - Create a Git-based skills repository for version control and sharing.
    - Standardize on the open skills spec for portability.
    - Assign ownership and schedule skill maintenance (like code updates).

12. **For enterprises**:
    - Use admin controls to provision skills workspace-wide.
    - Partner with SaaS vendors (Atlassian, Notion, Figma) for official skills.
    - Develop compliance skills encoding regulatory rules (finance, healthcare, legal).
    - Measure ROI: Track time savings, error reduction, and output consistency.

13. **Troubleshoot common issues**:
    - **Skill won’t trigger**: Revise description to include specific user phrases. Test variations.
    - **Skill triggers too often**: Add negative triggers (e.g., “do not use for simple data exploration”).
    - **Instructions not followed**: Put critical steps under `## CRITICAL`, use bullet points, bundle executable scripts for deterministic validation.
    - **MCP connection failures**: Verify MCP server is connected, check API keys, test MCP independently, ensure tool names match server docs exactly (case-sensitive).

## Examples
- When the user asks about “create a landing page” → Load the frontend-design skill to generate professional, modern UI with proper spacing, color theory, and accessibility.
- When the user asks about “fill out this PDF form” → Load the PDF form-filling skill to programmatically complete fillable fields using template rules.
- When the user asks about “review this GitHub PR” → Load the Sentry code review skill to analyze error logs and auto-suggest fixes.
- When the user asks about “make this PowerPoint brand-compliant” → Load the PowerPoint skill to auto-apply corporate fonts, colors, and slide structure.
- When the user says “I need to generate a quarterly report” → Load the enterprise document creation skill to auto-generate Word/Excel/PDF with correct formulas and branding.
- When the user says “help me build a new skill” → Load the skill-creator skill to scaffold a new SKILL.md file in 15–30 minutes.

## Key Details
- skills are not prompts — they are dynamic, organized packages that load context on demand.
- launched by Anthropic in October 2025; evolved into open standard adopted by OpenAI and Microsoft.
- skills.sh CLI released in early 2026; supports 35+ AI agents.
- skill structure: YAML frontmatter + SKILL.md body + optional scripts/, references/, assets/ directories.
- progressive disclosure: 3 levels — YAML (always loaded), SKILL.md (loaded when relevant), linked files (loaded as needed).
- two-message pattern: user-visible (`isMeta: false`) and meta (`isMeta: true`) messages.
- triggering accuracy target: 90% of relevant queries.
- enterprise document tasks: reduced from 30+ minutes to under 3 minutes.
- security: skills run in controlled environments; `claude.ai` has restricted access, `claude code` has full local access, API runs in container.
- allowed-tools: configurable in YAML to restrict API access.
- skill-creator skill: scaffolds new skills in 15–30 minutes.
- community skills: must be reviewed before installation.
- skill marketplaces: emerging commercial platforms for industry-specific skills.
- recursive improvement: AI-assisted skill creation (e.g., skill-creator skill builds new skills).

## Framework
### Progressive Disclosure System
1. **Level 1: YAML Frontmatter**  
   - Always injected into system prompt.  
   - Contains: `name`, `description`.  
   - Purpose: Enable agent to decide whether to load full skill without token waste.

2. **Level 2: SKILL.md Body**  
   - Loaded only when agent determines relevance.  
   - Contains: step-by-step instructions, examples, best practices.  
   - Purpose: Provide detailed guidance without constant context burden.

3. **Level 3: Linked Resources**  
   - Files in `scripts/`, `references/`, `assets/` directories.  
   - Loaded only when explicitly referenced in SKILL.md.  
   - Purpose: Minimize token usage; keep heavy assets separate.

### Two-Message Pattern
- **User-visible message** (`isMeta: false`): Appears in chat transcript.  
- **Meta message** (`isMeta: true`): Sent to API, hidden from user. Contains full skill instructions.  
- Purpose: Maintain UX clarity while enabling complex internal logic.

### Trust Model
- **Anthropic-created**: Professionally maintained, verified.
- **Self-created**: Full control, no external risk.
- **Partner skills**: From verified commercial vendors (e.g., Atlassian, Figma).
- **Community skills**: Must be manually reviewed before installation.

### Skill Categories
1. **Document & Asset Creation** — e.g., frontend-design, PowerPoint, PDF form-filling.
2. **Workflow Automation** — e.g., skill-creator, multi-step process enforcer.
3. **MCP Enhancement** — e.g., Sentry code review, GitHub PR analyzer.

## Mistakes to Avoid
- **Using vague descriptions**: Leads to poor triggering. → Fix: Include specific user phrases and file types.
- **Overloading SKILL.md**: Makes instructions hard to follow. → Fix: Use bullet points, put critical steps under `## CRITICAL`.
- **Relying solely on natural language for validation**: Leads to inconsistent outputs. → Fix: Bundle executable scripts for deterministic results.
- **Installing unreviewed community skills**: Risk of malicious code execution. → Fix: Always audit before installing.
- **Ignoring environment restrictions**: Assuming full network access everywhere. → Fix: Check if running on `claude.ai` (restricted) vs. `claude code` (full access).
- **Not testing triggering accuracy**: Skill loads too often or never. → Fix: Test 20+ user phrasings and refine description.
- **Assuming skills work out of the box**: Requires iterative testing. → Fix: Test on single challenging task first, then generalize.

## Tools & Resources
- **skills.sh CLI**: Command-line tool for installing, managing, and discovering skills. Supports 35+ agents. Install via `npm install -g skills.sh`.
- **Anthropic’s skill-creator skill**: Built-in skill in Claude.ai and Claude Code that scaffolds new SKILL.md files in 15–30 minutes.
- **Frontend-design skill**: Example skill for generating professional web interfaces.
- **Sentry code review skill**: MCP-enhanced skill for analyzing GitHub PRs using error monitoring data.
- **Enterprise document skills**: Pre-built skills for PowerPoint, Excel, Word, PDF (branding, templates, formulas, form filling).
- **Skills marketplace**: Emerging commercial platforms for purchasing industry-specific skills (e.g., finance, legal, healthcare).
- **GitHub repositories**: Organizational skills should be version-controlled in Git for sharing and iteration.

## Metrics & Numbers
- **Triggering accuracy target**: 90% of relevant queries.
- **Time savings (enterprise docs)**: 30+ minutes → under 3 minutes.
- **AI agents supported by skills.sh**: 35+ (including Claude Code, Cursor, Codex, Open Code, Windsurf).
- **Skill-creator scaffold time**: 15–30 minutes.
- **Skill structure components**: 3 levels of progressive disclosure.
- **Skill file structure**: 1 core file (`SKILL.md`) + optional directories (`scripts/`, `references/`, `assets/`).
- **Security environment types**: 3 (claude.ai, claude code, API container).
- **Skill categories**: 3 (document/asset, workflow, MCP enhancement).

## Implementation Guide
### For Individual Developers
- Start small: Build a skill for a task you do repeatedly (e.g., formatting emails, generating READMEs).
- Use the skill-creator skill to scaffold your first skill in 15–30 minutes.
- Install and study popular skills from skills.sh to learn patterns.
- Test each skill on 5–10 real user queries before deployment.

### For Teams
- Identify 3–5 high-value workflows where AI is repeatedly given the same instructions.
- Create a shared Git repository for organizational skills.
- Assign skill owners for maintenance and updates.
- Run monthly skill review sessions: test performance, update triggers, remove obsolete skills.
- Standardize on open skills spec to ensure portability across platforms.

### For Enterprises
- Use admin dashboards to deploy approved skills workspace-wide.
- Integrate official vendor skills (Notion, Figma, Atlassian) into workflows.
- Build compliance skills for regulated domains (e.g., HIPAA, GDPR, SOX).
- Track ROI metrics: time saved per task, error rate reduction, output consistency score.
- Establish a skills governance team: review, approve, and audit all skills before deployment.
- Plan for recursive improvement: pilot AI-assisted skill creation (e.g., use skill-creator to generate new skills from natural language).

## Metadata
- **Source:** x.com
- **Type:** playbook
- **Depth:** comprehensive
- **Source length:** ~1957 words