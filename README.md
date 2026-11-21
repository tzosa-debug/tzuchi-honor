# 慈濟國小｜生活榮譽競賽線上評分與管理系統

本系統專為**慈濟高級中學國民小學部**學務處與導護老師設計，用於即時辦理每週巡堂評分、服裝儀容抽檢、各年級成績統計與榮譽榜海報產生。

- **線上系統網址**：[https://tzosa-debug.github.io/tzuchi-honor/](https://tzosa-debug.github.io/tzuchi-honor/)
- **後端端點**：Google Apps Script Web App (`/exec`)
- **檔案資料存取**：Google Drive (`tzuchi_honor_db.json`)

---

## 📌 系統特色

1. **行動友善與離線快取**
   - 支援手機、平板與桌機操作，自動適應 safe-area 邊界。
   - 內建 `localStorage` 本機暫存機制，即使網路短暫中斷也不會遺失評分紀錄。

2. **完整評分與抽檢機制**
   - **巡堂評分**：提供環境整潔與秩序禮貌項目的點擊加扣分、自訂基準分與評分次數（第 1～4 次）。
   - **服儀抽檢**：支援隨機抽檢項目（領結、髮飾、皮帶、鞋子、指甲等），依未通過人數自動計算加減分（+2 ~ -2 分），並具備防竄改鎖定與解鎖機制。

3. **成績自動整合與匯出**
   - 每週自動彙整各年級「環境整潔獎」與「秩序禮貌獎」最終成績。
   - 內建海報生成與 SheetJS 報表匯出功能，可直接產出 Excel（`.xlsx`）成績明細。

4. **雲端雙向同步**
   - 搭配 Google Apps Script（`.gs`）以 RESTful 方式進行 JSON 格式之 `GET` / `POST` 讀寫，防範多人併發覆蓋。

---

## 🏗️ 系統架構

```
[使用者 / 老師 (手機/電腦)]
        │
        ▼ (開啟靜態網頁)
[GitHub Pages (index.html)]
        │
        ▼ (fetch API - GET / POST)
[Google Apps Script (/exec)]
        │
        ▼ (DriveApp API)
[Google 雲端硬碟 (tzuchi_honor_db.json)]
```

---

## 🚀 部署與啟用指南

### 1. 後端部署（Google Apps Script）

1. 開啟 [Google Apps Script](https://script.google.com/) 並貼入專案程式碼（`程式碼.gs`）。
2. 設定目標 Google 雲端硬碟資料夾 ID (`FOLDER_ID`)。
3. 點擊右上角 **部署** ➔ **管理部署作業** ➔ **新增部署作業**：
   - **類型**：網頁應用程式 (Web App)
   - **執行身分**：我 (Me)
   - **誰可以存取**：所有人 (Anyone) 或 學校網域成員 (Anyone within tcsh.tn.edu.tw)
4. 複製部署完成後取得的 **/exec 端點網址**。

### 2. 前端部署（GitHub Pages）

1. 確保儲存庫根目錄包含 `index.html`。
2. 進入 GitHub Repository ➔ **Settings** ➔ **Pages**：
   - **Source**: Deploy from a branch
   - **Branch**: `main` / `root`
3. 存檔後等待約 1–2 分鐘即可完成發布。

### 3. 雲端同步設定

1. 打開 GitHub Pages 系統網址：`https://tzosa-debug.github.io/tzuchi-honor/`
2. 點擊右上角 **行政管理後台**。
3. 在 **「雲端同步網址設定」** 貼上 Apps Script 的 `/exec` 網址並點擊 **「儲存網址」**。
4. 按下 **「測試讀取雲端」** 驗證連線狀況。

---

## 🛠️ 維護與設定說明

- **週次與導護建立**：於「行政管理後台」➔「新增週次」設定每週起訖日期與正/副導護老師姓名。
- **班級數調整**：各年級可自由切換 4 班或 5 班（預設帶入知足、感恩、善解、包容、合心）。
- **校徽設定**：可於管理後台填入學校 SVG/PNG 校徽網址，即時更新全站表頭與海報標誌。

---

## 📄 授權與版權

臺南市私立慈濟高級中學國民小學部 學務處 版權所有 © 2026.
