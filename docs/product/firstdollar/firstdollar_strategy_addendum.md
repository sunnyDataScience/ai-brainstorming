# FirstDollar — 策略補遺：牙刷檢驗法 × 護城河 × 飛輪 × 核心模組 × 資源整合

> **版本：** v2.0 ｜ **日期：** 2026-04-09 ｜ **狀態：** 草稿
> **配套文件：** [`firstdollar_prd.md`](./firstdollar_prd.md)（v2.0）
>
> 本文件是 PRD 的策略延伸。PRD 回答「要做什麼」；本文件回答「為什麼這能活、靠什麼滾、需要哪些關鍵資源」。
>
> **v2.0 重大變更：** 經第一性原理壓力測試（S1→F→S2），護城河策略從「建造護城河」轉為「繞過既有護城河」。新增 §2.5 護城河繞行策略、§4.4 Phase 0 手工模組定義。整合 `socratic_first_principles_rnd_workflow.md` 與 `first_principles_playbook.md` §2 物理量的檢驗結果。

---

## 0. TL;DR（策略三張牌）

| 維度 | 結論 |
| :--- | :--- |
| **牙刷檢驗** | 當前 PRD 只有 **7 天 Sprint**，通不過牙刷檢驗（用完就走）。必須補上三個 always-on 模組（Daily Card / Revenue Ticker / Audience Signal Feed），才有每日回訪的理由。**但 Phase 0 不需要通過牙刷檢驗 — 先驗證命題再談留存。** |
| **護城河策略（v2.0 修正）** | **不建護城河，繞護城河。** 不碰金流代收（避開金管會）、不做 LINE OA 系統推播（PM 親自 ping）、不建 AI 推薦（PM 就是推薦引擎）。Phase 0 唯一的護城河 = 反 idea-scoring 品牌立場（M3）+ PM 的人肉投入 |
| **主飛輪（v2.0 修正）** | Phase 0：**Human Sprint Flywheel** — PM 陪跑 → 學到 pattern → 下次陪跑更有效 → 成功率上升 → 口碑帶來新使用者。Phase 1+：轉為 Offer Template Flywheel（系統化） |
| **必要整合（v2.0 修正）** | **Phase 0**：PM 的時間、LINE 個人帳號、Google Doc、Lemon Squeezy 免費帳戶 ｜ **Phase 1**：Build（Sprint Engine、Offer Vault、Revenue Telemetry）｜ Buy（Stripe / TapPay / Resend / Supabase / LLM API）｜ Partner（LINE OA、創作者 affiliate） |

---

## 1. 牙刷檢驗法分析（Toothbrush Test）

> **Larry Page 原題**：這個產品是使用者每天會用 1-2 次、且讓他們生活更好的東西嗎？

### 1.1 PRD 目前通不過的診斷

PRD 核心是 **7-Day Sprint Engine**。Sprint 本質是「高強度、短週期、用完即走」的產品形態 — 跟「每日使用」矛盾。

| 牙刷檢驗子問題 | 目前 PRD 答案 | 問題 |
| :--- | :--- | :--- |
| 使用者每天會打開嗎？ | Sprint 期間會（7 天），結束後不會 | 失敗 |
| 讓他們生活更好嗎？ | 只在 Sprint 期間；結束後回到原狀 | 部分 |
| 沒有它會想念嗎？ | 除非正在跑 Sprint，否則不會 | 失敗 |

### 1.2 解法：Sprint 之外必須有 Always-on 的三個每日鉤子

| 鉤子 | 每日動作 | 頻率 | 為什麼是牙刷 |
| :--- | :--- | :--- | :--- |
| **Daily Task Card** | 早上打開看今日 1 個任務 | Sprint 期間 1×/day ｜ Sprint 間隙 1×/week | 像日曆/待辦，建立習慣 |
| **Revenue Ticker** | 看 `$ This Week`、累計 $、上次收款時間 | 3–5×/day（像看股價） | 數字多巴胺、高回訪動機 |
| **Audience Signal Feed** | 系統主動推「今天你的留言 / 訊息裡有 3 個可能的 offer」 | 1–2×/day（早 + 晚） | 主動提供價值、取代焦慮滑 X 的行為 |

