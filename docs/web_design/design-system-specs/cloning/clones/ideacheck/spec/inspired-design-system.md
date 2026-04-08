# Inspired Design System — ideacheck

> **Source**：https://ideacheck.cc/（擷取於 2026-04-08）
> **對齊**：`docs/web_design/design-system-specs/00_foundations_spec.md`
> **註記**：每個 token 標明 `[inspired by: ideacheck.cc]`（來自實際 SSR 觀察）或 `[original]`（無證據，依 Tailwind 預設與 00 spec 推斷）。
> **限制**：Hero / InteractiveDemo / Pricing / FAQ 為 client component，其字級、間距、陰影未在 SSR 出現，相關 token 標記為 TBD 或 `[original]`。
> **法律**：本檔僅引用 token 數值與類別名，不複製任何商標、文案、圖片資產。

---

## 1. Grid & Layout

| Token | 值 | 來源 |
|-------|-----|------|
| `layout.container.max-width` | `1152px` (`max-w-6xl`) | [inspired by: ideacheck.cc] header + footer 都用 `max-w-6xl mx-auto` |
| `layout.container.padding.x` | `24px` (`px-6`) | [inspired by: ideacheck.cc] |
| `layout.container.padding.y.header` | `12px` (`py-3`) | [inspired by: ideacheck.cc] |
| `layout.container.padding.y.footer` | `40px` (`py-10`) | [inspired by: ideacheck.cc] |
| `layout.section.id-anchors` | `#hero, #demo, #data-sources, #pricing, #faq` | [inspired by: ideacheck.cc]（建議重新命名以對齊你的產品語意） |
| `breakpoint.sm` | `640px` | [original] Tailwind 預設；ideacheck nav 使用 `sm:flex` 折疊 |
| `breakpoint.md` | `768px` | [original] |
| `breakpoint.lg` | `1024px` | [original] |
| `breakpoint.xl` | `1280px` | [original] |
| `breakpoint.2xl` | `1536px` | [original] |
| `layout.header.grid` | `grid grid-cols-3 items-center` | [inspired by: ideacheck.cc] 三欄式 header（logo / nav / actions） |

> ⚠️ 與 `00_foundations_spec.md` 差異：00 spec 預設 `1280px` container，ideacheck 縮為 `1152px`。clone 採用 1152px，需在你的衍生 spec 標註 override。

---

## 2. Color System

### 2.1 Brand

| Token | 值 | 來源 |
|-------|-----|------|
| `color.brand.primary` | `#4F46E5` (Tailwind `indigo-600`) | [inspired by: ideacheck.cc] login CTA `bg-indigo-600` |
| `color.brand.primary.hover` | `#4338CA` (`indigo-700`) | [inspired by: ideacheck.cc] `hover:bg-indigo-700` |
| `color.brand.primary.active` | `#3730A3` (`indigo-800`) | [original] 依 Tailwind 階梯外推 |
| `color.brand.secondary` | TBD | [original] SSR 無線索 |
| `color.brand.accent` | TBD | [original] |

### 2.2 Neutral / Surface

| Token | 值 | 來源 |
|-------|-----|------|
| `color.bg.page` | `#FFFFFF` | [inspired by: ideacheck.cc] body 預設白底 |
| `color.bg.nav` | `rgba(255,255,255,0.8) + backdrop-blur-md` | [inspired by: ideacheck.cc] `bg-white/80 backdrop-blur-md` |
| `color.bg.surface` | `#F9FAFB` (`gray-50`) | [original] 與 00 spec 對齊 |
| `color.bg.elevated` | `#FFFFFF` | [original] |
| `color.text.primary` | `#030712` (`gray-950`) | [inspired by: ideacheck.cc] `text-gray-950` 用於 logo wordmark |
| `color.text.secondary` | `#6B7280` (`gray-500`) | [original] |
| `color.text.tertiary` | `#9CA3AF` (`gray-400`) | [inspired by: ideacheck.cc] footer copyright `text-gray-400`（⚠️ AA 不足，建議提升） |
| `color.text.inverse` | `#FFFFFF` | [inspired by: ideacheck.cc] CTA 上的 `text-white` |
| `color.border.default` | `rgba(3,7,18,0.05)` (`border-gray-950/5`) | [inspired by: ideacheck.cc] header / footer border |

