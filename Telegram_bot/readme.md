
# Telegram 問題機器人 (Question Bot)

因為公司內部業務量逐漸增多，因此設置此telegram機器人，用以群發公告、檔案，以節省每日時間以及工作分配問題
會打包成exe方便同事們使用


## 功能特點

### 1. 問題文件轉發
- 自動將特定格式的 Excel 文件轉發至對應的客戶 Telegram 群組
- 支援按照文件名稱中的客戶名稱識別目標群組
- 自動追蹤轉發成功與失敗的文件

### 2. 群發訊息功能
- 根據預設的 Excel 文件內容向多個客戶群組發送訊息
- 支援多種發送模式：
  - 標題模式 (-t)：在訊息首行添加客戶名稱
  - 合併模式 (-m)：將同一客戶的多條訊息合併為一條發送
  - 檔案模式 (-f)：支援附加檔案

### 3. 使用者權限管理
- 僅允許預設的公司內部帳號使用機器人功能
- 防止未授權用戶訪問敏感功能
- 避免機器人啟動時有人惡意轉發
- 
### 4. 圖形化界面
- 提供簡潔的 GUI 界面操作機器人
- 實時顯示機器人運行日誌
- 設置問題數量並監控處理進度

## 使用方法

### 啟動機器人

1. 運行 `Question_bot.exe` 文件
2. 在圖形界面中輸入預期處理的問題數量
3. 點擊「啟動機器人」按鈕

### 機器人指令

機器人支援以下 Telegram 指令:

- `/help` - 顯示所有可用指令的說明
- `/check` - 查看目前設定的問題數量
- `/ID` - 獲取當前聊天的群組或使用者 ID
- `/reset` - 重設問題計數並重新載入群組 ID 數據
- `/gms` - 執行群發訊息功能，支援以下參數:
  - `-t [備註]` - 啟用標題模式，可選添加備註
  - `-m` - 啟用合併模式
  - `-f` - 啟用檔案模式

### 文件格式要求

1. **問題文件命名格式**:
   - 格式: `YYMMDD-客戶名稱-提問.xlsx`
   - 例如: `240101-ABC客戶-提問.xlsx`

2. **群發訊息檔案格式**:
   - Excel 檔案，包含「客戶」、「群發訊息」和「檔名」三個欄位
   - 存放於設定的 `群發訊息.xlsx` 路徑

3. **群組 ID 對應表**:
   - Excel 檔案，包含客戶名稱與對應的 Telegram 群組 ID
   - 用於將問題文件轉發至正確的客戶群組

## 系統架構

- `QuestionBot` 類: 實現主要的機器人功能
- `RedirectText` 類: 用於將控制台輸出重定向到 GUI 文本區域
- `Button` 類: 處理 GUI 按鈕事件

## 注意事項

- 機器人僅處理在啟動後收到的訊息
- 為避免 Telegram API 限制，機器人會在發送大量訊息時自動暫停
- 確保 Excel 文件格式正確，否則可能導致轉發失敗
- 使用前請確認所有路徑設置正確

## 故障排除

- 如果機器人無法啟動，請檢查 Token 是否正確
- 如果文件轉發失敗，請檢查文件命名格式和群組 ID 對應表
- GUI 界面會顯示錯誤訊息，有助於診斷問題

## 授權

此專案僅供內部使用，未經授權請勿外傳或商業使用。