### 1.3 設計原則

- **Daily Task Card 不能變 Todo List**：一天只顯示 1 件事，不讓使用者「累積未完成」（反焦慮）
- **Revenue Ticker 必須顯示絕對值 + 上次收款時間**：零收入時顯示「你的下一塊錢離你 1 個動作」而不是空狀態
- **Audience Signal Feed 必須先得到原始資料**：這是設計難點 — 使用者要授權資料來源（見 §5 整合）

### 1.4 檢驗結論

> 補上三個 always-on 模組後，FirstDollar 從「7 天衝刺工具」→「每日創業儀表板 + 週期性衝刺引擎」。通過牙刷檢驗。

---

## 2. 護城河分析（Moat）

### 2.1 競品護城河盤點

| 競品 | 護城河強度 | 來源 |
| :--- | :--- | :--- |
| IdeaCheck / ShipYourIdea | 極弱 | 僅為 LLM wrapper + landing 包裝；任何人 1 週可複製 |
| IdeaBrowser | 弱—中 | Reddit 資料擷取 + 趨勢分析；資料源可被取代 |
| Gummysearch | 中 | 深度整合 Reddit API + 長期資料 |
| Lovable / Bolt / v0 | 弱 | 同為 LLM wrapper，靠 DX 勝出，無鎖定效應 |

**結論**：整個賽道沒有真正護城河。FirstDollar 有機會建立不可模仿的立場。

### 2.2 FirstDollar 可建立的五種護城河

| # | 護城河類型 | 建立方式 | 強度預估 | 建立時間 |
| :--- | :--- | :--- | :--- | :--- |
| **M1** | **資料護城河 — Offer Template Vault** | 使用者 Sprint 成功後匿名化 offer → 累積成模板庫 → 新使用者得到「像你這樣的人上週做的成功 offer」 | ⭐⭐⭐⭐⭐ | 需 6 個月達 critical mass（~300 個有金流的 sprint） |
| **M2** | **資料護城河 — Revenue Ground Truth** | 唯一能追蹤「真實金流」的平台（透過 Stripe / TapPay webhook）→ 可訓練「什麼 offer 真的賺錢」模型 | ⭐⭐⭐⭐⭐ | 12 個月 |
| **M3** | **品牌 / 立場護城河** | 「反 idea scoring」的 positioning — 競品若模仿即否定自己商業模式 | ⭐⭐⭐⭐ | 上線即生效 |
| **M4** | **工作流鎖定護城河** | Landing hosting、Stripe 串接、歷史 Sprint 記錄、AI co-founder 對話記憶 → 離開成本高 | ⭐⭐⭐ | 3 個月 |
| **M5** | **分發護城河 — 創作者合作網絡** | 與 Kai 類創作者建立 affiliate 與 case study 循環 → 競品買不到同樣的真實案例 | ⭐⭐⭐ | 6 個月 |

### 2.3 護城河組合戰略

- **短期（0–6 個月）**：靠 M3（品牌立場）+ M4（工作流鎖定）先守住
- **中期（6–12 個月）**：啟動 M1（Offer Vault）+ M5（創作者網絡）
- **長期（12 個月+）**：M2（Revenue Ground Truth）進入難以被追上的資料優勢

### 2.4 反指標 — 會弱化護城河的決策

| 決策 | 為什麼不能做 |
| :--- | :--- |
| 加 idea score 功能（即使客戶要求） | 直接破壞 M3 |
| 把 Offer Vault 公開免費（SEO 誘惑） | 直接破壞 M1 |
| 允許使用者 export 所有資料後離開無 friction | 削弱 M4，但完全禁止會傷害信任 → 需設計平衡 |
| 接受 Enterprise 大單改客製 | 稀釋 PM 注意力，延緩 M1/M2 累積 |

