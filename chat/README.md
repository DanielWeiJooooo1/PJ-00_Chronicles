# PJ-00 Chronicles Chat

這個目錄存在的目的，是讓未來的 day-side Session Log cutover 仍保有 `chat/` 路徑語意，符合目前 append helper 的授權規則。

在下列條件全部完成前，請不要把同日 active log 直接搬到這裡：

1. `Append-SessionNode.ps1` 已完成目標路徑驗證或更新。
2. Twin-Sync / Project-Hub Harness 與相關法典文件已同步改寫。
3. 有明確的 rollback 與 retention 規劃。

在此之前，這裡只是一個已存在的 future target，不是當前 active write lane。