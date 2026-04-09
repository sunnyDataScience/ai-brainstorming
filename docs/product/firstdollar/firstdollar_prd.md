# 專案簡報與產品需求文件 (PRD) — FirstDollar（首單）

> **版本：** v1.0 ｜ **更新：** 2026-04-09 ｜ **狀態：** 草稿（待產品負責人審核）

---

## 前言：本文件的由來

本 PRD 來自一次「**產品經理視角 + 平行多角色 persona 訪談 + UX 市場調查**」的收斂演練。

**輸入材料**：
1. `ai_one_person_company_0to1_strategy.md` — 0→1 產品市場挖掘、評估到變現全流程策略文件
2. `VibeCcoing.md` — 市場側觀察：「Vibe Coding 做產品為什麼失敗」— 痛點不明與分發能力不足是產品失敗主因
3. `docs/web_design/design-system-specs/cloning/clones/ideacheck` 與 `shipyouridea` — 兩個台灣現役競品的 L0-L4 分析與差異化報告

**方法論**：
- 以 PM 視角逐條盤點現行 idea-validation SaaS 的斷點
- 平行派出 5 個具體 persona agent（indie hacker、電商媽媽、Growth PM、創作者、顧問）進行模擬深度訪談
- 以 UX 角度匯整市場調查結論
- 依 `02_project_brief_and_prd.md` 格式輸出

---

## 0. 市場調查摘要（Persona × UX 洞察）

### 0.1 五個 persona 的關鍵訊號

| Persona | 一句毒評 / 真實痛點 | 願付金額 |
| :--- | :--- | :--- |
| **阿傑**（32，資深後端 indie hacker） | 「把我 Google 5 分鐘就能查到的答案包裝成 AI 報告賣我錢。」痛點：技術潔癖讓他永遠在 setup，做到 60% 就對「有沒有人要」失去信心。 | $49–79 USD/月（for 陪執行） |
| **淑芬**（45，電商手作媽媽） | 「它憑什麼知道？它有買過我的東西嗎？」痛點：新品前無法 test water，每次都在賭；不會行銷、不會廣告；Shopee 演算法整她。 | NT$300–500/月，**不綁約** |
| **Vivian**（29，Growth PM wantrepreneur） | 「它們賣的是 validation，交付的是更焦慮的我。」痛點：羞恥感、冒牌者焦慮、孤獨；卡在 30% 就回去滑 X 看別人 MRR。 | $49–79/月；拿到第一個 paying user 可付到 $149 |
| **Kai**（27，AI 工具 YouTuber，8.5 萬訂閱） | 「score 是空氣，$ 才是真的。」痛點：有點子沒有手（外包崩壞）、粉絲需求爛在留言區、收入綁在別人產品。 | 會為「省 5 小時或真的賺到第一塊錢」做真心業配 |
| **David**（38，UX 顧問） | 「它們賣的是採取行動的幻覺——跟冥想 app 同一個貨架。」痛點：接案機會成本殺死 side project；隱性知識無法資產化；idea scoring 工具在優化錯的 15%。 | 為 client ops / knowledge graph「今天刷卡」 |

### 0.2 五個 persona 的跨越性共識（強訊號）

1. **沒有人真的用 IdeaCheck 類的分數做決策** — 5/5 persona 全部毒舌，包括兩位實際付過費的（Vivian、阿傑）。
2. **痛點不是「評估」是「執行」** — 他們要的是紀律、陪跑、成交，不是報告。
3. **「分發 / 獲客」的痛遠大於「產品力」** — Kai、淑芬、David 都明確點出；與 `VibeCcoing.md` 影片觀察一致。
4. **卡在 30–60% 棄坑的心理斷點** — Vivian 卡 30%、阿傑卡 60%、Kai 外包翻車，都缺一個「接住卡關那一刻」的機制。
5. **中文市場有在地化空窗** — 淑芬明確表示「不要叫我是創業者，我就是一個賣東西的媽媽」。現行 ideacheck 雖是 zh-Hant 但敘事仍是 indie hacker 話術。

### 0.3 UX 角度的四個市場洞察

