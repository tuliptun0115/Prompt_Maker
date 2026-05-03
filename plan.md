# My Prompt Maker — 指令產生器 實作計劃書

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** 建立一套「提示詞模板集合」，核心是一個 Meta-Prompt（指令產生指令），使用者輸入任何場景後，AI 會依三大廠商的分類架構，自動輸出各分類的提示詞，格式同時包含 YAML 與自然語言兩種版本。

**Architecture:** 純文件型專案（無程式碼），以 Markdown + YAML 檔案組成，放在現有 `My_Prompt Maker/` 資料夾中。使用者直接將 Meta-Prompt 複製進任何 AI 對話框使用，不依賴外部服務。

**Tech Stack:** Markdown、YAML、三大AI指南文件（Anthropic、Google Gemini、ChatGPT/OpenAI）；建議加入 Midjourney Prompt Guide 作為視覺提示第四來源。

---

## Context

使用者在 `My_Prompt Maker/` 收集了三大 AI 的官方提示詞設計指南（Anthropic、Google Gemini API、跨模型比較指南）。目前這些只是原始參考資料，缺乏一個可立即使用的「產生工具」。本計劃將這些資料整理成一套可執行的提示詞生成框架，讓使用者只要輸入場景描述，就能快速獲得多風格、多分類的提示詞集合（YAML + 自然語言）。

NotebookLM 視覺簡報背景提示詞是首個示範用例，已有明確的範例格式（視覺風格描述型自然語言提示詞）。

---

## 推薦加入的第四個 AI 來源

| 來源 | 理由 | 優先加入 |
|------|------|---------|
| **Midjourney Prompt Guide** | 視覺類提示詞最主流的規格：`--ar 16:9`、`--style raw`、`--v 6.1`，提供攝影/藝術/設計三大維度語法 | 強烈建議 |
| Microsoft Copilot | 企業簡報情境較強，但語法與 ChatGPT 高度重疊 | 可選 |
| Stability AI | Stable Diffusion 的負向提示詞（negative prompt）寫法獨特 | 可選 |

建議本計劃**先做 Midjourney**，因為示範用例就是視覺提示詞。

---

## 提示詞分類架構（由三大 AI 指南提煉）

### 通用結構層（7大必要元素）
| # | 分類 | 定義 |
|---|------|------|
| 1 | **角色層** | Role / Persona — 設定 AI 扮演的角色與知識背景 |
| 2 | **目標層** | Task / Purpose — 明確說明要達成什麼 |
| 3 | **上下文層** | Context — 背景資訊、受眾、使用情境 |
| 4 | **示例層** | Examples / Few-shot — 2–5 個具體示範 |
| 5 | **輸出規格層** | Output Format — 格式、長度、結構要求 |
| 6 | **約束條件層** | Constraints — 禁止事項與必要限制 |
| 7 | **精煉層** | Refinement — 語氣、風格、品質標準 |

### 視覺提示詞專屬分類（NotebookLM 示範用例）
| # | 分類 | 對應範例關鍵詞 |
|---|------|--------------|
| A | **色彩系統** | 深邃黑 + 霓虹青漸層 |
| B | **材質紋理** | 微型晶片、數據網格 |
| C | **光線情境** | 全息投影光暈、冷色調高光 |
| D | **構圖版式** | 左側深負空間 |
| E | **設計美學** | 科技極簡主義、AI 科技感 |
| F | **技術規格** | 8K、16:9 |
| G | **功能性需求** | 不干擾前景文字閱讀 |

---

## 交付物（檔案結構）

```
My_Prompt Maker/
├── 00-README.md                              ← 全局索引 + 使用說明
├── 01-三大AI提示詞分類架構.md                  ← 架構文件（供 Meta-Prompt 引用）
├── 02-核心Meta-Prompt.md                     ← 核心指令產生指令（主要工具）
├── 03-YAML輸出格式規範.md                     ← YAML 結構定義
└── examples/
    ├── notebooklm-簡報背景.yaml               ← NotebookLM 範例（YAML 格式）
    └── notebooklm-簡報背景.md                 ← NotebookLM 範例（自然語言格式）
```

現有五個原始指南檔案**保留不動**，作為 `01-三大AI提示詞分類架構.md` 的來源依據。

---

## Task 1：建立三大AI提示詞分類架構文件

