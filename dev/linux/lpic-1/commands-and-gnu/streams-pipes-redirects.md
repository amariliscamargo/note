---
date: '2018-12-17 18:30:53'
tags: [dev, linux, lpic-1, commands-and-gnu]
categories: [dev, linux, lpic-1, commands-and-gnu]
title: 字节 & 字节流 & 管道 & 重定向
updated: '2018-12-19 15:26:06'
...
---
# 字节 & 字节流 & 管道 & 重定向
<!-- MarkdownTOC -->

- [位 \(bit\)](#%E4%BD%8D-bit)
- [字节 \(Byte\)](#%E5%AD%97%E8%8A%82-byte)
    - [字节与编码](#%E5%AD%97%E8%8A%82%E4%B8%8E%E7%BC%96%E7%A0%81)
- [字节流 \(Byte stream\)](#%E5%AD%97%E8%8A%82%E6%B5%81-byte-stream)
    - [`流 stream` 的定义](#%E6%B5%81-stream-%E7%9A%84%E5%AE%9A%E4%B9%89)
    - [标准的 I/O 流](#%E6%A0%87%E5%87%86%E7%9A%84-io-%E6%B5%81)
- [重定向 流\(redirect Byte stream\)](#%E9%87%8D%E5%AE%9A%E5%90%91-%E6%B5%81redirect-byte-stream)
    - [重定向标准输出](#%E9%87%8D%E5%AE%9A%E5%90%91%E6%A0%87%E5%87%86%E8%BE%93%E5%87%BA)
    - [重定向标准输出相关的操作符](#%E9%87%8D%E5%AE%9A%E5%90%91%E6%A0%87%E5%87%86%E8%BE%93%E5%87%BA%E7%9B%B8%E5%85%B3%E7%9A%84%E6%93%8D%E4%BD%9C%E7%AC%A6)
    - [重定向标准输入](#%E9%87%8D%E5%AE%9A%E5%90%91%E6%A0%87%E5%87%86%E8%BE%93%E5%85%A5)
    - [重定向标准错误](#%E9%87%8D%E5%AE%9A%E5%90%91%E6%A0%87%E5%87%86%E9%94%99%E8%AF%AF)
    - [3个标准流 组合使用](#3%E4%B8%AA%E6%A0%87%E5%87%86%E6%B5%81-%E7%BB%84%E5%90%88%E4%BD%BF%E7%94%A8)
- [管道 \(pipe\)](#%E7%AE%A1%E9%81%93-pipe)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->
[回到目录](../index.md)

<a id="%E4%BD%8D-bit"></a>
## 位 (bit)
`bit` 是计算机`存储数据`的基本单位或最小单位;

计算机只能表示两种状态(因为计算机用高电平和低电平分别表示1和0): `0` 或 `1` (即: bit)  
所以计算机中的所有数据都以`二进制序列`存储

<a id="%E5%AD%97%E8%8A%82-byte"></a>
## 字节 (Byte)
'Byte' 是计算机系统`操作数据`的基本单位; 或者说最小的可寻址的存储器单位  
也就是说: 我们访问计算机最小的单位是`八个位构成`的`字节`，而不是值`0或值1`的单个`位`  

为什么 `Unix` 一个字节是八位而不是4位,5位? 参考: [为什么1个字节等8位][]

字节的范围: 00000000 - 11111111 (即: 十进制的 0 - 255) 共 256 种状态  
```js
parseInt('00000000', 2) // 0
parseInt('1111111', 2) // 7位是十进制的 127
parseInt('11111111', 2) // 8位是十进制的 255
```
把一个字节的`256种状态`分别对应一个符号,就是256个符号  
例如我们可以像下面这样规定`字节状态`和`符号`的对应关系:

| 字节状态 | 表示的字符 | 解释      |
| -        | -          | -         |
| 00000000 | null       | 空字符    |
| 00110000 | 0          | 数字0     |
| 01000001 | A          | 大写字母A |

这就构成了一个编码表;

<a id="%E5%AD%97%E8%8A%82%E4%B8%8E%E7%BC%96%E7%A0%81"></a>
### 字节与编码
那么具体用哪个`二进制序列`或(字节状态) 表示哪个字符?  
当然每个人都可以约定自己的一套（这就叫编码）  
而大家如果要想互相通信而不造成混乱，那么大家就必须使用相同的编码规则，  
于是美国国家标准学会 [ANSI][] American National Standards Institute 定制了美国信息交换标准代码 [ASCII][]编码，统一规定了常用的字符用哪些`二进制序列`来表示

需要指出的是 ANSI 最初是用 `7bit` 128中状态; 只能表示美国常用的 `128` 个字符; 而西欧文字 128 个字符是不够表示的  
所以又定义了 [EASCII][] 来作为 ASCII 的扩充版本; 将ASCII码由`7bit`扩充为`8bit`  
那么中文怎么表示? 参考: [ASCII, GB2312, 和 Unicode, UTF-8]

<a id="%E5%AD%97%E8%8A%82%E6%B5%81-byte-stream"></a>
## 字节流 (Byte stream)

<a id="%E6%B5%81-stream-%E7%9A%84%E5%AE%9A%E4%B9%89"></a>
### `流 stream` 的定义  
又叫做流或文本流  
流是一个可以使用库功能读取或写入的字节序列，库功能向应用程序隐藏了底层设备的细节。  
通过使用流，相同的程序可以使用独立于设备的方式从终端、文件或网络 socket 中读取，或向其中写入。  

<a id="%E6%B5%81-stream-%E7%9A%84%E8%A7%A3%E9%87%8A"></a>
**解释:**  
linux 中 "everything is a file" 更准确的说法是: "Everything is a stream of bytes"  
系统运行中，数据并不是在一个文件里定居。数据会在CPU的指挥下不断地流动，就好像一个勤劳的上班族。有时数据需要到办公室上班，因此被读入到内存，有时会去酒店休假，传送到外部设备。有的时候，数据需要搬个家，转移到另一个文件。  
在这样跑来跑去的过程中，数据像是排着队走路的人流，我们叫它文本流(text stream 或 byte stream)  
然而，计算机不同设备之间的连接方法差异很大，从内存到文件的连接像是爬山，从内存到外设像是游过一条河。  
为此，Unix定义了`流 (stream)`，作为连接操作系统各处的公路标准。  
有了 `流` 的概念，无论是从内存到外设，还是从内存到文件，所有的数据公路都是相同的格式。  
至于公路下面是石头还是土地，就都交给操作系统处理，不劳用户操心。**(即: 隐藏了底层设备的细节)**

<a id="%E6%A0%87%E5%87%86%E7%9A%84-io-%E6%B5%81"></a>
### 标准的 I/O 流
Linux shell（比如 Bash）接收或发送 序列和字符串 `流形式`的输入或输出。  
每个字符都独立于与之相邻的字符。字符没有被组织成结构化记录或固定大小的块。**(即: 流可以截取任意长度,可以读一点处理一点)**  
不管实际的`流`来自文件、键盘、显示窗口或其他 I/O 设备，都使用`文件 I/O 技术标准`来访问流。**(即: 隐藏了底层设备的细节)**  

现代编程环境和shell使用`标准 I/O 流`, 它由三种流组成,每种流都与一个文件描述符相关联：
-   stdin` 是标准输入流，它为命令提供输入。它的文件描述符为 `0`
-   stdout` 是标准输出流，它显示来自命令的输出。它的文件描述符为 `1`
-   stderr` 是标准错误流，它显示来自命令的错误输出。它的文件描述符为 `2`

**解释:**
当 `Unix` 执行一个程序的时候,会自动打开这三个流  
比如说你打开命令行的时候,默认情况下,命令行的标准输入连接到键盘,标准输出和标准错误都连接到屏幕。  
对于一个程序来说，尽管它总会打开这三个流，但它会根据需要使用，并不是一定要使用。

举个例子来理解`标准I/O`的三种流:
```bash
$ ls www/ a.txt
ls: a.txt: No such file or directory
www/:
head.css index.html main.js
```
首先:键盘输入的字节流 `ls www/ a.txt\n` ("\n"是敲击回车时的输入) **即:标准输入**  
然后:命令行程序调用`/bin/ls www/`得到结果 `head.css index.html main.js`**即:标准输出**
同时:命令行程序调用`/bin/ls a.txt`得到一个错误(因为没有a.txt这个目录或文件) `ls: a.txt: No such file or directory` **即:标准错误**
最后:标准输出的字节流和标准错误的字节流 都流向屏幕, 在屏幕上显示出来

<a id="%E9%87%8D%E5%AE%9A%E5%90%91-%E6%B5%81redirect-byte-stream"></a>
## 重定向 流(redirect Byte stream)
```bash
$ ls www/
head.css   index.html main.js
```
默认情况下 `命令行程序` 的 `标准输出`是流向屏幕的; 我们执行`ls`命令,屏幕上就会将文本流打印出来;  
<a id="%E9%87%8D%E5%AE%9A%E5%90%91%E6%A0%87%E5%87%86%E8%BE%93%E5%87%BA"></a>
### 重定向标准输出
如果我们不想让`字节流`流到屏幕,而是流到一个文件中; 可以通过 `重定向` 机制;
```bash
$ ls www > log.txt
```
命令中的 `>` 就是 *重定向标准输出* ;  
`>` 的作用就是告诉命令行程序,我现在要改变`字节流`的方向了.我们不让它流向屏幕,而是到 *log.txt* 这个文件中  
程序接收到我们的`redirect`指令后,会将标准输入指向 *log.txt* 这个文件;(如果文件不存在就创建,存在就覆写文件)  
我们执行下面的命令来验证一下:
```bash
$ ls
log.txt   readme.md www
$ cat log.txt
head.css
index.html
main.js
```
<a id="%E9%87%8D%E5%AE%9A%E5%90%91%E6%A0%87%E5%87%86%E8%BE%93%E5%87%BA%E7%9B%B8%E5%85%B3%E7%9A%84%E6%93%8D%E4%BD%9C%E7%AC%A6"></a>
### 重定向标准输出相关的操作符
- `>` 如果文件不存在就创建,存在就覆写(覆盖文件现有内容)
- `>>` 如果文件不存在就创建,存在则在文件后面追加文本流

<a id="%E9%87%8D%E5%AE%9A%E5%90%91%E6%A0%87%E5%87%86%E8%BE%93%E5%85%A5"></a>
### 重定向标准输入
```bash
$ cat < readme.md
README 说明
Lorem ipsum dolor sit amet, consectetur adipisicing elit.
```
`<` 符号来改变标准输入: 比如`cat`命令,它可以从标准输入读入`字节流`,并将stream导向到标准输出;  
上例子中,我们将cat标准输入指向 readme.md，文本会从文件流到 cat, 然后再导向到标准输出, 最后默认输出到屏幕上

<a id="%E9%87%8D%E5%AE%9A%E5%90%91%E6%A0%87%E5%87%86%E9%94%99%E8%AF%AF"></a>
### 重定向标准错误
```bash
$ cat a.txt readme.md
cat: a.txt: No such file or directory
README 说明
$ cat a.txt readme.md 2> log.txt
README 说明
```
上例中: cat 默认的标准输出,和标准错误都指向屏幕; 所以第一条命令,会把 `stdout` 和 `stderr` 都在屏幕上显示;  
而第二条命令使用 `2>` 将`标准错误`重新定向到 *log.txt*; 所以屏幕上只打印了 `stdout`;

因为 `标准错误的代码是 2` 所以用 `2>` 来表示

<a id="3%E4%B8%AA%E6%A0%87%E5%87%86%E6%B5%81-%E7%BB%84%E5%90%88%E4%BD%BF%E7%94%A8"></a>
### 3个标准流 组合使用
-   同时指定标准输入 和 标准输出 `< >`
    ```bash
    cat < readme.md > log.txt (效果: 将 readme.md 的内容复制到 log.txt)
    ```
-   同时指定标准输出 和 标准错误 `>&`
    ```bash
    $ cat a.txt readme.md >& log.txt
    $ cat log.txt
    cat: a.txt: No such file or directory (标准错误 也在 log.txt 文件中)
    README 说明 (标准输出也在 log.txt 文件中)
    ```

<a id="%E7%AE%A1%E9%81%93-pipe"></a>
## 管道 (pipe)
理解了流和重定向之后,管道的概念就易如反掌.  
管道可以将一个命令的`输出`导向到另一个命令的`输入`,  
从而让两个(或者更多命令)像流水线一样连续工作,不断地处理文本流.  
在命令行中,我们用 `|` 表示管道;

```bash
cat < a.txt | wc
```

`wc` 命令(word count),用于统计文本中的行数,单词个数,和 Byte数(对于纯英文文件就是字符个数,英文一个字母等于`1 Byte`)
a.txt中的文本先流到cat,然后从cat的标准输出流到wc的标准输入, 从而让 `wc` 统计a.txt中的字节流

Linux中的各个命令实际上高度专业化, 并尽量相互独立.每一个都只专注于一个小的功能.  
但通过 `pipe` 我们可以将这些功能合在一起, 实现一些复杂的目的.

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[Linux字节流][] | [ibm 1][] | [ibm 2][] | [ASCII][] | [EASCII][] | [为什么1个字节等8位][] | [ASCII, GB2312, 和 Unicode, UTF-8][] | [ANSI][]

[Linux字节流]:http://www.cnblogs.com/vamei/archive/2012/09/14/2683756.html
[ibm 1]:https://www.ibm.com/developerworks/cn/linux/l-lpic1-v3-103-4/
[ibm 2]:https://www.ibm.com/developerworks/cn/linux/l-lpic1-v3-103-2/
[ASCII]:https://baike.baidu.com/item/ASCII/309296?fr=aladdin
[EASCII]:https://zh.wikipedia.org/wiki/EASCII
[为什么1个字节等8位]:https://blog.csdn.net/fisherming/article/details/74009052
[ASCII, GB2312, 和 Unicode, UTF-8]:http://www.ruanyifeng.com/blog/2007/10/ascii_unicode_and_utf-8.html
[ANSI]:https://www.ansi.org/