| # | 洞察 | 設計含義 |
| :--- | :--- | :--- |
| UX-1 | **「AI 生分數」的 UX 是焦慮產品不是生產力產品**（David 語）。使用者付錢後得到數字 → 更焦慮 → 不行動。 | 產品**禁止出現 0-100 的 idea score**。所有輸出都必須是「下一個可執行動作」。 |
| UX-2 | **IdeaCheck 的 5 區段 landing 結構預設使用者是被說服付費的，但 validation 工具用戶是懷疑的**。 | Landing 要反向設計：先讓使用者**在未註冊狀態下跑完一次 demo**，看到「第一塊錢」的可能性再轉註冊。 |
| UX-3 | **現行工具把「輸出報告」當交付點，實際使用者的 Job-to-be-Done 是「拿到第一筆錢」**。 | North Star Metric = **使用者透過本平台收到的第一筆付款**（來自 David 的訪談金句）。 |
| UX-4 | **用戶最需要的是「外部紀律」而非更多自由**（阿傑：「我認真的，做不到就扣我信用卡當罰款」；Vivian：「現在的 AI 都太有禮貌了，我需要一個兇一點的」）。 | 產品需具備「主動 ping、倒數、羞恥感機制」的紀律層。 |

### 0.4 產品命題一句話

> **FirstDollar 是一個反 IdeaCheck 的 1 人公司執行陪跑平台。我們不打分數、不生報告；而是在 7 天內用真實受眾訪談、自動 landing page、waitlist 收集與 Stripe 金流串接，逼你拿到從 0→1 的第一個付費信號。**

---

## 1. 專案總覽

| 項目 | 內容 |
| :--- | :--- |
| **專案名稱** | FirstDollar（首單）|
| **Slug** | `firstdollar` |
| **狀態** | 規劃中（PRD v1.0） |
| **目標發布日期** | 2026-06-30（MVP Private Beta） |
| **核心團隊** | PM: TBD ｜ Lead Engineer: TBD ｜ UX: TBD |
| **一句話定位** | 不評估點子、只逼你在 7 天內拿到第一塊錢的 AI co-founder |
| **North Star Metric** | $ / 週：使用者透過本平台收到的實際付款金額（不是註冊數、不是 DAU） |

---

## 2. 商業目標

| 項目 | 內容 |
| :--- | :--- |
| **背景與痛點** | 台灣與東亞市場有一批 wantrepreneur（indie hacker、電商賣家、Growth PM、創作者、顧問）累積 idea 卻無法 ship。現行 idea-validation SaaS（IdeaCheck、ShipYourIdea、IdeaBrowser）普遍被認為是「焦慮產品」— 交付報告而非結果。使用者真正的痛點是：(1) 不知道怎麼開始驗證、(2) 卡在 30-60% 棄坑、(3) 沒有分發能力、(4) 沒有外部紀律。 |
| **策略契合度** | 承接 `ai_one_person_company_0to1_strategy.md` 的核心觀點：「1 人公司的勝負在把 需求 → 假設 → MVP → 付費驗證 做成一條可重複的流水線」。FirstDollar 就是這條流水線的可執行工具層。 |
| **成功指標（Year 1）** | **主要**：Paying Customer 產生第一筆真實 revenue 的比例 ≥ 25%（相較於行業 2-3%）<br>**次要**：自家 MRR US$10k（month 6）/ US$25k（month 12）；退款率 < 8%；NPS ≥ 40 |
| **差異化護城河** | (1) **North Star = 使用者的錢，不是自家 DAU**；(2) **反焦慮 UX**，禁止 idea score；(3) **外部紀律層**，主動 ping 與倒數；(4) **中文 / 台灣支付優先**（對比 ideacheck 表面 zh-Hant 但骨子 indie hacker 話術） |

---

## 3. 使用者故事與允收標準

### Epic 1: 無痛上手與期望設定（Onboarding & Expectation）

| ID | 描述 (As a / I want to / So that) | 允收標準 | BDD 連結 |
| :--- | :--- | :--- | :--- |
| US-001 | As 一位 wantrepreneur，I want to 在未註冊的狀態下完成一次「idea → 首個 landing page → 模擬收款」的 demo，so that 我能在付費前先感受真實交付，而不是被 5 段 landing 說服。 | 1. 首頁 CTA 點擊後直接進入 `/demo` 互動流程（不需 email）<br>2. 用戶輸入一句 idea 後，≤ 60 秒產出一份可預覽的 landing page 草稿<br>3. 頁尾出現「你下一步真實要做的 3 件事（未註冊不會儲存）」 | `onboarding-demo.feature` |
| US-002 | As 淑芬（非技術背景中年賣家），I want to 全中文介面且用「賣東西、試水溫」這種人話，so that 我不會被 founder 話術嚇跑。 | 1. 預設語系為 zh-Hant，複本避免 founder / MRR / PMF 等行話<br>2. 提供「我是 __」persona 選單（含「賣東西的個人店家」）調整複本<br>3. 付費方案至少支援一個「台幣月付、不綁約、可隨時停用」選項 | `persona-copy.feature` |

