<div align="center">

<img src="assets/hero.png" alt="AI Brainstorming" width="720" />

# AI Brainstorming — 一人公司 0→1 方法論倉庫

**從模糊點子 → 第一塊錢。用第一性原理砍掉所有代理動作。**

[![Version](https://img.shields.io/badge/version-v1.0-blue)]()
[![Language](https://img.shields.io/badge/language-繁體中文-red)]()
[![License](https://img.shields.io/badge/license-MIT-green)](LICENSE)

</div>

> 這不是一個 SaaS，不是一個工具，也不是另一份「AI 創業點子清單」。
> 這是一套**可執行、可驗證、可反覆使用的方法論文件庫** — 教 solo founder 和 indie hacker 在 AI 時代用最短路徑把點子變成第一筆收入。

---

## 這個 repo 在回答的本質問題

> **在 AI 全面壓縮工作量的 2026，一個人要把一個模糊點子變成第一筆收入，最少需要做什麼？**

核心論點：

- **AI 時代 0→1 的勝負，不在「快」，而在『不做』的紀律。**
- 把「點子 → 第一塊錢」reduce 到不可再分的**四個物理量**：具體的人／具體的痛／手工交付／錢的管道。
- 砍掉所有不服務物理量的工作 — 包括 logo、簡報、品牌、過度設計的系統。
- 剩下的用 AI 全開加速。

---

## 文件全景

```
docs/product/
├── 方法論層（Methodology）
│   ├── first_principles_playbook.md           # 第一性原理 Playbook（哲學層）
│   ├── first_principles_sprint_manual.md      # 72 小時 Sprint Manual（可執行手冊）
│   └── socratic_first_principles_rnd_workflow.md  # 蘇格拉底 × 第一性原理整合工作流
│
├── firstdollar/  — 產品一：FirstDollar（首單）
│   ├── firstdollar_prd.md                     # PRD v2.0（含 S1→F→S2 壓力測試修正）
│   └── firstdollar_strategy_addendum.md       # 策略補遺：牙刷檢驗 × 護城河 × 飛輪
│
└── painmap/      — 產品二：PainMap（題眼）
    ├── painmap_prd.md                         # PRD v1.0（FirstDollar 的上游題眼）
    ├── painmap_disruption_framework.md        # 破壞式創新框架工具化（Christensen）
    ├── painmap_moat_design.md                 # 護城河設計：Pain Atlas × 冷啟動 × 飛輪
    ├── skills/                                # 7 步工作坊 skills（教師版 + 學生版）
    └── slides/                                # 19 頁 Keynote 風格教學簡報 + 學員手冊
```

輔助資料：

- `ai_one_person_company_0to1_strategy.md` — 底層策略文件（需求雷達 → 市場驗證 → 迭代擴張全流程）
- `VibeCcoing.md` — 市場觀察：Vibe Coding 做產品為什麼失敗
- `docs/web_design/` — Prompt Architect Pipeline（將 PRD 轉為 AI 網頁開發指令集）
- `.claude/` — Claude Code 開發模板（12 skills、5-gate git 工作流）

---

## 方法論核心

### 四個物理量（First Principles）

> 任何步驟，只要不服務下列四項之一，就是冗餘。

| 物理量 | 具體含義 |
| :--- | :--- |
| **1. 具體的人** | 有名字、能打電話給 3 位的真人。不是 persona、不是 TAM |
| **2. 具體的痛** | 他今天用什麼方法解？花多少錢／時間？為什麼現行方案爛？ |
| **3. 手工交付** | 今晚就做一次給 1 個人。禁止先建系統 |
| **4. 錢的管道** | 一條能收到新台幣／美金的連結就夠了 |

### S1 → F → S2 壓力測試管線

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌──────────────┐
│ S1 對齊題目 │ → │ F  分解取捨 │ → │ S2 壓測假設 │ → │ 決策／實驗／交付 │
└─────────────┘    └─────────────┘    └─────────────┘    └──────────────┘
```

- **S1（蘇格拉底式）** — 鎖定語意、定義、成功標準、非目標
- **F（第一性分解）** — 還原到約束與基元；分解路徑與成本
- **S2（再壓測）** — 檢查定義漂移、錯把相關當因果、遺漏反例

### 72 小時 Sprint 三階段

| 階段 | 時段 | 交付 |
| :--- | :--- | :--- |
| **Hour 0–24** | 問題物理量 + 社群 10 人清單 | 能列出 10 個有名字的真人 |
| **Hour 24–48** | 手工交付 + 第一筆付款連結 | 收款連結 + 至少 1 人刷卡 |
| **Hour 48–72** | 決策：前進 / 轉向 / 放棄 | 有錢 → 進入 7 天執行循環；沒錢 → 換題目 |

讀完 Sprint Manual，72 小時後只會有兩種結果：**≥1 個真人掏錢** 或 **零人掏錢**。沒有灰色地帶。

---

## 兩個產品：從「找題」到「收錢」的完整閉環

### PainMap（題眼）— 上游：把散亂痛點結構化成可驗證問題

**一句話定位**：行業痛點結構化引擎。不幫你想點子、不打分數；把你已經看見但還沒整理的散亂痛點，結構化成**可驗證的問題定義 + 破壞式 GTM 切入路徑**。

**核心洞察**：使用者不缺點子，缺結構。阿傑「電腦裡有 40 個 idea.md」不知道做哪個；David「10 年顧問經驗但隱性知識無法資產化」。

**護城河策略**：Pain Atlas — 使用者結構化的痛點匿名化後累積成跨行業知識庫。越多人用 → 圖譜越準 → 新人越容易找到好題目。

**North Star Metric**：結構化問題 → 30 天內產生第一筆付費訊號的轉化率（目標 ≥ 20%）

### FirstDollar（首單）— 下游：72 小時逼你拿到第一塊錢

**一句話定位**：反 IdeaCheck 的 1 人公司執行陪跑平台。不打分數、不生報告；在 7 天內用真實受眾訪談、自動 landing page、waitlist 收集、Stripe 金流串接，**逼你拿到從 0→1 的第一個付費信號**。

**v2.0 重大變更**：經 S1→F→S2 壓力測試，發現三處定義漂移已全面修正：

- **D1** — persona 降格為假設（真人訪談才算數）
- **D2** — MVP 重定義為手工版（PM 本人 = Sprint Engine）
- **D3** — 不碰錢（教使用者自行開 Lemon Squeezy / Stripe 帳戶）

**護城河策略（v2.0 修正）**：不建護城河，**繞護城河**。避開金管會金流代收、LINE OA 系統推播、AI 推薦引擎 — 前 50 人全部 PM 人肉上陣，累積 pattern 後才系統化。

### 兩者關係

```
PainMap（找題）  →  產出「結構化問題」  →  FirstDollar（收錢）  →  產出「第一塊錢」
   題眼                Pain Atlas 餵養       首單               Offer Vault 餵養
```

---

## 工作坊教材（PainMap Skills + Slides）

完整一套**可直接上課**的破壞式創新工作坊，全程使用「Shopee 小賣家客服」貫穿案例。

### Skills — 7 步結構化流程

| Step | 主題 | 產出 | 時間 |
| :--- | :--- | :--- | :--- |
| 01 | 痛點採集 | 散亂素材 → 結構化痛點 | 30–60 min |
| 02 | 問題本質拆解 | 痛點聚合 → 問題主題 + 物理量畫布 | 30–45 min |
| 03 | 破壞式機會辨識 | 低端破壞 vs 新市場破壞 | 20–30 min |
| 04 | 策略圖設計 | Strategy Canvas + 紅隊 + 不做清單 | 30–45 min |
| 05 | 最小產品設計 | 手工交付 + 定價 + 預售 | 30–45 min |
| 06 | 不對稱動機檢驗 | 大公司會不會來搶 | 15–20 min |
| 07 | GTM 一頁紙 | 72 小時行動計畫 | 20–30 min |

每一步都有 `teacher/`（填好範例 + 老師提醒）和 `student/`（空白 prompt + 檢查點）雙版本。

### Slides — 19 頁 Keynote 風格教學簡報

Steve Jobs 極簡風、Gagné's 9 Events of Instruction 結構、60 分鐘含 12 分鐘課堂練習。見 [`docs/product/painmap/slides/`](docs/product/painmap/slides/)，含 HTML 手冊版本。

---

## 三條使用路徑

### Path A — 我想自己跑一次 0→1
1. 讀 `docs/product/first_principles_playbook.md` — 建立方法論心智
2. 執行 `docs/product/first_principles_sprint_manual.md` — 72 小時 Sprint
3. 跑完決策：前進 / 轉向 / 放棄

### Path B — 我是講師，想在課堂帶學員做一次
1. 讀 `docs/product/painmap/slides/README.md` — 簡報架構
2. 讀 `docs/product/painmap/skills/README.md` — 7 步上課節奏
3. 使用 `teacher/` + `student/` 雙版本教學

### Path C — 我想參考兩個產品的 PRD 做類似的事
1. 讀 `docs/product/firstdollar/firstdollar_prd.md` — v2.0 PRD（含壓力測試修正）
2. 讀 `docs/product/painmap/painmap_prd.md` — 上游題眼 PRD
3. 套用 `socratic_first_principles_rnd_workflow.md` 做自己的壓力測試

---

## 核心紀律（讀這裡，其他都是註腳）

1. **禁止分數** — 不輸出 0–100 分、成功率 X%、可行性 A/B/C。分數是焦慮產品，不是生產力產品。
2. **用「問題」不用「點子」** — 你在「釐清問題」，不在「驗證點子」。
3. **AI 做執行，你做判斷** — AI 負責整理素材，你負責決定做不做。
4. **每一步都有「具體的人」** — 填不出名字 = 先去社群認識人。
5. **代理動作全部禁止** — logo、簡報、品牌、過度設計系統、「再研究一下市場」。

---

## 版本記錄

| 版本 | 日期 | 變更 |
| :--- | :--- | :--- |
| v1.0 | 2026-04-16 | README 重寫以反映 docs/product 全景（方法論 + 兩產品 + 工作坊教材） |
| —    | 2026-04-09 | 新增 PainMap PRD / disruption framework / moat design / skills / slides |
| —    | 2026-04-09 | FirstDollar PRD v2.0（S1→F→S2 壓力測試修正 D1–D3） |
| —    | 2026-04-09 | 新增 First Principles Playbook / Sprint Manual / Socratic R&D Workflow |

---

## License

MIT
