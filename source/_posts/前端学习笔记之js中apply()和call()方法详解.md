---
title: 前端学习笔记之js中apply()和call()方法详解
date: 2017-04-15 11:34:14
tags: js
categories: 前端
copyright: true
---

>经过网上的大量搜索，渐渐明白了apply()和call方法的使用，为此写一篇文章记录一下。

<!--more -->

### **定义**


 - **apply()方法**：
    
   >Function.apply(obj,args)
obj：这个对象将代替Function类里this对象
args：这个是数组，它将作为参数传给Function(args-->arguments）

 -  **call()方法**：
 >Function.call(obj,[param1[,param2[,…[,paramN]]]])
obj：这个对象将代替Function类里this对象
params：这个是一个参数列表

---

### **相同点与不同点**

 1. **相同点**

	 作用是一样的，call 和 apply 都是为了改变函数体内部 this 的指向，也就是把Function(即this)绑定到obj，这时候obj具备了Function的属性和方法，说白一点就是obj继承了Function的属性和方法。
	 
 2. **不同点**
 
	 相信大家也已经发现了，他们唯一区别就是接受参数的方式不太一样，apply接受的是数组参数，call接受的是连续参数。

---

### **方法使用**

**我们来看下面一个例子：**

定义一个函数mul

```
function mul(a,b){
	return this+(a*b);
}
```

接着我们在控制台上打印出

```
console.log(mul.call(null,2,3));
console.log(mul.call('s',2,3));
console.log(mul.call(3,2,3));
console.log(mul.apply(null,[2,5]));
console.log(mul.apply(2,[2,5]));
```
分别为：
>[object Window]6
>s6
>9
>[object Window]10
>12

可能你会发现到，第一行 **console.log(mul.call(null,2,3))** 没什么变化，call()的第一个参数就是改变的 this 指向，如果为 null 则函数的 this 不变，注意，如果在严格模式下（函数体或全局的开头有这句话：'use strict'），this 会变成 null。如果函数本身有参数，则从 call 的第二个参数开始写起。
第二行 **console.log(mul.call('s',2,3))** 将函数的 this 指向一个字符串 's'.    ===>>  's'+2 \* 3=s6
第三行 **console.log(mul.call(3,2,3))**  将函数的this指向一个数字3   
     ===>>   3+2 \* 3=9
以此类推。

**再举一个例子**

学js的都知道 **Math.max()** 方法,比如有三个参数2,3,4那么我们要找出最大值可以这么写 **Math.max(2,3,4)** 那要是有 100 个或更多参数呢？这时候就可以结合 apply 和数组轻松实现了。

比如定义一个数组
> var arr=[2,3,4,5,6,7,8,9,10,23,45,66,22,11];

接着我们打印出
>console.log(Math.max.apply(null,arr));

这样一来就很简洁明了。


**再举一个例子实现对象继承**

```
function Person(name,age) {
	this.name=name;
	this.age=age;
}

var Student=function(name,age,gender) {
	Person.call(this,name,age);//this继承了person的属性和方法
	this.gender=gender;
}
var student=new Student("陈安东", 20, "男");
alert("姓名:"+student.name+"\n"+"年龄:"+student.age+"\n"+"性别:"+student.gender);
```
输出
>姓名:陈安东
年龄:20
性别:男

这样用call就实现了继承（用apply也类似）

