# Economics test（專案藍圖）
> 本檔為跨 Agent 通用的專案藍圖（AGENTS.md 開放標準）。

## 專案簡介
考試題庫

## 關鍵時程
- 2026/10/10：期限

## 目標與路線圖
- [ ] 整理現有經濟學題庫資源
- [ ] 建立題庫分類與檢索系統
- [ ] 補充缺失題目與解答

## 資料夾結構
```
Secondbrain/
├── Projects/
│   └── economics-exam-bank/
├── .obsidian/
└── AGENTS.md
```

## 同步層級
| 層級 | 平台 | 位置 | 讀取時機 |
|------|------|------|---------|
| L1 | 本地 | AGENTS.md + handoff.md | 每個 session |
| L2 | GitHub | https://github.com/carloschen694/ntpu-economics-exam | 指定時 |
| L3 | Obsidian | vault 根目錄 | 有需要時 |

## 獨立專案
- `Projects/economics-exam-bank/` 有自己的 repo（carloschen694/economics-exam-bank），vault 不追蹤其內容

## 工作約定
- 開工先讀 handoff.md，收工必更新 handoff.md
- 所有回應與文件使用繁體中文

## 安全與隱私
- 不把 API key 寫進 repo，一律放 .env 並列入 .gitignore
