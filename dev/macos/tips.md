---
categories: [dev, macos]
date: '2018-11-02 18:58:28'
tags: [dev, macos]
title: macos小技巧
updated: '2019-02-19 11:24:29'
...
---
# macos小技巧

<!-- MarkdownTOC -->

- [软件:](#%E8%BD%AF%E4%BB%B6)
    - [校验软件签名](#%E6%A0%A1%E9%AA%8C%E8%BD%AF%E4%BB%B6%E7%AD%BE%E5%90%8D)
    - [软件安装](#%E8%BD%AF%E4%BB%B6%E5%AE%89%E8%A3%85)
    - [不更改系统语言的情况下,更改软件语言](#%E4%B8%8D%E6%9B%B4%E6%94%B9%E7%B3%BB%E7%BB%9F%E8%AF%AD%E8%A8%80%E7%9A%84%E6%83%85%E5%86%B5%E4%B8%8B%E6%9B%B4%E6%94%B9%E8%BD%AF%E4%BB%B6%E8%AF%AD%E8%A8%80)
    - [Finder 等软件不在 launchpad 中显示](#finder-%E7%AD%89%E8%BD%AF%E4%BB%B6%E4%B8%8D%E5%9C%A8-launchpad-%E4%B8%AD%E6%98%BE%E7%A4%BA)
    - [Spotlight 无法关闭 Developer Results](#spotlight-%E6%97%A0%E6%B3%95%E5%85%B3%E9%97%AD-developer-results)
- [输入法和字体](#%E8%BE%93%E5%85%A5%E6%B3%95%E5%92%8C%E5%AD%97%E4%BD%93)
- [其他](#%E5%85%B6%E4%BB%96)
    - [终端显示 bogon](#%E7%BB%88%E7%AB%AF%E6%98%BE%E7%A4%BA-bogon)
    - [打开全键盘控制](#%E6%89%93%E5%BC%80%E5%85%A8%E9%94%AE%E7%9B%98%E6%8E%A7%E5%88%B6)
    - [语音](#%E8%AF%AD%E9%9F%B3)
    - [切换 root 用户](#%E5%88%87%E6%8D%A2-root-%E7%94%A8%E6%88%B7)
    - [如果 电池未充电](#%E5%A6%82%E6%9E%9C-%E7%94%B5%E6%B1%A0%E6%9C%AA%E5%85%85%E7%94%B5)

<!-- /MarkdownTOC -->

<a id="%E8%BD%AF%E4%BB%B6"></a>
## 软件:
<a id="%E6%A0%A1%E9%AA%8C%E8%BD%AF%E4%BB%B6%E7%AD%BE%E5%90%8D"></a>
### 校验软件签名
    ```
    验证SHA-256
    openssl dgst -sha256 /path/to/file
    验证SHA-1
    openssl sha1 /path/to/file
    验证 MD5
    openssl md5 /path/to/file
    ```
<a id="%E8%BD%AF%E4%BB%B6%E5%AE%89%E8%A3%85"></a>
### 软件安装
    ```
      到 app store 中直接安装
      xxx.app 直接移动到 /Applications 即可;
      xxx.dmg 双击后解压出 xxx.app, 执行上一步操作
    ```
<a id="%E4%B8%8D%E6%9B%B4%E6%94%B9%E7%B3%BB%E7%BB%9F%E8%AF%AD%E8%A8%80%E7%9A%84%E6%83%85%E5%86%B5%E4%B8%8B%E6%9B%B4%E6%94%B9%E8%BD%AF%E4%BB%B6%E8%AF%AD%E8%A8%80"></a>
### 不更改系统语言的情况下,更改软件语言
    ```
    情况1: 使用 defaults 命令书
    例如: 更改 “Mac 帮助” 为中文优先,英文次之
      defaults domains (列出所有软件的标识符,用来查看 “Mac 帮助” 的软件名称)
      defaults write com.apple.help AppleLanguages "(zh-CN,en-US)"
      defaults write com.apple.helpviewer AppleLanguages "(zh-CN,en-US)"      defaults write com.google.Chrome AppleLanguages "(zh-CN,en-US)" // 更改 chrome
    情况2: 对于 photoshop 等比较大的垃圾软件. 需要在网上下载语言包,然后替换到相应的目录.
    ```
<a id="finder-%E7%AD%89%E8%BD%AF%E4%BB%B6%E4%B8%8D%E5%9C%A8-launchpad-%E4%B8%AD%E6%98%BE%E7%A4%BA"></a>
### Finder 等软件不在 launchpad 中显示
    ```
    创建这个程序的软连接到 /Application 目录下即可
    例如:
    ln -s /System/Library/CoreServices/Finder.app /Applications/Finder.app
    ```

<a id="spotlight-%E6%97%A0%E6%B3%95%E5%85%B3%E9%97%AD-developer-results"></a>
### Spotlight 无法关闭 Developer Results
    ```
      3.1 cd /Applications
      3.2 touch Xcode.app
      3.3 到 Spotlight 的设置中将 Developer 的对勾去掉
    ```

<a id="%E8%BE%93%E5%85%A5%E6%B3%95%E5%92%8C%E5%AD%97%E4%BD%93"></a>
## 输入法和字体
-   中英文严格1:2等宽字体 M+ [网址](http://mplus-fonts.osdn.jp/about.html)
-   输入法: 唯一选择 rime
    1.  可以使用 shift 键切换输入法
    2.  可以根据不同的 应用设置默认的输入模式 修改 squirrel.yaml
        ```
        com.sublimetext.3:
          ascii_mode: true
        ```
    3.  可以配置中文下使用英文标点,使用中括号切换候选页
        修改 ~/Library/Rime/defalut.yaml
        ```yaml
        标点符合更改一下例如: '\' : [ 、, ＼ ] 改为: '\' : {commit: '\'}
        { when: has_menu, accept: bracketleft, send: Page_Up }
        { when: has_menu, accept: bracketright, send: Page_Down }
        从中文切换到英文输入法时,将英文字母自动上屏
        Shift_L: commit_code
        Shift_R: commit_code
        ascii_composer:
          good_old_caps_lock: true
          switch_key:
            Shift_L: commit_code
            Shift_R: commit_code
            Control_L: noop
            Control_R: noop
            Caps_Lock: clear
            Eisu_toggle: clear
        ```
    4.  可以配置各种皮肤 squirrel.yaml
        color_scheme: clean_white
    5.  注意 rime 的任何配置文件更改 都需要重新部署一下,点击 deploy 按钮
    6.  rime 词库同步备份: luna_pinyin.userdb.txt
    7.  删除系统 ABC 输入法 （注意备份）
        cd ~/Library/Preferences/
        plutil -p com.apple.HIToolbox.plist // 查看 plist 的命令
        plutil -remove AppleEnabledInputSources.0 com.apple.HIToolbox.plist // 删除具有 `"KeyboardLayout Name" => "ABC"` 的节点
        重启系统即可

<a id="%E5%85%B6%E4%BB%96"></a>
## 其他

<a id="%E7%BB%88%E7%AB%AF%E6%98%BE%E7%A4%BA-bogon"></a>
### 终端显示 bogon

更改主机名 `sudo scutil --set HostName Mac`
<a id="%E6%89%93%E5%BC%80%E5%85%A8%E9%94%AE%E7%9B%98%E6%8E%A7%E5%88%B6"></a>
### 打开全键盘控制
```
System Preferences > Keyboard > Shortcuts > All controls
Don't Save 按钮(备选按钮)有了一圈蓝边，这个意味着你可以通过空格键触发。不仅如此，你还可以用Tab键把蓝边转移到其他按钮，来实现全键盘控制。
```
<a id="%E8%AF%AD%E9%9F%B3"></a>
### 语音
```
1. 命令行中使用 say 命令;
2. alt + Esc 快捷键
3. cmd + ctrl + d 打开词典
```

<a id="%E5%88%87%E6%8D%A2-root-%E7%94%A8%E6%88%B7"></a>
### 切换 root 用户
```
sudo su
```

<a id="%E5%A6%82%E6%9E%9C-%E7%94%B5%E6%B1%A0%E6%9C%AA%E5%85%85%E7%94%B5"></a>
### 如果 电池未充电
1.  重置 [smc](https://support.apple.com/zh-cn/HT201295)
2.  重置不知道是啥
    1.  按一下开机键并松开
    2.  马上按住 `command + option + p + r` 持续 `20` 秒,然后松开.
