# DOM Tree (Simplified Semantic) — shipyouridea.today

> Source: `raw/dom.html` (captured 2026-04-08).
> Note: The captured HTTP response was a 500 `__next_error__` shell, but the RSC stream still serialized the full layout chrome (nav + footer) plus a registry of the four page-level client components. Inner copy of Hero/Demo/Pricing/FAQ is client-only and therefore absent from this tree.

## Top-level layout

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

## HEADER / NAV (rendered in HTML, confidence HIGH)

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

## MAIN (client-rendered, confidence LOW)

Component stack as registered in the RSC payload (render order):

```
<main>
  ├── <Hero />              ← module 38829   (TBD: headline, subhead, CTA copy, illustration)
  ├── <InteractiveDemo />   ← module 68975   (TBD: demo input, scoring widget, sample output)
  ├── <Pricing id="pricing" />  ← module 50512   (TBD: tier names, prices, feature lists)
  └── <FAQ id="faq" />      ← module 26697   (TBD: questions / answers, accordion behavior)
</main>
```

> CRITICAL FINDING: This site does NOT register a `DataSources` section.
> The companion site ideacheck.cc registers Hero → DataSources → InteractiveDemo → Pricing → FAQ.
> shipyouridea.today registers only Hero → InteractiveDemo → Pricing → FAQ.
> Verified via: `grep -c '"DataSources"' raw/dom.html` → 0.

## FOOTER (rendered in HTML, confidence HIGH)

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

## Section confidence summary

| Section          | Source            | Confidence |
|------------------|-------------------|------------|
| Nav              | HTML              | HIGH       |
| Hero             | RSC registry only | LOW (TBD)  |
| InteractiveDemo  | RSC registry only | LOW (TBD)  |
| Pricing          | RSC registry only | LOW (TBD)  |
| FAQ              | RSC registry only | LOW (TBD)  |
| Footer           | HTML              | HIGH       |

## Notable missing element vs ideacheck.cc

- No `DataSources` component anywhere in the registry — this is the single largest structural difference between the two sister sites.
