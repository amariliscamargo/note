---
categories: [dev, js, features]
date: '2018-12-23 20:29:16'
tags: [dev, js, features]
title: 数据类型的转换
titleen: Data type conversion
updated: '2019-02-07 09:58:45'
...
---
# 数据类型的转换
<!-- MarkdownTOC -->

- [概述](#%E6%A6%82%E8%BF%B0)
- [强制转换](#%E5%BC%BA%E5%88%B6%E8%BD%AC%E6%8D%A2)
    - [Number\(\)](#number)
        - [**原始类型值** 的转换规则:](#%E5%8E%9F%E5%A7%8B%E7%B1%BB%E5%9E%8B%E5%80%BC-%E7%9A%84%E8%BD%AC%E6%8D%A2%E8%A7%84%E5%88%99)
        - [**对象** 的转换规则:](#%E5%AF%B9%E8%B1%A1-%E7%9A%84%E8%BD%AC%E6%8D%A2%E8%A7%84%E5%88%99)
        - [`Number()` 与 `parseInt()` 的区别:](#number-%E4%B8%8E-parseint-%E7%9A%84%E5%8C%BA%E5%88%AB)
    - [String\(\)](#string)
        - [原始类型值](#%E5%8E%9F%E5%A7%8B%E7%B1%BB%E5%9E%8B%E5%80%BC)
        - [对象](#%E5%AF%B9%E8%B1%A1)
    - [Boolean\(\)](#boolean)
- [自动转换](#%E8%87%AA%E5%8A%A8%E8%BD%AC%E6%8D%A2)
- [参考](#%E5%8F%82%E8%80%83)

<!-- /MarkdownTOC -->
[回到系列教程主目录](../index.md)

<a id="%E6%A6%82%E8%BF%B0"></a>
## 概述
JavaScript 是一种动态类型语言，变量没有类型限制，可以随时赋予任意值。

虽然变量的数据类型是不确定的，但是各种运算符对数据类型是有要求的。  
如果运算符发现，运算子的类型与预期不符，就会自动转换类型。

本章主要内容:
1.  手动强制转换数据类型
2.  数据类型自动转换的规则

<a id="%E5%BC%BA%E5%88%B6%E8%BD%AC%E6%8D%A2"></a>
## 强制转换
-   Number()
-   String()
-   Boolean()

<a id="number"></a>
### Number()
<a id="%E5%8E%9F%E5%A7%8B%E7%B1%BB%E5%9E%8B%E5%80%BC-%E7%9A%84%E8%BD%AC%E6%8D%A2%E8%A7%84%E5%88%99"></a>
#### **原始类型值** 的转换规则:
```js
// 字符串 1 如果可以被解析为数值，则转换为相应的数值
Number('324') // 324
// 字符串 2 如果不可以被解析为数值，返回 NaN
Number('324abc') // NaN
// 字符串 3 空字符串转为0
Number('') // 0
// 布尔值 true 转成 1，false 转成 0
Number(true) // 1
Number(false) // 0
// undefined 转成 NaN
Number(undefined) // NaN
// null 转成0
Number(null) // 0
```
<a id="%E5%AF%B9%E8%B1%A1-%E7%9A%84%E8%BD%AC%E6%8D%A2%E8%A7%84%E5%88%99"></a>
#### **对象** 的转换规则:  
简单的规则是: 除了 *单个数值的数组* 外,全部返回 `NaN`
```js
Number({a: 1}) // NaN
Number([1, 2, 3]) // NaN
Number([5]) // 5
```
**背后的原理** 如下代码所示: (了解原理后,可以更改 `Number()` 的默认行为)  
1.  调用对象自身的valueOf方法。  
    1.1 如果返回原始类型的值，则 `return Number(原始类型)`;  
    1.2 如果返回的还是对象，则改为调用对象自身的`toString`方法。  
        1.2.1 如果toString方法返回原始类型的值，则`return Number(原始类型)`;  
        1.2.2 如果toString方法返回的是对象，就报错。
```js
obj = {a:1}
Number(obj)
if (typeof obj.valueOf() === 'object') { // 1. 真;    valueOf 返回对象本身;
    if (typeof obj.toString() === 'object') {// 2. 假;    toString返回字符串 "[object Object]"
        throw new Error('无法自动转换');
    } else {
        Number(obj.toString()); // 3. NaN;   Number("[object Object]") 返回 NaN
    }
} else {
    Number(obj.valueOf());
}
```
<a id="number-%E4%B8%8E-parseint-%E7%9A%84%E5%8C%BA%E5%88%AB"></a>
#### `Number()` 与 `parseInt()` 的区别:
`parseInt()` 逐个解析字符  
`Number()` 整体解析字符,只要有 *一个* 字符无法转成数值,整个字符串就会被转为 `NaN`
```js
parseInt('42 cats') // 42
Number('42 cats') // NaN
```

<a id="string"></a>
### String()
<a id="%E5%8E%9F%E5%A7%8B%E7%B1%BB%E5%9E%8B%E5%80%BC"></a>
#### 原始类型值
```js
// 数值
String(123) // "123"
// 布尔值
String(true) // "true"
// undefined 和 null
String(undefined) // "undefined"
String(null) // "null"
```
<a id="%E5%AF%B9%E8%B1%A1"></a>
#### 对象
-   如果是对象，返回一个类型字符串
-   如果是数组，返回该数组的字符串形式
```js
String({a: 1}) // "[object Object]"
String([1, 2, 3]) // "1,2,3"
```
转换对象参数 **背后的原理:**  
String方法背后的转换规则,与Number方法基本相同; 只是互换了valueOf方法和toString方法的执行顺序

<a id="boolean"></a>
### Boolean()
除了以下五个值的转换结果为 `false`, 其他的值全部为 `true`
```js
Boolean(undefined) // false
Boolean(null) // false
Boolean(0) // false
Boolean(NaN) // false
Boolean('') // false
```
注意: **所有对象(包括空对象)** 的布尔值都是 `true`
```js
Boolean({}) // true
Boolean([]) // true
Boolean(new Boolean(false)) // true    false的包装对象也是真
```

<a id="%E8%87%AA%E5%8A%A8%E8%BD%AC%E6%8D%A2"></a>
## 自动转换
`自动转换以强制转换为基础`,遇到以下三种情况时，JavaScript 会自动转换数据类型;
1.  不同类型的数据互相运算
```js
123 + 'abc'
```
2.  对非布尔类型的数据`求布尔值`
```js
if ('abc'){}
```
3.  对非数值类系的数据使用`一元运算符`
```js
- [1,2] // NaN
```

<a id="%E5%8F%82%E8%80%83"></a>
## 参考
[数据类型的转换 - JavaScript 教程 - 网道][]

[数据类型的转换 - JavaScript 教程 - 网道]:http://wangdoc.com/javascript/features/conversion.html
