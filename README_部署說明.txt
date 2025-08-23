固定網址前端（可書籤） — 部署與使用說明

用途
- 這是純前端（靜態頁面）。你把它部署到 GitHub Pages / Cloudflare Pages / Netlify 任一平台後，網址就固定不變。
- 後端（ngrok 或 Cloudflare 隧道）每天可換，訪客要能用，必須先在頁面右上角設定「後端」欄位。你把後端網址當成密碼發給付費者即可。

快速開始（Cloudflare Pages）
1. 登入 Cloudflare → Pages → Create a project → Upload assets → 上傳整包 ZIP（frontend_fixed.zip 解壓後的資料夾）。
2. 部署完成會得到固定網址如：https://xxx.pages.dev
3. （可選）如你想預先填好後端，請在專案裡把 backend.txt 填上完整的後端 base URL（例：https://abcd-xx-xx-xx.ngrok-free.app）。
   - 頁面載入順序：?b= 參數 > backend.txt > 瀏覽器 localStorage > 留空（同站）。

GitHub Pages（另一種簡單方案）
1. 建一個公開 repo，整包檔案放在根目錄，Settings → Pages → Deploy from a branch（選 main / root）。
2. 固定網址會是：https://你的帳號.github.io/你的repo/

Netlify（不綁 Git）
1. https://app.netlify.com/drop → 直接拖曳資料夾或 ZIP。
2. 立刻得到 https://xxxxx.netlify.app 供外部使用。

使用者端說明
- 右上角「後端」：可貼 ngrok/Cloudflare 隧道的 base URL，例如 https://xxx.ngrok-free.app
- 會自動記住（localStorage）。你也可用參數帶入：
  範例： https://你的固定前端網址/?b=https://xxx.ngrok-free.app
- 「清除」可清掉目前設定；「複製」可快速複製給別人。

維護建議
- 你每日開啟伺服器後，產生新的後端 URL，直接把該 URL 發給付費者，或把 Pages 專案中的 backend.txt 更新為最新 URL（若你想要自動帶入）。
- 遇到 CORS 被擋，確認後端 Flask（server.py）有啟用 CORS：CORS(app)；本包已假設你啟用了。

檔案說明
- index.html：前端主頁（支援 ?b=、backend.txt、自動記憶）。
- assets/logo.png：從你提供的 ICO 轉出。
- assets/line_qr.png：暫時用的占位圖，之後換成你的 QR 就好。
- backend.txt：可選。填上後端 URL 會自動載入。留空則不影響。

