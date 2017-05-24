---
title: 前端小项目：使用canvas绘画哆啦A梦
date: 2017-05-22 22:53:53
tags: canvas
categories: 前端
copyright: true
---

----

> 最近在学canvas元素,`<canvas>`标签只是图形容器，必须使用js来绘制图形。为了增强对canvas元素的理解,于是用canvas画了一个哆啦A梦来

<!--more-->

**要实现的效果图**


![哆啦A梦](http://upload-images.jianshu.io/upload_images/5308475-24ab4e6cda048199.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)



> [在线预览](https://shenzekun.github.io/doraemon/Doraemon.html)


要想绘画出这个哆啦a梦首先要掌握以下一些函数：
- [arcTo()](http://www.365mini.com/page/html5-canvas-arcto.htm)
- [canvas绘制圆形或弧线](http://www.365mini.com/page/html5-canvas-circle.htm)
- [bezierCurveTo()](http://www.w3school.com.cn/tags/canvas_beziercurveto.asp)
- [quadraticCurveTo() ](http://www.w3school.com.cn/tags/canvas_quadraticcurveto.asp)

开始绘画！！

首先我们需要创建一个400*600的画布，代码如下:
```
 <canvas id="doraemon" width="400" height="600"></canvas>
```
接着定义一个div，用来显示坐标
```
<div id="put" style="width: 50px" height="20px"></div>
```
接着我写了一个显示坐标的函数，可以用来看大概画到哪个点：
```
function zuobiao(event) {
        var x = event.clientX;
        var y = event.clientY;
        var out = document.getElementById("put");
        out.innerHTML = "x:" + x + " y:" + y;
    }
```
然后getContext() 方法返回一个用于在画布上绘图的环境。
```
var cxt = document.getElementById('doraemon').getContext('2d');
```
接着开始画头部:
```
        cxt.beginPath();//起始路径
        cxt.lineWidth = 1;//线宽度为1
        cxt.strokeStyle = '#000';//笔触的颜色
        cxt.arc(200, 175, 175, 0.7 * Math.PI, 0.3 * Math.PI);//绘制弧，中心点（200，175），半径175
        cxt.fillStyle = '#0bb0da';//设置填充时的颜色
        cxt.fill();//填充颜色
        cxt.stroke();//绘制路径
```
头部如下：


![头部](http://upload-images.jianshu.io/upload_images/5308475-14f0c90711c3b8d9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


接着绘画出脸部：
```
        cxt.beginPath();
        cxt.fillStyle = '#fff';
        cxt.moveTo(110, 110);//将路径移到点（110，110），不创建线条
        cxt.quadraticCurveTo(-10, 200, 120, 315);//创建二次贝塞尔曲线,控制点(-10,200),结束点(120,315)
        cxt.lineTo(280, 315);//添加一个新点，然后在画布中创建从（110，110）到（280，315）的线条
        cxt.quadraticCurveTo(410, 210, 290, 110);
        cxt.lineTo(110, 110);
        cxt.fill();
        cxt.stroke();
```
脸部如下：
![脸部](http://upload-images.jianshu.io/upload_images/5308475-3b275a0c5b472130.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接着绘画眼睛：
```
        cxt.beginPath();
        cxt.lineWidth = 1;
        cxt.fillStyle = '#fff';
        cxt.moveTo(110, 110);
        cxt.bezierCurveTo(110, 25, 200, 25, 200, 100);//创建三次贝塞尔曲线,控制点1(110,25),控制点2(200,25),结束点(200,100)，也就是画左上半椭圆
        cxt.bezierCurveTo(200, 175, 110, 175, 110, 100);//画左下半椭圆
        cxt.moveTo(200, 100);
        cxt.bezierCurveTo(200, 25, 290, 25, 290, 100);
        cxt.bezierCurveTo(290, 175, 200, 175, 200, 100);
        cxt.fill();
        cxt.stroke();

```

![眼睛](http://upload-images.jianshu.io/upload_images/5308475-951b6edf9229d296.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接着画左右眼球：
```
         /*右眼球*/
        cxt.beginPath();
        cxt.fillStyle = '#000';
        cxt.arc(230, 130, 12, 0, 2 * Math.PI);
        cxt.fill();
        cxt.stroke();
        /*左眼球*/
        cxt.beginPath();
        cxt.fillStyle = '#000';
        cxt.arc(170, 130, 12, 0, 2 * Math.PI);
        cxt.fill();
        cxt.stroke();
```
左右眼球：

![左右眼球](http://upload-images.jianshu.io/upload_images/5308475-bcc8fa1d28b86a65.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接着画鼻子：
```
        cxt.beginPath();
        cxt.arc(200, 165, 25, 0, 2 * Math.PI);
        cxt.fillStyle = '#d05823';
        cxt.fill();
        cxt.stroke();
```

鼻子：

![鼻子](http://upload-images.jianshu.io/upload_images/5308475-c435787e2ec2ca59.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接着画胡须：
```
        //左胡须
        cxt.beginPath();
        cxt.moveTo(80, 175);
        cxt.lineTo(150, 195);
        cxt.moveTo(80, 200);
        cxt.lineTo(150, 205);
        cxt.moveTo(80, 225);
        cxt.lineTo(150, 215);
        //中部胡须
        cxt.moveTo(200, 195);
        cxt.lineTo(200, 290);
        //右胡须
        cxt.moveTo(250, 195);
        cxt.lineTo(320, 175);
        cxt.moveTo(250, 205);
        cxt.lineTo(320, 200);
        cxt.moveTo(250, 215);
        cxt.lineTo(320, 225);
        cxt.stroke();
```
胡须:

![胡须](http://upload-images.jianshu.io/upload_images/5308475-dd9fdcb1b60c2fce.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


接着画嘴：
```
        cxt.moveTo(80, 240);
        cxt.quadraticCurveTo(200, 350, 320, 240);
        cxt.stroke();
```
嘴：
![嘴](http://upload-images.jianshu.io/upload_images/5308475-c8156d2154c31ab6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接下来画围巾：
```
        cxt.beginPath();
        cxt.moveTo(96, 316);
        cxt.lineTo(305, 316);
        cxt.lineTo(320, 316);
        cxt.arcTo(330, 316, 330, 326, 10);//在画布上创建介于两个切线之间的弧，起点坐标为(330,316),终点坐标为(330,326),半径为10
        cxt.lineTo(330, 336);
        cxt.arcTo(330, 346, 305, 346, 10);
        cxt.lineTo(81, 346);
        cxt.arcTo(71, 346, 71, 336, 10);
        cxt.lineTo(71, 326);
        cxt.arcTo(71, 316, 81, 316, 10);
        cxt.lineTo(96, 316);
        cxt.fillStyle = '#b13209';
        cxt.fill();
        cxt.stroke();
```
围巾：

![围巾](http://upload-images.jianshu.io/upload_images/5308475-00f257d5f26efa52.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接着画衣服：
```
        cxt.beginPath();
        cxt.fillStyle = '#0bb0da';
        cxt.moveTo(80, 346);
        //左衣服
        cxt.lineTo(26, 406);
        cxt.lineTo(65, 440);
        cxt.lineTo(85, 418);
        cxt.lineTo(85, 528);
        cxt.lineTo(185, 528);
        //右衣服
        cxt.lineTo(315, 528);
        cxt.lineTo(315, 418);
        cxt.lineTo(337, 440);
        cxt.lineTo(374, 406);
        cxt.lineTo(320, 346);
        cxt.fill();
        cxt.stroke();
```
衣服：
![衣服](http://upload-images.jianshu.io/upload_images/5308475-4c8e54b75228ffd3.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
接着画手：
```
        //左手
        cxt.beginPath();
        cxt.fillStyle = '#fff';
        cxt.arc(37, 433, 30, 0, 2 * Math.PI);
        cxt.fill();
        cxt.stroke();
        //右手
        cxt.beginPath();
        cxt.fillStyle = '#fff';
        cxt.arc(363, 433, 30, 0, 2 * Math.PI);
        cxt.fill();
        cxt.stroke();
```

手：
![手](http://upload-images.jianshu.io/upload_images/5308475-d49f6888ee45e0e6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接着画肚：
```
        cxt.beginPath();
        cxt.fillStyle = '#fff';
        cxt.arc(200, 400, 91, 1.8 * Math.PI, 1.2 * Math.PI);
        cxt.fill();
        cxt.stroke();
```
肚：
![肚](http://upload-images.jianshu.io/upload_images/5308475-2c51ca97eeec8c11.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

接着画小口袋
```
        cxt.beginPath();
        cxt.fillStyle = '#fff';
        cxt.moveTo(130, 394);
        cxt.lineTo(270, 394);
        cxt.moveTo(130, 394);
        cxt.bezierCurveTo(130, 490, 270, 490, 270, 394);
        cxt.fill();
        cxt.stroke();
```
小口袋：

![小口袋](http://upload-images.jianshu.io/upload_images/5308475-82fcde37b775d0ea.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

最后画两只脚以及两只脚的的空隙：
```
      /*两只脚的空隙*/
        cxt.beginPath();
        cxt.fillStyle = '#fff';
        cxt.arc(200, 529, 20,Math.PI, 0);
        cxt.fill();
        cxt.stroke();
        /*脚*/
        //左脚
        cxt.beginPath();
        cxt.fillStyle='#fff';
        cxt.moveTo(180,528);
        cxt.lineTo(72,528);
        cxt.bezierCurveTo(52,528,52,558,72,558);
        cxt.lineTo(180,558);
        cxt.moveTo(180,558);
        cxt.bezierCurveTo(200,558,200,528,180,528);
        cxt.fill();
        cxt.stroke();
        //右脚
        cxt.beginPath();
        cxt.fillStyle='#fff';
        cxt.moveTo(220,528);
        cxt.lineTo(328,528);
        cxt.bezierCurveTo(348,528,348,558,328,558);
        cxt.lineTo(220,558);
        cxt.moveTo(220,558);
        cxt.bezierCurveTo(200,558,200,528,220,528);
        cxt.fill();
        cxt.stroke();
```



完成了︿(￣︶￣)︿
![哆啦A梦](http://upload-images.jianshu.io/upload_images/5308475-24ab4e6cda048199.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


完整代码请点击：[哆啦A梦](https://github.com/shenzekun/doraemon/blob/master/Doraemon.html)


