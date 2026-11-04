# Marp Slides

以 Markdown 撰寫簡報，推送至 GitHub 後自動轉換為 HTML，透過 GitHub Pages 瀏覽。

## 專案結構

```
slides/
  <slide-name>/
    slide.md        ← 簡報原檔
    assets/         ← 圖片等資源（選用）
themes/
  corporate.css     ← 自訂主題範例
.github/workflows/
  build.yml         ← 自動建置與部署
```

## 新增一份簡報

1. 在 `slides/` 下建立新目錄（建議以數字前綴排序，例如 `02-my-topic`）
2. 在目錄內建立 `slide.md`，加入 front matter：

```yaml
---
marp: true
title: 簡報標題      # 會顯示在首頁清單
paginate: true
transition: slide   # 投影片切換效果，僅在 HTML 輸出／預覽時有效（PDF、PPTX 不支援）
---
```

3. 推送至 `main`，GitHub Actions 自動建置並發佈。

## 主題選擇

在 `slide.md` 的 front matter 中指定 `theme`：

| 值 | 說明 |
|---|---|
| 省略（不寫）| 預設使用 **gaia** |
| `gaia` | Marp 內建主題 |
| `default` | Marp 內建主題 |
| `uncover` | Marp 內建主題 |
| `corporate` | 本專案自訂主題（`themes/corporate.css`）|
| `gaia-cust` | 擴充 gaia 的自訂主題（`themes/gaia-cust.css`）|

## corporate 主題的投影片類型

在頁面上方加入 `<!-- _class: <type> -->` 切換版面：

| `_class` | 說明 | 必要元素 |
|---|---|---|
| （省略）| 標準內容頁 | `# 標題` + `<hr>` + 內文 |
| `cover` | 封面 | `# 主標題` + `## 副標題` + `<hr>` + 說明 |
| `section-page` | 章節標題頁 | `<span class="num">01</span>` + `# 標題` |
| `lead` | 置中版面（移植自 gaia）| `# 標題` + `## 副標題` |
| `cols` | 兩欄比較 | `<div class="col-wrap">` 包覆兩個 `<div class="col">` |
| `triplet` | 三欄重點 | `<div class="triplet-wrap">` 包覆三個 `<div class="item">` |
| `quad` | 四欄重點 | `<div class="quad-wrap">` 包覆四個 `<div class="item">` |
| `stats` | 數據卡片 | `<div class="stat-wrap">` 包覆多個 `<div class="stat">` |
| `closing` | 結尾頁 | `# 標題` + `<hr>` + 聯絡資訊 |

`cols` 的次要欄加 `alt` class（`<div class="col alt">`）可改為白底框線樣式。  
`stats` 的強調卡片加 `hi` class（`<div class="stat hi">`）可改為深色背景。

## gaia-cust 主題的投影片類型

`cover`、`lead`、`section-page`、`cols`、`cols3`、`compare`、`quad`，用法見範例檔。

## 版面範例檔

- `slides/_template/slide.md`：corporate 主題
- `slides/_template-gaia/slide.md`：gaia-cust 主題

## 本機預覽

需先安裝 [Marp CLI](https://github.com/marp-team/marp-cli)：

```bash
npm install -g @marp-team/marp-cli

# 預覽特定簡報
marp --theme-set themes/ --html --allow-local-files --preview slides/slide-a/slide.md

# 轉換為 HTML
marp --theme-set themes/ --html --allow-local-files slides/slide-a/slide.md -o slide-a.html
```

## GitHub Pages 設定（一次性）

1. 前往 GitHub repo → **Settings** → **Pages**
2. Source 選擇 **GitHub Actions**
3. 推送至 `main` 即觸發自動部署

部署完成後，首頁網址為：`https://<user>.github.io/<repo>/`
