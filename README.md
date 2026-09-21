# 龔龔里程碑

一個為朋友製作的單頁人生里程碑網站，記錄龔龔從 2017 到 2025 年，在台灣、西班牙、法國與日本之間累積的表演旅程。

專案以單一 HTML 檔交付，重點是手機閱讀體驗、日系作品集風格的滿版文字場景、輕量互動，以及適合輸出為 A4 PDF 的列印版面。

若你是接手本專案的 AI，請先閱讀 [`AGENTS.md`](./AGENTS.md)，再依其中指定的順序閱讀 [`docs/CURRENT_STATUS.md`](./docs/CURRENT_STATUS.md) 與其他文件。不要只根據舊對話或 README 開始修改。

## 快速開始

直接以瀏覽器開啟 [`index.html`](./index.html) 即可，不需要安裝套件、啟動伺服器或進行建置。`index.html` 也是 GitHub Pages 的發佈入口。分享版入口密碼為 `0916`；這只是前端視覺門檻，不是安全驗證。

## 專案架構

```text
Gong_Milestone/
├─ index.html                # GitHub Pages 入口與網站成品
├─ GongGong_Milestone.html   # 網站成品；HTML、CSS、JavaScript 均在同一檔案
├─ AGENTS.md                 # 後續工作必須遵守的專案規範
├─ README.md                 # 專案說明與維護入口
├─ CHANGELOG.md              # 重要修改紀錄
└─ docs/
   ├─ CURRENT_STATUS.md      # 最新進度、驗證結果與 AI 交接資訊
   ├─ PROJECT_BRIEF.md       # 原始需求整理
   ├─ CONTENT_SOURCE.md      # 里程碑原始內容
   ├─ DESIGN_SYSTEM.md       # 視覺系統與版面規則
   └─ DECISIONS.md           # 專案的重要設計決策
```

## 修改方式

### 修改文字

先修改 [`docs/CONTENT_SOURCE.md`](./docs/CONTENT_SOURCE.md)，再把相同文字同步至兩個 HTML。不得自行增加事件標題、銜接文字、口號或詮釋。

### 修改顏色

在 HTML 上方的 CSS `:root` 區塊調整色票。完整的色彩與字體說明請參考 [`docs/DESIGN_SYSTEM.md`](./docs/DESIGN_SYSTEM.md)。

### 新增里程碑

複製一個完整的 `<article class="event ... reveal">...</article>`，放進適合的 `.period` 區段。新增日期與文字前，必須先更新 `CONTENT_SOURCE.md`；不要為新事件增加自創標題。

## 列印成 PDF

1. 使用瀏覽器開啟 HTML。
2. 選擇「列印」。
3. 紙張選擇 A4、方向選擇直式。
4. 開啟「背景圖形」，再選擇「另存為 PDF」。

列印模式會自動關閉動畫、改用節墨色彩，並避免單一里程碑被分割到兩頁。

## 技術摘要

- 語言：繁體中文
- 技術：原生 HTML、CSS、JavaScript
- 字體：Google Fonts 的 Noto Sans TC、Montserrat，並提供系統備援字體
- 響應式：最小支援寬度 360px；760px 以上調整為桌面留白與字級
- 互動：所有尺寸共用全螢幕年份選單、四碼入口、目前區段標示與 `IntersectionObserver` 捲動浮現
- 發佈：GitHub Pages 相容的靜態 `index.html`
- 無障礙：語言標記、語意化章節、裝飾圖示隱藏，以及 `prefers-reduced-motion` 支援
- 列印：A4 直式專用 `@media print`

## 文件索引

- [`AGENTS.md`](./AGENTS.md)：所有 AI 協作者的入口、必讀順序與硬性規則
- [`docs/CURRENT_STATUS.md`](./docs/CURRENT_STATUS.md)：目前完成內容、最近驗證與待辦事項
- [`docs/PROJECT_BRIEF.md`](./docs/PROJECT_BRIEF.md)：專案目的、使用情境與驗收條件
- [`docs/CONTENT_SOURCE.md`](./docs/CONTENT_SOURCE.md)：未經版面加工的原始里程碑內容
- [`docs/DESIGN_SYSTEM.md`](./docs/DESIGN_SYSTEM.md)：色彩、字體、間距與響應式規則
- [`docs/DECISIONS.md`](./docs/DECISIONS.md)：為什麼使用單檔、滿版排版及目前的互動方式
- [`CHANGELOG.md`](./CHANGELOG.md)：歷次重要變更
