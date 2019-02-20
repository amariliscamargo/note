---
categories: [dev, developer]
date: '2018-12-24 20:36:36'
tags: [dev, developer]
title: 从 1Mbps 说起
titleen: Speaking from 1Mbps
updated: '2018-12-25 09:54:10'
...
---
# 从 1Mbps 说起
<!-- MarkdownTOC -->

- [`binary` \(二进制\)](#binary-%E4%BA%8C%E8%BF%9B%E5%88%B6)
- [`Bit | Binary digit 的缩写` \(直译为: 二进制数字; 意译为: 位; 音译为: 比特\)](#bit-%7C-binary-digit-%E7%9A%84%E7%BC%A9%E5%86%99-%E7%9B%B4%E8%AF%91%E4%B8%BA-%E4%BA%8C%E8%BF%9B%E5%88%B6%E6%95%B0%E5%AD%97-%E6%84%8F%E8%AF%91%E4%B8%BA-%E4%BD%8D-%E9%9F%B3%E8%AF%91%E4%B8%BA-%E6%AF%94%E7%89%B9)
- [Byte \(字节\)](#byte-%E5%AD%97%E8%8A%82)
- [MB 和 MiB](#mb-%E5%92%8C-mib)
- [Bit rate \(比特率\)](#bit-rate-%E6%AF%94%E7%89%B9%E7%8E%87)
- [1Mbps](#1mbps)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->

<a id="binary-%E4%BA%8C%E8%BF%9B%E5%88%B6"></a>
## `binary` (二进制)
1.  1854年，英国数学家 `乔治·布尔` 创立了 `布尔代数`; 他提出的逻辑演算在后来的电子电路设计中起基础性作用
2.  1937年，`克劳德·香农` 在 MIT 完成了其硕士论文; 成为现代数字电路的理论基础; 论文题为《继电器与开关电路的符号分析》

二进制是一种记数系统; 这一系统中,通常用两个不同的符号 `0` 和 `1` 来表示;

<a id="bit-%7C-binary-digit-%E7%9A%84%E7%BC%A9%E5%86%99-%E7%9B%B4%E8%AF%91%E4%B8%BA-%E4%BA%8C%E8%BF%9B%E5%88%B6%E6%95%B0%E5%AD%97-%E6%84%8F%E8%AF%91%E4%B8%BA-%E4%BD%8D-%E9%9F%B3%E8%AF%91%E4%B8%BA-%E6%AF%94%E7%89%B9"></a>
## `Bit | Binary digit 的缩写` (直译为: 二进制数字; 意译为: 位; 音译为: 比特)
通常缩写成 `b` (小写);  

数字电子电路中, `逻辑门` 的实现直接应用了二进制.  
因此现代的计算机和依赖计算机的设备里都用到二进制; 每个数字称为一个 `Bit` (Binary digit 的缩写) 

<a id="byte-%E5%AD%97%E8%8A%82"></a>
## Byte (字节)
通常缩写成 `B` (大写);  
`Byte` 表示用于`编码单个字符`所需要的 `Bit` 数量;

历史上字节长度曾基于硬件为 1-48 Bit 不等, 最初通常使用 *6 Bit* 或 *9 Bit* 为一字节.  
今日事实标准以 `8 Bit` 作为一字节,因8为二进制整数

it is the smallest addressable unit of memory in many computer architectures; (即:我们可操作的最小单位)

<a id="mb-%E5%92%8C-mib"></a>
## MB 和 MiB
MB
(Megabyte) (Mega 表示"兆") 这里的 "兆" 是 1百万; 而不是 [计数单位][] 中, `亿`之后的单位
1MB 的容量大小为: 1,000,000 Byte  一百万字节
换算关系为 1000; 1MB = 1000KB; 1KB = 1000比特

MiB (Mebibyte) (Mebi 表示 2的20次方)
1MiB 的容量大小为: 1,048,576 Byte  一百万零四万八千五百七十六 字节
换算关系为 1024; 即 `2的10次方`

<a id="bit-rate-%E6%AF%94%E7%89%B9%E7%8E%87"></a>
## Bit rate (比特率)
是单位时间内传输或处理的比特的数量; 当表示`传输`的时候和 `带宽` 是同义词

经常和国际单位制词头关联在一起，如 `千`(Kbit/s或Kbps) `兆`(Mbit/s或Mbps)

<a id="1mbps"></a>
## 1Mbps
Mbps 中 `ps` (per second 的缩写, 每秒的意思)
**注意:** 此单位的字母 `b` ,是 `小写` 的; 代表 `比特`; 而不是我们通常理解的 `字节`  
也就是说: 移动联通的 "100M" 与我们正常理解的 `100MiB` 缩水了 **8.39 倍**  
```
100Mbps = 100*1000*1000 bit 每秒
100MiB/s = 100*1024*1024*8 bit 每秒
```

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[二进制 - 维基百科][] | [比特 - 维基百科][] | [字节 - 维基百科][] | [Mebibyte - 维基百科][] | [比特率 - 维基百科][] | [计数单位][] | [家庭有线宽带业务服务协议 - 中国移动官方网站][] | [字节 & 字节流 & 管道 & 重定向][]

[二进制 - 维基百科]:https://zh.wikipedia.org/wiki/%E4%BA%8C%E8%BF%9B%E5%88%B6
[比特 - 维基百科]:https://zh.wikipedia.org/wiki/%E4%BD%8D%E5%85%83
[字节 - 维基百科]:https://zh.wikipedia.org/wiki/%E5%AD%97%E8%8A%82
[Mebibyte - 维基百科]:https://zh.wikipedia.org/wiki/Mebibyte
[比特率 - 维基百科]:https://zh.wikipedia.org/wiki/%E6%AF%94%E7%89%B9%E7%8E%87
[计数单位]:https://baike.baidu.com/item/%E8%AE%A1%E6%95%B0%E5%8D%95%E4%BD%8D/9836030?fr=aladdin
[家庭有线宽带业务服务协议 - 中国移动官方网站]:http://service.bj.10086.cn/bjyd/web/support/xieyi/yxxy.html
[字节 & 字节流 & 管道 & 重定向]:../linux/lpic-1/commands-and-gnu/streams-pipes-redirects.md
