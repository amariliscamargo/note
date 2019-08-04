---
categories: [dev, docker]
date: '2019-04-09 10:34:28'
tags: [dev, docker]
title: Docker 搭建 wordpress
titleen: Docker builds wordpress
updated: '2019-04-09 12:44:14'
...
---
# Docker 搭建 wordpress
<!-- MarkdownTOC -->

- [第二种方法: 使用 Wordpress 官方镜像](#%E7%AC%AC%E4%BA%8C%E7%A7%8D%E6%96%B9%E6%B3%95-%E4%BD%BF%E7%94%A8-wordpress-%E5%AE%98%E6%96%B9%E9%95%9C%E5%83%8F)
- [方法3 使用 Docker Compose 工具](#%E6%96%B9%E6%B3%953-%E4%BD%BF%E7%94%A8-docker-compose-%E5%B7%A5%E5%85%B7)

<!-- /MarkdownTOC -->

1.  安装 php-apache
    ```bash
    docker container run \
    --rm \
    -p 80:80 \
    --name wordpress \
    --volume "$PWD/":/var/www/html \
    php:7.3-apache
    ```
    访问 localhost:80
2.  下载 wordpress
    ```
    curl -O https://cn.wordpress.org/wordpress-5.0-zh_CN.tar.gz
    tar -xvf wordpress-5.0-zh_CN.tar.gz
    ```
3.  安装mysql
    ```
    docker container run \
    -d \
    --rm \
    --name wordpressdb \
    --env MYSQL_ROOT_PASSWORD=123456 \
    --env MYSQL_DATABASE=wordpress \
    mysql:5.7

    docker container logs wordpressdb # 查看wordpressdb容器中的shell输出,查找问题
    ```
4.  定制 `php:7.3-apache` 容器
    php 官方 image, 不带有 mysql 扩展, 必须自己基于它,添加 mysqli 扩展
    ```
    # 停止 wordpress 容器
     docker container stop wordpress
    # Dockerfile 文件
    FROM php:7.3-apache
    RUN docker-php-ext-install mysqli
    CMD apache2-foreground
    # 基于上面的 Dockerfile 文件新建镜像
    docker build -t phpwithmysql .
    # 基于新建的 `phpwithmysql image` 新建一个 wordpress 容器
    docker container run \
    --rm \
    -p 80:80 \
    --name wordpress \
    --volume "$PWD/":/var/www/html \
    --link wordpressdb:mysql \
    phpwithmysql

    # 注意: 此处的别名需要在wordpress容器链接wordpressdb容器时用到

    # 更改 wordpress 目录的权限,让容器可以将配置信息写入到目录
    chmod -R 777 wordpress
    ```


<a id="%E7%AC%AC%E4%BA%8C%E7%A7%8D%E6%96%B9%E6%B3%95-%E4%BD%BF%E7%94%A8-wordpress-%E5%AE%98%E6%96%B9%E9%95%9C%E5%83%8F"></a>
## 第二种方法: 使用 Wordpress 官方镜像
1.  新建mysql
    ```
    docker container run \
        -d \
        --rm \
        --name wordpressdb \
        --env MYSQL_ROOT_PASSWORD=123456 \
        --env MYSQL_DATABASE=wordpress \
        mysql:5.7
    ```
2.  基于官方 `wordpress:5.1-php7.1-apache image`, 新建并启动 wordpress 容器
    ```
    docker container run \
        -p 127.0.0.1:8080:80 \
        -d \
        --rm \
        --name wordpress \
        --env WORDPRESS_DB_PASSWORD=123456 \
        --link wordpressdb:mysql \
        --volume "$PWD/wordpress":/var/www/html \
        wordpress:5.1-php7.1-apache

    # --volume "$PWD/wordpress":/var/www/html \ 会自动把 对应的目录文件复制到本机
    docker container exec -it wordpress /bin/bash # 进入正在运行的 `wordpress容器` 查看文件目录
    exit # 退出登录容器
    # docker container cp wordpress:/var/www/html ./wordpress # 从 `wordpress容器` 中复制内容到本机目录
    ```

<a id="%E6%96%B9%E6%B3%953-%E4%BD%BF%E7%94%A8-docker-compose-%E5%B7%A5%E5%85%B7"></a>
## 方法3 使用 Docker Compose 工具
