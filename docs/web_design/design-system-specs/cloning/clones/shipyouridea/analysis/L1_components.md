# L1 Components — shipyouridea

> 來源：https://shipyouridea.today/ 的 static HTML / RSC payload（擷取於 2026-04-08）
> 對齊 `templates/L1_components_template.md`

> **頂部註記**：本站與 `ideacheck.cc` 共用 Next.js codebase。與 ideacheck
> 在元件層級的主要 delta：
> 1. Logo 尺寸為 **36 / 32**（nav / footer），相對於 ideacheck 的 **28 / 24** — logo 刻意放大。
> 2. **無 `DataSources` 元件** — 整個 data-sources section 在 RSC tree 中都不存在。
> 3. Footer 只有 **5 個連結**，相對於 ideacheck 的 7 個（缺少「服務」與「數據來源」）。
>
> 其餘的 primitives（Button、Nav shell、Footer chrome、NavLink）因為來自同一份共用 codebase，
> 在兩個站點之間是 byte-identical。所有在 static RSC payload 中可見的元件信心度皆為
> HIGH；Hero / InteractiveDemo / Pricing / FAQ 的 client-rendered 內部內容則標為 TBD。

---

## Button (Primary)

### 變體
| Variant | 背景 | 文字 | Border | 用途 |
|---------|------|------|--------|------|
| primary | `bg-indigo-600` → hover `bg-indigo-700` | `text-white` | none | nav、hero、pricing 的 CTA |
| secondary | TBD（client-rendered） | TBD | TBD | TBD |
| ghost | TBD | TBD | TBD | TBD |

### Tailwind classes（觀察值）
```
inline-flex h-8 items-center rounded-lg bg-indigo-600 px-4
text-sm font-medium text-white transition hover:bg-indigo-700
```

### 尺寸
| Size | Padding | Font Size | Height |
|------|---------|-----------|--------|
| sm（static HTML 中觀察到的唯一尺寸） | `px-4` | `text-sm` | `h-8` (32px) |

### 狀態
- default：`bg-indigo-600`
- hover：`bg-indigo-700`
- transition：`transition`（Tailwind 預設 ~150ms）
- active / disabled / loading：static HTML 未觀察到 — TBD

### Token 引用（proposed）
- background：`color.brand.primary`（= indigo-600）
- background-hover：`color.brand.primary-hover`（= indigo-700）
- radius：`radius.lg`（= 0.5rem）
- height：`size.control.sm`（= 2rem）

### 與 ideacheck 的差異
Class string 完全一致。無 drift。

**信心度：HIGH** — 直接來自 RSC payload。

---

## Nav（Top / Sticky Header）

### Tailwind classes（觀察值）
Outer wrapper：
```
sticky top-0 z-50 w-full border-b border-gray-950/5
bg-white/80 backdrop-blur-md
```

Inner grid：
```
mx-auto grid max-w-6xl grid-cols-3 items-center px-6 py-3
```

### 結構
3 欄 grid：
1. 左 — Logo + 品牌 wordmark（`/logo-v2.png` 36x36）
2. 中 — 主要 nav 連結（NavLink，見下）
3. 右 — LanguageSwitcher + 主要 CTA Button

### 狀態
- default：`bg-white/80` 半透明 + backdrop blur
- scrolled：視覺上完全相同（sticky，未觀察到 scroll-state class）

### Token 引用
- background：`color.surface.translucent`（= white/80）
- border-bottom：`color.border.subtle`（= gray-950/5）
- z-index：`z.sticky`（= 50）

### 與 ideacheck 的差異
Class string 完全一致。唯一差異是左側 cell 內部的 logo 尺寸（36 vs 28）。

**信心度：HIGH**

---

## Footer

### Tailwind classes（觀察值）
Outer：
```
border-t border-gray-950/5 px-6 py-10
```

Inner row：
```
mx-auto flex max-w-6xl flex-col items-center justify-between
gap-4 sm:flex-row
```

### 結構
- 品牌區塊（左）：`/logo-v2.png` 32x32 + wordmark
- 連結清單（右）：5 個 footer 連結 — 價格 / FAQ / 聯絡我們 / 隱私權政策 / 服務條款

### 狀態
靜態，除了 per-link hover（見 Nav Link / Footer 變體）之外無互動狀態。

### Token 引用
- border-top：`color.border.subtle`
- spacing-y：`space.10`（= 2.5rem）

### 與 ideacheck 的差異
- Logo 32 vs ideacheck 的 24。
- 5 個連結 vs ideacheck 的 7 個 — **缺少**：服務、數據來源。
- Outer + inner 的 class string：完全一致。

**信心度：HIGH**

---

## Nav Link

觀察到兩種視覺變體（header vs footer）。

### Header 變體
```
text-sm font-medium text-gray-500
transition-colors hover:text-gray-950
```
- default：`text-gray-500`
- hover：`text-gray-950`
- weight：`font-medium`

### Footer 變體
```
text-sm text-gray-400
transition-colors hover:text-gray-600
```
- default：`text-gray-400`
- hover：`text-gray-600`
- weight：regular

### Token 引用
- header default：`color.text.muted`（gray-500）
- header hover：`color.text.strong`（gray-950）
- footer default：`color.text.subtle`（gray-400）
- footer hover：`color.text.muted`（gray-600）