**Files:**
- Create: `My_Prompt Maker/01-三大AI提示詞分類架構.md`

- [ ] **Step 1: 建立架構文件**

內容結構：
1. 文件說明（來源：Anthropic / Google Gemini API / PromptBuilder 跨模型指南）
2. 通用 7 層架構（Role / Task / Context / Examples / Output / Constraints / Refinement）
3. 三大廠商各自的特殊語法規範
   - Claude：XML 標籤（`<instructions>`, `<context>`, `<examples>`）
   - Gemini：結構化 Markdown 或 XML，**指令放最末端**
   - ChatGPT：POWER 框架（Purpose / Output / Working Context / Examples / Refinement）
4. 視覺提示詞專屬分類（A~G，見上方架構表）
5. 各提示技術類型（Zero-shot / Few-shot / CoT / RAG / Metacognitive / Iterative）

- [ ] **Step 2: 確認內容正確引用現有指南**

對照以下現有檔案驗證內容準確性：
- `Prompting best practices-Anthropic.md`（Claude XML 標籤規範）
- `提示设计策略 _ Gemini API.md`（Gemini 結構化提示原則）
- `Prompt Engineering in 2025_ Complete Guide for ChatGPT, Claude, and Gemini.md`（POWER 框架）

---

## Task 2：建立核心 Meta-Prompt（指令產生指令）

**Files:**
- Create: `My_Prompt Maker/02-核心Meta-Prompt.md`

- [ ] **Step 1: 撰寫 Meta-Prompt**

Meta-Prompt 格式對應使用者提供的範例結構：
1. 指引 AI 讀取 `01-三大AI提示詞分類架構.md` 中的分類框架
2. 說明使用場景（由使用者填入，如「NotebookLM 簡報背景」）
3. 提供一個參考範例（使用者的自然語言格式範例）
4. 指定輸出要求：**每個分類架構各生成一個創意提示詞**，同時輸出 YAML 格式與自然語言格式兩種版本

Meta-Prompt 本體（需寫入檔案的內容）：

```
你是一位專業的提示詞工程師，熟悉 Anthropic Claude、Google Gemini 及 OpenAI ChatGPT 三大 AI 模型的官方提示詞設計標準。

請依照以下【提示詞分類架構】，協助我為指定場景創作多風格的提示詞集合。

【使用場景】
{場景描述} ← 使用者填入，例如：「NotebookLM 的簡報背景圖片生成」

【提示詞分類架構】
[貼入 01-三大AI提示詞分類架構.md 的視覺提示詞分類 A~G]

【參考範例格式】
以下是一個自然語言格式的優質提示詞範例，請以此作為風格與精緻度的參考基準：

{自然語言範例} ← 使用者填入，例如本計劃的 NotebookLM 範例

【輸出要求】
針對上述每個分類架構（A至G），各生成一個獨特的創意提示詞，並同時提供：
1. YAML 格式版本（依照 03-YAML輸出格式規範.md 結構）
2. 自然語言版本（風格與精緻度對齊參考範例）

每個分類的輸出格式：
---
分類：[分類名稱]
主題：[本提示詞的設計主題]

### YAML 版本
```yaml
[YAML 內容]
```

### 自然語言版本
[自然語言提示詞]
---
```

- [ ] **Step 2: 加入使用說明**

說明欄位包含：
- 如何填入「使用場景」
- 如何填入「自然語言範例」（可直接貼使用者的原始描述）
- 輸出結果的預期長度（7 個分類 × 2 種格式 = 約 14 個輸出區塊）

---

## Task 3：建立 YAML 輸出格式規範

**Files:**
- Create: `My_Prompt Maker/03-YAML輸出格式規範.md`

- [ ] **Step 1: 定義 YAML 結構**

針對視覺提示詞（NotebookLM 簡報背景），YAML 結構定義如下：

