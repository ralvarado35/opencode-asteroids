# AGENTS.md

## What this is

Vanilla HTML5 canvas game (Asteroids clone) with **zero toolchain**: no `package.json`, no dependencies, no bundler, no tests, no linter, no CI. Four files total: `index.html` (shell + CSS), `game.js` (all logic, ~420 lines), `favicon.svg`, `README.md`.

**Do not add tooling (npm, bundlers, test frameworks) unless explicitly asked.** There is no `npm test` / `lint` / `typecheck` to run — the only verification is opening the game in a browser.

## Run

- Open `index.html` directly in a browser, or `npx serve .` and visit the printed URL.

## Constraints

- `index.html` loads `game.js` as a **classic script** (`<script src="game.js">`), not an ES module. No imports/exports; everything is top-level in one file. Converting to modules requires changing `index.html` too.
- Canvas size is defined **twice**: `width="800" height="600"` in `index.html` and `const W = 800; const H = 600;` at the top of `game.js`. Keep them in sync — the game logic (wrapping, HUD, spawn positioning) all uses `W`/`H`.
- `README.md` is out of date: it mentions power-ups and a "estrella fugaz" asteroid type that **do not exist in `game.js`**. Trust the code; if you implement those features, update the README (it's in Spanish).

## Code conventions (follow the existing file)

- Comments, HUD text, and README are in **Spanish**; keep new ones consistent.
- Input uses `e.code` strings (`'ArrowLeft'`, `'Space'`). One-shot presses go through `pressed(code)` (consumes the `justPressed` flag); held state via `keys[code]`. Use `pressed()` for anything that must fire once per keypress.
- Game state is a module-level state machine: `state` is one of `'playing' | 'dead' | 'gameover'`, plus `score`, `lives`, `level`. `update(dt)` branches on it first.
- All entities have `update(dt)`, `draw()`, and a `dead` flag; dead ones are filtered each frame. World wraps toroidally via `wrap(v, max)`.
- Asteroid size data lives in the parallel arrays `RADII` / `SPEEDS` / `POINTS`, indexed by size `1..3` (`size 3` = large = 20 pts). New per-size stats go there, not inline.
- `loop()` clamps `dt` to 0.05 s max — physics constants assume seconds (px/s, rad/s).