### 2.5 護城河繞行策略（v2.0 新增 — S1→F→S2 壓測結果）

> **核心洞察**：v1.0 的 MVP 路徑正面撞上四道既有護城河。經 `first_principles_playbook.md` §2 物理量檢驗，發現這四道護城河保護的是**工具層**（金流代收、系統推播、AI 模板庫、電商開店），而非**物理量層**（具體的人、付錢的痛、手工交付、錢的管道）。走物理量的路，護城河根本不在路上。

#### 四道護城河的繞行路徑

| # | 護城河 | 持有者 | 保護的是什麼 | 物理量真正需要的 | v2.0 繞法 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **B1** | 金流代收合規 | Stripe / 金管會 | 「平台代使用者收款」 | 「使用者自己能收到錢」 | **不代收。** 教使用者自開 Lemon Squeezy / Stripe（10 分鐘）。FirstDollar 碰流程不碰錢。零法規門檻 |
| **B2** | LINE 生態封閉 | LINE | 「系統主動 ping 使用者」的通路 | 「外部紀律讓使用者不棄坑」 | **PM 個人 LINE 私訊。** 前 50 人不需要 OA、不需要 Messaging API、不需要推播費用。對話品質反而更高 |
| **B3** | Offer 模板資料飛輪 | 自身冷啟動 | 「什麼 offer 賣得動」的 AI 推薦 | 使用者知道「下一步做什麼」 | **PM 就是推薦引擎。** 前 50 個 Sprint 手動看受眾資料、手動給建議。累積 pattern 後才系統化為 Offer Vault |
| **B4** | 台灣電商 SaaS | 91APP / Shopline | 「已經在賣東西的人」的全套工具 | 「還沒開始賣的人」踏出第一步 | **不搶已有店的人。** 91APP 是開店工具，FirstDollar 是「決定要不要開店」的紀律。不同 JTBD |

#### 繞行策略的壓力測試（S2）

| 假設 | 壓測問題 | 結論 |
| :--- | :--- | :--- |
| 使用者自開 Lemon Squeezy 就能收款 | 淑芬（非技術）能自己開嗎？ | Phase 0 先服務有基本技術能力的 persona；淑芬延至 Phase 1 |
| PM 親自 ping 前 50 人 | 50 人 × 5 分鐘/天 = 250 分鐘/天，能 scale 嗎？ | 不能 scale，但不需要。Phase 0 目標是驗證 25% 成功率，不是服務 1000 人 |
| PM 手動給 offer 建議 | 如果 PM 比 AI 準，AI 版本就不是核心價值？ | 正確。真正驗證的是「有人逼你、陪你跑 7 天」這件事本身有沒有用。技術只是放大器 |
| 不碰錢就無法追蹤 Revenue Ground Truth | 長期 M2 護城河還能建嗎？ | Phase 0 由 PM 人工確認（截圖 / 對話）。Phase 1 再接 Stripe webhook。資料護城河延後但不放棄 |

#### 繞行策略的「回到正面」觸發條件

Phase 0 驗證成功後，依序恢復正面建設：

| 觸發條件 | 恢復動作 | 對應護城河 |
| :--- | :--- | :--- |
| ≥ 6 個成功 Sprint + 穩定 pattern | 建 Offer Vault、開始系統化 | M1 |
| 50+ 活躍使用者、PM 時間不夠 ping | 申請 LINE OA、建系統推播 | M4 |
| 100+ 使用者、有 Stripe 串接需求 | 評估 Stripe Connect / TapPay 商戶申請 | M2 |
| 品牌認知建立、有創作者主動聯繫 | 啟動 Creator Partnership | M5 |

---

## 3. 產品迭代飛輪（Flywheel）

### 3.1 三個候選飛輪

#### 飛輪 A — Success Story Flywheel（線性）

```
使用者拿到第一筆錢
  ↓
產生真實 $ 案例（非造假截圖）
  ↓
轉為 marketing content 與 social proof
  ↓
吸引更多 wantrepreneur 註冊
  ↓
更多 Sprint → 更多成功案例
```

