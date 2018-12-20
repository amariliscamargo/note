---
date: '2018-12-16 21:36:41'
tags: [dev, linux, lpic-1, filesystems]
categories: [dev, linux, lpic-1, filesystems]
title: 管理文件权限和所有权
updated: '2018-12-18 15:41:34'
...
---
# 管理文件权限和所有权
<!-- MarkdownTOC -->

- [概述](#%E6%A6%82%E8%BF%B0)
    - [学习目标](#%E5%AD%A6%E4%B9%A0%E7%9B%AE%E6%A0%87)
    - [先决条件](#%E5%85%88%E5%86%B3%E6%9D%A1%E4%BB%B6)
    - [术语](#%E6%9C%AF%E8%AF%AD)
- [用户和组](#%E7%94%A8%E6%88%B7%E5%92%8C%E7%BB%84)
    - [我是谁?](#%E6%88%91%E6%98%AF%E8%B0%81)
    - [我在哪个组中?](#%E6%88%91%E5%9C%A8%E5%93%AA%E4%B8%AA%E7%BB%84%E4%B8%AD)
- [文件的所有权和权限](#%E6%96%87%E4%BB%B6%E7%9A%84%E6%89%80%E6%9C%89%E6%9D%83%E5%92%8C%E6%9D%83%E9%99%90)
    - [`ls -l` 打印的各项参数](#ls--l-%E6%89%93%E5%8D%B0%E7%9A%84%E5%90%84%E9%A1%B9%E5%8F%82%E6%95%B0)
    - [普通文件](#%E6%99%AE%E9%80%9A%E6%96%87%E4%BB%B6)
    - [目录](#%E7%9B%AE%E5%BD%95)
    - [其他文件类型](#%E5%85%B6%E4%BB%96%E6%96%87%E4%BB%B6%E7%B1%BB%E5%9E%8B)
- [变更权限](#%E5%8F%98%E6%9B%B4%E6%9D%83%E9%99%90)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->
[回到目录](../index.md)

<a id="%E6%A6%82%E8%BF%B0"></a>
## 概述

<a id="%E5%AD%A6%E4%B9%A0%E7%9B%AE%E6%A0%87"></a>
### 学习目标
> Manage file permissions and ownership  
> 设置 文件或目录 的 `权限`和 `所有权` 达到控制文件访问的目的

-   管理普通和特殊文件及目录的访问权限
-   使用访问模式，如 suid、sgid 和粘贴位（sticky bit），维护安全性
-   变更文件创建屏蔽
-   向组成员授予访问权限
<a id="%E5%85%88%E5%86%B3%E6%9D%A1%E4%BB%B6"></a>
### 先决条件
-   具有基本的 Linux 知识, 且准备一个 Linux 系统
-   本文基于 `Fedora 13`, 不同版本的程序输出格式不同

<a id="%E6%9C%AF%E8%AF%AD"></a>
### 术语
-   权限: permissions
-   所有权: ownership

<a id="%E7%94%A8%E6%88%B7%E5%92%8C%E7%BB%84"></a>
## 用户和组
现在,您了解了 Linux 是一个多用户的系统,每个用户属于一个主要组,也可能是附加组.  
也可以作为一个用户登录,然后使用 su 或者 sudo -s 命令变为另一个用户.  
Linux 的文件所有权和访问授权是与用户 id 和组密切相关的,所以我们要复习一下基本的用户和组信息.

<a id="%E6%88%91%E6%98%AF%E8%B0%81"></a>
### 我是谁?
使用 `whoami` 命令来查看当前用户id
```bash
$ whoami
lardock
```
<a id="%E6%88%91%E5%9C%A8%E5%93%AA%E4%B8%AA%E7%BB%84%E4%B8%AD"></a>
### 我在哪个组中?
使用 `id` 命令,可以找出用户和组信息
使用 `groups` 命令,可以找到你的组信息
```bash
$ id
uid=1000(laradock) gid=1000(laradock) groups=1000(laradock),8377(docker_env)
$ id laradock
uid=1000(laradock) gid=1000(laradock) groups=1000(laradock),8377(docker_env)
$ groups
laradock docker_env
$ groups laradock
laradock : laradock docker_env
```

<a id="%E6%96%87%E4%BB%B6%E7%9A%84%E6%89%80%E6%9C%89%E6%9D%83%E5%92%8C%E6%9D%83%E9%99%90"></a>
## 文件的所有权和权限
如果每个用户都有 id 并且是主要组的成员  
那么 Linux 系统上的每个文件都有一个所有者和与其相关的组。

<a id="ls--l-%E6%89%93%E5%8D%B0%E7%9A%84%E5%90%84%E9%A1%B9%E5%8F%82%E6%95%B0"></a>
### `ls -l` 打印的各项参数
```
$ ls -l ~/.bashrc
-rw-r--r--. 1 ian  ian            124 Mar 31  2010 .bashrc
```

| 文件类型 | 权限      | 其他访问方法? | 文件的链接数<br>或目录的一级子目录数 | 用户名 | 组名 | 文件大小 | 最后修改时间 | 文件名  |
| :-       | :-        | :-           | :-                               | :-     | :-   | :-       | :-           | :-      |
| -        | rw-r--r-- | .            | 1                                | ian    | ian  | 124      | Mar 31 2010  | .bashrc |

<a id="%E6%99%AE%E9%80%9A%E6%96%87%E4%BB%B6"></a>
### 普通文件
```bash
$ ls -l /bin/bash ~/.bashrc helloworld.C 
-rw-r--r--. 1 ian  ian            124 Mar 31  2010 .bashrc
-rwxr-xr-x. 1 root root        943360 May 21  2010 /bin/bash
-rw-rw-r--. 1 ian  development    116 Nov 30 10:21 helloworld.C
```

在这个例子中:  
使用 `ls -l` 命令可以查看文件的权限和所有者信息  
用户 ian 的 .bashrc 文件由他自己所有并且属于 ian 的主要组。  
类似的，/bin/bash 由用户 root 所有，并且位于组 root。  
但是，helloworld.C 由用户 ian 所有，但是属于组 development。用户名和组名来自不同的名称空间.
事实上，很多版本默认为每个新用户创建一个匹配的(相同名称)组。

Linux 权限模型,每个文件系统对象有 3 种类型 `读（r），写（w）和执行（x）`  
写权限包括修改和删除对象的能力。  
权限的 9 个字母, 每三个字母为一组; 分别是 `文件所有者、文件组成员、其他人`

<a id="%E7%9B%AE%E5%BD%95"></a>
### 目录
目录的 `读权限` 允许`列出`该目录内容(子目录和文件)  
目录的 `写权限` 允许在目录中`创建或者删除`文件  
目录的 `执行权限` 允许用户输入目录并访问任意子目录  

```bash
[ian]$ ls -l /home
drwxr-x---.  4 greg     development  4096 Nov 30 12:44 greg
d-wx--x--x. 21 tom      tom          4096 Nov 30 11:30 tom
[ian]$ ls -a greg/.ba* # 用户 ian 有目录greg 的读权限,所以可以列出目录内容
/home/greg/.bash_history  /home/greg/.bash_profile
[ian]$ ls -a tom # 用户 ian 没有目录tom 的读权限,所以报错
ls: cannot open directory /home/tom: Permission denied
[ian]$ head -n 3 tom/.bashrc # 用户 ian 没有目录tom 的读权限, 但是有执行权限,所以可以直接输入文件路径进行访问
# .bashrc
# 这里列出了 tom/.bashrc 文件的前 3 行内容
# Source global definitions
```
参考: [head 命令][head]

<a id="%E5%85%B6%E4%BB%96%E6%96%87%E4%BB%B6%E7%B1%BB%E5%9E%8B"></a>
### 其他文件类型
`ls -l` 的输出可能包含`文件系统对象`，而不是文件和目录(即: 文件类型不同)  
下面列出了常见的对象类型  

| 类型代码 | 类型名称     |
| :-       | :-           |
| -        | 普通文件     |
| d        | 目录         |
| l        | 符号链接     |
| c        | 字符特殊设备 |
| b        | 模块特殊设备 |
| p        | FIFO         |
| s        | 套接字       |

<a id="%E5%8F%98%E6%9B%B4%E6%9D%83%E9%99%90"></a>
## 变更权限
假设您创建一个 “Hello world” 的 shell 脚本。  
当您第一次创建脚本时，它通常是不可执行的。  
使用 `chmod` 命令和 `+x` 选项, 来`添加执行权限`; 如下所示:
```bash
$ echo 'echo "Hello world!"'>hello.sh
$ ls -l hello.sh
-rw-rw-r--. 1 ian ian 20 Nov 30 13:05 hello.sh
$ ./hello.sh
bash: ./hello.sh: Permission denied
$ chmod +x hello.sh
$ ./hello.sh
Hello world!
$ ls -l hello.sh
-rwxrwxr-x. 1 ian ian 20 Nov 30 13:05 hello.sh
```

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[ibm][] | [head][]

[ibm]:https://www.ibm.com/developerworks/cn/linux/l-lpic1-v3-104-5/
[head]:http://man.linuxde.net/head
