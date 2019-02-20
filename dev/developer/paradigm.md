---
categories: [dev, developer]
date: '2019-02-20 20:59:20'
tags: [dev, developer]
title: 常见的编程范式 (草稿)
titleen: Common programming paradigm (draft)
updated: '2019-02-20 23:14:29'
...
---
# 常见的编程范式 (草稿)
<!-- MarkdownTOC -->

- [命令式编程 和 声明式编程 的对比](#%E5%91%BD%E4%BB%A4%E5%BC%8F%E7%BC%96%E7%A8%8B-%E5%92%8C-%E5%A3%B0%E6%98%8E%E5%BC%8F%E7%BC%96%E7%A8%8B-%E7%9A%84%E5%AF%B9%E6%AF%94)
    - [概念](#%E6%A6%82%E5%BF%B5)
    - [例子](#%E4%BE%8B%E5%AD%90)
- [声明式 和 函数式 的关系](#%E5%A3%B0%E6%98%8E%E5%BC%8F-%E5%92%8C-%E5%87%BD%E6%95%B0%E5%BC%8F-%E7%9A%84%E5%85%B3%E7%B3%BB)
- [编程范式之间的关系 Programming paradigm](#%E7%BC%96%E7%A8%8B%E8%8C%83%E5%BC%8F%E4%B9%8B%E9%97%B4%E7%9A%84%E5%85%B3%E7%B3%BB-programming-paradigm)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->

<a id="%E5%91%BD%E4%BB%A4%E5%BC%8F%E7%BC%96%E7%A8%8B-%E5%92%8C-%E5%A3%B0%E6%98%8E%E5%BC%8F%E7%BC%96%E7%A8%8B-%E7%9A%84%E5%AF%B9%E6%AF%94"></a>
## 命令式编程 和 声明式编程 的对比
<a id="%E6%A6%82%E5%BF%B5"></a>
### 概念
命令式: 需要用算法来明确的指出每一步该怎么做(即:明确流程)
声明式: 让计算机明白目标, 而非流程

命令式: 告诉计算机“如何”去计算; (默认程序不知道怎么做)
声明式: 告诉计算机需要计算“什么”而不是“如何”去计算 (默认程序已经明白怎么做)

<a id="%E4%BE%8B%E5%AD%90"></a>
### 例子
筛选出数组 `numbers` 中大于 5 的数字
**命令式编程的实现方式**
需要一步一步告诉计算机改怎么做
1.  创建一个存储结果的数组 `results`;
2.  遍历 `numbers` 数组
3.  一个一个的判断 `numbers` 数组中的数字是否大于 5, 满足条件则添加到 `results` 中;
```js
numbers = [1,2,6,7];
var results = [];
for (var i = 0; i < numbers.length; i++) {
    if (numbers[i] > 5) {
        results.push(numbers[i]);
    }
}
console.log(results); // [6,7]
```

**声明式编程的实现方式**
```js
numbers = [1,2,6,7];
// 更确切的说是"函数式编程"的实现方式
console.log( numbers.filter(num => num > 5) );
```
它的主要思想是告诉计算机应该做什么，但不指定具体要怎么做 
SQL 语句是一种典型的声明式编程形式;
```sql
SELECT * FROM numbers WHERE num > 5
```
除了 SQL，网页编程中用到的 HTML 和 CSS 也都属于声明式编程。
```html
<a href="www.google.com" style="color: #f00;">google</a>
```

<a id="%E5%A3%B0%E6%98%8E%E5%BC%8F-%E5%92%8C-%E5%87%BD%E6%95%B0%E5%BC%8F-%E7%9A%84%E5%85%B3%E7%B3%BB"></a>
## 声明式 和 函数式 的关系
声明式和函数式的思想是一致的:即只关注做什么而不是怎么做; 
函数式编程在声明式的基础上新增了 **"函数"** 的概念

函数式编程中的 **"函数"** 这个术语不是指计算机中的函数（实际上是Subroutine），而是指数学中的函数，即自变量的映射。也就是说一个函数的值仅决定于函数参数的值，不依赖其他状态。比如sqrt(x)函数计算x的平方根，只要x不变，不论什么时候调用，调用几次，值都是不变的。

纯函数式编程语言中的变量也不是命令式编程语言中的变量，即存储状态的单元，而是代数中的变量，即一个值的名称。变量的值是不可变的（immutable），也就是说不允许像命令式编程语言中那样多次给一个变量赋值。比如说在命令式编程语言我们写 `x = x + 1` 这依赖可变状态的事实，拿给程序员看说是对的，但拿给数学家看，却被认为这个等式为假。


<a id="%E7%BC%96%E7%A8%8B%E8%8C%83%E5%BC%8F%E4%B9%8B%E9%97%B4%E7%9A%84%E5%85%B3%E7%B3%BB-programming-paradigm"></a>
## 编程范式之间的关系 Programming paradigm
1.  命令式编程 Imperative programming
    1.  面向对象编程 Object-oriented programming
2.  声明式编程 Declarative programming
    1.  函数式编程 functional programming

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[编程范型 - 维基百科，自由的百科全书][] | [命令式编程 - 维基百科，自由的百科全书][] | [声明式编程 - 维基百科，自由的百科全书][] | [命令式、声明式、面向对象、函数式、控制反转之华山论剑（上） - 掘金][] | [编程范式：命令式编程(Imperative)、声明式编程(Declarative)和函数式编程... - 简书][] | [面向对象编程 VS 函数式编程 | SwanSpace][] | [渣翻——Function、Method、Procedure和Subroutine的区别 - millis的博客 - CSDN博客][] | [什么是函数式编程思维？ - 知乎][]

[编程范型 - 维基百科，自由的百科全书]:https://zh.wikipedia.org/wiki/%E7%BC%96%E7%A8%8B%E8%8C%83%E5%9E%8B
[命令式编程 - 维基百科，自由的百科全书]:https://zh.wikipedia.org/wiki/%E6%8C%87%E4%BB%A4%E5%BC%8F%E7%B7%A8%E7%A8%8B
[声明式编程 - 维基百科，自由的百科全书]:https://zh.wikipedia.org/wiki/%E5%AE%A3%E5%91%8A%E5%BC%8F%E7%B7%A8%E7%A8%8B
[命令式、声明式、面向对象、函数式、控制反转之华山论剑（上） - 掘金]:https://juejin.im/post/5950b0c56fb9a06bca0b7c04
[编程范式：命令式编程(Imperative)、声明式编程(Declarative)和函数式编程... - 简书]:https://www.jianshu.com/p/bbd0e9798221
[面向对象编程 VS 函数式编程 | SwanSpace]:http://blog.swanspace.org/oo_vs_fp/
[渣翻——Function、Method、Procedure和Subroutine的区别 - millis的博客 - CSDN博客]:https://blog.csdn.net/millis/article/details/76405489
[什么是函数式编程思维？ - 知乎]:https://www.zhihu.com/question/28292740/answer/40336090
