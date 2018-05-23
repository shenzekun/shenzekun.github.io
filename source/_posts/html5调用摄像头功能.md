---
title: html5调用摄像头功能
date: 2018-05-05 21:19:14
tags: [前端,html,js]
categories: 前端
copyright: true
keywords: html5调用摄像头
---

----

## 前言

> 前些天，线上笔试的时候，发现需要浏览器同意开启摄像头，感觉像是 js 调用的，由于当时笔试，也就没想到这么多🤣。今天闲来无事，看了下自己的 todo，发现有这个调用摄像头的todo，才想到😂。网上查了一下，果然 js 有调用摄像头的 api，为此自己写一个 demo ，避免忘记。

<!--more-->

## 正文
### 调用摄像头
一共有两种实现方式，一种是使用`navigator.getUserMedia`（**该特性已经从 Web 标准中删除**，虽然一些浏览器目前仍然支持它，但也许会在未来的某个时间停止支持，请尽量不要使用该特性），**前面一种已经从 Web 标准中删除**，仅为了向后兼容而存在，第二种是使用`navigator.mediaDevices.getUserMedia`(**推荐使用**),这两种方法 Safari 貌似都不支持。。。。

* 第一种方法`navigator.getUserMedia`用法详见 [mdn](https://developer.mozilla.org/zh-CN/docs/Web/API/Navigator/getUserMedia) ，代码如下：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>摄像头调用1</title>
</head>

<body>
    <video id="v"></video>
    <script>
        !(function () {
            function userMedia() {
                return navigator.getUserMedia = navigator.getUserMedia ||
                    navigator.webkitGetUserMedia ||
                    navigator.mozGetUserMedia ||
                    navigator.msGetUserMedia || null;
            }
            if (userMedia()) {
                var constraints = {
                    video: true,
                    audio: false
                };
                var media = navigator.getUserMedia(constraints, function (stream) {
                    var v = document.getElementById('v');
                    var url = window.URL || window.webkitURL;
                    v.src = url ? url.createObjectURL(stream) : stream;
                    v.play();
                }, function (error) {
                    console.log("ERROR");
                    console.log(error);
                });
            } else {
                console.log("不支持");
            }
        })();
    </script>
</body>
</html>
```



* 第二种方法`navigator.mediaDevices.getUserMedia`用法详见[mdn](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)。`navigator.mediaDevices.getUserMedia` 其实和第一种差不多，主要第二种返回是一个 Promise 对象，代码如下：

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>摄像头调用2</title>
</head>

<body>
    <video id="v"></video>
    <script>
        !(function () {
            // 老的浏览器可能根本没有实现 mediaDevices，所以我们可以先设置一个空的对象
            if (navigator.mediaDevices === undefined) {
                navigator.mediaDevices = {};
            }
            if (navigator.mediaDevices.getUserMedia === undefined) {
                navigator.mediaDevices.getUserMedia = function (constraints) {
                    // 首先，如果有getUserMedia的话，就获得它
                    var getUserMedia = navigator.webkitGetUserMedia || navigator.mozGetUserMedia || navigator.msGetUserMedia;

                    // 一些浏览器根本没实现它 - 那么就返回一个error到promise的reject来保持一个统一的接口
                    if (!getUserMedia) {
                        return Promise.reject(new Error('getUserMedia is not implemented in this browser'));
                    }

                    // 否则，为老的navigator.getUserMedia方法包裹一个Promise
                    return new Promise(function (resolve, reject) {
                        getUserMedia.call(navigator, constraints, resolve, reject);
                    });
                }
            }
            const constraints = {
                video: true,
                audio: false
            };
            let promise = navigator.mediaDevices.getUserMedia(constraints);
            promise.then(stream => {
                let v = document.getElementById('v');
                // 旧的浏览器可能没有srcObject
                if ("srcObject" in v) {
                    v.srcObject = stream;
                } else {
                    // 防止再新的浏览器里使用它，应为它已经不再支持了
                    v.src = window.URL.createObjectURL(stream);
                }
                v.onloadedmetadata = function (e) {
                    v.play();
                };
            }).catch(err => {
                console.error(err.name + ": " + err.message);
            })
        })();
    </script>
</body>
</html>
```

### 拍照

思路是设置一个标志变量 videoPlaying 看看是否 video 有在 play，监听拍照按钮的点击事件，如果videoPlaying 为 true ，使用一个canvas 获取 video 的宽高（默认 canvas 是不显示的），然后使用 canvas 的[drawImage](https://developer.mozilla.org/zh-CN/docs/Web/API/CanvasRenderingContext2D/drawImage),然后使用 canvas 的 [toDataURL](https://developer.mozilla.org/zh-CN/docs/Web/API/HTMLCanvasElement/toDataURL)返回一个 data url，将这个 url，设置在一个 img 标签上即可😀


* 第一种方法`navigator.getUserMedia`实现代码：

```html
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>拍照1</title>
</head>
<body>
    <button id="take">拍照</button>
    <br />
    <video id="v" style="width: 640px;height: 480px;"></video>
    <canvas id="canvas" style="display:none;"></canvas>
    <br />
    <img src="http://placehold.it/640&text=Your%20image%20here%20..." id="photo" alt="photo">
    <script>
        !(function () {
            function userMedia() {
                return navigator.getUserMedia = navigator.getUserMedia ||
                    navigator.webkitGetUserMedia ||
                    navigator.mozGetUserMedia ||
                    navigator.msGetUserMedia || null;
            }
            if (userMedia()) {
                let videoPlaying = false;
                let constraints = {
                    video: true,
                    audio: false
                };
                let video = document.getElementById('v');
                let media = navigator.getUserMedia(constraints, function (stream) {
                    let url = window.URL || window.webkitURL;
                    video.src = url ? url.createObjectURL(stream) : stream;
                    video.play();
                    videoPlaying = true;
                }, function (error) {
                    console.log("ERROR");
                    console.log(error);
                });
                document.getElementById('take').addEventListener('click', function () {
                    if (videoPlaying) {
                        let canvas = document.getElementById('canvas');
                        canvas.width = video.videoWidth;
                        canvas.height = video.videoHeight;
                        canvas.getContext('2d').drawImage(video, 0, 0);
                        let data = canvas.toDataURL('image/webp');
                        document.getElementById('photo').setAttribute('src', data);
                    }
                }, false);
            } else {
                console.log("不支持");
            }
        })();
    </script>
</body>
</html>
```

第二种`navigator.mediaDevices.getUserMedia`实现方法:

```html
<!doctype html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title>拍照2</title>
</head>

<body>
    <button id="take">拍照</button>
    <br />
    <video id="v" style="width: 640px;height: 480px;"></video>
    <canvas id="canvas" style="display:none;"></canvas>
    <br />
    <img src="http://placehold.it/640&text=Your%20image%20here%20..." id="photo" alt="photo">
    <script>
        !(function () {
            // 老的浏览器可能根本没有实现 mediaDevices，所以我们可以先设置一个空的对象
            if (navigator.mediaDevices === undefined) {
                navigator.mediaDevices = {};
            }
            if (navigator.mediaDevices.getUserMedia === undefined) {
                navigator.mediaDevices.getUserMedia = function (constraints) {
                    // 首先，如果有getUserMedia的话，就获得它
                    var getUserMedia = navigator.webkitGetUserMedia || navigator.mozGetUserMedia || navigator.msGetUserMedia;

                    // 一些浏览器根本没实现它 - 那么就返回一个error到promise的reject来保持一个统一的接口
                    if (!getUserMedia) {
                        return Promise.reject(new Error('getUserMedia is not implemented in this browser'));
                    }

                    // 否则，为老的navigator.getUserMedia方法包裹一个Promise
                    return new Promise(function (resolve, reject) {
                        getUserMedia.call(navigator, constraints, resolve, reject);
                    });
                }
            }
            const constraints = {
                video: true,
                audio: false
            };
            let videoPlaying = false;
            let v = document.getElementById('v');
            let promise = navigator.mediaDevices.getUserMedia(constraints);
            promise.then(stream => {
                // 旧的浏览器可能没有srcObject
                if ("srcObject" in v) {
                    v.srcObject = stream;
                } else {
                    // 防止再新的浏览器里使用它，应为它已经不再支持了
                    v.src = window.URL.createObjectURL(stream);
                }
                v.onloadedmetadata = function (e) {
                    v.play();
                    videoPlaying = true;
                };
            }).catch(err => {
                console.error(err.name + ": " + err.message);
            })
            document.getElementById('take').addEventListener('click', function () {
                if (videoPlaying) {
                    let canvas = document.getElementById('canvas');
                    canvas.width = v.videoWidth;
                    canvas.height = v.videoHeight;
                    canvas.getContext('2d').drawImage(v, 0, 0);
                    let data = canvas.toDataURL('image/webp');
                    document.getElementById('photo').setAttribute('src', data);
                }
            }, false);
        })();
    </script>
</body>

</html>
```



