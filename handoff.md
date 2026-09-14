# 交接檔（handoff.md）
> 任何 Agent、任何電腦接手前必讀；收工時必更新。

## ⏯️ 目前做到哪
三層初始化完成：L1 本地藍圖＋交接檔、L2 GitHub 私有 repo、L3 Obsidian MCP 設定。

## 🚦 目前狀態
- L1 ✅ AGENTS.md + handoff.md 已建立
- L2 ✅ repo：carloschen694/ntpu-economics-exam（私有，main 已推 4 個 commit）
- L3 ✅ 安裝 @bitbonsai/mcpvault v0.16.0，opencode.jsonc 已加 mcp.obsidian，專案工作流程.md 已建
- ⏳ 尚未重啟 opencode → MCP 工具未載入

## ➡️ 下一步
1. 重啟 opencode 確認 obsidian MCP 工具載入
2. 整理 Projects/economics-exam-bank 現有題庫資源（113/114/115 微觀）
3. 確認題庫分類與檢索需求

## ⚠️ 注意事項
- 路徑含「雲端硬碟」，確認雲端同步圖示已打勾
- 已設 `git config windows.appendAtomically false`
- 敏感檔已排除：.claude/settings.local.json、.obsidian/plugins/obsidian-local-rest-api/data.json
- Projects/economics-exam-bank 為獨立 repo，vault 不追蹤
- mcpvault 位於 C:\nvm4w\nodejs\mcpvault.cmd（nvm 版本切換可能改路徑）
- Untitled 1.canvas 有未 commit 變動（Obsidian 自動產生），收工時保留未處理

## 🕐 最後更新
- 時間：2026-09-14 22:56
- 更新者：opencode @ WH-26112-NB
- Git push：待推（灰色案，未含 Untitled 1.canvas）