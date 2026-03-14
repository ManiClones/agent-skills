---
name: karpathy-autoresearch-harness-design
description: >-
  Operational blueprint for building reliable autonomous AI research harnesses. Use when designing agent systems that modify training code, optimize for time-bounded metrics, or require reversible, observable experiments. Use when user asks about autoresearch, autonomous training optimization, stable evaluation harnesses, or agent failure recovery.
---

# How Karpathy's Autoresearch Works And What You Can Learn From It

> Source: https://x.com/i/article/2032398255095730177
> Created: 2026-03-14

## Overview
This skill helps you design autonomous AI research systems that operate reliably without human supervision by enforcing tight constraints, stable evaluation, and reversible experimentation. Use this when building agent systems that modify training scripts, optimize for real-world time budgets, or require auditability and crash resilience. It enables long-running, unattended optimization loops that improve model training efficiency without drifting benchmarks or accumulating untrackable changes.

## Instructions
1. **Define a single editable file** — Only allow the agent to modify one file: `train.py`. All other components (data prep, tokenization, evaluation) must be fixed and immutable.

2. **Lock the evaluation metric** — Use `val_bpb` (bits per byte) as the sole optimization target. Do not allow the agent to change the metric or the evaluation pipeline.

3. **Enforce a fixed time budget** — Every experiment must run for exactly 5 minutes of wall-clock time. Do not optimize for steps, epochs, or convergence — optimize for performance within this fixed duration.

4. **Start each experiment from the current frontier** — Before each run, the agent must check out the current best commit (frontier). All edits must be made on a branch derived from this state.

5. **Run the experiment with logging** — Execute `uv run train.py > run.log 2>&1` to capture all output, errors, and metrics. Never run without logging.

6. **Extract the metric from the log** — After the 5-minute run, parse `run.log` to extract the `val_bpb` value. Do not assume the metric is printed in a specific format — parse it programmatically from the log.

7. **Apply keep-or-reset logic** — If the new `val_bpb` is lower (better) than the frontier’s value, commit the change and make it the new frontier. If the new value is equal or worse, reset the branch to the previous frontier and discard the change.

8. **Handle failures explicitly** — If the run produces NaN, OOM, or crashes:
   - Inspect `run.log` for obvious errors (e.g., syntax, out-of-memory).
   - If the error is trivial (e.g., typo, missing import), attempt a single automated fix.
   - If the error is unresolvable, log the crash in `results.tsv` and reset to the frontier without committing.

9. **Separate operational history from code history** — Store all experiment results (including failures and crashes) in `results.tsv`. Do not commit `results.tsv` to git. Only git commits should contain winning code changes.

10. **Define agent behavior in `program.md`** — Write explicit instructions for the agent covering:
    - Allowed files to edit (`train.py` only)
    - Evaluation metric (`val_bpb`)
    - Time budget (5 minutes)
    - Commit/revert logic
    - Crash recovery steps
    - Logging format expectations
    - How to read and write to `results.tsv`

11. **Design for unattended operation** — Assume 100% of runs may fail. The system must recover autonomously without human intervention. Never design for perfect success — design for graceful failure and rollback.

12. **Never let the agent modify the harness** — `prepare.py` must be immutable. The agent cannot change data loading, tokenization, or evaluation logic. The benchmark must remain stable across all iterations.

## Examples
- When the user asks about “how to make an AI agent improve training code without breaking the benchmark” → Implement Autoresearch’s 5-minute wall-clock time budget with `val_bpb` metric and keep/reset logic on `train.py` only.
- When the user says “my agent keeps making bad changes that break training” → Enforce the keep-or-reset mechanism: only accept changes that improve `val_bpb` and reset the branch on failure.
- When the user asks “how do I track what the agent tried and failed?” → Log every run (success or crash) to `results.tsv` and preserve git history of only winning commits.
- When the user asks “can the agent change the dataset or tokenizer?” → Block all access to `prepare.py`. The agent must not touch data pipeline, tokenization, or evaluation code.
- When the user asks “how long should each experiment run?” → Set exactly 5 minutes of wall-clock time per run. Do not use steps or epochs.

