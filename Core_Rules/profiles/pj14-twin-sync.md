# Profile: PJ-14 Twin-Sync

> 這是 `PJ-14_Twin-Sync` 的專案層 profile。全域原則請先讀 `D:\Project\PJ-00_Chronicles\Core_Rules\CORE_RULES.md`。

## 專案定位

- `Twin-Sync` 是 GitHub bridge / 公開治理 repo，不是日間完整 PJ-14 SSOT。
- 日間 canonical source of truth 仍在 5P 的 PJ-14；本 repo 只承接已裁決可同步的 law、OpenSpec、Wiki、state 與公開治理事實。
- 若 routing、heartbeat 或 publication boundary 仍在 review，中途不得把 `Twin-Sync` 說成唯一治理權威。

## Canonical Read Order

1. `D:\Project\PJ-00_Chronicles\Core_Rules\CORE_RULES.md`
2. `D:\Project\PJ-00_Chronicles\Core_Rules\profiles\pj14-twin-sync.md`
3. `D:\Project\PJ-14_Twin-Sync\AGENTS.md`
4. `D:\Project\PJ-14_Twin-Sync\GEMINI.md`
5. `D:\Project\PJ-14_Twin-Sync\registry\state.yaml`，當任務碰到進度、治理或跨節點狀態時再讀
6. `D:\Project\PJ-14_Twin-Sync\docs\wiki\protocols\Instruction-Hierarchy-Protocol.md`，當要改 instruction / prompt / harness surface 時再讀

## 工作邊界

- 這個 repo 只承接已裁決可同步的內容，不承接未定案的全域治理。
- 專案特有的流程、路徑與狀態，應該留在 repo-local 文件與 state 中。
- 若某段內容開始影響所有 repo 入口，就回寫到 `CORE_RULES.md`，不要只放在這份 profile。
- `Spectra` 視為預設 SDD 流程；若未使用，需在本 profile 或 repo wrapper 明示替代流程。

## 禁止事項

- 不要把 runtime payload、一次性 task packet 或 session-specific data 寫進這份 profile。
- 不要把 persona 劇本或機器層差異寫進這份 profile。
- 不要把全域原則在這裡再重寫一遍。
