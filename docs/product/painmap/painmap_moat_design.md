# PainMap — 護城河設計：行業痛點圖譜 × 資料結構 × 冷啟動 × 飛輪

> **版本：** v1.0 ｜ **日期：** 2026-04-09 ｜ **狀態：** 草稿
> **配套文件：** [`painmap_prd.md`](./painmap_prd.md)、[`painmap_disruption_framework.md`](./painmap_disruption_framework.md)
>
> 本文件回答：PainMap 的護城河到底是什麼？怎麼建？需要多久？會怎麼壞？

---

## 0. TL;DR

| 維度 | 結論 |
| :--- | :--- |
| **主護城河** | **Pain Atlas（行業痛點圖譜）** — 使用者結構化的痛點匿名化後累積成跨行業知識庫。越多人用 → 圖譜越準 → 新人越容易找到好題目 → 更多人用。這是 IdeaCheck 類產品永遠做不到的。 |
| **冷啟動策略** | 三階段：(1) PM 手動 curate 200 條種子痛點 (2) 10 位 Design Partner 貢獻真實痛點 (3) Public Beta 啟動自然飛輪 |
| **飛輪啟動時機** | 預估 6 個月達 critical mass（~1,000 條經驗證痛點）。啟動前靠品牌護城河（反 idea score）和工具鎖定守住。 |
| **最大風險** | 使用者不願貢獻痛點到公共圖譜（隱私疑慮）→ 緩解：匿名化 + opt-in + 可撤回 + 貢獻者優先看到新痛點 |

---

## 1. 護城河全景分析

### 1.1 PainMap 可建立的五種護城河

| # | 護城河類型 | 建立方式 | 強度 | 建立時間 | 與 FirstDollar 護城河的關係 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **M1** | **資料護城河 — Pain Atlas** | 使用者結構化痛點 → 匿名化 → 累積成行業痛點圖譜 → 新使用者得到「這個行業已有 X 人驗證過這類痛點」 | ★★★★★ | 6 個月達 critical mass | 與 FirstDollar Offer Vault 互補：PainMap 收「問題端」資料，FirstDollar 收「解法端」資料 |
| **M2** | **資料護城河 — 驗證狀態追蹤** | 痛點條目附帶驗證狀態（未驗證 / 有訪談 / 有付費訊號），追蹤來自 FirstDollar 的金流回饋 | ★★★★★ | 12 個月 | 依賴 FirstDollar Revenue Telemetry 回傳驗證結果 |
| **M3** | **品牌護城河 — 反 idea score** | 「我們不打分，我們幫你看清問題」的 positioning。競品模仿 = 否定自己的商業模式 | ★★★★ | 上線即生效 | 與 FirstDollar 共享同一品牌基因 |
| **M4** | **知識鎖定護城河** | 使用者的結構化痛點庫、問題物理量畫布、GTM 策略歷史 → 離開成本高 | ★★★ | 3 個月 | 與 FirstDollar Sprint 歷史互鎖 |
| **M5** | **網絡護城河 — 行業專家貢獻** | David 類行業專家持續貢獻高品質痛點分析 → 形成「行業知識的 Wikipedia」效應 | ★★★★ | 12 個月 | 獨立於 FirstDollar |

### 1.2 護城河組合戰略

```
Phase 0（上線前）    ：M3 品牌立場（反 idea score 宣言）
Phase 1（0–6 月）    ：M3 + M4（品牌 + 工具鎖定）守住早期使用者
Phase 2（6–12 月）   ：啟動 M1（Pain Atlas 達 critical mass）
Phase 3（12 月+）    ：M1 + M2 + M5（資料 + 驗證 + 專家網絡）形成不可追上的壁壘
```

### 1.3 反指標 — 會弱化護城河的決策

| 決策 | 為什麼不能做 |
| :--- | :--- |
| 加 idea score（即使客戶要求） | 直接破壞 M3 |
| 把 Pain Atlas 完全公開免費 | 直接破壞 M1（需要 freemium 平衡：前 10 條免費，完整需訂閱） |
| 不做匿名化就上架 | 破壞使用者信任 → 貢獻率歸零 → 飛輪斷裂 |
| 允許 bulk export 所有圖譜資料 | 削弱 M4，但完全禁止傷信任 → 設計：可 export 自己的，不可 export 別人的 |
| 追求圖譜數量犧牲品質 | 低品質條目會劣幣驅逐良幣，破壞圖譜信任度 |

