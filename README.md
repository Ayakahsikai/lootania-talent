# LOOTANIA

一個 repository、一個 GitHub Pages 網站，原始檔分成兩個資料夾，由 GitHub Actions 組合後發佈。

| 資料夾 | 發佈位置 | 網址 |
|---|---|---|
| `talent/` | 網站根目錄 | `https://<帳號>.github.io/<repo>/`（天賦網址不變） |
| `wiki/` | `/wiki/` | `https://<帳號>.github.io/<repo>/wiki/` |

```
.github/workflows/pages.yml   自動部署（push 到 main 就會更新網站）
talent/
  index.html                  天賦模擬
  boards/
    index.json                天賦版本清單
    talentBoard_*.json        各版本天賦盤
wiki/
  index.html                  Wiki 首頁（目前是建置中頁面，可直接取代）
```

## 第一次設定（從原本的「根目錄部署」改過來）
1. 把 repo 根目錄原本的 `index.html`、`boards/` 移到 `talent/`（用 `git mv` 可保留歷史），刪掉根目錄的 `.nojekyll`。
2. 加入 `.github/workflows/pages.yml` 和 `wiki/`，commit 並 push 到 `main`。
3. Settings → Pages → Build and deployment → **Source 改成「GitHub Actions」**。
4. 到 Actions 分頁確認「Deploy GitHub Pages」跑完（綠勾），開原本的網址確認天賦頁正常、`/wiki/` 可開。

> 預設分支如果叫 `master`，把 `pages.yml` 裡的 `branches: [main]` 改成 `master`。
> 改 Source 到第一次部署完成之間，網站可能有一兩分鐘打不開。

## 日常更新
- **天賦**：只換 `talent/` 裡的檔案，push 後自動部署。
- **Wiki**：只動 `wiki/` 裡的檔案，push 後自動部署。
- 也可以在 Actions 分頁手動按「Run workflow」重新部署。

部署前會自動檢查：`talent/index.html`、`boards/index.json` 是否存在、`latest` 是否在清單裡、每個天賦盤檔案能否讀取且 `version` 與清單一致；`talent/` 裡不能有 `wiki` 資料夾。檢查失敗會停止部署，線上網站維持上一版。

## 新增天賦版本
1. 用天賦盤編輯器修改，先在「盤面版本」填新版本名稱，再「另存新檔」，把檔案放進 `talent/boards/`。
2. 編輯 `talent/boards/index.json`：在 `boards` 最前面加一筆，並把 `latest` 改成新版本。
   `version` 必須和該 JSON 檔內的 `version` 完全相同。舊版本檔案請保留，舊流派與分享碼才讀得到。

## 本機預覽
- 天賦：直接雙擊 `index.html` 讀不到資料。在 `talent/` 資料夾執行 `python -m http.server 8000`，開 http://localhost:8000/
- Wiki：依 wiki 本身的方式開啟即可。
- Wiki 連回天賦頁請用相對路徑 `../`；Wiki 若要用瀏覽器儲存（localStorage），名稱請避開 `lootania-talent`、`lootania-ver`、`lootania-stage` 開頭，以免和天賦頁互相覆蓋。
