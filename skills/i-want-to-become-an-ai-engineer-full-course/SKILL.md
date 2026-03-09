# I want to become an AI engineer (full course)

> Source: https://x.com/i/article/2029578615113777152  
> Created: 2026-03-09

## Overview
This is a comprehensive, step-by-step engineering curriculum for becoming an AI engineer in 2026, moving beyond superficial prompt engineering to master the full AI system stack: Prompt Engineering, Context Engineering, and Intent Engineering. It is for individuals seeking to build scalable, autonomous, enterprise-grade AI systems—not just chatbot users. The outcome is the ability to design, audit, deploy, and govern AI agents that operate with structural memory, deterministic intent, and tool integration, avoiding catastrophic failures like Klarna’s $60M loss. The article explicitly states that over 40% of agentic AI projects risk outright cancellation by the end of 2027 due to missing governance and structural frameworks, making this knowledge critical for survival in the field.

## Why This Works
The traditional approach of treating AI as a chat interface—optimizing solely through better wording—is obsolete and dangerously inadequate. Industry projections confirm that 40% of agentic AI projects will fail by 2027 due to lack of governance and structural frameworks. The core insight is that AI systems are no longer tools to be prompted—they are autonomous agents requiring architectural design. Prompt engineering alone treats every interaction as an isolated event, which collapses under multi-step workflows, extended timeframes, or dynamic environments. Context Engineering solves this by providing persistent, version-controlled memory and tool access. Intent Engineering solves the deeper problem of misalignment: even a perfectly engineered agent can cause catastrophic damage if its optimization target is wrong (e.g., Klarna’s AI optimized for speed over customer retention). The stack works because it is hierarchical and cumulative: you cannot build intent without context, and you cannot build context without prompt engineering. This layered architecture mirrors software engineering principles—abstraction, modularity, auditability—and transforms AI from a magic box into a provable, maintainable, enterprise-grade system.

## Core Framework

### 1: PROMPT ENGINEERING
Prompt engineering is the foundational layer that manipulates the probabilistic distribution of the model’s next-token generation. It narrows the model’s output space by controlling syntax, structure, and instruction clarity.

#### In-Context Learning: The Shot Paradigm
- **Zero-shot prompting**: Gives the model a task with no examples. Works for simple, common tasks (e.g., summarize this text, translate this sentence) but routinely fails for domain-specific formatting, complex logic, or precise output structures (e.g., generating a specific JSON schema often results in conversational prose instead).
- **One-shot prompting**: Injects one high-quality input-output example into the prompt. Demonstrates exact output schema and forces attention mechanisms to recognize semantic patterns.
- **Few-shot prompting**: Injects multiple (typically 2–3) high-quality input-output examples. Makes output consistency nearly bulletproof by eliminating ambiguity in tone, structure, and format.
- When zero-shot and few-shot fail, it signals an architectural ceiling: the pre-trained weights cannot synthesize the required output. At this point, you must either fine-tune the model or move to advanced cognitive scaffolding.

#### Cognitive Scaffolding: Making the Model Think Out Loud
- LLMs have no internal monologue; their “thinking” only occurs during token generation.
- Forcing the model to output intermediate reasoning steps creates temporary working memory.
- This is the key insight behind all advanced prompting: externalize reasoning to prevent skipped steps and hallucinations.
- Use explicit `<thinking>` sections with numbered sub-steps to force step-by-step analysis before final output.

#### Building Prompts Like an Engineer
- Professional prompt engineering in 2026 requires building prompts from the bottom up with explicit structural formatting.
- Do not write prompts as continuous prose. Engineer them with delimiters.
- Use XML tags like `<context>`, `<task>`, and `<example>` to strictly separate instructions from data payloads.
- This prevents prompt injection vulnerabilities and ensures proper attention weighting.
- A complete prompt contract includes:
  - A defined role
  - Extensive background context
  - Step-by-step task instructions
  - Explicit output format specifications
  - Few-shot examples
- Audit every prompt for hidden ambiguity: words like “better” or “creative” must be structurally defined.
- If a prompt tries to execute too many tasks at once, split it.

#### Where Prompt Engineering Breaks Down
- Prompt engineering treats every interaction as an isolated event.
- It optimizes wording for immediate tasks only.
- It fails for workflows requiring multi-step execution over extended time (e.g., week-long codebase audit, complex customer dispute, multi-cloud deployment).
- Static prompting collapses under accumulating context and shifting variables.
- Eloquent wording cannot substitute for structural memory and systemic awareness.
- As AI evolved from chat assistants to autonomous agents, the industry realized: context and intent are required for persistence and adaptation.

