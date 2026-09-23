# 目前狀態與 AI 交接

最後更新：2026-09-24（v49 專案目錄與資產命名重構）

## 目前狀態

四階段驗收與修正已完成。v49 將正式動畫、圖示與資料分別整理至 `assets/animations/`、`assets/icons/` 與 `data/`，十一份 SVG 改用一致的日期／事件語意檔名；歷史資產與私人素材則移至 Git 忽略的 `archive/` 與 `private/`。本次保留 v48 的完整動畫創作資料，未改動網站視覺或 SVG 動畫內容。

## 現行實作

- index.html 是唯一里程碑網站；11 幕本地 SVG 持續循環，四個年份錨點。網站直接公開，不再有 access.html 或密碼流程。
- `data/milestones.json` 是結構化日期、文案、資產關聯與逐幕動畫創作資料來源；CONTENT_SOURCE.md 與 index.html 靜態內容同步，確保 JSON 載入失敗、直接開檔或停用 JavaScript 時仍可閱讀。
- 11 份正式動畫位於 `assets/animations/`，favicon 位於 `assets/icons/`；根目錄只保留 GitHub Pages 與專案治理入口檔案。
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

- v49 已確認 JSON 可解析且 11 筆資料／動畫欄位完整，JSON 與 HTML 的文案及資產順序一致，JavaScript 語法與主要 HTML 標籤平衡。11 份 SVG 均可解析、無腳本或外部引用，共 182 個永久循環 SMIL 節點。
- 本機 HTTP 驗證確認首頁、`data/milestones.json`、favicon 與 11 份新路徑動畫共 14 個公開資源全部回應 200；根目錄無散落 SVG／JSON，`archive/` 與 `private/` 已被 Git 忽略且沒有追蹤檔案。未使用可見瀏覽器。

- v48 已確認 11 筆里程碑均含完整 `animation` 欄位，資產路徑、主週期、方向與循環描述對應現行 SVG／ANIMATION_STORYBOARD.md；JSON 可解析，網站 JavaScript 仍可忽略額外維護欄位並正常讀取原有內容。

- v47 已確認 JSON 語法與 11 筆 id／日期／內文完整，JSON、CONTENT_SOURCE.md 與 HTML 靜態備援一致；`access.html` 已移除。JavaScript 語法、主要 HTML 標籤、SVG 路徑與 git diff 空白檢查通過。

- v46 已確認一般 description 與 `og:description` 均為 `A dream chaser.`，Open Graph 標題、類型與地區設定齊全；JavaScript 語法、主要 HTML 標籤平衡及既有里程碑文案未受影響。

- v46 基準測試使用 Chrome 153、Edge 153、Playwright WebKit 26.5：各 11 種尺寸，共 33 組（360×640、390×844、430×932、740×360、759×800、760×800、768×1024、844×390、1024×768、1280×800、1440×900）。未發現頁面橫向溢出；手機 11 幕文字無裁切；年份跳轉正常；測試期間無頁面腳本錯誤或失敗請求。v47 未重跑瀏覽器 UI 驗證。
- 修正後補測原生按鈕鍵盤／觸控、選單正反向焦點循環、Escape、捲動位置還原、動態偏好切換、無 IntersectionObserver、無 JavaScript 與 SVG patternTransform 動畫，三個引擎通過。
- 11 幕各播放 13 秒並檢視分段影像；共 143 秒。桌面測試 requestAnimationFrame 間隔 p95 約 16.8–17ms、最大 17.6ms，未觀察到超過 50ms 的主執行緒停頓。此數值不代表手機 GPU 實際幀率。
- 洗衣店座標修正後另檢視畫面，Chrome／Edge／WebKit 重複圖層位移正常。
- 實際匯出兩頁 A4 PDF 並逐頁檢視：全文完整、白底黑字、事件未被拆斷，無黑底、文字裁切或額外空白首頁。
- JavaScript 語法、HTML 結構、SVG XML／動畫引用／時序、來源文案及 git diff 空白檢查通過。
- 本次依使用者明確許可使用可見瀏覽器，已確認開啟選單後叉叉顯示；日後仍遵守 AGENTS.md 的預設驗證規則。

## 驗證界線

未取得實體 iPhone、Android 或 macOS Safari。本次手機尺寸與觸控為模擬測試；WebKit 是引擎相容性檢查，不等同真機 Safari 驗收。真機字型載入、瀏海安全區、瀏覽器工具列伸縮與長時間效能仍需實機確認。

## 發布

- v49 目錄重構與 v48 動畫創作資料已由提交 `241aa7e` 推送至既有 GitHub `main`。GitHub Pages build／deploy 均成功；公開首頁、`data/milestones.json`、favicon 與 11 份新路徑動畫共 14 個資源全部回應 200，JSON 含 11 筆資料。舊 `/milestones.json`、`/2017_animation.svg` 與 `/access.html` 均回應 404。

- v47 依使用者明確要求直接公開，已推送至既有 GitHub `main`。GitHub Pages 已確認首頁與 `milestones.json` 回應 200、JSON 含 11 筆資料，舊 `access.html` 回應 404。

- v46 依使用者明確要求推送至既有 GitHub `main`；LINE 既有連結預覽仍可能保留快取，需等待重新抓取或以新網址參數分享。

- 遠端：https://github.com/chihpao/gong-milestone.git
- 網站：https://chihpao.github.io/gong-milestone/
- 發布前再次 fetch，main 與 origin/main 無分歧，未發生合併衝突。
- 叉叉圖示另於三個引擎各 11 種寬度補測，皆可見、可點擊，開關狀態正常。
- 本次僅提交網站、11 個現行 SVG 與交接文件；不提交 README.md、QA 暫存檔、私人圖片或舊版忽略資產。

歷史變更請查閱 CHANGELOG.md；本文件只描述目前版本。
