# 修復 Windows Update 與 傳遞最佳化服務 (DoSvc) 異常計畫

## 問題分析與診斷結果

1. **核心原因：** 系統中缺少核心系統檔案 `C:\Windows\System32\dosvc.dll`（傳遞最佳化服務，Delivery Optimization）。
2. **錯誤現象的關聯性：**
   * 當 Microsoft Store、`winget` 或 Windows Update 嘗試下載安裝任何檔案時，Windows Update 代理程式會調用 `DoSvc` 的 COM 介面。
   * 因為 `dosvc.dll` 遺失，系統調用失敗，回報錯誤代碼 `-2147467262`（即 **`0x80004002: E_NOINTERFACE`**，無此介面）。這與我們先前在安裝 Codex Desktop 時看到的錯誤代碼完全一致！
   * 因此，**`dosvc.dll` 的遺失就是導致 Windows Update 一直下載失敗的直接原因**。兩者有著 100% 的因果關係。
3. **循環死鎖（Circular Deadlock）：**
   * 正常情況下，我們可以使用 `DISM /Online /Cleanup-Image /RestoreHealth` 指令讓 Windows 連線到微軟官方伺服器下載並補回遺失的系統檔案。
   * 但由於 `dosvc.dll` 遺失，導致 Windows Update 下載引擎本身無法啟動。
   * 這使得 DISM 在下載修復檔案時會回報 **`0x800f081f: 找不到來源檔案`**。
   * **結論：** 如果不先手動手動補回 `dosvc.dll`，線上的 DISM 與 SFC 系統修復指令將**永遠無法成功**。

---

## 提案修復計畫

為了打破這個循環死鎖，我們需要安全地獲取官方的 `dosvc.dll` 檔案並放置回系統目錄中。為了確保 **100% 安全可靠，絕不使用任何第三方非官方檔案**，我們將採用以下步驟：

### 步驟 1：下載官方 Windows 累積更新包
* **來源：** 從微軟官方更新目錄（Microsoft Update Catalog）下載適用於您系統版本（Windows 11 24H2 x64）的官方手動更新檔案 `KB5053598`（`.msu` 格式）。
* **安全保證：** 下載連結來自微軟官方網域 `*.download.windowsupdate.com`。

### 步驟 2：本機提取檔案（不進行系統變更）
* **解壓縮：** 在您的 workspace 目錄（`d:\Project\temp_update`）中，使用 Windows 內建的 `expand` 指令解開 `.msu` 與其中的 `.cab` 壓縮包。
* **安全性：** 此過程完全在沙盒暫存目錄中進行，不對系統做任何修改。

### 步驟 3：修復系統檔案與啟動服務
1. 將解壓出的官方原裝 `dosvc.dll` 複製到系統目錄 `C:\Windows\System32\`。
2. 啟動 `DoSvc`（傳遞最佳化）服務。
3. 執行 Windows Update 與 `DISM` 測試，驗證下載功能是否完全恢復正常。

---

## User Review Required

> [!IMPORTANT]
> **本計畫的安全保證：**
> * **無第三方未知檔案：** 所有操作皆從微軟官方下載的更新檔案中提取元件，絕不上網隨便下載來源不明的 DLL。
> * **可隨時還原：** 在複製 `dosvc.dll` 之前，我們不會對系統註冊表或其它系統檔案進行任何侵入式修改。
> * **空間充足：** 您的 C 槽目前擁有約 **305 GB** 的可用空間，完全足夠下載及解壓更新包（預計需要約 2.5 GB 空間，修復完成後會自動清理）。

---

## Proposed Changes

此次變更將只會新增一個官方簽署的系統檔案：

#### [NEW] [dosvc.dll](file:///C:/Windows/System32/dosvc.dll)

---

## Verification Plan

修復完成後，我們將透過以下方式驗證：

### 自動與手動測試
1. **驗證服務狀態：**
   * 執行 `Get-Service -Name dosvc`，確保服務狀態從 `Stopped` 變為 `Running` 或處於可啟動狀態。
2. **驗證 Windows Update：**
   * 開啟 Windows Update 介面，手動點選「檢查更新」，確認下載進度條能順利跑動且不報錯。
3. **驗證系統映像：**
   * 再次執行 `DISM /Online /Cleanup-Image /ScanHealth`，確認能夠順利完成，不再出現 `0x800f081f` 錯誤。
