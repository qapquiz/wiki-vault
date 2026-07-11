# Wiki Log

> Chronological record of all wiki actions. Append-only.
> Format: `## [YYYY-MM-DD] action | subject`
> Actions: ingest, update, query, lint, create, archive, delete
> When this file exceeds 500 entries, rotate: rename to log-YYYY.md, start fresh.

## [2026-07-11] create | Wiki initialized
- Domain: personal second brain (general-purpose, cross-domain knowledge base)
- Structure created: raw/{articles,books,papers,videos,podcasts,transcripts,assets}, entities/, concepts/, comparisons/, queries/, _archive/
- Core files written: SCHEMA.md, index.md, log.md
- Tag taxonomy established: page-type, source-type, subject, idea-shape, meta/status

## [2026-07-11] ingest | The advisor strategy (Anthropic, 2026-04-09)
- Source: https://claude.com/blog/the-advisor-strategy → raw/articles/anthropic-advisor-strategy-2026.md (sha256 captured)
- Takeaway: "advisor strategy" = small model executes, large model (Opus) advises on demand; inverts orchestrator→worker pattern.
- Created: concepts/advisor-strategy.md, concepts/llm-agent-orchestration.md, entities/anthropic.md, entities/claude-models.md
- Updated: index.md (now 4 pages), this log
- Notes: benchmarks are vendor self-reported and the product is in beta → set confidence: medium on the two concept pages.

## [2026-07-11] ingest | Thoughts on slowing the fuck down (Mario Zechner, 2026-03-25)
- Source: https://mariozechner.at/posts/2026-03-25-thoughts-on-slowing-the-fuck-down/ → raw/articles/mariozechner-slowing-the-fuck-down-2026.md (sha256 captured)
- Takeaway: autonomous coding-agent swarms compound small errors into unmanageable complexity because agents neither learn nor are bottlenecked; prescription is human discipline (slow down, hand-write architecture, human quality gate).
- Created: concepts/agentic-coding-risks.md, concepts/compounding-errors.md, entities/mario-zechner.md
- Updated: entities/anthropic.md (+agent-swarm C-compiler anecdote + critique links), concepts/llm-agent-orchestration.md (+at-scale critique cross-link), SCHEMA.md (+software tag to taxonomy), index.md (now 7 pages), this log
- Notes: opinionated/anecdotal single-author source → confidence: medium on the new concept pages; flagged unverified bio on the mario-zechner page for later confirmation.

## [2026-07-12] ingest | AI Can't Recreate Thrust (But It Can Help You Understand It) (James Randall, 2026-02-23)
- Source: https://www.jamesdrandall.com/posts/thrust_ai_powered_software_archaeology/ → raw/articles/jamesdrandall-thrust-software-archaeology-2026.md (sha256 captured)
- Takeaway: AI **generation** of a nuanced artifact (recreating the 1986 game Thrust from spec+source) produced unusable slop; but the same model was an "extraordinary tool" for **understanding** the original 6502 assembly — a pattern worth naming: AI-powered *software archaeology*. The game's feel lives in exact update cadence (6 active physics slots per 16-tick window ≈ 12.5 Hz, asymmetric drag, Q7.8 fixed-point), not in the constants.
- Created: concepts/software-archaeology.md, entities/james-randall.md, entities/thrust-game.md
- Updated: concepts/agentic-coding-risks.md (+constructive counterpoint section linking archaeology), entities/claude-models.md (+code-comprehension role), index.md (now 10 pages), this log
- Notes: single-source, well-demonstrated case → confidence: medium on all three new pages; cross-linked as the constructive flip-side of the Mario Zechner agentic-coding caution. Wiki now has both sides: generation is risky ([[agentic-coding-risks]]), comprehension shines ([[software-archaeology]]).
