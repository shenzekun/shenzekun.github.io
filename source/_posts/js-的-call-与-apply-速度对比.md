---
title: js 的 call 与 apply 速度对比
date: 2017-10-20 12:37:57
tags: [前端,js]
categories: 前端
copyright: true
keywords: call,apply
---

----

>最近在看 underscore 的源码时发现，作者好多都用 call，而用 apply 比较少，比如说下面这段：👇

<!--more-->

```javascript
var optimizeCb = function(func, context, argCount) {
  // 如果没有指定 this 指向，则返回原函数
  if (context === void 0) return func;

  switch (argCount == null ? 3 : argCount) {
    case 1:
      return function(value) {
        return func.call(context, value);
      };
    case 2:
      return function(value, other) {
        return func.call(context, value, other);
      };

    // 如果有指定 this，但没有传入 argCount 参数
    // 则执行以下 case
    case 3:
      return function(value, index, collection) {
        return func.call(context, value, index, collection);
      };
    case 4:
      return function(accumulator, value, index, collection) {
        return func.call(context, accumulator, value, index, collection);
      };
  }
};
```
既然 call 和 apply 都能用，那为什么只用 call 而不用 apply 呢？
经过网上的搜索发现，**call 比 apply 速度快**，在 console运行如下代码：

```javascript
function x(a,b) {}
var a = [1, 2, 3];
console.time("call");
for (var i = 0; i < 1000000; i++) {
  x.call(this, 1, 2, 3);
}
console.timeEnd("call");

console.time("apply");
for (var j = 0; j < 1000000; j++) {
  x.apply(this, a);
}
console.timeEnd("apply");
```

console的结果：

![](http://upload-images.jianshu.io/upload_images/5308475-2f25092ecb658b17.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

可以发现 call 比 apply 快了10ms 左右，那是什么原因造成这样的呢？
**因为 apply 运行前要对作为参数的数组进行一系列检验和深拷贝，而 call 则没有**
我们看一下 ECMAScript 是怎么写的：

![](http://upload-images.jianshu.io/upload_images/5308475-40f7c9167b3a338d.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![](http://upload-images.jianshu.io/upload_images/5308475-93025d076479f624.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

由ECMAScript 标准发现 apply 比 call 的步骤多了好多，这就是 call 比 apply 执行速度快的原因！


