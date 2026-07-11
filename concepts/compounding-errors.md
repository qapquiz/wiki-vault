---
title: Compounding Errors (No Learning, No Bottleneck)
created: 2026-07-11
updated: 2026-07-11
type: concept
tags: [concept, mental-model, software, ai-ml]
sources: [raw/articles/mariozechner-slowing-the-fuck-down-2026.md]
confidence: medium
---

# Compounding Errors — No Learning, No Bottleneck

A portable mental model, articulated by [[mario-zechner]] in the context of coding agents:

> When an actor makes small errors **but neither learns from them nor is throttled by a
> throughput bottleneck**, those errors compound at an unsustainable rate — and the pain
> arrives too late to course-correct.

## The three ingredients
1. **Error rate > 0.** Any actor, human or machine, makes small mistakes (correctness bugs,
   code smells, duplication). Harmless in isolation.
2. **No learning.** A human eventually stops repeating an error (peer pressure, genuine
   learning). An agent, out of the box, repeats the same errors indefinitely — and may invent
   "glorious new interpolations of different errors" from training data.
3. **No bottleneck / no pain.** A human is a rate limiter: a few thousand lines a day, and
   pain forces cleanup before things get dire. Remove the human from the loop and you remove
   both the throttle *and* the pain signal.

## Why it generalizes
This isn't really about code. It's a systems pattern: **feedback loops need both a sensor
(pain/observation) and an actuator with limited bandwidth (the bottleneck).** Automate away
the bottleneck and you also blind the sensor. Wherever you deploy fast, tireless, non-learning
actors on a compounding substrate (code, content, financial trades, infra), expect the same
shape of failure: everything looks fine until it suddenly isn't.

## The coding-agent instantiation
An "orchestrated army of agents" hits all three: high error rate, no real learning, no human
bottleneck. Result: "innocent booboos form a monster of a codebase" — see
[[agentic-coding-risks]] for the full field report (delayed pain, untrustworthy tests,
architecture-as-booboos).

> `confidence: medium` — derived from a single essay, but the logic is sound and the pattern
> is independently familiar from enterprise-software decay. Worth corroborating with a
> second source on software-erosion / technical-debt dynamics.
