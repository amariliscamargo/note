---
date: '2018-12-15 20:06:13'
tags: [dev, developer]
categories: [dev, developer]
title: 阿里云-云服务器 (ECS) docker+laradock+git
updated: '2018-12-16 20:23:54'
...
---
# 阿里云-云服务器 (ECS) docker+laradock+git
<!-- MarkdownTOC -->

- [云服务器是什么](#%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%98%AF%E4%BB%80%E4%B9%88)
- [SSH 密钥对](#ssh-%E5%AF%86%E9%92%A5%E5%AF%B9)
- [系统安装](#%E7%B3%BB%E7%BB%9F%E5%AE%89%E8%A3%85)
    - [更换操作系统](#%E6%9B%B4%E6%8D%A2%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F)
    - [重装系统\(初始化系统\)](#%E9%87%8D%E8%A3%85%E7%B3%BB%E7%BB%9F%E5%88%9D%E5%A7%8B%E5%8C%96%E7%B3%BB%E7%BB%9F)
- [使用密钥登录服务器](#%E4%BD%BF%E7%94%A8%E5%AF%86%E9%92%A5%E7%99%BB%E5%BD%95%E6%9C%8D%E5%8A%A1%E5%99%A8)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->
<a id="%E4%BA%91%E6%9C%8D%E5%8A%A1%E5%99%A8%E6%98%AF%E4%BB%80%E4%B9%88"></a>
## 云服务器是什么
参考上一篇博文 [腾讯云的使用](./tengxunyun.md)

阿里云中的术语:
-   `地域和可用区`: 指服务器的地理位置
-   `实例`: 等同于一台虚拟机(包括cpu,内存,操作系统等)
-   `实例规格`: 虚拟机的配置(如cpu核数,内存大小)
-   `镜像`: 虚拟机的操作系统(如windows,linux)
-   `块存储`：基于分布式的`云盘`, `共享盘` 和 基于物理机本地硬盘的 `本地存储`
-   `安全组`：一种虚拟防火墙，用于设置实例的网络访问控制。
参考:[阿里云产品介绍][ECS]:

<a id="ssh-%E5%AF%86%E9%92%A5%E5%AF%B9"></a>
## SSH 密钥对
> 控制台->ECS->网络和安全->密钥对->创建密钥对

创建完成需要从浏览器下载到本地保存起来,以后使用此密钥登录服务器

参考: [ssh 方式登录的优势][ssh] | [创建SSH密钥对][]
<a id="%E7%B3%BB%E7%BB%9F%E5%AE%89%E8%A3%85"></a>
## 系统安装

<a id="%E6%9B%B4%E6%8D%A2%E6%93%8D%E4%BD%9C%E7%B3%BB%E7%BB%9F"></a>
### 更换操作系统
> 控制台->ECS->选择一个实例->右侧更多->磁盘和镜像->更换系统盘

1.  公共镜像：Ubuntu 16.04 64 位(或者其他)
2.  密钥对: 选择刚才创建的密钥对

参考: [更换系统盘][更换系统盘]
<a id="%E9%87%8D%E8%A3%85%E7%B3%BB%E7%BB%9F%E5%88%9D%E5%A7%8B%E5%8C%96%E7%B3%BB%E7%BB%9F"></a>
### 重装系统(初始化系统)
> 控制台->ECS->选择一个实例->右侧更多->磁盘和镜像->初始化磁盘

安全设置选择密钥登录,然后选择刚才创建的密钥对

<a id="%E4%BD%BF%E7%94%A8%E5%AF%86%E9%92%A5%E7%99%BB%E5%BD%95%E6%9C%8D%E5%8A%A1%E5%99%A8"></a>
## 使用密钥登录服务器
1.  找到你在 `创建 SSH 密钥对` 时下载.pem私钥文件
2.  运行命令修改私钥文件权限
    ```bash
    chmod 400 /path/to/密钥
    ```
3.  运行命令连接至服务器
    ```bash
    ssh -i /path/to/密钥 root@公网IP地址
    ```
参考: [ssh 方式登录的优势][ssh] | [使用SSH密钥对连接Linux实例][]
<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[ECS][] | [ssh][] | [创建SSH密钥对][] | [更换系统盘][]

[ECS]:https://help.aliyun.com/document_detail/25367.html?spm=5176.8789780.1092592.1.185557a80v0qSE
[ssh]:https://help.aliyun.com/document_detail/51792.html?spm=5176.11065259.1996646101.searchclickresult.2c11367f5M02q4
[创建SSH密钥对]:https://help.aliyun.com/document_detail/51793.html?spm=a2c4g.11186623.2.15.264dcc5awJLNzC#concept_wy4_th1_ydb
[更换系统盘]:https://help.aliyun.com/document_detail/50134.html?spm=a2c4g.11186623.2.25.2dab55fdejwX7j#concept-n4k-x3j-ydb
[使用SSH密钥对连接Linux实例]https://help.aliyun.com/document_detail/51798.html?spm=a2c4g.11186623.2.20.264dcc5awJLNzC#concept_ucj_wrx_wdb
