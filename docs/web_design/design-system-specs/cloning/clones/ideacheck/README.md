# Clone Target: ideacheck

> `ideacheck.cc` 的 Capture & Extract artifact 根目錄 — 一個台灣的 AI 驅動 startup idea validation SaaS。

---

## 基本資訊

| 欄位 | 值 |
|------|-----|
| Slug（資料夾名） | `ideacheck` |
| Target URL | `https://ideacheck.cc` |
| 擷取日期 | 2026-04-08 |
| 操作者 | clone-workflow agent (ideacheck-capture-extract unit) |
| 法律檢查 | [ ] robots.txt 確認 / [x] 僅公開首頁 SSR HTML，未下載 brand asset |

## 為什麼複製這個

- **看上它什麼**：乾淨的 zh-Hant SaaS landing — Next.js + Tailwind + Inter + 單一 indigo-600 強調色 + sticky `bg-white/80 backdrop-blur-md` nav，極簡到位。
- **想學的核心**：Token + Pattern + Template — 學繁中 SaaS landing 的最小骨架（5 個 client section：Hero / InteractiveDemo / DataSources / Pricing / FAQ）。
- **對應產品**：作為自家 zh-Hant SaaS landing 的骨架參考。

## 預設輸出範圍

- [x] L0 Foundations
- [x] L1 Components
- [x] L2 Patterns
- [x] L3 Templates
- [x] L4 Sitemap

## 進度追蹤

| 階段 | 狀態 | 完成日 | 備註 |
|------|------|--------|------|
| 1. Capture | ✅ | 2026-04-08 | `raw/dom.html` (14.5 KB) + `html-head-metadata.json` + `rsc-components.json` |
| 2. Extract | ✅ | 2026-04-08 | dom-tree, css-vars, media-queries, assets-inventory |
| 3. Analyze | ⬜ | | 待後續 unit |
| 4. Differentiate | ⬜ | | |
| 5. Specify | ⬜ | | |
| 6. Validate | ⬜ | | |

## 你的品牌覆蓋（給 Differentiate 階段參考）

- 主色：`#______`（待定，避開 indigo-600 #4F46E5）
- 次色：`#______`
- 字型：______（建議避開 Inter，改用 Noto Sans TC 或 LXGW WenKai TC 強化中文識別度）
- 受眾：______
- 風格定位：______

## 必避開的設計

- **直接複製 Hero 文案 / Pricing 方案**（屬於對方商業內容，不只是設計）
- **`logo-v2.png` / `og-image.png` / `favicon.ico`** — 必須以原創品牌資產替換
- **`bg-indigo-600` 強調色**（建議差異化，避免被誤認為 ideacheck 翻版）
- **完全相同的 nav 結構**（grid-cols-3 + sticky + backdrop-blur）— 可保留 pattern，但需有自家差異點

---

## 已知重複代碼基（IMPORTANT）

**`ideacheck.cc` 與 `shipyouridea.today` 共用同一份 Next.js 代碼基，僅換 brand。**

| 共同特徵 | 證據 |
|---|---|
| Tailwind + Inter (`inter_5972bc34`) | 相同 body className |
| `bg-background` CSS var | 相同 |
| `bg-indigo-600` 強調色 | 相同 |
| Sticky `bg-white/80 backdrop-blur-md border-b border-gray-950/5` nav | 相同 |
| `max-w-6xl` container | 相同 |
| `rounded-lg` button | 相同 |
| zh-Hant locale + © 2026 + LanguageSwitcher | 相同 |
| Component registry (Hero / InteractiveDemo / DataSources / Pricing / FAQ) | 相同 export 名 |

→ 推測為同一團隊 / 同一 Next.js boilerplate 兩個品牌實體。Analyze 階段應建立 `_comparison/ideacheck-vs-shipyouridea.md` 並列出 diff（logo、nav 連結、聯絡 email、配色微調）以萃取「共用 template」與「品牌變異點」。

---

## ideacheck.cc 站點具體事實

| 項目 | 值 |
|---|---|
| Title | `IdeaCheck — 你的點子能活多久？` |
| Description | `輸入你的產品點子，AI 從 7 個面向打分數，告訴你這個點子會怎麼死。` |
| Page sections (順序) | Hero → InteractiveDemo → DataSources → Pricing → FAQ |
| Primary nav | 服務 / 數據來源 / 價格 / FAQ |
| Logo | `/logo-v2.png` (28×28 nav, 24×24 footer) |
| Contact | `service@ideacheck.cc` |
| Locale | zh-Hant (`zh_TW`) |
| Build ID | `M61bP0CPahF6DmBfa7TKN` |

## 信心註記

Hero / InteractiveDemo / DataSources / Pricing / FAQ 為 client component，**內部 markup 不在 SSR HTML 中**。本次 capture 只能涵蓋 nav + footer + metadata；section 內部文案、表單、卡片等需在 Analyze 階段以 headless browser（Playwright / Puppeteer）補抓。所有 inner-section token / copy 在當前 artifact 中皆標記為 `confidence: low / TBD`。

## 檔案結構

```
ideacheck/
├── README.md                            ← 本檔
├── raw/
│   ├── dom.html                         ← curl 抓取的完整 SSR HTML
│   ├── html-head-metadata.json          ← title / meta / og / twitter / icon / preload
│   └── rsc-components.json              ← Next.js RSC component registry
└── extracted/
    ├── dom-tree.md                      ← 語意化 DOM 樹（含 client section 錨點）
    ├── css-vars.json                    ← Tailwind utility → design token 對應
    ├── media-queries.json               ← Tailwind breakpoint 觀察
    └── assets-inventory.md              ← 字型 / 圖片 / icon URL 清單（不下載）
```
