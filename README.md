# its-me.github.io

Personal site of **Sergey Kanafyev**, a single, static page.

Published at [https://its-me.github.io](https://its-me.github.io).

## Stack

- Plain HTML + Tailwind CSS via Play CDN, no build step
- Work Sans from Google Fonts
- Icons and portrait vendored under `assets/`

## Responsive layout

Three breakpoints:

| Breakpoint | Min-width | Padding | Content width |
|---|---|---|---|
| base | — | 24px | fluid |
| `md` | 768px | 48px | fluid, 2-col |
| `lg` | 1024px | 80px | fluid, 2-col |
| `xl` | 1280px | 0 | 960px centered, 3-col contact |

## Local preview

Serve the folder:

```sh
python3 -m http.server 8000
```

Then open [http://127.0.0.1:8000](http://127.0.0.1:8000).

Or open `index.html` directly in a browser.
