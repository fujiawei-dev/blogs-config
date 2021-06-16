---
title: "个人博客系统"
date: "2020-10-04"
author: "Rustle Karl"
---

# 个人博客系统

> Powered by Hugo

自定义的部件（搜索/目录等）不太完美，不过也不太想折腾。。。

## Release

在 Release 页面下载可执行文件即可。

```url
https://github.com/gohugoio/hugo/releases
```

然后设置环境变量。

## Docker 

```shell
docker pull klakegg/hugo
```

进入 Shell 终端：

```shell
docker run --rm -it --name hugo -v d:/onedrive/repositories/notes:/src -p 7856:7856 klakegg/hugo:0.74.3-alpine shell
```

```shell
docker attach hugo --detach-keys=ctrl-d
```

```shell
hugo server -p 8080
```

## 基本命令

```shell
hugo [command] [flags]
```

### 新建项目

```shell
hugo new site myblogs
```

### 添加主题

```shell
git submodule add https://github.com/panr/hugo-theme-hello-friend.git themes/hello-friend
```

### 新建文件

都是以 `content` 为相对路径，该路径可以在配置文件中自定义。

```shell
hugo new posts/quickstart.md

hugo new posts/docker/quickstart.md
```

## 编译网站

### 本地预览

编译生成缓存的静态文件，然后启动本地服务用于预览：

```shell
hugo server

# 指定主题
hugo server -t hello-friend-ng
hugo server -t hello-friend
```

手动结束命令后，将会清除缓存的静态文件。

### 生成静态文件

生成静态文件，输出到默认的 `public` 目录：

```shell
hugo
```

## 项目结构

```shell
.
├─archetypes         # Markdown 文件的模板，通常用来自定义设置扉页等
| └─default.md       # 缺省预设的一个模板
├─content            # 内容目录，存放网站内所有内容文件的源代码
| ├─_index.md        # 网站的主页
| ├─chapter        # 章节目录，内容文件分类存放
| | ├─_index.md      # 章节的主页
| | ├─content      # 章节内的子页面目录
| |   ├─xxx.md       # 子页面内容，通常是 Markdown 文件
| |   └─imgs      # Markdown 文件引用的图片 
├─data               # 网站的自定义配置文件，文件类型可以是 yaml|toml|json 等格式
├─layouts            # 布局目录，存放渲染 content 目录的模版文件，模版的文件类型是 html 格式
├─resource           # 主题产生的目录
├─static             # 静态资源目录，存放静态资源文件
├─themes             # 主题目录
| └─xxx          # 安装后的主题名称
| | └─layouts        # 某个主题下的网站模板文件
├─public             # 编译后生成的网站文件
└─config.toml        # 网站的配置文件
```

## URL 转换

```shell
├─content           # 网站源代码目录
| ├─_index.md       # URL转换为：https://example.com/
| ├─posts           # 一个名为 posts 的章节文件夹
| | ├─_index.md     # URL 转换为：https://example.com/posts/
| | ├─first.md      # URL 转换为：https://example.com/posts/first/
| | └─topic         # 章节内的子页面内容目录
| | | ├─second.md   # URL 转换为：https://example.com/posts/topic/second/
| | | └─xxx.jpg     # second.md 文件引用的本地图片
```

## 主题

若想修改主题，首先定位 HTML 文件了解主题的架构、使用浏览器的开发者工具了解标签元素和其样式，然后遵循此页面新建一个 HTML/JavaScript/CSS 文件，直接修改主题代码是一个坏习惯。

比如修改主题的预设部件 `layouts/partials` 中的文件，在项目 `layouts/partials` 目录内自定义一个同名文件即可，优先级高于主题预设的部件。

## 扉页

扉页用来配置文章的标题、时间、链接、分类等元信息，提供给模板调用。除了网站主页外，其它内容文件都需要扉页来识别文件类型和编译文件。

```yaml
---
date: {{ .Date }}  # 创建日期
author: "Rustle Karl"  # 作者

# 文章
title: "{{ replace .Name "-" " " | title }}"  # 文章标题
description: "文章描述"
url:  "{{ .Name }}"  # 设置网页链接，默认使用文件名
tags: [ "tag1", "tag2"] # 自定义标签

# 章节
weight: 20 # 文章在章节中的排序优先级，正序排序
chapter: false  # 将页面设置为章节

draft: false  # 草稿
---
```

## 自定义分类

- tag：文章标签
- topic：文章主题/文章系列
- category：文章分类

### 配置分类

在 `config.toml` 中增加分类。

```ini
[taxonomies]
  tag = "tags"
  series = "series"
  category = "categories"
```

而将每个 post 的头部也相应增加对应的分类：

```yaml
tags: ["hugo"]
series: ["部署个人博客系统"]
categories: ["浅尝辄止"]
```

### 分类集合列表

- `example.com/tags/` 列出 tags 中的所有术语；
- `example.com/tags/docker` 列出 tags 标为 docker 的所有网页列表。