---

## 2. Pain Atlas 資料結構設計

### 2.1 核心資料模型

```
PainEntry（痛點條目）
├── id: UUID
├── created_at: timestamp
├── updated_at: timestamp
├── contributor_id: UUID (anonymous reference)
├── status: enum [draft | structured | verified_interview | verified_payment]
│
├── problem_definition（問題定義）
│   ├── essence: string           # 問題本質一句話（≤ 100 字）
│   ├── jtbd: string              # JTBD 格式：「當 [誰] 在 [情境]，想要 [動機]，好讓 [結果]」
│   └── raw_signal: text          # 原始痛點素材（匿名化後）
│
├── physical_quantities（物理量檢驗）
│   ├── specific_people: enum [absent | claimed | verified]
│   ├── paying_pain: enum [absent | claimed | verified]
│   ├── manual_deliverable: enum [absent | claimed | verified]
│   └── payment_rail: enum [absent | claimed | verified]
│
├── industry_context（行業上下文）
│   ├── industry_tags: string[]   # 行業標籤（多選）
│   ├── target_audience: string   # TA 描述
│   ├── current_solutions: Solution[]  # 現行替代方案
│   └── market_segment: enum [b2c | b2b | b2b2c | creator_economy | ecommerce | saas | service]
│
├── disruption_analysis（破壞式分析，optional）
│   ├── overserved_segment: string    # 被過度服務的客群
│   ├── low_end_entry: string         # 低端切入方案
│   ├── strategy_canvas: JSON         # Strategy Canvas 資料
│   └── unit_economics: UnitEcon      # 每單收入-成本框算
│
├── verification（驗證資訊）
│   ├── interview_count: int          # 訪談次數
│   ├── payment_signal: boolean       # 是否有付費訊號
│   ├── payment_amount_range: enum [none | <500 | 500-2000 | 2000-5000 | >5000]  # 金額區間（非精確值）
│   └── firstdollar_sprint_id: UUID?  # 關聯的 FirstDollar Sprint
│
├── atlas_metadata（圖譜元資料，匿名化後）
│   ├── is_public: boolean            # 是否貢獻到公共圖譜
│   ├── anonymized_at: timestamp?
│   ├── quality_score: enum [seed | community | expert_curated]  # 品質層級（非 idea score！是資料品質）
│   └── view_count: int               # 被瀏覽次數
│
└── embedding: vector(1536)           # pgvector 向量（for 相似痛點推薦）


Solution（現行替代方案）
├── name: string              # 替代方案名稱（具體產品/工具/人）
├── type: enum [tool | service | manual | outsource | ignore]
├── cost: string              # 使用者目前付出的成本描述
└── dissatisfaction: string   # 最不滿意的點


UnitEcon（單位經濟學框算）
├── revenue_per_unit: string      # 每單預估收入
├── cost_per_unit: string         # 每單預估成本
├── margin_positive: boolean      # 毛利 > 0？
└── assumptions: string[]         # 關鍵假設
```

### 2.2 匿名化規則

| 原始欄位 | 匿名化處理 | 保留內容 |
| :--- | :--- | :--- |
| 人名 | 完全移除 | — |
| 公司名 | 替換為行業標籤（「某電商平台」） | 行業 + 規模 |
| 具體金額 | 替換為區間 | 金額區間 |
| 聯絡方式 | 完全移除 | — |
| 地理位置 | 模糊化（台灣 / 東亞 / 全球） | 區域 |
| 行業情境 | 保留 | 完整保留（核心價值） |
| JTBD 描述 | 移除可識別資訊 | 結構保留 |
| 替代方案名稱 | 保留（公開產品名） | 完整保留 |

**匿名化鐵律**：
- 匿名化是**不可逆操作** — 原始資料和匿名化版本分開儲存
- 使用者可撤回貢獻 → 從公共圖譜刪除，但不影響私人庫
- 任何能定位到「這是某個具體人的痛點」的組合資訊都必須被清除

### 2.3 痛點品質分級

不打分數，但需要區分資料品質以維護圖譜信任度：

