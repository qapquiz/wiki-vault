---
title: James Randall
created: 2026-07-12
updated: 2026-07-12
type: entity
tags: [entity, software, tech, source-article]
sources: [raw/articles/jamesdrandall-thrust-software-archaeology-2026.md]
confidence: medium
---

# James Randall

Software developer and writer at **jamesdrandall.com**. Works on **browser-native,
high-fidelity recreations of classic 8-bit games**, with deep respect for getting the
original *feel* exactly right. Author of this wiki's source on AI-powered
[[software-archaeology]].

## Projects mentioned (from this source)
- **[ts-thrust](https://github.com/JamesRandall/ts-thrust)** — a TypeScript/WebGPU
  recreation of the 1986 BBC Micro game [[thrust-game]], done by interrogating the
  original's 6502 disassembly with Claude. Emulates the BBC's SN76489 sound chip and MOS
  envelope processor in an AudioWorklet for identical audio. [Play it here.](https://www.jamesdrandall.com/thrust/)
- **[WebGLite](https://www.jamesdrandall.com/projects/webglite/)** — his earlier TypeScript
  conversion of *Elite*; source of the CRT shader effects he reused for Thrust.
- **Annhexation** — a browser-native 4X game (custom WebGPU engine, eight civilisations, an
  AI opponent), in early access / Steam wishlist at time of writing.

## In this wiki
- Author of *"AI Can't Recreate Thrust (But It Can Help You Understand It)"* (2026-02-23),
  the source behind [[software-archaeology]]. His lesson: AI is a powerful *explainer* of
  existing code even when it fails as a from-scratch *generator*.

## Stance on AI coding tools
Nuanced and pragmatic. He opens by showing AI **generation** of a nuanced artifact (the game
Thrust from a spec + source) producing unusable "slop" — echoing the caution in
[[agentic-coding-risks]]. But his constructive conclusion is that the same tool is
**extraordinary for understanding** legacy/foreign code, which is where he found the value.
Also a small fan of multimodal delegation for grunt work (replaying frames → "recreate that").

## To expand
> Bio limited to what this single source states. Likely more detail on his site's about page
> / project list — confirm any specifics before relying on them.

## Related
- His core idea: [[software-archaeology]]
- The game he recreated: [[thrust-game]]
- The generation-caution he exemplifies: [[agentic-coding-risks]]
