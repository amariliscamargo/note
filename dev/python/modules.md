---
date: '2018-12-09 15:56:21'
tags: [dev, python]
categories: [dev, python]
title: 模块
updated: '2018-12-09 18:39:03'
...
---
# 模块
<!-- MarkdownTOC -->

- [模块](#%E6%A8%A1%E5%9D%97)
- [字节码文件 .pyc](#%E5%AD%97%E8%8A%82%E7%A0%81%E6%96%87%E4%BB%B6-pyc)
- [from..import 语句](#fromimport-%E8%AF%AD%E5%8F%A5)
- [模块的`__name__`](#%E6%A8%A1%E5%9D%97%E7%9A%84__name__)
- [创建你自己的模块](#%E5%88%9B%E5%BB%BA%E4%BD%A0%E8%87%AA%E5%B7%B1%E7%9A%84%E6%A8%A1%E5%9D%97)
- [dir 函数](#dir-%E5%87%BD%E6%95%B0)
- [程序包](#%E7%A8%8B%E5%BA%8F%E5%8C%85)
- [小结](#%E5%B0%8F%E7%BB%93)

<!-- /MarkdownTOC -->
[回到目录](./index.md)

你已经看到了如何在你的程序中重复使用代码——只需定义一次`函数`就可以对其重复调用了。  
如果你想在其他程序中复用你写的大量的函数时，怎么办？可能你已经猜到了，答案就是`模块`。

编写模块的方式:
1.  最简单的方式就是创建一个包含很多方法和变量并以 .py 为扩展的文件。
2.  用编写 Python 解释器的语言来编写模块。例如，你可以用 C 语言 来写模块，在使用标准 Python 解释器中进行编译时，这些模块会从你的 Python 代码中调用。

使用模块的方法:

<a id="%E6%A8%A1%E5%9D%97"></a>
## 模块
<a id="%E5%AD%97%E8%8A%82%E7%A0%81%E6%96%87%E4%BB%B6-pyc"></a>
## 字节码文件 .pyc
<a id="fromimport-%E8%AF%AD%E5%8F%A5"></a>
## from..import 语句
<a id="%E6%A8%A1%E5%9D%97%E7%9A%84__name__"></a>
## 模块的`__name__`
<a id="%E5%88%9B%E5%BB%BA%E4%BD%A0%E8%87%AA%E5%B7%B1%E7%9A%84%E6%A8%A1%E5%9D%97"></a>
## 创建你自己的模块
<a id="dir-%E5%87%BD%E6%95%B0"></a>
## dir 函数
<a id="%E7%A8%8B%E5%BA%8F%E5%8C%85"></a>
## 程序包
<a id="%E5%B0%8F%E7%BB%93"></a>
## 小结
