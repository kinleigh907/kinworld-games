# Project notes for Claude

## Context
This is a game project built by a 9 year old on an iPad. Keep everything
as simple as possible:
- Prefer plain, readable single-file HTML/CSS/JS over build tools, bundlers,
  frameworks, or extra dependencies.
- Avoid introducing new tooling (linters, package managers, TypeScript, etc.)
  unless explicitly asked for.
- Favor small, easy-to-follow changes over clever or abstracted code.

## Repo structure
- `index.html` is just the game picker: a left sidebar (a top bar on
  narrow screens) that loads the chosen game into an iframe. Keep it
  small — it should not contain any game logic.
- Each game lives in its own self-contained file under `games/`
  (its own `<style>` and `<script>`, no files shared between games).
- To add a new game:
  1. Copy `games/placeholder.html` to `games/yourgame.html` and build
     the game there.
  2. Add one button to the sidebar in `index.html`:
     `<button class="gameBtn" data-src="games/yourgame.html">Your Game</button>`
- Why split like this: when working on one game, only that game's file
  needs to be read and edited, not the others. This keeps changes fast
  and keeps token usage down as more games get added.

## Mobile friendliness
We play on phones a lot, so every game must work well on a phone screen,
not just an iPad/desktop. `games/placeholder.html` already includes the
"mobile-safe base" CSS block described below — keep it when you copy the
template for a new game, and don't remove it from `games/life.html`.

- **One scroll container.** The page (`body`) can scroll vertically if a
  game is tall, but avoid nesting extra scrolling boxes inside it. If you
  do need an inner scrolling box (like the furniture shop tray), always
  give it an explicit `width: 100%; box-sizing: border-box;` — a
  scrolling box without a fixed width can grow to fit its content and
  blow out past the edge of the phone screen, dragging the whole page
  sideways. This exact bug happened once in `games/life.html`; don't
  reintroduce it.
- **No sideways scrolling of the page itself.** `html` and `body` should
  keep `overflow-x: hidden`. If something looks cut off on a narrow
  screen, fix its width — don't just let the page scroll sideways to
  reveal it.
- **Stop rubber-band bounce from stealing taps.** Keep
  `overscroll-behavior: none` on `html`/`body` (and `overscroll-behavior-x:
  contain` plus `touch-action: pan-x` on any horizontally-scrolling strip)
  so dragging near an edge doesn't bounce-scroll the whole page while
  someone's trying to tap a control.
- **Buttons should feel instant.** Give buttons and other tappable
  elements `touch-action: manipulation; user-select: none;
  -webkit-tap-highlight-color: transparent;` so taps aren't mistaken for
  scroll/zoom gestures and don't flash a highlight or select text.
- **Layout in relative units.** Use `width: 100%` with a `max-width`
  (like the existing `.panel { width: 100%; max-width: 400px; }`
  pattern) instead of fixed pixel widths for anything that should shrink
  to fit a small phone screen.
- Before calling a mobile change done, check it at a small phone width
  (~375px) — resize a browser window or use its device toolbar — and
  confirm nothing scrolls sideways and every button is reachable and
  tappable.

## Git workflow
- Push commits straight to `main`. Don't create feature branches or pull
  requests for normal changes — keep the workflow as simple as possible.
- This applies even if a session's platform defaults suggest a feature
  branch — merge/fast-forward into `main` and push there instead.
