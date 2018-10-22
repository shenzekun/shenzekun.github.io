---
title: react-native问题汇总
date: 2018-05-08 13:05:13
tags: react
categories: 前端
copyright: true
keywords: react-native
---

----

## 前言
> 前些天使用react-native 写了个项目，遇到的问题挺多的，在这里记录下来📝，避免忘记。本篇文章会不定期更新!

<!--more-->

## 问题汇总

### 问题一
出现Remote debugger is in a background tab which may cause apps to perform slowly黄色警报
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-043813.png)

**解决方法**
把那个chrome的Tab页保持最前，窗口不要最小化就好了。。。。

### 问题二
出现connection to http://localhost:8081 红色错误
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-044331.png)

**解决方法**
这个很神奇。遇到了多按 ⌘R几下或者把模拟器上的项目删除之后重新加载一般就会解决。
> bad news: metro v0.29.0 won't work with RN 0.54-0.55 because it introduced a new config param that RN is not handling yet (we're working on improving configuration compatibility between RN and metro).

> good news: the actual fix needed to solve this issue is in the RN repo (7be3d1c), so cherry-picking it into the 0.54 and 0.55 branches and releasing a RN minor version will fix this. (cc @hramos, @grabbou ).

或者使用下面命令可以解决问题

```bash
yarn cache clean&&yarn
```

### 问题三
出现Runtime is not ready for debugging红色错误
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-044718.png)

**两种解决方法**

1. 关掉http://localhost:8081/debugger-ui/ 再重新开启就行了
2. 按 command+d 将Debug JS Remotely关掉也可以

### 问题四
出现Unrecognized font family 红色报警
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-045023.png)

**解决方法**
在终端输入

```bash
react-native link react-native-vector-icons
```

然后重新启动即可


### 问题五
React Native不支持自动计算Image等View的大小

[详情](http://facebook.github.io/react-native/docs/images.html#why-not-automatically-size-everything)

### 问题六
react-native-interactable 出现 Invariant Violation红色警报
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/15257552426894.jpg)

**解决方法**
降级：将 react-native 版本降到0.53.0 就行了
参考 [wix/react-native-interactable#185](https://github.com/wix/react-native-interactable/issues/185)

### 问题七
Build后遇到'No bundle URL present’ error
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-045522.png)

**解决方法**
关闭SS,VPN这类的服务，重新 `react-native run-ios` 即可。很神奇。。。

官方也有这个 [issue](https://github.com/facebook/react-native/issues/12754)

### 问题八
出现regeneratorRuntime is not defined
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-045839.png)

**解决方法**

```
react-native start --reset-cache
```

最终原因是因为一个组件没删干净🤣

### 问题九
出现:CFBundleIdentifier", Does Not Exist 错误

**解决方法**
打开 xcode 运行项目出现
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-050038.png)
在这里面有个 libInteractable.a 删除掉就行了
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-050103.png)

参考：[rebeccahughes/react-native-device-info#251](https://github.com/rebeccahughes/react-native-device-info/issues/251)

### 问题十
删除包注意事项

首先 `react-native unlink <lib name>`
然后 `yarn remove <lib name>`

**一定要这样做**不然会有问题。。。

### 问题十一
出现Invariant Violation: View config not found for name 红色警报
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-050336.png)

**解决方法**
https://stackoverflow.com/questions/46750477/react-native-invariant-violation-view-config

### 问题十二
Button 组件无法直接使用 style定宽度和高度等等

**解决方法**
> If this button doesn't look right for your app, you can build your own button using TouchableOpacity or TouchableNativeFeedback.

也就是说可以使用 `TouchableOpacity` 或者 `TouchableNativeFeedback` 组件代替

### 问题十三
使用TouchableWithoutFeedback 出现错误
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-050857.png)

**解决方法**
TouchableWithoutFeedback，这个组件必须至少有一个child，如果是多个组件，必须以view来包装。写成这样就可以了

```
render() {
  return(
      <TouchableWithoutFeedback style={{flex: 1}} onPress={dismissKeyboard}>
            <View style={{flex: 1}}>
      。。。。。。。。。。
    </View>

    </TouchableWithoutFeedback>
  );
}
```

