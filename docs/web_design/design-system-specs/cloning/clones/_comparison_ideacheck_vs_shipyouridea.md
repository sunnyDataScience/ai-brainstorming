# Comparative Analysis: ideacheck.cc vs shipyouridea.today

- **Date**: 2026-04-08
- **Targets**: [https://ideacheck.cc/](https://ideacheck.cc/) and [https://shipyouridea.today/](https://shipyouridea.today/)
- **Unit**: comparative-analysis

## TL;DR

Both sites are the **same Next.js codebase** deployed twice with different branding and one structural delta (ideacheck.cc renders an extra `DataSources` section). They share identical Tailwind class vocabulary, identical Inter font asset hash, identical body className token, identical RSC component IDs, identical providers (LocaleProvider / AuthProvider / LanguageSwitcher / IconMark), identical locale (`zh-Hant`), and identical copyright year (`© 2026`). Build IDs and chunk hashes differ — they are independent deploys, not a single domain alias.

This is a clean case study for **one-codebase multi-brand launches**: a founder running two storefronts on top of one app to test brand framing, TLD, and section composition without forking the codebase.

## Evidence of Shared Codebase


| Attribute           | Match         | Notes                                                                                                                                    |
| ------------------- | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| Body className      | identical     | `inter_5972bc34-module__OU16Qa__className min-h-screen bg-background antialiased`                                                        |
| Inter font asset    | identical     | `/_next/static/media/83afe278b6a6bb3c-s.p.0q-301v4kxxnr.woff2` (verified by `diff` — empty)                                              |
| RSC component IDs   | overlapping   | `38829 Hero`, `68975 InteractiveDemo`, `50512 Pricing`, `26697 FAQ` registered on both; `18639 DataSources` registered on ideacheck only |
| Tailwind vocabulary | identical     | `indigo-600`, `bg-white/80`, `backdrop-blur-md`, `max-w-6xl`, `rounded-lg`, `border-gray-950/5`, `text-gray-950/500/400`                 |
| Nav structure       | identical     | 3-column grid, sticky, backdrop-blur                                                                                                     |
| Footer structure    | identical     | `border-t flex mx-auto` wrapper                                                                                                          |
| Providers           | identical     | `LocaleProvider`, `AuthProvider`, `LanguageSwitcher`, `IconMark`                                                                         |
| Locale              | identical     | `zh-Hant`                                                                                                                                |
| Copyright           | identical     | `© 2026`                                                                                                                                 |
| Meta description    | identical     | verbatim string                                                                                                                          |
| Robots meta         | identical     | `<meta name="robots" content="noindex"/>` on both                                                                                        |
| Build ID            | **different** | `M61bP0CPahF6DmBfa7TKN` vs `UkVvqOg2r4imiTx9mVAsu`                                                                                       |
| Chunk hashes        | **different** | independent builds, not a CDN alias                                                                                                      |


The combination "identical font hash + identical className token + different build IDs" is the strongest evidence: the source tree is shared, but each domain ran its own `next build`.

## Observable Deltas


| Attribute    | ideacheck.cc                                        | shipyouridea.today                                              |
| ------------ | --------------------------------------------------- | --------------------------------------------------------------- |
| `<title>`    | IdeaCheck — 你的點子能活多久？                               | ShipYourIdea — 你的點子能活多久？                                        |
| Brand        | IdeaCheck                                           | ShipYourIdea                                                    |
| TLD          | `.cc`                                               | `.today`                                                        |
| Sections     | Hero, Demo, **DataSources**, Pricing, FAQ           | Hero, Demo, Pricing, FAQ                                        |
| Nav links    | 服務 / 數據來源 / 價格 / FAQ                                | 範例 / 價格 / FAQ                                                   |
| Footer links | 7                                                   | 5                                                               |
| Logo size    | 28 / 24                                             | 36 / 32                                                         |
| Favicon      | 48×48                                               | 64×64                                                           |
| Contact      | [service@ideacheck.cc](mailto:service@ideacheck.cc) | [service@shipyouridea.today](mailto:service@shipyouridea.today) |
| Robots       | `noindex` (verified)                                | `noindex` (verified)                                            |
| HTML payload | 14,548 bytes                                        | 13,442 bytes                                                    |


The 1.1 KB delta is almost entirely the extra `DataSources` section block plus two extra footer links — consistent with a single conditional render (e.g. an env flag or per-brand config object).

## Strategic Interpretation

Three competing hypotheses for why one founder runs both:

### H1 — A/B test of trust narratives

ideacheck.cc leads with **trust-via-DataSources** (here are the public sources we ingest); shipyouridea.today leads with **trust-via-Demo** (here is the product working). Both are `noindex`, so neither is competing for SEO — consistent with an experiment that routes traffic from paid or community channels.

**How to confirm**: look for distinct UTM tags, distinct PostHog/GA project IDs, or distinct paid-ad creatives pointing at each domain. If both share the same analytics project but different `utm_source`, H1 is dominant.

### H2 — Localization / market segmentation by TLD

`.cc` is cheap, internationally neutral, popular in CN/TW indie circles; `.today` reads as English-first, founder-blog flavored. Same `zh-Hant` locale on both weakens this hypothesis but doesn't kill it — the founder could be staging an English variant.

**How to confirm**: monitor whether shipyouridea.today flips its `<html lang>` to `en` over the next weeks, or adds a hreflang pair pointing to ideacheck.cc.

### H3 — Gradual rebrand

The founder is migrating from IdeaCheck to ShipYourIdea, keeping the old domain alive during the transition. The leaner section list on shipyouridea.today (no DataSources) is consistent with an editorial decision that "DataSources is too cold for the new brand voice".

**How to confirm**: watch for DNS / 301 changes on ideacheck.cc, or for the IdeaCheck title to acquire a "(legacy)" marker. If ideacheck.cc disappears or starts redirecting within a few weeks, H3 wins.

The three hypotheses are not mutually exclusive — H1+H2 is the most likely combination given the public evidence today.

## Clone Implications for Our Workflow

When a clone target has a sibling site sharing its codebase, **the diff between siblings is a richer signal than either site alone**. The diff isolates what is configurable vs structural, what is brand vs product, and what the founder treats as the experimental surface. Single-site cloning loses this signal entirely.

**Recommendation to add to `CLONE_WORKFLOW_PLAYBOOK.md` in a future unit** (do not edit it here): add a "sibling discovery" pre-step — given a target URL, search for sites sharing its body className, font hash, or RSC component IDs. If a sibling exists, capture both and run a structural diff before extracting the design system. The diff will tell you which tokens are brand-locked vs product-locked.

## Reusable Takeaways

1. **Lean nav works.** shipyouridea.today ships only 3 nav links (範例 / 價格 / FAQ) and the landing still feels complete. We can drop nav items aggressively without breaking comprehension — especially on `noindex` experiment pages where SEO link equity is irrelevant.
2. **OG / favicon sizing.** shipyouridea.today bumped favicon to 64×64 and logo to 36/32 vs ideacheck.cc's 28/24. For social-share OG images we should target **1200×630** regardless — both sites currently under-invest here, which is a missed retweet-driver.
3. **i18n baseline is cheap.** Both sites ship `LocaleProvider` + `LanguageSwitcher` even though they only render `zh-Hant` today. Wiring i18n at MVP time costs almost nothing and unlocks H2-style market segmentation later. We should adopt the same pattern in our own landing scaffold.

## Verification Log

- HTML fetched via `curl -sL -A "Mozilla/5.0"` (both sites return HTTP 200; `/robots.txt` returns 500 — handled at app layer via meta tag instead).
- Font-hash diff: `diff <(curl ... ideacheck) <(curl ... shipyouridea)` of the substring `83afe278b6a6bb3c-s.p.0q-301v4kxxnr` → **empty** (confirmed identical).
- Build IDs extracted: `M61bP0CPahF6DmBfa7TKN` (ideacheck), `UkVvqOg2r4imiTx9mVAsu` (shipyouridea).
- Robots meta extracted: both `noindex`.

