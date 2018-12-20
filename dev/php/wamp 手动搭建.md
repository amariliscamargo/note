---
categories: [dev, php]
date: '2018-11-08 22:06:06'
tags: [dev, php, 环境]
title: Windows Server wamp 环境手动搭建
updated: '2018-12-20 16:40:01'
...
---
# Windows Server wamp 环境手动搭建

<!-- MarkdownTOC -->

- [说明](#%E8%AF%B4%E6%98%8E)
- [apache](#apache)
- [mysql](#mysql)
- [php](#php)
- [关联 Apache MySQL PHP](#%E5%85%B3%E8%81%94-apache-mysql-php)
- [wamp 相关命令](#wamp-%E7%9B%B8%E5%85%B3%E5%91%BD%E4%BB%A4)
- [bat 脚本启动和关闭 wamp](#bat-%E8%84%9A%E6%9C%AC%E5%90%AF%E5%8A%A8%E5%92%8C%E5%85%B3%E9%97%AD-wamp)
- [参考链接](#%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5)

<!-- /MarkdownTOC -->

<a id="%E8%AF%B4%E6%98%8E"></a>
### 说明
系统: `Windows Server 2012 R2 64 位`

<a id="apache"></a>
### apache
-   版本选择 apache 2.4 Vc11 (因为 2.4 可以与 php7线程安全版本 匹配, 且都是用的 vc11)
-   [Apache 2.4 VC11 下载地址](https://www.apachehaus.com/cgi-bin/download.plx#APACHE24VC11) 注意不同版本 apache 对应的 vc 库 
    -   将软件包 解压到 C:\apmenv  
    -   阅读 readme_first.html 文件并按照文件进行安装
        -   请务必安装所需的 Visual C ++ 2012 x64 (注意 VC11 对应Visual C ++ 2012 而不是 2011) [下载地址](https://www.microsoft.com/en-us/download/details.aspx?id=30679)
        -   修改 C:\apmenv\Apache24\conf\httpd.conf 文件中的 ServerRoot 地址
        -   测试是否安装成功: 打开 cmd , 把目录切换到 C:\apmenv\Apache24\bin, 执行 httpd.exe

-   安装为 windows 服务
    ```
    httpd -k install
    ```
    启动命令:注意必须具有 Administrator 权限
    ```
    httpd -k start
    ```

<a id="mysql"></a>
### mysql
-   版本  mysql-5.6.38-winx64.zip
-   [下载地址](https://dev.mysql.com/downloads/file/?id=473130)
-   [安装手册](https://dev.mysql.com/doc/refman/5.6/en/windows-install-archive.html)

1.  将 zip 解压缩到所需的安装目录
2.  将 MySQL bin 目录 添加至系统环境变量(可选)

3.  必须首先安装 mysql 对应版本的 VC 库;

    vc 版本查看方法: 打开 docs\INFO_BIN 文件 查找 Visual Studio  
    ```
    // 查询到如下字样
    Visual Studio 10 2010 Win64
    ```
    根据 Visual Studio 下载对应的 Microsoft Visual C++ <2010(版本号)> Redistributable Package (x64) 包

4.  复制 my-default.ini 文件 为 my.ini 并给 my.ini 文件 最大 权限

5.  修改 my.ini 增加内容如下:
    ```
    # 配置
    # MySQL 安装目录
    basedir = C:/apmenv/mysql/mysql-5.6.38-winx64
    # MySQL data 数据存储目录
    datadir = C:/apmenv/mysql/mysql-5.6.38-winx64/data
    ```

6.  选择一个 MySQL 服务器类型: 选择 mysqld 命令 不带调试模式的服务器

7.  测试 MySQL 是否成功

    进入 bin 目录 运行命令: `mysqld --console`
    ```
    // 有如下结果,代表安装成功
    Version: '5.6.38'  socket: ''  port: 3306
    ```
``
8.  启动或停止 MySQL:

    可以进入 bin 目录 运行命令 mysqld  
    或者直接运行: "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqld"  
    停止 MySQL 命令: "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqld" -u root shutdown

    将Windows作为Windows服务启动:
    ```
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqld" --install
    ```

<a id="php"></a>
### php
-   版本 (VC14 x64 Thread Safe)
-   下载: 到 php官网 下载 (VC14 x64 Thread Safe 线程安全版本可以使用 Apache )

1.  解压 PHP 压缩文件
2.  复制 php.ini-development 为 php.ini, 并修改
    ```
    ;修改 PHP 扩展目录
    ;extension_dir = "ext"
    extension_dir = "/path/to/PHP5.6/ext"

    ;开启扩展
    ;laravel 需要开启的 php 扩展
    extension=php_openssl.dll
    extension=php_pdo_mysql.dll
    extension=php_mysqli.dll
    extension=php_mbstring.dll
    ;Tokenizer PHP Extension PHP 的 Windows 版本已内建对此扩展的支持。不需要载入额外的扩展来使用这些函数。

    ;修改默认时区
    date.timezone = PRC (可选 laravel 中有相关配置此处不需要配置)

    ;配置 PHP 的 SESSION （可选）(laravel 中有相关配置此处不需要配置)
    ;session.save_path = "/tmp"
    session.save_path = "/path/to/tmp/session"

    ;配置 PHP 上传文件的临时存放目录（可选）(laravel 中有相关配置此处不需要配置)
    ;upload_tmp_dir =
    upload_tmp_dir = "/path/to/tmp/upload"
    ```

<a id="%E5%85%B3%E8%81%94-apache-mysql-php"></a>
### 关联 Apache MySQL PHP

1.  关联 Apache 与 MySQL

    apache 安装文档 apache/readme_first.html 中说明:  
    必须把 MySQL/lib/libmysql.dll 复制到 apache/bin 目录下才能 连接 mysql

2.  关联 Apache 与 PHP 

    修改 apache/conf/http.conf 引入 PHP 处理模块
    ```
    # 引入 php7 模块
    LoadModule php7_module C:/apmenv/php/php7.1/php7apache2_4.dll
    PHPIniDir "C:/apmenv/php/php7.1"
    AddType application/x-httpd-php .php .html .htm

    #修改 Apache 默认执行的文件类型
    <IfModule dir_module>
        DirectoryIndex index.php index.html
    </IfModule>
    ```

<a id="wamp-%E7%9B%B8%E5%85%B3%E5%91%BD%E4%BB%A4"></a>
### wamp 相关命令
-   apache:
    ```
    启动:
    "C:\apmenv\apache\Apache24\bin\httpd"
    退出:
    ctrl + C
    ```


-   mysql:
    ```
    启动:
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqld"
    退出:
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqladmin" -u root shutdown

    // 进入 mysql 控制台
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysql" -u root -p

    // 查看数据库或表
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqlshow" -u root -p
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqlshow" -u root -p test

    // 执行 sql 语句
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysql" -u root -p -e "SELECT User, Host, plugin FROM mysql.user" mysql
    //eg: 创建一个 pdfindexing 数据库
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysql" -u root -e "CREATE DATABASE pdfindexing"
    ```

<a id="bat-%E8%84%9A%E6%9C%AC%E5%90%AF%E5%8A%A8%E5%92%8C%E5%85%B3%E9%97%AD-wamp"></a>
### bat 脚本启动和关闭 wamp
启动
```
@echo off
start cmd /k "echo Apache is runing... don`t close this window && apache\Apache24\bin\httpd.exe"
start cmd /k "echo mysql is runing... don`t close this window && mysql\mysql-5.6.38-winx64\bin\mysqld.exe"
```
关闭
```
@echo off
mysql\mysql-5.6.38-winx64\bin\mysqladmin.exe -u root shutdown
```

<a id="%E5%8F%82%E8%80%83%E9%93%BE%E6%8E%A5"></a>
### 参考链接
[php 环境搭建](https://segmentfault.com/a/1190000004537925)
