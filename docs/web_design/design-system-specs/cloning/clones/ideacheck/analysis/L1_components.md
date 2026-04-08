# L1 Components — ideacheck

> Source: static HTML / RSC payload from `https://ideacheck.cc/`
> Method: server-rendered markup observation only (no DOM/CSSOM)
> Date: 2026-04-08

> **Note**: ideacheck.cc shares its Next.js codebase with shipyouridea.today.
> Components are nearly identical; see `_comparison` doc for logo size deltas
> (ideacheck uses 28px/24px logo; nav links include 服務 and 數據來源).

---

## Button / Primary (Login)

Top-right CTA in the header. Single observed instance routes to `/login`.

### Tailwind classes (verbatim)

```
inline-flex h-8 items-center rounded-lg bg-indigo-600 px-4 text-sm font-medium text-white transition hover:bg-indigo-700
```

### Token decomposition

| Property | Value |
|---|---|
| display | inline-flex |
| height | 2rem (32px) |
| radius | 0.5rem (rounded-lg) |
| bg (default) | indigo-600 |
| bg (hover) | indigo-700 |
| px | 1rem |
| font-size | 0.875rem (text-sm) |
| font-weight | 500 (font-medium) |
| color | white |
| transition | all (transition) |

### States observed
- default
- hover (class-driven)

### Variants observed
- primary only (no secondary/ghost in static HTML)

### Confidence
**HIGH** — class string and DOM position both observable in RSC payload.

---

## Nav / Top

Sticky header containing logo (left), nav links (center), login + LanguageSwitcher (right).

### Tailwind classes (verbatim)

Outer:
```
sticky top-0 z-50 w-full border-b border-gray-950/5 bg-white/80 backdrop-blur-md
```

Inner grid:
```
mx-auto grid max-w-6xl grid-cols-3 items-center px-6 py-3
```

Center link cluster:
```
hidden sm:flex gap-8
```

### Structure

| Slot | Content |
|---|---|
| left | Logo (28x28) + brand text |
| center | Nav links (hidden < sm) |
| right | Login button + LanguageSwitcher |

### States
- default (no observable scroll/hover variant in HTML)

### Confidence
**HIGH** — full class strings + slot structure visible in RSC payload.

---

## Footer

### Tailwind classes (verbatim)

Outer:
```
border-t border-gray-950/5 px-6 py-10
```

Inner row:
```
mx-auto flex max-w-6xl flex-col items-center justify-between gap-4 sm:flex-row
```

### Content

- Brand cluster: Logo (24x24) + brand text (`text-sm font-bold`)
- Nav links (7 items, in observed order):
  1. 服務
  2. 數據來源
  3. 價格
  4. FAQ
  5. 聯絡我們
  6. 隱私權政策
  7. 服務條款

### States
- default

### Confidence
**HIGH** — class strings and 7 link labels observable in static HTML.

---

## Nav Link

Two contexts: header and footer. Both are anchor elements.

### Tailwind classes (verbatim)

Header variant:
```
text-sm font-medium text-gray-500 transition-colors hover:text-gray-950
```

Footer variant:
```
text-sm text-gray-400 transition-colors hover:text-gray-600
```

### Variants
- header (medium weight, gray-500 → gray-950)
- footer (regular weight, gray-400 → gray-600)

### States
- default
- hover (class-driven)

### Confidence
**HIGH**

---

## Logo

Image asset reused in nav and footer.

### Source

`/logo-v2.png`

### Variants

| Context | Width × Height | Label class |
|---|---|---|
| Nav | 28 × 28 | `text-base font-bold` |
| Footer | 24 × 24 | `text-sm font-bold` |

### Notes
- Brand asset — do **not** copy in clone implementations.
- Size deltas vs shipyouridea.today are documented in the `_comparison` file.

### Confidence
**HIGH**

---

## LanguageSwitcher

Client component referenced in the RSC payload (right slot of the header).
Inner markup is hydrated client-side.

### Observable
- Mount point exists in the right grid cell of `Nav / Top`.

### Not observable
- Trigger button class strings
- Dropdown panel structure
- Locale list

### Confidence
**LOW** — presence only; structure not in static HTML.

---

## Hero / InteractiveDemo / DataSources / Pricing / FAQ / IconMark

These component identifiers appear in the RSC component registry but render
client-side or as client islands. Static HTML does not expose their internal
structure.

| Component | Static HTML evidence | Confidence |
|---|---|---|
| Hero | identifier in payload only | LOW |
| InteractiveDemo | identifier in payload only | LOW |
| DataSources | identifier in payload only | LOW |
| Pricing | identifier in payload only | LOW |
| FAQ | identifier in payload only | LOW |
| IconMark | identifier in payload only | LOW |

> **Status**: client-rendered — structure not observable in static HTML.
> Requires DOM-level capture (Playwright / browser snapshot) for L1 expansion.

---

## 元件信心度總表

| 元件 | 信心度 | 來源 |
|---|---|---|
| Button / Primary | HIGH | RSC payload class string |
| Nav / Top | HIGH | RSC payload structure + classes |
| Footer | HIGH | RSC payload structure + classes |
| Nav Link (header) | HIGH | RSC payload class string |
| Nav Link (footer) | HIGH | RSC payload class string |
| Logo | HIGH | `<img>` src + dimensions |
| LanguageSwitcher | LOW | mount point only |
| Hero | LOW | registry identifier |
| InteractiveDemo | LOW | registry identifier |
| DataSources | LOW | registry identifier |
| Pricing | LOW | registry identifier |
| FAQ | LOW | registry identifier |
| IconMark | LOW | registry identifier |

---

## Cross-site note

ideacheck.cc and shipyouridea.today share the same Next.js codebase.
Components documented above are **nearly identical** to the sister site;
the meaningful deltas are:

- Logo dimensions (28/24 here vs sister site values — see `_comparison`)
- Nav link labels include `服務` and `數據來源`

See `clones/_comparison/` (when authored) for the full delta matrix.
