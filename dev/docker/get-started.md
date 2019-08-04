---
categories: [dev, docker]
date: '2019-04-08 10:53:57'
tags: [dev, docker]
title: docker 入门
titleen: Getting started with docker
updated: '2019-04-09 11:17:46'
...
---
# docker 入门
<!-- MarkdownTOC -->

- [Why - 为什么用Docker](#why---%E4%B8%BA%E4%BB%80%E4%B9%88%E7%94%A8docker)
- [What - 什么是Docker](#what---%E4%BB%80%E4%B9%88%E6%98%AFdocker)
- [How - 如何使用Docker](#how---%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8docker)
    - [安装](#%E5%AE%89%E8%A3%85)
    - [image](#image)
    - [container](#container)
    - [image与container 例子](#image%E4%B8%8Econtainer-%E4%BE%8B%E5%AD%90)
    - [Dockerfile 制作image](#dockerfile-%E5%88%B6%E4%BD%9Cimage)
    - [发布 image](#%E5%8F%91%E5%B8%83-image)
    - [其他常用命令](#%E5%85%B6%E4%BB%96%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->
<a id="why---%E4%B8%BA%E4%BB%80%E4%B9%88%E7%94%A8docker"></a>
## Why - 为什么用Docker
解决环境配置问题: 只需配置一次即可运行于任何系统(类似于虚拟机,但是它启动快,资源占用少)  
Build Once, Run Anywhere

<a id="what---%E4%BB%80%E4%B9%88%E6%98%AFdocker"></a>
## What - 什么是Docker
Docker 是 Linux-container 的一种封装,提供简单易用的容器使用接口;(方便我们使用容器替代虚拟机)

<a id="how---%E5%A6%82%E4%BD%95%E4%BD%BF%E7%94%A8docker"></a>
## How - 如何使用Docker
<a id="%E5%AE%89%E8%A3%85"></a>
### 安装
Docker 是一个开源的商业产品,分为社区版(CE)和企业版(EE);
开发人员一般选择CE 参考: [安装 Docker | Docker 中文文档][]
Docker 是 `服务器-客户端` 架构; 命令行运行docker命令的时候,需要本机启动 `Docker 服务`;
对于 `类Unix` 使用 `sudo service docker start` 启动 `Docker 服务`;
对于 `MacOS,Win10` 启动`Docker软件`就行了;

<a id="image"></a>
### image
Docker 把系统,应用程序及依赖打包在 `image 文件`中,通过 `image` 来生成 `Docker 容器`;  
(image 相当于类, 容器相当于实例, 当然: 一个 image 可以生成多个 container)

相关命令:
```bash
docker images -a                           # 显示此机器上的所有镜像
docker rmi <imagename>                     # 从此机器中删除指定的镜像
docker rmi $(docker images -q)             # 从此机器中删除所有镜像
docker run [username/]repository[:tag]     # 运行镜像库中的镜像, 如何本地不存在镜像会到远程仓库自动获取
```

<a id="container"></a>
### container
image 文件生成的容器实例, 本身也是一个文件, 称为容器文件  

```bash
# 查看image列表
➜ docker images
REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
ubuntu                 16.04               9361ce633ff1        3 weeks ago         118MB
# 使用 run 命令基于 `ubuntu:16.04 image` 生成了 `容器ID为: e0b0fcdd8257` 的容器
➜ docker run -it ubuntu:16.04 /bin/bash
root@e0b0fcdd8257:/#
# 查看正在运行的容器 (e0b0fcdd8257)
➜ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
e0b0fcdd8257        ubuntu:16.04        "/bin/bash"         7 seconds ago       Up 6 seconds                            mystifying_mcnulty
# 停止容器<e0b0fcdd8257>
➜ docker stop e0b0fcdd8257
e0b0fcdd8257
# 查看所有容器包括停止运行的容器
➜ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                           PORTS               NAMES
e0b0fcdd8257        ubuntu:16.04        "/bin/bash"         46 seconds ago      Exited (0) 13 seconds ago                            mystifying_mcnulty
# 基于 `镜像 ubuntu:16.04` 再次创建一个容器, 注意:ID是不同的
➜ docker run -it ubuntu:16.04 /bin/bash
root@0771c36d53fc:/#
# 容器0771c36d53fc 正在运行
➜ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
0771c36d53fc        ubuntu:16.04        "/bin/bash"         3 minutes ago       Up 3 minutes                            gracious_shannon
# 查看所有容器,注意 STATUS 不同, e0b0fcdd8257的状态为 Exited(没有在运行)
➜ docker ps -a
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                           PORTS               NAMES
0771c36d53fc        ubuntu:16.04        "/bin/bash"         3 minutes ago       Up 3 minutes                                         gracious_shannon
e0b0fcdd8257        ubuntu:16.04        "/bin/bash"         4 minutes ago       Exited (0) 4 minutes ago                             mystifying_mcnulty
# start 命令,重新运行容器;
➜ docker container start e0b0fcdd8257
e0b0fcdd8257
# 两个容器现在都运行了
➜ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
0771c36d53fc        ubuntu:16.04        "/bin/bash"         5 minutes ago       Up 5 minutes                            gracious_shannon
e0b0fcdd8257        ubuntu:16.04        "/bin/bash"         5 minutes ago       Up 4 seconds                            mystifying_mcnulty
```

相关命令:
```bash
docker ps                           # 查看所有正在运行的容器的列表 等价于 (docker container ls)
docker ps -a                        # 查看所有容器的列表，甚至包含未运行的容器
docker container ls                 # 等价于 docker ps
docker run [参数] <imagename> [CMD] # 基于镜像运行并创建一个容器
docker container start <hash>       # 启动容器
docker stop <hash>                  # 平稳地停止指定的容器
docker kill <hash>                  # 强制关闭指定的容器
docker rm <hash>                    # 删除指定的容器
docker container prune              # 删除所有处于终止状态的容器
docker rm $(docker ps -a -q)        # 删除所有容器
```

<a id="image%E4%B8%8Econtainer-%E4%BE%8B%E5%AD%90"></a>
### image与container 例子
参考: [启动 · Docker —— 从入门到实践][]
1.  从 [DockerHub][] 拉取 `image`
    ```bash
    docker --version                        # 查看docker版本
    docker login                            # 注意: 用户名是 DockerHub 上的"用户名而不是邮箱",如果没有去注册一个
    docker pull ubuntu:16.04                # 拉取16.04 版本的
    docker images -a                        # 查看image是否拉取成功
    ```
2.  运行 `image` (通过 `image` 生成 `container`)
    ```bash
    docker run -it ubuntu:16.04 /bin/bash # 通过image生成container并运行(一个 bash 终端允许用户进行交互)
    docker ps                               # 查看运行image 后生成的 container
    docker stop <hash>                      # 结束 container
    ```

<a id="dockerfile-%E5%88%B6%E4%BD%9Cimage"></a>
### Dockerfile 制作image
会使用image后,下面就是如何制作自己的image;  
很简单,通过一个文本文件(Dockerfile)来告诉 Docker 如何配置 image;它会根据你的指令生成二进制的image文件.  
例子:
1.  编写`.dockerignore` 文件
    `.dockerignore` 文件,表示排除路径,不需要打包到 image 文件中
    ```
    .git
    node_modules
    npm-debug.log
    ```
2.  编写 `Dockerfile`
    Dockerfile文件,用来配置image
    ```bash
    FROM node:10.15.3                                          # 这个 image 需要继承自 https://hub.docker.com/_/node 版本是10.15.3
    WORKDIR /app                                               # 将工作目录设置为 /app
    ADD . /app                                                 # 将当前目录下的所有文件(除了.dockerignore排除的路径)都拷贝进入 image文件 的 /app 目录
    RUN npm install --registry=https://registry.npm.taobao.org # 在/app目录下, 运行npm install命令安装依赖(注意安装后所有的依赖,都将打包进入 image 文件)
    EXPOSE 3000                                                # 将容器 3000 (注意:这个端口是你在koa.js中设置的)端口暴露出来,允许外部连接这个端口
    CMD ["node", "koa.js"]                                     # 在容器启动时运行 koa.js
    ```
3.  建构 image
    ```
    docker build -t koa-demo:v1 . # -t参数用来指定 image 文件的名字和标签
    docker images                 # 查看 image 是否创建成功
    ```
4.  运行 image 生成 container
    ```
    docker run -p 8080:3000 koa-demo:v1    # 使用 -p 参数将`本机的8080端口`映射到`容器暴露的3000`端口
    # 或者
    docker run -d -p 8080:3000 koa-demo:v1 # 后台运行,不用一直开着命令行窗口
    ```
    访问: http://localhost:8080  
5.  结束运行 和 删除容器文件
    ```
    docker stop <容器id>   # 结束运行,但是容器文件还在
    docker ps -a           # 查看所有容器,包含已经关闭的
    docker rm <hash>       # 删除指定容器
    docker container prune # 清理所有处于终止状态的容器
    ```
6.  可以覆盖 `Dockerfile 中的 CMD`
    ```
    docker run -it -p 8080:3000 koa-demo:v1 /bin/bash
    ```
<a id="%E5%8F%91%E5%B8%83-image"></a>
### 发布 image
发布到镜像库,方便从任何设备下载使用镜像.首先需要[注册账户](hub.docker.com)
```
docker login                                          # 登录
docker image build -t [username]/[repository]:[tag] . # 建构并标注tag
docker image build -t linkhanfeng/koa-demo:0.0.1 .
docker image push linkhanfeng/koa-demo:0.0.1          # 发布, 前往 hub.docker.com 查看自己的镜像
docker push linkhanfeng/koa-demo:tagname              # 在任何设备上拉取自己的镜像
```

<a id="%E5%85%B6%E4%BB%96%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4"></a>
### 其他常用命令
```bash
# -i -t 参数, -i shell 标准输出, -t 伪终端; 有些命令,没有 -t
# --help 参数, 可以查看命令用法
# 设置加速镜像提示证书问题: macos 设置->通用->securely store Docker logins in macOs keychain 去掉勾选
docker container start <hash> # 启动容器,而像 run 命令那样新建一个容器
docker container logs <hash> # 可以查看容器中 shell 的标注输出
docker container exec -it <hash> /bin/bash # 进入一个正在运行的容器
docker container cp <hash>:[/path/to/file] . # 从正在运行的容器里拷贝容器中的文件到本机
```

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[Docker入门教程][] | [安装 Docker | Docker 中文文档][] | [DockerHub][] | [前言 · Docker —— 从入门到实践][] | [启动 · Docker —— 从入门到实践][] | [Can not use registry mirror · Issue #2146 · docker/for-mac][]

[Docker入门教程]:http://www.ruanyifeng.com/blog/2018/02/docker-tutorial.html
[安装 Docker | Docker 中文文档]:https://docs.docker-cn.com/engine/installation/
[DockerHub]:https://hub.docker.com/_/hello-world?tab=tags
[前言 · Docker —— 从入门到实践]:https://yeasy.gitbooks.io/docker_practice/content/
[启动 · Docker —— 从入门到实践]:https://yeasy.gitbooks.io/docker_practice/container/run.html
[Can not use registry mirror · Issue #2146 · docker/for-mac]:https://github.com/docker/for-mac/issues/2146
