# Wiki Schema — Second Brain

## Domain
**Personal second brain.** A general-purpose, cross-domain knowledge base.
Captures and connects anything worth remembering: articles, books, papers,
videos, podcasts, people, organizations, tools, ideas, mental models, and
personal notes. There is no fixed subject boundary — the goal is a compounding
web of personally meaningful knowledge, not a topical encyclopedia.

The organizing principle is **connection over collection**: every page links to
others, and ideas accumulate across sources rather than living in isolation.

## Conventions
- File names: lowercase, hyphens, no spaces (e.g., `compound-interest.md`,
  `naval-ravikant.md`, `mental-model-latitude.md`).
- Every wiki page starts with YAML frontmatter (see below).
- Use `[[wikilinks]]` to link between pages. **Minimum 2 outbound links per page.**
- When updating a page, always bump the `updated` date.
- Every new page must be added to `index.md` under the correct section.
- Every action must be appended to `log.md`.
- **Provenance markers:** On pages synthesizing 3+ sources, append
  `^[raw/articles/source-file.md]` at the end of paragraphs whose claims come
  from a specific source. Lets a reader trace each claim without re-reading the
  whole raw file. Optional on single-source pages where `sources:` suffices.

## Frontmatter
  ```yaml
  ---
  title: Page Title
  created: YYYY-MM-DD
  updated: YYYY-MM-DD
  type: entity | concept | comparison | query | note
  tags: [from taxonomy below]
  sources: [raw/articles/source-name.md]
  # Optional quality signals:
  confidence: high | medium | low        # how well-supported the claims are
  contested: true                        # set when the page has unresolved contradictions
  contradictions: [other-page-slug]      # pages this one conflicts with
  ---
  ```

`confidence` and `contested` are optional but recommended for opinion-heavy,
fast-moving, or single-source material. Lint surfaces `contested: true` and
`confidence: low` pages so weak claims don't silently harden into accepted fact.

### raw/ Frontmatter
Raw sources also get frontmatter so re-ingests can detect drift:

```yaml
---
source_url: https://example.com/article        # original URL, if applicable
author:                                         # author/speaker, if known
ingested: YYYY-MM-DD
sha256: <hex digest of the raw content below the frontmatter>
---
```

The `sha256:` lets a future re-ingest of the same URL skip processing when
content is unchanged, and flag drift when it has changed. Compute over the body
only (everything after the closing `---`), not the frontmatter itself.

## Tag Taxonomy
Rule: **every tag on a page must appear here.** If a new tag is needed, add it
to this list first, then use it. This prevents tag sprawl.

### Page type (use exactly one as the primary classifier; matches `type:`)
- `entity` — a person, organization, tool, product, or place
- `concept` — an idea, mental model, framework, technique, or topic
- `comparison` — a side-by-side analysis
- `query` — a filed research answer worth keeping
- `note` — a personal note, reflection, or synthesis not tied to one source

### Source type (for raw/ files and to indicate origin on wiki pages)
- `source-article`, `source-book`, `source-paper`, `source-video`,
  `source-podcast`, `source-transcript`, `source-note`

### Subject (broad domain — combine freely; pick the 1–2 that fit best)
- `tech`, `science`, `math`, `engineering`, `software`
- `health`, `fitness`, `nutrition`, `sleep`, `longevity`
- `business`, `finance`, `investing`, `startups`, `economics`
- `psychology`, `philosophy`, `ethics`, `learning`, `productivity`
- `design`, `art`, `writing`, `language`, `history`, `culture`, `politics`
- `ai-ml` — artificial intelligence / machine learning (kept separate from `tech`)

### Idea shape (optional, for concept pages)
- `mental-model`, `framework`, `principle`, `heuristic`, `fallacy`, `definition`

### Meta / status
- `decision` — supports a choice or tradeoff analysis
- `project` — tied to an active personal project
- `reference` — useful lookup / factual material
- `quote` — a notable quote with attribution
- `prediction` — a forecast or bet to track over time
- `controversy` — contested or debated topic
- `evergreen` — durable, won't go stale; vs. fast-moving material (no tag needed)

## Page Thresholds
- **Create a page** when something appears in 2+ sources, OR is central to one
  source, OR is a personally important idea you want to develop.
- **Add to an existing page** when a new source mentions something already covered.
- **DON'T create a page** for passing mentions, minor details, or trivia you'll
  never revisit.
- **Split a page** when it exceeds ~200 lines — break into sub-topics with cross-links.
- **Archive a page** when fully superseded — move to `_archive/`, remove from index.

## Entity Pages
One page per notable entity (person, org, tool, product). Include:
- Overview / what it is / why it matters to you
- Key facts, dates, relationships (`[[wikilinks]]`)
- For people: their ideas, work, affiliations, and links to concept pages
- Source references

## Concept Pages
One page per concept, mental model, or topic. Include:
- Definition / explanation in your own words
- Examples and edge cases
- Current state of understanding / open questions
- Related concepts (`[[wikilinks]]`)

## Comparison Pages
Side-by-side analyses. Include:
- What is being compared and why (the decision or question behind it)
- Dimensions of comparison (table format preferred)
- Verdict or synthesis
- Sources

## Note Pages (`type: note`)
Personal reflections or syntheses not tied to a single source. Use for:
- Your own thinking that builds on multiple pages
- Decisions and rationale
- Reading takeaways that span sources

## Update Policy
When new information conflicts with existing content:
1. Check the dates — newer sources generally supersede older ones.
2. If genuinely contradictory, note both positions with dates and sources.
3. Mark the contradiction in frontmatter: `contradictions: [page-name]`.
4. Flag for user review in the lint report.
