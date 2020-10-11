---
date: 2020-10-07T15:27:46+08:00  # 创建日期
author: "Rustle Karl"  # 作者
# cover: "/examples/imgs"  # 封面图，可以是相对于 static 的路径，也可以是相对于当前的路径

# 文章
title: "Hugo 全局创建模板文件技巧"  # 文章标题
description: "必须在根目录才能渲染生成基础文件太膈应人的，为此我创建了命令别名"
url:  "posts/hugo/skills"  # 设置网页链接，默认使用文件名
tags: [ "hugo", "skills", "alias"]  # 自定义标签
series: [ "博客系统摸爬滚打"]  # 文章主题/文章系列
categories: [ "浅尝辄止"]  # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

index: true  # 文章是否可以被索引
draft: false  # 草稿
toc: false  # 是否自动生成目录
---

```ps1
code $profile
```

```ps1
# hugo new
function HugoNew { hugo.exe new -s D:\OneDrive\Repositories\notes $args }
Set-Alias -Name hn -Value HugoNew

# hugo server
function HugoServer {
    cd D:\OneDrive\Repositories\notes
    hugo.exe server
}
Set-Alias -Name hs -Value HugoServer
```

```ps1
& $profile
```
