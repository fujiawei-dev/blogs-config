---
date: 2020-10-06T00:22:22+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "给 Hugo 添加文章搜索功能"  # 标题
description: "Hugo 集成 Algolia 搜索"
url:  "posts/hugo/search"  # 设置网页永久链接
tags: [ "hugo", "algolia"]  # 自标签
series: [ "博客系统摸爬滚打"]  # 系列
categories: [ "浅尝辄止"]  # 分类

# 章节
weight: 20 # 排序优先级
chapter: false  # 设置为章节

index: true  # 是否可以被索引
draft: false  # 草稿
---

## 注册账号

官方网站 https://www.algolia.com/，创建新的索引。

## 安装插件

```shell
npm install hugo-algolia -g
```

然后在项目根目录下新建 `config.yaml` 文件：

```yaml
---
baseurl: "/"
DefaultContentLanguage: "zh-cn"
hasCJKLanguage: true
languageCode: "zh-cn"
title: "Life-Long Learning"
theme: "hello-friend"
metaDataFormat: "yaml"
algolia:
  index: "notes"
  # Admin API Key
  key: "fddb7ac05baf79cac5c291a4c000d162"
  appID: "V484EHT8P4"
---
```

## 修改配置

修改 config.toml 文件

```ini
# ======== 搜索 ========
[params.algolia]
  appId = "V484EHT8P4"
  indexName = "notes"
  searchOnlyKey = "4977360d5e70c48256a6f11534b05780"

[outputs]
    home = ["HTML", "RSS", "Algolia"]

[outputFormats.Algolia]
  baseName = "algolia"
  isPlainText = true
  mediaType = "application/json"
  notAlternative = true
# ======== 搜索 ========
```

新建 `list.algolia.json` 文件

```go
{{/* 生成 Algolia 搜索索引文件 */}}
{{- $.Scratch.Add "index" slice -}}
{{/* content/posts 或 content/post目录下的文件才生成索引 */}}
{{- range where (where .Site.Pages "Type" "in" (slice "posts" "post")) "IsPage" true -}}
  {{- if and (not .Draft) (not .Params.private) -}}
    {{- $.Scratch.Add "index" (dict "objectID" .File.UniqueID "url" .Permalink "content" (.Summary | plainify) "tags" .Params.Tags "lvl0" .Title "lvl1" .Params.Categories "lvl2" "摘要") -}}
  {{- end -}}
{{- end -}}
{{- $.Scratch.Get "index" | jsonify -}}
```

## 编译网站

> 在生成索引数据之前必须先编译网站。

```shell
hugo
```

## 生成索引

```shell
hugo-algolia -s
```

## 前端页面

前端是我从未深入学习过的领域。。。勉强改成了现在的样子。
