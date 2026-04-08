# Assets Inventory — shipyouridea.today

> 於 2026-04-08 從 `raw/dom.html` 擷取。僅以 URL 參照 — 本 repo 不下載任何 binary。

## Fonts

| Asset | URL | Type | 備註 |
|---|---|---|---|
| Inter (next/font local) | `https://shipyouridea.today/_next/static/media/83afe278b6a6bb3c-s.p.0q-301v4kxxnr.woff2` | `font/woff2` | 以 `crossOrigin=""` 預載。**與 ideacheck.cc 為相同的 file hash**，確認兩站是從共用的 Next.js codebase 出貨。CSS class hook：`inter_5972bc34-module__OU16Qa__className`。 |

## Logos / Brand

| Asset | URL | 使用位置 | 尺寸 | 備註 |
|---|---|---|---|---|
| Primary logo | `https://shipyouridea.today/logo-v2.png` | Nav（sticky header） | `36 × 36` | 搭配 wordmark `ShipYourIdea`（`text-base font-bold`）。 |
| Footer logo | `https://shipyouridea.today/logo-v2.png` | Footer | `32 × 32` | 相同來源檔案，渲染尺寸較小。 |

> 不得將 logo 檔案或 wordmark 複製到本 repo。

## Icons

| Asset | URL | 尺寸 | Type | 備註 |
|---|---|---|---|---|
| Favicon | `https://shipyouridea.today/favicon.ico?favicon.16i07ngvr~7f_.ico` | `64x64` | `image/x-icon` | 與 ideacheck.cc 不同，後者提供 `48x48` favicon。 |

## Social / Open Graph

| Asset | URL | 尺寸 | 使用於 |
|---|---|---|---|
| OG image | `https://shipyouridea.today/og-image.png` | `1200 × 630` | `og:image`、`twitter:image`。Alt text：`ShipYourIdea — AI 創業點子驗證工具`。 |

## Stylesheets

| Asset | URL | 備註 |
|---|---|---|
| Compiled CSS | `https://shipyouridea.today/_next/static/chunks/08xfyi~fk9y64.css` | 以 stylesheet 方式預載。包含實際的 Tailwind 設定 — 本次 capture 未解析。 |

## 第三方

| Asset | URL | 用途 |
|---|---|---|
| Cloudflare Insights beacon | `https://static.cloudflareinsights.com/beacon.min.js/v8c78df7c7c0f484497ecbca7046644da1771523124516` | 網站分析（token `0e6a85f1486a4c4292b3a05bf489c165`）。 |

## 與 ideacheck.cc 的資產 hash 比對

| 屬性 | shipyouridea.today | ideacheck.cc | 相同？ |
|---|---|---|---|
| Inter woff2 hash prefix | `83afe278b6a6bb3c` | `83afe278b6a6bb3c` | YES（共用 codebase） |
| Logo filename | `logo-v2.png` | （不同 brand） | NO |
| Favicon 尺寸 | `64x64` | `48x48` | NO |
| OG image 尺寸 | `1200x630` | `1200x630` | YES（template 預設） |