### 问题十四
xcode出现Showing All Messages Code signing is required for product type 'Unit Test Bundle' in SDK 'iOS 11.2'
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-051045.png)

在Xcode上
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-051232.png) 
即可

### 问题十五
react-navigation TabNavigator点击切换反应迟钝。

在真机上调试react-navigation的TabNavigator，点击tab总感觉反应很慢，试了好久都是这样，大概有0.5秒之后才会切换体验很差。

**解决方法**
关闭debug模式。。。。

### 问题十六
React Navigation TabNavigator 一个帧的延迟

当页面加载时，下面的 tab 图标从第一个到第二个图标有一个帧的延迟

**解决方法**
定义initialLayout，用以防止react-native-tab-view渲染中一个帧的延迟

参考：https://github.com/react-native-community/react-native-tab-view#avoid-one-frame-delay

### 问题十七
出现timed out waiting for 红色警报
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-051715.png)

**解决方法**
重启模拟器。。。

### 问题十八
react native 没有\<br />组件换行

**解决方法**
可以在 Text 组件里写 {'\n'},如：
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-051845.png)

### 问题十九
react native checkbox 原生组件只适合安卓

**解决方法**
可以使用这个 https://github.com/crazycodeboy/react-native-check-box

### 问题二十
react-navigation的headerRight添加点击事件

**解决方法**
首先需要在componentDidMount(){}中动态的添加点击事件

```
componentDidMount(){
    this.props.navigation.setParams({
        navigatePress:this.navigatePress
    })
}
```

然后

```
navigatePress = () => {
    alert('点击headerRight');
    console.log(this.props.navigation);
}
```

接下来就可以通过params方法来获取点击事件了（**记住先要判断navigation.state.params是否存在，不然会报错**。。。）

```
static navigationOptions = ({ navigation, screenProps }) => ({
      title: navigation.state.params?navigation.state.params.title:null,
      headerRight:(
          <Text onPress={navigation.state.params?navigation.state.params.navigatePress:null}>
              返回
          </Text>
      )
});
```

### 问题二十一
react-navigation tab 点击 StatusBar 颜色问题 

**解决方法**
详情 https://reactnavigation.org/docs/status-bar.html

### 问题二十二
 Image 标签不支持 http 问题
 
 **解决方法**
 ios 9 以上，默认是Https请求，如需支持Http，修改info.plist文件添加键值对就好了
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-052245.png)

### 问题二十三
react-native-swiper 动态数据渲染，翻页出现错乱

**出现**
一开始，使用静态的数据没问题，但是使用动态加载数据就出现问题，经过一些调试发现，可能是 index 的问题，在 github 库里搜 issue 果然有人遇到过这个问题 https://github.com/leecade/react-native-swiper/issues/720

**解决方法**
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-052442.png)
添加 key 值是你**获取数据的长度**

### 问题二十四
react-native-swiper 跳转索引 bug 问题。

一开始
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-052540.png)

在翻页的时候，出现索引随机变化的问题，当时看了一下 api 是没有问题的，一直定位到
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-052704.png)

将标题不显示就发现索引没有问题了，不会随机翻页。。。，接着在某一页看到题目比较大，发生了抖动，结果造成了随机翻页，再一看里面有数字和文字，大小不一样，设置一下字体就好了。。。。个人认为是抖动的时候可能触发了react-native-swiper的翻页，结果造成随机翻页。。。
神坑的 bug，找了4，5个小时。。。。😡

### 问题二十五
ListView, FlatList, Sections and VirtualizedList paddingBottom 无效的问题。

ListView, FlatList, Sections and VirtualizedList 继承了 ScrollView
所以导致都有这个问题

**解决方法**

```
<ScrollView contentContainerStyle={{paddingBottom: 16}} />
```

### 问题二十六
出现 could not connect to development server红色警报
![](https://blog-1257878287.cos.ap-chengdu.myqcloud.com/2018-05-08-052952.png)

**解决方法**
关掉 vpn ，或者不要开全局模式。。。很神奇


