# Differentiation — shipyouridea

> 來源：[https://shipyouridea.today/](https://shipyouridea.today/)
> 日期：2026-04-08
> Codebase：與 `ideacheck.cc` 共用的 Next.js app（lite 變體）

---

## 來源網站定位

- 受眾：早期 indie hacker / solo founder，想快速「驗證一個點子值不值得做」
- 風格：極簡、indigo 主色、Inter 字體、單頁滾動、demo 先行
- 強項：4 區段精瘦結構（Hero → Demo → Pricing → FAQ）；sticky backdrop nav；快速 anchor 跳轉；OG metadata 完整

## 你的產品定位

- 受眾：TBD（替換為你的目標受眾）
- 風格：保留極簡 1-page 節奏，但更強調 SEO 與無障礙
- 差異點：在同樣的精瘦骨架上加上 SSR、a11y、structured data，讓 lite 變體不再因 CSR 失去 SEO

---

## 站點觀察（此 clone 特有）

> shipyouridea.today 是 ideacheck.cc 的「lite」變體 — 共用 codebase、章節更少、nav 更精簡。這是「同 codebase 多 brand A/B 測試」的真實案例。此處的 KEEP/DROP 決策必須先決定你要 clone 的是 lite（demo-first）還是 full（trust-first）敘事。

含義：

- 若你抄的是 lite，主軸是「先看 demo 再決定」，CTA 應接到互動元件而非長 landing
- 若你需要更高 trust signal（testimonial、case study、團隊介紹），請參考 ideacheck 的 differentiation，不要硬塞進這份 lite spec

---

## ✅ 值得保留（KEEP）


| 設計決策                                                | 為什麼好                            | 如何納入                                               |
| --------------------------------------------------- | ------------------------------- | -------------------------------------------------- |
| Sticky backdrop-blur nav                            | 永遠可達 CTA，又不擋內容                  | L1 Navigation 元件加 `backdrop-blur` + `sticky top-0` |
| `max-w-6xl` (1152px) container                      | 對 1-page landing 來說剛好，不會太寬而失焦   | L0 `layout.container.max-width = 1152px`           |
| Indigo-600 主色                                       | 高對比、CTA 明確、與白底 4.83:1 過 WCAG AA | 作為 baseline，後續 OVERRIDE 為自己品牌色                     |
| Inter 字型                                            | 開源、screen-optimized、字重齊全        | L0 `font.family.sans = Inter`                      |
| 4-section lean landing（Hero → Demo → Pricing → FAQ） | 認知負擔最小、轉換路徑單一                   | L3 template `landing-lean.md`                      |
| Anchor scroll 導覽                                    | 不需頁面切換、保持 context               | L2 pattern `anchor-nav`                            |
| OG metadata 完整                                      | 社群分享自帶卡片                        | L0 metadata baseline                               |


## ⚠️ 不適合（DROP）


| 元素                                | 為什麼不適合                                  |
| --------------------------------- | --------------------------------------- |
| `ShipYourIdea` 品牌名 / logo         | 商標，禁止抄                                  |
| `.today` TLD 品牌操作                 | 是來源獨有的命名 gimmick                        |
| 任何 hero / demo / pricing / FAQ 內文 | 著作權，需重寫                                 |
| 來源的 scoring 產品邏輯                  | 是 ideacheck 的核心 IP，lite 版只是 marketing 殼 |
| 來源的 contact email                 | 屬於來源組織                                  |


## 🎨 品牌覆蓋（OVERRIDE）


| 來源 Token                    | 來源值                    | 你的 Token                    | 你的值            |
| --------------------------- | ---------------------- | --------------------------- | -------------- |
| `color.brand.primary`       | `#4f46e5` (indigo-600) | `color.brand.primary`       | TBD（替換為自己色）    |
| `color.brand.primary.hover` | `#4338ca` (indigo-700) | `color.brand.primary.hover` | TBD            |
| `font.family.heading`       | Inter                  | `font.family.heading`       | TBD（可保留 Inter） |
| `brand.logo`                | ShipYourIdea wordmark  | `brand.logo`                | 自己 logo        |
| `brand.contact.email`       | （來源 email）             | `brand.contact.email`       | 你自己的聯絡 email   |
| `meta.og.image`             | 來源 OG 卡                | `meta.og.image`             | 自製 OG 卡        |


## 💡 改進機會（IMPROVE）

1. **SEO — robots meta**：若來源 production 上有 `noindex` 殘留，正式上線時改成 `index, follow`，並補上 canonical URL
2. **SEO — SSR 關鍵段落**：把 Pricing / FAQ 從 client-rendered 改為 SSR（Next.js `app/` 預設 server component），讓爬蟲看得到價格與 Q&A，並順帶改善 LCP
3. **Accessibility — skip-link + ARIA landmarks**：第一個 focusable 元素為 `<a href="#main">Skip to content</a>`；`<header role="banner">`、`<main role="main" id="main">`、`<footer role="contentinfo">` 補齊
4. **SEO — Structured Data JSON-LD**：在 `<head>` 加 `SoftwareApplication` schema（含 `name`, `applicationCategory`, `offers.price`, `aggregateRating` 若有），讓 Google 顯示 rich result
5. **Performance**：preconnect Inter 字型 CDN、`font-display: swap`、圖片 `next/image` priority for hero

## 結論

> shipyouridea.today 是值得抄的「lean landing」骨架，但因為它是 ideacheck 的 lite marketing 變體，clone 時要決定你做的是 demo-first 還是 trust-first 敘事。骨架（nav / container / 4 sections / indigo / Inter）保留；品牌、文案、產品邏輯換掉；同時補上 SSR、a11y、JSON-LD 三件來源缺的功課，clone 出來會比原站更穩。

