# L0 Foundations — shipyouridea

> 對齊 `00_foundations_spec.md` 結構

來源：https://shipyouridea.today/
擷取日期：2026-04-08
擷取方式：`curl -sL -A "Mozilla/5.0" https://shipyouridea.today/`（靜態 HTML）

> **共享代碼庫聲明**
> 與 ideacheck.cc 共用 Next.js codebase。L0 數值實質上完全相同。delta 摘要請參考 _comparison 文件。L0 範圍內唯一可觀察到的 delta：favicon 尺寸（64x64 vs 48x48）— 並非 token 層級的差異。

注意：Hero / Demo / Pricing / FAQ 內層文案為 client-rendered，本文件僅基於初始 HTML 中可觀察到的 token。

---

## 1. Grid & Layout System

| 屬性 | 值 |
|------|-----|
| Container max-width | `max-w-6xl` = 72rem = **1152px** |
| Mobile breakpoint | Tailwind `sm` = 640px |
| Tablet breakpoint | Tailwind `md` = 768px |
| Desktop breakpoint | Tailwind `lg` = 1024px |

## 2. Color System

### Brand
| Token | Value | 用途 |
|-------|-------|------|
| color.brand.primary | `#4f46e5` (Tailwind indigo-600) | 主要 CTA：登入按鈕 `bg-indigo-600 hover:bg-indigo-700` |
| color.brand.secondary | TBD | 靜態 HTML 未觀察到 |

### Neutral
| Token | Value |
|-------|-------|
| color.neutral.900 | `#030712` (Tailwind `text-gray-950`) |
| color.neutral.700 | TBD |
| color.neutral.500 | `#6b7280` (Tailwind `text-gray-500`) |
| color.neutral.400 | `#9ca3af` (Tailwind `text-gray-400`) |
| color.neutral.300 | TBD |
| color.neutral.100 | TBD |

### Surface
| Token | Value | 備註 |
|-------|-------|------|
| color.background | CSS var `bg-background` | 未渲染 CSS 無法解析 — TBD (low) |

### Semantic
| Token | Value |
|-------|-------|
| color.success | TBD |
| color.warning | TBD |
| color.error | TBD |
| color.info | TBD |

## 3. Typography System

- **Font Family**: Inter
- **Font 檔案**: `/_next/static/media/83afe278b6a6bb3c-s.p.0q-301v4kxxnr.woff2`
- **與 ideacheck 比對**: hash **完全相同**，確認共用同一字型 bundle。

| Token | Family | Size (Tailwind) | Weight | 備註 |
|-------|--------|------|--------|-------------|
| display | Inter | `text-4xl` | `font-bold` | 觀察到 |
| h1 | Inter | TBD | TBD | client-rendered |
| h2 | Inter | TBD | TBD | client-rendered |
| body | Inter | `text-base` | `font-medium` | 觀察到 |
| caption | Inter | `text-sm` | TBD | 觀察到 |

## 4. Spacing System

Base unit: **4px**（Tailwind 預設）

| Token | Value | Tailwind class |
|-------|-------|-------|
| space.xs | 8px | `gap-2` |
| space.sm | 16px | `gap-4` / `px-4` |
| space.md | 24px | `gap-6` / `px-6` |
| space.lg | 32px | `gap-8` |
| space.padY.sm | 12px | `py-3` |
| space.padY.lg | 40px | `py-10` |

## 5. Border & Radius System

| Token | Value | 來源 |
|-------|-------|-------|
| radius.sm | TBD | |
| radius.md | TBD | |
| radius.lg | **8px** (`rounded-lg`) | 主 CTA 按鈕 |
| radius.full | 9999px | 預設 |

## 6. Elevation & Shadow System

| Token | Value |
|-------|-------|
| shadow.sm | TBD（靜態 HTML 未觀察到） |
| shadow.md | TBD |
| shadow.lg | TBD |

## 7. Iconography

- **元件**: `IconMark`、`LanguageSwitcher`
- **風格**: TBD（client-rendered，需後續 L1 確認）
- **標準尺寸**: TBD

## 8. Motion & Animation

- **Transition**: `transition-colors`（hover 狀態）
- **Duration**: TBD
- **Easing**: TBD

---

## 來源信心度

| 章節 | 信心度 | 為什麼 |
|------|--------|--------|
| Grid | HIGH | `max-w-6xl` 直接出現於 HTML class；breakpoints 為 Tailwind 預設 |
| Color | MEDIUM | Brand primary 與 neutral text 來自 class 名稱可解析；`bg-background` CSS var 未解析 |
| Typography | HIGH | Font 檔案 hash 與 ideacheck 比對完全相同 |
| Spacing | HIGH | 多個 Tailwind spacing class 直接觀察 |
| Radius | MEDIUM | 僅按鈕 `rounded-lg` 可確認 |
| Shadow | LOW | 靜態 HTML 無觀察 |
| Icons | LOW | 元件名稱可見但 SVG client-rendered |
| Motion | LOW | 僅 `transition-colors` 可見 |
