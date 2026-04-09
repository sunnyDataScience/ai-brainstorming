# FirstDollar — 策略補遺：牙刷檢驗法 × 護城河 × 飛輪 × 核心模組 × 資源整合

> **版本：** v1.0 ｜ **日期：** 2026-04-09 ｜ **狀態：** 草稿
> **配套文件：** [`firstdollar_prd.md`](./firstdollar_prd.md)
>
> 本文件是 PRD 的策略延伸。PRD 回答「要做什麼」；本文件回答「為什麼這能活、靠什麼滾、需要哪些關鍵資源」。

---

## 0. TL;DR（策略三張牌）

| 維度 | 結論 |
| :--- | :--- |
| **牙刷檢驗** | 當前 PRD 只有 **7 天 Sprint**，通不過牙刷檢驗（用完就走）。必須補上三個 always-on 模組（Daily Card / Revenue Ticker / Audience Signal Feed），才有每日回訪的理由。 |
| **最強護城河** | (1) 真實金流數據 × (2) Offer 模板庫（越多人用越準）× (3) 反 idea-scoring 的品牌立場（競品無法模仿，除非否定自家商業模式） |
| **主飛輪** | **Offer Template Flywheel** — 使用者成功 Sprint → 匿名化 offer → 下次使用者更容易成功 → 更多成功 → 更多模板。這是唯一有規模效應的飛輪。 |
| **必要整合** | Build：Sprint Engine、Offer Vault、Revenue Telemetry、Co-founder Memory ｜ Buy：Stripe / TapPay / Resend / Supabase / LLM API ｜ Partner：LINE OA、創作者 affiliate、台灣金流夥伴 |

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
| **MVP（0-3 月）** | C（Co-founder Memory） | A（Success Story 手動運營） | B 先記錄不推理 |
| **PMF 驗證（3-6 月）** | A + C | 開始 seed B | — |
| **規模化（6-12 月）** | **B（Offer Vault）** | A + C | — |
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

### 4.3 MVP 優先順序（對照 PRD）

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

## 6. 整合優先級總表（依 MVP 交付日 2026-06-30 回推）

| 時間點 | 必須完成 | Build/Buy/Partner | 風險 |
| :--- | :--- | :--- | :--- |
| **Week 1–2** | Supabase 建置、Vercel 部署、Claude API、Resend | Buy | 低 |
| **Week 3–4** | Stripe 主要金流 + Webhook → C4 Revenue Telemetry MVP | Buy + Build | 中（Webhook 驗證複雜） |
| **Week 5–6** | TapPay 在地金流 + LINE OA 申請 | Partner + Buy | **高**（LINE OA 商用審核約 2 週） |
| **Week 7–8** | C1 Sprint Engine + C3 Audience-to-Offer 輕量版（剪貼+CSV） | Build | 中 |
| **Week 9–10** | C2 Landing Builder（5 模板）+ 串 C4 | Build | 中 |
| **Week 11** | C5 Co-founder Memory（最小版）+ 紀律層推播 | Build | 中 |
| **Week 12** | 法務審閱（承諾金 + 隱私條款）+ 10 位 Design Partner 招募完成 | Partner | **高**（法務時程不可控） |
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

### 8.1 策略結論

> FirstDollar 的勝負不在產品功能，而在三個約束是否守得住：
>
> 1. **North Star 只追 $**（別偷偷加註冊數指標）
> 2. **禁止 idea score**（別被客戶要求動搖）
> 3. **Offer Vault 的資料飛輪必須優先於功能擴張**（別急著加功能）

### 8.2 下一步行動（48 小時內）

| # | 動作 | 負責 |
| :--- | :--- | :--- |
| 1 | 將本策略補遺提交 Product Lead 評審 | PM |
| 2 | 啟動 LINE OA 商用帳號申請（Week 5–6 前必須完成） | PM + BD |
| 3 | 啟動台灣法務諮詢（承諾金 + 隱私條款） | PM + Legal |
| 4 | 列出前 10 位 Design Partner 候選名單 | PM |
| 5 | 建立 Seed Offer 收集腳本與 30 份 seed 模板 | PM |
| 6 | PRD `Q-001` ~ `Q-005` 決策會議排程 | PM |

---

**文件版本：** v1.0（草稿）
**建立日期：** 2026-04-09
**配套：** PRD v1.0（`firstdollar_prd.md`）
**審核需求：** Product Lead、Legal、Lead Engineer、UX Lead