### Epic 2: 七日 Sprint — 從 idea 到首單

| ID | 描述 (As a / I want to / So that) | 允收標準 | BDD 連結 |
| :--- | :--- | :--- | :--- |
| US-010 | As Vivian（Growth PM），I want to 進入一個有明確 Day 1–Day 7 任務卡的 Sprint 模式，so that 我不會卡在第 30% 就跑去滑 X。 | 1. 啟動 Sprint 後系統產出 7 天任務卡（每天 1-3 個任務，總時間 ≤ 90 分鐘）<br>2. 每天未達成會觸發「逼迫機制」（見 Epic 4）<br>3. 任務卡內容是動作而非學習（如「貼到這 3 個社團」而不是「學習分發」） | `sprint-7day.feature` |
| US-011 | As 阿傑（有技術能力但卡在 setup），I want to 系統鎖定我的技術棧選擇（不准換），so that 我不會再掉進 rabbit hole。 | 1. Sprint 開始時鎖定 stack（預設：Next.js + Stripe + Resend + Supabase）<br>2. 任何 stack 變更需 friction 確認（輸入「我知道這會讓我更慢」）<br>3. 提供 1 個預設 template repo 直接 clone，不提供多選 | `stack-lock.feature` |
| US-012 | As Kai（有受眾但沒手），I want to 把我 IG 私訊 / YouTube 留言 / Discord 貼進來，so that 系統幫我萃取「這週受眾最想買的 3 個 offer」。 | 1. 支援貼上 raw text / 上傳 CSV / 接 IG Basic Display API（v1 僅支援前兩者）<br>2. 輸出 3 個具體 offer（含定價建議、一句話賣點、適合的 landing page 模板）<br>3. 不得輸出任何 0-100 分數 | `audience-to-offer.feature` |

### Epic 3: 真實金流閉環（The First Dollar）

| ID | 描述 (As a / I want to / So that) | 允收標準 | BDD 連結 |
| :--- | :--- | :--- | :--- |
| US-020 | As 任何使用者，I want to 在不懂程式的情況下 1 小時內產出一個「能真的收到付款」的 landing page + 結帳按鈕，so that 我知道有沒有人願意掏錢。 | 1. 提供 5 個預設 landing 模板（Hero+CTA+Waitlist、Hero+Price+Stripe、Hero+Pre-order、Hero+Service booking、Hero+Donate）<br>2. 內建 Stripe / TapPay（台灣）一鍵串接<br>3. 發布後回傳可分享 URL，並自動加上 UTM 與追蹤 | `landing-checkout.feature` |
| US-021 | As 使用者，I want to 看到「這週我因為這個平台多賺了多少錢」的 revenue dashboard，so that 我知道平台值不值得續訂。 | 1. Dashboard 首卡片是 **$ This Week** 絕對數字，而非百分比<br>2. 若本週為零，顯示「下一步該做什麼」而非空狀態圖<br>3. 禁止出現任何 idea score、health score、AI confidence 等抽象指標 | `revenue-dashboard.feature` |

### Epic 4: 外部紀律層（The Cofounder Who Won't Let You Ghost）

| ID | 描述 (As a / I want to / So that) | 允收標準 | BDD 連結 |
| :--- | :--- | :--- | :--- |
| US-030 | As 一個會放棄的人（所有 persona），I want to 系統在我卡關時主動聯繫我，so that 我不會默默消失。 | 1. 任務卡未完成超過 24hr 觸發 Email / LINE 推播<br>2. 連續 3 天未完成觸發 AI co-founder 深度對話介入（含「我知道你卡在哪，要我幫你做 X 嗎？」而非空洞鼓勵）<br>3. 對話要有記憶（記住上次卡點與選擇） | `discipline-ping.feature` |
| US-031 | As 自認需要被逼的使用者（opt-in），I want to 設定「承諾金」，so that 我不達標會被扣款。 | 1. Sprint 開始時 opt-in「承諾金」$50-$200（預授權）<br>2. 7 天內未達成任一「硬門檻」（如發布 landing、收到 1 個 email waitlist）則扣款<br>3. 款項作為捐款而非平台收入（避免道德問題） | `commitment-bond.feature` |

