---
title: github博客绑定个性域名
date: 2017-05-22 22:41:34
tags: 技巧
categories: 技巧
copyright: true
---

-----

首先我们先买个域名,可以在[阿里云](https://cn.aliyun.com/)购买域名，买完之后登陆阿里云的管理控制台,然后点击域名，再点击解析如下

<!--more-->

![](http://upload-images.jianshu.io/upload_images/5308475-4953432e1dae183e.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接下来点击添加解析，并输入以下信息（记录值不一样，第一个的记录值填你的github访问地址,如`shenzekun.github.io`,第二个填的是你的网站的ip地址，比如我原来的网站是`shenzekun.github.io`,那么就查找`shenzekun.github.io`的ip地址，网站的ip地址可以在这查[ip地址](http://ip.chinaz.com/)）

![](http://upload-images.jianshu.io/upload_images/5308475-8b27bab6a8c389d2.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


然后向你的 Github Pages 仓库添加一个CNAME(一定要*大写*)文件，在CNAME里面添加你的域名信息（`不加http://`），如`shenzekun.cn`,并上传到你的GitHub中

填完之后登陆你博客的github，点击setting
![](http://upload-images.jianshu.io/upload_images/5308475-d73094344c7c7f6f.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
在这填写你的域名，点击保存即可

![](http://upload-images.jianshu.io/upload_images/5308475-86c99fdf87c8fef8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接下来就是等了，我的博客大概半个小时就可以看到了。😝

---

