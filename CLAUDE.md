# Site layout reference

## Stack

Static HTML + Tailwind CSS via **Play CDN** (`https://cdn.tailwindcss.com`). No build step. Fonts from Google Fonts. All assets vendored under `assets/`.

## Tailwind theme extension

```js
tailwind.config = {
  theme: {
    extend: {
      fontFamily: {
        sans: ['"Work Sans"', 'system-ui', '-apple-system', 'sans-serif'],
      },
      colors: {
        accent: '#0078b8',  // blue — labels, eyebrow
        muted:  '#6e6e6e',  // secondary text — handles, captions, footer
      },
    },
  },
}
```

Body background is `#e9e9e9` (not in theme, applied as `bg-[#e9e9e9]`).

## Breakpoints — Option C (Tailwind md / lg / xl)

| State | Min-width | Padding | Content width | Column layout |
|---|---|---|---|---|
| base | — | `p-6` (24px) | viewport − 48px | 1 col |
| `md` | 768px | `p-12` (48px) | viewport − 96px → **672px** min | 2 col |
| `lg` | 1024px | `px-20 py-12` (80px / 48px) | viewport − 160px → **864px** | 2 col |
| `xl` | 1280px | `px-0 py-16` (64px) | **960px** max-width centered | 3 col (contact) |

Page shell: `flex flex-col gap-6 p-6 md:p-12 lg:px-20 lg:py-12 xl:max-w-[960px] xl:mx-auto xl:px-0 xl:py-16`

## Section structure

```
<main>                         flex-col gap-6
  <header.intro>               flex-col → md:flex-row gap-7/8/20
    <p.eyebrow-mobile>         block md:hidden
    <div.photo>                aspect-[420/359] → md:w-[220px] → lg:w-[200px] → xl:w-[240px]
    <div.body>                 flex-col gap-7, md:flex-1
      <p.eyebrow-desktop>      hidden md:block
      <h1.name>                text-[50px], lg:whitespace-nowrap
      <p.bio>                  xl:max-w-[500px]
  <div.vt-grid>                flex-col → md:flex-row, gap-10/6/10
    <section> × 2              flex-1 each
  <section.profiles>           flex-col
    <div.profiles-cols>        flex-col → md:flex-row gap-6/10
      <div.col> × 2            flex-1 each
  <section.contact>            flex-col
    <div.contact-grid>         grid-cols-1 → md:grid-cols-2 → xl:grid-cols-3
  <footer>                     flex justify-between
```

## Contact grid notes

`gap-x-6` (column gap only, **no row gap**). Using `gap-6` would add 24px between grid rows, creating a visible hole above WhatsApp in the 2-col layout where the third item wraps to row 2.

The 3-col layout is deferred to `xl` (1280px) rather than `lg` because at lg the columns are only ~272px wide (80px side padding + 24px gaps), too narrow for `sergeykanafyev@gmail.com` at 14px. At xl the 960px max-width with `gap-x-6` gives (960−48)/3 = 304px columns — wide enough for the full address with no truncation.

The Email column carries `md:border-r` and the Telegram column carries `xl:border-r` (both `border-black/[.08]`). These act as column separators so adjacent items in different columns don't appear merged. Email gets the border at md+ (it is never the last column). Telegram gets it only at xl, where it sits between Email and WhatsApp in the 3-col row.

## Photo positioning

The `<img>` inside `.photo` is `absolute inset-0 w-full h-full object-cover`. This removes intrinsic content from the div so that:
- At mobile (`w-full aspect-[420/359]`): width is 100% (definite) → aspect-ratio resolves height correctly.
- At `md`+ (`flex-none self-stretch aspect-auto`): width is fixed per breakpoint; height = body column height via stretch.

Photo widths: `md:w-[220px]` / `lg:w-[200px]` / `xl:w-[240px]`. The lg dip (200px) is because the header gap widens to 80px at lg, so a slightly smaller photo keeps the body column comfortable. xl grows back to 240px as the full 960px content width has room for it.

## Row pattern

Rows are non-interactive `<div>`s. Only the handle + arrow on the right side is a link:

```html
<div class="flex items-center justify-between gap-4 py-[13px] px-1 border-b border-black/[.08]">
  <span class="flex items-center gap-3.5 shrink-0">
    <img class="shrink-0 w-[18px] h-[18px] object-contain" ... />
    <span class="text-[17px] font-semibold whitespace-nowrap">Name</span>
  </span>
  <a class="flex items-center gap-2 text-[14px] min-w-0" href="..." target="_blank" rel="noopener">
    <span class="text-muted overflow-hidden text-ellipsis whitespace-nowrap">@handle</span>
    <span class="shrink-0">↗</span>
  </a>
</div>
```

Ventures/Tinkering rows use `py-3.5` (14px) and `text-[18px]` for the name. All others use `py-[13px]` and `text-[17px]`. The ↗ arrow inherits the main font (no `font-mono`).

### Right-side span classes by content type

| Content | Classes on the inner `<span>` |
|---|---|
| Short handle (`@username`) | `text-muted overflow-hidden text-ellipsis whitespace-nowrap` |
| Email address | `text-muted` — no overflow; contact grid is sized so the full address fits |
| Phone number | `text-muted whitespace-nowrap` — prevents breaks at hyphens; no truncation |

`overflow-hidden` on a flex item implicitly sets `min-width: 0`, allowing it to shrink and activating ellipsis. Omitting it (email, phone) keeps `min-width: auto` so the span never clips its content.

## Panel head pattern

```html
<div class="flex items-baseline justify-between pb-2 border-b border-black/[.18] text-[11px] gap-4 whitespace-nowrap">
  <span class="text-accent tracking-[0.04em]">SECTION LABEL</span>
  <span class="text-muted">caption</span>
</div>
```
