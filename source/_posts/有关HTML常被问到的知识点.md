---
title: 有关HTML常被问到的知识点
date: 2017-05-22 22:47:36
tags: html
categories: 前端
copyright: true
---

----

## HTML、XML、XHTML 有什么区别?

<!--more-->

>1. **HTML**即是超文本标记语言（Hyper Text Markup Language），是**最早**写网页的语言，但是由于时间早，规范不是很好，大小写混写且编码不规范,是语法较为松散的、不严格的Web语言
2. **XHTML**是升级版的html（Extensible Hyper Text Markup Language），对html进行了规范，编码更加严谨纯洁，也是一种过渡语言，html向xml过渡的语言。实际上XHTML 与 HTML 4.01 标准没有太多的不同。
3. **XML**是可扩展标记语言（Extensible Markup Language），是一种跨平台语言，编码更自由，可以自由创建标签（
比如像下面这样创建：
```
<note>
<to>Tove</to>
<from>Jani</from>
<heading>Reminder</heading>
<body>Don't forget me this weekend!</body>
</note>
```
），主要用于存储数据和结构，可扩展

## HTML和XML的区别：
1. XML 被设计用来传输和存储数据，其焦点是数据的内容。
2. HTML 被设计用来显示数据，其焦点是数据的外观。
3. HTML 旨在显示信息，而 XML 旨在传输信息。
4. XML在定义标记时区分大小写，而HTML标记不区分大小写。


## HTML和XHTML的区别：
 
1. XHTML 元素必须被正确地嵌套。
例如：XHTML必须要这样`<b><i>This text is bold and italic</i></b>`
而在 HTML 中，某些元素可以像这样彼此不正确地嵌套：
`<b><i>This text is bold and italic</b></i>`

2. XHTML 元素必须被关闭。
*例如*`<p>This is a paragraph</p>`===>>*这是正确的*
`<p>This is a paragraph`===>>*这是错误的*
3. 标签名必须用小写字母。
*例如: *`<p>This is a paragraph</p>`==>>*这是正确的*
` <P>This is a paragraph</P>`===>>*这是错误的*

4. XHTML 文档必须拥有根元素。
所有的 XHTML 元素必须被嵌套于 `<html>` 根元素中

---






## 怎样理解 HTML 语义化?

>HTML语义化是让大家直观的认识标签(markup)和属性(attribute)的用途和作用，选择合适的标签（代码语义化）便于开发者阅读和写出更优雅的代码的同时让浏览器的爬虫和机器很好地解析，并且便于团队开发和维护。

---

## 怎样理解内容与样式分离的原则?

>写 HTML 的时候先不管样式, 重点放在HTML的结构和语义化上，让 HTML 能体现页面结构或者内容。之后再去写样式。
写 JS 的时候，尽量不要用 JS 去直接操作样式，而是通过给元素添加删除class来控制样式变化。
文档结构与文档样式的分离可以确保网页的平稳退化，也让内容和样式在可以分开独立编辑。

---

## 有哪些常见的meta标签?

>* 指定字符集
> `<meta charset="utf-8"> ` 
>* 向搜索引擎说明你的网页的关键词
>`<meta name="keywords" content="">` 
>* 告诉搜索引擎你的站点的主要内容 
>`<meta name="description" content="">`  
>* 告诉搜索引擎你的站点的制作的作者
>`<meta name="author" content="your name"> `
>*  响应式页面
> `<meta name="viewport" content="width=device-width, initial-scale=1.0"> `
* 定时让网页在3秒内跳转到mozilla首页(`http-equiv` 属性为名称/值对提供了名称。并指示服务器在发送实际的文档之前先在要传送给浏览器的 MIME 文档头部包含名称/值对。)
`<meta http-equiv="refresh" content="3" url=https://www.mozilla.org"> `
* 如果安装了GCF (Google Chrome Frame)，则使用GCF来渲染页面 ("chrome=1"), 如果没有安装GCF，则使用最高版本的IE内核进行渲染 ("IE=edge")。`X-UA-Compatible`(浏览器采取何种版本渲染当前页面)
`<meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1"> `
* 浏览器的内核控制
` <meta name="renderer" content="webkit|ie-comp|ie-stand">`

---

## 文档声明的作用?

>文档声明用来告知浏览器当前文档所使用的类型，让浏览器解析器知道要用什么规范来解析文档。

---

## 严格模式和混杂模式指什么?

>在严格模式中，浏览器以其支持的最高标准呈现页面。
在混杂模式中，又称怪异模式或兼容模式，浏览器用自己的方式解析代码，页面以一种比较宽松的向后兼容的方式显示。混杂模式通常模拟老式浏览器的行为以防止老站点无法工作。


---

## <!doctype html> 的作用?

>它是html5标准网页声明,告诉浏览器用最新的 HTML5标准来解析渲染页面；如果不写，浏览器就会进入混杂模式。

---

## 浏览器乱码的原因是什么？如何解决？

>  乱码产生的**根本原因**是保存的编码格式和浏览器解析时的解码格式不匹配导致的。
**解决方式：** 写代码的时候在html 的 `<head>`里添加`<meta charset='xxx'>`并且保存的时候仍选择同样的编码方式。

---

## 常见的浏览器有哪些？什么内核？

>* **Internet explorer** 使用的是**Trident**
* **Firefox**使用的是**Gecko**。
* **opera**之前使用的是**Presto**，后来用**Blink**
* 苹果的**Safari**，谷歌的**Chrome**使用的是**WebKit**，还有国产的大部分双核浏览器其中一核就是**WebKit**。


---

## 列出常见的标签，并简单介绍这些标签用在什么场景？

| 标签      | 运用场景          | 
| ------------- |:-------------:| 
| `<html>`      | HTML 页面的根元素 | 
| `<body>`    | 文档的内容   |  
| `<head>` | 用于定义文档的头部   | 
|  `<meta>` | 提供了元数据.元数据也不显示在页面上，被浏览器解析  |
| `<title>`  | 文档的标题  |
| `<h1>-<h6>` | 定义了一级标题到六级标题，标题字体大小逐渐减弱  |
| `<p>`  |  定义一个段落 |
|  `<a>` | 网页链接  |
| `<div>`  | 块级元素，它可用于组合其他 HTML 元素的容器,没有特定的含义  |
|`<span> `| 内联元素，也没有特定的含义，可用作文本的容器|
| `<u>`  | 下划线  |
| `<em>`  | 强调文本  |
| `<strong>`  |  加重文本 |
| `<ol>`  |  	有序列表 |
| `<ul>`  | 	无序列表  |
| `<li>`  |  定义列表项目 |
| `<img>`  |   	图片|
| `<br >`  | 	换行  |
| `<input>`  |  定义输入控件 |
| `<i>`  |  	斜体字 |
| `<table>`  |  定义表 |
| `<tr>`  |  	定义表格中的行 |
| `<td>`  |定义表中的单元格 |
|`<th>`| 定义表格的表头|
|`<tbody>`|定义表格的主体|
|`<tfoot>`|定义表格的页脚|
| `<hr> `  |创建一条水平线   |
| `<iframe>`  |定义内联框架 |
| `<cite>`  | 定义作品的标题|
| `<button>`  | 按钮|
| `<b>`  | 定义粗体文本|
| `<form>`  | 定义用于用户输入的HTML表单|
| `<caption>`  | 定义表标题|
| `<footer>`  |定义文档或节的页脚 |