## Key Details
- metric: `val_bpb` (bits per byte) — used as the sole evaluation metric
- editable file: `train.py` — only file the agent is allowed to modify
- immutable files: `prepare.py`, `program.md`, data pipeline, tokenizer, evaluation code
- time budget: 5 minutes per experiment (wall-clock time)
- experiment cycle: check out frontier → edit `train.py` → run `uv run train.py > run.log 2>&1` → extract `val_bpb` → keep if better, reset if equal/worse
- failure handling: inspect `run.log`, attempt trivial fix, log crash, reset to frontier
- log file: `run.log` — captures all stdout/stderr from training run
- results tracker: `results.tsv` — stores all runs (winning and discarded), not committed to git
- git history: contains only winning commits (improvements), not speculative or failed runs
- agent instruction file: `program.md` — defines workflow, boundaries, recovery, logging, and selection criteria
- hardware context: designed for single NVIDIA GPU, high-end CUDA setup
- optimization goal: maximize performance per unit time, not abstract model quality

## Framework
### Autoresearch Harness Architecture
- **Control Plane**: `program.md` — defines agent behavior, rules, and constraints
- **Fixed Harness**: `prepare.py` — handles data download, tokenization, dataloader, evaluation — immutable
- **Search Surface**: `train.py` — only mutable file; contains model, optimizer, hyperparameters, training logic
- **Experiment Loop**:
  1. Start from frontier commit
  2. Edit `train.py`
  3. Run for 5 minutes → log to `run.log`
  4. Extract `val_bpb` from `run.log`
  5. If `val_bpb` improves → commit as new frontier
  6. Else → reset branch to frontier
- **Operational Logging**: `results.tsv` — records all runs (success/fail/crash), timestamp, metric, commit hash, error logs
- **Failure Resilience**: Agent must handle NaN, OOM, crashes by logging and resetting — no manual intervention
- **Git Discipline**: Only winning changes are committed; all history is traceable and reversible

## Mistakes to Avoid
- Mistake: Letting the agent modify `prepare.py` or data pipeline → Action: Block all edits to `prepare.py`; the benchmark must be fixed
- Mistake: Optimizing for validation loss instead of `val_bpb` → Action: Use `val_bpb` to ensure comparability across tokenizer changes
- Mistake: Running experiments for variable time (e.g., until convergence) → Action: Enforce 5-minute wall-clock limit to optimize for real-world speed
- Mistake: Committing failed or discarded runs to git → Action: Only commit winning changes; store all runs in `results.tsv` outside git
- Mistake: Treating `program.md` as optional documentation → Action: Treat `program.md` as core system architecture — it defines the agent’s operating rules
- Mistake: Assuming agent failures are rare → Action: Design for 100% failure tolerance; assume every run may crash
- Mistake: Building open-ended agents that browse papers or form theories → Action: Restrict agent to one file, one metric, one time budget — narrow scope enables reliability

## Tools & Resources
- `uv` — Python package manager used to run `uv run train.py`
- `train.py` — editable training script (model, optimizer, hyperparameters)
- `prepare.py` — fixed data and evaluation pipeline (immutable)
- `program.md` — agent instruction manual (core control layer)
- `results.tsv` — operational log of all experiments (tab-separated values, not git-tracked)
- `run.log` — stdout/stderr capture from each training run
- NVIDIA GPU — recommended hardware; system optimized for high-end CUDA setup
- Git — used to track winning code changes only

## Metrics & Numbers
- **Time per experiment**: 5 minutes (wall-clock)
- **Editable files**: 1 (`train.py`)
- **Immutable files**: 2+ (`prepare.py`, `program.md`, data pipeline, tokenizer, evaluation code)
- **Evaluation metric**: `val_bpb` (bits per byte)
- **Failure tolerance**: Designed for NaN, OOM, script crashes
- **Storage**: `results.tsv` stores all runs (winning and losing); git stores only winning commits
- **Hardware**: Single NVIDIA GPU (high-end); forks exist for smaller machines but default is CUDA-optimized

## Implementation Guide
- **Day 1**: Set up `prepare.py` with fixed data pipeline, tokenizer, and `val_bpb` evaluation
- **Day 2**: Create `train.py` with baseline model, optimizer, and training loop
- **Day 3**: Write `program.md` with explicit agent instructions: allowed file, metric, time limit, keep/reset logic, crash recovery
- **Day 4**: Implement experiment loop: checkout frontier → edit → run → parse log → compare → commit/reset
- **Day 5**: Set up `results.tsv` logging with headers: timestamp, commit_hash, val_bpb, status (success/fail/crash), error_message
- **Day 6**: Test with 10-20 random edits to `train.py` — verify only improvements are kept
- **Day 7**: Run unattended for 24 hours — monitor `results.tsv` for crash patterns and improvement trends
- **Scaling**: Add parallel runs on multiple GPUs by isolating each in its own directory with independent `results.tsv` and git repo

## Metadata
- **Source:** x.com
- **Type:** framework
- **Depth:** comprehensive
- **Source length:** ~1639 words