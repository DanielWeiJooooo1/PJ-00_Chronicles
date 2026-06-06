# PJ-00 Chronicles Agent Entry

這個 repo 的第一入口是 [AI_Workflow_OnePager.md](./AI_Workflow_OnePager.md)。

## 開局順序

1. 先讀 [AI_Workflow_OnePager.md](./AI_Workflow_OnePager.md)
2. 再讀 [NEXT_STEPS.md](./NEXT_STEPS.md)
3. 若是今天的 session，讀 `chat/` 底下最新的 `yyyyMMdd_Twin-Sync_AI_Session.md`

## 工作原則

- 只把 `PJ-00_Chronicles\chat` 當作 session log 權威位置。
- 有 workflow 漂移、路徑漂移或工具邊界漂移時，先記錄現況，再做最小可驗證修正。
- 任務收口時，優先留下三行結論：做了什麼、怎麼驗證、下次要不要流程化。
- Git 操作維持 path-scoped，不使用 `git add .`、`git add -A` 或 `git commit -a`。

## 這個 repo 的角色

`PJ-00_Chronicles` 是紀錄與收口工作區，不是新的法典本體。真正需要跨 repo 的治理、狀態與協定，仍以 `PJ-14_Twin-Sync` 與其對應文件為準。