### Epic 5: 反焦慮設計紀律（Design Constraints）

| ID | 描述 | 允收標準 |
| :--- | :--- | :--- |
| US-040 | As 使用者，I do NOT want to 在任何畫面看到 idea score、市場評分、AI 信心分數等抽象數字。 | 所有 UI 禁止渲染 0–100 / 五星評分 / A-F 等抽象評價。QA 有一條 lint rule 檢查 design system。 |
| US-041 | As 使用者，I want to 所有 AI 輸出都以「下一步可執行動作」結尾。 | AI prompt 模板強制要求輸出結構：`發現 → 動作 → 今天做哪一件`。沒有 action 的回應視為 bug。 |

---

## 4. 範圍與限制

| 項目 | 內容 |
| :--- | :--- |
| **MVP 功能範圍（≤ 3 個核心）** | 1. **7-Day Sprint Engine**（任務編排 + 每日推播 + 紀律層）<br>2. **Landing + Stripe 一鍵發布**（5 個模板 + TapPay 台灣金流）<br>3. **Audience-to-Offer**（受眾原始資料 → 3 個可賣的 offer） |
| **非功能需求** | **性能**：Landing page 發布 TTFB < 200ms、LCP < 2s<br>**安全**：Stripe / TapPay webhook 全程 HMAC 驗證；使用者受眾資料預設不上雲訓練（呼應 David 訴求）<br>**可用性**：99.5% SLA（MVP 階段）；i18n zh-Hant 預設，en 次之<br>**SEO**：所有 landing page 採 Server Component + Structured Data（補 ideacheck 沒做的功課）<br>**無障礙**：WCAG AA；skip-link、ARIA landmarks 齊備 |
| **不做什麼（救命清單）** | 1. **不做 idea scoring** — 這是本產品的 identity，任何 PM / engineer 提議加分數一律駁回<br>2. **不做 AI 生成 PRD / 商業計畫書** — 那是 David 眼中的「結構正確但缺 context 的廢話」<br>3. **不做 App（iOS/Android）** — Web-first，降低一人公司維運成本<br>4. **不做 B2B / Enterprise plan** — 焦點在 solo<br>5. **不做「100 個點子產生器」** — 使用者不缺點子<br>6. **不做訂閱綁約** — 淑芬訊號；影響信任<br>7. **不做 Discord / Slack bot 整合**（v1）— 延後<br>8. **不做模糊的 NPS / engagement 報告** — 只呈現 $ |
| **假設與依賴** | **假設 1**：至少 25% 的活躍使用者願意在 7 天內公開發布 landing 並嘗試收款（**高風險，必須在 Private Beta 驗證**）<br>**假設 2**：台灣 solo wantrepreneur 的 willingness-to-pay 中位數能支撐 NT$690–1,490/月定價<br>**假設 3**：AI co-founder 的「紀律層」不會引發使用者反感（需 A/B 測試「主動 ping」強度）<br>**依賴**：Stripe、TapPay、Resend（email）、Supabase（auth + DB）、LLM 供應商（Claude / OpenAI） |
| **定價草案** | **Free**：1 次 Sprint 體驗（無紀律層、含本平台 branding）<br>**Pro** NT$690/月：unlimited Sprint、紀律層、5 個 landing 模板、台幣金流<br>**Coach** NT$1,490/月：+ AI co-founder 深度對話（有記憶）、承諾金機制、1v1 月度 office hour<br>**承諾**：皆可隨時停用、月付為主、年付 7 折 |

---

## 5. 待辦問題與決策

