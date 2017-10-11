---
title: 解决inline-block元素的bug
date: 2017-08-30 21:21:53
tags: css
categories: 前端
copyright: true
keywords: inline-block
---

----

>在使用inline-block时，有时候出现的效果莫名奇妙，例如：
>
>* 两个inline-block 元素之间如果有空格、回车、tab，那么在页面上就有一个空隙
>* 两个不同高度的 inline-block 元素顶部无法对齐，或者使用inline-block下面无缘无故多出几像素

<!--more-->

## 例子1,出现空隙

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    div{
      display: inline-block;
      width:100px;
      height: 100px;
      background-color: rgb(233, 148, 148);
    }
  </style>
</head>

<body>
  <div></div>
  <div></div>
</body>

</html>
```

### 效果：


![](http://upload-images.jianshu.io/upload_images/5308475-efbd5e22bb492464.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 解决方法

**1.去掉空格**

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    div{
      display: inline-block;
      width:100px;
      height: 100px;
      background-color: rgb(233, 148, 148);
    }
  </style>
</head>

<body>
  <div></div><div></div>
</body>

</html>
```

**2. 添加父元素，将父元素的 font-size 设置为0，然后在 inline-block 元素中将 font-size 设置为 14px**

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    .parent{
      font-size:0;
    }
    .child{
      font-size:14px;
      display: inline-block;
      width:100px;
      height: 100px;
      background-color: rgb(233, 148, 148);
    }
  </style>
</head>

<body>
  <div class="parent">
    <div class="child"></div>
    <div class="child"></div>
  </div>
</body>

</html>
```

**3. 使用`margin-right`**

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    .child{
      display: inline-block;
      width:100px;
      height: 100px;
      background-color: rgb(233, 148, 148);
      margin-right:-5px;
    }
  </style>
</head>

<body>
  <div class="child"></div>
  <div class="child"></div>
</body>

</html>
```

**4. 添加父元素，使用letter-spacing（该属性增加或减少字符间的空白（字符间距））**

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    .parent{
      letter-spacing:-5px;
    }
    .child{
      display: inline-block;
      width:100px;
      height: 100px;
      background-color: rgb(233, 148, 148);
    }
  </style>
</head>

<body>
  <div class="parent">
    <div class="child"></div>
    <div class="child"></div>
  </div>
</body>

</html>
```

**5. 使用word-spacing （该属性增加或减少单词间的空白（即字间隔））**

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    .parent{
      word-spacing:-5px;
    }
    .child{
      display: inline-block;
      width:100px;
      height: 100px;
      background-color: rgb(233, 148, 148);
    }
  </style>
</head>

<body>
  <div class="parent">
    <div class="child"></div>
    <div class="child"></div>
  </div>
</body>

</html>
```

### 解决效果：

![](http://upload-images.jianshu.io/upload_images/5308475-e11f863d7e7beccc.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 例子2，设置inline-block 后，莫名其妙出现一些空白

```
<!doctype html>
<html>

<head>
  <meta charset="utf-8">
  <title>span设为inline-block之后下面的空白</title>
  <style>
    div{
      border:solid 1px rgb(202, 43, 43);
      width:250px;
    }
    span{
      display:inline-block;
      width:200px;
      height:200px;
      background-color:rgb(109, 195, 252);
      
    }
  </style>
</head>

<body>
  <div>
    <span></span>
  </div>
</body>

</html>
```

### 效果

![](http://upload-images.jianshu.io/upload_images/5308475-733a6cd2882f1d23.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 解决方法

**使用vertical-align**

```
<!doctype html>
<html>

<head>
  <meta charset="utf-8">
  <title>span设为inline-block之后下面的空白</title>
  <style>
    div{
      border:solid 1px rgb(202, 43, 43);
      width:250px;
    }
    span{
      display:inline-block;
      width:200px;
      height:200px;
      background-color:rgb(109, 195, 252);
      vertical-align:top;//新增
    }
  </style>
</head>

<body>
  <div>
    <span></span>
  </div>
</body>

</html>
```

### 解决效果

![](http://upload-images.jianshu.io/upload_images/5308475-74787680d7bfab18.jpg?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


## 例子3，两个不同高度的 inline-block 元素顶部无法对齐


```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    
    .child1{
      display: inline-block;
      width:100px;
      height: 100px;
      
      background-color: rgb(109, 195, 252);
    }
    .child2{
      display: inline-block;
      width:100px;
      height: 120px;
      background-color: rgb(233, 148, 148);
    }
  </style>
</head>

<body>
  
    <div class="child1"></div>
    <div class="child2"></div>

</body>

</html>
```

### 效果


![](http://upload-images.jianshu.io/upload_images/5308475-3974cddc92207720.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


### 解决方法

**还是使用vertical-align**

```
<!DOCTYPE html>
<html>

<head>
  <meta charset="utf-8">
  <title>JS Bin</title>
  <style>
    
    .child1{
      display: inline-block;
      width:100px;
      height: 100px;
      vertical-align:top;//新增
      background-color: rgb(109, 195, 252);
    }
    .child2{
      display: inline-block;
      width:100px;
      height: 120px;
      background-color: rgb(233, 148, 148);
    }
  </style>
</head>

<body>
  
    <div class="child1"></div>
    <div class="child2"></div>

</body>

</html>
```


### 解决效果


![](http://upload-images.jianshu.io/upload_images/5308475-330207fc3fb88ea6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