**特性**：線性、需手動運營、無網絡效應。**屬於行銷輪，非護城河輪**。

#### 飛輪 B — Offer Template Flywheel（主飛輪 ⭐）

```
使用者 Sprint → 產生 offer（含 $ 結果）
  ↓
匿名化後進入 Offer Vault
  ↓
AI 學習「什麼 offer × 什麼受眾 × 什麼分發 = 成交」
  ↓
新使用者開 Sprint 時得到更準的 offer 建議
  ↓
更多使用者首次成交
  ↓
更多 offer 進 Vault（飛輪加速）
```

**特性**：越多使用者 → 產品越強 → 對後進者價值遞增。**有規模效應，是真護城河**。

#### 飛輪 C — Co-founder Memory Flywheel（個人層）

```
AI co-founder 對話 → 累積使用者 context
  ↓
下次 ping 更精準
  ↓
使用者更願意分享私密資料（audience / 收入）
  ↓
context 更豐富
  ↓
對話品質再提升 → switching cost ↑
```

**特性**：個別使用者層面的鎖定，不具備群體網絡效應，但能大幅降低流失率。**屬於 retention 輪**。

### 3.2 飛輪優先級

| 階段 | 主飛輪 | 支援飛輪 | 放棄 |
| :--- | :--- | :--- | :--- |
| **Phase 0（0-1 月）手工驗證** | **Human Sprint Flywheel**（PM 陪跑 → 學 pattern → 下次更有效 → 口碑） | A（手動成功案例分享） | B + C 不啟動 |
| **Phase 1 MVP（1-4 月）** | C（Co-founder Memory） | A（Success Story 手動運營） | B 先記錄不推理 |
| **PMF 驗證（4-7 月）** | A + C | 開始 seed B | — |
| **規模化（7-12 月）** | **B（Offer Vault）** | A + C | — |
| **成熟（12 月+）** | B | Revenue Ground Truth model | — |

### 3.3 飛輪的斷點風險

| 飛輪 | 斷點 | 緩解 |
| :--- | :--- | :--- |
| A | 使用者不願公開 = 無案例 | 匿名成功案例 + 金額區間公開（不揭露身份） |
| B | 冷啟動無足量 offer 資料 | 初期 PM 手動 curate 30–50 個 seed offer（含真實金流） |
| C | 使用者擔心隱私 = 不願分享 audience data | 明確承諾 local-first / 不上雲訓練 / 可隨時刪除 |

---

## 4. 主力核心模組（Core Modules）

### 4.1 六大模組 × 對應護城河 × 對應飛輪

| # | 模組 | 職責 | 護城河 | 飛輪 | Build/Buy |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **C1** | **Sprint Engine** | 7 天任務編排、進度追蹤、紀律層（主動 ping、承諾金） | M4 | C | **Build** |
| **C2** | **Landing & Checkout Builder** | 5 個 landing 模板、Stripe/TapPay 一鍵串接、部署到 *.firstdollar.app 或自訂網域 | M4 | — | Build + Buy（金流 SDK） |
| **C3** | **Audience-to-Offer** | 受眾原始資料擷取（剪貼 / CSV / API）→ LLM 萃取 → 產出 3 個可賣 offer | M1 seed | B | **Build**（核心 IP） |
| **C4** | **Revenue Telemetry** | 追蹤 Stripe/TapPay webhook → 計算 $ / 週 → 驅動 Dashboard 與 North Star | M2 | B | Build（需金流整合） |
| **C5** | **AI Co-founder Memory** | 使用者對話、Sprint 決策、卡點紀錄的長期記憶層（pgvector） | M1 | C | **Build**（核心 IP） |
| **C6** | **Offer Template Vault** | 成功 Sprint 的匿名化 offer 資料庫；提供給新使用者的「類似你的人怎麼做」推薦 | **M1 + M2** | **B** | **Build**（長期 moat） |

