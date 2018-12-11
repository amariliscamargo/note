---
date: '2018-12-07 13:34:54'
tags: [life, book, technology, mysql-doc]
title: 1.5 MySQL 5.7中添加,弃用,或删除的配置项
updated: '2018-12-10 18:35:59'
...
---
# 1.5 MySQL 5.7中添加,弃用,或删除的配置项
<!-- MarkdownTOC -->

- [QL 5.7 引入的选项或变量](#ql-57-%E5%BC%95%E5%85%A5%E7%9A%84%E9%80%89%E9%A1%B9%E6%88%96%E5%8F%98%E9%87%8F)
- [QL 5.7 不推荐使用的选项或变量](#ql-57-%E4%B8%8D%E6%8E%A8%E8%8D%90%E4%BD%BF%E7%94%A8%E7%9A%84%E9%80%89%E9%A1%B9%E6%88%96%E5%8F%98%E9%87%8F)
- [QL 5.7 删除的选项或变量](#ql-57-%E5%88%A0%E9%99%A4%E7%9A%84%E9%80%89%E9%A1%B9%E6%88%96%E5%8F%98%E9%87%8F)

<!-- /MarkdownTOC -->
[回到目录](../index.md)

<a id="ql-57-%E5%BC%95%E5%85%A5%E7%9A%84%E9%80%89%E9%A1%B9%E6%88%96%E5%8F%98%E9%87%8F"></a>
## QL 5.7 引入的选项或变量
-   `default_password_lifetime`：密码有效过期
-   `Connection_control_delay_generated`：服务器延迟连接请求的次数
-   等等
<a id="ql-57-%E4%B8%8D%E6%8E%A8%E8%8D%90%E4%BD%BF%E7%94%A8%E7%9A%84%E9%80%89%E9%A1%B9%E6%88%96%E5%8F%98%E9%87%8F"></a>
## QL 5.7 不推荐使用的选项或变量
-   `Qcache_free_memory`：查询缓存的可用内存量
-   等等
<a id="ql-57-%E5%88%A0%E9%99%A4%E7%9A%84%E9%80%89%E9%A1%B9%E6%88%96%E5%8F%98%E9%87%8F"></a>
## QL 5.7 删除的选项或变量
-   `Max_statement_time_exceeded`：超过执行超时值的语句数
-   等等
