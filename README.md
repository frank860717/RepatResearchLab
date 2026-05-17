# 研究筆記 — GitHub Pages

個人投資研究報告歸檔站,使用 GitHub Pages 託管。

## 目錄結構

```
notes/
├── index.html          # 儀表板 (首頁,自動載入 reports.json 產生卡片)
├── reports.json        # 報告清單 (新增報告時手動更新)
├── reports/            # 所有 HTML 報告檔
│   └── DDR4_DDR5_報價追蹤_20260517.html
└── README.md
```

---

## 一次性設定 — 啟用 GitHub Pages

1. 把這個資料夾的內容上傳到 GitHub repo 根目錄 (上傳方法見下方)
2. 進入 repo → **Settings** → 左側選單 **Pages**
3. **Source** 區塊選 **Deploy from a branch**
4. **Branch** 選 `main` (或 `master`) → 資料夾選 `/ (root)` → **Save**
5. 約 1~2 分鐘後重新整理,頁面頂部會出現網址:
   `https://你的帳號.github.io/notes/`
6. 點進去確認 index 載入正常即完成

---

## 日常 — 新增一份報告

### 方法 A:網頁拖拉上傳 (最簡單)

1. 開啟 GitHub repo 主頁
2. 進入 `reports/` 資料夾
3. 點右上角 **Add file** → **Upload files**
4. 把新的 HTML 檔拖進去
5. 下方填寫 commit message (例如「Add 0050 ETF report」)
6. 點 **Commit changes**

接著更新 `reports.json`:

1. 回到 repo 根目錄,點 `reports.json`
2. 點右上角鉛筆圖示「Edit」
3. 在陣列開頭 (`[` 之後) 加入新的物件,**記得在前一筆後加逗號**:

```json
[
  {
    "file": "新報告檔名.html",
    "title": "報告標題",
    "date": "2026-05-20",
    "summary": "一句話摘要,會顯示在卡片中。",
    "tags": ["dram", "taiwan"]
  },
  {
    "file": "DDR4_DDR5_報價追蹤_20260517.html",
    ...
  }
]
```

4. 點下方 **Commit changes**
5. 約 30 秒後重整網站首頁即可看到新卡片

### 方法 B:用 git 指令 (適合熟悉者)

```bash
git clone https://github.com/你的帳號/notes.git
cd notes
# 把新 HTML 放進 reports/
# 編輯 reports.json
git add .
git commit -m "Add new report"
git push
```

---

## reports.json 欄位說明

| 欄位 | 必填 | 說明 |
|------|------|------|
| `file` | ✅ | HTML 檔名 (放在 `reports/` 目錄下) |
| `title` | ✅ | 卡片標題 |
| `date` | ✅ | 報告日期,格式 `YYYY-MM-DD` (用於排序) |
| `summary` | 建議 | 1~2 句摘要,顯示在卡片中 |
| `tags` | 建議 | 標籤陣列,用於篩選 |

### 可用 tags (可自行擴充)

| tag key | 顯示名稱 | 顏色 |
|---------|----------|------|
| `dram` | DRAM | 金 |
| `semi` | 半導體 | 藍 |
| `dcf` | DCF 估值 | 紫 |
| `taiwan` | 台股 | 綠 |
| `us` | 美股 | 紅 |
| `ai` | AI 供應鏈 | 灰 |
| `earnings` | 財報 | 灰 |
| `macro` | 總經 | 灰 |

若要新增 tag 樣式,編輯 `index.html` 中的 `tagLabels` 物件與 CSS 中的 `.card .tag.xxx` 區塊。

---

## 常見問題

**Q: 我不想公開報告內容怎麼辦?**
A: GitHub Pages 免費版只支援 Public repo。如需私密,有兩個選項:
- 升級 GitHub Pro ($4/月) 即可在 Private repo 使用 Pages
- 或改用 Cloudflare Pages,免費版即可私密部署 (連 Cloudflare Access 做密碼保護)

**Q: 網址可以用自己的網域嗎?**
A: 可以。買網域後在 repo Settings → Pages → Custom domain 填入即可,GitHub 會自動處理 HTTPS。

**Q: 報告太多卡片載入很慢?**
A: 目前一次載入全部 JSON,大約 200 筆內都很快。超過後可改為分頁或按年份分檔。

**Q: 想加 Google Analytics / Plausible?**
A: 在 `index.html` 的 `</head>` 前貼入追蹤 script 即可。
