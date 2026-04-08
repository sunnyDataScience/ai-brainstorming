# DOM Tree（簡化語意）— shipyouridea.today

> 來源：`raw/dom.html`（擷取於 2026-04-08）。
> 註記：擷取到的 HTTP 回應是 500 `__next_error__` shell，但 RSC stream 仍然序列化了完整的 layout chrome（nav + footer）以及 4 個 page-level client component 的 registry。Hero/Demo/Pricing/FAQ 的內部 copy 為 client-only，因此不在這棵樹中。

## 頂層 layout

```
<html lang="zh-Hant">
└── <body class="inter_5972bc34-module__OU16Qa__className min-h-screen bg-background antialiased">
    └── LocaleProvider
        └── AuthProvider
            └── (parallel router children)
                ├── HEADER / NAV       ← rendered in HTML
                ├── MAIN               ← client-rendered (Hero / InteractiveDemo / Pricing / FAQ)
                └── FOOTER             ← rendered in HTML
```

## HEADER / NAV（於 HTML 中渲染，信心度 HIGH）

```
<nav class="sticky top-0 z-50 w-full border-b border-gray-950/5 bg-white/80 backdrop-blur-md">
  <div class="mx-auto grid max-w-6xl grid-cols-3 items-center px-6 py-3">
    ├── <Link href="/" class="flex items-center gap-2">                  ← brand
    │     ├── <Image src="/logo-v2.png" width=36 height=36 alt="ShipYourIdea" />
    │     └── <span class="text-base font-bold tracking-tight text-gray-950">ShipYourIdea</span>
    │
    ├── <div class="hidden items-center justify-center gap-8 sm:flex">    ← primary nav (md+)
    │     ├── <a href="/#demo">範例</a>
    │     ├── <a href="/#pricing">價格</a>
    │     └── <a href="/#faq">FAQ</a>
    │
    └── <div class="col-start-3 flex items-center justify-end gap-2">     ← actions
          ├── <LanguageSwitcher />
          └── <Link href="/login"
                    class="inline-flex h-8 items-center rounded-lg bg-indigo-600 px-4
                           text-sm font-medium text-white transition hover:bg-indigo-700">
                登入
              </Link>
  </div>
</nav>
```

## MAIN（client-rendered，信心度 LOW）

依 RSC payload 中註冊順序列出的 component stack（渲染順序）：

```
<main>
  ├── <Hero />              ← module 38829   (TBD: headline, subhead, CTA copy, illustration)
  ├── <InteractiveDemo />   ← module 68975   (TBD: demo input, scoring widget, sample output)
  ├── <Pricing id="pricing" />  ← module 50512   (TBD: tier names, prices, feature lists)
  └── <FAQ id="faq" />      ← module 26697   (TBD: questions / answers, accordion behavior)
</main>
```

> 重要發現：本站**未**註冊 `DataSources` section。
> 姊妹站 ideacheck.cc 註冊的是 Hero → DataSources → InteractiveDemo → Pricing → FAQ。
> shipyouridea.today 只註冊 Hero → InteractiveDemo → Pricing → FAQ。
> 驗證方式：`grep -c '"DataSources"' raw/dom.html` → 0。

## FOOTER（於 HTML 中渲染，信心度 HIGH）

```
<footer class="border-t border-gray-950/5 px-6 py-10">
  <div class="mx-auto flex max-w-6xl flex-col items-center justify-between gap-4 sm:flex-row">
    ├── <div class="flex items-center gap-6">
    │     ├── <Link href="/" class="flex items-center gap-2">           ← brand (smaller)
    │     │     ├── <Image src="/logo-v2.png" width=32 height=32 />
    │     │     └── <span class="text-sm font-bold text-gray-950">ShipYourIdea</span>
    │     │
    │     └── <nav class="flex gap-4">                                  ← footer nav
    │           ├── <a href="#pricing">價格</a>
    │           ├── <a href="#faq">FAQ</a>
    │           ├── <a href="mailto:service@shipyouridea.today">聯絡我們</a>
    │           ├── <Link href="/privacy">隱私權政策</Link>
    │           └── <Link href="/terms">服務條款</Link>
    │
    └── <p class="text-sm text-gray-400">© 2026 ShipYourIdea.</p>
</footer>
```

## 各 Section 信心度摘要

| Section          | 來源              | 信心度     |
|------------------|-------------------|------------|
| Nav              | HTML              | HIGH       |
| Hero             | 僅 RSC registry   | LOW (TBD)  |
| InteractiveDemo  | 僅 RSC registry   | LOW (TBD)  |
| Pricing          | 僅 RSC registry   | LOW (TBD)  |
| FAQ              | 僅 RSC registry   | LOW (TBD)  |
| Footer           | HTML              | HIGH       |

## 與 ideacheck.cc 的明顯缺失元素

- registry 中任何地方都沒有 `DataSources` 元件 — 這是兩個姊妹站之間單一最大的結構差異。
