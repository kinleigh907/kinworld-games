# Kinworld Games

A collection of single-file HTML/CSS/JS games with a left sidebar menu to
switch between them.

- `index.html` — the game picker/launcher. Small and simple: it just shows
  the sidebar and loads the picked game into an iframe.
- `games/life.html` — Life!, a life-sim game — decorate your house, drive
  around the neighborhood, visit friends, go to work, and go to school.
- `games/placeholder.html` — an empty starter page for the next game.

## Why split into separate files?

Each game lives in its own file under `games/`. That way, when you (or
Claude) work on one game, only that file needs to be opened and edited —
you're not reading through every other game's code just to make one
change. This keeps edits fast and cheap.

## Adding a new game

1. Copy `games/placeholder.html` to a new file in `games/`, e.g.
   `games/mygame.html`, and build your game there. Each game file should
   stay self-contained (its own `<style>` and `<script>`, no shared
   files) so it's easy to work on by itself.
2. Open `index.html` and add a new button in the sidebar, e.g.:
   ```html
   <button class="gameBtn" data-src="games/mygame.html">My Game</button>
   ```

## Running locally

Just open `index.html` in a browser, or serve the folder with any static
file server:

```
npx serve .
```

## Deploying to Vercel

This is a static site with no build step, so Vercel will deploy it
automatically:

1. Import this repo in [Vercel](https://vercel.com/new).
2. Framework preset: **Other** (or leave auto-detected).
3. Build command: none. Output directory: `.` (root, since `index.html`
   lives there).
4. Deploy.

Or via the CLI:

```
npx vercel --prod
```
