# IdeaCheck — Semantic DOM Tree

> 來源：`raw/dom.html`（Next.js RSC payload，2026-04-08 擷取）
> 註：Hero / InteractiveDemo / DataSources / Pricing / FAQ 為 client component，內部 markup 不在 SSR HTML 中，僅標記為錨點。

```
<html lang="zh-Hant">
└── <body class="inter_… min-h-screen bg-background antialiased">
    └── LocaleProvider
        └── AuthProvider
            ├── header
            │   └── nav.sticky.top-0.z-50.bg-white/80.backdrop-blur-md.border-b.border-gray-950/5   [ref $3]
            │       └── div.mx-auto.grid.max-w-6xl.grid-cols-3.items-center.px-6.py-3
            │           ├── Link href="/" (logo)
            │           │   ├── Image src="/logo-v2.png" w/h=28
            │           │   └── span.text-base.font-bold.tracking-tight.text-gray-950 → "IdeaCheck"
            │           ├── div.hidden.sm:flex.items-center.justify-center.gap-8  (primary nav)
            │           │   ├── a href="/#demo"          → "服務"
            │           │   ├── a href="/#data-sources"  → "數據來源"
            │           │   ├── a href="/#pricing"       → "價格"
            │           │   └── a href="/#faq"           → "FAQ"
            │           └── div.col-start-3.flex.items-center.justify-end.gap-2
            │               ├── LanguageSwitcher  [ref $L18]
            │               └── Link href="/login" .inline-flex.h-8.rounded-lg.bg-indigo-600.px-4.text-sm.font-medium.text-white.hover:bg-indigo-700 → "登入"
            │
            ├── main
            │   ├── <Hero />              [client, ref $L4 → chunk 38829]   §id=hero (TBD: copy not in SSR)
            │   ├── <InteractiveDemo />   [client, ref $L5 → chunk 68975]   §id=demo
            │   ├── <DataSources />       [client, ref $L6 → chunk 18639]   §id=data-sources
            │   ├── <Pricing />           [client, ref $L7 → chunk 50512]   §id=pricing
            │   └── <FAQ />               [client, ref $L8 → chunk 26697]   §id=faq
            │
            └── footer.border-t.border-gray-950/5.px-6.py-10               [ref $9]
                └── div.mx-auto.flex.max-w-6xl.flex-col.items-center.justify-between.gap-4.sm:flex-row
                    ├── div.flex.items-center.gap-6
                    │   ├── Link href="/" (footer brand)
                    │   │   ├── Image src="/logo-v2.png" w/h=24
                    │   │   └── span.text-sm.font-bold.text-gray-950 → "IdeaCheck"
                    │   └── nav.flex.gap-4
                    │       ├── a href="#demo"            → "服務"
                    │       ├── a href="#data-sources"    → "數據來源"
                    │       ├── a href="#pricing"         → "價格"
                    │       ├── a href="#faq"             → "FAQ"
                    │       ├── a href="mailto:service@ideacheck.cc" → "聯絡我們"
                    │       ├── Link href="/privacy"      → "隱私權政策"
                    │       └── Link href="/terms"        → "服務條款"
                    └── p.text-sm.text-gray-400 → "© 2026 IdeaCheck."
```

## 信心評估

| 區段 | 信心 | 原因 |
|---|---|---|
| header / nav | high | SSR 完整輸出 |
| footer | high | SSR 完整輸出 |
| Hero | low | client component，內容 hydrate 後才出現 |
| InteractiveDemo | low | 同上 |
| DataSources | low | 同上 |
| Pricing | low | 同上 |
| FAQ | low | 同上 |

## 待補（需要 headless browser 渲染）

- Hero h1 / sub-headline / primary CTA 文案與樣式
- InteractiveDemo 表單欄位、佔位符、按鈕、結果區
- DataSources 卡片清單與來源 logo
- Pricing 方案、價錢、特性條列、CTA
- FAQ 問題清單與展開動畫
