# PJ-00 Chronicles

## 角色

PJ-00 Chronicles 是 Session Log 的非 bridge 歷史保留與 cutover 預備區，不是 GitHub 發佈 repo，也不是目前 day-side active log 的強制寫入點。

## 2026-05-11 現場定錨

- `D:\PersonalOS\scripts\Append-SessionNode.ps1` 目前只允許包含 `chat`、`chatHistory` 或 `projects` 的路徑，並會拒絕 `github-bridge`。
- 因此 `PJ-00_Chronicles\chat\` 被建立為未來可用的安全 target，但 day-side active Session Log 暫時仍維持在 `D:\PersonalOS\projects\PJ-14_twin-sync-bridge\chat\`。
- 未經 helper、Harness 與法典引用同步 cutover 前，不得盲目搬移同日 active log。

## 現況

- `chat/`：future active / archive target
- `chat/archive/`：預留給跨日或已完成切換契約後的歷史 log
- `chat/20260515_Twin-Sync_AI_Sessions.snapshot.md`：2026-05-15 目錄整併時建立的本地 snapshot mirror；active write path 仍以 `D:\PersonalOS\projects\PJ-14_twin-sync-bridge\chat\` 為準

## 備註

本目錄目前只完成結構預備與真相定錨，尚未進行歷史 Session Log 批次搬遷。