### 2: CONTEXT ENGINEERING
Context engineering is the systemic practice of designing, optimizing, and maintaining the exact configuration of tokens available to an LLM during inference. It determines what information the AI can immediately access.

#### Core Principle
- Your AI agent is only as capable as the information it can immediately access.
- Prompt engineering = giving a digital worker a specific task.
- Context engineering = providing them with the correct files, historical records, tools, and environmental awareness.

#### Advanced RAG: How Agents Access Real Knowledge
- RAG (Retrieval-Augmented Generation) is the primary mechanism for injecting external, proprietary knowledge into an LLM’s context window.
- Mitigates hallucinations and ensures factual accuracy.
- Early RAG (pre-2025) used rudimentary methods like TF-IDF or BM25—keyword matching without semantic understanding.
- By 2025–2026, context engineering formalized sophisticated chunking and dense transformer-based embeddings (e.g., BERT) that capture semantic meaning (e.g., “feline pets” ≈ “cats”).
- Modern RAG decouples into two stages:
  - **Search Stage (Semantic Matching)**: Uses small, semantically pure text units (100–256 tokens) for high-precision recall and low noise.
  - **Retrieve Stage (Context Understanding)**: Uses larger chunks (1024+ tokens) to ensure logical completeness, background, and sustained reasoning.
- Success depends entirely on chunking logic before vectorization.
- Tools used: Docling (for extracting multi-modal data from PDFs and tables), Chroma, Pinecone.
- Modern RAG systems are evaluated on:
  - **Chunk attribution**: How much retrieved context influenced the model’s output.
  - **Chunk utilisation**: How effectively retrieved chunks were used.

#### Context as Code: The Paradigm Shift
- Treat context as version-controlled software infrastructure.
- Historically, system prompts, data schemas, and API docs were pasted manually or hardcoded as string literals → created amnesia, untraceable hallucinations, zero auditability.
- A 2024 study found programmers spent 11.56% of coding time instructing LLMs with context—nearly equal to the 14.05% spent writing actual code.
- Context as Code applies GitOps principles:
  - Context files, business logic rules, architectural definitions, security boundaries, tool schemas are encoded into structured files (JSON, YAML).
  - Committed directly into version control alongside application code.
- Visible example: Repository-level instruction files like `AGENTS.md` or `context.yaml`.
- Unlike human-readable README.md, these are machine-readable blueprints.
- Standardizes context injection regardless of code style (snake_case vs CamelCase), testing frameworks, or architectural conventions.
- Enables deterministic audits: if an autonomous coding agent introduces a regression, you can review the exact Git commit of the context file that guided it at that timestamp.
- Enables “Context Bundling”: ensures every deployed AI tool across large teams shares identical, version-controlled memory about product vision, tone, edge cases, and compliance requirements.

#### MCP: The Universal Plug for AI Agents
- The Model Context Protocol (MCP) emerged in late 2025 as an open-source standard for routing data and tool access to LLMs.
- Think of MCP as a “USB-C port for AI applications.”
- Standardizes how LLM clients (desktop apps, IDEs, cloud agents) connect to external data sources, enterprise databases, and execution tools.
- Before MCP: developers wrote fragile, custom glue-code for every integration → technical debt.
- MCP eliminates this via a language-agnostic, two-layer architecture:
  - **Data Layer (JSON-RPC 2.0)**:
    - Defines strict protocols for client-server communication.
    - Manages connection lifecycles.
    - Three core primitives:
      - **Resources**: Read-only, file-like data providing foundational context (database schemas, API logs, policy documents).
      - **Tools**: Executable functions the LLM can invoke to take action (SQL queries, shell scripts, API calls).
      - **Prompts**: Reusable, server-side instruction templates for standardised tasks.
    - Supports real-time, bidirectional notifications: if a tool changes or a resource updates, the server notifies the client → context shifts dynamically without human intervention.
  - **Transport Layer**:
    - **STDIO Transport**: For local integrations (e.g., Claude Desktop accessing local codebases). Runs as a local child process over standard I/O. Zero HTTP overhead. Local data stays entirely on the host machine.
    - **HTTP with SSE / Streamable HTTP**: For distributed enterprise deployments (querying remote BigQuery, AWS infrastructure, Sentry). Enables secure, stateless scalability across cloud environments.
