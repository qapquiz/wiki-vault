---
title: Agentic Coding — Risks and Discipline
created: 2026-07-11
updated: 2026-07-12
type: concept
tags: [concept, ai-ml, software, controversy, source-article]
sources: [raw/articles/mariozechner-slowing-the-fuck-down-2026.md]
confidence: medium
---

# Agentic Coding — Risks and Discipline

The thesis of [[mario-zechner]]'s "Thoughts on slowing the fuck down" (2026-03-25): a year
into capable coding agents, the push to fully automate production codebases is producing
brittle, unmaintainable software. The fix isn't a better model — it's **human discipline**:
slow down, stay in the loop, and keep the human as the quality gate.

> ⚠️ `confidence: medium` — an opinionated, anecdotal essay (the author is explicit that
> it's anecdotal). It articulates failure modes many practitioners report, but the specific
> anecdotes (AWS outage, Microsoft/Windows, "100% AI" companies) are unsourced hearsay.
> ^[raw/articles/mariozechner-slowing-the-fuck-down-2026.md]

## The core failure mechanism
Three properties combine to make autonomous agent swarms dangerous on real codebases:
1. **Agents make small errors** (correctness bugs, code smells, duplication) — same as humans.
2. **Agents don't learn** from their errors the way humans do — they repeat them, and may
   interpolate new ones from training data.
3. **Agents have no throughput bottleneck** — a human caps out at a few thousand lines/day
   with pain as a forcing function; an agent swarm emits 20k lines in hours with no pain.

→ This is the [[compounding-errors]] trap: small errors, no learning, no bottleneck, delayed
   pain. The codebase turns into "a monster of booboos" before anyone feels it.

## Second-order effects
- **Merchants of learned complexity.** Agents trained on cargo-cult "best practices" produce
  abstraction-for-abstraction's-sake. Their decisions are always **local** — they can't see
  the whole codebase or each other's runs — so they duplicate and over-abstract. Human
  enterprise codebases reach this state in *years*; an agent swarm + 2 humans reaches it in
  *weeks*.
- **Agentic search has low recall.** As the codebase grows, the agent fails to find all the
  code it should change or reuse (regardless of tool: ripgrep, LSP, vector DB, codebase
  index). Low recall is *why* the duplication/smell errors happen in the first place — and
  it also blocks agents from later fixing the mess they made.
- **Tests become untrustworthy.** Once the codebase is untrustworthy, the unit/snapshot/e2e
  tests the agents wrote are too. The only reliable check left is manual testing.

## The prescription: slow the fuck down
- **Keep the human as the final quality gate.** Always.
- **Good agent tasks** are: scoped (agent needn't understand the full system), **closed-loop**
  (agent can evaluate its own work), non-mission-critical, or exploratory ("a rubber duck
  against the compressed wisdom of the internet").
- **Hand-write the gestalt** — architecture, APIs, the shape of the system. Use agents for
  tab completion / pair programming, not for architectural decisions. The *friction* of
  writing it yourself is where understanding, taste, and learning happen.
- **Cap generated code/day** to what you can actually review.
- **Karpathy's auto-research** is the canonical "good" pattern: give the agent an evaluation
  function so it can self-measure — but recognize the eval captures only a narrow metric and
  the agent will happily sacrifice anything not in it (quality, complexity, even correctness).

> Connects to [[llm-agent-orchestration]]: this is a critique of scaling the
> orchestrator→worker ("army of autonomous agents") pattern on real codebases — the pattern
> the [[advisor-strategy]] names as the "common" one. Same vocabulary, sobering field report.

## A constructive counterpoint
This page is about where AI **generation** fails. But the same tool, pointed at *existing*
code instead of a blank page, is a powerful comprehension aid — see [[software-archaeology]].
[[james-randall]]'s attempt to have Claude *generate* the game [[thrust-game]] from a spec
produced unusable slop (a perfect small example of the failure mode above); yet the same
model was extraordinary at *explaining* the original 6502 assembly. The honest picture is
both: generation is risky, comprehension shines.

## Bottom line
"All of this requires discipline and agency. All of this requires humans." The risk isn't
that agents are dumb; it's that removing human friction removes the feedback loop that keeps
complexity in check.