### 4.2 模組依賴圖

```
                 ┌──────────────────┐
                 │ C1 Sprint Engine │◀──────┐
                 └─────┬────────────┘       │
                       │ 編排                │ 紀律 ping
                       ▼                     │
    ┌──────────────────┬───────────────┐    │
    │                  │               │    │
    ▼                  ▼               ▼    │
┌────────┐      ┌────────────┐   ┌───────────────┐
│C3 A2O  │      │C2 Landing &│   │C5 Co-founder  │
│(Audience│◀───▶│  Checkout  │   │   Memory      │
│to Offer)│     └─────┬──────┘   └───────────────┘
└────┬───┘            │ 金流 webhook     ▲
     │                ▼                   │ context
     │          ┌─────────────┐           │
     │          │C4 Revenue   │───────────┘
     │          │  Telemetry  │
     │          └──────┬──────┘
     │                 │ $ 確認 + offer 結果
     ▼                 ▼
┌────────────────────────────┐
│  C6 Offer Template Vault    │ ← 主護城河 / 主飛輪
└────────────────────────────┘
```

### 4.3 Phase 0 手工模組定義（v2.0 新增）

> **原則**：Phase 0 的每個「模組」都是 PM 本人執行的動作，不是軟體。目的是用最低成本驗證「7-Day Sprint 陪跑能讓人收到第一筆錢」這個命題。

| # | 手工模組 | PM 做什麼 | 工具 | 對應 Phase 1 軟體模組 |
| :--- | :--- | :--- | :--- | :--- |
| **H1** | 手工 Sprint 編排 | 用 Google Doc 模板為每位使用者排 Day 1–7 任務 | Google Doc | C1 Sprint Engine |
| **H2** | 手工紀律層 | 每天 LINE 私訊 ping「今天做了嗎？卡哪裡？」+ 深度對話 | LINE 個人帳號 | C1 紀律層 + C5 Co-founder Memory |
| **H3** | 手工 Offer 建議 | 看使用者貼來的留言/訊息，手動產出 3 個 offer 建議 | 人腦 + Google Doc | C3 Audience-to-Offer |
| **H4** | 協助開收款連結 | 教使用者自己開 Lemon Squeezy，必要時螢幕共享 | Lemon Squeezy / Stripe（使用者帳戶） | C2 Landing & Checkout |
| **H5** | 手工 Revenue 確認 | 問使用者「收到錢了嗎？」看截圖確認 | LINE 對話 | C4 Revenue Telemetry |
| **H6** | 手工 Pattern 記錄 | 每個 Sprint 結束後記錄「什麼有效 / 什麼沒效」到 Notion | Notion | C6 Offer Vault |

### 4.4 Phase 1 軟體模組優先順序（Phase 0 通過後）

| 優先 | 模組 | 理由 |
| :--- | :--- | :--- |
| **P0** | C1 + C2 + C4 | 使使用者能「跑 Sprint → 發 landing → 收 $」閉環 |
| **P0** | C3（輕量版：只剪貼 + CSV） | 讓使用者有「下一步動作」輸入源 |
| **P1** | C5（最小版：單 Sprint 對話記憶） | 紀律層需要它 |
| **P2** | C6（資料庫先收，推理後做） | Vault 先累積資料，推薦功能 v1.1 再出 |

---

## 5. 必要資源與整合（Build / Buy / Partner 決策表）

### 5.1 技術基礎設施（Buy — 不自建）

| 類別 | 供應商選擇 | 月成本估計（MVP） | 備註 |
| :--- | :--- | :--- | :--- |
| **Frontend / Hosting** | Vercel Pro | $20 × 人 | Next.js 原生支援、Edge + Cron |
| **Database** | Supabase（Postgres + pgvector + Auth + Storage） | $25 Pro | 一站式降低維運；pgvector 給 C5 |
| **LLM — 主力對話** | Anthropic Claude Sonnet 4.6 | 用量計費（估 $300–800/月） | C3 + C5 主要推理 |
| **LLM — 高頻輕量** | Anthropic Claude Haiku 4.5 | 用量計費（估 $50–150/月） | C1 任務生成、Daily Card 排程 |
| **Email** | Resend | $20 | 紀律層推播 |
| **Scheduling / Cron** | Vercel Cron（MVP）→ Upstash QStash（規模後） | $10–30 | 紀律層 24hr 檢查 |
| **Analytics** | PostHog Cloud | $0–50 | 隱私友善、可自 host |
| **Error tracking** | Sentry | $26 | 金流相關必備 |