- Power of MCP: An MCP Server is entirely agnostic to which LLM interacts with it. Build a tool once, containerise it, and expose it to any current or future AI model that supports the protocol.

### 3: INTENT ENGINEERING
Intent engineering is the structural design of AI systems around goals, constraints, and measurable business outcomes—not surface-level instructions. It sits above context engineering, like strategy above tactics.

#### The Intent Gap: The Klarna Disaster
- Klarna launched an autonomous AI customer service agent in January 2025.
- Handled 2.3 million conversations across 23 markets and 35 languages—equivalent to 853 full-time employees.
- Average ticket resolution dropped from 11 minutes to 2 minutes.
- CEO projected $40M in savings; actual result: $60M in cost reduction.
- Technically flawless.
- By mid-2025, Klarna was forced to rehire human agents.
- Failure: intent engineering failure.
- AI was implicitly told to “resolve tickets fast” and optimised for that metric ruthlessly.
- It could not balance trade-offs: a human agent knows to escalate a highly profitable, 3-year customer’s frustration—even if it slows resolution—to prioritise empathy and long-term retention.
- AI lacked tacit organisational knowledge → intent gap.
- Result: saved $60M but became the “public face of AI gone wrong.”

#### The 7-Component Intent Framework
Intent engineering replaces vague mission statements with machine-readable structural schemas defining decision boundaries, trade-off hierarchies, and escalation triggers.
Each component translates directly into working code (JSON/YAML schemas with conflict resolution protocols and trade-off matrices).

1. **Primary Objective**: The core business outcome the agent must achieve (e.g., “maximise customer retention”).
2. **Success Criteria**: Measurable, binary indicators of success (e.g., “customer does not churn within 30 days of resolution”).
3. **Constraints**: Hard boundaries the agent must never violate (e.g., “never disclose PII,” “never override manual override flag”).
4. **Trade-Off Hierarchy**: Explicit priority order when objectives conflict (e.g., “retention > speed > cost”).
5. **Escalation Triggers**: Conditions under which the agent must hand off to a human (e.g., “customer mentions legal action,” “sentiment score < -0.8 for 3 consecutive messages”).
6. **Audit Requirements**: What data must be logged for compliance and debugging (e.g., “log all decisions with timestamp, context hash, intent rule invoked”).
7. **Feedback Loops**: How the agent learns from outcomes (e.g., “if human overrides decision, log reason and retrain intent model weekly”).

- In Software-Defined Networking environments, structured intent prompts explicitly separate queuing intents from forwarding rules, preventing the AI from accidentally blocking critical infrastructure while optimising traffic flow.

#### Vibe Coding vs. Deterministic Intent
- **Vibe Coding**: Coined in early 2025. Developers use natural language to vaguely describe the “vibe” of an application and let LLMs generate architecture, APIs, boilerplate.
- Powerful for rapid prototyping; empowers non-technical product managers.
- Creates immense systemic risk in enterprise environments: brittle, untraceable codebases riddled with latent vulnerabilities.
- Nobody can fully trace, trust, or maintain it.
- Enterprise repositories flood with bot-generated noise and technical debt.
- **Intent Engineering**: Professional antidote.
- Forces translation of informal “vibes” into strict prompt contracts and intent schemas.
- Chaining the AI’s generative power to verifiable logic, organisational strategy, and maintainable standards.
- Your role shifts from writing code to orchestrating verifiable intent pipelines.

### 4: BECOMING AN AI ENGINEER

#### 1: LEARNING TO PROMPT ENGINEER

##### Skill 1: Structural Formatting with Delimiters
- **What to learn**: Stop writing prompts as casual paragraphs. Use explicit structural delimiters: XML tags, markdown headers, or clear section markers to separate instructions from data.
- **Why it matters**: Mixing instructions and data forces the model to guess where “what I should do” ends and “what I should work with” begins → root cause of inconsistent outputs.
- **The mistake**: Writing prompts like emails: “Hey, can you look at this data and maybe summarise it in a nice format?” → zero structural guidance, maximum room to hallucinate.
- **How to practise**: Take any prompt used in the last week. Rewrite it using XML tags to separate role, context, task, format, and examples. Run both versions and compare outputs.
- **Prompt Template - Structural Formatting**:
  ```
  <role>You are a senior data analyst.</role>
  <context>[Insert data here]</context>
  <task>Analyse the sales trends and identify the top 3 underperforming regions.</task>
  <format>Return a JSON object with keys: top_3_regions, trend_summary, recommendation.</format>
  <example>
    Input: [sample data]
    Output: {"top_3_regions": ["Southeast", "Midwest", "Northeast"], "trend_summary": "Sales declined 18% QoQ...", "recommendation": "Reallocate marketing budget to Northwest."}
  </example>
  ```
