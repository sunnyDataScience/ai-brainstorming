# Inspired Design System — shipyouridea

> Source: https://shipyouridea.today/ （shared codebase with ideacheck.cc，lite 變體）
> Aligned to: `docs/web_design/design-system-specs/00_foundations_spec.md`
> Tag convention: `[inspired by: shipyouridea.today]` = 來源觀察值；`[original]` = 自己決定 / Tailwind 預設補洞

---

## 1. Grid & Layout

| Token | Value | 來源 |
|-------|-------|------|
| `layout.container.max-width` | 1152px (`max-w-6xl`) | [inspired by: shipyouridea.today] |
| `layout.container.padding` | 16px / 24px / 32px | [inspired by: shipyouridea.today] (Tailwind `px-4 md:px-6 lg:px-8`) |
| `layout.container.center` | `mx-auto` | [inspired by: shipyouridea.today] |
| `breakpoint.sm` | 640px | [inspired by: shipyouridea.today] (Tailwind default) |
| `breakpoint.md` | 768px | [inspired by: shipyouridea.today] |
| `breakpoint.lg` | 1024px | [inspired by: shipyouridea.today] |
| `breakpoint.xl` | 1280px | [original] (Tailwind default) |
| `breakpoint.2xl` | 1536px | [original] (Tailwind default) |
| `layout.section.py` | 64px desktop / 48px mobile | [original]（lite 版未明示，採 Tailwind `py-16 md:py-24`） |
| `layout.grid.columns` | 12 (desktop) / 4 (mobile) | [original] |

---

## 2. Color

### 2.1 Brand
| Token | Value | 來源 |
|-------|-------|------|
| `color.brand.primary` | `#4f46e5` (indigo-600) | [inspired by: shipyouridea.today] |
| `color.brand.primary.hover` | `#4338ca` (indigo-700) | [inspired by: shipyouridea.today] |
| `color.brand.primary.active` | `#3730a3` (indigo-800) | [original]（推測 `active:` 加深一階） |
| `color.brand.secondary` | TBD | [original]（lite 版未觀察到） |
| `color.brand.accent` | TBD | [original] |

### 2.2 Neutral / Text
| Token | Value | 來源 |
|-------|-------|------|
| `color.text.primary` | `#030712` (gray-950) | [inspired by: shipyouridea.today] |
| `color.text.secondary` | `#6b7280` (gray-500) | [inspired by: shipyouridea.today] |
| `color.text.muted` | `#9ca3af` (gray-400) | [inspired by: shipyouridea.today] (footer) |
| `color.border.subtle` | `rgba(0,0,0,0.05)` (`border-gray-950/5`) | [inspired by: shipyouridea.today] |
| `color.background` | `#ffffff` | [inspired by: shipyouridea.today] |

### 2.3 Semantic
| Token | Value | 來源 |
|-------|-------|------|
| `color.success` | `#22c55e` | [original] (Tailwind green-500) |
| `color.warning` | `#eab308` | [original] (Tailwind yellow-500) |
| `color.error` | `#ef4444` | [original] (Tailwind red-500) |
| `color.info` | `#3b82f6` | [original] (Tailwind blue-500) |

> WCAG AA 對比：indigo-600 on white = **4.83:1** ✅ PASS

---

## 3. Typography

| Token | Value | 來源 |
|-------|-------|------|
| `font.family.sans` | `Inter, system-ui, sans-serif` | [inspired by: shipyouridea.today] (`/_next/static/media/...Inter...woff2`) |
| `font.family.heading` | `Inter` | [inspired by: shipyouridea.today] |
| `font.family.mono` | `ui-monospace, SFMono-Regular, monospace` | [original] |
| `font.size.display` | 48px / 60px (mobile / desktop) | [original] (lean landing 慣例 `text-5xl md:text-6xl`) |
| `font.size.h1` | 36px / 48px | [original] |
| `font.size.h2` | 30px / 36px | [original] |
| `font.size.body` | 16px | [original] (Tailwind `text-base`) |
| `font.size.small` | 14px | [original] |
| `font.weight.regular` | 400 | [original] |
| `font.weight.medium` | 500 | [original] |
| `font.weight.semibold` | 600 | [original] |
| `font.weight.bold` | 700 | [original] |
| `font.lineheight.tight` | 1.15 | [original] |
| `font.lineheight.normal` | 1.5 | [original] |

