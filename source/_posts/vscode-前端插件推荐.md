---
title: vscode 前端插件推荐
date: 2017-10-30 16:38:04
tags: 插件
categories: 前端
copyright: true
keywords: 编辑器
---

----

<!--more-->


## 常用插件

### Auto Close Tag

>自动添加HTML / XML关闭标签（必备）

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15092830970499.gif)

### Auto Rename Tag

>自动重命名配对的HTML / XML标签(必备)


![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15092838452118.gif)


### Beautify

>格式化javascript，JSON，CSS，Sass，和HTML


### Bootstrap 4 & Font awesome snippets

>包含Bootstrap 4＆Font awesome 的代码片段

![](https://ws1.sinaimg.cn/large/006tNc79ly1fkzg3v9bfnj30rk02ymx1.jpg)

### Bracket Pair Colorizer

>颜色识别匹配括号

![](https://ws4.sinaimg.cn/large/006tNc79ly1fkzg8ththdj30k40500ss.jpg)


### Class autocomplete for HTML

>智能提示HTML class =“”属性（必备）


### Code Runner


>非常强大的一款插件，能够运行多种语言的代码片段或代码文件：C，C ++，Java，JavaScript，PHP，Python，Perl，Ruby，Go等等，安装完成后，右上角出现：
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15092851845587.jpg)
点击这个按钮就可以运行你的文件了（必备）

### css peek

>能够查看CSS ID和类的字符串作为HTML文件中相应的CSS定义（必备）

**使用方法**：将光标放在class里面的属性，右击
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15092856731870.jpg)

### Dash

>查文档必备，搭配 dash（不过似乎只有 mac 版）😁

>**快捷键 `ctrl + h`** 它根据你当前选中的语言查找 dash 里面的文档

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/navicat-id-increase.gif)

### Debugger for Chrome

>让 vscode 映射 chrome 的 debug功能，使静态页面都可以用 vscode 来打断点调试

**简单使用**：[戳我](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/001470969077294a6455fc9cd1f48b69f82cd05e7fa9b40000)

### Document This

>添加注释块

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093400730364.jpg)


**设置：**

```
 "docthis.includeAuthorTag": true,//出现@Author
 "docthis.includeDescriptionTag": true,//出现@Description
 "docthis.authorName": "shenzekun",//作者名字
```

**快捷键**： 按两次Ctrl+alt+d


### ESLint

>EsLint可以帮助我们检查Javascript编程时的语法错误。比如：在Javascript应用中，你很难找到你漏泄的变量或者方法。EsLint能够帮助我们分析JS代码，找到bug并确保一定程度的JS语法书写的正确性。

**配置**：[戳我](https://segmentfault.com/a/1190000010462601)

### Font-awesome codes for html 

>用于 html 的Font-awesome代码片段

### filesize

>在底部状态栏显示当前文件大小，点击后还可以看到详细创建、修改时间

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093414045557.jpg)


### Git History

>以图表的形式查看git日志 
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093254060028.jpg)

使用 command+shift+p（Ctrl+shift+p） 输入git log就可以看到了

### Git Lens

>git 日志插件

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093256313651.jpg)

### HTML CSS Support

>在 html 标签上写class 智能提示当前项目所支持的样式（必备）

### HTML Snippets

>html 代码片段（必备）

### htmlhint

>html代码检测

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093260108371.jpg)

### htmltagwrap

>可以在选中HTML标签中外面套一层标签

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/vscode-htmltagwrap.gif)


**使用**：选择一大段代码，然后按“Alt + W”

### Indenticator

>突出目前的缩进深度


![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/Indenticator.gif)


### IntelliSense for CSS class names

智能提示 css 的 class 名

### Image Preview

>鼠标移到路径里显示图像预览

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093708776977.jpg)


### JavaScript (ES6) code snippets

>es6代码片段（必备）



### JavaScript Snippet Pack

>js代码片段（必备）

### jQuery Code Snippets

>jQuery 代码片段

### Live Sass Compiler

>实时编译 sass ,不过需要配置，附上我的配置


```
"liveSassCompile.settings.formats":[
        // You can add more
        {
            "format": "compressed",//压缩
            "extensionName": ".min.css",//编译后缀名
            "savePath": "./css"//编译保存的路径
        }
    ],
```

**使用**

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093281194279.jpg)


### markdownlint

>markdown 语法检查

### Node.js Modules Intellisense

>可以在导入语句中自动完成JavaScript / TypeScript模块。

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/vscode-node.gif)

### npm Intellisense

>在导入语句中自动填充npm模块,跟Node.js Modules Intellisense差不多


### open in browser

>当前的 html 文件用浏览器打开，类似 webstorm 的那四个小浏览器图标功能，前提条件html 文件必须保存

**快捷键alt+b**

### Output Colorizer

>输出提示的文字颜色有一些变化，方便获取关键信息

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093384952721.jpg)


### Path Intellisense

>路径自动补全（必备）

### Prettier

>格式化JavaScript / TypeScript / CSS 。

### Project Manager


>工程项目过多时，shift+cmd+p(shift+ctrl+p) 然后输入project，第一次选择edit Project编辑自己的工程项目，之后就可以直接选择open打开你的项目

### Sass

>写 sass 必备

### vscode-faker

>生成假数据，地址，电话，图片等等

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/vscode-faker.gif)

打开方式shift+cmd+p(shift+ctrl+p)) 然后输入faker 就可以选择了

### Quokka.js

>实时观看 javascript 的变量的变化

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/vscode-quokka.gif)

**使用**：先shift+cmd+p （ctrl+shift+p）输入 quokka 选择 new javascript 就行了😀

### Regex Previewer

>测试正则的插件

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093406954760.jpg)


### TSLint

>检查typescript编程时的语法错误语法


### TypeScript Importer

>自动搜索工作区文件中的TypeScript定义，并将所有已知符号作为完成项，以允许代码完成。

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/vscode-ts.gif)


### vscode-icons

>目录树图标


## react

### React-Native/React/Redux snippets for es6/es7

>react代码片段，下载人数超多😉


### react-beautify

>格式化 javascript, JSX, typescript, TSX 文件

## vue

### vetur
>语法高亮、智能感知

### VueHelper

>vue代码片段

### Vue TypeScript Snippets

>vue的 typescript 代码片段

###  Vue 2 Snippets

>vue 2代码片段

## 主题

### Dracula Official
个人最喜欢的主题，应该是最好看的主题之一😀

![](https://ws4.sinaimg.cn/large/006tNc79ly1fkzxpf6tevj30l206s74d.jpg)

### One Dark Pro

这个也好看😄

![](https://ws3.sinaimg.cn/large/006tNc79ly1fkzy0i7rutj30py06yglq.jpg)

### Atom One Dark Theme(老版本)

这个和 One Dark Pro差不多，One Dark Pro颜色主题多一些

![](https://ws3.sinaimg.cn/large/006tNc79ly1fkzxzhoqkrj30l6062jrl.jpg)



### One Monokai Theme


![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093223049049.jpg)


### Eva Theme

里面包含黑色和白色主题，这个白色主题感觉挺好看的

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093223899355.jpg)


![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093223624542.jpg)


### Boxy Theme Kit

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15093265368328.jpg)




---

大家还有什么好的插件推荐吗🤓


