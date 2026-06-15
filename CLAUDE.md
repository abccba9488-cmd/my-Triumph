# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 專案說明

萱鎧國際人力仲介股份有限公司（Triumph HR）官方網站，**單一靜態 HTML 檔案**，無建置工具或套件依賴。

- 開啟：直接用瀏覽器開啟 `index.html`，無需伺服器
- 部署：上傳 `index.html` 至靜態主機（Hostinger、Netlify、GitHub Pages 等）
- 正式網域：`https://www.triumph-hr.com.tw/`（canonical 與 og:url 須與實際網域一致）

## 檔案結構

- `index.html`：主頁面，內部分三區
- `favicon.svg`：網站圖示
- `robots.txt` / `sitemap.xml`：搜尋引擎索引設定，網域變更時須同步更新 `sitemap.xml` 的 `<loc>` 與 `robots.txt` 的 `Sitemap:`

### `index.html` 內部分三區：

### `<head>` — SEO 標籤
- `<title>` + `meta description`：含主要關鍵字，長度分別控制在 60 / 155 字元內
- JSON-LD 結構化資料：`EmploymentAgency`（公司資訊）+ `BreadcrumbList`（導覽）
- Open Graph / Twitter Card：社群分享預覽
- Geo meta tags：本地 SEO（台北市大安區）
- 修改網域時須同步更新：`canonical`、`og:url`、JSON-LD 內的 `url` 與 `item` 欄位

### `<style>` — CSS 設計系統
- **設計代幣**：色彩、陰影、圓角定義於 `:root`；暗色模式覆寫於 `[data-theme=dark]`
- **主題切換**：`html[data-theme]` attribute 控制，值存於 `localStorage`
- **動畫**：`.fi`（單元素淡入）、`.st`（子元素交錯淡入），IntersectionObserver 加 `.vis` 觸發

### `<body>` — 頁面結構

| 區塊 | ID / Class | 備註 |
|------|-----------|------|
| 導覽列 | `#nav` | fixed，捲動加 `.scrolled` |
| Hero | `#home` | 背景圖 + 多層漸層遮罩 |
| 關於我們 | `#about` | |
| 服務總覽 | `.svc-grid` | 4 張卡片，hover 有頂部色條動畫 |
| 服務特色 | `.feat-grid` | 6 張特色卡片 |
| 服務詳情 | `#services` | 奇偶列左右交替：偶數項加 `.rev`（`direction:rtl`） |
| CTA | `.cta` | |
| 聯絡 | `#contact` | 聯絡資訊 + 表單 + Google Maps iframe |
| Footer | `.footer` | |
| LINE 浮動鈕 | `.line-fab` | 固定右下角，含脈衝動畫與 QR Code tooltip |
| 回頂部 | `#scTop` | 捲動 400px 後顯示 |

## 外部服務

| 服務 | 用途 | 注意事項 |
|------|------|---------|
| FormSubmit.co | 聯絡表單發信 | **首次使用需點擊確認信**才會轉發，目標信箱 `lta63978@gmail.com` |
| Google Fonts | Noto Sans TC + Inter | `preconnect` 已設定 |
| maps.google.com | 地圖嵌入 iframe | 無需 API key |
| api.qrserver.com | LINE QR Code 圖片 | 即時產生，URL 含 LINE ID |
| images.unsplash.com | 服務區塊與 Hero 背景圖 | 免費授權，參數 `?auto=format&fit=crop&w=800&q=80&fm=webp`（已加 `fm=webp` 縮小檔案） |

## 聯絡資訊（常修改項目）

- 電話：`0973-915-715`
- LINE ID：`homboma`（連結、顯示文字、QR Code URL 共三處）
- Email：`lta63978@gmail.com`
- 地址：台北市大安區忠孝東路四段223巷53號7樓

## 修改提醒

- **換色**：只改 `:root` CSS 變數
- **新增服務**：複製 `.svc-det` 區塊，偶數項加 `.rev`
- **換圖片**：替換 `images.unsplash.com` 的 photo ID，保留查詢參數格式
- **更新 LINE ID**：需同步修改連結 href、顯示文字、QR Code `data=` 參數共三處
