# Murmuration

## Brief (from the prompt)
- **Concept:** Lead a starling flock at dusk. Draw a path and 300 boids flow behind you like living smoke; thread rings of light, evade the falcon.
- **Quality bar:** polished
- **Scope:** M
- **Budget:** default (600k)

## Core Concept
You are the lead starling of a murmuration over a marsh at dusk. Your finger (or mouse) is the flock's intent: wherever you draw, the swarm bends, stretches, and pours after it, driven by real boid rules. Glowing rings drift across the sky; pull the flock through them to score. A falcon periodically stoops at the flock's heart, forcing you to whip the swarm aside. The fun is the feel: the flock is a brush, the sky is the canvas, and the game gently pressures you to paint fast.

## Core Loop
Every few seconds: spot the next ring → sweep the flock toward and through it (score + chime + shimmer) → read the falcon warning → yank the flock clear → line up the next ring. Combos build for consecutive rings without a falcon hit.

## Win / Lose
Endless twilight run. Score = rings threaded, with a combo multiplier. Falcon strikes each snatch a handful of starlings; when the flock drops below 60 birds, the run ends (survivors roost, score screen). Best score persists in-page for the session.

## Objects & Entities
Player attractor (invisible; pointer position), ~300 boid starlings, glowing rings (spawn, drift, expire), falcon (telegraphed dive with warning cry glyph + red streak), score/combo/flock-count HUD, marsh silhouette foreground, dusk sky gradient with low sun.

## Mechanics (cause → effect rules)
- Pointer down + drag → flock steering target moves; boids blend seek(target) with separation/alignment/cohesion → flock flows like smoke.
- Flock center passes within a ring's radius while ring is live → ring bursts into motes, +1 ring, combo +1, soft chime.
- Ring expires unthreaded → fades out, combo resets to 0.
- Every 12-20s → falcon warning (1.2s: red glint at screen edge + rising tone) → falcon streaks through the flock's current center; any boids within kill radius are taken (max ~12 per strike, screen-edge feather puff).
- Flock count < 60 → run over, roost sequence, score screen with replay button.
- No input → flock idles in a slow lazy orbit (a self-playing murmuration; the attract mode IS the beauty shot).

## UI Needs
- [v1] Title overlay (name, one-line how-to, tap to start), HUD (rings, combo, flock count), game-over card with score/best/replay, mute toggle.
- [later] Persistent best score, difficulty ramps, multiple falcon patterns.

## Chosen Stack + Why
- **Stack:** html (single file, canvas 2D + WebAudio)
- **Why:** 300 boids on a 2D canvas with a spatial grid is comfortably 60fps; no engine needed. Single file deploys straight to GitHub Pages.

## Scope Notes
- **v1 (shippable):** boid flock + pointer steering, rings, falcon, score/combo, game over, idle attract mode, sound (chime, falcon cry, wind bed).
- **Later:** roost-to-roost level structure, photo mode, flock size upgrades.

## Mobile Considerations
Touch drag anywhere on screen steers (no buttons needed mid-play). HUD in top corners clear of thumbs. Ring spawn positions keep 10% margin from edges. devicePixelRatio-aware canvas; cap boids to ~200 if a coarse pointer + small viewport is detected.

## Polish Hooks (for the Vibe stage)
1. Ring thread: mote burst + chord chime that rises with combo.
2. Falcon near-miss: slow-mo 0.3s + flock compression wave when the falcon misses by little.
3. The idle attract-mode murmuration on the title screen: it should look like a nature documentary before a single input.
