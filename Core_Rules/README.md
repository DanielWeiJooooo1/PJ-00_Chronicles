# Core Rules

這個目錄是 `PJ-00_Chronicles` 的核心 SSOT 承載區。

## 目錄用途

- `CORE_RULES.md`：全域最高原則與拓樸規則
- `profiles/`：專案層 profile，供各 repo wrapper 引用

## 維護原則

- 先改 `CORE_RULES.md`，再改各 repo wrapper。
- profile 只放專案層資訊，不放全域原則。
- 若某段內容已經影響到所有專案入口，就應提升回 `CORE_RULES.md`，而不是複製到每個 wrapper。
- `Spectra` 若成為預設流程，應寫在 `CORE_RULES.md`，不是藏在單一 repo 的入口檔。

## 引用方式

典型順序是：

1. 先讀 `CORE_RULES.md`
2. 再讀對應專案 profile
3. 最後才讀 repo-local wrapper 與當輪 workflow 文件

## 與技能 profile 的關係

- `D:\Project\Skills\doc-regulation\references\profiles\` 保持 skill 專用語意。
- 這裡的 `profiles/` 只負責 agent / instruction 入口的專案層 profile。
- 兩邊若有重疊，優先用 pointer，不做全文雙寫。
