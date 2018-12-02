---
title: 'hexo'
date: '2018-12-02 19:52:29'
updated: '2018-12-02 19:52:29'
tags: ['dev', 'nodejs', 'packages']
---
# Hexo 使用指南

<!-- MarkdownTOC -->

- [安装](#%E5%AE%89%E8%A3%85)
- [初始化及目录结构](#%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8F%8A%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84)
- [配置](#%E9%85%8D%E7%BD%AE)
- [命令](#%E5%91%BD%E4%BB%A4)
    - [generate 生成](#generate-%E7%94%9F%E6%88%90)
    - [deploy 部署](#deploy-%E9%83%A8%E7%BD%B2)
    - [init](#init)
    - [new](#new)

<!-- /MarkdownTOC -->

> Hexo 是一个博客框架,使用 Markdown 等解析文章，可利用的主题快速生成静态网页

<a id="%E5%AE%89%E8%A3%85"></a>
## 安装
安装前提
-   Node.js
-   Git
```
npm install -g hexo-cli
```

<a id="%E5%88%9D%E5%A7%8B%E5%8C%96%E5%8F%8A%E7%9B%AE%E5%BD%95%E7%BB%93%E6%9E%84"></a>
## 初始化及目录结构
```
hexo init <folder>
cd <folder>
npm install
```

新建完成后，指定文件夹的目录如下：
```
|── _config.yml // 网站的 配置 信息
|── package.json // 包
|── scaffolds // 模版,新建文章时会根据 scaffold 来建立文件
|── source // 存放用户资源的地方
|    |── _posts // 将 markdown 文件放到下面,可以包含目录结构
|── themes // 主题,会根据主题来生成静态页面
```

source 说明:  
开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。  
Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去

<a id="%E9%85%8D%E7%BD%AE"></a>
## 配置
```
# Site 网站信息
title: "韩枫的博客"
description: "韩枫的博客"
keywords: "web开发"
author: 'han feng'
language: 'zh-CN'
timezone: 'Asia/Shanghai'

# URL 网站根目录
url: https://linkhanfeng.github.io/

# Deployment 网站 git 仓库地址
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: 'git@github.com:linkhanfeng/linkhanfeng.github.io.git'
  branch: master
  message: fromhexo
```

<a id="%E5%91%BD%E4%BB%A4"></a>
## 命令
<a id="generate-%E7%94%9F%E6%88%90"></a>
### generate 生成
```
hexo generate -d
```
生成静态文件  
-   -d, --deploy     文件生成后立即部署网站
-   -w, --watch     监视文件变动

<a id="deploy-%E9%83%A8%E7%BD%B2"></a>
### deploy 部署
```
hexo deploy -g
```
部署网站
`hexo deploy -g` 作用等同于 `hexo generate -d`
-   -g, --generate  部署之前预先生成静态文件

<a id="init"></a>
### init
```
hexo init [folder]
```
新建一个网站。如果没有设置 folder ，Hexo 默认在目前的文件夹建立网站。

<a id="new"></a>
### new
```
$ hexo new [layout] <title>
```
新建一篇文章。layout 默认使用`_config.yml 中的 default_layout`参数代替  
如果标题包含空格的话，请使用引号括起来。