**MVP 月度技術成本**：**約 $500–1,200 USD/月**

### 5.2 金流與支付整合（Buy — 核心）

| 整合 | 角色 | 必要性 | 備註 |
| :--- | :--- | :--- | :--- |
| **Stripe** | 國際金流、訂閱、Connect（代使用者收款） | **P0** | 核心。C4 Revenue Telemetry 依賴 webhook |
| **TapPay** | 台灣信用卡、Line Pay、Apple Pay | **P0** | 在地化關鍵；無它則淑芬 persona 流失 |
| **NewebPay / 綠界** | 備援金流 | P2 | 僅在 TapPay 有中斷風險時接 |
| **Stripe Connect Express** | 代使用者收款並抽成 | P1 | 商業模式若走「每筆抽 X%」才需要 |

**策略決策**：MVP 採雙金流（Stripe + TapPay）並行，使用者可選。這是相對 IdeaCheck 的**真實在地化**差異化點。

### 5.3 通訊與紀律層整合（Partner + Buy）

| 整合 | 角色 | 必要性 | 決策 |
| :--- | :--- | :--- | :--- |
| **Resend**（Email） | 基礎推播 | **P0** | Buy |
| **LINE Official Account Messaging API** | 台灣使用者主要通訊渠道 | **P0** | **Partner**（需申請 LINE OA + Messaging API 商用帳號） |
| **Telegram Bot** | 技術 persona（阿傑）偏好 | P1 | Buy（免費 API） |
| **SMS — Twilio** | 承諾金扣款前的最後通知 | P2 | Buy |
| **Browser Push** | 桌面使用者 | P1 | Build（Web Push API） |

**關鍵洞察**：在台灣，沒有 LINE = 失敗一半。這是 IdeaCheck / ShipYourIdea 可能缺少的在地整合，**是真實差異化點**。

### 5.4 受眾資料來源整合（C3 核心）

| 資料源 | MVP 策略 | 長期策略 |
| :--- | :--- | :--- |
| **剪貼簿貼上（raw text）** | ✅ P0 | 保留 |
| **CSV / Excel upload** | ✅ P0 | 保留 |
| **IG Business Account（私訊 + 留言）** | P1 | Instagram Graph API（需 Facebook Business 認證） |
| **YouTube Data API v3（留言）** | P1 | 官方 API，門檻低 |
| **Discord Bot**（社群訊息擷取） | P2 | OAuth + Bot |
| **Notion / Airtable API** | P2 | 使用者筆記來源 |
| **Gmail / Email forwarding** | P2 | SES inbound 或 CloudMailin |
| **Slack workspace** | P3 | 多為團隊工具，solo 用途少 |

**MVP 鐵律**：**先只支援「剪貼 + CSV」**。任何 OAuth 整合都延後，因為每個整合都消耗審核時間（IG / YT Business API 審核各 2–4 週），會拖垮 PMF 驗證節奏。

### 5.5 內容 / 社群 / 信任資源（Build + Partner）

| 資源 | 角色 | 決策 | 優先級 |
| :--- | :--- | :--- | :--- |
| **Landing page 案例庫**（真實使用者成功案例） | 推動飛輪 A | Build + 手動運營 | P0 |
| **Creator Partnership Program** | 與 Kai 類 YouTuber 簽 affiliate + 真心業配合作 | **Partner**（前 5 位創作者提供 lifetime free + 50% rev share） | P1 |
| **Private Discord / LINE 社群** | 同儕紀律層（peer accountability） | Build | P1 |
| **七日 Sprint Case Study Content Pipeline** | 每週產出 1 篇真實案例分析 | Build + 手動 | P0 |
| **Weekly Office Hour**（Coach tier 用戶） | 與 PM 直接 1v1 互動 | Build + 時間投入 | P2 |

