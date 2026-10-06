# LOOTANIA 天賦模擬

原始檔放在 `talent/`，由 GitHub Actions 發佈到網站根目錄：`https://<帳號>.github.io/<repo>/`（天賦網址不變）。

```
.github/workflows/pages.yml   自動部署（push 到 main 就會更新網站）
talent/
  index.html                  天賦模擬
  boards/
    index.json                天賦版本清單
    talentBoard_*.json        各版本天賦盤
```

## 部署設定
- Settings → Pages → Build and deployment → **Source 選「GitHub Actions」**（不要選建議的 Jekyll / Static HTML 範本）。
- 預設分支如果叫 `master`，把 `pages.yml` 裡的 `branches: [main]` 改成 `master`。

## 日常更新
- 只換 `talent/` 裡的檔案，push 後自動部署；也可以在 Actions 分頁手動按「Run workflow」重新部署。

部署前會自動檢查：`talent/index.html`、`boards/index.json` 是否存在、`latest` 是否在清單裡、每個天賦盤檔案能否讀取且 `version` 與清單一致。檢查失敗會停止部署，線上網站維持上一版。

## 新增天賦版本
1. 用天賦盤編輯器修改，先在「盤面版本」填新版本名稱，再「另存新檔」，把檔案放進 `talent/boards/`。
2. 編輯 `talent/boards/index.json`：在 `boards` 加一筆，並把 `latest` 改成新版本。
   `version` 必須和該 JSON 檔內的 `version` 完全相同。舊版本檔案請保留，舊流派與分享碼才讀得到。

## 本機預覽
直接雙擊 `index.html` 讀不到資料。在 `talent/` 資料夾執行 `python -m http.server 8000`，開 http://localhost:8000/
