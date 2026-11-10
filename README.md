# Happiness Table™ Digital (幸福餐桌 數位知識智財系統)

> **為申請 Paddle (Merchant of Record) 與全球販售數位知識產品而建的官方網站。**

---

## 📌 對應 Paddle 審查重點的設計

Paddle 審查團隊（歐洲/英國風控）主要查驗以下 5 大維度，本網站均已嚴格對應：

1. **排除實體物流風險 (Zero Physical Shipping)**
   - 全站首頁、定價區塊、頂部導航條均以醒目標籤聲明：
     > `⚡ All products are 100% digital goods with instant access upon purchase. No physical items will be shipped.`
2. **定價清晰與交付明確 (Transparent Pricing & Deliverables)**
   - **Starter ($39 USD)**: PDF 策略白皮書 + Notion 商業化模組 (線上即時下載)
   - **Pro ($149 USD)**: 12 章節線上影音大師課 + 四季儀式 SOP 手冊 (立即取得線上學習後台權限)
   - **All-Access ($299 USD/yr)**: 數位創作者會員社群 + 季度研討會
3. **頁尾四大法定合規獨立子頁面 (Footer 4 Mandatory Legal Pages)**
   - [`refund.html`](refund.html)：**14 天內全額退款、不需說明理由 (14-Day Money Back Guarantee)**，寫明退款途徑與 24 小時回覆 SLA。
   - [`terms.html`](terms.html)：數位產品單人使用授權、著作權聲明與免責條款。
   - [`privacy.html`](privacy.html)：GDPR / CCPA 權利說明，不使用廣告與追蹤 Cookie，列出 Paddle、GitHub Pages、iCloud Mail 三個服務供應商。
   - [`contact.html`](contact.html)：清楚揭露創辦人姓名（Alex Chien / 簡家旗）、客服支援信箱與回覆承諾。
4. **英中雙語專業展示 (Bilingual Clarity)**
   - 審查員打開即見流暢的專業商業英文，完全消除因在地文化術語造成的「產品描述不明確 (Vague Description)」拒件風險。
5. **符合大道至簡網頁標準 (Zen Web Standards)**
   - 米白紙底（`#FAF6EF`）、墨色文字（`#2A2520`）、直角美學與靜構防孤字排版，極速加載無外掛阻擋。

---

## 🚀 部署上線指南 (GitHub Pages)

### 1. 遠端倉庫建立
1. 前往 GitHub 建立新倉庫：[https://github.com/new](https://github.com/new)
2. 倉庫名稱填入：`happytable-digital`
3. 設為 **Public (公開)**
4. 不需要勾選 Initialize with README (本機已有完整檔案)
5. 點擊 **Create repository**

### 2. 推送代碼
本機已完成所有設定與 Remote Origin 綁定，只需執行：
```bash
git push -u origin main
```

### 3. 開啟 GitHub Pages
1. 在 GitHub 倉庫進入 **Settings** -> **Pages**
2. 在 **Build and deployment** 下方的 **Branch** 選擇 `main` / `/(root)`
3. 點擊 **Save**
4. 幾分鐘後即可透過 `https://Alexchiachi.github.io/happytable-digital/` 查看線上網站！

---

## 🔎 SEO 與分享

- 每頁都有 `canonical`、Open Graph、`twitter:card`；分享圖是 `assets/images/og-image.jpg`（1200×630）。
- 首頁有 JSON-LD：`Organization`、三個方案的 `Product`／`Offer`（尚未開賣，標 `PreOrder`；接上 Paddle 後改 `InStock`），以及和頁面 FAQ 一致的 `FAQPage`。改 FAQ 文字時兩邊一起改。
- `sitemap.xml` 列出 5 頁；`404.html` 用根目錄相對路徑（`/happytable-digital/...`）。
- 專案頁網址放不了有效的 `robots.txt`（只認網域根目錄），sitemap 請在 Google Search Console 手動提交。

### 換成自訂網域時要改的地方

網址目前是 `https://alexchiachi.github.io/happytable-digital/`，出現在：

1. 5 個頁面的 `canonical`、`og:url`、`og:image`
2. `index.html` 的 JSON-LD
3. `sitemap.xml`
4. `404.html` 裡的 `/happytable-digital/` 前綴（自訂網域時改成 `/`）

另外在倉庫根目錄加一個 `CNAME` 檔，內容寫網域。

## 💳 Paddle 過審後串接

審核通過並在 Paddle 取得 Vendor ID / Product ID 後，將各方案按鈕切換為 Paddle 官方結帳組件：
```html
<script src="https://cdn.paddle.com/paddle/v2/paddle.js"></script>
<script>
  Paddle.Environment.set("live"); // or sandbox
  Paddle.Initialize({ token: "YOUR_CLIENT_TOKEN" });
</script>
```
方案按鈕加入：
```html
<button onclick="Paddle.Checkout.open({ items: [{ priceId: 'pri_xxx', quantity: 1 }] })">
  Buy Now
</button>
```
