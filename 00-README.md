# My Prompt Maker — 提示詞指令產生器

> 一套基於 Anthropic、Google Gemini、OpenAI 三大官方指南的提示詞生成工具集，讓你輸入任何場景，立即獲得多風格、多分類的提示詞（YAML + 自然語言雙格式）。

---

## 快速開始（3 步驟）

```
1. 開啟 prompt-generator.html → 填入場景與設定 → 複製生成結果
   （或）
1. 開啟 02-核心Meta-Prompt.md → 複製全文
2. 填入 {場景描述} 與 {自然語言範例}
3. 貼入任一 AI 對話框送出
```

---

## 檔案索引

| 檔案 | 用途 |
|------|------|
| `prompt-generator.html` | **主要工具** — 網頁表單介面，填入設定後自動組裝 Meta-Prompt |
| `01-三大AI提示詞分類架構.md` | 分類架構參考文件（7層通用架構 + A–G視覺分類） |
| `02-核心Meta-Prompt.md` | 核心指令產生指令，可直接複製貼入任何 AI 使用 |
| `03-YAML輸出格式規範.md` | YAML 結構定義與欄位說明 |
| `examples/notebooklm-簡報背景.yaml` | NotebookLM 示範範例（YAML 格式，7個分類） |
| `examples/notebooklm-簡報背景.md` | NotebookLM 示範範例（自然語言格式，含快速比較表） |
| `Prompting best practices-Anthropic.md` | 原始來源：Anthropic 官方指南 |
| `提示设计策略 _ Gemini API.md` | 原始來源：Google Gemini API 官方指南 |
| `Prompt Engineering in 2025_...md` | 原始來源：跨模型比較指南（ChatGPT/Claude/Gemini） |

---

## 使用情境範例

除了 NotebookLM 簡報背景，這套工具同樣適用於：

| 使用情境 | 填入場景描述 |
|---------|------------|
| YouTube 頻道封面 | `YouTube 科技教育頻道封面，2560×1440px，吸引 Z 世代` |
| LinkedIn Banner | `LinkedIn 個人品牌 Banner，1584×396px，商業科技風` |
| 企業年報封面 | `企業年報封面，A4 直式，正式商業風，傳統與創新兼具` |
| Instagram 貼文背景 | `Instagram 知識卡片背景，1:1 正方形，教育型帳號` |
| Podcast 封面 | `Podcast 封面藝術，3000×3000px，科技財經主題` |
| 電子報 Header | `電子報 Header 圖，600px 寬，深色商業科技風` |

---

## 提示詞分類架構快速對照

### 通用 7 層結構
```
角色層 → 目標層 → 上下文層 → 示例層 → 輸出規格層 → 約束條件層 → 精煉層
```

### 視覺提示詞專屬（A–G）
```
A 色彩系統 → B 材質紋理 → C 光線情境 → D 構圖版式 → E 設計美學 → F 技術規格 → G 功能性需求
```

---

## 三大 AI 特殊語法快速對照

| AI | 關鍵語法特性 | 提示 |
|----|------------|------|
| **Claude** | XML 標籤（`<instructions>`, `<context>`, `<examples>`, `<task>`） | 在 02-核心Meta-Prompt 末尾加「請用 XML 標籤輸出」 |
| **Gemini** | 指令放末端；XML/Markdown 結構化 | 確認場景描述在前、指令在後 |
| **ChatGPT** | POWER 框架（Purpose/Output/Working Context/Examples/Refinement） | 可選擇 POWER 或 CO-STAR 框架輸出 |
| **Midjourney** | 自然語言末尾加參數行 | 在輸出末尾補 `--ar 16:9 --style raw --v 6.1 --quality 2` |

---

## 如何新增使用場景

1. 開啟 `prompt-generator.html`，填入新場景描述
2. 選擇需要的分類（可只選 A–G 中的特定幾類）
3. 複製生成結果貼入 AI，獲得新場景的提示詞集合
4. 把好的輸出結果存到 `examples/` 資料夾備用

---

## 更新紀錄

### 2026-05-02 v1.0
- 建立三大AI提示詞分類架構文件
- 建立核心 Meta-Prompt（視覺提示詞版）
- 建立 YAML 輸出格式規範
- 生成 NotebookLM 簡報背景示範範例（7分類 × 雙格式）
- 建立網頁版提示詞產生器（`prompt-generator.html`）
