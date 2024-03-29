---
categories: [dev, linux, commands]
date: '2018-12-18 16:12:24'
tags: [dev, linux, commands]
title: 数据的显示
updated: '2018-12-21 12:47:53'
...
---
# 数据的显示
<!-- MarkdownTOC -->

- [cat](#cat)
    - [将标准输入导向到标准输出](#%E5%B0%86%E6%A0%87%E5%87%86%E8%BE%93%E5%85%A5%E5%AF%BC%E5%90%91%E5%88%B0%E6%A0%87%E5%87%86%E8%BE%93%E5%87%BA)
    - [显示文件](#%E6%98%BE%E7%A4%BA%E6%96%87%E4%BB%B6)
    - [组合文件](#%E7%BB%84%E5%90%88%E6%96%87%E4%BB%B6)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->
[回到系列教程主目录](./index.md)

<a id="cat"></a>
## cat

<a id="%E5%B0%86%E6%A0%87%E5%87%86%E8%BE%93%E5%85%A5%E5%AF%BC%E5%90%91%E5%88%B0%E6%A0%87%E5%87%86%E8%BE%93%E5%87%BA"></a>
### 将标准输入导向到标准输出
`cat a.txt` 的作用是: 通过`标准输入流`读取将文件 a.txt 的内容, 默认将读取的`字节流`导向到标准输出,显示到屏幕上

<a id="%E6%98%BE%E7%A4%BA%E6%96%87%E4%BB%B6"></a>
### 显示文件
将cat标准输入指向 m1，文本会从m1文件流到cat，然后再输出到屏幕上。
```bash
cat < m1 （在屏幕上显示文件 ml 的内容, 重定向标准输入可省略;等同于 cat m1）
cat < m1 < m2 （同时显示文件 ml 和 m2 的内容, 重定向标准输入可省略;等同于 cat m1 m2）
```
<a id="%E7%BB%84%E5%90%88%E6%96%87%E4%BB%B6"></a>
### 组合文件
同时重定向 标准输入和标准输出
将标准输入指向m1,并将m1的字节流导向到标准输出,然后将标准输出指向 f1
```bash
cat < m1 > f1 (将文件 m1 的内容复制到 文件 f1)
cat m1 m2 > file （将文件 ml 和 m2 合并后放入文件 file 中）
```

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[cat][] | [commands][]

[cat]:http://man.linuxde.net/cat
[commands]:../commands/index.md
