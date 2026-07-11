---
title: Thrust (1986 BBC Micro game)
created: 2026-07-12
updated: 2026-07-12
type: entity
tags: [entity, software, reference, evergreen, source-article]
sources: [raw/articles/jamesdrandall-thrust-software-archaeology-2026.md]
confidence: medium
---

# Thrust (1986 BBC Micro game)

A 1986 BBC Micro game written by **Jeremy C. Smith** (then ~16–18 years old) and published
that year. A deceptively deep physics game: pilot a ship through caverns, collect fuel,
dodge turret fire, and retrieve a pod for bonus points — all while fighting gravity and
momentum. [Play the original online.](http://bbcmicro.co.uk/game.php?id=432)

Despite running in 32K of RAM, its *feel* — the specific weight, timings, and momentum — is
what makes it revered, and what makes it hard to recreate faithfully.

> 📌 In this wiki primarily as the **case study** for [[software-archaeology]]:
> [[james-randall]]'s 2026 TypeScript recreation (see his [writeup](https://www.jamesdrandall.com/posts/thrust_ai_powered_software_archaeology/)
> and [source](https://github.com/JamesRandall/ts-thrust)). Facts below come from that source.
> ^[raw/articles/jamesdrandall-thrust-software-archaeology-2026.md]

## Why it's hard to recreate (the "feel" is in the timing)
The magic is **not** in the constants — it's in the exact **update cadence**:
- Physics does **not** run at the BBC's 50 Hz VSync. The tick loop waits ≥3 centiseconds/frame
  → ~33.33 Hz effective.
- Within each tick, force/drag updates are **gated to 6 active slots per 16-tick window**
  (`{0,3,5,8,11,13}`) → ~12.5 Hz effective force rate. Position integrates every tick.
- Rotation has its own gating: it skips every 4th tick, integer steps only.
- **Asymmetric linear drag**: X axis `*63/64`, Y axis `*255/256` — so horizontal movement
  feels "stickier" than vertical.
- Arithmetic is **Q7.8 fixed-point** (no FPU on 8-bit hardware); rotation uses 32 steps with
  lookup tables for force components.

Matching the constants but not these timings produces a ship that is far too fast and agile
— "it didn't have the right weight." Matching the exact cadence makes the recreation
indistinguishable in feel from the emulator. **This is the concrete demonstration that AI
generation from a description can't capture feel, while AI-aided understanding of the
source can.**

## Subsystem notes (from the recreation)
- **Sound:** continuous, input-responsive engine drone + specific explosion envelopes. Best
  reproduced by **emulating the SN76489 sound chip and the BBC MOS interface** (OSWORD 7/8
  calls) in an AudioWorklet — the MOS ticks at 100 Hz on the audio thread. Sampling would
  have felt "wrong"; hardware emulation got identical results.
- **Graphics:** the ship isn't vector-drawn — it's **32 hand-optimized rotation sprites**
  (tuned by Jeremy Smith to look right at each angle). Terrain uses **scanline-parity
  polygon fill** (every other line) at an internal 320×256 resolution.
- **Demo (attract) mode:** no separate renderer — the live engine runs with **timed fake key
  presses** from two parallel tables (bit-mask + duration), 3 of the timer slots randomized
  per run for variation. Its success is itself proof the physics recreation is accurate.
- **Turret nuance:** turrets stop firing for a while if you hit the generator; firing-angle
  subtleties only surface when reading the code.

## Author's fate
Jeremy C. Smith went on to co-create *Exile* (with Peter Irvin) — "something else entirely"
in ambition — before dying in an accident in 1992.

## Related
- The recreation and the lesson it taught: [[james-randall]], [[software-archaeology]]
- The generation-failure it illustrates: [[agentic-coding-risks]]
