---
categories: [dev, developer]
date: '2018-12-21 17:45:04'
tags: [dev, developer]
title: laradock
updated: '2018-12-21 20:27:57'
...
---
# laradock
<!-- MarkdownTOC -->

- [linux 上安装](#linux-%E4%B8%8A%E5%AE%89%E8%A3%85)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->

<a id="linux-%E4%B8%8A%E5%AE%89%E8%A3%85"></a>
## linux 上安装
1.  检测 docker-compose 是否安装, 如果没有安装需要安装; 安装参考: [docker compose][]
    ```
    docker-compose --version
    // 如果没有安装的话执行下面的步骤
    sudo curl -L https://github.com/docker/compose/releases/download/1.23.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```
2.  将 repository 克隆到你机器的任意位置,并选择一个最新稳定的 Releases 版本
    ```
    git clone https://github.com/laradock/laradock.git
    // 选择一个稳定的发行版本,基于tag v7.8.0 创建一个新分支"version7.8.0",并且以后都是基于这个分支操作.
    git tag
    git checkout -b version7.8.0 v7.8.0
    ```
    你的文件夹结构应该如下所示
    ```
    * laradock
    * project-z
    ```
3.  编辑你的 web 服务器站点配置
    ```
    cp env-example .env
    // 更改如下配置
    // 必须:
    CHANGE_SOURCE=true
    MYSQL_VERSION=5.7
    WORKSPACE_TIMEZONE=PRC
    // WORKSPACE_INSTALL_PYTHON=true    #安装 python
    // 可选:
    WORKSPACE_NPM_REGISTRY=https://registry.npm.taobao.org
    WORKSPACE_COMPOSER_REPO_PACKAGIST=https://packagist.phpcomposer.com
    ```
4. 构建容器
    ```
    // 第一次启动会自动构建这四个容器,php-fpm默认构建
    sudo docker-compose up -d nginx mysql workspace
    ```
    2018-12-21 20:27:51

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[docker compose][]

[docker compose]:https://github.com/docker/compose/releases