- **Why this prompt works**: Every section has a single, clear purpose. Model’s attention mechanisms can cleanly weight role against task against data. No ambiguity.

##### Skill 2: Few-Shot Demonstrations
- **What to learn**: Instead of describing what you want, show the model with one or more complete input-output examples.
- **Why it matters**: Language is ambiguous. “Write it in a professional tone” means different things to you and the model. A single example eliminates the gap. Three make it bulletproof.
- **The mistake**: Providing examples that are too short or too simple. Examples must match the complexity of the actual task.
- **How to practise**: Pick a recurring output format (email responses, code reviews, data summaries). Write 2–3 “gold standard” examples. Build them into a reusable prompt template.
- **Prompt Template - Few-Shot with Quality Control**:
  ```
  <role>You are a customer support agent for a premium SaaS company.</role>
  <context>Customer email: “I’ve been a customer for 3 years and my billing just doubled without warning.”</context>
  <task>Write a response that is empathetic, professional, and includes a clear action plan.</task>
  <format>One paragraph, 100–150 words. Include: apology, explanation, solution, timeline, offer of direct contact.</format>
  <example>
    Input: “My subscription just went up $50. This is unacceptable.”
    Output: “I’m truly sorry for the surprise increase. This was due to a planned upgrade in our premium features. We’ve reversed the charge and will notify you 14 days before any future changes. You can reach me directly at [number] if you’d like to discuss options.”
  </example>
  <example>
    Input: “I paid for annual but got charged monthly. Fix this.”
    Output: “Thank you for bringing this to our attention. We’ve identified a system error that incorrectly billed you monthly instead of annually. Your account has been corrected, and a $120 refund has been processed. You’ll receive confirmation within 3 business days. Please reply if you don’t see it.”
  </example>
  ```
- **Why this prompt works**: Model doesn’t interpret vague adjectives like “empathetic” or “professional.” It has two concrete demonstrations showing tone, structure, length, specificity. Format reinforces pattern → output is remarkably consistent.

##### Skill 3: Cognitive Scaffolding (Chain-of-Thought)
- **What to learn**: Force the model to externalise its reasoning step-by-step before giving a final answer.
- **Why it matters**: LLMs skip critical intermediate steps and arrive at plausible-sounding but incorrect conclusions. CoT forces those steps into the open.
- **The mistake**: Using CoT for simple tasks (summarise this paragraph) and not using it for complex tasks (analyse financial data and recommend strategy). CoT adds latency and token cost—use only when reasoning complexity demands it.
- **How to practise**: Take a complex analytical question where the answer was mediocre. Rebuild the prompt with explicit CoT instructions and a thinking section. Compare depth and accuracy.
- **Prompt Template - Chain-of-Thought Analysis**:
  ```
  <role>You are a financial analyst.</role>
  <context>[Insert quarterly financial data]</context>
  <task>Analyse the data and recommend whether to invest in Product X.</task>
  <thinking>
    Step 1: Identify revenue growth trends for Product X over the last 4 quarters.
    Step 2: Compare cost of goods sold (COGS) to industry benchmarks.
    Step 3: Evaluate customer retention rate and churn risk.
    Step 4: Assess competitive positioning and market share changes.
    Step 5: Synthesise findings into a single investment recommendation.
  </thinking>
  <format>Return a JSON object with keys: analysis, recommendation, confidence_score (0–1).</format>
  ```
- **Why this prompt works**: Explicit thinking section with numbered sub-steps prevents jumping to conclusions. Each step forces processing of a different dimension. Separation between `<thinking>` and final recommendation allows auditing—if conclusion doesn’t match analysis, you see exactly where logic broke down.

