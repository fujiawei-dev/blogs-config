---
date: 2020-10-08T18:51:23+08:00  # 创建日期
author: "Rustle Karl"  # 作者
# cover: "/examples/imgs"  # 封面图，可以是相对于 static 的路径，也可以是相对于当前的路径

# 文章
title: "将 Hugo 网站分享到局域网"  # 文章标题
description: "在局域网内分享 Hugo 网站"
url:  "posts/2020/10/08/wlanshare"  # 设置网页链接，默认使用文件名
tags: [ "hugo"]  # 自定义标签
series: [ "博客系统摸爬滚打"]  # 文章主题/文章系列
categories: [ "浅尝辄止"]  # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

index: true  # 文章是否可以被索引
draft: false  # 草稿
toc: false  # 是否自动生成目录
---

在启动 Hugo 服务器的时候必须指定两个参数：

```shell
hugo server --bind 0.0.0.0 --baseURL http://192.168.199.140/ -p 12347
```

- `-bind 0.0.0.0` ：局域网 IP
- `-baseURL` ： 覆盖 baseURL 参数，不加这个参数的话网站上的相关图片会显示不出来，即使配置文件里已经改了，似乎也无效
