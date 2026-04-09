# 專案簡報與產品需求文件 (PRD) — FirstDollar（首單）

> **版本：** v2.0 ｜ **更新：** 2026-04-09 ｜ **狀態：** 草稿（待產品負責人審核）
>
> **v2.0 重大變更：** 經 S1→F→S2 第一性原理壓力測試（見 `socratic_first_principles_rnd_workflow.md`），發現 v1.0 存在三處定義漂移（D1–D3），已全面修正 MVP 定義。詳見 §0.5。

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

### 0.5 v2.0 定義漂移修正（S1→F→S2 壓力測試結果）

> **背景**：v1.0 經 `socratic_first_principles_rnd_workflow.md` 的 S1→F→S2 管線壓力測試，發現三處與 `first_principles_playbook.md` §2 物理量矛盾的定義漂移。以下為修正紀錄。

#### 三處定義漂移

| # | 漂移 | 物理量要求 | v1.0 的偏離 | v2.0 修正 |
| :--- | :--- | :--- | :--- | :--- |
| **D1** | 把 AI 模擬的 persona 當真人 | 具體的人 = 有名字、能打電話給 3 位 | 5 個 persona 皆為 AI agent 模擬訪談產出 | **persona 降格為假設**，須用真人訪談驗證後才能作為設計依據 |
| **D2** | 把「建系統」當「交付價值」 | 手工交付 = 今晚就做一次給 1 個人 | MVP 定義為 6 大軟體模組（Sprint Engine、Landing Builder 等） | **MVP 重定義為手工版**：PM 本人 = Sprint Engine + Co-founder + 紀律層 |
| **D3** | 把「基礎設施」當「產品」 | 錢的管道 = 一條收款連結即可 | 需 Stripe Connect + TapPay 整合 + Revenue Telemetry | **不碰錢**：教使用者自行開 Lemon Squeezy / Stripe 帳戶（10 分鐘） |

#### 繞過護城河策略（核心 v2.0 新增）

v1.0 的 MVP 路徑會撞上四道既有市場護城河。v2.0 不打穿護城河，而是**走物理量的路，護城河保護的那條路根本不走**：

| 護城河 | 誰建的 | v1.0 正面撞 | v2.0 繞法 |
| :--- | :--- | :--- | :--- |
| **金流代收合規**（Stripe Connect 審核 + 台灣金管會第三方支付登記） | Stripe / 金管會 | 平台代使用者收款 | **不代收。** 教使用者自己開帳戶。FirstDollar 碰流程不碰錢 |
| **LINE 生態封閉**（OA 商用審核 + 推播成本 NT$0.2-0.5/則） | LINE | 系統推播紀律層 | **PM 個人 LINE 私訊。** 前 50 人不需要 OA |
| **Offer 模板資料飛輪**（需 ~300 個有金流 Sprint 達 critical mass） | 自身冷啟動 | 需 AI 推薦引擎 | **PM 就是推薦引擎。** 前 50 個 Sprint 人工給建議，累積 pattern 後才系統化 |
| **台灣電商 SaaS**（91APP / Shopline 全套開店工具） | 既有電商平台 | 搶「賣東西的人」 | **只搶「還沒開始賣的人」。** 不同 JTBD：決定要不要開店的紀律 ≠ 開店工具 |

#### 重新定義的 MVP（Phase 0：手工驗證）

| 維度 | v1.0 MVP | v2.0 Phase 0（手工版） |
| :--- | :--- | :--- |
| 產品形態 | 6 大軟體模組 | **一個人 + LINE 私訊 + Google Doc 模板** |
| 金流 | Stripe Connect + TapPay | 使用者自行開 Lemon Squeezy（10 分鐘） |
| 紀律層 | LINE OA + Messaging API | PM 每天親自私訊 ping |
| Offer 推薦 | LLM API（$300-800/月） | PM 親自看受眾資料、手動給建議 |
| 開發時間 | 12 週 | **本週末開始第一個 Sprint** |
| 驗證成本 | ~$500-1,200/月 | **$0**（你的時間） |
| 驗證目標 | 上線收費 | **6 人中 ≥ 2 人真的收到第一筆錢 → 命題成立** |

