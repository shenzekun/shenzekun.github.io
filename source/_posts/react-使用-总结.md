---
title: react使用总结
date: 2017-10-02 15:34:31
tags: react
categories: 前端
copyright: true
keywords: react
---

----

>最近学了一些 react 和es6 的一些知识，并且使用 react 写了一个 TodoList 项目===>[预览](http://shenzekun.cn/R-Todo/build/index.html) && [源码](https://github.com/shenzekun/R-Todo) 感觉学的挺多的，并且遇到的坑也不少😂，说实话，一开始学 react 看到 jsx 语法有点不适应，说好的结构和行为分离呢😁，不过随着通过一个项目的完成，渐渐明白了这么写的好处


<!--more-->

### **好处**
* 自定义标签
* 结构清晰
* 代码模块化
* 更加语义化

### **不过也有缺点**
* 浏览器不支持这语法
* 必须通过一大堆工具来转换


### 一些需要注意的点

**1. react声明组件时，组件名称必须以大写字母开头如**👉：`<Todo />`
**2. 每个标签必须闭合,因为采用的 js+xml 写法，如**👉: `<input />`
**3. 组件的返回值只能有一个顶层元素，如**👇：

下面是错误的：

```javascript
render () {
  return (
    <div>1</div>
    <div>2</div>
  )
}
```

必须这样

```javascript
render () {
  return (
    <div>
        <div>1</div>
        <div>2</div>
    </div>
  )
}
```

**4.  return后面要加一个括号,目的是防止 JavaScript 代码在解析时自动在换行处添加分号**:


```javascript
 renderSquare(i) {
        return (
          <Todo />
        );
}    
```


**5. render()里面不能写 class,for,而是要写成`className`和`htmlFor`,因为 class ，for 是 javascript 的关键字，因此不能使用，如**：

下面是错误的

```
<div class=“xxx”>
```
而是要写 className：

```
<div className="xxx">
```

**6. 不要直接更新状态，如**

```javascript
 this.state.comment = 'Hello';
```
此代码**不会**重新渲染组件的，之前就这么写，啥反应也没有😂，应该要用`setState()`:👇

```javascript
 this.setState({comment: 'Hello'});
```

（**注意！！**：构造函数（constructor）是唯一能够初始化 this.state 的地方。）

**7. 使用`style`**

我们在 html 可以这么写：

```
<div style="background-color:red;"></div>
```

但是在 jsx 里面却不能这么写，必须用两个花括号包裹，并且里面不能写`-`，要用驼峰形式写，如上面的 `background-color`写成`backgroundColor`:

```
<div style={{backgroundColor: 'red'}}></div>
```

**8. 关于 setState**

setState方法用于更新当前组件的state状态值，但调用这个方法后，state并不会立即更新，而是在render方法调用后才会更新

### react 特点

1. **虚拟DOM**: React是以数据驱动的，每次数据变化React都会扫描整个虚拟DOM树，自动计算与上次虚拟DOM的差异变化，然后针对需要变化的部分进行实际的浏览器DOM更新。
2. **组件化：** React可以从功能角度划分，将UI分解成不同组件，各组件都独立封装，整个UI是由一个个小组件构成的一个大组件，每个组件只关系自身的逻辑，彼此独立（比如你有个按钮，很多页面都有这个按钮，那么就可以把这个按钮封装成该组件）。
3. **单项数据流**：React只有单向数据流动-从父节点传递到子节点