| 品質層級 | 定義 | 標記方式 |
| :--- | :--- | :--- |
| **Seed** | PM 手動 curate 或早期使用者初始貢獻，未經驗證 | 灰色標籤「種子資料」 |
| **Community** | 使用者結構化後貢獻，物理量部分填寫 | 藍色標籤「社群貢獻」 |
| **Interview-Verified** | 附帶訪談紀錄（≥ 1 次真人對話） | 綠色標籤「有訪談驗證」 |
| **Payment-Verified** | 有真實付費訊號（透過 FirstDollar 回傳） | 金色標籤「有付費訊號」 |

**注意**：品質層級是**事實標記**（有沒有做過這件事），**不是評分**。不存在「好的痛點 / 壞的痛點」的判斷。

### 2.4 向量搜尋與推薦

```
使用者輸入新痛點
    ↓
結構化為 JTBD 格式
    ↓
生成 embedding（Claude / OpenAI embedding）
    ↓
pgvector cosine similarity 搜尋 Pain Atlas
    ↓
回傳「相似痛點 Top 5」
    ├── 有人驗證過嗎？驗證到什麼程度？
    ├── 他們的替代方案是什麼？
    └── 有人做出 GTM 策略嗎？
```

推薦的呈現方式：**「這些人遇過類似的問題」** — 不是排名，是相關性地圖。

---

## 3. 冷啟動策略

### 3.1 冷啟動的核心問題

Pain Atlas 有經典的雙邊冷啟動問題：
- 沒有資料 → 新使用者覺得圖譜沒用 → 不願貢獻 → 還是沒有資料

打破方式：**在飛輪啟動前，靠人工 + Design Partner 填充到 critical mass。**

### 3.2 三階段冷啟動

#### Phase 0：種子庫建置（上線前 4 週）

**目標**：200 條高品質種子痛點

**來源**：

| 來源 | 數量 | 方式 | 品質層級 |
| :--- | :--- | :--- | :--- |
| PM 從公開社群提取 | 80 條 | 掃 PTT 創業板 / Indie Hackers / Reddit / Facebook 社團，提取真實使用者描述的痛點 | Seed |
| PM 從 FirstDollar persona 訪談延伸 | 30 條 | 從 5 位 persona 的訪談逐字稿中結構化提取 | Interview-Verified |
| PM 從競品評論提取 | 40 條 | IdeaCheck / ShipYourIdea / Gumroad / Product Hunt 的使用者評論 | Seed |
| PM 從行業報告提取 | 50 條 | 台灣中小企業調查、東亞 solo founder 調查等公開報告中的痛點 | Seed |

**執行方式**：
1. 建立結構化模板（Google Sheet）
2. PM 每天 curate 10 條（3 小時 / 天 × 20 天）
3. 每條都經過 JTBD 格式化 + 物理量檢驗
4. 匯入 Supabase + 生成 embedding

**品質控制**：
- 每條種子痛點必須有「原始來源 URL」（即使匿名化後移除）
- 種子痛點標記為「Seed」品質層級，使用者知道這是初始資料
- 任何編造的痛點一律刪除（寧缺勿假）

#### Phase 1：Design Partner 貢獻（Private Beta，月 1-2）

**目標**：10 位 Design Partner 每人貢獻 20–30 條 → 額外 200–300 條

**Design Partner 招募條件**：

| 條件 | 理由 |
| :--- | :--- |
| 至少有 1 年行業經驗 | 能貢獻高品質的行業痛點 |
| 至少嘗試過 1 次 side project | 理解「找題」的痛 |
| 願意每週花 30 分鐘使用 PainMap | 持續回饋 |
| 覆蓋 ≥ 5 個不同行業 | 避免圖譜偏向單一行業 |

**激勵機制**：
- Lifetime Pro plan 免費
- 圖譜中標記「Design Partner 貢獻」徽章
- 優先看到新增痛點條目
- 月度 1v1 with PM（直接影響產品方向）

**目標行業覆蓋**：

| 行業 | Design Partner 數 | 種子 + DP 目標條目數 |
| :--- | :--- | :--- |
| SaaS / 軟體 | 2 | 80 |
| 電商 / 零售 | 2 | 80 |
| 創作者經濟 | 2 | 60 |
| 專業服務（顧問、設計） | 2 | 60 |
| 教育 / 線上課程 | 1 | 40 |
| 其他 | 1 | 40 |
| **合計** | **10** | **~360** |

