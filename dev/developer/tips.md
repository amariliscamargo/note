---
title: 开发记录
date: 2018-11-05 22:06:06
tags: [dev, tips]
---
# 开发记录

<!-- MarkdownTOC -->

- [npm和yarn](#npm%E5%92%8Cyarn)
- [docker](#docker)
    - [dockr搭建centos7](#dockr%E6%90%AD%E5%BB%BAcentos7)
    - [laradock安装 macos](#laradock%E5%AE%89%E8%A3%85-macos)
    - [laradock安装 centos7](#laradock%E5%AE%89%E8%A3%85-centos7)
    - [laradock命令](#laradock%E5%91%BD%E4%BB%A4)
    - [laradock部署laravel centos7](#laradock%E9%83%A8%E7%BD%B2laravel-centos7)
    - [laradock中laravel项目生产环境](#laradock%E4%B8%ADlaravel%E9%A1%B9%E7%9B%AE%E7%94%9F%E4%BA%A7%E7%8E%AF%E5%A2%83)
- [git](#git)
    - [git开发流程](#git%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B)
    - [git命令](#git%E5%91%BD%E4%BB%A4)
    - [git服务器的搭建 centos7](#git%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E6%90%AD%E5%BB%BA-centos7)
- [linux](#linux)
    - [linux命令](#linux%E5%91%BD%E4%BB%A4)
    - [centos7新建用户及sudo](#centos7%E6%96%B0%E5%BB%BA%E7%94%A8%E6%88%B7%E5%8F%8Asudo)
    - [SSH通讯 centos7](#ssh%E9%80%9A%E8%AE%AF-centos7)
- [php](#php)
    - [composer](#composer)
- [laravel](#laravel)
    - [laravel目录权限设置](#laravel%E7%9B%AE%E5%BD%95%E6%9D%83%E9%99%90%E8%AE%BE%E7%BD%AE)
    - [php artisan](#php-artisan)
- [mysql](#mysql)
    - [创建数据库,用户及权限设置](#%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93%E7%94%A8%E6%88%B7%E5%8F%8A%E6%9D%83%E9%99%90%E8%AE%BE%E7%BD%AE)

<!-- /MarkdownTOC -->

<a id="npm%E5%92%8Cyarn"></a>
## npm和yarn
```
npm install lodash // 安装一个包 `npm install <package_name>`
npm install -g jshint // 全局安装 `npm install -g <package>`
npm uninstall --save lodash // 卸载包并从 package.json 中删除
npm config list -l // 查看所有配置项
npm config get registry // 查看当前 registry 的地址
npm config set registry https://registry.npm.taobao.org –global // 设置镜像地址
npm config set disturl https://npm.taobao.org/dist –global // 设置镜像地址
yarn config list // 查看所有配置项
yarn config get <key>
yarn config set <key> <value> [-g|--global]
```

<a id="docker"></a>
## docker

<a id="dockr%E6%90%AD%E5%BB%BAcentos7"></a>
### dockr搭建centos7
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
10.  安装 docker-compose(可选) 如果使用 laradock 则必须安装
    ```
    sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```
99.  参考:
    | [docker 官方教程](https://docs.docker.com/install/linux/docker-ce/centos/)
    | [docker Linux的安装后步骤](https://docs.docker.com/install/linux/linux-postinstall/#manage-docker-as-a-non-root-user)
    | [docker compose](https://github.com/docker/compose/releases)

<a id="laradock%E5%AE%89%E8%A3%85-macos"></a>
### laradock安装 macos
-   添加 docker-hub 的镜像代理地址:
    ```
    // 推荐先尝试 ustc 国内源都不是太稳定, 多试试
    // 推荐 docker 中国的官方镜像也不错
    https://registry.docker-cn.com (mac提示没有证书错误时,将https更改为 http)
    https://docker.mirrors.ustc.edu.cn/
    https://mz5qzh52.mirror.aliyuncs.com/
    docker info // 查看配置是否生效
    ```
-   下载 laradock 并选择一个最新稳定的 Releases 版本
    ```
    // 下载 laradock
    git clone https://github.com/Laradock/laradock.git
    // 选择一个稳定的发行版本,基于tag v7.8.0 创建一个新分支"version7.8.0",并且以后都是基于这个分支操作.
    git checkout -b version7.8.0 v7.8.0
    ```
-   配置 laradock .env 文件
    ```
    CHANGE_SOURCE=true    # 安装 nginx 更快
    WORKSPACE_COMPOSER_REPO_PACKAGIST=https://packagist.phpcomposer.com
    WORKSPACE_NPM_REGISTRY=https://registry.npm.taobao.org
    WORKSPACE_INSTALL_PYTHON=true    #安装 python
    WORKSPACE_TIMEZONE=PRC    #时区必须设置
    // mysql 相关配置
    MYSQL_VERSION=5.7
    MYSQL_DATABASE=hfhuishoudb
    MYSQL_USER=hfhuishoudbadmin
    MYSQL_PASSWORD=xpq1*hM6o#w7x@3wu
    MYSQL_PORT=3306
    MYSQL_ROOT_PASSWORD=root
    ```
-   更换源 workspace (./workspace/Dockerfile)
    查找`always run apt update when start`,并在此行后添加下面的代码;  
    ```
    RUN sed -i 's/archive.ubuntu.com/cn.archive.ubuntu.com/g' /etc/apt/sources.list && \
        sed -i 's/cdn-fastly.deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list && \
        sed -i 's|security.debian.org/debian-security|mirrors.ustc.edu.cn/debian-security|g' /etc/apt/sources.list && \
        sed -i 's/deb.debian.org/mirrors.ustc.edu.cn/g' /etc/apt/sources.list
    ```
    镜像替换详情查看 ustc 镜像使用帮助
-   更换源 php-fpm (./php-fpm/Dockerfile)
    步骤同上
-   第一次启动 laradock
    ```
    // 1. 第一次启动会自动构建这四个容器,php-fpm默认构建
    docker-compose up -d nginx mysql workspace
    // 2. 运行命令查看四个容器是否安装成功 如果四个 State 都为 "Up" 则代表成功
    docker-compose ps
    // 3. 如果没有安装成功,需要重新构建容器, 如果还是不行,检查 Dockerfile 文件,并添加 --no-cache 重新build
    docker-compose build {container-name} // 例如: docker-compose build workspace
    docker-compose build --no-cache {container-name}
    ```
-   参考链接:
    [laradock中文文档](https://laradock-docs.linganmin.cn/zh/getting-started/#%E5%AE%89%E8%A3%85)

<a id="laradock%E5%AE%89%E8%A3%85-centos7"></a>
### laradock安装 centos7
-   检测 docker-compose 是否安装, 如果没有安装需要安装
    ```
    docker-compose --version
    // 如果没有输出则需要运行以下命名
    sudo curl -L https://github.com/docker/compose/releases/download/1.22.0/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose
    sudo chmod +x /usr/local/bin/docker-compose
    ```
-   将repository克隆到你机器的任意位置,并选择一个最新稳定的 Releases 版本
    ```
    git clone https://github.com/laradock/laradock.git
    // 选择一个稳定的发行版本,基于tag v7.8.0 创建一个新分支"version7.8.0",并且以后都是基于这个分支操作.
    git checkout -b version7.8.0 v7.8.0
    ```
    你的文件夹结构应该如下所示
    ```
    * laradock
    * project-z
    ```
-   编辑你的 web 服务器站点配置
    ```
    cp env-example .env
    // 更改如下配置
    // 必须:
    CHANGE_SOURCE=true
    MYSQL_VERSION=5.7
    WORKSPACE_TIMEZONE=PRC
    WORKSPACE_INSTALL_PYTHON=true    #安装 python
    // 可选:
    WORKSPACE_NPM_REGISTRY=https://registry.npm.taobao.org
    WORKSPACE_COMPOSER_REPO_PACKAGIST=https://packagist.phpcomposer.com
    ```

<a id="laradock%E5%91%BD%E4%BB%A4"></a>
### laradock命令
```
docker-compose up -d nginx mysql workspace // 启动服务
docker-compose stop // 关闭所有正在运行的容器
docker-compose exec workspace bash // 进入相应服务的容器
docker-compose exec --user laradock workspace bash // 指定用户进入相应服务的容器
docker-compose restart nginx // 在更改 nginx 配置后需要重启 nginx 使配置生效
docker-compose build 容器名称例如: workspace // 重新 build 容器 (仅在更改 Dockerfile 文件后需要, 修改 .env 文件不需要)
```

<a id="laradock%E9%83%A8%E7%BD%B2laravel-centos7"></a>
### laradock部署laravel centos7
假设我们的域名为 blog.test

1.  使用 laradock 启动 nginx, mysql, php-fpm 等服务.(如果第一次启动程序会自动安装)
    ```
    cd laradock/
    docker-compose up -d nginx mysql
    ```
    大多数情况下 workspace 和 php-fpm 会自动运行, 所以不需要再up命令中指定它们
2.  进入 Workspace 容器,安装 laravel 应用 执行比如(Artisan, Composer, PHPUnit, Gulp, ...)等命令
    ```
    docker-compose exec --user=laradock workspace bash
    ```
3.  通过 composer 创建 laravel 项目
    ```
    composer create-project --prefer-dist laravel/laravel blog "5.7.*"
    // 设置项目所有者为 nginx 所属的用户, 并给 storage cache 目录分配读写权限
    // 参考 laravel目录权限设置
    ```
4.  配置 nginx 虚拟主机
    ```
    exit // 退出 workspace
    cp nginx/sites/laravel.conf.example nginx/sites/blog.conf
    vim nginx/sites/blog.conf
    // 批量替换 laravel 为 blog 也就是下面这四行
    server_name laravel.test;
    root /var/www/laravel/public;
    error_log /var/log/nginx/laravel_error.log;
    access_log /var/log/nginx/laravel_access.log;
    ```
5.  重启 nginx 服务
    ```
    docker-compose restart nginx
    ```

<a id="laradock%E4%B8%ADlaravel%E9%A1%B9%E7%9B%AE%E7%94%9F%E4%BA%A7%E7%8E%AF%E5%A2%83"></a>
### laradock中laravel项目生产环境
1.  登陆到 workspace 中, 自己的 git 服务器,需要创建 ssh 密钥, 将公钥添加自己的 git 服务器
    ```
    docker-compose exec workspace bash
    cd ~
    ssh-keygen
    ```
    将公钥(~/.ssh/id_rsa.pub)添加到 git 服务器
2.  拉代码
    ```
    git clone 用户名@ip:/项目路径.git
    ```
3.  项目权限设置并安装 laravel 依赖
    ```
    chown -R www-data:www-data 项目
    chmod -R 775 项目/storage 项目/bootstrap/cache
    cd 项目目录
    composer install --optimize-autoloader --no-dev
    composer dump-autoload --optimize
    ```
4.  清理, 重新生成 laravel 类映射加载优化
    ```
    php artisan clear-compiled
    php artisan optimize
    ```
5.  配置 laravel 环境文件(.env), 并生成应用密钥
    ```
    cp .env.example .env
    php artisan key:generate
    vim .env // 设置一些配置, mysql, 邮箱等
    ```
6.  配置 nginx 虚拟主机
    ```
    exit // 退出 workspace
    cp nginx/sites/laravel.conf.example nginx/sites/项目名称.conf
    vim nginx/sites/项目名称.conf
    // 批量替换 laravel 为 项目名称字符, servername 更改为对应的 ip 或域名
    ```
7.  重启 nginx 服务, 上线成功.
    ```
    docker-compose restart nginx
    ```
99.  参考:
    (laravel5项目部署到生产环境的最佳实践？)[https://www.zhihu.com/question/35537084/answer/63260095]

<a id="git"></a>
## git

<a id="git%E5%BC%80%E5%8F%91%E6%B5%81%E7%A8%8B"></a>
### git开发流程
为每一个模块创建一个 git 分支, 开发完毕后将分支合并到主分支上.
```
git checkout master // 切换到主分支
git checkout -b user-login // 创建一个名为 user-login 的新分支
git branch // 查看当前的分支, 然后用 checkout 命令选择一个分支进行对应的功能开发
// 功能模块开发完毕将代码纳入到 git 版本管理中
git add -A
git commit -m "Finish user login"
git merge user-login // 切换到主分支然后 合并分支
git branch -d user-login // 删除分支
```

<a id="git%E5%91%BD%E4%BB%A4"></a>
### git命令
```
// 版本回退
git reset --hard 版本号前几位数字
```

<a id="git%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%9A%84%E6%90%AD%E5%BB%BA-centos7"></a>
### git服务器的搭建 centos7
-   安装 git
    ```
    yum install git
    git --version
    ```
-   创建一个新用户, 用来运行 git
    ```
    sudo adduser mygit
    ```
-   配置 ssh 证书登陆
    将客户端(即:需要登陆到这台git服务器的电脑)的公钥写入  
    `/home/mygit/.ssh/authorized_keys` 文件中, 一行一个.  
    如果 authorized_keys 文件不存在,需要手动创建, 创建过程如下:
    ```
    // 创建文件:
    cd /home/mygit/
    mkdir .ssh
    touch .ssh/authorized_keys
    // 设置文件权限:
    chmod -R 700 .ssh/
    chmod -R 600 .ssh/authorized_keys
    // 设置文件所属用户:
    chown -R mygit:mygit .ssh
    ```
-   创建 git 仓库并初始化
    ```
    // 创建并初始化
    mkdir /mygitlib
    cd /mygitlib && git init --bare test.git
    // 更改所属用户并设置权限
    cd / && chown -R mygit:mygit mygitlib
    chmod 755 mygitlib
    ```
-   安全目的, 限制 git 账号的 ssh 连接只能是登录 git-shell, 而不是登陆 bash
    ```
    // 查找 git-shell 的目录
    which git-shell
    // 输出 /usr/bin/git-shell
    // 修改 /etc/passwd 文件
    vim /etc/passwd
    // 将 mygit 最后的 /bin/bash 更改为 git-shell 的目录
    //原始文本: mygit:x:1000:1000::/home/mygit:/bin/bash
    // 修改后
    mygit:x:1000:1000::/home/mygit:/usr/bin/git-shell
    ```
-   使用 git (本地没有项目的情况下)
    ```
    // 路径与服务器中的路径一致, 使用 gitlib 搭建可以隐藏服务器路径和设置不同用户的权限,但更耗费服务器资源
    git clone mygit@IP地址:/mygitlib/test.git
    ```
-   使用 git (本地已有项目)如果本地已经有项目,需要关联到远程仓库 参考 https://git-scm.com/book/zh/
    ```
    例如: 本地项目文件夹 testapp/
    // 在服务器上新建一个空项目并更改所属用户
    cd /mygitlib && git init --bare testapp.git
    chown -R mygit:mygit testapp.git
    // git 关联远程仓库
    git remote add origin mygit@IP:/mygitlib/testapp.git
    git remote -v (检测是否关联成功)
    origin  mygit@IP:/mygitlib/tuike.git (fetch)
    origin  mygit@IP:/mygitlib/tuike.git (push)
    // 远程分支关联
    git push --set-upstream origin master
    // 推送代码到 git 服务器
    git push
    ```

<a id="linux"></a>
## linux

<a id="linux%E5%91%BD%E4%BB%A4"></a>
### linux命令
-   find 查找文件
    ```
    find /home -name "*.txt" // 在/home目录下查找以.txt结尾的文件名 
    ```
-   ln 硬链接和软链接
    ```
    // 硬连接 将目录/home下的文件a.txt链接到目录/usr/liu下的文件a2.txt (注意,硬链接只能用于文件)
    ln /home/a.txt /usr/liu/a2.txt
    // 软链接 (可以链接目录和文件)
    ln -s /home/a.txt /usr/liu/a2.txt
    ```

<a id="centos7%E6%96%B0%E5%BB%BA%E7%94%A8%E6%88%B7%E5%8F%8Asudo"></a>
### centos7新建用户及sudo
-   创建用户及密码
    ```
    adduser -m foo
    passwd foo
    ```
-   给新建的用户增加 sudo 使用权
    ```
    whereis sudoers // sudoers: /etc/sudoers /etc/sudoers.d /usr/share/man/man5/sudoers.5.gz
    ll /etc/sudoers // 查看 sudoers 权限为 440, 需要增加写入权限, 改为 640
    chmod 640 /etc/sudoers
    vim /etc/sudoers
    // 在 root    ALL=(ALL)       ALL  后面新增 foo    ALL=(ALL)       ALL
    // 改回原来的权限
    chmod 440 /etc/sudoers
    ll /etc/sudoers
    ```
    或者直接 vim 编辑 /etc/sudoers 文件, 以 :wq! 强制写入即可. 不需要更改和改回文件权限.

<a id="ssh%E9%80%9A%E8%AE%AF-centos7"></a>
### SSH通讯 centos7
1.  首先用密码登陆到你打算使用密钥登陆的用户(假设用户名为: 小红帽), 然后创建密钥对
    ```
    yum list installed | grep openssh-server // 查看是否安装了 openssh-server, 没有则需要安装
    ssh-keygen
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
8.  ssh 其他 tips
    + ssh 超时连接中断,可以从客户端和服务器设置定时发送心跳解决, 推荐修改客户端
    ```
    subl /etc/ssh/ssh_config // 客户端
    ServerAliveInterval 60 // 每隔 60 秒向服务器发送一个空包,表示我还活着.
    ```

<a id="php"></a>
## php

<a id="composer"></a>
### composer
```
composer config -gl // 查看镜像地址等全局设置
composer config -g repo.packagist composer https://packagist.phpcomposer.com // 设置镜像地址
```

<a id="laravel"></a>
## laravel

<a id="laravel%E7%9B%AE%E5%BD%95%E6%9D%83%E9%99%90%E8%AE%BE%E7%BD%AE"></a>
### laravel目录权限设置
1.  查看 nginx(或其他 web server 例如 Apache) 使用的系统用户名称
    ```
    // 目录权限的设置,与 php-fpm, 和 php 无关
    docker-compose exec nginx bash // 如果使用 laradock的话
    find /etc -name "nginx.conf"
    cat /etc/nginx/nginx.conf // 查看 user www-data; 字样,代表nginx使用的用户为 www-data
    // 查看 www-data 用户的组
    docker-compose exec --user laradock workspace bash
    cat /etc/passwd
    // 输出 www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
    // 第二个 www-data 代表组名也是 www-data
    ```
2.  将 laravel 项目目录的所有者和组,更改为 web server 的用户名和组
    ```
    chown -R www-data:www-data /path/to/your/laravel/root/directory
    ls -al .
    // 出现如下字样代表成功
    // drwxr-xr-x 25 www-data www-data  800 Nov 23 15:51 laravel项目目录
    ```
3.  将你的用户名添加到 www-data 组中.因为你要用你的用户名来上传一些文件等操作.
    ```
    docker-compose exec workspace bash // 切换到root用户
    usermod -a -G www-data laradock // 将laradock用户添加到www-data组
    id laradock // 验证是否添加成功
    // 如下所示 groups 中包含www-data字样即代码添加成功
    // uid=1000(laradock) gid=1000(laradock) groups=1000(laradock),33(www-data),8377(docker_env)
    ```
4.  设置目录和文件的权限, 目录755,文件644, 读(4) 写(2) 执行(1)
    ```
    // 所有文件的权限时 644(即:rw-r-r)
    find ./项目目录路径 -type f -exec chmod 644 {} \;
    find ./huishou -type f -exec chmod 644 {} \;
    // 所有目录的权限时 755(即:rwx-rx-rx)
    find ./项目目录路径 -type d -exec chmod 755 {} \;
    find ./huishou -type d -exec chmod 755 {} \;
    ```

<a id="php-artisan"></a>
### php artisan

<a id="mysql"></a>
## mysql

<a id="%E5%88%9B%E5%BB%BA%E6%95%B0%E6%8D%AE%E5%BA%93%E7%94%A8%E6%88%B7%E5%8F%8A%E6%9D%83%E9%99%90%E8%AE%BE%E7%BD%AE"></a>
### 创建数据库,用户及权限设置
1.  登录 mysql
    ```
    docker-compose exec mysql bash // 进入mysql容器
    mysql -u root -p // 以root用户登录
    ```
2.  新建数据库
    ```
    // 查看数据库支持的 utf8 字符集(Charset)及字符序(collation)
    SHOW CHARACTER SET LIKE 'utf8%';
    // 一般中文项目设置字符集为 utf8mb4 字符序为 utf8mb4_general_ci
    CREATE DATABASE db_name CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
    ```
3.  新建用户及授权
    ```
    // 查看所有用户
    select User, Host from mysql.user;
    // 创建一个没有任何权限的用户 jeffrey 允许它可以从任意 ip 登录
    CREATE USER 'jeffrey'@'%' IDENTIFIED BY 'pass123';
    CREATE USER 'leadvervain'@'%' IDENTIFIED BY 'jH*C3E+@NRaLmvFA';
    SHOW PRIVILEGES; // 查看所有支持的权限及简介
    // (通常 web 项目需要的权限) ALTER: 修改表结构 CREATE: 新建数据库和表 DROP: 删除数据库和表
    GRANT SELECT, INSERT, UPDATE, DELETE, INDEX, ALTER, CREATE, DROP ON db2.* TO 'jeffrey'@'%';
    // 或者赋予 jeffrey 操作数据库 db1 中所有表的所有权限 (这样做不安全)
    GRANT ALL ON db1.* TO 'jeffrey'@'%'; 
    // 查看用户的权限
    SHOW GRANTS FOR 'jeffrey'@'localhost';
    ```
4.  修改用户权限和用户名和密码
    ```
    // 修改用户名
    RENAME USER 'jeffrey'@'localhost' TO 'jeff'@'127.0.0.1';
    // 修改密码
    SET PASSWORD FOR 'jeffrey'@'localhost' = 'new_password';
    // 撤销权限 撤销 jeffrey (ALTER CREATE DROP)三个权限
    REVOKE ALTER CREATE DROP ON db2.* FROM 'jeffrey'@'localhost';
    ```
99. 参考链接
    [字符集和字符序](https://dev.mysql.com/doc/refman/5.7/en/charset-general.html)
    [数据库设置字符集和字符序](https://dev.mysql.com/doc/refman/5.7/en/charset-database.html)
    [用户及权限](https://dev.mysql.com/doc/refman/5.7/en/account-management-sql.html)
    [用户密码](https://dev.mysql.com/doc/refman/5.7/en/set-password.html)
