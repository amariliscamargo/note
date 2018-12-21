---
categories: [life, book, technology, mysql-doc]
date: '2018-12-10 18:54:03'
tags: [life, book, technology, mysql-doc]
title: ' MySQL 与 SQL标准'
updated: '2018-12-21 12:47:44'
...
---
#  MySQL 与 SQL标准
<!-- MarkdownTOC -->

- [1.8.1 标准SQL的MySQL扩展](#181-%E6%A0%87%E5%87%86sql%E7%9A%84mysql%E6%89%A9%E5%B1%95)
- [1.8.2 MySQL与标准SQL的区别](#182-mysql%E4%B8%8E%E6%A0%87%E5%87%86sql%E7%9A%84%E5%8C%BA%E5%88%AB)
- [1.8.3 MySQL如何处理约束](#183-mysql%E5%A6%82%E4%BD%95%E5%A4%84%E7%90%86%E7%BA%A6%E6%9D%9F)

<!-- /MarkdownTOC -->
[回到系列教程主目录](../index.md)

我们对该产品的主要目标之一是继续努力遵守SQL标准，但不会牺牲速度或可靠性。  
我们不怕添加SQL扩展或支持非SQL功能，如果这大大增加了可用性。例如:13.2.4节“HANDLER语法”  

我们继续支持事务性和非事务性数据库，以满足任务关键型24/7使用和繁重的Web或日志记录使用。

MySQL服务器最初设计用于在小型计算机系统上使用中型数据库（1000万-100万行，或每个表约100MB）。  
今天MySQL服务器处理数TB大小的数据库，但代码也可以编译成适用于手持和嵌入式设备的简化版本

MySQL使用NDBCLUSTER存储引擎支持高可用性数据库集群

我们实现支持 XML 和 JSON

MySQL服务器可以在不同的SQL模式下运行

<a id="181-%E6%A0%87%E5%87%86sql%E7%9A%84mysql%E6%89%A9%E5%B1%95"></a>
## 1.8.1 标准SQL的MySQL扩展

MySQL Server支持一些您可能在其他SQL DBMS中找不到的扩展。
请注意，如果您使用它们，您的代码将无法移植到其他SQL服务器。
在某些情况下，您可以使用以下格式的注释编写包含MySQL扩展的代码，但仍可移植。
`/*! MySQL-specific code */`

<a id="182-mysql%E4%B8%8E%E6%A0%87%E5%87%86sql%E7%9A%84%E5%8C%BA%E5%88%AB"></a>
## 1.8.2 MySQL与标准SQL的区别
我们尝试使MySQL Server遵循ANSI SQL标准和ODBC SQL标准，但MySQL Server在某些情况下执行不同的操作

<a id="183-mysql%E5%A6%82%E4%BD%95%E5%A4%84%E7%90%86%E7%BA%A6%E6%9D%9F"></a>
## 1.8.3 MySQL如何处理约束
1.8.3.1 PRIMARY KEY和UNIQUE索引约束
1.8.3.2外键约束
1.8.3.3对无效数据的约束
1.8.3.4 ENUM和SET约束
