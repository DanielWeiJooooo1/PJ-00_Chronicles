# 個人 AI 工作流程一頁作戰手冊 v0.1

最後更新：2026-06-06

## 目的

這份手冊是每天使用 AI 的固定入口。它不取代 Twin-Sync 法典、Spectra/OpenSpec、Skills 或 session log，而是把它們串成一個低摩擦的日常閉環：先定今日成果，再讓 AI 依證據工作，最後留下可追蹤的收口。

## 真實 SSOT

| 類型 | 權威位置 |
| --- | --- |
| Session log | `D:\Project\PJ-00_Chronicles\chat` |
| Chronicles 工作區 | `D:\Project\PJ-00_Chronicles` |
| Twin-Sync 實體 repo | `D:\Project\PJ-14_Twin-Sync` |
| Twin-Sync 狀態機 | `D:\Project\PJ-14_Twin-Sync\registry\state.yaml` |
| Agentic workflow 參考 | `D:\Project\PJ-14_Twin-Sync\docs\wiki\protocols\Agentic-Development-Workflow.md` |
| Federal sync 腳本 SSOT | `D:\Project\Skills\federal-sync\scripts\sync_federation.ps1` |

> 第一個流程修正點：舊規則若仍指向 `D:\Project\Twin-Sync\registry\state.yaml`，視為路徑漂移；目前應改用 `D:\Project\PJ-14_Twin-Sync\registry\state.yaml`。

## Start：每日開局

每天開始只回答三個問題：

1. 今天最重要的 1 個成果是什麼？
2. 這件事屬於哪個 repo / project？
3. 它需要規劃、執行、知識整理，還是同步收口？

開局檢查：

- 先讀本文件，再讀相關 repo 的 README / NEXT_STEPS / AGENTS 或 GEMINI。
- 涉及進度、治理或跨節點狀態時，讀 `PJ-14_Twin-Sync\registry\state.yaml`。
- 涉及 session 歷史時，只以 `PJ-00_Chronicles\chat` 為授權路徑。
- 若工作區現況和記憶衝突，先回報現況，再做最小、安全、可驗證的一步。

## Mission：任務循環

每個任務都走同一條路：

| 階段 | 行為 | 產物 |
| --- | --- | --- |
| Observe | 讀檔、看狀態、確認現況，不先腦補 | 已驗證事實、缺口、風險 |
| Plan | 收斂目標、Non-Goals、驗收方式 | 簡短計畫或 Spectra/OpenSpec 工件 |
| Execute Packet | 限定 allowed paths、forbidden paths、驗證命令、停止條件 | 可交給 AI 執行的邊界封包 |
| Verify | 跑測試、dry-run、檢查輸出或人工驗收 | Pass / Fail、剩餘 blocker、後續行動 |

任務分級：

- `Tiny`：小到可以直接做，但仍需驗證與回報。
- `Spec`：需求或風險不小，先進 Spectra/OpenSpec；先規格，後實作。
- `Skill`：同類任務重複第 3 次，不再靠臨時提示詞硬撐，改收斂成 skill、SOP 或腳本。
- `Sync`：涉及跨機、GitHub、GitLab、NotebookLM 或 Google Workspace 時，只走已驗證的同步邊界；不得把未驗證能力說成可用。

## Close：每日收口

每次任務結束，都留下三行結論：

```text
做了什麼：
怎麼驗證：
下次要不要流程化：
```

收口規則：

- Session log 寫入以 `D:\Project\PJ-00_Chronicles\chat` 為準。
- 更新文件時只改本輪必要路徑；Git 操作必須 path-scoped，禁止 `git add .`、`git add -A`、`git commit -a`。
- 失敗不能包裝成成功；改列 blocker、follow-up 或下一個 Tiny task。
- 若本輪產生可重用偏好、模板或操作規則，先記入 NEXT_STEPS，再評估是否技能化。

## Evolve：每週進化

每週只挑 1 個最高摩擦點處理，避免把流程改造本身變成新負擔。

判斷順序：

1. 能用文件說清楚嗎？寫成 one-pager / SOP。
2. 需要 AI 每次照固定邏輯做嗎？寫成 skill。
3. 需要穩定處理檔案、同步或驗證嗎？寫成腳本。
4. 成本大於收益嗎？明確放棄或移入 parking lot。

驗收標準：

- 5 分鐘內知道今天從哪裡開始。
- AI 不需要重新猜 repo、SSOT、流程邊界。
- 每次任務都有收口，不只留下長對話。
- 每週至少找出 1 個可以文件化、技能化、腳本化或放棄的摩擦點。