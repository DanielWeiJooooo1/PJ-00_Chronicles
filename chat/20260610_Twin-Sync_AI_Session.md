# 20260610 13:52 Federal AI Session

請問我在三月份的時候，是怎麼執行 DP-ToolKit 的資料 insert 呢？
我有落地說明文件嗎？

===========================================================================================

# 13:53

在三月份執行 DP-ToolKit 的資料匯入時，您與 AI 團隊為了解決千萬筆（約 300MB）大型 CSV 檔案匯入所帶來的效能與記憶體問題，捨棄了早期的簡易作法，發展出一套極高效的寫入架構。以下是當時執行 Insert 的核心技術細節與對應的文件落地狀況：

### 一、 三月份執行 DP-ToolKit 資料 Insert 的核心技術實作

當時的資料匯入架構具備以下幾項關鍵的防線與技術決策：

1. **放棄 Dapper，改用原生的 `OracleBulkCopy`**
   初期技術團隊原本考慮使用 Dapper 的 `IEnumerable` 發送，但發現其底層仍是逐筆 Insert，會成為效能災難。因此最終改採 C# 原生的 `OracleBulkCopy` (Direct Path Load) 搭配 `DataTable` 進行極速批次寫入。當時針對批次大小進行了最佳化（GLS 頭檔表 1,000 筆/批、DTL 明細表 10,000 筆/批），實測寫入速度高達 **34,780 rows/sec**。
2. **串流讀取與連續性去重 (Panel-Scope Deduplication)**
   為防止 `OutOfMemoryException` (OOM)，系統採用 `StreamReader` 進行前向（Forward-only）逐行串流讀取。為了避免資料寫入時發生 PK 衝突 (`ORA-00001`)，實作了全域 `HashSet` 的去重邏輯，並將其生命週期綁定在同一個 `PANELID` (玻璃 ID) 內，一旦處理完一個 Panel 就會清除快取，將記憶體佔用完美壓制在極低水平。
3. **規避 `ORA-39831` 雙重前綴 Bug**
   在 `OracleBulkCopy` 執行時，若直接帶入 Schema 前綴會引發報錯。當時的解法是在程式啟動連線時，立刻執行 `ALTER SESSION SET CURRENT_SCHEMA = IEHM_IAS_SYS_DB` 鎖定命名空間，接著強制使用「不含 Schema 前綴的純表名」進行資料灌入。
4. **記憶體快取中英轉譯**
   針對 FDC DB 不支援儲存中文的限制，DP-ToolKit 會在啟動時載入 `MEA_EDC_ITEM_DICT` 建立 In-Memory 字典快取 (`ConcurrentDictionary`)。讀取到中文測項時，會以 $O(1)$ 的複雜度即時轉譯成英文代碼 (`ITEM_CODE`)，並加上 30 字元的長度截斷防線後再 Insert 到資料庫中。

### 二、 關於落地說明文件

**有的，這套機制不僅有完整的落地文件，甚至在近期（五月底）被正式提煉成了對外談判的「鋼鐵合約」。**

* **三月份的即時歷史紀錄：**
  在 3 月 10 日成功完成千萬筆大檔案生產級匯入測試後，您隨即透過 `doc-regulation` 技能將所有的技術成就落地。包括 `OracleBulkCopy` 架構選型、批次大小調優、`ALTER SESSION` 解決方案、效能基準等設計決策，都已完整寫入當時專案的 `README.md` (標記為 v2.1.7-prod 生產級狀態) 與 `NEXT_STEPS.md` 中，確保了從設計到驗證的全程可追溯性。
* **五月份的 OpenSpec 規格化升級：**
  為了因應六月份要與主管和客戶進行 API 串接與商業化落地的談判，您在五月底進行了一次大規模的歷史足跡萃取，將這些經驗法典化至 **PJ-26_DP-ToolKit** 的 Spectra (SDD) 規格書中：
  1. **`fdc-oracle-write-contract/spec.md`**：明確鎖定了 `OracleBulkCopy`、`DataTable`、`CURRENT_SCHEMA` 切換與純表名寫入的規則，並禁止未來新增的 Parser 覆寫此核心寫入合約。
  2. **`fdc-ingestion-pipeline/spec.md`** 與 **`design.md`**：將三月份實測的極速效能數據與防禦機制（如逐行讀取、錯誤 CSV 隔離）作為技術合約固化下來。
  3. **《資料處理微服務（DP-ToolKit）V3.0 規格書.md》**：這份主規格書也詳細記載了上述的欄位映射與輸出表格定義（包含 GLS 和 DTL 的對應關係），近期也成為您與團隊溝通第一版 API 設計的最重要參考文件。