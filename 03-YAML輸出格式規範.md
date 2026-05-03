# YAML 輸出格式規範

> 本文件定義 My Prompt Maker 的 YAML 提示詞輸出結構。Meta-Prompt 生成的 YAML 版本均需符合此規範，以確保可被程式解析、易於批次管理與版本控制。

---

## 完整 YAML 結構定義

```yaml
prompt:
  # ── 後設資料（必填）──────────────────────────────────
  meta:
    category: "分類代號與名稱"          # 必填，如 "A - 色彩系統"
    style_name: "設計主題名稱"          # 必填，如 "暗夜熔岩雙色對比"
    use_case: "使用場景簡述"            # 必填，如 "NotebookLM 16:9 簡報背景"
    ai_target:                         # 必填，可多選
      - "Claude"
      - "Gemini"
      - "ChatGPT"
      - "Midjourney"                   # 視覺生成工具
    version: "1.0"                     # 選填，版本號
    created: "2026-05-02"              # 選填，建立日期

  # ── 視覺設計（視覺提示詞必填）────────────────────────
  visual:
    color_system:
      primary: "主色（色名 + 色碼）"    # 必填，如 "深邃黑 #0A0A0A"
      accent: "強調色"                  # 必填，如 "霓虹青 #00FFE0"
      background: "背景底色"            # 選填
      secondary: "次要色"              # 選填
      gradient:
        direction: "漸層方向"          # 選填，如 "由左至右" / "放射狀"
        description: "漸層描述"        # 選填，如 "黑到青，透明度 85%"
      palette_type: "配色類型"         # 選填，如 "互補色" / "類比色" / "單色"

    texture:
      elements:                        # 必填，至少一項
        - "紋理元素1"                  # 如 "方形微型晶片"
        - "紋理元素2"                  # 如 "發光數據網格"
      opacity: "透明度描述"            # 必填，如 "微隱（10-20%）"
      scale: "尺寸描述"                # 選填，如 "微型 / 中型 / 大型"
      blend_mode: "疊加模式"           # 選填，如 "疊加（Overlay）/ 濾色（Screen）"

    lighting:
      type: "光線類型"                  # 必填，如 "霓虹燈光 / 全息投影光 / 環境漫射"
      effects:                         # 必填，至少一項
        - "光線效果1"                  # 如 "全息投影光暈"
        - "光線效果2"                  # 如 "冷色調高光"
      mood: "氛圍描述"                  # 必填，如 "科技感 / 神秘 / 溫暖"
      intensity: "光線強度"             # 選填，如 "強烈 / 柔和 / 微弱"

    composition:
      layout: "版式描述"               # 必填，如 "非對稱留白"
      focal_point: "視覺焦點位置"      # 選填，如 "右側三分之一"
      negative_space: "留白描述"       # 必填，如 "左側 40% 深負空間"
      depth_layers: "層次描述"         # 選填，如 "前景粒子 / 中景紋理 / 背景漸層"

  # ── 風格定義（必填）──────────────────────────────────
  style:
    aesthetic: "整體美學風格"          # 必填，如 "科技極簡主義"
    era: "時代感"                     # 選填，如 "近未來 / 現代 / 復古未來"
    mood:                             # 必填，2–4 個形容詞
      - "形容詞1"
      - "形容詞2"
    references:                       # 選填，風格參照
      - "參照風格或作品"               # 如 "Blade Runner 2049 視覺風格"

  # ── 技術規格（必填）──────────────────────────────────
  technical:
    resolution: "解析度"              # 必填，如 "8K" / "4K" / "1080p"
    aspect_ratio: "比例"              # 必填，如 "16:9" / "4:3" / "1:1"
    color_profile: "色彩空間"         # 選填，如 "sRGB" / "DCI-P3"
    midjourney_params: ""             # 選填，如 "--ar 16:9 --style raw --v 6.1 --quality 2"

  # ── 功能性需求（必填）────────────────────────────────
  functional:
    foreground_compatibility: "前景相容性說明"  # 必填
    safe_zones: "安全區域描述"                  # 選填，如 "邊緣 5% 不放關鍵元素"
    contrast_ratio: "對比度要求"               # 選填，如 "文字對比度 ≥ 4.5:1（WCAG AA）"
    text_color_suggestion: "建議文字顏色"      # 選填，如 "白色或冷灰色"

  # ── 自然語言版本（必填）──────────────────────────────
  natural_language: |
    完整的自然語言提示詞放在這裡。
    使用多行文字，精緻度對齊優質範例。
    建議 100–250 字。
```

---

## 必填 vs 選填欄位速查

| 欄位路徑 | 必填 | 說明 |
|---------|------|------|
| `meta.category` | 必填 | 分類代號 |
| `meta.style_name` | 必填 | 設計主題 |
| `meta.use_case` | 必填 | 使用場景 |
| `meta.ai_target` | 必填 | 目標 AI |
| `visual.color_system.primary` | 必填 | 主色 |
| `visual.color_system.accent` | 必填 | 強調色 |
| `visual.texture.elements` | 必填 | 紋理元素（陣列） |
| `visual.texture.opacity` | 必填 | 透明度 |
| `visual.lighting.type` | 必填 | 光線類型 |
| `visual.lighting.effects` | 必填 | 光線效果（陣列） |
| `visual.lighting.mood` | 必填 | 氛圍描述 |
| `visual.composition.layout` | 必填 | 版式 |
| `visual.composition.negative_space` | 必填 | 留白 |
| `style.aesthetic` | 必填 | 美學風格 |
| `style.mood` | 必填 | 氛圍形容詞（陣列） |
| `technical.resolution` | 必填 | 解析度 |
| `technical.aspect_ratio` | 必填 | 比例 |
| `functional.foreground_compatibility` | 必填 | 前景相容性 |
| `natural_language` | 必填 | 自然語言版本 |

---

## 多提示詞集合格式（examples/ 資料夾使用）

當同一個場景有多個分類的提示詞時，使用 YAML list 整合：

```yaml
# 標頭說明
collection:
  title: "集合名稱"                   # 如 "NotebookLM 簡報背景提示詞集合"
  use_case: "統一使用場景描述"
  created: "2026-05-02"
  total_prompts: 7

prompts:
  - category_id: "A"
    prompt:
      meta:
        category: "A - 色彩系統"
        style_name: "..."
        # ...完整 prompt 結構...

  - category_id: "B"
    prompt:
      meta:
        category: "B - 材質紋理"
        # ...

  # C ~ G 依此類推
```

---

## 常見錯誤與修正

| 錯誤 | 正確寫法 |
|------|---------|
| `elements: "晶片, 網格"` | `elements: ["晶片", "網格"]`（陣列用方括號） |
| `mood: 科技感, 神秘` | `mood: ["科技感", "神秘"]`（陣列需引號） |
| `resolution: 8K解析度` | `resolution: "8K"` |
| `aspect_ratio: 16比9` | `aspect_ratio: "16:9"` |
| 縮排不一致（混用 tab/空格） | 全部使用 2 個空格縮排 |
| `natural_language` 沒用 `|` 多行符號 | `natural_language: |` 後換行縮排 |
