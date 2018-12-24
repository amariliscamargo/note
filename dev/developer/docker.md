---
categories: [dev, developer]
date: '2018-12-21 13:37:06'
tags: [docker]
title: centos7 ubuntu16 安装 docker
updated: '2018-12-21 20:42:35'
...
---
# centos7 ubuntu16 安装 docker
<!-- MarkdownTOC -->

- [centos7](#centos7)
- [ubuntu 16](#ubuntu-16)
  - [安装步骤](#%E5%AE%89%E8%A3%85%E6%AD%A5%E9%AA%A4)
  - [可选步骤](#%E5%8F%AF%E9%80%89%E6%AD%A5%E9%AA%A4)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->

> 新版本的 docker 安装可能有部分不同; 遇到问题请查看文章后的参考链接

<a id="centos7"></a>
## centos7

1.  卸载旧版本
    ```
    sudo yum update
    sudo yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-selinux docker-engine-selinux docker-engine
    ```
2.  确保安装 docker 库所依赖的包
    ```
    sudo yum install -y yum-utils \
      device-mapper-persistent-data \
      lvm2
    ```
3.  设置存储库地址, 注意替换为国内镜像
    ```
    sudo yum-config-manager \
        --add-repo \
        https://mirrors.ustc.edu.cn/docker-ce/linux/centos/docker-ce.repo

    // 官方源: https://download.docker.com/linux/centos/docker-ce.repo
    ```
4.  安装最新版本 Docker CE
    ```
    sudo yum install docker-ce
    ```
    如果提示接受 GPG 密钥，请验证指纹是否匹配 060A 61C5 1B55 8A7F 742B 77AA C52F EB6B 621E 9F35，如果匹配 ，则接受它。
5.  安装特定版本的 Docker CE
    ```
    yum list docker-ce --showduplicates | sort -r
    docker-ce.x86_64            18.03.0.ce-1.el7.centos             docker-ce-stable
    sudo yum install docker-ce-<VERSION STRING>
    ```
6.  启动 Docker
    ```
    sudo systemctl start docker
    ```
7.  通过运行 hello-world 映像验证 docker 是否已正确安装
    ```
    sudo docker run hello-world
    ```
8.  非root用户身份管理Docker
    ```
    $ sudo groupadd docker //创建docker组。
    $ sudo usermod -aG docker $USER //将您的用户添加到该docker组。
    $ docker run hello-world // 重启服务器之后,运行此命令,验证你是否可以运行 docker
    ```
9.  配置 Docker 以在启动时启动(可选)
    ```
    sudo systemctl enable docker
    ```
10. 安装 docker-compose(可选) 如果使用 laradock 则必须安装
    ```
    sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```

<a id="ubuntu-16"></a>
## ubuntu 16
<a id="%E5%AE%89%E8%A3%85%E6%AD%A5%E9%AA%A4"></a>
### 安装步骤
1.  卸载旧版本的 docker
    ```
    sudo apt-get remove docker docker-engine docker.io
    ```
2.  确保安装 docker 库所依赖的包
    ```
    sudo apt-get update
    sudo apt-get install \
        linux-image-extra-$(uname -r) \
        linux-image-extra-virtual
    ```
3.  设置存储库地址, 注意替换为国内镜像
    ```
     $ sudo apt-get update
     // 安装软件包，以允许 apt 通过 HTTPS 使用镜像仓库：
     $ sudo apt-get install \
         apt-transport-https \
         ca-certificates \
         curl \
         software-properties-common
    // 添加 Docker 的官方 GPG 密钥：
     $ curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    // 验证密钥指纹是否为 9DC8 5822 9FC7 DD38 854A E2D8 8D81 803C 0EBF CD88。
     $ sudo apt-key fingerprint 0EBFCD88
     // 使用下列命令设置 stable 镜像仓库。
    $ sudo add-apt-repository \
        "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
        $(lsb_release -cs) \
        stable"
    ```
4.  安装 Docker CE
    ```
     $ sudo apt-get update
     $ apt-cache madison docker-ce // 查看 docker-ce 所有版本
     $ sudo apt-get install docker-ce=<VERSION> // <VERSION> 在上一条命令的结果中选
    ```
5.  验证是否安装成功(Docker 守护进程将自动启动。)
    ```
    sudo docker run hello-world
    ```
    如果出现 `Hello from Docker!` 字样, 则安装成功

<a id="%E5%8F%AF%E9%80%89%E6%AD%A5%E9%AA%A4"></a>
### 可选步骤
1.  以非 root 用户身份管理 Docker
    ```
    // 创建 docker 组。
     $ sudo groupadd docker
     // 查看docker组是否存在
     $ grep docker /etc/group
    // 向 docker 组中添加您的用户。
     $ sudo usermod -aG docker $USER
     $ grep docker /etc/group // 查看 $USER 是否添加成功
    // 注销并重新登录，以便对您的组成员资格进行重新评估。
    // 验证您是否可以在不使用 sudo 的情况下运行 docker 命令。
     $ docker run hello-world
    ```
2.  将 Docker 配置为在启动时启动
    ```
    // systemd
    $ sudo systemctl enable docker
    ```
3. 安装 docker-compose(可选) 如果使用 laradock 则必须安装
    ```
    sudo curl -L https://github.com/docker/compose/releases/download/1.23.2/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```


<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[docker centos][] | [docker ubuntu][] | [docker Linux的安装后步骤][] | [docker compose][]

[docker centos]:https://docs.docker.com/install/linux/docker-ce/centos/
[docker ubuntu]:https://docs.docker-cn.com/engine/installation/linux/docker-ce/ubuntu/
[docker Linux的安装后步骤]:https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user
[docker compose]:https://github.com/docker/compose/releases
