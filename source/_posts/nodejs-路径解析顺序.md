---
title: nodejs 路径解析顺序
date: 2018-06-04 19:48:58
tags: node
categories: 前端
copyright: true
keywords: nodejs
---

----

## 前言
> 平时在使用 nodejs 去 require 的时候是不是有使用绝对路径或者相对路径去引用，那么 nodejs 解析路径顺序是怎么样的呢？接下来我会讲一下 nodejs 路径解析顺序

<!--more-->

## 相对路径解析顺序

假设有一个文件路径为 `/root/src/moduleA.js`，包含了一个导入`var x = require("./moduleB");`, 也就是导入了一个相对路径的一个模块，那么Node.js以下面的顺序解析这个导入：

* 到`/root/src/moduleB.js`这个路径是否存在，如果不存在进入下一步。
* 检查`/root/src/moduleB` 目录是否包含一个`package.json`文件，且`package.json`文件指定了一个"main"模块,比如 ，Node.js发现文件 `/root/src/moduleB/package.json` 包含了 `{ "main": "lib/mainModule.js" }`,那么 nodejs 就会去 `/root/src/moduleB/lib/mainModule.js`
* 如果没有 main 字段,nodejs会检查`/root/src/moduleB`目录是否包含一个 `index.js` 文件。 这个文件会被隐式地当作那个文件夹下的"main"模块。

## 绝对路径解析顺序

假设有一个文件路径为`/root/src/moduleA.js`，里面包含了一个导入`var x = require("moduleB");`，也就是绝对路径的一个模块，那么Node.js以下面的顺序解析这个导入：

* `/root/src/node_modules/moduleB.js`
* `/root/src/node_modules/moduleB/package.json`（里面指定了 main 字段，跟上面相对路径是一样的）
* `/root/src/node_modules/moduleB/index.js`
如果上面三个没有找到，往**上一级**目录找：
* `/root/node_modules/moduleB.js`
* `/root/node_modules/moduleB/package.json`
* `/root/node_modules/moduleB/index.js`
如果还没有找到，继续往**上一级**找：
* `/node_modules/moduleB.js`
* `/node_modules/moduleB/package.json`
* `/node_modules/moduleB/index.js`


