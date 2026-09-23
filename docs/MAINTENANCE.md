# 專案維護指南

本文件說明目前的檔案架構與日常維護流程。AI 協作者仍須先閱讀根目錄 `AGENTS.md`，再依其中順序閱讀其他文件。

## 專案架構

```text
Gong_Milestone/
├─ index.html                    # 唯一網站與 GitHub Pages 根頁面
├─ AGENTS.md                     # AI 協作規則與必讀順序
├─ CHANGELOG.md                  # 重要修改歷史
├─ README.md                     # 極簡 GitHub 專案名稱
├─ .gitignore
├─ assets/
│  ├─ animations/               # 11 份正式滿版動畫 SVG
│  └─ icons/                    # favicon 等介面圖示
├─ data/
│  └─ milestones.json           # 文案、資產關聯與完整動畫創作資料
├─ docs/                         # 設計、內容、狀態與維護文件
├─ archive/                      # 本機歷史資產；Git 忽略，不發布
└─ private/                      # 本機私人素材；Git 忽略，不發布
```

網站沒有建置步驟、套件管理器、後端或資料庫。GitHub Pages 直接發布根目錄 `index.html`。

## 修改里程碑文案

1. 先修改 `data/milestones.json` 的 `date` 或 `content`。
2. 同步 `docs/CONTENT_SOURCE.md`。
3. 同步 `index.html` 內相同 `data-milestone-id` 的靜態文字備援。
4. 驗證 JSON、Markdown 與 HTML 三者逐字一致。

不得把 `animation.name`、製作腳本或其他維護欄位渲染成網站可見標題。

## 新增里程碑與動畫

1. 在 `data/milestones.json` 複製相鄰物件，給予唯一 `id` 並選擇正確 `section`。
2. 依 `docs/ANIMATION_STORYBOARD.md` 完成內容轉譯、手機構圖、時間節拍、動態分層與循環規格。
3. 將正式 SVG 命名為小寫英文、數字與連字號組成的語意檔名，放入 `assets/animations/`。
4. JSON 的 `asset` 使用從 `index.html` 出發的完整相對路徑，例如 `assets/animations/2026-new-milestone.svg`。
5. 在 `index.html` 加入相同事件的靜態 HTML、外部 SVG 路徑及減少動態／列印備援。
6. 同步 CONTENT_SOURCE、CURRENT_STATUS、ANIMATION_STORYBOARD 與 CHANGELOG。

## 檔名規則

- 正式動畫：`日期或範圍-事件語意.svg`
- 只用小寫 ASCII、數字與 `-`，不使用空格、底線或中文。
- 正式網站資產只放 `assets/`；歷史版本放 `archive/`；私人素材放 `private/`。
- GitHub Pages 路徑大小寫敏感，程式、JSON 與實際檔名必須完全一致。

## 本機驗證

- JavaScript 語法與主要 HTML 標籤平衡。
- JSON 可解析、里程碑 id 唯一，所有 asset 路徑存在。
- HTML 靜態 SVG 路徑與 JSON 完全一致。
- SVG 可解析為 XML，無腳本、外部圖片或外部網路引用。
- SMIL 動畫節點與循環狀態未意外改變。
- 本機 HTTP 伺服器下，首頁、JSON、favicon 與每份正式 SVG 均回應 200。
- 無 JavaScript、減少動態及 A4 列印仍可閱讀完整文案。
- `git diff --check` 通過，`archive/` 與 `private/` 未進入提交。

專案規則禁止預設使用可見瀏覽器驗證；只有使用者在當次要求明確指定時才使用。

## GitHub Pages 發布

發布前先 fetch 並確認 `main` 與 `origin/main` 無分歧。路徑搬移必須和所有引用修正放在同一個提交中，不得只推送其中一半。發布後以公開網址確認首頁、JSON、favicon 與 11 份動畫全部回應 200，再把實際結果寫入 CURRENT_STATUS.md。
