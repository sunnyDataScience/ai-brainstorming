# L0 Foundations — ideacheck

> 對齊 `00_foundations_spec.md` 結構

來源：https://ideacheck.cc/
擷取日期：2026-04-08

> **Note**: Site shares codebase with shipyouridea.today — L0 values identical except where documented.

---

## 1. Grid & Layout System

| 屬性 | 值 |
|------|-----|
| Container max-width | 1152px (`max-w-6xl` = 72rem) |
| Mobile breakpoint | 640px (Tailwind `sm:`) |
| Tablet breakpoint | 768px (Tailwind `md:`) |
| Desktop breakpoint | 1024px (Tailwind `lg:`) |

來源：靜態 HTML 中觀察到 `max-w-6xl` 用於主要 container；breakpoints 為 Tailwind 預設值（HTML 中可見 `md:` / `lg:` prefixes）。

## 2. Color System

### Brand
| Token | Value | 用途 |
|-------|-------|------|
| color.brand.primary | `#4f46e5` (indigo-600) | 主要 CTA / Login button bg |
| color.brand.primary.hover | `#4338ca` (indigo-700) | hover 狀態 |
| color.brand.secondary | TBD | 未在靜態 HTML 觀察到 |

### Neutral
| Token | Value | Tailwind |
|-------|-------|----------|
| color.neutral.950 | `#030712` | `text-gray-950` (主要文字) |
| color.neutral.900 | `#111827` | `text-gray-900` |
| color.neutral.500 | `#6b7280` | `text-gray-500` (次要文字) |
| color.neutral.400 | `#9ca3af` | `text-gray-400` (footer) |
| color.border.subtle | `rgba(0,0,0,0.05)` | `border-gray-950/5` |

### Background
| Token | Value |
|-------|-------|
| color.background | CSS var `bg-background` (TBD — 需 rendered CSS 才能解析) |

### Semantic
| Token | Value |
|-------|-------|
| color.success | TBD |
| color.warning | TBD |
| color.error | TBD |
| color.info | TBD |

## 3. Typography System

字體家族：**Inter**（觀察自 `/_next/static/media/83afe278b6a6bb3c-s.p.woff2` font 引用）

| Token | Family | Size | Weight | Line-height |
|-------|--------|------|--------|-------------|
| display | Inter | TBD (client-rendered) | TBD | TBD |
| h1 (404) | Inter | 36px (`text-4xl`) | bold | TBD |
| h2 | Inter | TBD | TBD | TBD |
| body | Inter | 16px (`text-base`) | normal/medium | TBD |
| caption | Inter | 14px (`text-sm`) | normal | TBD |

觀察到的 weight class：`font-bold`、`font-medium`。

## 4. Spacing System

Base unit: **4px** (Tailwind 預設 scale)

| Token | Value | 觀察到的 class |
|-------|-------|---------------|
| space.xs | 8px | `gap-2`, `py-2` |
| space.sm | 16px | `gap-4`, `px-4` |
| space.md | 24px | `gap-6`, `px-6` |
| space.lg | 32px | `gap-8` |
| space.xl | 40px | `py-10` |
| space.btn-y | 12px | `py-3` (button vertical padding) |

## 5. Border & Radius System

| Token | Value | 來源 |
|-------|-------|------|
| radius.sm | TBD | 未在靜態 HTML 觀察到 |
| radius.md | TBD | |
| radius.lg | 8px (`rounded-lg`) | 主要 button (Login) |
| radius.full | 9999px | Tailwind 預設 |

Border：`border-gray-950/5`（黑色 5% 透明度）用於分隔線。

## 6. Elevation & Shadow System

| Token | Value |
|-------|-------|
| shadow.sm | TBD |
| shadow.md | TBD |
| shadow.lg | TBD |

靜態 HTML 中未觀察到 shadow utility class。Hero/CTA 區的 elevation 需在 L1 或 rendered DOM 階段補上。

## 7. Iconography

- 風格：TBD（需 rendered SVG）
- 標準尺寸：TBD
- 觀察到元件：`IconMark` component（Next.js client component reference）、`LanguageSwitcher`
- Logo / brand mark 透過 `IconMark` 渲染，靜態 HTML 不含 inline SVG

## 8. Motion & Animation

- Duration：TBD（class 中見 `transition` / `transition-colors`，未指定 duration → 預設 150ms）
- Easing：TBD（Tailwind 預設 `ease-in-out` 1.0,0,0.2,1）
- 觀察到的 transition：button hover 顏色變化（`hover:bg-indigo-700` 配合 `transition-colors`）

---

## 來源信心度

| 章節 | 信心度 | 為什麼 |
|------|--------|--------|
| Grid | HIGH (max-w-6xl) / MEDIUM (breakpoints) | container 直接觀察；breakpoints 為 Tailwind 預設推論 |
| Color | HIGH (brand/neutral) / LOW (background var, semantic) | 主色與灰階直接從 class name 解析；背景為 CSS variable，semantic 未出現 |
| Typography | MEDIUM | 字體家族 HIGH（font 檔名確認）；heading sizes 多為 client-rendered，僅 404 頁可觀察 |
| Spacing | HIGH | Tailwind scale 為標準，class names 直接觀察 |
| Radius | MEDIUM | 僅觀察到 `rounded-lg`，其他 size TBD |
| Shadow | LOW | 靜態 HTML 無 shadow class |
| Icons | LOW | 元件為 client-only，無法解析 SVG 細節 |
| Motion | LOW | 僅觀察到 transition class，未指定 duration |