### 2.3 Semantic

| Token | 值 | 來源 |
|-------|-----|------|
| `color.success` | `#22C55E` | [original] 對齊 00 spec |
| `color.warning` | `#EAB308` | [original] |
| `color.error` | `#EF4444` | [original] |
| `color.info` | `#3B82F6` | [original] |

> SSR 無語意色出現；以 00 spec 預設值補齊，避免 spec 空洞。

---

## 3. Typography

| Token | 值 | 來源 |
|-------|-----|------|
| `text.font.sans` | `Inter, -apple-system, BlinkMacSystemFont, 'Segoe UI', sans-serif` | [inspired by: ideacheck.cc] body class `inter_…` |
| `text.font.zh` | `'Noto Sans TC', 'PingFang TC', 'Microsoft JhengHei', sans-serif` | [original] 對齊 00 spec（ideacheck 為 `lang="zh-Hant"` 但未指定中文 stack） |
| `text.body.md` | `16px / 1.5 / 400` | [inspired by: ideacheck.cc] login button `text-sm`，footer `text-sm` |
| `text.body.sm` | `14px / 1.5 / 400` (`text-sm`) | [inspired by: ideacheck.cc] |
| `text.body.base` | `16px / 1.5 / 400` (`text-base`) | [inspired by: ideacheck.cc] logo wordmark `text-base font-bold tracking-tight` |
| `text.heading.md` | `24px / 1.3 / 600` | [original] Hero 為 client，無實證 |
| `text.heading.lg` | `30px / 1.25 / 600` | [original] |
| `text.heading.xl` | `36px / 1.2 / 700` | [original] |
| `text.display` | `48px / 1.1 / 700` | [original] Hero 假設值 |
| `text.tracking.tight` | `-0.025em` | [inspired by: ideacheck.cc] `tracking-tight` 用於 brand wordmark |
| `text.weight.bold` | `700` (`font-bold`) | [inspired by: ideacheck.cc] |
| `text.weight.medium` | `500` (`font-medium`) | [inspired by: ideacheck.cc] CTA |

---

## 4. Spacing

| Token | 值 | 來源 |
|-------|-----|------|
| `space.base` | `4px` | [original] Tailwind 4px 基數 |
| `space.2` | `8px` (`gap-2`) | [inspired by: ideacheck.cc] header actions gap |
| `space.4` | `16px` (`gap-4`) | [inspired by: ideacheck.cc] footer column gap |
| `space.6` | `24px` (`px-6`, `gap-6`) | [inspired by: ideacheck.cc] 容器 padding 與 footer 群組間距 |
| `space.8` | `32px` (`gap-8`) | [inspired by: ideacheck.cc] 主 nav 連結間距 |
| `space.10` | `40px` (`py-10`) | [inspired by: ideacheck.cc] footer 垂直 padding |

---

## 5. Border & Radius

| Token | 值 | 來源 |
|-------|-----|------|
| `border.width.default` | `1px` | [inspired by: ideacheck.cc] `border-b border-gray-950/5` |
| `border.style` | `solid` | [original] |
| `radius.sm` | `4px` | [original] |
| `radius.md` | `6px` | [original] |
| `radius.lg` | `8px` (`rounded-lg`) | [inspired by: ideacheck.cc] login CTA `rounded-lg` |
| `radius.xl` | `12px` | [original] |
| `radius.full` | `9999px` | [original] |

---

## 6. Elevation & Shadow

