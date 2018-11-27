Windows Server 2012 R2 64 位

https://segmentfault.com/a/1190000004537925
------------------------------------------------------------------------
1. apache 2.4 ( 2.4 可以与 php7(线程安全版本) 匹配)
------------------------------------------------------------------------
https://www.apachehaus.com/cgi-bin/download.plx#APACHE24VC11
注意下载 不同版本 apache 对应的 vc 库
1.1 将软件包 解压到 C:\apmenv
1.2 阅读 readme_first.html 文件并按照
- 请务必安装所需的 Visual C ++ 2012 x64 https://www.microsoft.com/en-us/download/details.aspx?id=30679
- 把 Apache24 文件夹复制到安装目录下
- 修改 C:\apmenv\Apache24\conf\httpd.conf 文件中的 ServerRoot 地址
- 测试是否安装成功: 打开 cmd , 把目录切换到 C:\apmenv\Apache24\bin, 执行 httpd.exe

安装为 windows 服务
In most cases you will want to run Apache as a Windows Service.
To do so you install Apache as a service by typing at the command prompt [1];

httpd -k install
You can then start Apache by typing

httpd -k start
Apache will then start and eventually release the command prompt window.

[1] You have to run the command prompt as Administrator in Windows Vista/7/2008/8/8.1/10/2012/

------------------------------------------------------------------------
2. mysql
------------------------------------------------------------------------
  下载地址: https://dev.mysql.com/downloads/file/?id=473130
  安装手册: https://dev.mysql.com/doc/refman/5.6/en/windows-install-archive.html

2.1 将 zip 解压缩到所需的安装目录
2.1.1 将 MySQL bin 目录 添加至系统环境变量(可选)

2.2 必须首先安装 mysql 对应版本的 VC 库;
    vc 版本查看方法: 打开 docs\INFO_BIN 文件 查找 Visual Studio
    ===== Compiler / generator used: =====
    Visual Studio 10 2010 Win64
    根据 Visual Studio 下载对应的 Microsoft Visual C++ <2010(版本号)> Redistributable Package (x64) 包

2.3 复制 my-default.ini 文件 为 my.ini
    并给 my.ini 文件 最大 权限
增加内容如下:

# 配置
# MySQL 安装目录
basedir = C:/apmenv/mysql/mysql-5.6.38-winx64
# MySQL data 数据存储目录
datadir = C:/apmenv/mysql/mysql-5.6.38-winx64/data

2.4 选择一个 MySQL 服务器类型
    选择 mysqld 命令 不带调试模式的服务器

2.5 测试 MySQL 是否成功
    进入 bin 目录 运行命令: mysqld --console
    有如下结果,代表安装成功
    Version: '5.6.38'  socket: ''  port: 3306

2.6 启动 MySQL 的方式:
    2.6.1 可以进入 bin 目录 运行命令 mysqld  或者直接运行: "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqld"
    停止 MySQL 命令: "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqld" -u root shutdown

    2.6.2 将Windows作为Windows服务启动
    "C:\apmenv\mysql\mysql-5.6.38-winx64\bin\mysqld" --install

2.6 确保默认的用户帐户

------------------------------------------------------------------------
3. php 下载 (VC14 x64 Thread Safe 线程安全版本可以使用 Apache )
------------------------------------------------------------------------
1. 解压 PHP 压缩文件


2. 复制 php.ini-development 为 php.ini

修改 PHP 扩展目录
;extension_dir = "ext"
extension_dir = "/path/to/PHP5.6/ext"

开启扩展
#laravel 需要开启的 php 扩展
extension=php_openssl.dll
extension=php_pdo_mysql.dll
extension=php_mysqli.dll
extension=php_mbstring.dll
Tokenizer PHP Extension PHP 的 Windows 版本已内建对此扩展的支持。不需要载入额外的扩展来使用这些函数。

修改默认时区
date.timezone = PRC (可选 laravel 中有相关配置此处不需要配置)

配置 PHP 的 SESSION （可选）(laravel 中有相关配置此处不需要配置)
;session.save_path = "/tmp"
session.save_path = "/path/to/tmp/session"

配置 PHP 上传文件的临时存放目录（可选）(laravel 中有相关配置此处不需要配置)
;upload_tmp_dir =
upload_tmp_dir = "/path/to/tmp/upload"


------------------------------------------------------------------------
3. 把 Apache、MySQL 以及 PHP 整合起来
------------------------------------------------------------------------
3.1 整合 Apache 与 MySQL
    apache 安装文档 apache/readme_first.html 中说明:
    必须把 MySQL/lib/libmysql.dll 复制到 apache/bin 目录下才能 连接 mysql

3.2 整合 Apache 与 PHP
修改 apache/conf/http.conf 引入 PHP 处理模块

# 引入 php7 模块
LoadModule php7_module C:/apmenv/php/php7.1/php7apache2_4.dll
PHPIniDir "C:/apmenv/php/php7.1"
AddType application/x-httpd-php .php .html .htm

#修改 Apache 默认执行的文件类型
<IfModule dir_module>
    DirectoryIndex index.php index.html
</IfModule>


------------------------------------------
命令
apache:
启动:
"C:\apmenv\apache\Apache24\bin\httpd"
退出:
ctrl + C


mysql:
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

bat 脚本快捷启动
------------------------------------------
@echo off
start cmd /k "echo Apache is runing... don`t close this window && apache\Apache24\bin\httpd.exe"
start cmd /k "echo mysql is runing... don`t close this window && mysql\mysql-5.6.38-winx64\bin\mysqld.exe"
bat 脚本快捷关闭
@echo off
mysql\mysql-5.6.38-winx64\bin\mysqladmin.exe -u root shutdown
