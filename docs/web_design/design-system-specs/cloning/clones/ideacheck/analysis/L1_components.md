# L1 Components — ideacheck

> 來源：`https://ideacheck.cc/` 的 static HTML / RSC payload
> 方法：僅觀察 server-rendered markup（無 DOM/CSSOM）
> 日期：2026-04-08

> **註記**：ideacheck.cc 與 shipyouridea.today 共用同一份 Next.js codebase。
> 元件幾乎完全相同；logo 尺寸差異請參考 `_comparison` 文件
> （ideacheck 使用 28px/24px logo；nav 連結包含「服務」與「數據來源」）。

---

## Button / Primary (Login)

位於 header 右上角的 CTA。唯一觀察到的實例導向 `/login`。

### Tailwind classes（原樣）

```
inline-flex h-8 items-center rounded-lg bg-indigo-600 px-4 text-sm font-medium text-white transition hover:bg-indigo-700
```

### Token 拆解

| Property | Value |
|---|---|
| display | inline-flex |
| height | 2rem (32px) |
| radius | 0.5rem (rounded-lg) |
| bg (default) | indigo-600 |
| bg (hover) | indigo-700 |
| px | 1rem |
| font-size | 0.875rem (text-sm) |
| font-weight | 500 (font-medium) |
| color | white |
| transition | all (transition) |

### 觀察到的狀態
- default
- hover（由 class 驅動）

### 觀察到的變體
- 僅 primary（static HTML 中無 secondary/ghost）

### 信心度
**HIGH** — class string 與 DOM 位置皆可在 RSC payload 中觀察到。

---

## Nav / Top

Sticky header，包含 logo（左）、nav 連結（中）、登入按鈕 + LanguageSwitcher（右）。

### Tailwind classes（原樣）

Outer：
```
sticky top-0 z-50 w-full border-b border-gray-950/5 bg-white/80 backdrop-blur-md
```

Inner grid：
```
mx-auto grid max-w-6xl grid-cols-3 items-center px-6 py-3
```

Center link cluster：
```
hidden sm:flex gap-8
```

### 結構

| Slot | 內容 |
|---|---|
| left | Logo (28x28) + 品牌文字 |
| center | Nav 連結（< sm 時隱藏） |
| right | 登入按鈕 + LanguageSwitcher |

### 狀態
- default（HTML 中無可觀察的 scroll/hover 變體）

### 信心度
**HIGH** — 完整 class strings 與 slot 結構皆可在 RSC payload 中觀察到。

---

## Footer

### Tailwind classes（原樣）

Outer：
```
border-t border-gray-950/5 px-6 py-10
```

Inner row：
```
mx-auto flex max-w-6xl flex-col items-center justify-between gap-4 sm:flex-row
```

### 內容

- 品牌群組：Logo (24x24) + 品牌文字（`text-sm font-bold`）
- Nav 連結（7 項，依觀察順序）：
  1. 服務
  2. 數據來源
  3. 價格
  4. FAQ
  5. 聯絡我們
  6. 隱私權政策
  7. 服務條款

### 狀態
- default

### 信心度
**HIGH** — class strings 與 7 個連結標籤皆可在 static HTML 中觀察到。

---

## Nav Link

兩種使用情境：header 與 footer。兩者皆為 anchor 元素。

### Tailwind classes（原樣）

Header 變體：
```
text-sm font-medium text-gray-500 transition-colors hover:text-gray-950
```

Footer 變體：
```
text-sm text-gray-400 transition-colors hover:text-gray-600
```

### 變體
- header（medium weight，gray-500 → gray-950）
- footer（regular weight，gray-400 → gray-600）

### 狀態
- default
- hover（由 class 驅動）

### 信心度
**HIGH**

---

## Logo

圖片資產於 nav 與 footer 重複使用。

### 來源

`/logo-v2.png`

### 變體

| 情境 | Width × Height | 標籤 class |
|---|---|---|
| Nav | 28 × 28 | `text-base font-bold` |
| Footer | 24 × 24 | `text-sm font-bold` |

### 註記
- 品牌資產 — clone 實作中**不得**複製。
- 與 shipyouridea.today 的尺寸差異記錄於 `_comparison` 文件。

### 信心度
**HIGH**

---

## LanguageSwitcher

於 RSC payload 中被引用的 client component（位於 header 右側 slot）。
內部 markup 於 client-side 進行 hydrate。

### 可觀察項目
- `Nav / Top` 右側 grid cell 中的掛載點存在。

### 不可觀察項目
- Trigger button 的 class strings
- Dropdown panel 的結構
- Locale 清單

### 信心度
**LOW** — 僅可確認存在；結構未出現在 static HTML 中。

---

## Hero / InteractiveDemo / DataSources / Pricing / FAQ / IconMark

這些元件 identifier 出現在 RSC component registry 中，但以 client-side
或 client islands 形式渲染。Static HTML 不暴露其內部結構。

| Component | Static HTML 證據 | 信心度 |
|---|---|---|
| Hero | 僅 payload 中有 identifier | LOW |
| InteractiveDemo | 僅 payload 中有 identifier | LOW |
| DataSources | 僅 payload 中有 identifier | LOW |
| Pricing | 僅 payload 中有 identifier | LOW |
| FAQ | 僅 payload 中有 identifier | LOW |
| IconMark | 僅 payload 中有 identifier | LOW |

> **狀態**：client-rendered — 結構無法於 static HTML 中觀察。
> 需 DOM-level capture（Playwright / browser snapshot）才能展開 L1。

---

## 元件信心度總表

| 元件 | 信心度 | 來源 |
|---|---|---|
| Button / Primary | HIGH | RSC payload class string |
| Nav / Top | HIGH | RSC payload 結構 + classes |
| Footer | HIGH | RSC payload 結構 + classes |
| Nav Link (header) | HIGH | RSC payload class string |
| Nav Link (footer) | HIGH | RSC payload class string |
| Logo | HIGH | `<img>` src + 尺寸 |
| LanguageSwitcher | LOW | 僅有掛載點 |
| Hero | LOW | registry identifier |
| InteractiveDemo | LOW | registry identifier |
| DataSources | LOW | registry identifier |
| Pricing | LOW | registry identifier |
| FAQ | LOW | registry identifier |
| IconMark | LOW | registry identifier |

---

## 跨站註記

ideacheck.cc 與 shipyouridea.today 共用同一份 Next.js codebase。
上述記錄的元件與姊妹站**幾乎完全相同**；有意義的差異為：

- Logo 尺寸（此處 28/24，姊妹站為其他值 — 詳見 `_comparison`）
- Nav 連結標籤包含「服務」與「數據來源」

完整的 delta matrix 請參考 `clones/_comparison/`（待撰寫）。
