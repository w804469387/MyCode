---
title: 单行Javascript语句 #标题
date: 2021-11-12 #创作日期
author: Samuel #作者
img: #背景图
top: true
hide: false
cover: true
coverImg:
password:
toc: true  #目录
mathjax: false
summary: 收藏关于JavaScript一句话实现功能的语句 #子标题
categories: JavaScript #分类
tags: #标签
  - JavaScript
  - ECMAScript
---


### 获取浏览器Cookie的值
> 通过使用document.cookie访问来检索cookie的值。

```js
const cookie = name => `; ${document.cookie}`.split(`; ${name}=`).pop().split(';').shift();

cookie('_ga');
// Result: "GA1.2.1929736587.1601974046"
```

### 将RGB转换为十六进制

```js
const rgbToHex = (r, g, b) =>
  "#" + ((1 << 24) + (r << 16) + (g << 8) + b).toString(16).slice(1);

rgbToHex(0, 51, 255); 
// Result: #0033ff
```

### 复制到剪贴板
> 使用navigator.clipboard.writeText可以轻松将文本复制到剪贴板。

```js
const copyToClipboard = (text) => navigator.clipboard.writeText(text);

copyToClipboard("Hello World");
```

### 检查日期是否有效
> 使用以下代码段检查给定日期是否有效。

```js
const isDateValid = (...val) => !Number.isNaN(new Date(...val).valueOf());

isDateValid("December 17, 1995 03:24:00");
// Result: true
```

### 查找一年中的某一天
> 查找给定日期。

```js
const dayOfYear = (date) =>
  Math.floor((date - new Date(date.getFullYear(), 0, 0)) / 1000 / 60 / 60 / 24);

dayOfYear(new Date());
// Result: 272
```

### 大写字符串
> Javascript没有内置的大写函数，但是我们可以使用以下代码实现大写。

```js
const capitalize = str => str.charAt(0).toUpperCase() + str.slice(1)

capitalize("follow for more")
// Result: Follow for more
```

### 查找两个日期之间的天数
> 使用以下代码段查找给定两个日期之间的天数。

```js
const dayDif = (date1, date2) => Math.ceil(Math.abs(date1.getTime() - date2.getTime()) / 86400000)

dayDif(new Date("2020-10-21"), new Date("2021-10-22"))
// Result: 366
```

### 清除所有Cookie
> 你可以通过使用document.cookie访问cookie并清除它，从而轻松地清除存储在网页中的所有cookie。

```js
const clearCookies = document.cookie.split(';').forEach(cookie => document.cookie = cookie.replace(/^ +/, '').replace(/=.*/, `=;expires=${new Date(0).toUTCString()};path=/`));
```

### 生成随机十六进制
> 你可以使用Math.random和padEnd属性生成随机的十六进制颜色。

```js
const randomHex = () => `#${Math.floor(Math.random() * 0xffffff).toString(16).padEnd(6, "0")}`;

console.log(randomHex());
// Result: #92b008
```

### 从数组中删除重复项
> 你可以使用JavaScript中的Set轻松删除重复项。这是救命稻草。

```js
const removeDuplicates = (arr) => [...new Set(arr)];

console.log(removeDuplicates([1, 2, 3, 3, 4, 4, 5, 5, 6]));
// Result: [ 1, 2, 3, 4, 5, 6 ]
```

### 从URL获取查询参数
> 你可以通过传递window.location或原始URLgoole.com?search=easy&page=3从url轻松检索查询参数。

```js
const getParameters = (URL) => {
  URL = JSON.parse('{"' + decodeURI(URL.split("?")[1]).replace(/"/g, '\\"').replace(/&/g, '","').replace(/=/g, '":"') +'"}');
  return JSON.stringify(URL);
};
```

### 从日期输出时间
> 我们可以从给定日期以hour::minutes::seconds的格式输出时间

```js
const timeFromDate = date => date.toTimeString().slice(0, 8);

console.log(timeFromDate(new Date(2021, 0, 10, 17, 30, 0))); 
// Result: "17:30:00"
```

### 检查数字是偶数还是奇数

```js
const isEven = num => num % 2 === 0;

console.log(isEven(2)); 
// Result: True
```

### 求数字的平均值
> 使用reduce方法查找多个数字的平均值。

```js
const average = (...args) => args.reduce((a, b) => a + b) / args.length;

average(1, 2, 3, 4);
// Result: 2.5
```

### 滚动到顶部
> 你可以使用window.scrollTo(0, 0)方法自动滚动到顶部。将x和y都设置为0

```js
const goToTop = () => window.scrollTo(0, 0);

goToTop();
```

### 反转字符串
> 你可以使用split、reverse和join方法轻松反转字符串。

```js
const reverse = str => str.split('').reverse().join('');

reverse('hello world');     
// Result: 'dlrow olleh'
```

### 检查数组是否为空
> 只要简简单单的一行代码就可以检查数组是否为空，返回true或false。


```js
const isNotEmpty = arr => Array.isArray(arr) && arr.length > 0;

isNotEmpty([1, 2, 3]);
// Result: true
```

### 获取选定的文本
> 使用内置的getSelection属性获取用户选择的文本。

```js
const getSelectedText = () => window.getSelection().toString();

getSelectedText();
```

### 打乱数组
> 使用sort和random方法打乱数组非常容易。


```js
const shuffleArray = (arr) => arr.sort(() => 0.5 - Math.random());

console.log(shuffleArray([1, 2, 3, 4]));
// Result: [ 1, 4, 3, 2 ]
```


- - - 
 以上只是个人理解
- - - 


