# Clone Target: shipyouridea

> 每個複製專案的入口檔案。先填這份再開始六階段。

> ⚠️ **本站與 ideacheck.cc 共用同一份 Next.js codebase** — 相同的 font 檔案 hash（`83afe278b6a6bb3c`）、相同的 Tailwind class patterns、相同的 component registry 形狀、相同的 `LanguageSwitcher`、相同的 `© 2026` footer copy。此 clone 有價值的產出是**與 ideacheck.cc 的 comparative differentiation**，而非原始結構 capture。

---

## 基本資訊

| 欄位 | 值 |
|------|-----|
| Slug（資料夾名） | `shipyouridea` |
| Target URL | `https://shipyouridea.today` |
| 擷取日期 | 2026-04-08 |
| 操作者 | shipyouridea-capture-extract unit |
| 法律檢查 | [x] 僅公開頁面（landing） / [ ] robots.txt 確認（HTML 帶 `meta robots="noindex"`，僅針對搜尋索引，不影響公開抓取的合法性，但需謹慎使用） |

## 為什麼複製這個

- 你看上它什麼？台灣本地化的 AI 創業點子驗證 SaaS landing（繁中 zh-Hant），與 ideacheck.cc 同源但走簡化變體 — 是少見的「同骨架不同 brand/scope」對照樣本。
- 想學的核心：Sitemap / Templates 對照（觀察一個共用骨架如何被刪掉一個 section、改 brand、改 favicon 後成為「看似不同」的產品）。
- 對應到你哪個產品？任何需要「同 codebase 多 brand」策略的 SaaS landing 系列。

## 預設輸出範圍

- [x] L0 Foundations
- [x] L1 Components
- [x] L2 Patterns
- [x] L3 Templates
- [x] L4 Sitemap

## 進度追蹤

| 階段 | 狀態 | 完成日 | 備註 |
|------|------|--------|------|
| 1. Capture | ✅ | 2026-04-08 | HTTP 500 (`__next_error__`) 但 RSC payload 完整序列化，nav/footer 與 component registry 全部到手。Hero/Demo/Pricing/FAQ 為 client-rendered。 |
| 2. Extract | ✅ | 2026-04-08 | dom-tree、css-vars、media-queries、assets-inventory 全部完成。 |
| 3. Analyze | ⬜ | | |
| 4. Differentiate | ⬜ | | 重點：對照 ideacheck.cc 找出共用樣板 vs 真正差異點。 |
| 5. Specify | ⬜ | | |
| 6. Validate | ⬜ | | |

## 你的品牌覆蓋（給 Differentiate 階段參考）

- 主色：`#______`（觀察值：`bg-indigo-600` = `#4f46e5`）
- 次色：`#______`
- 字型：______（觀察值：Inter via next/font local）
- 受眾：______
- 風格定位：______

## 必避開的設計

- 不要直接抄 `bg-indigo-600` 主按鈕 + sticky `bg-white/80 backdrop-blur-md` nav 組合 — 這是同骨架兩站共用的「無差異化」預設外觀。
- 不要照抄 `max-w-6xl` + 三欄 grid nav 的精確比例 — 這是 Next.js 模板痕跡。

## Capture 要點摘要

- 站台只註冊四個 page-level client component：**Hero → InteractiveDemo → Pricing → FAQ**。
- ⚠️ **沒有 DataSources section**（ideacheck.cc 有）— 透過 `grep -c '"DataSources"' raw/dom.html` 驗證為 0。這是兩站之間最顯著的結構差異。
- Nav 連結：範例 / 價格 / FAQ。Footer 連結：價格 / FAQ / 聯絡我們 (`mailto:service@shipyouridea.today`) / 隱私權政策 / 服務條款。
- Logo 在 nav 為 36×36，footer 為 32×32（同檔案 `/logo-v2.png`）。
- Favicon 64×64（vs ideacheck.cc 的 48×48）。
- OG image 1200×630。
- HTML `lang="zh-Hant"`，body class `inter_5972bc34-module__OU16Qa__className min-h-screen bg-background antialiased`。
- Build id: `UkVvqOg2r4imiTx9mVAsu`。

## Files

| Path | 用途 |
|---|---|
| `raw/dom.html` | 擷取下來的 HTML（HTTP 500 shell + 完整 RSC stream） |
| `raw/html-head-metadata.json` | 解析過的 `<head>` metadata |
| `raw/rsc-components.json` | 從 RSC payload 解析出的 component registry |
| `extracted/dom-tree.md` | 簡化的語意 DOM 樹 |
| `extracted/css-vars.json` | Tailwind utility classes → 推導出的 design tokens（含使用次數） |
| `extracted/media-queries.json` | 實際使用到的 Tailwind breakpoints |
| `extracted/assets-inventory.md` | Fonts、logos、icons、OG、第三方資源 |
