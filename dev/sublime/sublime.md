---
date: '2018-11-10 22:06:06'
tags: [dev, sublime]
title: sublime 常用的优秀插件列表和介绍
updated: '2018-12-14 12:19:08'
...
---
# sublime 常用的优秀插件列表和介绍

<!-- MarkdownTOC -->

- [常用命令](#%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4)
- [优秀的插件介绍](#%E4%BC%98%E7%A7%80%E7%9A%84%E6%8F%92%E4%BB%B6%E4%BB%8B%E7%BB%8D)
    - [Material Theme](#material-theme)
    - [AceJump](#acejump)
    - [Align Arguments](#align-arguments)
    - [AutoFileName](#autofilename)
    - [FileManager](#filemanager)
    - [PackageResourceViewer](#packageresourceviewer)
    - [Markdown 完美支持](#markdown-%E5%AE%8C%E7%BE%8E%E6%94%AF%E6%8C%81)
    - [SaneSnippets](#sanesnippets)
- [常用扩展包列表 \(高亮的必装\)](#%E5%B8%B8%E7%94%A8%E6%89%A9%E5%B1%95%E5%8C%85%E5%88%97%E8%A1%A8-%E9%AB%98%E4%BA%AE%E7%9A%84%E5%BF%85%E8%A3%85)

<!-- /MarkdownTOC -->

<a id="%E5%B8%B8%E7%94%A8%E5%91%BD%E4%BB%A4"></a>
### 常用命令
-   禁用/启用一些扩展包

    命令 `disable package` / `enable package`, 可以临时禁用和启用一些插件

-   查看插件或编辑器中的文件

    命令 `view package file`, 可以用来查看插件包中的文件, 好处是可以借鉴别人写的
    代码.如果忘记某个插件的用法,可以查看插件的 readme 文件.

<a id="%E4%BC%98%E7%A7%80%E7%9A%84%E6%8F%92%E4%BB%B6%E4%BB%8B%E7%BB%8D"></a>
### 优秀的插件介绍

<a id="material-theme"></a>
#### Material Theme
感觉最好的主题之一,可惜作者转投 atom,vsCode 了. 嗯,如果哪一天 atom 能减减肥,我也
很乐意投奔.毕竟 st 不开源.

<a id="acejump"></a>
#### AceJump
输入想要跳转的位置的单词首字母,立即就可以跳转过去. 键盘党的福音.

<a id="align-arguments"></a>
#### Align Arguments
对齐等号或者任意自定义的符号. 两边对齐.代码洁癖必备.

<a id="autofilename"></a>
#### AutoFileName
自动补全路径

<a id="filemanager"></a>
#### FileManager
文件管理神器, 嗯用了这个插件比 IDE 的鼠标拖动移动复制文件还爽. sublime 最强文件
管理之一. 可以替代 SideBarTools,SideBarEnhancements,AdvancedNewFile 等

修复 open in brower 命令无法打开中文名称文件的 bug
`FileManager/FMcommands/open_in_browser.py`
```python
import urllib
// 大概在 24,后面将 path 变量 urlencode 格式化一下
path = urllib.parse.quote(path)
```

修复: fm_creater 命令批量创建时新文件都会打开的问题
`FileManager/FMcommands/create.py`
```python
class FmCreaterCommand(AppCommand):
    def run(self, abspath, input_path, is_open=True): # 增加参数 is_open=True
        ...
        if is_open:  # 增加判断 if is_open:
            window = get_window()
            ...
```

<a id="packageresourceviewer"></a>
#### PackageResourceViewer
`修改`或查看sublime安装的包;
使用方法:
```
PackageResourceViewer: Open Resource
// 修改后, 如果不生效,需要重新启动 sublime; mac os 需要强制退出程序
```

<a id="markdown-%E5%AE%8C%E7%BE%8E%E6%94%AF%E6%8C%81"></a>
#### Markdown 完美支持
-   `MarkdownEditing` // 编辑 markdown 支持各种代码高亮和补全
-   `Markdown Preview` // markdown 预览, 如果想热加载的话,可以安装 `LiveLoad`
-   `MarkdownTOC` // 自动生成目录
MarkdownTOC 修要修改 `/Packages/MarkdownTOC/markdowntoc/autorunner.py`
```
// 禁止 保存时自动更新 toc
if False:
    view.run_command('markdowntoc_update')
```

<a id="sanesnippets"></a>
#### SaneSnippets
嗯,更友好的 snippet 模板.对 xml 无爱.

<a id="%E5%B8%B8%E7%94%A8%E6%89%A9%E5%B1%95%E5%8C%85%E5%88%97%E8%A1%A8-%E9%AB%98%E4%BA%AE%E7%9A%84%E5%BF%85%E8%A3%85"></a>
### 常用扩展包列表 (高亮的必装)
-   `AceJump` // 代替鼠标快速跳转
-   `Align Arguments` // 等号两边对齐
-   `AutoFileName` // 自动补全文件名
-   `All Autocomplete` // 所有打开的标签页中寻找补全
-   AutoSetSyntax // 自动切换文件的格式
-   Blade Snippets // laravel blade 模板
-   Bootstrap 3 Snippets // bt3 snippets
-   `BracketHighlighter` // 括号,引号这类高亮功能
-   DeleteBlankLines // 删除空行 (key: Ctrl+Alt+Backspace)
-   `DocBlockr` // 注释 (key: /** + tab 补全)
-   `Emmet` // web 自动补全(key: tab)
-   `FileManager` // 文件管理
-   Git // git
-   `HTML-CSS-JS Prettify` // 格式化
-   IMESupport // win10 中文输入法支持 (安装第三方输入法需要安装此插件)
-   Laravel Blade Highlighter // blade 模板高亮
-   Markdown Table Formatter // 格式化 markdown Table
-   `MarkdownEditing` // 编辑 markdown 支持各种代码高亮和补全
-   `Markdown Preview` // markdown 预览 (cmd: markdown preview)
-   `MarkdownTOC` // markdown 自动添加目录 (cmd: markdowntoc)
-   `Material Theme`
-   `PackageResourceViewer` // 修改或查看 包
-   `SaneSnippets` // 更友好的 snippet
-   Package Control // 包管理
-   Pretty JSON // json 格式化 (cmd: pretty json)
-   Trimmer // 删除空格空行等
-   PyV8 // emmet 依赖的扩展
-   SFTP // ftp 插件 (cmd: sftp)
-   Vue Syntax Highlight // vue 模板语法高亮
