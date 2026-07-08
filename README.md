# 🌸 蜜友 MiYou — PWA 部署指南

## 📁 檔案結構

```
miyu-pwa/
├── index.html           ← 主程式（完整 App）
├── manifest.json        ← PWA 安裝設定
├── sw.js                ← Service Worker（離線支援）
├── icons/
│   ├── icon.svg         ← SVG 來源圖示
│   ├── generate-icons.html  ← 圖示產生器（先執行這個）
│   ├── badge-72.png     ← 通知用小圖示（產生後放入）
│   ├── icon-128.png     ← 128×128
│   ├── icon-192.png     ← 192×192（必要）
│   ├── icon-384.png     ← 384×384
│   └── icon-512.png     ← 512×512（必要）
└── README.md            ← 本文件
```

---

## 🚀 部署步驟

### 第一步：產生圖示

1. 用瀏覽器開啟 `icons/generate-icons.html`
2. 點擊「產生並下載全部圖示」
3. 將下載的 5 個 PNG 檔案放入 `icons/` 資料夾

---

### 第二步：選擇部署方式

#### ✅ 方式 A — Netlify Drop（最快，推薦）

1. 開啟 [app.netlify.com/drop](https://app.netlify.com/drop)
2. 把整個 `miyu-pwa/` **資料夾**直接拖進去
3. Netlify 會自動給你一個 `https://xxx.netlify.app` 網址
4. 用手機瀏覽器開啟這個網址即可安裝

---

#### ✅ 方式 B — GitHub Pages（免費永久）

```bash
# 1. 建立 GitHub repo（在 github.com 上操作）

# 2. 在 miyu-pwa/ 資料夾中執行
git init
git add .
git commit -m "初始化蜜友 PWA"
git remote add origin https://github.com/你的帳號/miyu-pwa.git
git push -u origin main

# 3. 到 GitHub repo 的 Settings → Pages
#    Source 選 main branch / root
#    儲存後幾分鐘就會有 https://你的帳號.github.io/miyu-pwa/ 網址
```

---

#### ✅ 方式 C — 本機測試

```bash
# 方法一：Python（內建）
cd miyu-pwa
python3 -m http.server 8080

# 方法二：Node.js
npx serve miyu-pwa -p 8080

# 開啟瀏覽器：http://localhost:8080
# ⚠️ 本機測試時 Service Worker 需要 localhost，Safari 可能不支援
```

---

## 📱 安裝到手機

### Android（Chrome）
1. 用 Chrome 開啟你的網址
2. 點右上角 ⋮ 選單
3. 點「新增至主畫面」或「安裝應用程式」
4. 確認後即完成安裝

### iPhone（Safari）
1. 用 **Safari** 開啟你的網址（Chrome 不支援 iOS 安裝 PWA）
2. 點底部的「分享」按鈕 □↑
3. 往下滑找「加入主畫面」
4. 點右上角「新增」即完成

---

## 🔔 功能說明

| 功能 | 狀態 |
|------|------|
| 完整註冊流程（7步驟） | ✅ 完成 |
| 手機號碼 + OTP 驗證（UI） | ✅ 完成 |
| 照片上傳（真實相機/相簿） | ✅ 完成 |
| 8種照片濾鏡效果 | ✅ 完成 |
| 性別 / 年齡 / 興趣設定 | ✅ 完成 |
| MBTI 選擇 | ✅ 完成 |
| 離線使用（Service Worker） | ✅ 完成 |
| 「加到主畫面」安裝提示 | ✅ 完成 |
| 推播通知（介面預留） | ⏳ 需後端 |
| 附近的人（附近地圖） | ⏳ 需後端 |
| 活動揪團完整功能 | ⏳ 需後端 |
| 配對 + 聊天 | ⏳ 需後端 |
| 帳號系統（真實 OTP） | ⏳ 需後端 |

---

## 🛠 後續開發建議

### 後端技術棧（推薦）

```
前端（目前）：Pure HTML/CSS/JS → 可升級為 Vue 3 或 React
後端 API   ：Node.js + Express 或 Go Fiber
資料庫     ：PostgreSQL（用戶資料）+ Redis（OTP / 快取）
即時通訊   ：WebSocket 或 Socket.io（聊天功能）
簡訊 OTP   ：Twilio 或 AWS SNS
地理位置   ：PostGIS + Geolocation API
圖片儲存   ：AWS S3 或 Cloudflare R2
推播通知   ：Web Push API + VAPID 金鑰
```

### 推薦的下一步

1. **串接真實 OTP**：Twilio 約每條 $0.05 USD，可先用 Firebase Phone Auth（免費方案）
2. **加入後端 API**：建議先用 Firebase Firestore 做快速 MVP 驗證
3. **加入地圖**：Google Maps API 或 Leaflet.js（開源免費）
4. **上架 App Store**：完成 MVP 後可用 Capacitor 包成 .ipa / .apk

---

## 🔑 PWA 關鍵特性說明

### Service Worker（sw.js）
- 快取首次載入的資源，之後離線也能使用
- 背景同步（未來可用來在有網路時同步訊息）
- 推播通知介面已預留

### Manifest（manifest.json）
- 讓瀏覽器知道這是可安裝的 App
- 定義 App 名稱、圖示、啟動畫面顏色
- `display: standalone` = 安裝後隱藏瀏覽器介面，像原生 App

### 安全性要求
- PWA 必須在 **HTTPS** 下才能安裝（localhost 除外）
- Netlify / GitHub Pages 都自動提供 HTTPS ✓

---

## 📞 聯絡 & 問題排解

**安裝後看不到圖示？**
→ 確認 `icons/icon-192.png` 和 `icons/icon-512.png` 存在

**iOS 無法安裝？**
→ 必須用 Safari，且網站要有 HTTPS

**Service Worker 沒有更新？**
→ 修改 `sw.js` 中的 `CACHE` 版本號，如 `'miyu-v2'`

**Chrome DevTools 測試 PWA**
→ F12 → Application → Manifest / Service Workers 查看狀態
