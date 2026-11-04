---
marp: true
theme: gaia-cust
title: 示範簡報（gaia-cust）
paginate: true
transition: slide
---

<!-- _class: cover -->

# Markdown

許智超

cchsu@mail.nsysu.edu.tw

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