```yaml
prompt:
  meta:
    category: "分類名稱（如：色彩系統）"
    style_name: "本提示詞的主題名稱"
    use_case: "使用場景"
    ai_target: "Claude / Gemini / ChatGPT / Midjourney（可多選）"

  visual:
    color_system:
      primary: "主色（色名 + 色碼）"
      accent: "強調色"
      background: "背景色"
      gradient: "漸層描述"
    texture:
      elements: []      # 紋理元素清單
      opacity: "透明度描述"
      scale: "尺寸描述（大/小/微型）"
    lighting:
      type: "光線類型"
      effects: []       # 光線效果清單
      mood: "情緒描述"
    composition:
      layout: "版式描述"
      focal_point: "視覺焦點位置"
      negative_space: "留白描述"

  style:
    aesthetic: "整體美學風格"
    era: "時代感（未來/現代/復古）"
    mood: "氛圍形容詞（2-4個）"

  technical:
    resolution: "8K / 4K / 1080p"
    aspect_ratio: "16:9 / 4:3 / 1:1"
    color_profile: "sRGB / P3"

  functional:
    foreground_compatibility: "前景文字/色塊相容性說明"
    safe_zones: "安全區域描述"

  natural_language: |
    （完整的自然語言版本提示詞，放在最後）
```

- [ ] **Step 2: 加入各分類的 YAML 欄位使用說明**

說明哪些欄位是必填，哪些是選填，以及範例值。

---

## Task 4：生成 NotebookLM 示範範例

**Files:**
- Create: `My_Prompt Maker/examples/notebooklm-簡報背景.yaml`
- Create: `My_Prompt Maker/examples/notebooklm-簡報背景.md`

- [ ] **Step 1: 執行 Meta-Prompt，生成 NotebookLM 範例**

使用 Task 2 的 Meta-Prompt，填入：
- 場景：「NotebookLM 的簡報底圖生成，供知識型簡報使用」
- 參考範例：使用者原始提供的霓虹青科技風格提示詞

針對 7 個視覺分類（A~G）各生成一個提示詞，格式同時包含 YAML 和自然語言版本。

- [ ] **Step 2: 將 YAML 版本寫入 `notebooklm-簡報背景.yaml`**

7 個分類的 YAML 提示詞，以 YAML list 結構整合在單一檔案：

```yaml
# NotebookLM 簡報背景提示詞集合
# 生成日期：2026-05-02
# 場景：NotebookLM 知識型簡報底圖

prompts:
  - category: "A_色彩系統"
    prompt:
      meta: {...}
      visual: {...}
      ...
  - category: "B_材質紋理"
    prompt: {...}
  ...（共 7 個分類）
```

- [ ] **Step 3: 將自然語言版本寫入 `notebooklm-簡報背景.md`**

7 個分類的自然語言提示詞，每個以 `---` 分隔，標明分類名稱與設計主題。

---

## Task 5：建立索引文件

**Files:**
- Create: `My_Prompt Maker/00-README.md`

- [ ] **Step 1: 撰寫使用說明**

內容包含：
1. 專案定位（三句話說明）
2. 快速開始（3 步驟：讀架構 → 填 Meta-Prompt → 複製輸出）
3. 檔案索引（每個檔案的用途一句話說明）
4. 使用情境範例（NotebookLM 以外還能用在哪些場景）
5. 如何新增使用場景（步驟說明）
6. 三大 AI 的特殊語法快速對照表

---

## 驗證方法

- [ ] 開啟 `02-核心Meta-Prompt.md`，複製全文貼入 Claude 對話，填入任一場景後檢查輸出是否符合格式
- [ ] 確認 YAML 輸出可以被任意 YAML parser 解析（無語法錯誤）
- [ ] 確認 `examples/notebooklm-簡報背景.yaml` 中 7 個分類的風格明顯不同（無重複）
- [ ] 確認自然語言版本的精緻度與使用者原始範例相當

---

## 補充說明：Midjourney 整合建議

若後續要加入 Midjourney 作為第四個 AI 來源，在 YAML 的 `ai_target` 欄位加上 `Midjourney`，並在自然語言版本末尾補上參數行：

```
--ar 16:9 --style raw --v 6.1 --quality 2 --chaos 20
```

此部分不在本計劃範圍內，可在初版完成後獨立擴充。

---

## 更新紀錄

### 2026-05-03 — GitHub 正式發佈與改版紀錄