##### Skill 4: Meta Prompting (Making the AI Improve Its Own Prompts)
- **What to learn**: Instruct the model to generate, critique, and refine prompts for you based on your goals.
- **Why it matters**: You understand your domain. The model understands its own interpretive patterns. Meta prompting combines both → accelerates prompt development dramatically.
- **Prompt Template - Meta Prompt Generator**:
  ```
  <role>You are a senior prompt engineer.</role>
  <context>My goal: I want an AI to generate compliance reports for GDPR data processing activities.</context>
  <task>Generate 3 prompt variations for this task. Then critique each one for ambiguity, missing structure, or risk of hallucination. Finally, return the best version with XML delimiters.</task>
  <format>Return a JSON object with keys: variations (array of 3 prompts), critique (array of 3 critiques), best_prompt (string with XML tags).</format>
  ```
- **Why this prompt works**: Turns the model into your prompt engineering co-pilot. Critique step forces audit of its own work → catches ambiguities you might miss.

#### 2: LEARNING TO CONTEXT ENGINEER

##### Skill 1: Context Auditing - What Does Your AI Actually Know?
- **What to learn**: Before engineering context, audit it. Systematically map knowledge gaps between what your AI has and what it needs.
- **Why it matters**: Every hallucination, inconsistent output, or “AI doesn’t understand my business” complaint traces back to a context failure. The model is just uninformed.
- **The mistake**: Adding more context when the real problem is wrong context. Dumping your entire company wiki drowns signal in noise. Context engineering is about precision, not volume.
- **How to practise**: Take a task where AI consistently underperforms. Instead of tweaking wording, ask the model: “What information is missing that would make this output accurate?”
- **Prompt Template - Context Gap Analysis**:
  ```
  <role>You are a context auditor for an AI system.</role>
  <context>AI output: “The product launch date is June 15.” But the real date is July 1.</context>
  <task>Identify the 3 most likely missing pieces of context that caused this hallucination. Be specific. Format: JSON with keys: missing_context_1, missing_context_2, missing_context_3.</task>
  <format>Return a JSON object with exactly 3 keys. Each value must be a specific document, database field, or policy name—not vague statements like “timeline info.”</format>
  ```
- **Why this prompt works**: Turns the model into a diagnostic tool. Instead of guessing why outputs are inconsistent, you get a structured report telling you exactly what to fix. Specificity requirement prevents vague feedback.

##### Skill 2: Building Context Files (Context as Code)
- **What to learn**: Encode business context, rules, and standards into structured, reusable files (JSON/YAML) that any AI tool can consume.
- **Why it matters**: If you’re pasting the same context into chat windows repeatedly, you’re doing manual labour that should be automated. Context files make knowledge persistent, version-controlled, and shareable.
- **How to practise**: Start with a single workflow where you use AI regularly. Document everything the AI needs to know in a structured file. Reference that file in prompts instead of pasting raw context.
- **Prompt Template - Generate Your First AGENTS.md File**:
  ```
  <role>You are an AI systems architect.</role>
  <context>Our team uses Python, pytest, and follows PEP8. Our product is a SaaS analytics dashboard. We use Stripe for billing. Our tone is professional but approachable. We never mention competitors. Our security policy requires all PII to be masked.</context>
  <task>Generate an AGENTS.md file in Markdown format that an AI agent can use as its default context when working on this codebase.</task>
  <format>Use Markdown headers: ## Code Standards, ## Product Context, ## Communication Guidelines, ## Security Rules. Each section must be a bulleted list.</format>
  ```
- **Why this prompt works**: Bootstraps your first context file from plain language. Once generated, refine it, commit to repo, and every AI interaction on that project starts with consistent, comprehensive foundation. No more “AI doesn’t understand our conventions.”

##### Skill 3: RAG Pipeline Design
- **What to learn**: When context is too large for a single prompt (always true in enterprise), build a RAG pipeline that dynamically retrieves only the most relevant context chunks for each query.
- **Why it matters**: Context windows are large but not infinite. Stuffing everything in wastes tokens, increases noise, degrades output quality. RAG delivers laser-focused context.
- **How to practise**: Start by understanding how chunking affects retrieval. Use this prompt to design your chunking strategy before writing code.
- **Prompt Template - RAG Architecture Designer**:
  ```
  <role>You are a RAG systems architect.</role>
  <context>We have 10,000 PDFs of regulatory compliance documents, 500 API logs, and 200 internal policy wikis. Our users ask questions like: “What’s the retention period for EU customer data under GDPR Article 17?”</context>
  <task>Design a RAG pipeline. Specify: chunk size for search stage, chunk size for retrieve stage, embedding model, vector database, and retrieval strategy (e.g., hybrid keyword + semantic).</task>
  <format>Return a JSON object with keys: search_chunk_size, retrieve_chunk_size, embedding_model, vector_db, retrieval_strategy.</format>
  ```
