---
title: Software Archaeology (AI-Powered)
created: 2026-07-12
updated: 2026-07-12
type: concept
tags: [concept, ai-ml, software, mental-model, source-article]
sources: [raw/articles/jamesdrandall-thrust-software-archaeology-2026.md]
confidence: medium
---

# Software Archaeology (AI-Powered)

Using an LLM to **interrogate an existing codebase** — especially legacy, foreign, or
low-level code you don't fully understand — by feeding in chunks (disassembly, comments,
specs, datasheets) and asking pointed questions: *"how does the level data work?"*,
*"what is the physics model doing here?"*. The model returns detailed, accurate
explanations of what the code is doing, far faster than reading it cold.

Named after [[james-randall]]'s account of recreating the 1986 game [[thrust-game]]:
where AI **failed to generate** the game from scratch, it **succeeded brilliantly as an
explainer** of the original 6502 assembly. That contrast is the whole point.

> ⚠️ `confidence: medium` — a single, well-demonstrated case (one developer, one codebase).
> The pattern rings true and generalizes, but is not yet corroborated by other sources in
> this wiki. ^[raw/articles/jamesdrandall-thrust-software-archaeology-2026.md]

## The thesis: AI as understanding tool, not just generator
For work steeped in tacit knowledge — game *feel*, hardware timing, hand-tuned constants —
AI **generation from a spec produces slop**. It captures the surface (looks roughly right)
but misses the thing that matters (the weight, the timings, the momentum). See
[[agentic-coding-risks]] for the broader case that raw AI generation is brittle on real
systems.

But the **same model**, pointed at *existing* code instead of a blank page, becomes a
powerful comprehension aid. The value is in **understanding**, and understanding is what
lets you recreate or maintain something faithfully. In Randall's words: "AI couldn't
recreate Thrust for me… But it could help me understand the original well enough to
recreate it myself."

## Why it works so well
- **The code already disambiguates.** Generation has no ground truth; comprehension has the
  code as an anchor. The model is explaining something concrete, not inventing it.
- **Comments + assembly together.** The model extracts signal from both the human comments
  and the raw instructions and synthesizes a description. Randall's intuition: without
  comments to focus attention, it would have been *much* less useful — a hint that **good
  context curation** (you deciding what to feed it) is the human's leverage.
- **It scales across subsystems.** Once a subsystem is understood, the answer can be turned
  into a spec the human then implements. The flow is: *disassembly → questions → specs →
  code*, with the human owning the implementation and the feel.

## The pattern, generalized
This is AI in a ** comprehension / pair-explainer** role over a codebase the human doesn't
fully own in their head: old 8-bit assembly, a large inherited codebase, an unfamiliar
language or framework, hardware datasheets + driver code, reverse-engineered binaries. It
sits adjacent to [[llm-agent-orchestration]] but is distinct — the goal isn't to *produce*
code at scale, it's to **transfer understanding to the human** quickly.

## A related multimodal win
The same posture (let AI handle the uninteresting stuff) showed up in a small multimodal
case: the teleport animation didn't match the original, so Randall recorded the game,
grabbed the frames, pasted them into Claude Code and said "recreate that" — done in five
minutes. Not hard, but a good delegation of grunt work so attention stays on the
interesting parts.

## Bottom line
The durable lesson isn't "AI can write a game." It's: **point AI at understanding, not
just output.** Where generation is risky ([[agentic-coding-risks]]), comprehension shines.
The human supplies focus and taste; the model supplies tireless, fluent explanation of
code that would otherwise take days to read.

## Related
- Source and case study: [[james-randall]] on [[thrust-game]]
- The generation-failure side of the same coin: [[agentic-coding-risks]],
  [[compounding-errors]]
- The model used: [[claude-models]] (Claude / Claude Code)
- Adjacent pattern, different goal: [[llm-agent-orchestration]]