| ID | 描述 | 狀態 | 負責人 |
| :--- | :--- | :--- | :--- |
| Q-001 | 「承諾金扣款」的法務風險（台灣金管會對預授權扣款 + 績效連動的灰色地帶）是否需要改為「捐款承諾」而非平台扣款？ | 待討論 | Legal / PM |
| Q-002 | North Star Metric 要追蹤「使用者透過平台 landing 收到的 $」還是「使用者『聲稱』收到的 $」？前者受限於 Stripe 串接，後者有造假風險。 | 待討論 | PM |
| Q-003 | Persona「淑芬」（非技術中年賣家）是 MVP TA 還是 v2 TA？若納入則 UI 與複本需大幅調整。 | 待討論 | PM / UX |
| Q-004 | AI co-founder 的「兇一點」語氣要不要做語氣滑桿（禮貌 ↔ 嚴格）？Vivian 訊號要兇，但可能會傷到焦慮敏感用戶。 | 待討論 | UX / PM |
| Q-005 | 是否接受單一使用者同時跑多條 Sprint？策略文件建議「同時最多跑 1–2 條產品線」，預設應鎖定 1 條。 | 待討論 | PM |
| D-001 | **禁止渲染 idea score、health score 等抽象評分** — 這是產品 identity，不可妥協。 | 已決定 | PM |
| D-002 | **North Star Metric = 使用者收到的第一筆真實付款** — 不是 DAU、註冊數、retention。 | 已決定 | PM |
| D-003 | **MVP 禁做 App**，Web-first。 | 已決定 | PM |
| D-004 | **預設語系 zh-Hant，複本避免 founder 話術**。en 為 v1.1 目標。 | 已決定 | PM / UX |
| D-005 | **技術棧鎖定 Next.js + Supabase + Stripe + Resend**；任何替換需 RFC。 | 已決定 | Lead Eng |
| D-006 | **landing page 必須採 Server Component + JSON-LD**（補 ideacheck 缺失）。 | 已決定 | Lead Eng |

---

## 附錄 A：與 IdeaCheck / ShipYourIdea 的競品差異表

| 維度 | IdeaCheck / ShipYourIdea | FirstDollar |
| :--- | :--- | :--- |
| 核心交付 | AI 打分數 + 分析報告 | 7 天內的第一筆付款 |
| North Star | 註冊數 / 瀏覽量（推測） | $ / 週 |
| UX 結構 | 5 段 landing + CSR | 未註冊即可跑 demo + SSR |
| 使用者行動 | 看報告後自己想辦法 | 系統主動推播 + 紀律層 + 承諾金 |
| 定價敘事 | 以評估次數計費 | 以結果承諾計費（不達標退款） |
| i18n 真實度 | 表面 zh-Hant、骨子 indie hacker | zh-Hant 優先 + 在地 persona 複本 + 台幣金流 |
| SEO | client-rendered、無 Structured Data | Server Component + JSON-LD + 可被 indexed |
| 反焦慮設計 | 無 | 禁止分數、禁止抽象指標、只輸出 next action |

---

## 附錄 B：七日 Sprint Roadmap（給使用者看）

| Day | 任務 | 過關條件 |
| :--- | :--- | :--- |
| Day 1 | 定義 Problem Statement（一段話公式）+ 鎖定一個 TA | PM 可一句話描述「誰、情境、痛點、願付成本」 |
| Day 2 | 產生 3 個 offer 草案 + 選 1 | 從 audience source（貼留言 / 打 3 個電話 / 發 1 則貼文）產出證據 |
| Day 3 | 發布 landing（5 個模板任選）+ 串 Stripe / TapPay | URL 可被爬蟲抓到、結帳按鈕可點 |
| Day 4 | 在 3 個具體分發點發布（非「社群」這種模糊詞） | 3 筆真實 link 記錄 |
| Day 5 | 進行 3 個真實客戶訪談（給問題模板） | 訪談筆記 ≥ 3 筆，每筆含「替代成本」 |
| Day 6 | 調整 offer（依訪談結果） + 再次分發 | Offer diff 可追溯 |
| Day 7 | 檢視 $ / Waitlist / 回覆率 → Go / Pivot / Kill | Dashboard 自動判讀 |

---

## 附錄 C：Persona 訪談原文摘錄（市場調查根據）

> 完整訪談稿保存於 task 執行紀錄。以下為關鍵引述。

- **阿傑**：「我不缺點子，我電腦裡有 40 個 idea.md，我缺的是把其中一個做完的紀律。」
- **淑芬**：「不要叫我是『創業者』，我就是一個賣東西的媽媽，講人話我才會付錢。」
- **Vivian**：「它們賣的是 validation，交付的是更焦慮的我。」
- **Kai**：「你給我 score 我只會冷笑。score 是空氣，$ 才是真的。」
- **David**：「1 人公司只有一個真問題：能不能收到更多錢。North Star 應該是使用者每月因為這個工具多收到的付款金額。」

這 5 句話是 FirstDollar 整份 PRD 的思想源頭。任何違反這 5 句話精神的功能提案都應該被駁回。

---

**文件版本：** v1.0（草稿）
**建立日期：** 2026-04-09
**作者：** PM (via AI-assisted multi-persona UX research workflow)
**審核狀態：** 待 Product Lead / Design Lead / Legal 審閱（Q-001 ~ Q-005）
