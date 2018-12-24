---
categories: [dev, developer]
date: '2018-12-20 11:34:03'
tags: [dev, developer, server]
title: 阿里云 ecs 安装 shadowsocket
titleen: Ali cloud ecs installation shadowsocket
updated: '2018-12-24 17:14:20'
...
---
# 阿里云 ecs 安装 shadowsocket
<!-- MarkdownTOC -->

- [安装 shadowsocks-libev](#%E5%AE%89%E8%A3%85-shadowsocks-libev)
- [配置](#%E9%85%8D%E7%BD%AE)
- [开放服务器端口](#%E5%BC%80%E6%94%BE%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E5%8F%A3)
- [启动](#%E5%90%AF%E5%8A%A8)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->

> 推荐使用 `shadowsocks-libev` 占用内存少

<a id="%E5%AE%89%E8%A3%85-shadowsocks-libev"></a>
## 安装 shadowsocks-libev

Ubuntu 14.04 and 16.04 users, please install from PPA:
```bash
sudo apt-get install software-properties-common -y
sudo add-apt-repository ppa:max-c-lv/shadowsocks-libev -y
sudo apt-get update
sudo apt install shadowsocks-libev
```

<a id=""></a>
<a id="%E9%85%8D%E7%BD%AE"></a>
## 配置
Configure and start the service
**注意** 服务器ip 填写 `私有ip`
```bash
// 编辑配置文件(修改配置后需 restart)
$ sudo vim /etc/shadowsocks-libev/config.json
{
    "server":"服务器ip地址", // 重点在这里: ecs 必须填写 私有网络ip (即:vpc 的ip) 或者填写 0.0.0.0
    "server_port":8989,
    "local_port":1080,
    "password":"密码",
    "timeout":60,
    "method":"aes-128-cfb"
}
```
<a id="%E5%BC%80%E6%94%BE%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E5%8F%A3"></a>
## 开放服务器端口
假如需要 开放 8989 端口:  
登录 阿里云控制台 -> 网络和安全组 -> 配置规则 -> 添加安全组规则
```
协议类型：自定义TCP
* 端口范围： 8989/8989
* 授权对象：0.0.0.0/0
```

<a id="%E5%90%AF%E5%8A%A8"></a>
## 启动
**注意:** 如果.无法启动尝试重启服务器
```bash
// sysvinit 或 systemctl 方式启动
sudo /etc/init.d/shadowsocks-libev start    # for sysvinit, or
sudo systemctl start shadowsocks-libev      # for systemd;
sudo systemctl restart shadowsocks-libev      # 重启
```

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[什么是专有网络 VPC-阿里云][] | [安全组应用案例 ECS-阿里云][]

[什么是专有网络 VPC-阿里云]:https://help.aliyun.com/document_detail/34217.html?spm=a2c4g.11174359.6.542.50324bffXFqhpX
[安全组应用案例 ECS-阿里云]:https://help.aliyun.com/document_detail/25475.html?spm=5176.2020520101.121.1.2ecc4df5wGib8m
