---
date: 2020-10-10T21:33:50+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "记录 Hugo 日常问题"  # 文章标题
description: "记录在使用 Hugo 的过程中遇到的各种问题"
url:  "posts/hugo/problems"  # 设置网页永久链接
tags: [ "hugo", "problems"]  # 标签
series: [ "博客系统摸爬滚打"]  # 系列
categories: [ "浅尝辄止"]  # 分类

# 章节
weight: 20 # 排序优先级
chapter: false  # 设置为章节

index: true  # 是否可以被索引
toc: true  # 是否自动生成目录
draft: false  # 草稿
---

# 外置 exFAT 格式硬盘编译错误

```
hugo
Start building sites …
Total in 15540 ms
Error: Error copying static files: chtimes your\path\to\site\: The parameter is incorrect.
```

在 StackOverflow 找到了一样的问题，唯一的回答是可能网站源码放在了 exFAT 格式的移动硬盘中，跟我的情况一模一样。

```
https://stackoverflow.com/questions/64069079/blogdownserve-site-error-copying-static-files
```

```
hugo.exe -b / -D -F -d "public" --themesDir themes -t hugo-lithium --noTimes
```
