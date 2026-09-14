---
category: project
created: 2026-09-12
project: economics-exam-bank
status: in-progress
tags:
  - project
  - economics
  - exam-bank
  - backend-api
  - fastapi
updated: 2026-09-13
---

# 經濟學研究所考試題庫 & 經濟學考試練習 (economics-exam-bank)

- **專案類型**：API 後端服務
- **專案狀態**：🟢 開發中 (MVP 基礎架構已完成)
- **儲存庫**：https://github.com/carloschen694/economics-exam-bank
- **專案路徑**：`G:\我的雲端硬碟\Secondbrain\Projects\economics-exam-bank`
- **主要考科**：
  - 個體經濟學 (Microeconomics)
  - 總體經濟學 (Macroeconomics)
  - 統計學與計量經濟學 (Statistics & Econometrics)

---

## 🎯 專案目標與定位
為報考國內外經濟學研究所之考生，打造集中化的考古題題庫與練習測驗 API 服務：
1. **考古題資料庫**：支援台大、政大、清大、交大等歷年題目與詳細解答。
2. **主題式檢索與標籤**：依知識點分類（如：Solow 成長模型、賽局 Nash 均衡、計量 OLS 估計性質）。
3. **測驗與統計 API**：提供即時測驗作答、批改、解析回傳與個人弱點分析。

---

## 📅 開發里程碑與待辦清單 (Roadmap & TODO)

- [x] 專案基礎建設：初始化 Git、GitHub 儲存庫、ANTIGRAVITY.md 與 README.md
- [x] 後端技術棧選型與建置：FastAPI + Pydantic + SQLModel + uv 套件管理
- [x] 核心資料模型建立：Exam（試卷）、Question（題目含 LaTeX、題型、解析、標籤）
- [x] 核心 API 路由實作：
  - `/api/v1/health`：健康檢查
  - `/api/v1/exams`：試卷 CRUD 與多條件檢索
  - `/api/v1/questions`：題目 CRUD、關鍵字與標籤過濾
  - `/api/v1/practice`：隨機題目練習、作答批改與解析回傳
- [x] 整合測試：通過 Pytest 單元與整合測試
- [x] 題庫批次匯入工具（支援 Markdown / JSON 檔案批次匯入歷屆考題，提供 `scripts/import_exam_data.py` 與 `/api/v1/import` API）
- [x] 擴充真實題庫資料（已完成國立臺北大學經研所 113-115 年個體經濟學共 25 題建檔匯入，各年試卷總分均為 100 分）
- [ ] 擴充其他學校題庫資料（台大、政大經研所考古題建檔）
- [ ] 前端介面或串接規劃

---

## 📝 開發記錄與踩坑筆記
- **2026-09-13**：
  - 完成歷屆考題批次匯入工具實作 (`scripts/import_exam_data.py`)。
  - 成功整合 `D:\antigravity\economics-test\research_downloads` 歷屆試題資源（113、114、115 年個體經濟學共 25 題）：
    - 113 學年度：12 題（包含選擇題選項、LaTeX 公式與配分，總分 100 分）
    - 114 學年度：7 題（包含賽局、寡占 Cournot/Cartel、道德風險等大題與子題，總分 100 分）
    - 115 學年度：6 題（包含偏好理論、立法賽局、R&D Cournot、CEO 激勵等申論分析題，總分 100 分）
  - 所有題目均已寫入 SQLite 資料庫 `economics_exam.db`，並在 `data/import/ntpu_micro_113_115.json` 建立結構化備份檔。
  - 修復 `python-multipart` 依賴缺失問題，Pytest 單元測試維持 100% 通過。
- **2026-09-12**：
  - 完成專案初始化，配置於 `Projects/economics-exam-bank`，建立公開 GitHub Repo。
  - 採用 `uv` 建立 Python 3.12 虛擬環境，安裝 FastAPI、Uvicorn、SQLModel、Pydantic。
  - **踩坑注意**：SQLModel 關聯模型在跨檔案字串型別提示時，需留意 Python 3.12 `from __future__ import annotations` 會將型別提示轉為純字串導致 SQLAlchemy mapper 解析失敗。已整合為標準 `entities.py` 與 `typing.Optional` / `List` 處理。
  - 完成測試套件 `tests/test_api.py`，通過 100% 測試。
