---
categories: [dev, developer]
date: '2018-12-21 19:29:39'
tags: [dev, developer]
title: SSH 通讯
updated: '2018-12-21 19:43:23'
...
---
# SSH 通讯
<!-- MarkdownTOC -->

- [安装](#%E5%AE%89%E8%A3%85)
- [ssh 超时连接中断](#ssh-%E8%B6%85%E6%97%B6%E8%BF%9E%E6%8E%A5%E4%B8%AD%E6%96%AD)

<!-- /MarkdownTOC -->

<a id="%E5%AE%89%E8%A3%85"></a>
## 安装
1.  首先用密码登陆到你打算使用密钥登陆的用户(假设服务器的用户名为: 小红帽), 然后创建密钥对
    ```
    ssh-keygen -t rsa -b 4096 -C "xiaohongmao@gmail.com"
    ```
    执行上面的命令后,在 ~/.ssh/ 目录下会生成小红帽的 私钥 id_rsa 和公钥 id_rsa.pub
2.  在服务器上批准使用小红帽的公钥
    ```
    cd .ssh
    touch authorized_keys
    cat id_rsa.pub >> authorized_keys
    // 确保文件权限如下
    chmod 700 ../.ssh
    chmod 600 authorized_keys
    ```
3.  设置 SSH, 打开密钥登录功能 (需要 root 权限)
    ```
    sudo vim /etc/ssh/sshd_config
    确保 PubkeyAuthentication 不为 no,
    PermitRootLogin 是否允许 root 用户登陆
    PasswordAuthentication 是否允许密码登陆, 当你完成密钥方式登陆后,再禁用密码登陆
    ```
4.  必须重启 ssh 服务,使配置生效.
    ```
    sudo service sshd restart
    ```
5.  复制或者下载小红帽的私钥到客户端, 使用它登陆服务器
    ```
    chmod 400 path/to/id_rsa
    ssh -i 小红帽的私钥路径 小红帽@服务器IP
    ```
6.  最后使用小红帽的私钥登陆服务器, 可以删除小红帽在服务器上的公钥和私钥确保安全
    ```
    sudo vim /etc/ssh/sshd_config // PasswordAuthentication yes 改为 no
    sudo service sshd restart
    rm -fr .ssh/id_rsa*
    ```
7.  最后也可以将大灰狼等管理员的公钥, 在服务器上批准使用(重复步骤2), 则可以实现大灰狼不需要小红帽的私钥,用自己的私钥登陆服务器.参考 [centos7 搭建 git 服务器](#centos7-git)
    ```
    将大灰狼的公钥复制到 服务器 ~/.ssh/authorized_keys 文件中, 一行一个.
    ssh 小红帽@服务器IP
    ```
<a id="ssh-%E8%B6%85%E6%97%B6%E8%BF%9E%E6%8E%A5%E4%B8%AD%E6%96%AD"></a>
## ssh 超时连接中断
可以从客户端和服务器设置定时发送心跳解决, 推荐修改客户端
```bash
subl /etc/ssh/ssh_config // 客户端
ServerAliveInterval 60 // 每隔 60 秒向服务器发送一个空包,表示我还活着.不要关闭链接
```
