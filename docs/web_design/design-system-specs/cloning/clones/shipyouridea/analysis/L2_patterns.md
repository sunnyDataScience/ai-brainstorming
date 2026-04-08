# L2 Patterns — shipyouridea

> 從 https://shipyouridea.today/ 的 static HTML 中觀察到的重複 UX/UI patterns。
> 對齊 `02_patterns_spec.md`。

**頂部註記。** shipyouridea.today 與 ideacheck.cc 共用 Next.js codebase。pattern 層級的主要 delta 是：（1）簡化的 anchor navigation（3 個 anchor vs 4 個）、以及（2）第一個 nav slot 從「服務」（Service）重新定義為「範例」（Example）。兩者合起來暗示這是一次 repositioning 實驗 — 同一份 codebase、更精簡的資訊架構、以 example-first 為 CTA 框架。

> Live 驗證註記：擷取當下的 server-rendered HTML 第一個 nav 標籤仍是「服務」，但 React 元件原始碼使用的是「範例」。3-vs-4 anchor 差異與「範例」重新定義在原始碼層級已確認；SSR snapshot 可能落後於已部署的 client bundle。

---

## 1. Sticky Backdrop Navigation

- **出現位置**：頂層 `<header>`（root layout，每個頁面）。
- **Pattern**：`sticky top-0 z-50 bg-white/80 backdrop-blur-md border-b border-gray-950/5`，3 欄 grid（logo / 置中連結 / actions）。
- **理由**：讓 nav 在長版 landing page 滾動時保持可見，同時在 hero 圖像上視覺上保持低調；backdrop blur 維持內容可讀性。
- **信心度**：HIGH
- **Spec 對應**：`02_patterns_spec.md` → Navigation Patterns → sticky header 變體。

## 2. Max-width Centered Container

- **出現位置**：landing、pricing、FAQ 的每個 section wrapper。
- **Pattern**：`mx-auto max-w-6xl px-6`（約 1152px 內容欄 + 24px gutter）。
- **理由**：單一標準內容寬度簡化垂直節奏，並在寬螢幕上保持 line-length 可讀性。
- **信心度**：HIGH
- **Spec 對應**：Layout Patterns → container token `container.max-6xl`。

## 3. Responsive Flex Column-to-Row

- **出現位置**：Hero CTA group、pricing card actions、FAQ rows。
- **Pattern**：`flex flex-col gap-4 sm:flex-row` — mobile 堆疊、由 `sm:` breakpoint 開始 inline。
- **理由**：單一來源的 layout 即可同時處理 touch 與 desktop，無需 media-query 分支；gap token 到處重用以維持一致間距。
- **信心度**：HIGH
- **Spec 對應**：Layout Patterns → responsive stack utility。

## 4. Simplified Anchor Navigation（與 ideacheck 的 pattern delta）

- **出現位置**：Header nav 連結。
- **Pattern**：剛好 3 個頁內 anchor — `#demo`、`#pricing`、`#faq`。ideacheck.cc 額外暴露 `#data-sources`。元件原始碼中的第一個 nav 標籤是「範例」（Example），取代了 ideacheck 的「服務」（Service）。
- **理由**：將產品重新定位為圍繞單一可展示範例，而非 feature/service catalog。移除 `#data-sources` 讓 IA 變短，並把證據推進 demo block 自身。這是 shipyouridea 變體的核心 repositioning 假說。
- **信心度**：HIGH（anchor 數量、原始碼標籤）；MEDIUM（live SSR 仍顯示「服務」 — 見頂部註記）。
- **Spec 對應**：Navigation Patterns → IA hierarchy；Differentiation → repositioning experiments。

## 5. Inline Interactive Demo Form

- **出現位置**：Hero 下方的 `InteractiveDemo` client component。
- **Pattern**：推測 — 單步 inline 表單（無 modal），client-rendered，可能 POST 到後端 route 進行 idea validation。
- **理由**：相較於 modal 或 route 導航，inline 表單降低摩擦；強化 pattern #4 的 example-first framing。
- **信心度**：LOW（元件為 client-side；static HTML 不含表單 markup）。
- **Spec 對應**：Form Patterns → inline single-step form。

## 6. Internationalization Shell

- **出現位置**：Root layout — `<html lang="zh-Hant">`、header 中的 `LanguageSwitcher`、包住整棵樹的 `LocaleProvider`。
- **Pattern**：Locale-aware provider + header 切換器；預設 locale 為繁體中文。
- **理由**：同一份 codebase 服務多個市場定位（ideacheck / shipyouridea）與可能的多語；集中在 provider 中可避免 per-page wiring。
- **信心度**：HIGH
- **Spec 對應**：Global Shell Patterns → i18n provider。

## 7. Auth Gate

- **出現位置**：root layout 中的 `AuthProvider`；route tree 中存在 `/login` route。
- **Pattern**：全域 auth context + 專屬登入 route；需受保護的動作推測會 redirect 到 `/login`。
- **理由**：讓 marketing 介面保持公開，同時保護 demo 提交 / 儲存 idea 的流程。
- **信心度**：HIGH
- **Spec 對應**：Auth Patterns → provider + route gate。

## 8. Metadata-First SEO

- **出現位置**：`/` 的 `<head>`。
- **Pattern**：完整 Open Graph 與 Twitter card meta — `og:title`、`og:description`、`og:image`（1200×630）、`og:url`、`og:type`，加上 `twitter:card=summary_large_image` 與對應的 `twitter:*` 欄位。
- **理由**：優化社群連結預覽，而社群是以 X/LinkedIn 貼文上線的 idea-validation 產品的主要傳播通路。
- **信心度**：HIGH
- **Spec 對應**：SEO Patterns → metadata-first。
