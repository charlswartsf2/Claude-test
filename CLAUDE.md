# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

Browser-based games built as self-contained single HTML files — no build tools, no dependencies, no external assets. Everything (HTML, CSS, JS) lives in one file per game.

## Running

Open any `.html` file directly in a browser (`open game.html` on macOS). No server needed.

## Architecture

Each game is a standalone HTML file using Canvas API for rendering:

- **game.html** — "Pixel Blaster", a retro top-down shooter with wave-based gameplay, 5 enemy types, particle effects, and Web Audio API sound
- **tictactoe.html** — Tic Tac Toe with score tracking

### Pixel Blaster structure (game.html)

The game follows a scene-based state machine (`menu` → `game` → `gameover`) with a `requestAnimationFrame` loop. Key systems:

- **Sprite system**: Pixel art defined as 2D arrays of color indices, pre-rendered to offscreen canvases via `createSprite()`
- **Entity model**: Player, enemies, bullets, and enemy bullets are plain objects in flat arrays — no classes
- **Wave system**: `startWave()` spawns enemies with progressive difficulty scaling; boss every 5th wave
- **Particles**: Simple position + velocity + lifetime objects in a flat array
- **Audio**: Web Audio API oscillators (square/sawtooth) — no audio files

## Conventions

- All games must be single self-contained HTML files with no external dependencies
- Sprites are programmatic (Canvas `fillRect`), not image assets
- High scores persist via `localStorage`
- Game state uses simple object literals, not classes

## Git Workflow

All changes are committed with descriptive messages and pushed to GitHub (origin: `charlswartsf2/Claude-test`).
