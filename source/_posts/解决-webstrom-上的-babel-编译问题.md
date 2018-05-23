---
title: 解决 webstrom 上的 babel 编译问题
date: 2017-12-05 07:13:15
tags: [工具,babel]
categories: 技巧
copyright: true
keywords: webstrom
---

----

## 前言

>近日，在写 ejs 文件时，我发现用 vscode 没有啥提示，因此换成 webStrom ，但是用 webStrom 将 es6 编译成 es5 的时候出现了一些问题😭，经过一番搜索， 最后终于成功解决，这里记录一下🖊

<!--more-->

## 方法

* 首先建立一个新的工程，点击**设置**

* 在设置里面，把JavaScript language version改成**ECMAScript 6**
![](http://upload-images.jianshu.io/upload_images/5308475-384e088e614a106c.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 然后在js文件里写一段ES6代码

* 现在IDE会出现一个`File watcher`提示条

* 此时先别点Add watcher！

* 在终端切换到项目的路径，输入以下命令

```
npm init -y //package.json
```

* 安装babel-cli

```
npm install --save-dev babel-cli
```

* 现在可以去点Add watcher，点完之后会弹出一个框

* 下面第三行，`Program` 那一项，填

```
$ProjectFileDir$/node_modules/.bin/babel
```

* 然后点OK，这个时候你就会发现左边多出来一个新文件

* 但是现在还没搞定！现在只是搞定了自动转换的功能，系统默认把ES6 编译成了ES6...

* 打开终端，输入：

```
npm install --save-dev babel-preset-es2015
```

* 再次打开设置，在搜索框输入`file watchers`，点击`babel`

* 在 Arguments 里面将 `env` 改为  `=es2015`,点击ok
![](http://upload-images.jianshu.io/upload_images/5308475-cd5fda1fb471aa6b.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 在根目录下新建一个`.babelrc`文件（就是babel在当前项目的配置文件），写上：

```
{
  "presets": [
    "es2015"
  ]
}
```

* 完成😁




