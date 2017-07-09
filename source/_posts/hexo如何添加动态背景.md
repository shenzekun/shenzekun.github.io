---
title: next主题如何添加动态背景
date: 2017-03-04 13:57:37
tags: hexo
categories: hexo 
copyright: true
---

-------

>**注意**：如果next主题在5.1.1以上的话就不用我这样设置，直接在主题配置文件中找到canvas_nest: false，把它改为canvas_nest: true就行了（注意分号后面要加一个空格）



其实挺简单的︿(￣︶￣)︿
### 修改`_layout.swig`

打开  ` next/layout/_layout.swig `
在 `< /body>`之前添加代码(注意不要放在< /head>的后面)

```JavaScript
{% if theme.canvas_nest %}
<script type="text/javascript" src="//cdn.bootcss.com/canvas-nest.js/1.0.0/canvas-nest.min.js"></script>
{% endif %}
```

-------

<!-- more -->

### 修改配置文件
打开 `/next/_config.yml`,在里面添加如下代码：(可以放在最后面)

```
# --------------------------------------------------------------
# background settings
# --------------------------------------------------------------
# add canvas-nest effect
# see detail from https://github.com/hustcc/canvas-nest.js
canvas_nest: true
```
到此就结束了，运行 `hexo clean`，然后运行 `hexo g`,然后运行 `hexo s`，最后打开浏览器在浏览器的地址栏输入 `localhost:4000` 就能看到效果了\（￣︶￣）/

-------


### 如果你感觉默认的线条太多的话

#### 可以这么设置====>

在上一步修改  `_layout.swig`中，把刚才的这些代码：

```JavaScript
{% if theme.canvas_nest %}
<script type="text/javascript" src="//cdn.bootcss.com/canvas-nest.js/1.0.0/canvas-nest.min.js"></script>
{% endif %}

```
改为

```JavaScript
{% if theme.canvas_nest %}
<script type="text/javascript"
color="0,0,255" opacity='0.7' zIndex="-2" count="99" src="//cdn.bootcss.com/canvas-nest.js/1.0.0/canvas-nest.min.js"></script>
{% endif %}

```

-------

### 配置项说明
* `color` ：线条颜色, 默认: `'0,0,0'`；三个数字分别为(R,G,B)
* `opacity`: 线条透明度（0~1）, 默认: `0.5`
* `count`: 线条的总数量, 默认: `150`
* `zIndex:` 背景的z-index属性，css属性用于控制所在层的位置, 默认: `-1`

