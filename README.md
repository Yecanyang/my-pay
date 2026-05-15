# 💰 雲端理財生存戰 4.1 (公版)

這是一個結合 **GitHub Pages** 與 **Google Sheets** 的輕量化理財系統。支援 365 天存錢挑戰與即時雲端同步，資料完全儲存在您自己的 Google 雲端空間。

---

## 🚀 快速開始 (3步驟設定)

為了確保數據能安全地存入您的雲端，請先完成以下設定：

### 1. 建立雲端資料庫
* 開啟一個新的 [Google 試算表](https://sheets.new/)。
* 點擊上方選單：**擴充功能** > **Apps Script**。

### 2. 植入同步腳本
* 將原本的內容清空，貼入以下代碼：

```javascript
function doGet(e) {
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getSheets()[0];
  var data = sheet.getRange("A1").getValue();
  return ContentService.createTextOutput(data || "{}").setMimeType(ContentService.MimeType.JSON);
}

function doPost(e) {
  var params = JSON.parse(e.postData.contents);
  var ss = SpreadsheetApp.getActiveSpreadsheet();
  var sheet = ss.getSheets()[0];
  sheet.getRange("A1").setValue(JSON.stringify(params.data));
  return ContentService.createTextOutput(JSON.stringify({"result":"success"})).setMimeType(ContentService.MimeType.JSON);
}
