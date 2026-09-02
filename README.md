# Life!

A single-file HTML/CSS/JS life-sim game — decorate your house, drive around the neighborhood, visit friends, go to work, and go to school.

## Running locally

Just open `index.html` in a browser, or serve the folder with any static file server:

```
npx serve .
```

## Deploying to Vercel

This is a static site with no build step, so Vercel will deploy it automatically:

1. Import this repo in [Vercel](https://vercel.com/new).
2. Framework preset: **Other** (or leave auto-detected).
3. Build command: none. Output directory: `.` (root, since `index.html` lives there).
4. Deploy.

Or via the CLI:

```
npx vercel --prod
```