- **Why this prompt works**: Forces systematic design before implementation. Ensures chunking logic aligns with use case.

##### Skill 4: MCP Server Design
- **What to learn**: The Model Context Protocol is how you give AI agents secure, standardised access to data and tools. Essential for building AI systems that interact with real-world infrastructure.
- **How to practise**: Before writing server code, use this prompt to design your MCP server’s capability schema.
- **Prompt Template - MCP Server Blueprint**:
  ```
  <role>You are an MCP server designer.</role>
  <context>We need an AI agent to query our PostgreSQL database, run shell scripts to deploy code, and read our company’s security policy PDFs.</context>
  <task>Define the MCP server’s Data Layer primitives: Resources, Tools, Prompts. For each, specify name, description, input schema, output schema, and transport protocol (STDIO or HTTP).</task>
  <format>Return a JSON object with keys: resources (array), tools (array), prompts (array). Each array item must have: name, description, input_schema (JSON Schema), output_schema (JSON Schema), transport.</format>
  ```
- **Why this prompt works**: Forces structured, reusable, protocol-compliant design before coding. Ensures compatibility with any LLM client.

#### 3: LEARNING TO INTENT ENGINEER

##### Skill 1: Outcome Definition - Shifting from Outputs to Outcomes
- **What to learn**: Tell the AI what to achieve, not what to produce. An instruction generates output. An intent generates outcomes.
- **Why it matters**: “Write me a report” → AI produces a report. But will it serve the business purpose? Without outcome definition, AI is guessing.
- **The mistake**: Defining success by format (“write 1000 words”) instead of impact (“this report must enable the CFO to approve or reject the budget within 5 minutes of reading it”). Format is a constraint. Impact is the intent.
- **How to practise**: Take your most important recurring AI task. Rewrite the prompt replacing every format instruction with an outcome instruction. Ask: “If this output was perfect in format but failed to achieve its purpose, would I be satisfied?”
- **Prompt Template - Outcome-Driven Task Definition**:
  ```
  <role>You are a business intelligence analyst.</role>
  <intent>The CFO must be able to approve or reject the Q3 budget within 5 minutes of reading this report.</intent>
  <context>[Insert financial data]</context>
  <task>Generate a report that highlights only the 3 most critical budget variances and their business impact.</task>
  <format>One-page PDF. Use bold headers for variances. Include: variance %, dollar impact, root cause, recommendation. No charts. No fluff.</format>
  <success_criteria>CEO can make decision in ≤5 minutes without asking follow-up questions.</success_criteria>
  ```
- **Why this prompt works**: The `<intent>` block changes what the AI optimises for. Instead of producing a generically “good” report, it’s calibrated to a specific audience, decision, and time constraint. Success criteria give the AI self-evaluation checkpoints.

##### Skill 2: The Full 7-Component Intent Schema
- **What to learn**: How to build a complete, machine-readable intent configuration that governs an autonomous agent’s entire decision-making process.
- **Why it matters**: This is the difference between deploying an AI that completes tasks and deploying an AI that operates as a governed, accountable member of your organisation.
- **How to practise**: Design a full intent schema for a real workflow. Use this template to generate it, then refine iteratively as you observe the agent’s behaviour.
- **Prompt Template - Full Intent Schema Generator**:
  ```
  <role>You are an AI governance engineer.</role>
  <context>We are deploying an AI agent to handle customer refund requests for our e-commerce platform. The agent must balance speed, compliance, and customer satisfaction.</context>
  <task>Generate a complete 7-component intent schema in YAML format.</task>
  <format>YAML with keys: primary_objective, success_criteria, constraints, trade_off_hierarchy, escalation_triggers, audit_requirements, feedback_loops.</format>
  ```
- **Why this prompt works**: Generates a complete, deployable intent configuration from plain language. YAML output is immediately usable in real systems—not just a planning document, but actual infrastructure code.

