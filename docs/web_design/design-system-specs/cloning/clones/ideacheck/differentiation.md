# Differentiation — ideacheck

> 來源網站：[https://ideacheck.cc/](https://ideacheck.cc/)
> 擷取日期：2026-04-08
> 觀察：ideacheck.cc 與 shipyouridea.today 共用同一份 Next.js codebase。
> 我們其實是在學一個「品牌變體（brand variation）」練習，而不是單一站。
> 這代表 KEEP 的東西來自「結構共識」、OVERRIDE 的東西通常就是「品牌差異」。

---

## 來源網站定位

- **受眾**：想驗證新點子的個人創業者、indie hacker、PM
- **風格**：極簡 SaaS landing；indigo 主色 + 大量留白；單頁錨點導向
- **強項**：
  - SSR header / footer 結構乾淨，sticky backdrop-blur nav 視覺現代
  - 完整 OG / Twitter metadata；SEO 起手式齊全
  - 單頁五段式（Hero / Demo / DataSources / Pricing / FAQ）對轉換漏斗友善

## 你的產品定位

- **受眾**：待你（產品擁有者）填入；建議先寫一句「為誰、解決什麼」
- **風格**：可保留簡潔，但替換主色與字型 token 以建立辨識度
- **差異點**：避開「7 維度評分」這種強綁定 IdeaCheck 的功能敘事，改用你的核心價值主張

---

## ✅ 值得保留（KEEP）


| 設計決策                                      | 為什麼好                      | 如何納入                                  |
| ----------------------------------------- | ------------------------- | ------------------------------------- |
| Sticky `bg-white/80 backdrop-blur-md` 導覽列 | 滾動時保持品牌出現；現代且不擋內容         | L1 Navbar 元件採用相同類別策略                  |
| `max-w-6xl mx-auto px-6` 容器               | 1152px 內容寬，行長對閱讀友善        | `layout.container.max-width = 1152px` |
| Inter 字體（拉丁主字）                            | 中性、解析度高，適合 SaaS           | `text.font.sans = Inter`              |
| 錨點式單頁滾動（`/#demo`、`/#pricing`...）          | Landing Page 轉換漏斗自然       | L4 sitemap 採同一錨點清單                    |
| 完整 OG / Twitter metadata                  | 對社群分享、SEO 起步友善            | L3 page template 內建 metadata block    |
| 三欄 grid header（logo / nav / actions）      | 視覺對齊穩定、好做 RWD 折疊          | L1 Header 元件骨架                        |
| Footer 雙列（brand + 法遵 + 聯絡）                | 必備法遵連結齊全（privacy / terms） | L1 Footer 範本                          |


## ⚠️ 不適合（DROP）


| 元素                                               | 為什麼不適合                               |
| ------------------------------------------------ | ------------------------------------ |
| 「7 維度評分」此類具體服務文案                                 | 強綁定 IdeaCheck 業務，搬到別站變抄襲             |
| 「IdeaCheck」品牌名與 `/logo-v2.png`                   | 商標，禁止複製                              |
| Nav 標籤「數據來源」                                     | 若你的產品沒有「資料來源」這層概念，硬留會誤導使用者           |
| `<meta name="robots" content="noindex">`（若擷取時存在） | 來源站可能尚在內測；正式上線一定要 `index, follow`    |
| InteractiveDemo / Pricing / FAQ 的具體 client copy  | client-rendered 內容未在 SSR；無證據可參考也不該照抄 |
| 共用 codebase 中可能殘留的另一品牌（shipyouridea.today）痕跡     | 不應繼承別人的品牌切換邏輯，會混淆身份                  |


## 🎨 品牌覆蓋（OVERRIDE）


| 來源 Token                    | 來源值                                        | 你的 Token                    | 你的值                                                 |
| --------------------------- | ------------------------------------------ | --------------------------- | --------------------------------------------------- |
| `color.brand.primary`       | `indigo-600` (#4F46E5)                     | `color.brand.primary`       | TBD（建議避開 indigo；如 emerald-600 / sky-600 / rose-600） |
| `color.brand.primary.hover` | `indigo-700` (#4338CA)                     | `color.brand.primary.hover` | 對應主色 -10% L                                         |
| `font.family.heading`       | Inter (`inter_`* body class)               | `font.family.heading`       | TBD（可保留 Inter，或選 Geist / Manrope 建立辨識度）             |
| `logo.asset`                | `/logo-v2.png` 28×28                       | `logo.asset`                | 你的 logo（必須自製）                                       |
| `footer.copyright`          | `© 2026 IdeaCheck.`                        | `footer.copyright`          | `© {year} {你的品牌}.`                                  |
| `contact.email`             | `service@ideacheck.cc`                     | `contact.email`             | 你的 mailbox                                          |
| `og.image`                  | IdeaCheck OG 圖                             | `og.image`                  | 你的 OG 圖（1200×630）                                   |
| 品牌字                         | 「IdeaCheck」字級 base / bold / tracking-tight | brand wordmark              | 你的 wordmark + 設計化處理                                 |


## 💡 改進機會（IMPROVE）

1. **SEO 上線預備**：補上 `<meta name="robots" content="index, follow">`、`canonical` link、產生 `sitemap.xml` 與 `robots.txt`。來源站可能還是 `noindex`，正式發布前必須切換。
2. **真實信任區塊**：把「DataSources」這種抽象元件，升級為含有真實 logo wall / 客戶見證 / 數據佐證的 Trust 區塊。沒有實際社會證明的 landing 不會轉換。
3. **可及性強化**：加上 skip-to-content link、明確的 `<header> / <main> / <footer>` ARIA landmarks、focus-visible ring、WCAG AA 對比驗證。Inter + 純白底容易產生淺灰副文案對比不足，要把 `text-gray-400` 拉到至少 `gray-600`。
4. **SSR 化關鍵內容**：來源站把 Hero / Pricing / FAQ 全塞 client component，導致 SSR HTML 沒文字——對 SEO 與首屏 LCP 都吃虧。改為 Server Component 渲染主文案，互動元素才走 client。

## 結論

> ideacheck.cc 的價值在於「乾淨的 Next.js landing 骨架」與「OG / 結構化 metadata 的起手式」，但因為它與 shipyouridea.today 共用 codebase，本質上已經是品牌變體練習；我們應該繼承它的結構紀律，丟掉它的具體文案與品牌資產，並補上 SEO 上線、真實信任、可及性、SSR 這四個它沒做的功課。

