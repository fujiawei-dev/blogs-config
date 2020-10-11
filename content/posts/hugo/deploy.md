---
date: 2020-10-05T19:15:24+08:00  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "基于 Docker 部署 Hugo"  # 文章标题
description: "为了方便随时浏览，而不必每次都手动启动 Hugo 自带的服务器，缺点在于无法实时更新内容"
url:  "posts/hugo/deploy"  # 设置网页链接，默认使用文件名
tags: [ "hugo", "docker", "nginx"]  # 自定义标签
series: [ "博客系统摸爬滚打"]  # 文章主题/文章系列
categories: [ "浅尝辄止"]  # 文章分类

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

index: true  # 文章是否可以被索引
draft: false  # 草稿
---

## Hugo 容器部署

```shell
docker pull klakegg/hugo
```

`hugo server`

### 运行命令

**D 盘**

```shell
docker run --restart=always -itd --name hugo -v d:/onedrive/repositories/notes:/src:ro,z -p 12345:12345 klakegg/hugo server -p 12345
```

**H 盘**

```shell
docker run --restart=always -itd --name hugo -v h:/onedrive/repositories/notes:/src:ro,z -p 12345:12345 klakegg/hugo server -p 12345
```

**E 盘**

```shell
docker run --restart=always -itd --name hugo -v e:/onedrive/repositories/notes:/src:ro,z -p 12345:12345 klakegg/hugo server -p 12345
```

### 重启容器

端口号不一致将出现跨域问题。另外 Docker 无法实时更新。解决方法是创建 Windows 任务计划，定时重启。

```shell
docker restart hugo
```

## Nginx 容器部署

一个基本的适用于 Hugo 站点的 Nginx 配置如下：

{{< code language="html" title="/etc/nginx/conf.d/default.conf" id="1" expand="" collapse="" isCollapsed="false" >}}
server {
    listen       8080;
    server_name  localhost;

    index  index.html;

    root   /app/public;

    location / {
        try_files $uri $uri/index.html =404; #fixup for hugo
    }

    error_page   500 502 503 504  /50x.html;
    location = /50x.html {
        root   /usr/share/nginx/html;
    }
}
{{< /code >}}

然后直接运行 Docker 官方的 Nginx 容器，映射 `/etc/nginx/conf.d/default.conf` 配置文件，并映射 `/app/public` 目录即可：

**D 盘**

```shell
docker run -d --name hugo-nginx -v d:/onedrive/repositories/notes/public:/app/public:ro,z  -v d:/onedrive/repositories/notes/nginx.conf:/etc/nginx/conf.d/default.conf:z --mount type=tmpfs,destination=/tmp -p 8000:8080 nginx
```

**E 盘**

```shell
docker run -d --name hugo-nginx -v e:/onedrive/repositories/notes/public:/app/public:ro,z  -v e:/onedrive/repositories/notes/nginx.conf:/etc/nginx/conf.d/default.conf:z --mount type=tmpfs,destination=/tmp -p 8000:8080 nginx
```

不太对，CSS 都缺失了，待填坑。。。

原因是端口不一致。
