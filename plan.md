# Retro Top-Down Shooter Game Plan

## Context
The user wants a retro-style top-down shooter playable in the browser, built as a single self-contained HTML file (same pattern as the existing `tictactoe.html`). No external dependencies or assets — all sprites drawn programmatically via Canvas API.

## Output File
- `/Users/Charl/Desktop/claude-test/game.html` — single file, all HTML/CSS/JS embedded

## Core Mechanics
- **Movement:** Arrow keys (+ WASD), diagonal normalization, clamped to canvas
- **Aiming/Shooting:** Mouse aim, click to shoot, fire rate cooldown
- **Enemies:** Spawn from screen edges, move toward player, circle-circle collision
- **HP:** Player has 5 HP, brief invincibility on hit, game over at 0

## Sprite System
- Pixel art defined as 2D arrays of color indices (7x7 to 15x15 grids)
- Rendered via `fillRect` at 3x scale, pre-rendered to offscreen canvases for performance
- Palettes: green (player), red (basic), yellow (fast), purple (tank), orange (shooter), dark red (boss)

## Enemy Types
| Type | HP | Speed | Behavior | Unlocks |
|------|----|-------|----------|---------|
| Basic | 1 | 80 | Beeline to player | Wave 1 |
| Fast | 1 | 160 | Zigzag toward player | Wave 3 |
| Tank | 4 | 50 | Slow, beefy | Wave 6 |
| Shooter | 2 | 60 | Stops at range, fires back | Wave 10 |
| Boss | 20+ | 40 | Spread shots, charge attack | Every 5th wave |

## Wave System
- Wave N spawns `3 + N*2` enemies (boss waves are special)
- Enemy types unlocked progressively
- Speed scales +3% per wave
- 2-second rest between waves
- Boss every 5th wave

## Scenes (State Machine)
1. **MenuScene** — Title "PIXEL BLASTER", starfield bg, controls hint, "PRESS ENTER TO START"
2. **GameScene** — Gameplay with HUD (score, wave, HP bar)
3. **GameOverScene** — Final score, waves survived, high score via localStorage

## Visual Polish
- Particle system for explosions, muzzle flash, hit sparks
- Screen shake on damage
- Dark grid background (`#1a1a2e` + subtle grid lines)
- Canvas cursor set to `crosshair`
- Retro sound effects via Web Audio API (square/sawtooth oscillators)

## HUD
- Top-left: wave number
- Top-center: score
- Top-right: HP hearts/bar

## Implementation Order
1. Boilerplate: HTML, canvas, game loop, input handler
2. Player: sprite, movement, aim rotation
3. Shooting: bullets, rendering, lifetime
4. Basic enemy: spawn, AI, collision, death
5. Wave system: progression, wave-complete text
6. More enemy types: fast, tank, shooter, boss
7. Particles & effects: explosions, shake, muzzle flash
8. HUD: score, wave, HP display
9. Menu & Game Over screens: scene transitions
10. Polish: sound effects, high score, animation frames, tuning

## Verification
- Open `game.html` in browser
- Menu screen appears with title and instructions
- Press Enter → gameplay starts
- Arrow keys move player, mouse aims, click shoots
- Enemies spawn from edges and approach
- Killing enemies awards points, waves progress
- Taking 5 hits → game over screen with score
- Press Enter → restart
