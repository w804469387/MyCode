---
title: ECMAScript的成长史 #标题
date: 2021-11-17 #创作日期
author: Samuel #作者
img: https://samuel-1308214755.cos.ap-shanghai.myqcloud.com/img/ECMAScript.jpg #背景图
top: true
hide: false
cover: true
coverImg:
password:
toc: false #目录
mathjax: false
summary: xxx #子标题
categories: JavaScript #分类
tags: #标签
  - JavaScript
  - ECMAScript
---

#### 来聊一聊 ECMAScript 的发展过程

> 这是发展的过程

![ECMASCRIPT](https://samuel-1308214755.cos.ap-shanghai.myqcloud.com/img/ecma1.jpg)

### ECMAScript 2015(ES6)

1. let 和 const
   > ES2015(ES6) 新增加了两个重要的 JavaScript 关键字: let 和 const。
   > let 声明的变量只在 let 命令所在的代码块内有效。
   > const 声明一个只读的常量，一旦声明，常量的值就不能改变。
   > 在 ES6 之前，JavaScript 只有两种作用域： **_ 全局变量 _** 与 函数内的 **_ 局部变量 _**。

##### 全局变量

在函数外声明的变量作用域是全局的：

```js
var myName = "Samuel";

// 这里可以使用 myName 变量

function myFunction() {
  // 这里也可以使用 myName 变量
  console.log("My Name is" + myName);
}
```

##### 局部变量

在函数内声明的变量作用域是局部的（函数内）：

```js
// 这里不能使用 myName 变量

function myFunction() {
  var myName = "Samuel";
  // 这里可以使用 myName 变量
}

// 这里不能使用 myName 变量
```

- 在 javascript 中有三种声明变量的方式：var、let、const。
  > _var_
  > var 声明全局变量，换句话理解就是，声明在 for 循环中的变量，跳出 for 循环同样可以使用。
  > var 定义的变量可以修改，如果不初始化会输出 undefined，不会报错。

> _let_
> 同一个变量，不可在声明之前调用，必须先定义再使用，否则会报错，循环体中可以用 let
> let 是块级作用域，函数内部使用 let 定义后，对函数外部无影响。

> _const_
> const：用于声明常量，也具有块级作用域 ，也可声明块级。const 定义的变量不可以修改，而且必须初始化。
> 也就是说一但声明了 const 就必须初始化，不能等到以后在赋值

2. 类（class）

> ES6 提供了更接近传统语言的写法，引入了 Class（类）这个概念，作为对象的模板。通过 class 关键字，可以定义类。
> 基本上，ES6 的 class 可以看作只是一个语法糖，它的绝大部分功能，ES5 都可以做到，新的 class 写法只是让对象原型的写法更加清晰、更像面向对象编程的语法而已。

```js
function Point(x, y) {
  this.x = x;
  this.y = y;
}

Point.prototype.toString = function () {
  return "(" + this.x + ", " + this.y + ")";
};

var p = new Point(1, 2);

//下面这个代码就是用 ES6 的class改写
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return "(" + this.x + ", " + this.y + ")";
  }
}
```

#### ES6 的类，完全可以看作构造函数的另一种写法。

3. 模块化(ES Module)
   > ES6 模块的设计思想是尽量的静态化，使得编译时就能确定模块的依赖关系，以及输入和输出的变量。CommonJS 和 AMD 模块，都只能在运行时确定这些东西。比如，CommonJS 模块就是对象，输入时必须查找对象属性。

```js
// CommonJS模块
let { stat, exists, readfile } = require("fs");

// 等同于
let _fs = require("fs");
let stat = _fs.stat;
let exists = _fs.exists;
let readfile = _fs.readfile;
```

ES6 模块不是对象，而是通过 export 命令显式指定输出的代码，再通过 import 命令输入;

```js
// ES6模块
import { stat, exists, readFile } from "fs";
```

上面代码的实质是从 fs 模块加载 3 个方法，其他方法不加载。这种加载称为“编译时加载”或者静态加载，即 ES6 可以在编译时就完成模块加载
由于 ES6 模块是编译时加载，使得静态分析成为可能。有了它，就能进一步拓宽 JavaScript 的语法

4. 箭头（Arrow）函数
   > 箭头函数的出现很大方面解决的 this 指向的问题，在以往的函数作用域内所用到的 this，指向的实际上是 window 的全局对象而在剪头函数内所指向的就是作用域内自己的对象；

例子：

```js
var obj = {
  like: "Vscode",
  myLike: function () {
    var myLike = this.like; // Vscode
    var fn = function () {
      return "I like:" + this.like; // this指向window或undefined
    };
    return fn();
  },
};
obj.myLike(); // I like: undefined
```

```js
var obj = {
  like: "Vscode",
  myLike: function () {
    var myLike = this.like; // Vscode
    var fn = () => {
      return "I like:" + this.like; // this指向window或undefined
    };
    return fn();
  },
};
obj.myLike(); // I like:Vscode
```

5. 函数参数默认值

```js
const fun =(a,b)=>{
    console.log('a:'a,'b:',b)
};
const fun1 =(a=1,b=2)=>{
    console.log('a:'a,'b:',b)
};

fun();  // a:undefind b:undefind
fun()1; // a:1,b:2
```

6. 模板字符串
   > 传统的 JavaScript 语言，输出模板通常是这样写的（下面使用了 jQuery 的方法）

```js
$("#result").append(
  "There are <b>" +
    basket.count +
    "</b> " +
    "items in your basket, " +
    "<em>" +
    basket.onSale +
    "</em> are on sale!"
);
```

> 上面这种写法相当繁琐不方便，ES6 引入了模板字符串解决这个问题。

```js
$("#result").append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```

> 模板字符串（template string）是增强版的字符串，用反引号（`）标识。它可以当作普通字符串使用，也可以用来定义多行字符串，或者在字符串中嵌入变量。

```js
// 普通字符串
`In JavaScript '\n' is a line-feed.` // 多行字符串
`In JavaScript this is
 not legal.`;

console.log(`string text line 1
string text line 2`);

// 字符串中嵌入变量
let name = "Bob",
  time = "today";
`Hello ${name}, how are you ${time}?`;
```

7. 解构赋值
   > ES6 允许按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构

以前，为变量赋值，只能直接指定值

```js
let a = 1;
let b = 2;
let c = 3;
```

ES6 允许写成下面这样。

```js
let [a, b, c] = [1, 2, 3];
```

> 本质上，这种写法属于“模式匹配”，只要等号两边的模式相同，左边的变量就会被赋予对应的值。

```js
let [foo, [[bar], baz]] = [1, [[2], 3]];
foo; // 1
bar; // 2
baz; // 3

let [, , third] = ["foo", "bar", "baz"];
third; // "baz"

let [x, , y] = [1, 2, 3];
x; // 1
y; // 3

let [head, ...tail] = [1, 2, 3, 4];
head; // 1
tail; // [2, 3, 4]

let [x, y, ...z] = ["a"];
x; // "a"
y; // undefined
z; // []
```

如果解构不成功，变量的值就等于 undefined。

```js
let [foo] = [];
let [bar, foo] = [1];
```

以上两种情况都属于解构不成功，foo 的值都会等于 undefined。

8. 延展操作符 ...
   > 扩展运算符（spread）是三个点（...）。它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列。

```js
console.log(...[1, 2, 3])
// 1 2 3

console.log(1, ...[2, 3, 4], 5)
// 1 2 3 4 5

[...document.querySelectorAll('div')]
// [<div>, <div>, <div>]
```

该运算符主要用于函数调用。

```js
function push(array, ...items) {
  array.push(...items);
}

function add(x, y) {
  return x + y;
}

const numbers = [4, 38];
add(...numbers); // 42
```

> 上面代码中，array.push(...items)和 add(...numbers)这两行，都是函数的调用，它们都使用了扩展运算符。该运算符将一个数组，变为参数序列。

9. 对象属性简写
   > ES6 允许在大括号里面，直接写入变量和函数，作为对象的属性和方法。这样的书写更加简洁。

```js
const foo = "bar";
const baz = { foo };
baz; // {foo: "bar"}

// 等同于
const baz = { foo: foo };
```

上面代码中，变量 foo 直接写在大括号里面。这时，属性名就是变量名, 属性值就是变量值。下面是另一个例子。

```js
function f(x, y) {
  return { x, y };
}

// 等同于

function f(x, y) {
  return { x: x, y: y };
}

f(1, 2); // Object {x: 1, y: 2}
```

_实际的例子_

```js
let birth = "2000/01/01";

const Person = {
  name: "张三",

  //等同于birth: birth
  birth,

  // 等同于hello: function ()...
  hello() {
    console.log("我的名字是", this.name);
  },
};
```

这种写法用于函数的返回值，将会非常方便。

```js
function getPoint() {
  const x = 1;
  const y = 10;
  return { x, y };
}

getPoint();
// {x:1, y:10}
```

10. Promise
    > Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了 Promise 对象。
    > [Promise](http://47.102.144.56:4000/2021/11/10/Promise/)

### ECMAScript 2016(ES7)

1. Array.prototype.includes();
   includes 的加入无疑让 js 的写法更加方便了
   来看看对比

```js
function fun(a) {
  if (a == "1" || a == "2" || a == "3") {
    return a;
  } else {
    return null;
  }
}

function fun1(a) {
  if (["1", "2", "3"].includes(a)) {
    return a;
  } else {
    return null;
  }
}

// includes 直接返回true或false
```

2. 指数操作符 \*\*
   > 这个运算符的一个特点是右结合，而不是常见的左结合。多个指数运算符连用时，是从最右边开始计算的

```js
2 ** 2; // 4
2 ** 3; // 8

// 相当于 2 ** (3 ** 2)
2 ** (3 ** 2);
// 512
```

上面代码中，首先计算的是第二个指数运算符，而不是第一个。

指数运算符可以与等号结合，形成一个新的赋值运算符（\*\*=）。

```js
let a = 1.5;
a **= 2;
// 等同于 a = a * a;

let b = 4;
b **= 3;
// 等同于 b = b * b * b;
```

### ECMAScript 2017(ES8)

1. async/await: 异步终极解决方案;
   > async 函数返回一个 Promise 对象，可以使用 then 方法添加回调函数。当函数执行的时候，一旦遇到 await 就会先返回，等到异步操作完成，再接着执行函数体内后面的语句。

```js
function timeout(ms) {
  return new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value);
}

