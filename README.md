# its-me.github.io

Personal site for **Sergey Kanafyev** — a single, static page.

Published at https://its-me.github.io

## Stack

Plain HTML + CSS — no build step, no dependencies. Fonts (Wix Madefor Display, IBM Plex Mono) are loaded from Google Fonts; all icons and the portrait are vendored under `assets/`.

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
```

then visit http://127.0.0.1:8000

## Editing content

Names, links, and handles live as plain text in `index.html`. Design tokens
(colors, fonts, spacing) are CSS custom properties at the top of `styles.css`.
