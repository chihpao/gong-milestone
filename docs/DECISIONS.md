# 設計與技術決策

最後更新：2026-09-22。舊版視覺與時序演進請查 CHANGELOG.md。

## 靜態架構

index.html 是唯一里程碑網站，CSS／JavaScript 內嵌；11份本地SVG為背景，內嵌SVG為靜態備援。網站直接公開，不再設 access.html。格式化的 `milestones.json` 保存日期、內文、所屬年份段與動畫資產對應；頁面載入時以安全的 DOM API 套用資料，載入失敗時保留 HTML 靜態內容。沒有框架、後端或建置流程，保留GitHub Pages與直接開檔相容性。

## 可讀內容優先

`milestones.json` 是結構化里程碑文案來源，CONTENT_SOURCE.md 為人類可讀對照，index.html 保留無 JavaScript 備援。保留使用者在本機合併的2019/01句子；分享用的一般 description 與 Open Graph 描述依使用者要求統一為英文 `A dream chaser.`。2024引言及最終祝福已刪除，不再保留相應樣式。現有動畫橘／紅橘色已獲使用者接受。

## 原生控制與焦點

以獨立原生按鈕覆蓋手機場景，避免把包含正文的article冒充按鈕，也避免手寫Enter／Space重複觸發。面板透過aria-expanded／aria-controls／aria-hidden同步可讀狀態。桌面與減少動態不保留無作用的按鈕。

全螢幕選單使用inert隔離背景，限制Tab焦點範圍；關閉回復焦點與原捲動位置。固定body讓觸控環境的背景鎖定更可靠，選單本身可捲動。

## 捲動與動畫生命週期

捲動、resize合併到單次requestAnimationFrame，讀取11幕與4段落的幾何，統一更新目前場景及年份。這取代原先兩個獨立IntersectionObserver：避免無支援環境初始化中斷、回呼增量狀態遺失及減少動態切換後未建立觀察器。進入／離開分別38%／22%，減少門檻抖動。

rAF不會自我重排；背景完全由SVG的SMIL運行。固定座標與旋轉／縮放以巢狀群組隔離，持續橫移層使用可重複pattern，粒子重設則有透明接點。維持持續播放的原始需求，不把捲動顯示狀態當作SVG起播訊號。

## 漸進顯示與列印

只有腳本初始化成功後才加入js顯示控制類別；無JavaScript仍可閱讀。減少動態偏好透過change事件即時同步，備援插圖使用可見的薄荷色。列印規則明確覆寫場景背景，移除首屏與互動層，防止深底黑字及多餘首屏空間。

## 驗證與發布

桌面Chrome／Edge與Playwright WebKit為自動化驗證引擎；裝置尺寸及觸控模擬不等於真正的iPhone、Android或Mac Safari驗收。本次使用者明確允許有介面檢查，另以可見預覽補查。

發布前fetch並比對現有main，保留使用者修改；不得force push。只明確暫存本次程式、SVG與文件，不包含README.md或已忽略的私人／舊資產。最新執行結果、commit與部署狀態以CURRENT_STATUS.md為準。
