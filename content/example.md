---
title: "Markdown 语法与内容编辑示例"
date: "2020-10-04"
author: "Rustle Karl"
cover: "/examples/[CAH]20160428162520.jpg"
---

## 作者

{{<friend desc="这里展示了内容编辑基本语法，同时展示了网站的内容呈现能力。" url="https://github.com/fujiawei-dev" email="fu.jiawei@outlook.com" nickName="Rustle Karl" >}}

设置了一行只展示一人，改的话必须修改源码，挺难搞的。因为 shortcode 的原因，无法显示源码是什么，以下都是删除了 `{{` 与代码之间的空格。

```html
{{ <friend desc="这里展示了内容编辑基本语法，同时展示了网站的内容呈现能力。" url="https://github.com/fujiawei-dev" email="fu.jiawei@outlook.com" nickName="Rustle Karl" > }}
```

## 多级标题

# H1

## H2

### H3

目录不显示一级标题，且只能呈现到三级标题。

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

| Name  | Age |
| ----- | --- |
| Bob   | 27  |
| Alice | 23  |

### 表格内联

| Inline    | Markdown | In                | Table  |
| --------- | -------- | ----------------- | ------ |
| *italics* | **bold** | ~~strikethrough~~ | `code` |

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
  - Another item
  - And another item

## 代码块

### 普通代码块

> 鼠标指向右上角就可以复制内容。

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

```shell
{{ <code language="html" title="Collapsable Code" id="1" expand="" collapse="" isCollapsed="false" > }}

{{ </code > }}
```

{{<code language="html" title="Collapsable Code" id="1" expand="" collapse="" isCollapsed="false" >}}
<!-- HTML code -->

<section id="main">
  <div>
   <h1 id="title">{{ .Title }}</h1>
    {{ range .Pages }}
      {{ .Render "summary"}}
    {{ end }}
  </div>
</section>
{{</code >}}

## 图片

### 只显示图片

```shell
{{ <image src="/examples/[CAH]20200203151427.png" alt="雨中的女孩" position="center" style="border-radius: 8px;" > }}
```

{{<image src="/examples/[CAH]20200203151427.png" alt="雨中的女孩" position="center" style="border-radius: 8px;" >}}

### 带标题的图片

```shell
{{ <figure src="/examples/[JAV]20191212085133.png" alt="蓝天枫树" position="left" style="border-radius: 8px; width: 400px; height: auto;" caption="蓝天枫树" captionPosition="center" captionStyle="color: white; font-size: 18px; padding-top: 10px" > }}
```

{{<figure src="/examples/[JAV]20191212085133.png" alt="蓝天枫树" position="left" style="border-radius: 8px; width: 400px; height: auto;" caption="蓝天枫树" captionPosition="center" captionStyle="color: white; font-size: 18px; padding-top: 10px" >}}

## 卡片式显示内链

**这个东西是文件系统的路径，坑死我了！**

```shell
{{ <link "music"> }}
```

{{<link "about">}}

## 音乐

### 网易云音乐歌单

嵌入歌单将导致中文目录页内跳转失败，原因未知。

```shell
{{ <music auto="https://music.163.com/#/playlist?id=439191388"> }}
```

个人网易云音乐歌单合辑：

{{<link "music">}}

## 看板娘

页面左下角，关闭了设置和对白。

```toml
[params]
  # 是否开启看板娘
  live2D = true
```

## 评论区

评论区基于 Valine 和 Leancloud 实现。