**Phase 0 時間表**：

| 週次 | 動作 | 過關條件 |
| :--- | :--- | :--- |
| Week 1 | 找到 3 個**真人**（不是 AI persona），免費陪跑 | 3 人同意進入 7-Day Sprint |
| Week 2 | Google Doc 排任務 + 每天 LINE ping + 幫開 Lemon Squeezy | ≥ 1 人發布 landing + 收款連結 |
| Week 3 | 第二批 3 人，**收費 NT$500** | 有人付費 = FirstDollar 自身的 First Dollar |
| Week 4 | 6 人結果評估：≥ 2 人收到首筆錢 → Go；0 人 → Kill | 決策點 |

**Phase 0 → Phase 1 的觸發條件**：Phase 0 驗證成功後，才進入 v1.0 定義的軟體 MVP 開發（見 §4）。Phase 1 的範圍依 Phase 0 學到的 pattern 重新定義。

---

## 1. 專案總覽

| 項目 | 內容 |
| :--- | :--- |
| **專案名稱** | FirstDollar（首單）|
| **Slug** | `firstdollar` |
| **狀態** | 規劃中（PRD v1.0） |
| **目標發布日期** | Phase 0：2026-04-30（手工驗證 4 週）｜ Phase 1：2026-06-30（軟體 MVP，Phase 0 通過後） |
| **核心團隊** | PM: TBD ｜ Lead Engineer: TBD ｜ UX: TBD |
| **一句話定位** | 不評估點子、只逼你在 7 天內拿到第一塊錢的 AI co-founder |
| **North Star Metric** | $ / 週：使用者透過本平台收到的實際付款金額（不是註冊數、不是 DAU） |

---

## 2. 商業目標

