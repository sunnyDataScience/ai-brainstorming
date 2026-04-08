# Assets Inventory — shipyouridea.today

> Captured 2026-04-08 from `raw/dom.html`. Reference by URL only — no binaries are downloaded into this repo.

## Fonts

| Asset | URL | Type | Notes |
|---|---|---|---|
| Inter (next/font local) | `https://shipyouridea.today/_next/static/media/83afe278b6a6bb3c-s.p.0q-301v4kxxnr.woff2` | `font/woff2` | Preloaded with `crossOrigin=""`. **Same file hash as ideacheck.cc**, confirming the two sites ship from a shared Next.js codebase. CSS class hook: `inter_5972bc34-module__OU16Qa__className`. |

## Logos / Brand

| Asset | URL | Used in | Dimensions | Notes |
|---|---|---|---|---|
| Primary logo | `https://shipyouridea.today/logo-v2.png` | Nav (sticky header) | `36 × 36` | Paired with wordmark `ShipYourIdea` (`text-base font-bold`). |
| Footer logo | `https://shipyouridea.today/logo-v2.png` | Footer | `32 × 32` | Same source file, smaller render. |

> Do not copy the logo file or wordmark into this repo.

## Icons

| Asset | URL | Sizes | Type | Notes |
|---|---|---|---|---|
| Favicon | `https://shipyouridea.today/favicon.ico?favicon.16i07ngvr~7f_.ico` | `64x64` | `image/x-icon` | Differs from ideacheck.cc, which serves a `48x48` favicon. |

## Social / Open Graph

| Asset | URL | Dimensions | Used by |
|---|---|---|---|
| OG image | `https://shipyouridea.today/og-image.png` | `1200 × 630` | `og:image`, `twitter:image`. Alt text: `ShipYourIdea — AI 創業點子驗證工具`. |

## Stylesheets

| Asset | URL | Notes |
|---|---|---|
| Compiled CSS | `https://shipyouridea.today/_next/static/chunks/08xfyi~fk9y64.css` | Preloaded as stylesheet. Contains the actual Tailwind config — not parsed in this capture. |

## Third-party

| Asset | URL | Purpose |
|---|---|---|
| Cloudflare Insights beacon | `https://static.cloudflareinsights.com/beacon.min.js/v8c78df7c7c0f484497ecbca7046644da1771523124516` | Web analytics (token `0e6a85f1486a4c4292b3a05bf489c165`). |

## Asset hash comparison vs ideacheck.cc

| Attribute | shipyouridea.today | ideacheck.cc | Same? |
|---|---|---|---|
| Inter woff2 hash prefix | `83afe278b6a6bb3c` | `83afe278b6a6bb3c` | YES (shared codebase) |
| Logo filename | `logo-v2.png` | (different brand) | NO |
| Favicon size | `64x64` | `48x48` | NO |
| OG image dimensions | `1200x630` | `1200x630` | YES (template default) |