#### Phase 2：自然飛輪啟動（Public Beta，月 3-6）

**前提**：圖譜已有 ~400–500 條，覆蓋 ≥ 5 個行業

**飛輪機制**：
```
新使用者進入 PainMap
    ↓
結構化自己的痛點
    ↓
系統推薦「相似痛點 Top 5」（from Pain Atlas）
    ↓
使用者看到「原來有人也遇到這個問題，而且已經驗證過了」
    ↓ 價值感建立
使用者 opt-in 貢獻自己的痛點到圖譜
    ↓
圖譜資料量 +1
    ↓
下一位使用者得到更好的推薦（飛輪加速）
```

**飛輪加速器**：
- 每週 email digest：「本週新增了 12 個你所在行業的痛點條目」→ 拉回舊使用者
- 圖譜貢獻者排行（不是排名分數，是「貢獻條目數」的事實標記）
- 「被 X 人參考」通知 → 貢獻者看到自己的痛點幫助了別人

### 3.3 Critical Mass 定義

| 指標 | Critical Mass 門檻 | 理由 |
| :--- | :--- | :--- |
| 總痛點條目數 | ≥ 1,000 | 任何行業搜尋都能找到 ≥ 5 個相關條目 |
| 行業覆蓋 | ≥ 10 個行業 | 新使用者不會遇到「你的行業還沒有資料」 |
| Interview-Verified 比例 | ≥ 20% | 圖譜信任度的底線 |
| Payment-Verified 比例 | ≥ 5% | 有真金白銀的證據才有說服力 |
| 月新增條目 | ≥ 100 / 月 | 飛輪已自轉（不再依賴 PM 手動） |

**預估達成時間**：上線後 6 個月（基於 Design Partner 月增 100 + 自然增長月增 50 的保守估計）

---

## 4. 飛輪深度設計

### 4.1 三個飛輪及其關係

#### 飛輪 A — Pain Atlas 知識飛輪（主飛輪 ★）

```
使用者結構化痛點
    ↓
匿名化進入 Pain Atlas
    ↓
AI 學習「什麼行業 × 什麼情境 × 什麼 TA = 高驗證痛點」
    ↓
新使用者結構化時得到更精準的「相似痛點」推薦
    ↓
結構化品質提升（看到好的範本 → 自己的輸出也更好）
    ↓
更多高品質痛點進入 Atlas
```

**規模效應**：越多人用 → 圖譜越準 → 對後來者價值遞增 → 這是 IdeaCheck 靠 AI 打分永遠無法做到的，因為 AI 打分不累積真實世界驗證資料。

#### 飛輪 B — 驗證回饋飛輪

```
使用者在 PainMap 結構化問題
    ↓
帶著結構化問題進入 FirstDollar Sprint
    ↓
Sprint 結果（成功 / 失敗 / pivot）回傳 PainMap
    ↓
Pain Atlas 條目更新驗證狀態
    ↓
新使用者看到「這類痛點有 X% 成功收到第一塊錢」
    ↓
選題決策有真實數據支撐
```

**關鍵**：這個飛輪依賴 FirstDollar 的金流回饋。兩個產品串接越緊密，這個飛輪越強。

#### 飛輪 C — 行業專家知識飛輪

```
David 類行業專家使用蘇格拉底對話
    ↓
隱性知識被結構化
    ↓
高品質痛點進入 Atlas（Expert-Curated 標記）
    ↓
其他使用者看到專家級分析 → PainMap 品牌信任度提升
    ↓
更多專家願意使用（因為平台品質高）
    ↓
Expert-Curated 比例提升
```

**特性**：這是品質飛輪，不是數量飛輪。Expert-Curated 條目的存在本身就是品牌資產。

### 4.2 飛輪優先級

| 階段 | 主飛輪 | 支援飛輪 | 暫緩 |
| :--- | :--- | :--- | :--- |
| **MVP（0-3 月）** | A（痛點累積，先有量） | — | B（等 FirstDollar 串接）、C（等專家入駐） |
| **PMF 驗證（3-6 月）** | A + C（品質提升） | B（開始串接 FirstDollar） | — |
| **規模化（6-12 月）** | **A（主）+ B（回饋）** | C | — |
| **成熟（12 月+）** | B（驗證回饋成為最強護城河） | A + C | — |

