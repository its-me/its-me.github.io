# its-me.github.io

Personal site for **Sergey Kanafyev** — a single, static page.

## Stack

Plain HTML + CSS — no build step, no dependencies. Fonts (Wix Madefor Display, IBM Plex Mono) are loaded from Google Fonts; all icons and the portrait ara vendored under `assets/`.

```
index.html      # markup
styles.css      # styles + responsive rules
assets/         # portrait, brand icons (SVG), GitHub follow badge
.nojekyll       # serve assets/ verbatim on GitHub Pages
```

## Local preview

Open `index.html` directly, or serve the folder:

```sh
python3 -m http.server 8000
# then visit http://localhost:8000
```

## Deploy to GitHub Pages

This repo is named `its-me.github.io`, so it publishes as a **user site** at `https://its-me.github.io`.

```sh
git init
git add .
git commit -m "Personal site"
git branch -M main
git remote add origin git@github.com:its-me/its-me.github.io.git
git push -u origin main
```

Then in the repo: **Settings → Pages → Build and deployment → Source: Deploy from a branch**, branch `main` / root. The site goes live within a minute or two.

## Editing content

Names, links, and handles live as plain text in `index.html`. Design tokens
(colors, fonts, spacing) are CSS custom properties at the top of `styles.css`.