### 5.6 法遵與隱私資源（Partner — 不可省）

| 資源 | 角色 | 急迫性 |
| :--- | :--- | :--- |
| **台灣法務諮詢**（承諾金扣款合規性） | PRD Q-001 直接依賴 | **MVP 上線前必須完成** |
| **個資法 / GDPR 隱私權政策** | 資料護城河承諾的法律基礎 | MVP 上線前 |
| **Stripe / TapPay 商戶協議審閱** | 代使用者收款涉及金融監理 | P0 |
| **AI 不上雲訓練承諾**的 DPA（Data Processing Agreement） | David persona 的信任底線 | P0 |

### 5.7 冷啟動種子資源（Seed Resources — 最容易被低估）

| 資源 | 為什麼需要 | 數量 | 負責 |
| :--- | :--- | :--- | :--- |
| **Seed Offer 模板**（30–50 個含真實金流結果的 offer） | C6 Offer Vault 冷啟動 | 30–50 | PM 手動 curate + 早期使用者同意 |
| **10 位 Design Partner** | PMF 驗證 + 產生第一批真實案例 | 10 | PM 1v1 招募 |
| **3 位創作者合作夥伴**（Kai 類） | 分發護城河 M5 啟動 | 3 | BD |
| **50 筆真實訪談腳本** | C3 Audience-to-Offer 的 few-shot 範例 | 50 | PM + 早期使用者 |

**警告**：這部分常被工程團隊低估。冷啟動種子資源的累積速度決定飛輪啟動時機。

---

## 6. 整合優先級總表（v2.0：Phase 0 + Phase 1）

### 6.1 Phase 0 時間表（2026-04-09 起，4 週）

| 時間點 | 必須完成 | 需要什麼 | 風險 |
| :--- | :--- | :--- | :--- |
| **Week 1** | 找到 3 位真人、準備 Google Doc Sprint 模板 | PM 的社群人脈 + Google Doc | 低（找不到人 = 命題本身有問題） |
| **Week 2** | 第一批 3 人 Sprint 進行中、每天 LINE ping | PM 時間（~90 min/天） | 中（使用者棄坑） |
| **Week 3** | 第一批結果評估 + 招募第二批 3 人（收 NT$500） | Lemon Squeezy（PM 自己收費用） | 低 |
| **Week 4** | 6 人結果評估 → Go/Kill 決策 | PM 判斷 | **關鍵決策點** |

**Phase 0 總成本：$0**（僅 PM 時間）

### 6.2 Phase 1 時間表（Phase 0 通過後，依 2026-06-30 回推）

| 時間點 | 必須完成 | Build/Buy/Partner | 風險 |
| :--- | :--- | :--- | :--- |
| **Week 1–2** | Supabase 建置、Vercel 部署、Claude API、Resend | Buy | 低 |
| **Week 3–4** | Stripe 主要金流 + Webhook → C4 Revenue Telemetry MVP | Buy + Build | 中（Webhook 驗證複雜） |
| **Week 5–6** | TapPay 在地金流 + LINE OA 申請 | Partner + Buy | **高**（LINE OA 商用審核約 2 週） |
| **Week 7–8** | C1 Sprint Engine + C3 Audience-to-Offer 輕量版（剪貼+CSV） | Build | 中 |
| **Week 9–10** | C2 Landing Builder（5 模板）+ 串 C4 | Build | 中 |
| **Week 11** | C5 Co-founder Memory（最小版）+ 紀律層推播 | Build | 中 |
| **Week 12** | 法務審閱（承諾金 + 隱私條款）+ Design Partner 擴招 | Partner | **高**（法務時程不可控） |
| **Week 13+** | Private Beta 啟動、C6 開始記錄資料（不推理） | Build + 運營 | — |

