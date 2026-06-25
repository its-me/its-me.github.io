# its-me.github.io

Personal site for **Sergey Kanafyev** — a single, static page.

Published at https://its-me.github.io

## Stack

Plain HTML + **Tailwind CSS** (Play CDN) — no build step, no dependencies. Fonts (Wix Madefor Display, IBM Plex Mono) loaded from Google Fonts; all icons and the portrait vendored under `assets/`.

```
index.html      # markup + Tailwind utility classes
assets/         # portrait, brand icons (SVG), favicon
CLAUDE.md       # layout reference for AI-assisted editing
.nojekyll       # serve assets/ verbatim on GitHub Pages
```

## Responsive layout

Three breakpoints following Tailwind's default scale:

| Breakpoint | Min-width | Padding | Content width |
|---|---|---|---|
| base | — | 24px | fluid |
| `md` | 768px | 48px | fluid, 2-col |
| `lg` | 1024px | 80px | fluid, 3-col contact |
| `xl` | 1280px | 0 | 960px centered |

## Local preview

Open `index.html` directly, or serve the folder:

```sh
python3 -m http.server 8000
```

then visit http://127.0.0.1:8000

## Editing content

Names, links, and handles live as plain text in `index.html`. Colors and fonts are configured in the `tailwind.config` block at the top of `index.html`.
