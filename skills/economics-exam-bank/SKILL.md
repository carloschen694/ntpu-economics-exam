---
name: economics-exam-bank
description: 經濟學研究所歷屆考題整理、答案計算、LaTeX 數學解析編寫、SQLite 資料庫同步與網頁/CLI 驗收工作流程。當使用者提及「題庫整理」、「答案解析」、「經濟學考題」、「驗收系統」或相關工作時載入此 Skill。
---

# 經濟學研究所考古題庫處理與驗收工作指引 (economics-exam-bank)

本技能提供經濟學研究所歷屆考題之資料整理、LaTeX 數學推導解析撰寫、SQLite 資料庫結構化同步、多維度 API/CLI 檢索以及前端網頁驗收的標準作業程序 (SOP)。

---

## 1. 🔄 開工與收工規範 (Workflow Convention)

- **開工 SOP**：
  1. 閱讀 Vault 根目錄之 [handoff.md](file:///g:/我的雲端硬碟/Secondbrain/handoff.md) 與 [AGENTS.md](file:///g:/我的雲端硬碟/Secondbrain/AGENTS.md)。
  2. 檢查獨立專案 `Projects/economics-exam-bank/` 之資源檔與資料庫狀態。
- **收工 SOP**：
  1. 確認資料庫中所有考題之解答與解析完全寫入。
  2. 檢查 `git status`，確保工作區乾淨。
  3. 更新 [handoff.md](file:///g:/我的雲端硬碟/Secondbrain/handoff.md)，記錄當前進度、狀態與下一步。

---

## 2. 📐 解答計算與 LaTeX 數學解析撰寫標準

撰寫題目之 `answer` 與 `explanation` 時，需遵照以下 Markdown & LaTeX 規範：

1. **標準答案 (`answer`) 格式**：
   - 複選題：`A, C, E`
   - 計算申論題：`(a) P = 65.22, q1 = 21.74; (b) P = 70, q1 = 20, 每家利潤 750`
2. **詳細推導 (`explanation`) 格式**：
   - 使用 Markdown 結構（`【主題標頭】`、`1. 2. 數字標號`、`小項清單`）。
   - **數學算式語法**：
     - 行內公式（Inline Math）：使用單字號 `$`，例如 `$MRS_{xy} = \frac{MU_x}{MU_y} = \frac{3}{2}$`。
     - 獨立區塊公式（Display Math）：使用雙字號 `$$` 另起一行，例如：
       $$MRS_{xy} = \frac{MU_x}{MU_y} = \frac{1}{2\sqrt{x}} = \frac{P_x}{P_y} = \frac{3}{2}$$
   - 包含經濟意涵與福利效果剖析。

---

## 3. 🗄️ 資料庫同步與防錯設計 (Database & Import SOP)

- **絕對路徑連線配置 (`config.py`)**：
  為避免執行指令時工作目錄改變（如 `src/` 與專案根目錄切換）導致 SQLite 相對路徑 `./economics_exam.db` 讀取到空白資料庫，`config.py` 必須固定為絕對路徑：
  ```python
  from pathlib import Path
  BASE_DIR = Path(__file__).resolve().parent.parent.parent
  DEFAULT_DB_PATH = BASE_DIR / "economics_exam.db"
  DATABASE_URL = f"sqlite:///{DEFAULT_DB_PATH.as_posix()}"
  ```
- **匯入邏輯修復 (`import_exam_data.py`)**：
  更新題目時，必須確保 `question.answer` 與 `question.explanation` 被一併同步更新：
  ```python
  if question:
      question.answer = item.get("answer") or None
      question.explanation = item.get("explanation") or None
      session.add(question)
  ```
- **舊 Sample 假資料清理**：
  若資料庫中存在預設或範例產生之無意義/無答案測試題目（如 `NationalTaiwanUniversity` 測試頁），需撰寫 Cleanup 腳本定期刪除，維持 100% 正確率。

---

## 4. 🔍 多維度 API 與 CLI 檢索擴充

- **API 檢索優化 (`/api/v1/questions`)**：
  - 支援 `year`, `school`, `tag`, `question_type` (相容中文如「複選題」與英文代碼) 查詢。
  - **全欄位模糊搜尋 (`keyword`)**：搜尋關鍵字時應同時涵蓋 `content`, `tags`, `answer`, `explanation` 四個欄位，提高檢索靈敏度。
- **CLI 查詢工具 (`scripts/query_questions.py`)**：
  - 支援命令行參數：`--year`, `--tag`, `--keyword`, `-s` (顯示解答解析)。

---

## 5. 🌐 視覺化網頁驗收系統部署 (Web UI Verification)

- **前端介面 (`static/index.html`) 引擎配置**：
  - 引入 **Marked.js**：自動將解析轉為 HTML Markdown 格式。
  - 引入 **KaTeX Auto-Render**：自動掃描 `$$...$$` 與 `$...$` 並渲染為高品質數學算式。
  - **一鍵展開答案**：使用者可點擊「📖 檢視標準答案與詳細推導解析」瀏覽推導細節。
  - **重置與防呆提示**：無檢索結果時自動提示可搜尋的年份區間並提供重置按鈕。
- **FastAPI 路由掛載 (`main.py`)**：
  ```python
  app.mount("/static", StaticFiles(directory=STATIC_DIR), name="static")
  @app.get("/web")
  def web_ui():
      return FileResponse(STATIC_DIR / "index.html")
  ```
- 瀏覽器開啟 [http://127.0.0.1:8000/web](http://127.0.0.1:8000/web) 即可直觀驗收。
