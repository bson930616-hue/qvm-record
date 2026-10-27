# QVM 記錄 App（手機網頁，可加到 iPhone 主畫面）

只做一件事：**在手機上記錄買賣，直接寫進 GitHub 私有儲存庫的 `V10_交易紀錄.csv`**，並顯示持股與部位設定。
績效、警示、研究清單仍由 GitHub Actions 自動產生（email／Issues），App 只提供連結。

## 它怎麼運作
- 純靜態網頁（`index.html` 一個檔案，沒有框架、沒有伺服器、沒有資料庫）。
- 用你的 GitHub 存取金鑰（token）呼叫 GitHub API 讀寫兩個檔案：`V10_交易紀錄.csv`、`V10_設定.csv`。
- 金鑰只存在這支手機的瀏覽器（localStorage），不會傳到 GitHub 以外的地方。
- 網頁本身**不含任何你的資料或金鑰**，所以可以放在公開網址。

## 部署（一次性）
GitHub 免費帳號的私有儲存庫不能用 GitHub Pages，所以網頁放在**另一個公開的小儲存庫**：
1. GitHub → 右上 ＋ → New repository → 名稱 `qvm-record`、選 **Public** → Create。
2. 把本資料夾的檔案放進去：`index.html`、`manifest.webmanifest`、`sw.js`、`icon.svg`、`icon-180.png`、`icon-192.png`、`icon-512.png`（根目錄，不要放子資料夾）。
3. 該儲存庫 → Settings → Pages → Source 選 `Deploy from a branch`，Branch 選 `main`、資料夾 `/ (root)` → Save。
4. 約 1 分鐘後網址是 `https://你的帳號.github.io/qvm-record/`。

## iPhone 安裝
1. 用 **Safari** 打開上面的網址。
2. 點下方分享鈕 → 「加入主畫面」→ 新增。
3. 從主畫面打開，到「設定」貼上金鑰（取得步驟在設定頁的「怎麼取得金鑰？」）。

## 維護
- 金鑰到期（建議設 1 年）：到 GitHub 重新產生，貼在「設定」。
- App 壞了：把錯誤畫面與 `index.html` 貼給任何 AI 助手即可修；程式約 500 行，沒有相依套件。
- 測試：`NODE_PATH=$(npm root -g) node app/test/app.test.mjs`（需要 Node 與 Playwright；用假的 GitHub，不連網）。
