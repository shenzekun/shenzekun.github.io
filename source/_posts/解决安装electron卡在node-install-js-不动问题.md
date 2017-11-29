---
title: 解决安装electron卡在node install.js 不动问题
date: 2017-11-13 07:54:57
tags: 技巧
categories: 技巧
copyright: true
keywords: electron
---

----


>在安装electron的时候，一直卡在node install.js不动😭，翻了墙也不行，于是在 github 上搜索终于找到解决方法，为此记录下来📝

<!--more-->

## 说明

`install.js`,里面的下载是依赖于`electron-download`这个模块
![](http://upload-images.jianshu.io/upload_images/5308475-6a5758873a75a2c5.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

搜索[electron-download](https://github.com/electron-userland/electron-download)发现：👇

![](http://upload-images.jianshu.io/upload_images/5308475-0b73ee9483927679.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 解决方法

打开终端，输入`vi ~/.npmrc`,在里面添加

```
electron_mirror="https://npm.taobao.org/mirrors/electron/"
```

![](http://upload-images.jianshu.io/upload_images/5308475-433a4c62d776c545.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

再试一次`npm install electron -g`,这次就成功了😄



