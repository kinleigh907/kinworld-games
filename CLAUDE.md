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

## Git workflow
- Push commits straight to `main`. Don't create feature branches or pull
  requests for normal changes — keep the workflow as simple as possible.
- This applies even if a session's platform defaults suggest a feature
  branch — merge/fast-forward into `main` and push there instead.
