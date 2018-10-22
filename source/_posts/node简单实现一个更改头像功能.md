---
title: node简单实现一个更改头像功能
date: 2017-12-28 10:23:05
tags: node
categories: 前端
copyright: true
keywords: 图片上传，更改头像
---

----

## 前言

> 一直想写这篇文章，无奈由于要考试的原因，一直在复习，拖延到现在才写🤣，之前用 node 的 express 框架写了个小项目，里面有个上传图片的功能，这里记录一下如何实现（我使用的是 **ejs**）📝

<!--more-->

## 思路
1.  **首先**，当用户点击上传头像，更新头像的时候，将头像上传到项目的一个文件夹里面（*我是存放在项目的`public/images/img`里面*），并且将图像名重命名（*可以以时间戳来命名*）。![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15144357069018.jpg)

2. **同时**图片在项目的路径插入到用户表的当前用户的 `userpicturepath` 里面
3. 然后更新用户的 session，将图片里面的路径赋值给 session 的里面的`picture`属性里面
4. `<img>` 的 `src` 获取到当前用户的session里面的 `picture` 的值，最后动态刷新页面头像就换成了用户上传的头像了

## 实现效果

![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2017-12-28-user-upload.gif)

## 代码

ejs部分

```
<img class="nav-user-photo" src="<%= user.picture.replace(/public(\/.*)/, "$1") %>" alt="Photo" style="height: 40px;"/>

<form enctype="multipart/form-data" method="post" name="fileInfo">
    <input type="file" accept="image/png,image/jpg" id="picUpload" name="file">
</form>

<button type="button" class="btn btn-primary" id="modifyPicV">确定</button>
```

js部分

```javascript
document.querySelector('#modifyPicV').addEventListener('click', function () {
    let formData = new FormData();
    formData.append("file",$("input[name='file']")[0].files[0]);//把文件对象插到formData对象上
    console.log(formData.get('file'));
    $.ajax({
        url:'/modifyPic',
        type:'post',
        data: formData,
        processData: false,  // 不处理数据
        contentType: false,   // 不设置内容类型
        success:function () {
            alert('success');
            location.reload();
        },
    })
});
```

路由部分，使用`formidable`，这是一个Node.js模块，用于解析表单数据，尤其是文件上传

```javascript
let express = require('express');
let router = express.Router();
let fs = require('fs');
let {User} = require('../data/db');
let formidable = require('formidable');
let cacheFolder = 'public/images/';//放置路径
router.post('/modifyPic', function (req, res, next) {
    let userDirPath = cacheFolder + "Img";
    if (!fs.existsSync(userDirPath)) {
        fs.mkdirSync(userDirPath);//创建目录
    }
    let form = new formidable.IncomingForm(); //创建上传表单
    form.encoding = 'utf-8'; //设置编码
    form.uploadDir = userDirPath; //设置上传目录
    form.keepExtensions = true; //保留后缀
    form.maxFieldsSize = 2 * 1024 * 1024; //文件大小
    form.type = true;
    form.parse(req, function (err, fields, files) {
        if (err) {
            return res.json(err);
        }
        let extName = ''; //后缀名
        switch (files.file.type) {
            case 'image/pjpeg':
                extName = 'jpg';
                break;
            case 'image/jpeg':
                extName = 'jpg';
                break;
            case 'image/png':
                extName = 'png';
                break;
            case 'image/x-png':
                extName = 'png';
                break;
        }
        if (extName.length === 0) {
            return res.json({
                msg: '只支持png和jpg格式图片'
            });
        } else {
            let avatarName = '/' + Date.now() + '.' + extName;
            let newPath = form.uploadDir + avatarName;
            fs.renameSync(files.file.path, newPath); //重命名
            console.log(newPath)
            //更新表
            User.update({
                picture: newPath
            }, {
                where: {
                    username: req.session.user.username
                }
            }).then(function (data) {
                if (data[0] !== undefined) {
                    User.findAll({
                        where: {
                            username: req.session.user.username
                        }
                    }).then(function (data) {
                        if (data[0] !== undefined) {
                            req.session.user.picture = data[0].dataValues.picture;
                            res.send(true);
                        } else {
                            res.send(false);
                        }
                    })
                }
            }).catch(function (err) {
                console.log(err);
            });
        }
    });
});
```





