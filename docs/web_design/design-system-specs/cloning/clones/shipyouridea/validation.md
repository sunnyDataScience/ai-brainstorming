# Validation — shipyouridea

> 來源：https://shipyouridea.today/
> 日期：2026-04-08
> 受審 spec：`clones/shipyouridea/spec/inspired-design-system.md` + `differentiation.md`
> 參考：`checklists/validation_checklist.md`

---

## 法律與倫理

| # | 項目 | 結果 | 證據 |
|---|------|------|------|
| 1 | 無複製商標 / logo / 品牌名 | ✅ PASS | spec 與 differentiation 中 `ShipYourIdea` 僅作為來源引用，OVERRIDE 表已標記替換 logo / brand name |
| 2 | 無複製文案內容 | ✅ PASS | 所有 hero / demo / pricing / FAQ 內文均標記 TBD，無原文 |
| 3 | 無複製圖片 / 插畫資產 | ✅ PASS | clones/shipyouridea/ 下未存任何來源圖片；OG image 標 OVERRIDE |
| 4 | 來源網站已標註於 spec 開頭 | ✅ PASS | `inspired-design-system.md` 第 3 行 `Source: https://shipyouridea.today/` |

## 差異化驗證

| # | 項目 | 結果 | 證據 |
|---|------|------|------|
| 5 | differentiation.md 四章節齊全（KEEP / DROP / OVERRIDE / IMPROVE） | ✅ PASS | `grep -c "^##" differentiation.md` 顯示 ≥ 4 個 H2 區塊，含全部四類 |
| 6 | IMPROVE 至少 3 條 | ✅ PASS | 共列 5 條：robots meta、SSR、a11y skip-link、JSON-LD、performance |
| 7 | OVERRIDE 至少包含主色與字型 | ✅ PASS | OVERRIDE 表含 `color.brand.primary`, `color.brand.primary.hover`, `font.family.heading` |
| 8 | DROP 項目已從 spec 移除 | ✅ PASS | `inspired-design-system.md` 中無 `ShipYourIdea`、無 `.today` TLD、無 scoring product token |
| 9 | 站點獨特觀察已記錄 | ✅ PASS | differentiation.md「站點觀察」段落明示 lite vs full 變體決策 |

## 技術品質

| # | 項目 | 結果 | 證據 |
|---|------|------|------|
| 10 | 顏色對比度 WCAG AA（indigo-600 on white） | ✅ PASS | 4.83:1 ≥ 4.5:1（normal text） |
| 11 | Token 命名對齊 `00_foundations_spec.md` 規範 | ✅ PASS | 採 `category.subcategory.variant.state` 點分式（spec §9） |
| 12 | Token 完整度 ≥ 80% vs 00_foundations_spec.md | ⚠️ MEDIUM (~65%) | 涵蓋 grid/color/typography/spacing/radius/shadow/icon/motion 八章；但 brand.secondary、brand.accent、semantic（success/warning/error/info 細階）、dark mode 缺；估算覆蓋約 60–70% |
| 13 | 所有 token 引用層級正確 | ✅ PASS | spec 為 L0 only，無跨層引用錯誤 |

## Pipeline 接入

| # | 項目 | 結果 | 證據 |
|---|------|------|------|
| 14 | spec 結構對齊 `global/BASE_DESIGN_SYSTEM.md` | ✅ PASS | 八章節順序與命名對應 BASE_DESIGN_SYSTEM 結構 |
| 15 | 與既有 `00_foundations_spec.md` 衝突已解決 | ✅ PASS | 品牌色 indigo-600 為「受啟發」baseline，已在 OVERRIDE 表標記必須由實作專案替換為自身品牌色，避免直接污染 base spec |
| 16 | Sitemap 對應到 `WEBSITE_MODULE_MATRIX.md` | ⚠️ DEFER | shipyouridea 為「Tier 1 純展示型 / Lean Landing」原型，對應 matrix 中的 landing/marketing 類別；正式對應需在 `clones/shipyouridea/analysis/L4_sitemap.md` 補上 module 編號 |

---

## 總結

| 類別 | PASS | WARN | FAIL |
|------|------|------|------|
| 法律與倫理 | 4 | 0 | 0 |
| 差異化 | 5 | 0 | 0 |
| 技術品質 | 3 | 1 | 0 |
| Pipeline 接入 | 2 | 1 | 0 |
| **合計** | **14** | **2** | **0** |

**結論**：可進入 Pipeline 試接，但需在合入前處理：
1. 補完 brand.secondary / accent / semantic 細階以衝高 token 完整度至 ≥ 80%
2. 補上 dark mode tokens
3. 在 `analysis/L4_sitemap.md` 加 `WEBSITE_MODULE_MATRIX.md` 對應編號

無 CRITICAL fail，可同步推進 L1/L2 spec。
