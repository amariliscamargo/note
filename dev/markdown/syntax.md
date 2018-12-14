---
date: '2018-12-13 14:51:19'
tags: [dev, markdown]
title: Markdown 语法
updated: '2018-12-14 00:02:07'
...
---
# Markdown 语法
<!-- MarkdownTOC -->

- [标题 `h`](#%E6%A0%87%E9%A2%98-h)
    - [ATX 形式](#atx-%E5%BD%A2%E5%BC%8F)
    - [Setext 形式](#setext-%E5%BD%A2%E5%BC%8F)
- [段落 `p`](#%E6%AE%B5%E8%90%BD-p)
- [换行 `br`](#%E6%8D%A2%E8%A1%8C-br)
- [引用 `blockquote`](#%E5%BC%95%E7%94%A8-blockquote)
    - [单行与多行,及换行](#%E5%8D%95%E8%A1%8C%E4%B8%8E%E5%A4%9A%E8%A1%8C%E5%8F%8A%E6%8D%A2%E8%A1%8C)
    - [嵌套引用](#%E5%B5%8C%E5%A5%97%E5%BC%95%E7%94%A8)
- [列表 `ul,ol`](#%E5%88%97%E8%A1%A8-ulol)
    - [无序列表 `ul`](#%E6%97%A0%E5%BA%8F%E5%88%97%E8%A1%A8-ul)
    - [有序列表 `ol`](#%E6%9C%89%E5%BA%8F%E5%88%97%E8%A1%A8-ol)
    - [列表的嵌套](#%E5%88%97%E8%A1%A8%E7%9A%84%E5%B5%8C%E5%A5%97)
- [代码 `figure,pre,code`](#%E4%BB%A3%E7%A0%81-figureprecode)
    - [行内代码 `code`](#%E8%A1%8C%E5%86%85%E4%BB%A3%E7%A0%81-code)
    - [普通代码块](#%E6%99%AE%E9%80%9A%E4%BB%A3%E7%A0%81%E5%9D%97)
    - [高亮代码块](#%E9%AB%98%E4%BA%AE%E4%BB%A3%E7%A0%81%E5%9D%97)
- [分隔线 `hr`](#%E5%88%86%E9%9A%94%E7%BA%BF-hr)
- [超链接 `a`](#%E8%B6%85%E9%93%BE%E6%8E%A5-a)
    - [行内式](#%E8%A1%8C%E5%86%85%E5%BC%8F)
    - [参考式](#%E5%8F%82%E8%80%83%E5%BC%8F)
    - [短链接和邮箱](#%E7%9F%AD%E9%93%BE%E6%8E%A5%E5%92%8C%E9%82%AE%E7%AE%B1)
- [图像 `img`](#%E5%9B%BE%E5%83%8F-img)
    - [行内式](#%E8%A1%8C%E5%86%85%E5%BC%8F-1)
    - [参考式](#%E5%8F%82%E8%80%83%E5%BC%8F-1)
    - [指定图片的显示大小](#%E6%8C%87%E5%AE%9A%E5%9B%BE%E7%89%87%E7%9A%84%E6%98%BE%E7%A4%BA%E5%A4%A7%E5%B0%8F)
- [强调 `em,strong`](#%E5%BC%BA%E8%B0%83-emstrong)
- [反斜线转义](#%E5%8F%8D%E6%96%9C%E7%BA%BF%E8%BD%AC%E4%B9%89)
- [GFM 扩展语法](#gfm-%E6%89%A9%E5%B1%95%E8%AF%AD%E6%B3%95)
    - [删除线 `del`](#%E5%88%A0%E9%99%A4%E7%BA%BF-del)
    - [语法高亮](#%E8%AF%AD%E6%B3%95%E9%AB%98%E4%BA%AE)
    - [任务列表 `checkbox`](#%E4%BB%BB%E5%8A%A1%E5%88%97%E8%A1%A8-checkbox)
    - [表格 `table`](#%E8%A1%A8%E6%A0%BC-table)

<!-- /MarkdownTOC -->

<a id="%E6%A0%87%E9%A2%98-h"></a>
## 标题 `h`

<a id="atx-%E5%BD%A2%E5%BC%8F"></a>
### ATX 形式
> 支持 h1 - h6 六级标题;

```markdown
# H1
###### H6
```

<a id="setext-%E5%BD%A2%E5%BC%8F"></a>
### Setext 形式
> 仅支持 H1 和 H2 两级

```markdown
一级标题
========

二级标题
--------
```

<a id="%E6%AE%B5%E8%90%BD-p"></a>
## 段落 `p`
> 两个`空行`中包含的文字是段落

```markdown

这是一个段落,它的前后都是空行

```

<a id="%E6%8D%A2%E8%A1%8C-br"></a>
## 换行 `br`
> 如果要在段落中换行(即:插入 `<br/>`), 在行尾打`两个空格`即可

```markdown

注意此行末尾有两个空格  
我换行了

```

注意此行末尾有两个空格  
我换行了

<a id="%E5%BC%95%E7%94%A8-blockquote"></a>
## 引用 `blockquote`
<a id="%E5%8D%95%E8%A1%8C%E4%B8%8E%E5%A4%9A%E8%A1%8C%E5%8F%8A%E6%8D%A2%E8%A1%8C"></a>
### 单行与多行,及换行
> 在需要引用的`块`前添加 `>` 符号即可;  

```markdown
> 单行引用

> 多行引用:
> 第二行(这一行的`>`可以省略)

> 引用中换行, 注意:此行后面有(两个空格)  
> 第二行(也可以用空行代替 行尾的两个空格)
```

> 单行引用

> 多行引用:
> 第二行(这一行的`>`可以省略)

> 引用中换行, 注意:此行后面有(两个空格)  
> 第二行(也可以用空行代替 行尾的两个空格)

<a id="%E5%B5%8C%E5%A5%97%E5%BC%95%E7%94%A8"></a>
### 嵌套引用
```markdown
>也可以在引用中
>>使用嵌套的引用
```

>也可以在引用中使用
>>嵌套的引用

<a id="%E5%88%97%E8%A1%A8-ulol"></a>
## 列表 `ul,ol`

<a id="%E6%97%A0%E5%BA%8F%E5%88%97%E8%A1%A8-ul"></a>
### 无序列表 `ul`
> 使用 `+` `-` `*` 中任意一个符号,加上`空格`(空格推荐3个,方便嵌套).

```markdown
_   项目1
-   项目二
```

_   项目1
-   项目二

<a id="%E6%9C%89%E5%BA%8F%E5%88%97%E8%A1%A8-ol"></a>
### 有序列表 `ol`
> 使用数字和`.`加`空格` (空格推荐2个, 数字可以不按顺序)

```markdown
1.  项目1
2.  项目2
```

1.  项目1
2.  项目2

<a id="%E5%88%97%E8%A1%A8%E7%9A%84%E5%B5%8C%E5%A5%97"></a>
### 列表的嵌套
> 有序和无序列表可以任意嵌套

```markdown
-   无序一
    1.  有序1
    1.  有序2
-   无序二
```

-   无序一
    1.  有序1
    1.  有序2
-   无序二

<a id="%E4%BB%A3%E7%A0%81-figureprecode"></a>
## 代码 `figure,pre,code`

<a id="%E8%A1%8C%E5%86%85%E4%BB%A3%E7%A0%81-code"></a>
### 行内代码 `code`
> 使用 \` 符号来包含代码

```markdown
超文本文档的根标签是 `<html></html>` 不是 `<body></body>` 标签
```

超文本文档的根标签是 `<html></html>` 不是 `<body></body>` 标签

<a id="%E6%99%AE%E9%80%9A%E4%BB%A3%E7%A0%81%E5%9D%97"></a>
### 普通代码块
> 缩进四个空格

```
    // 注意: 每行开头都 缩进了四个空格
    $php_arr = array('hello' => 'world');
    echo $php_arr;
```

    // 注意: 每行开头都 缩进了四个空格
    $php_arr = array('hello' => 'world');
    echo $php_arr;

<a id="%E9%AB%98%E4%BA%AE%E4%BB%A3%E7%A0%81%E5%9D%97"></a>
### 高亮代码块
> 推荐使用 注意:这不是 **traditonal markdown** 的语法, 是 [GFM][gfm] 语法

    ```php
    $arr = array('hello' => 'world');
    echo $arr;
    ```

```php
$arr = array('hello' => 'world');
echo $arr;
```

<a id="%E5%88%86%E9%9A%94%E7%BA%BF-hr"></a>
## 分隔线 `hr`
> 推荐使用减号; `*` `-` `_` (至少连续使用3次)

```markdown
---
***
__________________
```

---
***
__________________

<a id="%E8%B6%85%E9%93%BE%E6%8E%A5-a"></a>
## 超链接 `a`

<a id="%E8%A1%8C%E5%86%85%E5%BC%8F"></a>
### 行内式
```markdown
[Google](http://www.google.com/)
[icon.png](./images/icon.png)
[Google](http://www.google.com/ "Google")
```

[Google](http://www.google.com/)
[icon.png](./images/icon.png)
[Google](http://www.google.com/ "Google 这里是 title")

<a id="%E5%8F%82%E8%80%83%E5%BC%8F"></a>
### 参考式
> 可以省略 *识别符*, 使用 *链接文本* 作为 *识别符*

```markdown
新版 [firfox][2] 性能和 [google][] 开发的 [chrome][google] 浏览器不分上下.

[google]:https://www.google.com
[2]:https://developer.mozilla.org/zh-CN/
```

新版 [firfox][2] 性能和 [google][] 开发的 [chrome][google] 浏览器不分上下.

[google]:https://www.google.com
[2]:https://developer.mozilla.org/zh-CN/

<a id="%E7%9F%AD%E9%93%BE%E6%8E%A5%E5%92%8C%E9%82%AE%E7%AE%B1"></a>
### 短链接和邮箱
> 自动链接方式, 适合行内 `较短的链接或邮箱`, 会使用 URL 作为链接文字; 邮箱地址会转换为 `<a href="mailto:"></a>` 的形式

```markdown
<https://www.google.com>
<name@gmail.com>
```
<https://www.google.com>
<name@gmail.com>

<a id="%E5%9B%BE%E5%83%8F-img"></a>
## 图像 `img`
> 与超链接一样,只是多了一个 *!*

<a id="%E8%A1%8C%E5%86%85%E5%BC%8F-1"></a>
### 行内式
```markdown
![ALT属性](https://developer.cdn.mozilla.net/static/img/mdn-logo-sm.png "TITLE属性")
```
![mdn-logo](https://developer.cdn.mozilla.net/static/img/mdn-logo-sm.png)

<a id="%E5%8F%82%E8%80%83%E5%BC%8F-1"></a>
### 参考式
```markdown
![MDN][mdn-logo] 参考式可以多次使用 ![火狐开发者][mdn-logo]

[mdn-logo](https://developer.cdn.mozilla.net/static/img/mdn-logo-sm.png)
```
![MDN][logo] 参考式可以多次使用 ![火狐开发者][logo]

[logo]:https://developer.cdn.mozilla.net/static/img/mdn-logo-sm.png

<a id="%E6%8C%87%E5%AE%9A%E5%9B%BE%E7%89%87%E7%9A%84%E6%98%BE%E7%A4%BA%E5%A4%A7%E5%B0%8F"></a>
### 指定图片的显示大小
> 通过 `<img/>`来指定图片大小

<img src="https://developer.cdn.mozilla.net/static/img/mdn-logo-sm.png" alt="mdn-logo" width="50" height="20">

<a id="%E5%BC%BA%E8%B0%83-emstrong"></a>
## 强调 `em,strong`
```markdown
*斜体* _斜体_
**粗体** __粗体__
```

*斜体* _斜体_
**粗体** __粗体__

<a id="%E5%8F%8D%E6%96%9C%E7%BA%BF%E8%BD%AC%E4%B9%89"></a>
## 反斜线转义
> 反斜线 `\` 将 Markdown 语法中的特殊符号转化为普通字符

```markdown
例如可以转义 **粗体文字** 符号(转义前)  
例如可以转义 \*\*粗体文字\*\* 符号(转义后)
```

例如可以转义 **粗体文字** 符号(转义前)  
例如可以转义 \*\*粗体文字\*\* 符号(转义后)


<a id="gfm-%E6%89%A9%E5%B1%95%E8%AF%AD%E6%B3%95"></a>
## GFM 扩展语法
> 注意: Markdown 有很多扩展语法, [GitHub Flavored Markdown][gfm] 是比较流行的一种  
> 参考 [gfm 详细文档][gfm-doc] | [gfm 基本语法][gfm] | [mastering-markdown][]

<a id="%E5%88%A0%E9%99%A4%E7%BA%BF-del"></a>
### 删除线 `del`
```markdown
~~删除线~~
```

~~删除线~~

<a id="%E8%AF%AD%E6%B3%95%E9%AB%98%E4%BA%AE"></a>
### 语法高亮

    ```javascript
    function fancyAlert(arg) {
        alert(arg)
    }
    ```

```javascript
function fancyAlert(arg) {
    alert(arg)
}
```

<a id="%E4%BB%BB%E5%8A%A1%E5%88%97%E8%A1%A8-checkbox"></a>
### 任务列表 `checkbox`
```markdown
- [x] @mentions, and <del>tags</del> supported
- [ ] this is an incomplete item
```

- [x] @mentions, and <del>tags</del> supported
- [ ] this is an incomplete item

<a id="%E8%A1%A8%E6%A0%BC-table"></a>
### 表格 `table`
```markdown
| 姓名   | 爱好   | 其他表头信息                |
| :---   | ---:   | :----------:                |
| 左对齐 | 右对齐 | 居中                        |
| 小明   | 刚首   | content in the three column |
```

| 姓名   | 爱好   | 其他表头信息                |
| :---   | ---:   | :----------:                |
| 左对齐 | 右对齐 | 居中                        |
| 小明   | 刚首   | content in the three column |



[gfm]:https://help.github.com/articles/basic-writing-and-formatting-syntax/
[gfm-doc]:https://github.github.com/gfm/
[mastering-markdown]:https://guides.github.com/features/mastering-markdown/
