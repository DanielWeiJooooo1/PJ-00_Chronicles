# PJ-00 Chronicles

最後更新：2026-05-29 16:51

## Objective

- 管理 `D:\Project\PJ-00_Chronicles` 下的 session log 與正式報告產物。
- 本 repo 是 Chronicles / reports 工作區，不作 bridge repo 或對外發佈用途。

## Topology

- `chat/`：session log 與歷史紀錄。
- `README.md`：專案總覽。
- `NEXT_STEPS.md`：立即行動與已完成事項。

## Index

- 目前以 `chat/` 為主；`reports/` 已退場，需新報告時再重建。

## Constraints

- Session log 授權路徑以 `D:\Project\PJ-00_Chronicles\chat\` 為準。
- 文件封裝採 path-scoped stage / commit，不得捲入無關 dirty worktree。
- 報告輸出以主管可讀、可列印、可轉 PPT 為優先。

## Recent Notes

### 2026-05-28 20:05

- `D:\Project\Skills\federal-sync\scripts\sync_federation.ps1` 已升格為唯一 SSOT；`PJ-14` repo-local path 改為 compatibility wrapper，舊 `sync_federal_laws.ps1` 已移入 archive。
- heartbeat runtime 已原生納入 `PJ-00_Chronicles`，push 改以 upstream-derived explicit refspec 處理 `master -> origin/main`，不再依賴手動補 push。
- Twin-Sync Wiki 已新增 lesson，記錄這次「skill contract 存在，但真正 runtime script 不在 skill folder」造成的 hidden backend drift。

### 2026-05-28 17:16

- 已用 bridge v2 `sync_federation.ps1` 完成 `PJ-14_Twin-Sync` safe pull；Twin-Sync ff-only 拉下 1 commit，`Skills` 確認 already current。
- `PJ-00_Chronicles` 已完成該輪 doc-regulation 收口，準備將當日 session log 與 `README.md` / `NEXT_STEPS.md` 一併推上 GitHub。
- 當時觀察到 repo-local `PJ-14_Twin-Sync\tools\sync_federation.ps1` 仍屬 legacy candidate；`PJ-00_Chronicles` 也仍需 explicit refspec 才能安全推到 `origin/main`。

### 2026-05-28 17:45

- `reports/` 目錄（3 files）已正式移除並推上 GitHub（commit `cb402eb`）。
- `chat/20260527_Twin-Sync_AI_Session.md` 已加入 tracking，與 20260515–20260527 歷史 session log 一起推上雲端（commit `635ac2b`）。
- `.git/info/exclude` 的忽略規則已清除，`chat/20*_Twin-Sync_AI_Session*.md` 恢復可追蹤狀態。
- doc-regulation 收口：`README.md` 與 `NEXT_STEPS.md` 已同步更新。

### 2026-05-27 10:08

- 釐清 `chat/` 底下的 `yyyyMMdd_Twin-Sync_AI_Session*.md` 應保持可追蹤，方便後續同步到雲端。