asyncPrint("hello world", 50);

// 50毫秒后输出 hello word
```

由于 async 函数返回的是 Promise 对象，可以作为 await 命令的参数。所以，上面的例子也可以写成下面的形式

```js
async function timeout(ms) {
  await new Promise((resolve) => {
    setTimeout(resolve, ms);
  });
}

async function asyncPrint(value, ms) {
  await timeout(ms);
  console.log(value);
}

asyncPrint("hello world", 50);
```

async 函数有多种写法

```js
// 函数声明
async function foo() {}

// 函数表达式
const foo = async function () {};

// 对象的方法
let obj = { async foo() {} };
obj.foo().then(...)

// Class 的方法
class Storage {
  constructor() {
    this.cachePromise = caches.open('avatars');
  }

  async getAvatar(name) {
    const cache = await this.cachePromise;
    return cache.match(`/avatars/${name}.jpg`);
  }
}

const storage = new Storage();
storage.getAvatar('jake').then(…);

// 箭头函数
const foo = async () => {};
```

_async 函数返回一个 Promise 对象_

_async 函数内部 return 语句返回的值，会成为 then 方法回调函数的参数。_

```js
async function f() {
  return "hello world";
}

f().then((v) => console.log(v));
// "hello world"
```

2. Object.values();
   > Object.values 方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值。

```js
const obj = { foo: "bar", baz: 42 };
Object.values(obj);
// ["bar", 42]

