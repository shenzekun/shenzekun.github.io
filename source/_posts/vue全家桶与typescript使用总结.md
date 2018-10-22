---
title: vue全家桶与typescript使用总结
date: 2018-03-01 11:38:31
tags: [vue,typescript]
categories: 前端
copyright: true
keywords: vue,vuex,vue-router,typescript
---

----

## 前言
> 最近重构了我之前项目 qq 音乐移动端，使用的技术是 vue，vuex，vue-router，和 typescript，在这期间，遇到的问题还是蛮多的，一会儿我会把我遇到的问题以及解决方法列出来，避免忘记。

<!--more-->

重构完成的项目 ===> [vue-qq-music](https://github.com/shenzekun/vue-qq-music)

TypeScript与Vue全家桶的配置可以参考以下两篇文章（在这里由衷感谢两位作者）：

1. [vue + typescript 新项目起手式](https://segmentfault.com/a/1190000011744210#articleHeader12)

2. [Vue2.5+ Typescript 引入全面指南 - Vuex篇](https://segmentfault.com/a/1190000011864013)

## TypeScript
为什么我要将`TypeScript` 和 `Vue` 集成呢？因为TypeScript 有以下几个优势：

* **可读性**。TypeScript 是 JavaScript 的超集，这意味着他支持所有的 JavaScript 语法。并在此之上对 JavaScript 添加了一些扩展，如interface等。这样会大大提升代码的可阅读性
*  **静态类型检查**。静态类型检查可以避免很多不必要的错误，不用在调试的时候才发现问题。
*  **代码提示**。ts 搭配 vscode，代码提示非常友好
*  **代码重构**。例如全项目更改某个变量名（也可以是类名、方法名，甚至是文件名[重命名文件自动修改的是整个项目的import]），在JS中是不可能的，而TS可以轻松做到。看看下面发生了什么神奇的事情😁⬇️
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-03-01-ts-chonggou.gif)

## 遇到的问题以及解决方法

### 问题一

ts 无法识别$ref

**解决方法**
① 直接在 this.$refs.xxx 后面申明类型如：

```javascript
this.$refs.lyricsLines as HTMLDivElement;
```
② 在`export default class xxx extends Vue`里面声明全部的$ref 的类型

```javascript
$refs: {
    audio: HTMLAudioElement,
    lyricsLines: HTMLDivElement
}
```

### 问题二

ts 无法识别 require

**解决方法**

安装声明文件

```bash
yarn add @types/webpack-env -D
```


### 问题三
运行`npm run build` 出现
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-03-01-044916.png)

**解决方法**
>You can fix this by **using the most recent beta version** of `uglifyjs-webpack-plugin`. Our team is working to remove completely the UglifyJsPlugin from within webpack, and instead have it as a standalone plugin.

>If you do `yarn add uglifyjs-webpack-plugin@beta --dev` or `npm install uglifyjs-webpack-plugin@beta --save-dev `you should receive the latest beta which does successfully minify es6 syntax. We are hoping to have this released from beta extremely soon, however it should save you from errors for now!

也就是说升级你的uglifyjs-webpack-plugin版本：
`yarn add uglifyjs-webpack-plugin@beta --dev`

### 问题四
[vue-property-decorator](https://github.com/kaorun343/vue-property-decorator) 装饰器写法不对。当时我是要把 mixins，注入到组件里，我就这样写：
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-03-01-052833.png)
ts提示找不到 mixin。我就很纳闷为什么找不到名字，由于官网vue-property-decorator例子太少，只好一步一步摸索😂

**解决方法**

把mixins写在@Component里面...，像这样：

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-03-01-053215.png)

## 注意点
1. 如果你引用第三方无类型声明的库，那就需要自己编写x.d.ts文件
2. 如果引用 ui 组件的时候，如果控制台出现`Property '$xxx' does not exist on type 'App'`的话，那么可以在`vue-shim.d.ts`增加

```
declare module 'vue/types/vue' {
  interface Vue {
    $xxx: any,
  }
}
```

## 最后
经过几天的折腾，终于把项目重构完成，我个人认为加上 `TypeScript`，确实效率挺高了许多，不过 `Vue+TypeScript` 还是没 `Angular`支持那么完善，相信之后 vue 对于 ts 的集成会更加完善！


