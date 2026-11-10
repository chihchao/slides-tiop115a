---
marp: true
theme: gaia-cust
title: Markdown × Gradio
paginate: true
transition: slide
---

<!-- _class: cover -->

# Markdown × Gradio

許智超

<cchsu@mail.nsysu.edu.tw>

---

<!-- _class: section-page -->

## Markdown

---

### Introduction

- Markdown的目標是「易讀易寫」
- HTML與Markdown，Markdown並不是取代HTML，而是相輔相成
    - HTML – 就像骨架，規劃整體的架構及格式
    - Markdown – 就像血肉，便於撰寫及閱讀內容
- Colab提供簡易編輯器協助編輯

---

### 標題

- 使用 # 建立標題

```markdown
# Title H1
## Title H2
### Title H3
```

---

### 段落及換行

- 空白行表示段落；二個空白加\n代表換行

```markdown
段落一

段落二  
段落二行內換行
```

---

### 強調文字

- 使用符號 * _
- 斜體 *text*
粗體 **text**

```markdown
*文字*  
**文字**
```

---

### 清單

- 無序清單符號 * + -，有序清單符號1. 2.
- 符號和文字間要加空白

```markdown
無序清單
* 星號
+ 加號
- 減號

有序清單
1. menu 1
2. menu 2
```

---

### 待辦事項

- 每行最前面加上-[ ]
- 符號和文字間要加空白

```markdown
- [ ] 待辦事項  
- [x] 完成事項
```

---

### 分隔線

- 三個或以上的 * - _

```markdown
***
---
___
```

---

### 連結

可用[text](link "title")及<link>的方式建立

```markdown
[中山大學](http://www.nsysu.edu.tw/ "Link to NSYSU")  
<http://www.nsysu.edu.tw>  
<chihchao@go.edu.tw>
```

---

### 引用

- 使用 > 建立引用文字

```markdown
> Fear can hold you prisoner. Hope can set you free.
```


---

### 圖片

- ![alt text](path/to/img.png "title")
- ![alt text][id]
搭配
[id]: url "title"

```markdown
![Python Logo](https://www.python.org/static/community_logos/python-logo-master-v3-TM.png "Python Logo")
![Python Logo][logo]

[logo]: https://www.python.org/static/community_logos/python-logo-master-v3-TM.png "Python Logo"
```

---

### 表格
- 依下列格式建置，冒號設定內容對齊方式，:- 靠左，-: 靠右，:-:置中

```markdown
| 項目 | 說明 | 數值 |
|------|------|------|
| 項目一 | 說明文字 | 100 |
| 項目二 | 說明文字 | 200 |
```

---

<!-- _class: section-page -->

## Gradio

---

### Gradio 簡介

