---
title: 解决Charles乱码问题
date: 2017-05-22 22:45:48
tags: 技巧
categories: 技巧
copyright: true
---

----

>在网上查了半天说在Info.plist文件加字符串就好了，其实没有用，下面有一个方法亲试可以解决乱码问题

<!--more-->

## 安装ssl证书
**3.10版本之前的**需要去[http://www.charlesproxy.com/ssl.zip](http://www.charlesproxy.com/ssl.zip) 下载 CA 证书文件，然后双击 .crt 文件，选择‘总是信任’按钮，在钥匙串访问中即可看到添加成功的证书。 

**我是4.02版本的，在3.10版本之后的**，操作如下：

* 先点**proxy**中的**macOS Proxy** ，如果点击网页，Charles没有出现东西的话，**把翻墙软件关了**
![](http://upload-images.jianshu.io/upload_images/5308475-a54d663becbba0de.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

*  然后点击**help**中的**SSL Proxying**如下图：
![](http://upload-images.jianshu.io/upload_images/5308475-23376f5b87f5cebc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 点击之后在搜索框中输入Charles，出现（我是已经改好了，原来的话是红色的）：
![](http://upload-images.jianshu.io/upload_images/5308475-61b1c3be4d7b83d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 双击那个证书，改成如下图所示，然后保存：
![](http://upload-images.jianshu.io/upload_images/5308475-c6844a5e46784c51.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

* 接下来点击**proxy**中的**SSL Proxying  Settings**，出现如下图所示，然后点**add** 在Host里填 * 号 ，在Port里填443，然后点ok：
![](http://upload-images.jianshu.io/upload_images/5308475-a79e27352086fa0c.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](http://upload-images.jianshu.io/upload_images/5308475-4ee2987c2d59d79d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



* 接下来，你会惊奇的发现，乱码没有了\（￣︶￣）/


