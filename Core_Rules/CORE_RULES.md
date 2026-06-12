# Core Rules SSOT

`Core_Rules` 是 `PJ-00_Chronicles` 底下的核心單一真相來源。所有專案入口都應引用這份文件，而不是各自重寫全域原則。

## 核心原則

1. **SSOT 優先**
   - 每一層資訊只保留一份清楚的權威來源。
   - 先找 canonical source，再看副本或派生文件。
   - 如果文件、狀態或規則重疊，優先收斂，不要讓多份版本並存。

2. **人類決策，AI 協作**
   - 人類負責定目標、做裁決、確認風險。
   - AI 負責盤點、推演、整理、執行與回報。
   - 遇到模糊地帶、未定義情況、權限不足或重大風險時，先停下來回報，不要腦補。

3. **PEGT**
   - 先觀察，再提出假設，再驗證，最後執行。
   - 沒有證據，不先動手。
   - 變更前先盤點，變更後要能驗證結果。

4. **降低摩擦力**
   - 只要流程證明有價值，就把它文件化、技能化或腳本化。
   - 同類操作重複第三次以上，不要再靠臨時提示詞硬撐。
   - 能讓未來自己一鍵接手的，就不要維持在高摩擦手工狀態。

5. **區分事實與提案**
   - 已驗證事實、推測、設計提案、待決事項要分開寫。
   - 不把暫時方案寫成永久規則。

6. **預設採用 Spectra / SDD**
   - 需要規劃、提案、設計、變更時，優先使用 Spectra 驅動的流程。
   - 若某個專案不走 SDD，必須在對應 profile 明示例外與替代流程。
   - `Spectra` 是核心工作方式，不是單一 repo 的私有習慣。

## 拓樸規則

- `Core_Rules` 是全域核心 SSOT。
- 各 repo 的 `AGENTS.md`、`GEMINI.md`、`CLAUDE.md` 只當薄 wrapper，不重寫核心原則。
- `profiles` 第一版只做專案層，不承載機器層或任務層。
- runtime payload、一次性 task packet、session-specific data 不屬於這一層。
- `doc-regulation` 的技能 profile 系統維持獨立，不在這一輪合併。

## Wrapper 合約

薄 wrapper 應只做這些事：

- 指向 `CORE_RULES.md`
- 指向對應專案 profile
- 補少量 repo-local facts
- 補少量工具 / 流程差異
- 明示若與核心規則衝突，以核心規則為準

## Profile 合約

專案 profile 只承載：

- 專案定位
- canonical read order
- repo-local SSOT / state / tracker 路徑
- 專案特有的工作邊界
- 專案特有的 instruction / workflow 入口
- 專案特有的禁止事項
- 專案是否採用 Spectra / 若否則說明替代流程

專案 profile 不承載：

- 全域最高原則
- persona 劇本
- 一次性 task packet
- runtime payload
- 機器層差異