### 4.3 飛輪斷點風險與緩解

| 飛輪 | 斷點 | 嚴重度 | 緩解措施 |
| :--- | :--- | :--- | :--- |
| A | 使用者不願匿名化貢獻（隱私疑慮） | **CRITICAL** | Opt-in + 可撤回 + 貢獻者優先看新痛點 + 匿名化規則透明公開 |
| A | 低品質灌水（為了「貢獻數」亂填） | HIGH | 品質分級標記 + 社群舉報機制 + PM 定期 audit |
| B | FirstDollar 串接延遲 | MEDIUM | 允許使用者手動回報驗證結果（自填問卷） |
| B | 使用者 Sprint 失敗後不回報 | MEDIUM | 預設追蹤（opt-out 而非 opt-in）+ 30 天後自動 ping |
| C | 行業專家覺得「我的知識被稀釋」 | HIGH | Expert-Curated 專屬標記 + 專家 profile 頁 + 分潤機制（v2） |

---

## 5. 與 FirstDollar 護城河的互鎖設計

### 5.1 雙產品護城河矩陣

```
                    PainMap                     FirstDollar
                    ───────                     ───────────
M1 資料護城河     Pain Atlas（問題端）         Offer Vault（解法端）
                        ↕ 互補 ↕
M2 驗證護城河     驗證狀態追蹤                  Revenue Telemetry
                        ↕ 回饋 ↕
M3 品牌護城河     ──── 共享：反 idea score ────
M4 鎖定護城河     痛點知識庫 + GTM 歷史         Sprint 歷史 + 對話記憶
M5 網絡護城河     行業專家貢獻                  創作者合作網絡
```

### 5.2 資料流動

```
PainMap                                FirstDollar
────────                               ───────────
結構化問題          →→→                  Sprint 初始化
+ 物理量畫布        →→→                  （問題已定義，直接進入驗證）
+ GTM 策略          →→→

                    ←←←                  Sprint 結果
                    ←←←                  （成功 / 失敗 / pivot）
                    ←←←                  Revenue 金額區間
痛點驗證狀態更新    ←←←
```

### 5.3 聯合定價考量

| 方案 | 描述 | 優點 | 缺點 |
| :--- | :--- | :--- | :--- |
| **A. 獨立訂閱** | PainMap Pro + FirstDollar Pro 分開計費 | 各自獨立驗證 PMF | 使用者總成本高、體驗割裂 |
| **B. 套餐折扣** | 同時訂閱兩者 -30% | 激勵串接使用 | 增加定價複雜度 |
| **C. 統一品牌** | 同一產品的兩個功能模組 | 體驗最流暢 | 單一產品過重、失焦風險 |

**建議**：MVP 採方案 A（獨立驗證），PMF 後轉方案 B（套餐激勵串接）。

---

## 6. 圖譜治理與品質維護

### 6.1 治理原則

| 原則 | 具體做法 |
| :--- | :--- |
| **透明** | 匿名化規則、資料使用方式、品質分級標準全部公開 |
| **使用者主權** | 自己的資料隨時可 export / 刪除 / 撤回公共貢獻 |
| **品質 > 數量** | 寧可圖譜小但準，不要大但雜 |
| **事實標記 ≠ 評分** | 品質層級是「做過什麼事」的事實，不是「好不好」的判斷 |

### 6.2 品質維護機制

| 機制 | 頻率 | 負責 |
| :--- | :--- | :--- |
| PM 人工 audit | 每週抽查 10% 新增條目 | PM |
| 社群舉報 | 即時 | 使用者 |
| 重複偵測 | 自動（cosine similarity > 0.92 flagged） | 系統 |
| 過時標記 | 每 6 個月自動標記「6 個月無更新」的條目 | 系統 |
| Expert review | 每月邀請 Design Partner 審核 50 條 | PM + Expert |

### 6.3 資料生命週期

