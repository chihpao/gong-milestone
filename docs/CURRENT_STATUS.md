# 目前狀態與 AI 交接

最後更新：2026-09-22（v46 LINE 分享描述）

## 目前狀態

四階段驗收與修正已完成。v46 將一般 description 與 Open Graph 分享描述統一改為 `A dream chaser.`，讓 LINE 等分享服務優先使用指定英文摘要，而非年份範圍。發布提交與部署結果記錄於下方「發布」。README.md 未納入本次修改。

## 現行實作

- index.html 是唯一里程碑網站；11 幕本地 SVG 持續循環，四個年份錨點。access.html 維持 0916 前端入口，非安全驗證。
- 手機點擊場景的原生按鈕切換文字，一次展開一幕；支援觸控、Enter、Space 與 aria-expanded。桌面依可見比例顯示文字，以進入／退出門檻避免邊界閃動。
- 捲動與尺寸更新合併到單次 requestAnimationFrame，沒有計時器或自行重複的動畫迴圈，也不再依賴 IntersectionObserver。
- 年份選單固定背景捲動、保存位置、限制 Tab／Shift+Tab 焦點，Escape 關閉並還原焦點，選年後移到對應段落。
- 選單開啟時，深色叉叉與站名優先於捲動後的白色樣式，避免白底上消失。
- 動態偏好與斷點可即時切換；減少動態使用薄荷色靜態插圖。無 JavaScript 時仍可閱讀全文。
- A4 白底黑字列印，隱藏首屏與控制項；列印前自動關閉選單，避免固定背景影響分頁。
- 分享描述為 `A dream chaser.`，並以一般 description 與 Open Graph 標籤同步提供；保留使用者手動修改的 2019/01 合併句。現有 SVG 橘／紅橘配色已獲使用者接受。

## 動畫修正

十一幕共 182 個持續循環的 SMIL 節點。修正定位被旋轉／縮放覆蓋、京都鳥居中心、吊鍋與盆栽定位、洗衣店循環圖層、雨線、人物影子與鏡像方向。城市、街景、山丘、星空使用重複圖層；粒子與接點淡化；人物落地與舞台手臂時序調整。詳細週期見 ANIMATION_STORYBOARD.md。

## 已驗證

- v46 已確認一般 description 與 `og:description` 均為 `A dream chaser.`，Open Graph 標題、類型與地區設定齊全；JavaScript 語法、主要 HTML 標籤平衡及既有里程碑文案未受影響。

- Chrome 153、Edge 153、Playwright WebKit 26.5：各 11 種尺寸，共 33 組（360×640、390×844、430×932、740×360、759×800、760×800、768×1024、844×390、1024×768、1280×800、1440×900）。未發現頁面橫向溢出；手機 11 幕文字無裁切；年份跳轉與密碼入口正常；測試期間無頁面腳本錯誤或失敗請求。
- 修正後補測原生按鈕鍵盤／觸控、選單正反向焦點循環、Escape、捲動位置還原、動態偏好切換、無 IntersectionObserver、無 JavaScript 與 SVG patternTransform 動畫，三個引擎通過。
- 11 幕各播放 13 秒並檢視分段影像；共 143 秒。桌面測試 requestAnimationFrame 間隔 p95 約 16.8–17ms、最大 17.6ms，未觀察到超過 50ms 的主執行緒停頓。此數值不代表手機 GPU 實際幀率。
- 洗衣店座標修正後另檢視畫面，Chrome／Edge／WebKit 重複圖層位移正常。
- 實際匯出兩頁 A4 PDF 並逐頁檢視：全文完整、白底黑字、事件未被拆斷，無黑底、文字裁切或額外空白首頁。
- JavaScript 語法、HTML 結構、SVG XML／動畫引用／時序、來源文案及 git diff 空白檢查通過。
- 本次依使用者明確許可使用可見瀏覽器，已確認開啟選單後叉叉顯示；日後仍遵守 AGENTS.md 的預設驗證規則。

## 驗證界線

未取得實體 iPhone、Android 或 macOS Safari。本次手機尺寸與觸控為模擬測試；WebKit 是引擎相容性檢查，不等同真機 Safari 驗收。真機字型載入、瀏海安全區、瀏覽器工具列伸縮與長時間效能仍需實機確認。

## 發布

- v46 依使用者明確要求推送至既有 GitHub `main`；LINE 既有連結預覽仍可能保留快取，需等待重新抓取或以新網址參數分享。

- 遠端：https://github.com/chihpao/gong-milestone.git
- 網站：https://chihpao.github.io/gong-milestone/
- 發布前再次 fetch，main 與 origin/main 無分歧，未發生合併衝突。
- 叉叉圖示另於三個引擎各 11 種寬度補測，皆可見、可點擊，開關狀態正常。
- 本次僅提交網站、11 個現行 SVG 與交接文件；不提交 README.md、QA 暫存檔、私人圖片或舊版忽略資產。

歷史變更請查閱 CHANGELOG.md；本文件只描述目前版本。
