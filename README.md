# SQL Formatter

純前端的 SQL 即時格式化工具，特別針對 **MyBatis** 場景做了不少優化。整個應用就是單一檔案 `index.html`——沒有建置步驟、沒有後端、不用安裝，打開瀏覽器就能用。

## 功能

### 格式化
- **即時格式化**：輸入時自動排版（300ms debounce），也可按 `Format SQL` 或 `⌘↵` / `Ctrl+↵`。
- **11 種資料庫**：Standard SQL、MySQL、MariaDB、PostgreSQL、BigQuery、T-SQL、Spark、Hive、SQLite、Snowflake、Redshift。
- **縮排選項**：2 格 / 4 格 / Tab。
- **關鍵字大小寫**：保持原樣 / 大寫 / 小寫（只影響 SQL 關鍵字，不動表名、欄位名）。
- **註解處理**：可選「保留」或「移除」，支援 `--`、`/* */`、以及 XML 的 `<!-- -->` 三種註解。
- **Minify**：壓成單行，同樣可選保留 / 移除註解。

### MyBatis 支援
- **佔位符 `#{}` / `${}`**：正常格式化不會壞（解決 MySQL 把 `#` 當註解的問題），並在結果中以**琥珀色底色**凸顯。
- **動態標籤**：貼含 `<if>`、`<where>`、`<foreach>`、`<set>`、`<choose>` 等標籤的 mapper 片段，`Format SQL` 會自動辨識，讓標籤各自一行、依巢狀縮排，標籤間的 SQL 照常格式化；標籤以**紫色**與 SQL 關鍵字區分。
- **轉 CDATA**：`MyBatis` 下拉可把 `<`、`>`、`<=`、`>=`、`<>`、`&`、`&&` 個別包成 `<![CDATA[ … ]]>`，方便貼回 XML mapper；帶 CDATA 的 SQL 也會自動還原、不重複包。

### 輸入 / 輸出
- **匯入檔案**：支援 `.sql` / `.txt`，也可直接把檔案**拖進輸入框**。
- **下載結果**：存成 `.sql` 或 `.txt`。
- **匯出圖片**：把結果區塊轉成 PNG，可下載、複製到剪貼簿，或複製 Base64。
- **複製 / 回填**：一鍵複製格式化結果，或回填到輸入框繼續編輯。
- **一鍵範例**：載入示範 SQL 快速體驗各功能。

### 其他
- **分享連結**：把 SQL 與所有選項（資料庫、縮排、大小寫）編碼進網址，支援中文。
- **狀態記憶**：自動存進瀏覽器 LocalStorage，下次打開延續上次內容。
- **語法高亮**與輸入字數 / 行數統計。
- **友善錯誤提示**：格式化失敗時給白話說明，不是一長串英文錯誤。

## 使用方式

直接用瀏覽器開啟 `index.html` 即可：

```bash
open index.html
```

或把整個資料夾丟到任何靜態網站服務（GitHub Pages、Netlify 等）就能上線。

## 技術

所有依賴皆透過 CDN 載入，版本已釘死：

- [**sql-formatter**](https://github.com/sql-formatter-org/sql-formatter) `15.6.9` — 核心格式化引擎
- [**Prism**](https://prismjs.com/) `1.29.0` — SQL 語法高亮
- [**html2canvas**](https://html2canvas.hertzen.com/) `1.4.1` — 結果區塊轉圖片

沒有 `package.json`、沒有 build / lint / test 指令——改完 `index.html` 存檔、重新整理瀏覽器就能看到結果。