##### Skill 3: Trade-Off Hierarchies - Teaching AI to Make Hard Decisions
- **What to learn**: Explicitly encode the priority order your AI should follow when objectives conflict.
- **Why it matters**: In the real world, “fast” and “thorough” conflict. “Cheap” and “high-quality” conflict. “Honest” and “tactful” conflict. Without explicit hierarchy, AI defaults to easiest-to-optimize objective—almost never the one you care about most.
- **Prompt Template - Trade-Off Matrix**:
  ```
  <role>You are an AI decision architect.</role>
  <context>Our AI handles customer complaints. We want to minimise resolution time, maximise customer satisfaction, and minimise cost.</context>
  <task>Define a trade-off hierarchy as a ranked list of priorities. Then define a scoring system: if resolution time increases by 10%, how much must satisfaction increase to justify it? If cost increases by $5, how much must satisfaction increase?</task>
  <format>Return a JSON object with keys: hierarchy (array of strings), tradeoff_rules (array of objects with: metric_1, metric_2, threshold, required_change).</format>
  ```
- **Example output**:
  ```json
  {
    "hierarchy": ["customer_satisfaction", "resolution_time", "cost"],
    "tradeoff_rules": [
      {
        "metric_1": "resolution_time",
        "metric_2": "customer_satisfaction",
        "threshold": "10% increase",
        "required_change": "15% increase"
      },
      {
        "metric_1": "cost",
        "metric_2": "customer_satisfaction",
        "threshold": "$5 increase",
        "required_change": "10% increase"
      }
    ]
  }
  ```

##### Skill 4: Building Audit Trails - Making Every AI Decision Traceable
- **What to learn**: Design systems that log every autonomous decision with enough detail to reconstruct exactly why it happened.
- **Why it matters**: When an AI makes a mistake (and it will), you need to diagnose the root cause. Without audit trails, you’re guessing. With them, you can trace the exact chain of context, intent rules, and reasoning that led to failure, fix the specific component, and deploy with confidence.
- **Prompt Template - Audit Chain Architecture**:
  ```
  <role>You are an AI compliance engineer.</role>
  <context>Our AI agent approves loan applications. It must be auditable for regulatory compliance.</context>
  <task>Design an audit trail system. Specify: what data must be logged, how it’s stored, how it’s linked to context and intent, and how it’s queried.</task>
  <format>Return a JSON object with keys: log_fields (array), storage_format, context_linkage, intent_linkage, query_interface.</format>
  ```
- **Example output**:
  ```json
  {
    "log_fields": ["timestamp", "user_id", "input_prompt_hash", "context_hash", "intent_rule_triggered", "decision", "confidence_score", "human_override_flag"],
    "storage_format": "PostgreSQL table with JSONB column for metadata",
    "context_linkage": "Each log entry includes SHA-256 hash of context.yaml file used",
    "intent_linkage": "Each log entry includes name of intent schema version (e.g., v2.1)",
    "query_interface": "REST endpoint: GET /audit?agent_id=123&start=2026-03-01&end=2026-03-31"
  }
  ```

## Content Strategy & Categories
- **Prompt Templates**: Structured, reusable templates for each skill (e.g., Structural Formatting, Few-Shot, CoT, Meta Prompting, Context Gap Analysis, AGENTS.md generation, RAG Designer, MCP Blueprint, Intent Schema Generator, Trade-Off Matrix, Audit Chain).
- **Framework Diagrams**: Implicitly referenced (e.g., “infographic for you!”) but not included in text—assumed to be visual aids accompanying the article.
- **Case Studies**: Klarna disaster (2025) as a canonical example of intent failure.
- **Tool-Driven Examples**: Docling, Chroma, Pinecone, Claude Desktop, NotebookLM.
- **Code Examples**: XML-tagged prompts, JSON/YAML schemas, GitOps-style context files (`AGENTS.md`, `context.yaml`).
- **Auditing Prompts**: Prompts designed to make the AI diagnose its own failures (e.g., “What’s missing?”).
- **Meta-Prompts**: Prompts that generate other prompts.

## Implementation & Operations
- **Team Structure**: Not explicitly defined, but implied roles:
  - **Prompt Engineer**: Designs and audits prompts.
  - **Context Architect**: Builds and maintains RAG pipelines, context files, MCP servers.
  - **Intent Designer**: Defines 7-component schemas, trade-off hierarchies, audit trails.
  - **AI Governance Officer**: Oversees version control, compliance, auditability.
- **Daily Workflows**:
  - Prompt engineers use templates daily