- **使用工具：** Antigravity (Git, Shell)
- **做到哪裡：**
  - **正式發佈：** 專案已成功推送到 GitHub [tuliptun0115/Prompt_Maker](https://github.com/tuliptun0115/Prompt_Maker)。
  - **安全性強化：** 新增 `robots.txt` 與 `.gitignore`，確保內部工具不被爬蟲索引，並排除 AI 紀錄檔。
  - **工具改版：** `index.html` 視覺提示詞頁面完成 v1.2 改版，支援 A–F 欄位化輸入與 Midjourney 參數自動生成。
- **下一步：**
  - 邀請使用者進行測試，確認視覺提示詞生成的流暢度。
  - 若有需要，可進一步整合 localStorage 儲存個人自訂模板。
- **注意事項：**
  - 公開倉庫已鎖定爬蟲封鎖，部署後應檢查 Vercel/GitHub Pages 是否正確讀取 `robots.txt`。

### 2026-05-03 — v1.2 視覺提示詞改版

- **使用工具：** Claude Code（Edit、Read）
- **做到哪裡：** `index.html` 視覺提示詞頁面完整改版
  - **改版核心：** 從「Meta-Prompt 產生器」改為「直接輸出完整視覺提示詞」
  - 側欄欄位依 A–F 分類拆分為具體設定項：主色、強調色、漸層方向、紋理多選、光線效果、高光陰影、構圖留白、美學風格、解析度/比例
  - 新增紋理 chip 多選（8 種：晶片、數據網格、蜂巢格、電路板、金屬波紋、量子粒子、幾何框架、稜鏡折射）
  - 新增三張對應表：`lightingMap`（6 種光線）、`compositionMap`（5 種構圖）、`shadowMap`（4 種陰影）
  - 改寫 `genVisual()` 函數，將各段設定組裝成一段流暢自然語言提示詞
  - 勾選 Midjourney 平台後自動附加參數行（`--ar --style raw --v 6.1 --quality 2`）
  - 修正 `genOfficial()` 模板替換邏輯：移除多餘【】包覆，空值 fallback 為 `[欄位名稱]`
  - 新增 `resetVisual()` 清除函數
  - `init()` 補上紋理 chip 點擊事件監聽
- **下一步（可選）：**
  - 新增「隨機生成」按鈕，從各設定項隨機挑選組合
  - 加入顏色選擇器（color picker）輔助主色/強調色輸入
  - 「我的常用設定」儲存功能（localStorage）
- **注意事項：**
  - 紋理 chip 需透過 `init()` 掛事件，不是 inline onclick，避免重複綁定
  - `lightingMap` key 對應 `<select>` 的 `value` 屬性（holo / neon / lava / prism / ambient / quantum）

### 2026-05-02 — v1.1 完成

- **使用工具：** Claude Code（Write、Edit、Read、Agent/Explore subagent）
- **做到哪裡：** 所有 Task 1–5 全部完成，並額外新增網頁工具（原計劃外需求）
  - Task 1：`01-三大AI提示詞分類架構.md` 建立完成
  - Task 2：`02-核心Meta-Prompt.md` 建立完成
  - Task 3：`03-YAML輸出格式規範.md` 建立完成
  - Task 4：`examples/notebooklm-簡報背景.yaml` + `.md` 兩種格式均完成（7 分類 A–G）
  - Task 5：`00-README.md` 索引文件建立完成
  - **額外：** `index.html` 網頁工具完成，單一 HTML 檔案，無需伺服器
- **index.html 功能摘要：**
  - 「官方範本庫」Tab：依據 Gemini for Workspace Prompting Guide 101，內建 10 部門 / 20+ 角色 / 55+ 任務模板（雙語 zh/en）
  - 三層級聯選單（部門 → 角色 → 任務），選完自動產生情境填寫欄位
  - 模板替換後直接輸出可貼入 AI 的 PTCF 格式指令
  - 「視覺提示詞」Tab：Meta-Prompt 產生器，支援 A–G 分類選擇、比例、解析度、參考範例
  - 系統資訊頁：PTCF 框架說明、部門覆蓋表、四大 AI 語法卡片
- **下一步（可選）：**
  - 在「官方範本庫」補充更多部門任務（如法務、財務、IT）
  - 加入「我的自訂模板」功能（localStorage 儲存）
  - 加入直接呼叫 AI API 的功能（需後端或 API key 輸入欄）
- **注意事項：**
  - 模板佔位符格式：中文用 `[欄位名稱]`（使用者未填時的 fallback），英文同
  - 替換邏輯為「按欄位順序依次替換第一個匹配」，多欄位模板需照順序填寫
  - HTML 已加 `noindex, nofollow` meta tag，安全無虞
