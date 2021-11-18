---
title: Arrary 对象操作
date: 2021-11-09
author: Samuel
img: 
top: true
hide: false
cover: true
coverImg: 
password: 
toc: true
mathjax: false
summary: 常用的数组对象操作
categories: JavaScript
tags:
  - JavaScript
---
<!-- ## All -->
### Is Arrary
var a = [];

// 1.基于instanceof

a instanceof Array; // true

// 2.基于constructor

a.constructor === Array;  //true

// 3.基于Object.prototype.isPrototypeOf

Array.prototype.isPrototypeOf(a);

// 4.基于getPrototypeOf

Object.getPrototypeOf(a) === Array.prototype;

// 5.基于Object.prototype.toString

Object.prototype.toString.apply(a) === '[object Array]';

//以上，除了Object.prototype.toString外，其它方法都不能正确判断变量的类型。

最好的方式：

```js
Array.isArray([]); // true
Array.isArray({0: 'a', length: 1}); // false
```

### 深拷贝
深拷贝：
```js
let arr = [ ];

let newArr = JSON.parse(JSON.stringify(arr))
```
不改变原数组

### 浅拷贝
浅拷贝：
```js
let arr = [ ];
let newArr = arr;
```
改变原数组

### Array 构造器
Array 构造器

```js
// 使用Array构造器
var a = Array(8) // [undefined x 8]
// 使用对象字面量
var a =[ ] ;
a.length = 8; // [undefined x 8]
```

ES6 新增构造函数：

Array.of将参数依次转化为数组中的一项，然后返回新数组

```js
//单个数字参数处理与Array不同
Array.of(8.0); // [8]
Array(8.0); // [empty × 8]
//单个参数不是数字时，Array.of 与 Array构造器等同
Array.of(8.0, 5); // [8, 5]
Array(8.0, 5); // [8, 5]
Array.of('8'); // ["8"]
Array('8'); // ["8"]

```

**Array.from** 从一个类似数组的可迭代对象创建一个新的数组实例

```js
语法：Array.from(arrayLike[,processingFn[,thisArg]])
```