[Gradio 官網](https://www.gradio.app/)

Gradio 是一個 Python 套件，核心目的是讓你在短短幾行程式碼內，為你的 Python 函式或機器學習模型建立一個美觀的網頁介面。三大特色：

- 極度簡單：你完全不需要懂得 HTML、CSS 或 JavaScript。只要定義好「輸入」和「輸出」，Gradio 就會自動幫你產生網頁。
- 多種元件：它內建了許多適合 AI 的元件，例如：文字輸入框、圖片上傳、語音辨識、結果信心度圖表（Label）等。
- 一鍵分享：只要在啟動時加上 share=True，它會產生一個公開連結，讓世界各地的其他人直接透過瀏覽器測試你的程式。


---

### 建置步驟

1. 安裝指令
```bash
!pip install gradio -q
```
安裝最新版：
```bash
!pip install --upgrade gradio -q
```

2. 定義函式: 定義處理函式或機器學習模型。
3. 建立介面: 使用 `gr.Interface` 綁定函式與元件。
4. 啟動伺服器: 執行 `.launch()` 啟動伺服器。


---

### 建立介面：gr.Interface

三大關鍵參數：
- fn: 你要呼叫的 Python 函式名。
- inputs: 定義輸入元件 (如："text", "slider")。
- outputs: 定義輸出元件 (如："label", "text")。

其他參數：
- flagging_mode='never'
- clear_btn=None
- live=True
- title=""


---

### Demo Hello World

```python
import gradio as gr

def greet(name):
    return f"Hello {name}!"

demo = gr.Interface(fn=greet, inputs="text", outputs="text")
demo.launch()
```
---

### 設定主題

- [Theme Gallery](https://www.gradio.app/themes/gallery)

```python
import gradio as gr

def greet(name):
    return f"Hello {name}!"

demo = gr.Interface( fn=greet, inputs="text", outputs="text",
    theme=gr.themes.Soft()
)
demo.launch()
```

- 新版請將 `theme=gr.themes.Soft()` 移至 `demo.launch()` 中

---

### 基礎輸入元件

| 元件名稱 | 程式碼範例 | 適用場景 |
| :--- | :--- | :--- |
| 文字框 | `gr.Textbox(label="姓名")` | 姓名、長文輸入 (`lines=3`) |
| 數字框 | `gr.Number()` | 年齡、價格、座標 |
| 滑塊 | `gr.Slider(0, 100)` | 參數微調、音量、機率 |
| 下拉選單 | `gr.Dropdown(["A", "B"])` | 類別、國家、多選一 |
| 單選鈕 | `gr.Radio(["男", "女"])` | 選項少時直覺選擇 |
| 核取方塊 | `gr.Checkbox()` | 布林值 (True/False) |
| 複選框群組| `gr.CheckboxGroup(["A", "B"])`| 多項同時勾選 |

---

### 基礎輸入元件：多媒體與檔案

| 元件名稱 | 程式碼範例 | 適用場景 |
| :--- | :--- | :--- |
| 圖片 | `gr.Image(type="numpy")` | 上傳圖片、手寫板、攝影 |
| 語音 | `gr.Audio()` | 錄音或音訊檔上傳 |
| 檔案 | `gr.File()` | 通用檔案上傳 (PDF, CSV 等) |

---

### Demo BMI 計算機

- 輸入：身高 (cm)、體重 (kg)
- 輸出：BMI 數值

```python
import gradio as gr

def bmi(height, weight):
    return weight / (height / 100) ** 2

demo = gr.Interface(fn=bmi, inputs=["number", "number"], outputs="number")
demo.launch()
```

---

### 基礎輸出元件

| 元件名稱 | 程式碼範例 | 適用場景 |
| :--- | :--- | :--- |
| Markdown | `gr.Markdown()` | 格式化標題、說明文字、LaTeX |
| 圖表 | `gr.Plot()` | Matplotlib/Plotly 數據視覺化 |
| 數據表格 | `gr.Dataframe()` | 顯示查詢結果、Pandas 表格 |
| 標籤 | `gr.Label()` | AI 分類機率、情緒預測結果 |
| 高亮文字 | `gr.HighlightedText()` | NER 實體辨識、關鍵字標註 |
| 相簿 | `gr.Gallery()` | 批量顯示生成的圖片或照片 |

---

### Demo 數據表格

- 美食資訊 CSV 網址：[點此前往](https://docs.google.com/spreadsheets/d/e/2PACX-1vSOA1er0nbdP347H0JgfsNpL8xbIEQefiufYS-Y6s2MJFg7LtkahTHLM6Hvczh_A4ZFLIwpj-8yEqJN/pub?gid=662007514&single=true&output=csv)

```python
import pandas as pd
import gradio as gr

CSV_URL = "url of csv on google drive"
df = pd.read_csv(CSV_URL)

def get_data():
    return df

demo = gr.Interface( fn=get_data,  inputs=[], outputs=gr.Dataframe(), title="雲端試算表顯示器",
    live=True,
    flagging_mode='never',
    clear_btn=None
)

demo.launch()
```

---

### 進階介面設計：gr.Blocks

當 `gr.Interface` 的固定排版（輸入在左/上，輸出在右/下）無法滿足需求時，我們可以使用 `gr.Blocks`：

- 高度自訂：隨意編排元件位置。
- 佈局元件：提供 `Row` (行)、`Column` (列)、`Tab` (分頁) 等容器。
- 精準觸發：可以指定特定按鈕點擊後觸發特定函式，甚至多個函式。
- 多功能整合：在同一個 App 內放多個不同的功能模組。

---

### gr.Blocks 佈局元件

使用 `with` 語句來定義排版結構：

| 元件 | 說明 |
| :--- | :--- |
| `gr.Row()` | 將內部的元件**橫向**排列。 |
| `gr.Column()` | 將內部的元件**縱向**排列（預設）。 |
| `gr.Tab("標題")` | 建立**分頁**容器。 |
| `gr.Accordion("標題")` | 建立可摺疊的**抽屜式**區域。 |

---

### gr.Blocks 範例：自訂排版

```python
import gradio as gr

with gr.Blocks() as demo:
    gr.Markdown("# 簡易 Blocks 範例")
    
    with gr.Row():
        inp = gr.Textbox(label="輸入文字")
        out = gr.Textbox(label="輸出結果")
    
    btn = gr.Button("執行")
    
    # 綁定事件：點擊按鈕後，將 inp 的值傳給函式，結果顯示在 out
    btn.click(fn=lambda x: x.upper(), inputs=inp, outputs=out)

demo.launch()
```

---

### HW06 數據篩選器

- 目標：設計一個能篩選數據的 Web 介面。
- 必須包含：
1. 至少 3 種 不同類型的輸入元件。
2. 能夠針對輸入給出正確的計算或篩選結果。
3. 介面需包含標題 (title) 與敘述 (description)。