---

## 7. 關鍵放棄清單（Strategic No）

| 放棄 | 理由 | 影響 |
| :--- | :--- | :--- |
| MVP 不做 iOS/Android App | 一人公司維運成本過高 | 損失部分 always-on 場景（用 LINE OA 補） |
| MVP 不做 OAuth 資料整合（IG/YT/Discord） | 審核拖垮節奏 | C3 僅靠剪貼 + CSV；Kai persona 體驗打折 |
| MVP 不做 B2B / Team plan | 稀釋 solo focus | 放棄部分 TAM |
| MVP 不做 idea score / 任何抽象評分 | 破壞品牌護城河 | 放棄「看起來專業」的短期轉換率 |
| MVP 不做多語系（除 zh-Hant 外） | 聚焦台灣在地化護城河 | 放棄國際市場；v1.1 再開 en |
| MVP 不做自訂 LLM / fine-tuning | 成本高、效果未證 | 接受供應商鎖定風險（用 prompt 工程補） |
| MVP 不做 Offer Vault 推薦功能 | 資料未到 critical mass | 先累積資料；v1.1 才開 AI 推薦 |

---

## 8. 結論與下一步

### 8.1 策略結論（v2.0 修正）

> FirstDollar 的勝負不在產品功能，而在四個約束是否守得住：
>
> 1. **North Star 只追 $**（別偷偷加註冊數指標）
> 2. **禁止 idea score**（別被客戶要求動搖）
> 3. **Phase 0 先驗證命題，不寫程式**（別掉進「先建系統再找客戶」的反模式）
> 4. **繞護城河，不撞護城河**（別把基礎設施誤認成產品）

### 8.2 下一步行動 — Phase 0 啟動（48 小時內）

| # | 動作 | 負責 | 備註 |
| :--- | :--- | :--- | :--- |
| 1 | **找到 3 位真人**：從自己的社群中找到願意被陪跑 7 天的人 | PM | 不是 AI persona，是「現在就能打電話」的人 |
| 2 | **準備 Google Doc Sprint 模板**：Day 1–7 任務卡 | PM | 基於 PRD 附錄 B，簡化為手工版 |
| 3 | **自己開一個 Lemon Squeezy 帳戶**：測試流程，確認 10 分鐘可完成 | PM | 確保能教使用者操作 |
| 4 | **定義 Phase 0 成功標準**：6 人中 ≥ 2 人收到首筆錢 = Go | PM | 寫入決策紀錄 |
| 5 | PRD `Q-003` ~ `Q-005` 內部對齊（Q-001、Q-002 已在 Phase 0 層級解除） | PM | — |

**刻意不做（Phase 0 期間）**：

| 不做 | 理由（對應 playbook 反模式） |
| :--- | :--- |
| 不寫任何程式碼 | 反模式 C「技術自瀆」— 第一個付費客戶前不寫 code |
| 不申請 LINE OA | 繞行策略 B2 — PM 個人 LINE 就夠 |
| 不做法務諮詢 | Phase 0 不碰錢、不做承諾金，無法務風險 |
| 不設計 UI / Landing | 反模式 B「PowerPoint 現實」— Google Doc 就是產品 |
| 不選技術棧 | 反模式 C — Phase 0 沒有技術棧 |

---

**文件版本：** v2.0（草稿）
**建立日期：** 2026-04-09 ｜ **v2.0 更新：** 2026-04-09
**配套：** PRD v2.0（`firstdollar_prd.md`）
**v2.0 變更摘要：** 新增 §2.5 護城河繞行策略、§4.3 Phase 0 手工模組、§6.1 Phase 0 時間表；修正飛輪優先級（Phase 0 = Human Sprint Flywheel）；修正下一步行動為 Phase 0 啟動清單
**審核需求：** Product Lead（Phase 0 無需 Legal / Lead Engineer — 不碰錢、不寫 code）
