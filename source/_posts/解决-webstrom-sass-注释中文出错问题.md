---
title: 解决 webstrom sass 注释中文出错问题
date: 2017-09-27 07:28:12
tags: [css,工具]
categories: 前端
copyright: true
keywords: webstrom sass
---

----

>最近用 webStrom 写 sass，感觉非常好用，自动帮你编译好，但是有一个问题，就是在写中文注释的时候，就会出错

<!--more-->

如下：
![](http://upload-images.jianshu.io/upload_images/5308475-95a3cfb869f7aa79.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

网上查了一下，说在 scss 文件头部加上：

```
@charset "utf-8";
```

但是，我试了一下并不管用！！😂

经过一番查找终于找到方法，在这里记录一下：

① 在 scss 文件的头部加上：

```
@charset "utf-8";
```

② 打开`/Library/Ruby/Gems/2.0.0/gems/sass-3.4.22/lib/sass/engine.rb`(mac)

在 require 后面加上：

```
Encoding.default_external = Encoding.find('utf-8')
```

如下：

![](http://upload-images.jianshu.io/upload_images/5308475-26193cd4cb4b4746.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

现在就可以支持中文注释了😀


