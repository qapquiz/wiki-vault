---
title: LLM Agent Orchestration Patterns
created: 2026-07-11
updated: 2026-07-11
type: concept
tags: [concept, ai-ml, framework]
sources: [raw/articles/anthropic-advisor-strategy-2026.md]
confidence: medium
---

# LLM Agent Orchestration Patterns

Ways to structure an agent that uses more than one model — specifically, *which model
decides* and *which model does*. The two ends of a spectrum:

## 1. Orchestrator → Workers (top-down)
A **large model decomposes** the task and **delegates subtasks to smaller models**.
This is the common sub-agent pattern: the expensive model spends its budget on
planning/routing, cheap models do the bulk execution. Cost is driven by the orchestrator
running over the full task, plus the orchestration/decomposition logic itself.

## 2. Executor → Advisor (bottom-up escalation)
A **small model owns the whole task** and **calls a large model only for guidance** at
stuck points. No decomposition, no worker pool. This is the [[advisor-strategy]].

## The tradeoff, in one line
- **Orchestrator→Workers** spends frontier intelligence *up front* on structuring work.
- **Executor→Advisor** spends frontier intelligence *on demand* only where the run actually
  needs it — so easy stretches cost nothing extra and hard moments get full reasoning.

## Why this matters for cost
Intelligence is the expensive thing. The two patterns place that expense differently:
top-down pays for it over the entire orchestration loop; bottom-up confines it to brief
advisory turns (a few hundred tokens). For high-volume tasks, that difference compounds.

> Building-out concept. Grounded in the [[anthropic]] advisor-strategy announcement, now
> joined by [[mario-zechner]]'s field report on what happens when the orchestrator→worker
> pattern ("an army of autonomous agents") is scaled on real codebases — see
> [[agentic-coding-risks]].

## Related
- Concrete instance: [[advisor-strategy]]
- Models these patterns are built on: [[claude-models]]