### 與 ideacheck 的差異
完全一致。

**信心度：HIGH**

---

## Logo

### 資產
- 來源：`/logo-v2.png`
- Nav：36 x 36 px（Next.js `<Image width={36} height={36}>`）
- Footer：32 x 32 px

### 與 ideacheck 的差異
ideacheck 使用 28 / 24。shipyouridea 刻意放大（nav 約 +28%，footer 約 +33%）。
檔名相同；僅渲染尺寸不同。**不得複製** binary 資產 — clone 必須以自家品牌
標記替換。

**信心度：HIGH** — 透過 live RSC payload 中的 `width\":36` / `width\":32` grep 驗證。

---

## LanguageSwitcher

存在於 nav 右側 cell 的 RSC component registry 中。內部 markup 為
client-rendered（mount 後 hydrate），因此 option list、current-locale 樣式、
以及 dropdown chrome 在 L2 以 headless browser 或 DevTools snapshot 擷取前皆為 **TBD**。

### 已知事項
- 位置：nav 右側 cell，位於主要 CTA button 之前
- Payload 中的元件名稱：`LanguageSwitcher`
- Server-rendered placeholder 為空（無 class string 可取）

### 與 ideacheck 的差異
相同元件名稱、相同 nav slot。行為差異 TBD。

**信心度：MEDIUM**（存在性 HIGH，樣式 LOW）

---

## Hero / InteractiveDemo / Pricing / FAQ / IconMark

這些元件註冊於 RSC（其元件名稱出現在 payload manifest 中），但其
渲染 markup 是在 client 產生。static HTML 回應只包含 React Server Component shell
— 沒有 class strings、沒有文案、沒有 media URL。

| Component | Slot | Static class 證據 | 備註 |
|-----------|------|------------------------|-------|
| Hero | `<main>` 頂部 | 無 | 可能是 H1 + sub + CTA 堆疊 — TBD |
| InteractiveDemo | Hero 下方 | 無 | 互動 widget，完全 client-rendered |
| Pricing | 頁面中段 | 無 | 方案卡片 — TBD |
| FAQ | Pricing 下方 | 無 | Disclosure list — TBD |
| IconMark | inline（icons） | 無 | 可能是 Hero / Pricing 使用的 SVG primitive |

### 與 ideacheck 的關鍵結構差異
**`DataSources` 元件在 shipyouridea 的 RSC tree 中不存在**。ideacheck 有
一個專門列出資料提供者的 section；shipyouridea 完全捨棄。這是兩站之間
page-structure 最大的單一差異。

**信心度：LOW** 為內部樣式，**HIGH** 為 registry 層級的存在/不存在。

---

## 必抽元件清單（status）

- [x] Button（僅 primary — secondary/ghost TBD）
- [ ] Input / TextArea / Select — static HTML 中不存在
- [ ] Card — static HTML 中不存在（可能在 Pricing 內部，TBD）
- [ ] Badge / Tag — TBD
- [ ] Avatar — 未使用
- [ ] Modal / Dialog — TBD（可能在 InteractiveDemo 內部）
- [ ] Tooltip — TBD
- [ ] Tabs — TBD
- [ ] Dropdown / Menu — 部分（LanguageSwitcher 暗示有一個）
- [ ] Toast / Alert — TBD
- [ ] Pagination — 未使用
- [ ] Breadcrumb — 未使用
- [x] Nav（top）
- [x] Footer
- [x] Nav Link
- [x] Logo
- [x] LanguageSwitcher（僅存在性）

---

## 元件信心度

| 元件 | 信心度 | 來源 |
|------|--------|------|
| Button (primary) | HIGH | RSC payload class string |
| Nav (top) | HIGH | RSC payload class string |
| Footer | HIGH | RSC payload class string |
| Nav Link (header) | HIGH | RSC payload class string |
| Nav Link (footer) | HIGH | RSC payload class string |
| Logo (sizing) | HIGH | RSC `width\":36` / `width\":32` |
| LanguageSwitcher | MEDIUM | 僅 registry 中的元件名稱；內部 TBD |
| Hero | LOW | 僅 registry |
| InteractiveDemo | LOW | 僅 registry |
| Pricing | LOW | 僅 registry |
| FAQ | LOW | 僅 registry |
| IconMark | LOW | 僅 registry |
| DataSources | N/A | **不存在**（與 ideacheck 的差異） |

---

## 跨站差異總表（shipyouridea vs ideacheck）

| 面向 | ideacheck | shipyouridea | 備註 |
|--------|-----------|--------------|-------|
| Logo nav 尺寸 | 28 px | **36 px** | +28% |
| Logo footer 尺寸 | 24 px | **32 px** | +33% |
| Footer 連結 | 7（價格 / FAQ / 服務 / 數據來源 / 聯絡我們 / 隱私權政策 / 服務條款） | **5**（價格 / FAQ / 聯絡我們 / 隱私權政策 / 服務條款） | 移除 服務、數據來源 |
| `DataSources` 元件 | 有 | **無** | 結構差異 |
| Button primary class | 完全一致 | 完全一致 | 共用 codebase |
| Nav / Footer chrome | 完全一致 | 完全一致 | 共用 codebase |
| NavLink 色彩 | 完全一致 | 完全一致 | 共用 codebase |
