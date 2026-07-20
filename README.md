# 🌸 蜜友 MiYou — PWA 部署指南

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


## 📞 聯絡 & 問題排解

**安裝後看不到圖示？**
→ 確認 `icons/icon-192.png` 和 `icons/icon-512.png` 存在

**iOS 無法安裝？**
→ 必須用 Safari，且網站要有 HTTPS

**Service Worker 沒有更新？**
→ 修改 `sw.js` 中的 `CACHE` 版本號，如 `'miyu-v2'`

**Chrome DevTools 測試 PWA**
→ F12 → Application → Manifest / Service Workers 查看狀態
