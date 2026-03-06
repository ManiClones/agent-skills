# I want to become an AI engineer (full course)

> Source: https://x.com/i/article/2029578615113777152

## What is this?
This skill teaches the complete engineering stack for building reliable, scalable, and aligned AI systems — moving beyond superficial prompt engineering to master Context Engineering and Intent Engineering. It solves the problem of AI systems that appear functional but fail at scale due to poor memory, unstructured knowledge, or misaligned objectives — common causes of project cancellation, hallucinations, and operational disasters like Klarna’s $60M failure.

## When to use
- You are building autonomous AI agents that run multi-step workflows (e.g., code audits, customer service, cloud deployments)
- Your AI outputs are inconsistent, hallucinatory, or fail under real-world data volume
- You need to deploy AI across teams with shared knowledge and governance
- You are transitioning from chat-based AI use to production-grade AI systems
- Your organization has experienced AI failures due to misaligned incentives (e.g., optimizing speed over customer retention)
- You are responsible for auditing, maintaining, or scaling AI systems in enterprise environments

## Core Concepts
1. **Prompt Engineering** — The micro-syntax layer: using structured delimiters, few-shot examples, and chain-of-thought to guide token generation. It controls immediate instruction but is insufficient alone.
2. **Context Engineering** — The infrastructure layer: designing, versioning, and retrieving persistent, high-quality knowledge for the AI using RAG pipelines, chunking strategies, and Context as Code (e.g., AGENTS.md files).
3. **Model Context Protocol (MCP)** — A universal standard for AI-agent communication: defines structured access to Resources (data), Tools (functions), and Prompts (templates) via JSON-RPC 2.0 over STDIO or HTTP/SSE.
4. **Intent Engineering** — The strategy layer: encoding organizational goals, trade-off hierarchies, and outcome metrics into machine-readable schemas (JSON/YAML) to align AI behavior with business objectives.
5. **The AI Engineering Stack** — A layered hierarchy: Prompt → Context → Intent. Each layer builds on the one below. Skipping layers leads to brittle, unscalable, or dangerous systems.
6. **Context as Code** — Treating AI context (system prompts, rules, schemas) as version-controlled software: stored in Git, auditable, reusable, and shareable across teams.
7. **Outcome vs Output** — Distinguishing between what the AI produces (format, length) and what it must achieve (business impact, decision enablement).
8. **The Intent Gap** — When an AI is technically perfect but optimizes for the wrong metric (e.g., speed over customer satisfaction), leading to catastrophic misalignment.

## Step-by-Step
1. **Start with Prompt Engineering**
   - Rewrite every prompt using XML delimiters: `<role>`, `<context>`, `<task>`, `<format>`, `<example>`
   - Replace vague instructions (“be professional”) with concrete few-shot examples (2–3 input-output pairs)
   - For complex tasks, force chain-of-thought: add `<thinking>` section with numbered steps before final output

2. **Build Context as Code**
   - Identify a recurring AI task (e.g., code review, report generation)
   - Create a file named `AGENTS.md` or `context.yaml` containing all necessary background: company tone, formatting rules, tool access, edge cases
   - Commit this file to your project’s Git repository
   - Reference it in prompts with: “Use the context from AGENTS.md”

3. **Design a RAG Pipeline**
   - Split your source documents into two chunk types:
     - Small chunks (100–256 tokens) for semantic search
     - Large chunks (1024+ tokens) for context understanding
   - Use vector embeddings (e.g., BERT) to encode chunks, not keyword matching
   - Store chunks in a vector database (Chroma, Pinecone)
   - Use Docling to extract tables and PDFs into clean text

4. **Implement MCP Server**
   - Define three core primitives for your AI agent:
     - **Resources**: Read-only data (e.g., API docs, policy PDFs)
     - **Tools**: Executable functions (e.g., `run_sql(query)`, `send_email(to, subject, body)`)
     - **Prompts**: Reusable templates (e.g., `summarize_customer_feedback`)
   - Expose them via JSON-RPC 2.0 over STDIO (local) or HTTP/SSE (cloud)
   - Use a language-agnostic server (Python, Node.js) that any LLM client can connect to

5. **Define Intent Schema**
   - For any autonomous agent, create a YAML file with these 7 components:
     - **Primary Objective**: What the agent must achieve (e.g., “Reduce customer churn”)
     - **Success Metrics**: Measurable KPIs (e.g., “Increase NPS by 10 points in 30 days”)
     - **Constraints**: Hard limits (e.g., “Never disclose PII”)
     - **Trade-off Hierarchy**: Priority order (e.g., “Accuracy > Speed > Cost”)
     - **Escalation Triggers**: When to hand off to humans (e.g., “If sentiment score < -0.7, escalate”)
     - **Audit Trail Requirements**: What to log (e.g., “Log all decisions with context hash and tool used”)
     - **Ethical Boundaries**: Values-based rules (e.g., “Prioritize long-term trust over short-term resolution”)
   - Deploy this schema as code alongside your agent

