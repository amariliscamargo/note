---
categories: [life, book, technology, mysql-doc]
date: '2018-12-05 18:03:21'
tags: [life, book, technology, mysql-doc]
title: 1.4 MySQL 5.7中的新功能
updated: '2018-12-21 12:47:53'
...
---
# 1.4 MySQL 5.7中的新功能
<!-- MarkdownTOC -->

- [MySQL 5.7中添加的功能](#mysql-57%E4%B8%AD%E6%B7%BB%E5%8A%A0%E7%9A%84%E5%8A%9F%E8%83%BD)
- [MySQL 5.7中不推荐使用的功能](#mysql-57%E4%B8%AD%E4%B8%8D%E6%8E%A8%E8%8D%90%E4%BD%BF%E7%94%A8%E7%9A%84%E5%8A%9F%E8%83%BD)
    - [用户管理相关](#%E7%94%A8%E6%88%B7%E7%AE%A1%E7%90%86%E7%9B%B8%E5%85%B3)
- [MySQL 5.7中删除的功能](#mysql-57%E4%B8%AD%E5%88%A0%E9%99%A4%E7%9A%84%E5%8A%9F%E8%83%BD)

<!-- /MarkdownTOC -->
[回到系列教程主目录](../index.md)

<a id="mysql-57%E4%B8%AD%E6%B7%BB%E5%8A%A0%E7%9A%84%E5%8A%9F%E8%83%BD"></a>
## MySQL 5.7中添加的功能
-   管理员为自动密码过期建立策略
-   管理员可以锁定和解锁帐户
-   使用mysqld --initialize安装的MySQL部署默认是安全的(不会创建匿名用户帐户, 不会创建test 数据库)
-   InnoDB增强功能
-   JSON支持
-   sys架构
-   条件处理, MySQL现在支持堆栈诊断区域
-   日志记录
-   全球化改进,MySQL 5.7.4包含一个gb18030 支持中国国家标准GB18030字符集的字符集
-   将多个服务器备份到单个服务器
-   ...

<a id="mysql-57%E4%B8%AD%E4%B8%8D%E6%8E%A8%E8%8D%90%E4%BD%BF%E7%94%A8%E7%9A%84%E5%8A%9F%E8%83%BD"></a>
## MySQL 5.7中不推荐使用的功能
<a id="%E7%94%A8%E6%88%B7%E7%AE%A1%E7%90%86%E7%9B%B8%E5%85%B3"></a>
### 用户管理相关
-   不推荐使用`GRANT`创建用户; 请使用`CREATE USER`替代
-   不推荐使用`GRANT`锁定或解锁帐户; 请使用`CREATE USER`创建并用`ALTER USER`修改
-   ...

<a id="mysql-57%E4%B8%AD%E5%88%A0%E9%99%A4%E7%9A%84%E5%8A%9F%E8%83%BD"></a>
## MySQL 5.7中删除的功能
-   ...