| 項目 | 內容 |
| :--- | :--- |
| **背景與痛點** | 台灣與東亞市場有一批 wantrepreneur（indie hacker、電商賣家、Growth PM、創作者、顧問）累積 idea 卻無法 ship。現行 idea-validation SaaS（IdeaCheck、ShipYourIdea、IdeaBrowser）普遍被認為是「焦慮產品」— 交付報告而非結果。使用者真正的痛點是：(1) 不知道怎麼開始驗證、(2) 卡在 30-60% 棄坑、(3) 沒有分發能力、(4) 沒有外部紀律。 |
| **策略契合度** | 承接 `ai_one_person_company_0to1_strategy.md` 的核心觀點：「1 人公司的勝負在把 需求 → 假設 → MVP → 付費驗證 做成一條可重複的流水線」。FirstDollar 就是這條流水線的可執行工具層。 |
| **成功指標** | **Phase 0（4 週）**：6 人中 ≥ 2 人收到首筆真實付款（33%+ 成功率）<br>**Phase 1（Year 1）**：Paying Customer 產生第一筆真實 revenue 的比例 ≥ 25%（相較於行業 2-3%）<br>**次要**：自家 MRR US$10k（month 6）/ US$25k（month 12）；退款率 < 8%；NPS ≥ 40 |
| **差異化護城河** | (1) **North Star = 使用者的錢，不是自家 DAU**；(2) **反焦慮 UX**，禁止 idea score；(3) **人肉紀律層**（Phase 0）→ 系統紀律層（Phase 1）；(4) **不碰錢、不建基礎設施** — 只做使用者自己做不到的事：紀律與陪跑 |

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
| **Phase 0 範圍（手工驗證）** | 1. **PM 人肉 Sprint 陪跑**（Google Doc 任務模板 + LINE 私訊紀律）<br>2. **使用者自開收款連結**（Lemon Squeezy / Stripe 個人帳戶，PM 協助設定）<br>3. **PM 手動 Offer 建議**（看受眾原始資料後人工產出 3 個 offer）<br><br>**Phase 1 功能範圍（Phase 0 驗證通過後）**：<br>1. **7-Day Sprint Engine**（任務編排 + 每日推播 + 紀律層）<br>2. **Landing + Stripe 一鍵發布**（5 個模板 + TapPay 台灣金流）<br>3. **Audience-to-Offer**（受眾原始資料 → 3 個可賣的 offer） |
| **非功能需求** | **性能**：Landing page 發布 TTFB < 200ms、LCP < 2s<br>**安全**：Stripe / TapPay webhook 全程 HMAC 驗證；使用者受眾資料預設不上雲訓練（呼應 David 訴求）<br>**可用性**：99.5% SLA（MVP 階段）；i18n zh-Hant 預設，en 次之<br>**SEO**：所有 landing page 採 Server Component + Structured Data（補 ideacheck 沒做的功課）<br>**無障礙**：WCAG AA；skip-link、ARIA landmarks 齊備 |
| **不做什麼（救命清單）** | 1. **不做 idea scoring** — 這是本產品的 identity，任何 PM / engineer 提議加分數一律駁回<br>2. **不做 AI 生成 PRD / 商業計畫書** — 那是 David 眼中的「結構正確但缺 context 的廢話」<br>3. **不做 App（iOS/Android）** — Web-first，降低一人公司維運成本<br>4. **不做 B2B / Enterprise plan** — 焦點在 solo<br>5. **不做「100 個點子產生器」** — 使用者不缺點子<br>6. **不做訂閱綁約** — 淑芬訊號；影響信任<br>7. **不做 Discord / Slack bot 整合**（v1）— 延後<br>8. **不做模糊的 NPS / engagement 報告** — 只呈現 $ |
| **假設與依賴** | **假設 1**：至少 25% 的活躍使用者願意在 7 天內公開發布 landing 並嘗試收款（**高風險，v1.0 為 AI 模擬結論，必須在 Phase 0 用真人驗證**）<br>**假設 2**：台灣 solo wantrepreneur 的 willingness-to-pay 中位數能支撐 NT$690–1,490/月定價<br>**假設 3**：「人肉紀律層」（PM 私訊 ping）的效果 ≥ 系統推播（Phase 0 驗證）<br>**Phase 0 依賴**：PM 本人的時間、LINE 個人帳號、Google Doc、Lemon Squeezy 免費帳戶<br>**Phase 1 依賴**：Stripe、TapPay、Resend（email）、Supabase（auth + DB）、LLM 供應商（Claude / OpenAI） |
| **定價草案** | **Free**：1 次 Sprint 體驗（無紀律層、含本平台 branding）<br>**Pro** NT$690/月：unlimited Sprint、紀律層、5 個 landing 模板、台幣金流<br>**Coach** NT$1,490/月：+ AI co-founder 深度對話（有記憶）、承諾金機制、1v1 月度 office hour<br>**承諾**：皆可隨時停用、月付為主、年付 7 折 |

---

## 5. 待辦問題與決策

| ID | 描述 | 狀態 | 負責人 |
| :--- | :--- | :--- | :--- |
| Q-001 | 「承諾金扣款」的法務風險 — **v2.0 決策：Phase 0 不做承諾金，延至 Phase 1 評估。** 手工版不涉及預授權扣款，法務風險歸零。 | Phase 0 解除 | PM |
| Q-002 | North Star Metric 追蹤方式 — **v2.0 決策：Phase 0 由 PM 親自確認（看截圖 / 問使用者）。** 不需要 Stripe 串接，也不靠使用者自述。Phase 1 再接 webhook。 | Phase 0 解除 | PM |
| Q-003 | Persona「淑芬」（非技術中年賣家）是 MVP TA 還是 v2 TA？ — **v2.0 建議：Phase 0 先服務有基本技術能力的 persona（阿傑/Vivian/Kai），淑芬延至 Phase 1。** 理由：自開 Lemon Squeezy 對淑芬可能是障礙。 | 建議決定 | PM / UX |
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

**文件版本：** v2.0（草稿）
**建立日期：** 2026-04-09 ｜ **v2.0 更新：** 2026-04-09
**作者：** PM (via AI-assisted multi-persona UX research workflow)
**v2.0 變更摘要：** 經 S1→F→S2 第一性原理壓測，修正 D1–D3 定義漂移；新增 Phase 0 手工驗證階段；繞過金流代收 / LINE OA / Offer Vault / 電商 SaaS 四道護城河；Q-001、Q-002 在 Phase 0 層級解除
**審核狀態：** 待 Product Lead / Design Lead 審閱（Q-003 ~ Q-005）
