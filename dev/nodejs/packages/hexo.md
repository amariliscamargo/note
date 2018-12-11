---
date: '2018-12-02 19:52:29'
tags: [dev, nodejs, packages]
title: Hexo 使用指南
updated: '2018-12-11 17:16:29'
...
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
  - [clean](#clean)
- [优化](#%E4%BC%98%E5%8C%96)
    - [文件夹名称, 中划线小写](#%E6%96%87%E4%BB%B6%E5%A4%B9%E5%90%8D%E7%A7%B0-%E4%B8%AD%E5%88%92%E7%BA%BF%E5%B0%8F%E5%86%99)
    - [替换谷歌字体 \(众所周知的原因\)](#%E6%9B%BF%E6%8D%A2%E8%B0%B7%E6%AD%8C%E5%AD%97%E4%BD%93-%E4%BC%97%E6%89%80%E5%91%A8%E7%9F%A5%E7%9A%84%E5%8E%9F%E5%9B%A0)
    - [替换谷歌cnd加速地址 \(众所周知\)](#%E6%9B%BF%E6%8D%A2%E8%B0%B7%E6%AD%8Ccnd%E5%8A%A0%E9%80%9F%E5%9C%B0%E5%9D%80-%E4%BC%97%E6%89%80%E5%91%A8%E7%9F%A5)
    - [去掉幻灯片播放图片 fancybox: false](#%E5%8E%BB%E6%8E%89%E5%B9%BB%E7%81%AF%E7%89%87%E6%92%AD%E6%94%BE%E5%9B%BE%E7%89%87-fancybox-false)
    - [修复相对链接\(./ or ../\) 无法正确解析的问题](#%E4%BF%AE%E5%A4%8D%E7%9B%B8%E5%AF%B9%E9%93%BE%E6%8E%A5-or--%E6%97%A0%E6%B3%95%E6%AD%A3%E7%A1%AE%E8%A7%A3%E6%9E%90%E7%9A%84%E9%97%AE%E9%A2%98)

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
# 链接形式去掉 年月日
permalink: :title/

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

<a id="clean"></a>
### clean
```
hexo clean
```
清除缓存文件 (db.json) 和已生成的静态文件 (public)。  
在某些情况（尤其是更换主题后），如果发现您对站点的更改无论如何也不生效，您可能需要运行该命令。

<a id="%E4%BC%98%E5%8C%96"></a>
## 优化
<a id="%E6%96%87%E4%BB%B6%E5%A4%B9%E5%90%8D%E7%A7%B0-%E4%B8%AD%E5%88%92%E7%BA%BF%E5%B0%8F%E5%86%99"></a>
#### 文件夹名称, 中划线小写
<a id="%E6%9B%BF%E6%8D%A2%E8%B0%B7%E6%AD%8C%E5%AD%97%E4%BD%93-%E4%BC%97%E6%89%80%E5%91%A8%E7%9F%A5%E7%9A%84%E5%8E%9F%E5%9B%A0"></a>
#### 替换谷歌字体 (众所周知的原因)
```js
// 修改 /themes/landscape/layout/_partial/head.ejs
// 将 fonts.googleapis.com/css?family=Source+Code+Pro 替换为:
https://fonts.proxy.ustclug.org/css?family=Source+Code+Pro
```
<a id="%E6%9B%BF%E6%8D%A2%E8%B0%B7%E6%AD%8Ccnd%E5%8A%A0%E9%80%9F%E5%9C%B0%E5%9D%80-%E4%BC%97%E6%89%80%E5%91%A8%E7%9F%A5"></a>
#### 替换谷歌cnd加速地址 (众所周知)
```js
// 修改 /themes/landscape/layout/_partial/after-footer.ejs
// 将 jquery/2.0.3/jquery.min.js 替换为:
https://cdn.staticfile.org/jquery/2.0.3/jquery.min.js
```
<a id="%E5%8E%BB%E6%8E%89%E5%B9%BB%E7%81%AF%E7%89%87%E6%92%AD%E6%94%BE%E5%9B%BE%E7%89%87-fancybox-false"></a>
#### 去掉幻灯片播放图片 fancybox: false
```
// 修改 /themes/landscape/_config.yml
fancybox: false // fancybox 图片幻灯片展示,没必要
// 删除 /themes/landscape/source/fancybox
// 修改 /themes/landscape/Gruntfile.js 中 fancybox 相关的内容
```
<a id="%E4%BF%AE%E5%A4%8D%E7%9B%B8%E5%AF%B9%E9%93%BE%E6%8E%A5-or--%E6%97%A0%E6%B3%95%E6%AD%A3%E7%A1%AE%E8%A7%A3%E6%9E%90%E7%9A%84%E9%97%AE%E9%A2%98"></a>
#### 修复相对链接(./ or ../) 无法正确解析的问题
```
// 修改 /themes/landscape/source/js/script.js

```
