---
date: 2020-10-07T02:06:35+08:00  # 创建日期
author: "Rustle Karl"  # 作者
# cover: "/examples/imgs"  # 封面图，可以是相对于 static 的路径，也可以是相对于当前的路径

# 文章
title: "修改 Hugo 源代码允许访问工作目录之外的文件"  # 文章标题
description: "官方不允许程序访问工作目录之外的文件，没办法只能动手修改 Hugo 源码，然后重新编译"
url:  "posts/hugo/readdir"  # 设置网页链接，默认使用文件名
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

暴力改成直接读取目录

`tpl/os/os.go`

```go
// ReadDir lists the directory contents relative to the configured WorkingDir.
func (ns *Namespace) ReadDir(i interface{}) ([]_os.FileInfo, error) {
	path, err := cast.ToStringE(i)
	if err != nil {
		return nil, err
	}

    //list, err := afero.ReadDir(ns.deps.Fs.WorkingDir, path)
    // 暴力改成直接读取目录
	list, err := ioutil.ReadDir(path)
	if err != nil {
		return nil, fmt.Errorf("failed to read directory %q: %s", path, err)
	}

	return list, nil
}
```
