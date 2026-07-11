---
title: Claude Models (Opus / Sonnet / Haiku)
created: 2026-07-11
updated: 2026-07-11
type: entity
tags: [entity, ai-ml]
sources: [raw/articles/anthropic-advisor-strategy-2026.md]
confidence: high
---

# Claude Models (Opus / Sonnet / Haiku)

The [[anthropic]] model family, positioned as a **capability/cost tiering**: pick the tier
that matches the job, and (per the [[advisor-strategy]]) combine tiers within one agent.

## The tiers
- **Opus** — frontier / most capable; the "advisor" tier. Highest intelligence, highest cost.
- **Sonnet** — balanced; the default executor for cost-sensitive agentic work.
- **Haiku** — fast and cheap; executor for very high-volume tasks where some quality can be
  traded for cost (advisable only when paired with an Opus advisor for hard moments).

## Current generation (as of mid-2026)
From the advisor-strategy announcement: **Opus 4.6**, **Sonnet 4.6** (API id
`claude-sonnet-4-6`), **Haiku 4.5**. Opus 4.6 was the advisor model in all reported runs.

## Why the tiering exists
It's the substrate that makes [[llm-agent-orchestration]] patterns pay off: you only get a
cost win from "small executes, large advises" if there *is* a meaningful small/large gap to
exploit. The advisor tool formalizes that gap as a single API call.

## Related
- Company: [[anthropic]]
- Pattern built on this family: [[advisor-strategy]]
- Broader framing: [[llm-agent-orchestration]]
