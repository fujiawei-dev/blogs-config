---
title: "Markdown 示例"
date: "2020-10-04"
author: "Rustle Karl"
---

这里展示了 Markdown 的语法，同时展示了该网站实现的内容呈现能力。

## 多级标题

# H1

## H2

### H3

#### H4

##### H5

###### H6

## 段落

仅仅是普通文本是不够的，来试一试**加粗文字**吧！

I was reading *Les Misérables* recently.

## 引用

> Here shows the content presentation capabilities of the website.

> Don’t communicate by sharing memory, share memory by communicating.
>
> — *Rob Pike*[1](#引用)

## 表格

### 普通表格

| Name | Age |
| ----- | ---- |
| Bob | 27 |
| Alice | 23 |

### 表格内联

| Inline | Markdown | In | Table  |
| --------- | --------- | --------- | --------- |
| *italics* | **bold** | ~~strikethrough~~ | `code` |

### 普通代码块

我特别喜欢这个代码块的设计，鼠标指向右上角就可以复制内容，太酷了！

```html
<!-- HTML code -->

<section id="main">
  <div>
   <h1 id="title">{{ .Title }}</h1>
    {{ range .Pages }}
      {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
```

### 可折叠代码块

{{< code language="html" title="Collapsable Code" id="1" expand="" collapse="" isCollapsed="false" >}}
<!-- HTML code -->

<section id="main">
  <div>
   <h1 id="title">{{ .Title }}</h1>
    {{ range .Pages }}
      {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{< /code >}}

## 列表

### Ordered List

1. First item
2. Second item
3. Third item

### Unordered List

- List item
- Another item
- And another item

### Nested list

- Item

1. First Sub-item
2. Second Sub-item
