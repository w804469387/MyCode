---
title: Promise
date: 2021-11-10
author: Samuel
img:
top: true
hide: false
cover: true
coverImg:
password:
toc: true
mathjax: false
summary:
categories: JavaScript
tags:
  - JavaScript
  - ES6
---

### 什么是 Promise？

Promise 是异步编程的一种解决方案，比传统的解决方案——回调函数和事件——更合理和更强大。
它由社区最早提出和实现，ES6 将其写进了语言标准，统一了用法，原生提供了 Promise 对象。
所谓 Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。
从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。
Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

### Promise 有什么优点？

1. 对象的状态不受外界影响。
   Promise 对象代表一个异步操作，有三种状态：
   pending（进行中）、fulfilled（已成功）和 rejected（已失败）。
   只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态。
   这也是 Promise 这个名字的由来，它的英语意思就是“承诺”，表示其他手段无法改变。

2. 一旦状态改变，就不会再变，任何时候都可以得到这个结果。
   Promise 对象的状态改变，只有两种可能：从 pending 变为 fulfilled 和从 pending 变为 rejected。
   只要这两种情况发生，状态就凝固了，不会再变了，会一直保持这个结果，这时就称为 resolved（已定型）。
   如果改变已经发生了，你再对 Promise 对象添加回调函数，也会立即得到这个结果。
   这与事件（Event）完全不同，事件的特点是，如果你错过了它，再去监听，是得不到结果的。

### Promise 有什么缺点？

- 首先，无法取消 Promise，一旦新建它就会立即执行，无法中途取消。
- 如果不设置回调函数，Promise 内部抛出的错误，不会反应到外部。
- 当处于 pending 状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）

### Promise 怎么用？

废话不多说直接上代码

```js
const data = new Promise((resolve,reject)=>{
    if(/*判断符合你的正确条件*/){
        // 成功的返回
        resolve()
    }else{
        //失败的返回
        reject()
    }
})
```

上面我们说了 Promise 有三种状态，pending（进行中）、fulfilled（已成功）和 rejected（已失败）。
就是说 你的方法一但被调用那么 promise 内当前的状态就是 pending（进行中），
resolve() 和 reject()
如果没有这两个方法，那么这个 Promise 就会一直处于 pending 的状态不会返回
**注意:这俩对象必须返回一个**

<b>resolve</b>的作用就是把当前的 Promise 内的状态从 pending 改为 fulfilled(进行中->已成功),在异步操作成功时调用，并将异步操作的结果，作为参数传递出去;

<b>reject</b>的作用就是把当前的 Promise 内的状态从 pending 改为 rejected(进行中->已失败,在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

#### 当 Promise 对象生成后我们可以获得成功或者失败的结果

```js
data.then((result)=>{
    //返回成功的结果
    // result就是resolve传递的参数
}).catch((err))=>{
    // 同理 err就是reject传递的错误信息
})
```

###### Promise 新建后就会立即执行

比如：

```js
const newPromise = new Promise((resolve, reject) => {
  console.log("柳暗花明又一村");
  resolve("My name is Promise");
});
newPromise.then((data) => {
  console.log(data);
});
console.log("Hello word");
```

他们输出的结果是什么呢？

```js
//柳暗花明又一村
// Hello word
// My name is Promise
```

跟你心中的答案一样吗？

上面代码中，Promise 新建后立即执行，所以首先输出的是'柳暗花明又一村'。
然后，then 方法指定的回调函数，将在当前脚本所有同步任务执行完才会执行，所以 resolved 最后输出。

### Promise 对 Ajax 的封装

```js
function getJson(url) {
  return new Promise((resolce, reject) => {
    const handler = function () {
      if (this.readyState !== 4) {
        return;
      }
      if (this.status === 200) {
        resolve(this.response);
      } else {
        reject(new Error(this.statusText));
      }
    };
    const client = new XMLHttpRequest();
    client.open("GET", url);
    client.onreadystatechange = handler;
    client.responseType = "json";
    client.setRequestHeader("Accept", "application/json");
    client.send();
  });
}
getJson("/getjson")
  .then((json) => {
    console.log("获得的数据是：" + json);
  })
  .catch((err) => {
    console.log("getJson出错了：" + err);
  });
```
上面代码中，getJSON是对 XMLHttpRequest 对象的封装，
用于发出一个针对 JSON 数据的 HTTP 请求，并且返回一个Promise对象。

### 如果有多个Promise对象怎么办？

这个时候可以用到Promise.all();
Promise.all()方法用于将多个 Promise 实例，包装成一个新的 Promise 实例
```js
const ps = Promise.all([a,b,c]);
```
上面数组中传入的都是Promise对象,
这里ps的状态会受到a，b，c三个对象的影响，如果a,b,c三个都返回了fulfilled(成功的)
ps为成功，接收的是一个数组类型的值，由a,b,c三个返回值组成。
如果三个对象中有一个返回了rejected,会直接返回，
此时ps接收的为第一个返回rejected的值；


- - -
- - - 

先更到这里




内容参考[阮一峰ES6入门](https://es6.ruanyifeng.com/)

