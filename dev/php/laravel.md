---
categories: [dev, php]
date: '2018-11-08 22:06:06'
tags: [dev, php, laravel, laradock, env, 草稿]
title: laravel5.* 基于 laradock 项目流程
updated: '2018-12-25 09:57:41'
...
---
# laravel5.* 基于 laradock 项目流程

<!-- MarkdownTOC -->

- [此文未完成](#%E6%AD%A4%E6%96%87%E6%9C%AA%E5%AE%8C%E6%88%90)
    - [说明](#%E8%AF%B4%E6%98%8E)
    - [安装](#%E5%AE%89%E8%A3%85)

<!-- /MarkdownTOC -->

<a id="%E6%AD%A4%E6%96%87%E6%9C%AA%E5%AE%8C%E6%88%90"></a>
## 此文未完成

<a id="%E8%AF%B4%E6%98%8E"></a>
### 说明
`$` 为真实环境  
`^` 为 docker 环境  
假设项目名称为 `blog`

<a id="%E5%AE%89%E8%A3%85"></a>
### 安装
1. 设置 composer 镜像
```
$ cd laradock
$ docker-compose up -d nginx mysql
$ docker-compose exec workspace bash
^ composer config -g repo.packagist composer https://packagist.laravel-china.org // 设置镜像地址
^ composer config -gl // 查看镜像地址是否设置成功
^ composer config -g --unset repos.packagist // 取消镜像
```
2. 通过 Composer 创建项目, 并更改项目所有者为 nginx
```
^ su laradock
^ composer create-project --prefer-dist laravel/laravel blog "5.6.*"
^ chown -R www-data:www-data blog
^ chmod -R 775 blog/storage blog/bootstrap/cache
```

3. 配置 nginx
```
$ cd laradock
$ cp nginx/sites/laravel.conf.example blog.conf
// 批量替换 laravel 为 blog
```

4. 配置 mysql
```
```
