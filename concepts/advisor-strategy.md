---
title: The Advisor Strategy
created: 2026-07-11
updated: 2026-07-11
type: concept
tags: [concept, ai-ml, framework, source-article]
sources: [raw/articles/anthropic-advisor-strategy-2026.md]
confidence: medium
---

# The Advisor Strategy

An LLM agent pattern for getting near-frontier intelligence at low cost: a **small
model runs the task** (the *executor*), and **escalates to a large model for guidance
only** (the *advisor*) when it hits a decision it can't reasonably make on its own.

> Introduced by Anthropic on 2026-04-09 as both a named pattern and a server-side
> **advisor tool** on the Claude Platform. ^[raw/articles/anthropic-advisor-strategy-2026.md]

## How it works
- The executor (e.g. Sonnet or Haiku) owns the loop: calls tools, reads results, iterates.
- When it's stuck, it invokes the advisor (Opus). The advisor sees the curated shared
  context and returns a **plan, a correction, or a stop signal** — *not* tool calls, *not*
  user-facing output.
- The executor resumes. Frontier reasoning is paid for only at the moments it's needed.

## The key inversion
This is the load-bearing idea, and the reason it's cheap. The dominant [[llm-agent-orchestration]]
pattern is **orchestrator → workers**: a *large* model decomposes the task and delegates
to *small* models. The advisor strategy flips it: a **small model drives, a large model
advises on demand** — no decomposition, no worker pool, no orchestration logic.

## Reported results (vendor self-reported, beta)
- Sonnet + Opus advisor: **+2.7 pp on SWE-bench Multilingual** vs Sonnet solo, **−11.9% cost** per agentic task.
- Sonnet + Opus advisor: improved on BrowseComp and Terminal-Bench 2.0 while costing less than Sonnet solo.
- Haiku + Opus advisor on BrowseComp: **41.2% vs 19.7% solo** (more than doubled), trailing Sonnet solo by 29% in score but **85% cheaper** per task.

> ⚠️ `confidence: medium` — all numbers come from Anthropic's own announcement and the
> product is in beta. Benchmark setups vary by harness (thinking on/off, effort level,
> system prompt) — see methodology footnotes in the source before quoting a figure.

## API shape (one-line change)
Declare `advisor_20260301` as a tool in a `/v1/messages` request. The model handoff
happens **inside a single request** — no extra round-trips, no context management.
- Advisor tokens billed at advisor rates; executor tokens at executor rates.
- Advisor typically emits only **400–700 tokens** (a short plan), so total cost stays well
  below running Opus end-to-end.
- `max_uses` caps advisor calls per request; advisor usage reported separately for spend tracking.
- Beta header: `anthropic-beta: advisor-tool-2026-03-01`.

## When it's a good fit
High-volume agentic workloads where you want frontier-quality decisions without
frontier-level cost on every token — coding agents, browsing research, document extraction.
The customer quote about "no overhead on simple ones, night-and-day plans on complex ones"
captures the value: intelligence scales *with task difficulty*, not uniformly.

## Related
- Parent pattern: [[llm-agent-orchestration]]
- The models involved: [[claude-models]]
- Published by: [[anthropic]]