---

## 4. Spacing

| Token | Value | 來源 |
|-------|-------|------|
| `space.0` | 0 | [original] |
| `space.1` | 4px | [original] (Tailwind scale) |
| `space.2` | 8px | [original] |
| `space.3` | 12px | [original] |
| `space.4` | 16px | [original] |
| `space.6` | 24px | [original] |
| `space.8` | 32px | [original] |
| `space.12` | 48px | [original] |
| `space.16` | 64px | [original] |
| `space.24` | 96px | [original] |

> 完整 scale 採 Tailwind 預設（4px base）— [original]

---

## 5. Border & Radius

| Token | Value | 來源 |
|-------|-------|------|
| `radius.sm` | 4px | [original] |
| `radius.md` | 6px | [original] |
| `radius.lg` | 8px | [inspired by: shipyouridea.today]（CTA 按鈕觀察為 `rounded-lg`） |
| `radius.xl` | 12px | [original] |
| `radius.full` | 9999px | [original] |
| `border.width.1` | 1px | [original] |
| `border.color.subtle` | `rgba(0,0,0,0.05)` | [inspired by: shipyouridea.today] |

---

## 6. Elevation / Shadow

| Token | Value | 來源 |
|-------|-------|------|
| `shadow.sm` | `0 1px 2px 0 rgb(0 0 0 / 0.05)` | [original] (Tailwind `shadow-sm`) |
| `shadow.md` | `0 4px 6px -1px rgb(0 0 0 / 0.1)` | [original] |
| `shadow.lg` | `0 10px 15px -3px rgb(0 0 0 / 0.1)` | [original] |
| `shadow.nav.backdrop` | `backdrop-filter: blur(8px)` + `bg-white/80` | [inspired by: shipyouridea.today] (sticky nav) |

---

## 7. Iconography

| Token | Value | 來源 |
|-------|-------|------|
| `icon.set` | Lucide / Heroicons | [original]（lite 版圖示量少，未明確觀察） |
| `icon.size.sm` | 16px | [original] |
| `icon.size.md` | 20px | [original] |
| `icon.size.lg` | 24px | [original] |
| `icon.stroke-width` | 1.5 | [original] |

---

## 8. Motion

| Token | Value | 來源 |
|-------|-------|------|
| `motion.duration.fast` | 150ms | [original] |
| `motion.duration.base` | 200ms | [original] |
| `motion.duration.slow` | 300ms | [original] |
| `motion.easing.standard` | `cubic-bezier(0.4, 0, 0.2, 1)` | [original] (Tailwind `ease-in-out`) |
| `motion.scroll.smooth` | `scroll-behavior: smooth` | [inspired by: shipyouridea.today]（anchor nav 平滑捲動） |

---

## 9. Token 命名規範

採 `category.subcategory.variant.state` 點分式 — 對齊 `00_foundations_spec.md` §9。

範例：
- `color.brand.primary.hover`
- `font.size.h1`
- `space.4`

---

## 10. Token Mode

| Mode | 狀態 |
|------|------|
| Light | [inspired by: shipyouridea.today]（來源為 light-only） |
| Dark | [original]（建議補上，lite 版未提供） |

---

## 註記

- TBD 標記之處皆因 lite 版為 client-rendered，靜態 HTML 無法觀察；接入 Pipeline 前需以 rendered DOM 補齊。
- 本 spec 為「受啟發」版本，所有商標 / 文案 / 圖片資產一律不抄。
