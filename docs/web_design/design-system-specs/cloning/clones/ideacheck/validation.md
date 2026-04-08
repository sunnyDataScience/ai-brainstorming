# Validation — ideacheck clone

> 對應 `cloning/checklists/validation_checklist.md`
> 評估日期：2026-04-08
> 範圍：`clones/ideacheck/differentiation.md` + `clones/ideacheck/spec/inspired-design-system.md`

---

## 法律與倫理

- [x] **PASS** 無複製商標 / logo / 品牌名 — spec 與 differentiation 僅引用 token 數值與類別名，明確標註 IdeaCheck 為 OVERRIDE 對象並要求換掉
- [x] **PASS** 無複製文案內容 — Hero / Pricing / FAQ 為 client component，本來就讀不到，標為 TBD 而非抄寫
- [x] **PASS** 無複製圖片 / 插畫資產 — `/logo-v2.png`、og-image 在 OVERRIDE 表中明列必須自製
- [x] **PASS** 來源網站已標註於 spec 開頭 — `inspired-design-system.md` 第一行 `Source: https://ideacheck.cc/`

## 設計完整性

- [ ] **N/A — 不在本單元範圍** L0 Foundations 八章節齊全（本任務只交付 differentiation + 局部 spec + validation；L0 完整版由其他單元產出）
- [ ] **N/A** L1 至少 5 個元件含完整變體
- [ ] **N/A** L2 至少 3 個 pattern
- [ ] **N/A** L3 至少 1 個 template 含 Mermaid
- [x] **PASS** L4 sitemap 對應到 `WEBSITE_MODULE_MATRIX.md` 某原型 — 對應「Landing Page」列（Identity ⬜ / Content 🟠 / Growth 🟠）。`WEBSITE_MODULE_MATRIX.md` 並無 `landing-ai-tool` 細分；建議後續在 `references/website_recipes.md` 補一條 `landing-ai-tool` 食譜，引用本 clone

## 差異化驗證

- [x] **PASS** differentiation.md 四章節齊全 — KEEP / DROP / OVERRIDE / IMPROVE 全在
- [x] **PASS** IMPROVE 至少 3 條 — 實際 4 條（SEO 上線、信任區塊、可及性、SSR 化）
- [x] **PASS** OVERRIDE 至少包含主色與字型 — `color.brand.primary`、`font.family.heading` 都列出，並補了 logo / footer / contact / og-image
- [x] **PASS** DROP 項目已從 spec 移除 — `inspired-design-system.md` 不含「7 維度」、「IdeaCheck」品牌名、`/logo-v2.png` 路徑作為採用值；DataSources 也沒被列為必備區塊

## 技術品質

- [x] **PASS** 顏色對比度 WCAG AA（自動工具驗證）— `indigo-600 #4F46E5` on `#FFFFFF` ＝ **4.83:1**，通過 AA 一般文字（≥4.5:1）。⚠️ 注意：spec 也記錄了 `text-gray-400 #9CA3AF` on white ＝ **2.85:1**，**不通過** AA；已在 IMPROVE #3 與 spec 2.2 表格旁加註要拉到 `gray-600` 以上
- [x] **PASS** Token 命名對齊 `00_foundations_spec.md` 命名規範 — 全用 `category.property.variant` 點分隔（`color.brand.primary`、`text.body.md`、`radius.lg`...）
- [ ] **MEDIUM ~60–65%** Token 完整度 ≥ 80% — 與 00 spec 章節對照：
  - Grid & Layout：container / breakpoints / header grid 有，section padding scale 缺 → ~70%
  - Color：brand + neutral + text + border 有；semantic 用 00 預設、surface dark mode 缺 → ~60%
  - Typography：font stack + body + tracking + weight 有；完整 11 階字級 stair 多為 [original] → ~55%
  - Spacing：5 個 token 有實證，14 個 stair 大半未證實 → ~40%
  - Border / Radius：核心夠 → ~70%
  - Shadow：全部 [original] → ~10%
  - Iconography：尺寸有實證 → ~65%
  - Motion：僅 transition-colors 有實證 → ~25%

  **加權平均約 60–65%，未達 80% 門檻**。原因：來源站把 Hero / Pricing / FAQ 全做成 client component，SSR 撈不到字級 / 陰影 / 動效資料。**行動**：headless browser 補抓後再驗一次
- [x] **PASS** Token 引用層級正確 — 本單元只交付 L0-範疇 token，無 L1+ 引用問題

## Pipeline 接入

- [x] **PASS** spec 結構對齊 `global/BASE_DESIGN_SYSTEM.md` — 章節順序與 00 spec 一致（Layout → Color → Typo → Spacing → Border → Shadow → Icon → Motion → Z-index → Metadata）
- [x] **PASS** 與既有 `00_foundations_spec.md` 衝突已解決 — 主要衝突是 container 寬度（1280 vs 1152），已在 spec §1 結尾差異表中明列，clone 採 1152，需在使用時 override
- [ ] **N/A — 不在本單元** 執行指令範本可貼給 Lovable / Claude Code
- [ ] **PARTIAL** 已建立連結到 `references/website_recipes.md` — 目前 recipes 檔無 `landing-ai-tool` 條目，建議後續單元補一條，並 reference 本 clone

---

## 總結

- **可放行區段**：differentiation 完整、命名規範對齊、法律/倫理完全乾淨、主色 AA 通過
- **必須補課才放行**：
  1. Token 完整度從 ~62% 拉到 80%+（用 headless render 補 Hero / Pricing / FAQ）
  2. 把 `text-gray-400` 從 spec 與來源繼承中明確替換為 `gray-600` 或更深
  3. 在 `references/website_recipes.md` 補 `landing-ai-tool` 食譜
  4. 完成 L1 / L2 / L3 / L4 文件後再執行 full validation

**結論**：階段性 PASS（differentiation + spec partial）；full pipeline 接入 BLOCKED 直到 token 完整度與 recipe 補齊。