```
痛點條目 created
    ↓
使用者結構化（draft → structured）
    ↓
opt-in 匿名化（private → public on Atlas）
    ↓
被其他使用者瀏覽 / 參考
    ↓
被 FirstDollar Sprint 驗證 → 更新驗證狀態
    ↓
6 個月無更新 → 標記「可能過時」
    ↓
12 個月無更新 → 降低推薦權重（不刪除）
    ↓
使用者撤回 → 從 Atlas 移除（不可逆操作的逆操作）
```

---

## 7. 技術架構要點

### 7.1 儲存層

| 資料類型 | 儲存方案 | 理由 |
| :--- | :--- | :--- |
| 結構化痛點（原始 + 匿名化） | Supabase Postgres | 與 FirstDollar 統一技術棧 |
| 向量 embedding | Supabase pgvector | 相似痛點搜尋 |
| 原始素材（截圖、CSV） | Supabase Storage | 短期保留（匿名化後可選刪除） |
| 搜尋索引 | Supabase Full-Text Search | 行業 / 關鍵字搜尋 |

### 7.2 關鍵 API

| API | 職責 | SLA |
| :--- | :--- | :--- |
| `POST /pain/extract` | 從 raw text 提取結構化痛點 | ≤ 90 秒 |
| `POST /pain/structure` | 蘇格拉底對話一輪 | ≤ 10 秒 |
| `GET /atlas/search` | 相似痛點搜尋（向量 + 關鍵字） | ≤ 2 秒 |
| `GET /atlas/heatmap` | 行業痛點熱力圖資料 | ≤ 5 秒 |
| `POST /atlas/contribute` | 匿名化 + 貢獻到圖譜 | ≤ 5 秒 |
| `POST /firstdollar/handoff` | 打包結構化問題 → FirstDollar | ≤ 3 秒 |

---

## 8. 關鍵指標與監控

| 指標 | 目標 | 監控頻率 | 警戒線 |
| :--- | :--- | :--- | :--- |
| 圖譜月新增條目 | ≥ 100 | 每週 | < 50 → 飛輪可能停轉 |
| 貢獻 opt-in 率 | ≥ 30% | 每週 | < 15% → 隱私疑慮過大 |
| 結構化完成率 | ≥ 60% | 每週 | < 40% → UX 太複雜 |
| 相似痛點命中率 | ≥ 70% 使用者覺得「相關」 | 每月 NPS | < 50% → embedding 品質問題 |
| FirstDollar 串接率 | ≥ 20% 結構化後進入 Sprint | 每月 | < 10% → handoff UX 問題 |
| 圖譜 Interview-Verified 比例 | ≥ 20% | 每月 | < 10% → 圖譜品質太低 |

---

## 9. 結論與下一步

### 9.1 護城河結論

> PainMap 的勝負在一件事：**Pain Atlas 能不能在 6 個月內達到 critical mass（1,000 條 × 10 行業 × 20% 驗證率）。** 達到了 → 飛輪自轉 → 護城河建立。沒達到 → 只是又一個 AI 工具。

### 9.2 最高風險

| 風險 | 影響 | 緩解 |
| :--- | :--- | :--- |
| 使用者不願貢獻 | 飛輪斷裂 | 激勵設計（貢獻者優先看新痛點） |
| 種子品質太低 | 新使用者失望離開 | PM 嚴格 audit + 品質 > 數量 |
| FirstDollar 串接延遲 | 驗證飛輪無法啟動 | 先允許手動回報 |

### 9.3 48 小時行動項

| # | 動作 | 負責 |
| :--- | :--- | :--- |
| 1 | 開始 curate 種子痛點庫（目標：第一週 50 條） | PM |
| 2 | 列出前 10 位 Design Partner 候選名單 | PM |
| 3 | 設計匿名化規則 v1 並請 Legal 審閱 | PM + Legal |
| 4 | 建立結構化模板（Google Sheet）for 種子 curate | PM |
| 5 | 與 FirstDollar team 討論串接 API 規格 | PM + Eng |

---

**文件版本：** v1.0（草稿）
**建立日期：** 2026-04-09
**配套：** PRD v1.0（`painmap_prd.md`）、破壞式創新框架（`painmap_disruption_framework.md`）
**審核需求：** Product Lead、Legal（匿名化規則）、Lead Engineer（技術架構）
