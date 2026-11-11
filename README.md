# Happiness Table™ Digital（幸福餐桌數位工具包）

幸福餐桌數位產品的官方網站：PDF 指南、Notion 規劃模板與線上影音課。
純 HTML＋CSS，沒有建置步驟，部署在 GitHub Pages。

## 檔案

| 檔案 | 內容 |
| --- | --- |
| `index.html` | 產品介紹、交付清單、內容預覽（目前隱藏）、方案定價、FAQ |
| `terms.html` | 服務條款與數位授權 |
| `refund.html` | 退款與取消政策（14 天內全額退款） |
| `privacy.html` | 隱私權政策與服務供應商 |
| `contact.html` | 客服與品牌主理人資訊 |
| `404.html` | 找不到頁面（`noindex`） |
| `assets/css/style.css` | 全站樣式 |
| `assets/images/` | favicon、分享圖 |

視覺規範照大道至簡的 `DESIGN.md`：米白紙底、墨色字、單一茶褐強調色、直角細線、
Noto Serif TC＋Cormorant Garamond，不用 emoji。

## 產品、賣方與交付

| 項目 | 內容 |
| --- | --- |
| 方案 | Starter Toolkit $39、Pro Masterclass $149，都是一次付費。不賣社群、直播、一對一指導（Paddle 不收不綁軟體的人工服務與社群存取） |
| 賣方 | CHIEN CHIA CHI（簡家旗），個人賣家，台灣；筆名 Alex Chien。條款、聯絡頁、隱私權頁都寫這個名字，要和 Paddle 帳號一致 |
| 交付 | 付款後以 email 寄送 Google 雲端硬碟資料夾連結（分享給結帳信箱），通常幾分鐘、最遲 24 小時；影片在雲端硬碟直接播放 |
| 作者佐證 | 首頁「About the Author」連到英文書 *The Architecture of Inner Flow*（Amazon） |

## 寫文案時注意

- 白話描述交付物：檔案格式、單元數、怎麼取得。不用抽象的方法論名稱當主標。
- 不寫收入、獲利或「高溢價」之類的承諾。
- 不寫還沒做出來的內容；數字（頁數、單元數、片長）以實際產品為準。
- 首頁 FAQ 與 JSON-LD 的 `FAQPage` 要同步修改。
- 法律頁改動後，更新頁首的「Last Updated」日期。

## 內容預覽區塊

`index.html` 裡的 `#preview` 區塊目前加了 `hidden`，不會顯示。
放上真實的白皮書目錄截圖、Notion 模板截圖、12 單元課程名稱與片長之後，
照區塊上方註解的四個步驟打開。

## 部署

推到 `main` 後由 GitHub Pages 發布（Settings → Pages → `main` / `(root)`）。
網址：`https://alexchiachi.github.io/happytable-digital/`

## SEO 與分享

- 每頁都有 `canonical`、Open Graph、`twitter:card`；分享圖是 `assets/images/og-image.jpg`（1200×630）。
- 首頁有 JSON-LD：`Organization`、兩個方案的 `Product`／`Offer`（尚未開賣，標 `PreOrder`；接上 Paddle 後改 `InStock`），和頁面 FAQ 一致的 `FAQPage`，以及作者英文書的 `Book`。改 FAQ 文字時兩邊一起改。
- `sitemap.xml` 列出 5 頁；`404.html` 用根目錄相對路徑（`/happytable-digital/...`）。
- 專案頁網址放不了有效的 `robots.txt`（只認網域根目錄），sitemap 請在 Google Search Console 手動提交。

### 換成自訂網域時要改的地方

網址目前是 `https://alexchiachi.github.io/happytable-digital/`，出現在：

1. 5 個頁面的 `canonical`、`og:url`、`og:image`
2. `index.html` 的 JSON-LD
3. `sitemap.xml`
4. `404.html` 裡的 `/happytable-digital/` 前綴（自訂網域時改成 `/`）

另外在倉庫根目錄加一個 `CNAME` 檔，內容寫網域。

## 串接 Paddle 結帳

在 Paddle 取得 client-side token 與各方案的 price ID 後，載入 Paddle.js：
```html
<script src="https://cdn.paddle.com/paddle/v2/paddle.js"></script>
<script>
  Paddle.Environment.set("sandbox"); // 上線改 "live"
  Paddle.Initialize({ token: "YOUR_CLIENT_TOKEN" });
</script>
```
方案按鈕改成：
```html
<button class="btn-checkout" onclick="Paddle.Checkout.open({ items: [{ priceId: 'pri_xxx', quantity: 1 }] })">
  Get Starter Toolkit
</button>
```
接上後，把 JSON-LD 的 `availability` 從 `PreOrder` 改成 `InStock`。