| Token | 值 | 來源 |
|-------|-----|------|
| `shadow.none` | `none` | [original] header 沒下陰影，靠 backdrop-blur 與 1px border 區分 |
| `shadow.sm` | `0 1px 3px rgba(0,0,0,0.1), 0 1px 2px rgba(0,0,0,0.06)` | [original] 對齊 00 spec |
| `shadow.md` | `0 4px 6px rgba(0,0,0,0.1), 0 2px 4px rgba(0,0,0,0.06)` | [original] |
| `shadow.lg` | `0 10px 15px rgba(0,0,0,0.1), 0 4px 6px rgba(0,0,0,0.05)` | [original] |
| `shadow.xl` | `0 20px 25px rgba(0,0,0,0.1), 0 10px 10px rgba(0,0,0,0.04)` | [original] |

> SSR 無 shadow class，皆為 `[original]`。

---

## 7. Iconography

| Token | 值 | 來源 |
|-------|-----|------|
| `icon.size.sm` | `16px` | [original] |
| `icon.size.md` | `20px` | [original] |
| `icon.size.lg` | `24px` | [inspired by: ideacheck.cc] footer logo `w/h=24` |
| `icon.size.xl` | `28px` | [inspired by: ideacheck.cc] header logo `w/h=28` |
| `icon.style` | outline, 1.5px stroke | [original] 建議 Lucide |
| `icon.color` | `currentColor` | [original] |

---

## 8. Motion & Animation

| Token | 值 | 來源 |
|-------|-----|------|
| `motion.duration.fast` | `150ms` | [original] Tailwind `transition-colors` 預設 |
| `motion.duration.normal` | `200ms` | [original] |
| `motion.duration.slow` | `300ms` | [original] |
| `motion.ease.default` | `cubic-bezier(0.4, 0, 0.2, 1)` | [original] |
| `motion.transition.button` | `transition-colors 150ms` | [inspired by: ideacheck.cc] login CTA hover 為顏色過渡 |

> Hero / Demo / FAQ 為 client component，可能含開合動畫，但 SSR 無證據；皆 `[original]`。

---

## 9. Z-Index

| Token | 值 | 來源 |
|-------|-----|------|
| `z.sticky` | `50` (`z-50`) | [inspired by: ideacheck.cc] sticky nav |
| `z.dropdown` | `20` | [original] |
| `z.modal` | `40` | [original] |
| `z.toast` | `50` | [original] |
| `z.tooltip` | `60` | [original] |

---

## 10. Metadata Block（SEO）

| 欄位 | 來源 |
|------|------|
| `<title>` | [inspired by: ideacheck.cc] 完整 OG / Twitter metadata 是來源最大優點 |
| `<meta name="description">` | [inspired by: ideacheck.cc] |
| OG: `og:title / og:description / og:image / og:url / og:type` | [inspired by: ideacheck.cc] |
| Twitter Card: `summary_large_image` | [inspired by: ideacheck.cc] |
| `<meta name="robots">` | ⚠️ 來源若為 `noindex`，clone 必須改為 `index, follow` |
| `<link rel="canonical">` | [original] 來源未確認；建議補上 |

---

## 與 `00_foundations_spec.md` 對應差異（必須在使用前知道）

| 項目 | 00 spec 預設 | ideacheck 觀察 | clone 採用 |
|------|--------------|----------------|------------|
| Container max-width | 1280px | 1152px (`max-w-6xl`) | 1152px |
| Brand primary | TBD | indigo-600 | OVERRIDE 為你的選擇 |
| Header style | TBD | sticky + backdrop-blur + 1px bottom border | 沿用 |
| Section anchors | 無強制 | 5 段錨點 | 沿用骨架，內容自定 |

---

## TBD 清單（需 headless render 才能補齊）

- Hero h1 字級、字重、tracking、與 `text.display` token 對應
- InteractiveDemo 表單欄位 token（input height、border、padding）
- Pricing 卡片 padding、shadow、`radius` 等級
- FAQ accordion duration / easing
- 任何 hero / pricing 用到的 secondary brand 色

---

**版本**：v0.1
**最後更新**：2026-04-08
**狀態**：partial（client-rendered 區塊未涵蓋）
