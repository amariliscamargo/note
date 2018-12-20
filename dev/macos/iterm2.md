---
date: '2018-12-02 19:04:53'
tags: [dev, macos]
categories: [dev, macos]
title: iTerm2
updated: '2018-12-15 18:57:40'
...
---
# iTerm2

<!-- MarkdownTOC -->

- [更改配色方法为 Solarized](#%E6%9B%B4%E6%94%B9%E9%85%8D%E8%89%B2%E6%96%B9%E6%B3%95%E4%B8%BA-solarized)
- [其他配置](#%E5%85%B6%E4%BB%96%E9%85%8D%E7%BD%AE)
- [快捷键](#%E5%BF%AB%E6%8D%B7%E9%94%AE)
- [Oh My Zsh](#oh-my-zsh)

<!-- /MarkdownTOC -->

<a id="%E6%9B%B4%E6%94%B9%E9%85%8D%E8%89%B2%E6%96%B9%E6%B3%95%E4%B8%BA-solarized"></a>
## 更改配色方法为 Solarized
iTerm2 - Preferences - Profiles - Colors 中选择 `Solarized Dark`

<a id="%E5%85%B6%E4%BB%96%E9%85%8D%E7%BD%AE"></a>
## 其他配置
-   复用上个会话的目录:  
    Preferences - Profiles - General - Working Directory - Reuse previous session’s directory

<a id="%E5%BF%AB%E6%8D%B7%E9%94%AE"></a>
## 快捷键
- ⌘ + d: 左右分屏
- ⌘⇧ + d: 上下分屏
- ⌘ + Click: 可以打开文件,文件夹和链接
- ⌘ + enter: 切换全屏

<a id="oh-my-zsh"></a>
## Oh My Zsh

[项目主页](https://github.com/robbyrussell/oh-my-zsh)

-   配置文件位置: `~/.zshrc`
-   tab 键补全
-   ctrl + n/p 选择历史命令
-   alias 别名
    ```
    alias cdhome="cd ~"
    ```
-   `alias -s` 指定特定的方式打开文件
    ```
    alias -s md=open // 表明在命令行中输入 md 后缀的文件名，会用 open 命令打开
    ```
-   设置不提示某一个 git 仓库
    ```
    # 在当前 git 根目录下运行下面的命令
    sudo git config --add oh-my-zsh.hide-status 1
    ```
