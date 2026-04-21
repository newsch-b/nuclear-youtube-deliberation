# nuclear-youtube-deliberation

**台灣 YouTube 核能議題研究：提示詞、字典與編碼簿**

本 repo 釋出李宜靜（2026）碩士論文研究中使用的 LLM 提示詞、文本處理字典，以及人工編碼簿，供後續研究者重現或延伸使用。

---

## 研究摘要

本研究系統性分析台灣 YouTube 核能議題的論述結構與審議特徵（2018、2021、2025 年三次核能公投），蒐集 334 部影片與 223,691 則留言，採用大型語言模型進行論述框架與不文明性的自動化標注。

**主要發現**：
- 影片框架以「公共問責」（24.8%）與「失控科技與代價負擔」（22.4%）為主
- 整體不文明留言率達 51.74%，「公共問責」框架不文明率最高（65%）
- Granger 因果檢定顯示，留言量增加顯著帶動不文明留言增加（審議螺旋）

---

## 目錄結構

```
nuclear-youtube-deliberation/
├── README.md
├── prompts/
│   ├── video_stance_prompt.md      # 影片立場標注 prompt（claude-sonnet-4-6）
│   ├── video_frame_prompt.md       # 影片框架標注 prompt（9 類框架）
│   ├── comment_frame_prompt.md     # 留言框架標注 prompt（GPT-4.1-mini）
│   ├── incivility_prompt.md        # 不文明留言標注 prompt
│   └── iteration_log.md            # 提示詞迭代紀錄
├── dictionaries/
│   ├── recognition_corrections.csv # Whisper 誤辨對照表（21 種、934 處）
│   ├── stop_words.txt              # 詞頻分析停用詞
│   ├── reserved_words.txt          # CKIP 斷詞保留詞
│   └── nuclear_keywords.txt        # 留言主題篩選關鍵字庫
├── codebooks/
│   ├── frame_codebook.md           # 9 類框架人工編碼簿
│   └── incivility_codebook.md      # 不文明操作型定義與邊界案例
└── notebooks/
    └── reproducibility_example.ipynb  # 示範 notebook（預處理 + 框架 + 不文明標注）
```

---

## 使用說明

### Prompts

| 檔案 | 模型 | 任務 |
|------|------|------|
| `video_stance_prompt.md` | claude-sonnet-4-6 | 影片逐字稿立場判定（pro/anti/neutral） |
| `video_frame_prompt.md` | claude-sonnet-4-6 | 影片框架分類（9 類） |
| `comment_frame_prompt.md` | GPT-4.1-mini | 留言框架分類（同框架定義） |
| `incivility_prompt.md` | GPT-4.1-mini | 留言不文明二元標注（0/1） |

**模型選擇邏輯**：影片逐字稿文本較長且口語雜訊多，使用 Claude 以獲得較強的長文本推理能力（人機 κ = 0.85）；留言文本較短且數量龐大（22 萬筆），使用 GPT-4.1-mini 兼顧信度與成本效益。

### Dictionaries

| 檔案 | 內容 | 用途 |
|------|------|------|
| `recognition_corrections.csv` | 21 種 Whisper 誤辨詞對照 | 逐字稿後處理品質校正 |
| `nuclear_keywords.txt` | 核能主題關鍵字 | 從 22 萬筆留言中篩選核能相關留言 |
| `stop_words.txt` | 中文功能詞停用詞 | 詞頻分析前置過濾 |
| `reserved_words.txt` | 核能領域專有名詞 | CKIP 斷詞保留詞設定 |

### Codebooks

- **`frame_codebook.md`**：9 類框架的定義、包含/不包含範圍、邊界案例區分規則、範例
- **`incivility_codebook.md`**：不文明操作型定義（禮貌規範 + 民主規範）、邊界案例處理規則

---

## 信度

| 任務 | 比較對象 | 子集 | Cohen's κ |
|------|----------|------|-----------|
| 影片立場 | Human vs Claude | 全樣本 | 0.85 |
| 影片框架 | Human vs Claude | 高信心子集 | 0.79 |
| 留言框架 | Human vs GPT-4.1-mini | 高信心子集 | 0.83 |
| 不文明標注 | Human vs GPT-4.1-mini | 最佳策略 | 0.701 |

可接受門檻：κ ≥ 0.61

---

## 引用

```bibtex
@mastersthesis{lee2026nuclear,
  author  = {Lee, Yi-Jing},
  title   = {Nuclear Energy Controversy on {YouTube}: Frame Construction, Public Response, and Incivility Dynamics in Taiwan},
  school  = {Graduate Institute of Journalism, National Taiwan University},
  year    = {2026},
  month   = {April},
  address = {Taipei, Taiwan}
}
```

---

## 授權

本 repo 的提示詞、字典與編碼簿以 **CC BY 4.0** 授權釋出。使用時請引用上方論文資訊。
