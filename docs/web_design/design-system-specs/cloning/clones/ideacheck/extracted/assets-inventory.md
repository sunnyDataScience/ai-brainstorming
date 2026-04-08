# IdeaCheck — Asset Inventory

> 來源：`raw/dom.html`（2026-04-08）
> 原則：**只記錄 URL 與用途，絕不下載 brand asset。** 重新實作必須以原創資產替換。

## Fonts

| 名稱 | URL | 格式 | 來源 | 用途 |
|---|---|---|---|---|
| Inter (next/font self-hosted subset) | `https://ideacheck.cc/_next/static/media/83afe278b6a6bb3c-s.p.0q-301v4kxxnr.woff2` | woff2 | Next.js `next/font/google` | body 全站字型；body className `inter_5972bc34-module__OU16Qa__className` |

預載：`<link rel="preload" as="font" href="…woff2" type="font/woff2" crossorigin />`

## Images

| 名稱 | URL | 尺寸 | 用途 | 備註 |
|---|---|---|---|---|
| Logo (nav) | `https://ideacheck.cc/logo-v2.png` | 28×28 | 頂部 sticky nav 品牌標 | next/image |
| Logo (footer) | `https://ideacheck.cc/logo-v2.png` | 24×24 | 頁尾品牌標 | 同檔案，不同尺寸 |
| OG image | `https://ideacheck.cc/og-image.png` | 1200×630 | OpenGraph / Twitter card | alt: "IdeaCheck — AI 創業點子驗證工具" |

## Icons

| 名稱 | URL | 尺寸 | 用途 |
|---|---|---|---|
| Favicon | `https://ideacheck.cc/favicon.ico?favicon.0tdrde6t7jpyv.ico` | 48×48 | 瀏覽器分頁 / bookmark |

## Stylesheets / Scripts (reference only)

| 種類 | URL |
|---|---|
| Tailwind compiled CSS | `https://ideacheck.cc/_next/static/chunks/021hm9y1r3r_x.css` |
| RSC framework chunks | `/_next/static/chunks/0y~2fdjrei_x4.js`, `0sb3q3mewmjjl.js`, `04~1xt_2_4sdp.js`, `01ysuzph9d_d2.js`, `10.bkg6_hbec_.js`, `17r8~3es_404n.js` |

## 法律/版權注意

- `logo-v2.png`、`og-image.png`、`favicon.ico` 為 IdeaCheck 品牌資產，**不得在 clone 中重用或衍生**。
- Inter 字型本身為 SIL OFL 1.1 授權，可自由使用，但**不要 hotlink** 對方 CDN — 改用本地 next/font 重新打包。
- 待 Differentiate 階段以自家品牌資產替換所有 brand entry。