6. **Audit and Iterate**
   - After deployment, ask the AI: “What context was missing when you made this decision?”
   - Review audit logs to trace failures back to specific context files or intent rules
   - Update AGENTS.md or intent.yaml in Git, redeploy, and verify improvement

## Rules & Pitfalls
- Never treat AI as a chatbot for complex workflows — static prompts collapse under multi-step, long-duration tasks
- Don’t dump all your data into context — noise degrades performance. Precision > volume
- Avoid “vibe coding” — vague natural language prompts create untraceable, brittle systems
- Never deploy an autonomous agent without an intent schema — you risk catastrophic misalignment (see Klarna)
- Don’t use zero-shot for structured outputs (e.g., JSON) — use few-shot examples to enforce schema
- Don’t assume the model “knows” your business — explicitly encode all conventions in context files
- Don’t ignore audit trails — without them, you cannot debug or improve AI behavior
- Don’t use prompt engineering alone to solve systemic problems — it’s a surface-level fix

## Examples & Resources
**Prompt Template - Structural Formatting** (example)  
> ```  
> <role>You are a senior software engineer reviewing code for production readiness.</role>  
> <context>Our team uses Python 3.10, pytest, and follows PEP8. All functions must have docstrings and unit tests.</context>  
> <task>Analyze the following code and identify risks.</task>  
> <format>Return a JSON object with keys: "issues", "recommendations", "severity".</format>  
> <example>  
> Input: def calc(x): return x * 2  
> Output: {"issues": ["No docstring", "No unit test"], "recommendations": ["Add type hints", "Write test in test_calc.py"], "severity": "medium"}  
> </example>  
> ```  

**Prompt Template - Few-Shot with Quality Control** (example)  
> ```  
> Here are two examples of empathetic customer responses:  
> Example 1:  
> Input: "I’ve been charged twice!"  
> Output: "I’m so sorry this happened — you shouldn’t have been charged twice. I’ve initiated a full refund and will personally follow up with our billing team to prevent this. Thank you for your patience."  
>  
> Example 2:  
> Input: "Your app crashed during my purchase!"  
> Output: "I completely understand your frustration — losing progress during checkout is unacceptable. I’ve restored your cart and applied a 15% discount as a gesture of goodwill. Let me know if you’d like help completing it."  
>  
> Now respond to: "I’ve waited 3 days for my order!"  
> ```  

**Prompt Template - Chain-of-Thought Analysis** (example)  
> ```  
> <task>Analyze this financial report and recommend whether to approve the budget.</task>  
> <thinking>  
> Step 1: Identify key metrics — revenue growth, burn rate, customer acquisition cost  
> Step 2: Compare to last quarter — is growth accelerating or decelerating?  
> Step 3: Check team size vs. output — is scaling efficient?  
> Step 4: Evaluate risk — are there hidden liabilities?  
> Step 5: Synthesize — does this align with our 2026 goal of profitability by Q4?  
> </thinking>  
> <output>Recommendation: [approve/reject/revise] with 1-sentence justification.</output>  
> ```  

**Prompt Template - Context Gap Analysis** (example)  
> ```  
> You are an AI system auditing your own knowledge.  
> I asked you to: [insert failed task]  
> You responded: [insert incorrect output]  
>  
> What specific information was missing from your context that caused this error?  
> List only facts, not guesses.  
> Format:  
> - Missing: [exact document, policy, or data point]  
> - Location: [where it should be found, e.g., “AGENTS.md section 3.2”]  
> ```  

**Prompt Template - Full Intent Schema Generator** (example)  
> ```  
> Generate a YAML intent schema for an AI customer service agent.  
> Primary Objective: Reduce churn by resolving issues before escalation  
> Success Metrics: 90% first-contact resolution, <2 min avg handle time  
> Constraints: Never promise refunds without manager approval  
> Trade-off Hierarchy: Customer satisfaction > Speed > Cost  
> Escalation Triggers: Sentiment < -0.6, mention of “lawyer” or “better business bureau”  
> Audit Trail: Log all decisions with context hash, tool used, and outcome  
> Ethical Boundaries: Prioritize long-term trust over ticket closure rate  
>  
> Output as valid YAML.  
> ```  

**MCP (Model Context Protocol)** (framework) — https://github.com/model-context-protocol/mcp  
> “MCP is a universal plug for AI agents. It standardizes how LLM clients connect to external data and tools via Resources, Tools, and Prompts — eliminating fragile glue code.”  

**Chroma** (tool) — https://www.trychroma.com  
> “Open-source vector database for storing and retrieving context chunks in RAG pipelines.”  

**Docling** (tool) — https://github.com/docling/docling  
> “Extracts text, tables, and images from PDFs and documents for clean context ingestion.”  

**AGENTS.md** (file format)  
> “A repository-level instruction file that provides machine-readable context for AI agents — version-controlled alongside code. Replaces manual context pasting.”  

## Metadata
- **Source:** x.com
- **Type:** framework
- **Created:** 2026-03-06