const obj = { 100: "a", 2: "b", 7: "c" };
Object.values(obj);
// ["b", "c", "a"]
```

上面代码中，属性名为数值的属性，是按照数值大小，从小到大遍历的，因此返回的顺序是 b、c、a。
Object.values 只返回对象自身的可遍历属性。

```js
const obj = Object.create({}, { p: { value: 42 } });
Object.values(obj); // []
```

3. Object.entries();
   > Object.entries()方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组。

```js
const obj = { foo: "bar", baz: 42 };
Object.entries(obj);
// [ ["foo", "bar"], ["baz", 42] ]
```

除了返回值不一样，该方法的行为与 Object.values 基本一致。

如果原对象的属性名是一个 Symbol 值，该属性会被忽略。

```js
Object.entries({ [Symbol()]: 123, foo: "abc" });
// [ [ 'foo', 'abc' ] ]
```

*Object.entries*的基本用途是遍历对象的属性。

```js
let obj = { one: 1, two: 2 };
for (let [k, v] of Object.entries(obj)) {
  console.log(`${JSON.stringify(k)}: ${JSON.stringify(v)}`);
}
// "one": 1
// "two": 2
```

*Object.entries*方法的另一个用处是，将对象转为真正的 Map 结构。

```js
const obj = { foo: "bar", baz: 42 };
const map = new Map(Object.entries(obj));
map; // Map { foo: "bar", baz: 42 }
```
### ECMAScript 2018(ES9)
1. 异步迭代：await可以和for...of循环一起使用，以串行的方式运行异步操作
```js
async function f() {
  for await (const x of createAsyncIterable(['a', 'b'])) {
    console.log(x);
  }
}
// a
// b
```
上面代码中，createAsyncIterable()返回一个拥有异步遍历器接口的对象，for...of循环自动调用这个对象的异步遍历器的next方法，会得到一个 Promise 对象。await用来处理这个 Promise 对象，一旦resolve，就把得到的值（x）传入for...of的循环体。

for await...of循环的一个用途，是部署了 asyncIterable 操作的异步接口，可以直接放入这个循环.\;

### ECMAScript 2019(ES10)
1. Array.flat()和Array.flatMap()：数组展平
2. String.trimStart()和String.trimEnd()：去掉开头结尾空格文本
3. JSON.stringify() 加强格式转化

### ECMAScript 2020(ES11)
1. 动态 import ()：按需导入
2. 空值合并运算符：表达式在 ?? 的左侧 运算符求值为undefined或null，返回其右侧
3. 可选链接：?.用户检测不确定的中间节点

### ECMAScript 2021 (ES12)
1. String.prototype.replaceAll ：有了这个 API，替换字符不用写正则了
2. 新增逻辑赋值操作符： ??=、&&=、 ||=
3. 下划线 (_) 分隔符：使用 _ 分隔数字字面量以方便阅读

 - - - 

 先到这里