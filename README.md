# LOOTANIA 天賦模擬

天賦配點模擬器（GitHub Pages 靜態網站）。

## 檔案結構
```
index.html              模擬器頁面
.nojekyll               讓 GitHub Pages 直接提供檔案
boards/
  index.json            版本清單
  talentBoard_*.json    各版本天賦盤
```

## 部署
1. 把整個資料夾內容放到 repository 根目錄（或 `docs/`）並 push。
2. Settings → Pages → Source 選 **Deploy from a branch**，Branch 選 `main`，資料夾選 `/ (root)` 或 `/docs`。
3. 網址：`https://<帳號>.github.io/<repository>/`

## 新增天賦版本
1. 用天賦盤編輯器修改，先在「盤面版本」填新版本名稱，再「另存新檔」，把檔案放進 `boards/`。
2. 編輯 `boards/index.json`：在 `boards` 最前面加一筆，並把 `latest` 改成新版本：
```json
{
  "latest": "LOOTANIA Beta v 0.9.3",
  "boards": [
    { "version": "LOOTANIA Beta v 0.9.3", "file": "talentBoard_LOOTANIA_Beta_v_0.9.3.json", "note": "說明" },
    { "version": "LOOTANIA Beta v 0.9.2", "file": "talentBoard_LOOTANIA_Beta_v_0.9.2.json", "note": "v 0.9.2" }
  ]
}
```
`version` 必須與該 JSON 檔內的 `version` 欄位完全相同，流派檔才能對應。舊版本檔案請保留，舊流派才讀得到。

## 本機預覽
直接雙擊 `index.html` 讀不到資料，請在此資料夾執行 `python -m http.server 8000`，再開 http://localhost:8000/

## 分享流派
頁面上「複製分享碼」產生 `LT1` 開頭的代碼，「複製分享連結」產生 `網址#LT1…`，點開即載入該流派。分享碼記錄天賦版本，舊版本的盤面檔案請保留在 `boards/`。
