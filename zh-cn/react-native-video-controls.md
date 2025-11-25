> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-video-controls</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/itsnubix/react-native-video-controls">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/itsnubix/react-native-video-controls/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/itsnubix/react-native-video-controls)

| 三方库版本                 | 支持RN版本                 |
| ------------------------- | -------------------------- |
| 2.8.1               |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

> [!TIP] 需要配套的服务和三方依赖

react-native-video-controls依赖于以下三方库

| Dependencies       | Version |
| :----------------- | :------ |
| react-native-video | >=2.0.0 |
| lodash             | ^4.16.4 |

本库依赖[@react-native-oh-tpl/react-native-video](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-video.md#link)以及简化开发的JS工具[lodash](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/js/lodash.md)

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install --save react-native-video-controls
```

#### **yarn**

```bash
yarn add react-native-video-controls
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, StyleSheet } from "react-native";
import VideoPlayer from 'react-native-video-controls';

const App = () => {
  function handleOnBack() {
    alert("this is onBack event test,because navigator properties depends on others parity");
  }
  return(
      <View>
       <VideoPlayer
      		title = 'oceans'
      		style = {styles.container}
         	videoStyle = {styles.video}
            source = {{ uri: 'https://vjs.zencdn.net/v/oceans.mp4' }}
            toggleResizeModeOnFullscreen = {true}
            controlAnimationTiming = {3000}
            doubleTapTime = {10}
            controlTimeout = {4000}
            scrubbing = {5}
			onBack = {handleOnBack}
            showOnStart = {false}
            seekColor = {'#00FFFF'}
            tapAnywhereToPause = {true}
        />
     </View>
    );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#000',
  }, 
  video: {  
    width: '100%',  
    height: '100%',  
  },
});

export default App;
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-video代码以及简化开发工具lodash，如已在 HarmonyOS 工程中引入过这些库，且版本无误则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-video文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-video.md#link)和[lodash文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/js/lodash.md)进行引入。安装完成后请在终端使用`npm list react-native-video`和`npm list lodash`查看video组件版本和lodash工具版本是否正确

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.28; SDK: HarmonyOS NEXT Developer Beta3 5.0.0.36(12 Beta3); IDE: DevEco Studio 5.0.3.535; ROM: 5.0.0.31;
2. RNOH：0.77.17; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!TIP] "Name"列属性navigator在使用时，请参考本文档其他

| Name                         | Description                                                  |     Type     | Required |  Platform   | HarmonyOS Support |
| ---------------------------- | ------------------------------------------------------------ | :----------: | :------: | :---------: | :---------------: |
| toggleResizeModeOnFullscreen | 如果为true，点击全屏按钮将在cover/contain模式之间切换`<Video />`组件，设为false可自定义全屏行为 |     Bool     |    no    | iOS/Android |        yes        |
| controlAnimationTiming       | 控制界面动画显示和隐藏的时间（毫秒） |     Int      |    no    | iOS/Android |        yes        |
| doubleTapTime                | 在此时间（毫秒）内双击被视为双击操作，在此时间到期前不会执行单击操作 |     Int      |    no    | iOS/Android |        yes        |
| controlTimeout               | 在指定时间（毫秒）后隐藏控制界面         |     Int      |    no    | iOS/Android |        yes        |
| scrubbing                    | 如果大于0，移动进度条时启用实时拖动。提供的值是以毫秒为单位的拖动最小时间步长 |     Int      |    no    | iOS/Android |        yes        |
| showOnStart                  | 首次渲染时显示或隐藏控制界面                    |     Bool     |    no    | iOS/Android |        yes        |
| videoStyle                   | 附加到`<Video>`组件的React Native样式对象 |  StyleSheet  |    no    | iOS/Android |        yes        |
| navigator                    | 使用默认React Native导航器且未重写`onBack`函数时，需要将导航器传递给VideoPlayer才能正常工作 |  Navigator   |    no    | iOS/Android |        yes        |
| seekColor                    | 进度条的填充/手柄颜色                            | String(#HEX) |    no    | iOS/Android |        yes        |
| style                        | 附加到视频父`<View>`的React Native样式对象 |  StyleSheet  |    no    | iOS/Android |        yes        |
| tapAnywhereToPause           | 如果为true，在视频任意位置（控件除外）单击可在播放和暂停之间切换 |     Bool     |    no    | iOS/Android |        yes        |
| disableFullscreen            | 隐藏全屏按钮                                   |     Bool     |    no    | iOS/Android |        yes        |
| disablePlayPause             | 隐藏播放/暂停切换按钮                                   |     Bool     |    no    | iOS/Android |        yes        |
| disableSeekbar               | 隐藏进度条                                             |     Bool     |    no    | iOS/Android |        yes        |
| disableVolume                | 隐藏音量控制                                      |     Bool     |    no    | iOS/Android |        yes        |
| disableTimer                 | 隐藏计时器                                               |     Bool     |    no    | iOS/Android |        yes        |
| disableBack                  | 隐藏返回按钮                                         |     Bool     |    no    | iOS/Android |        yes        |
| onEnterFullscreen            | 按下全屏按钮后视频进入全屏时触发 |    Event     |    no    | iOS/Android |        yes        |
| onExitFullscreen             | 按下全屏按钮后视频退出全屏时触发 |    Event     |    no    | iOS/Android |        yes        |
| onHideControls               | 控制界面消失时触发                            |    Event     |    no    | iOS/Android |        yes        |
| onShowControls               | 控制界面出现时触发                               |    Event     |    no    | iOS/Android |        yes        |
| onError                      | 加载视频时遇到错误时触发    |    Event     |    no    | iOS/Android |        yes        |
| onPause                      | 按下播放/暂停按钮后视频暂停时触发 |    Event     |    no    | iOS/Android |        yes        |
| onPlay                       | 按下播放/暂停按钮后视频开始播放时触发 |    Event     |    no    | iOS/Android |        yes        |
| onBack                       | 按下返回按钮时触发的函数，使用自定义导航时可重写此函数 |    Event     |    no    | iOS/Android |        yes        |
| onEnd                        | 视频播放完成时触发                             |    Event     |    no    | iOS/Android |        yes        |

## 遗留问题

## 其他

+ 源库未提供navigator属性功能实现也未提及该属性的依赖，但可由navigation相关库提供该属性的功能，在使用时请参照[react-navigation-stack文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-navigation-stack.md)和[react-navigation-native文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-navigation-native.md)引入navigation相关库。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/itsnubix/react-native-video-controls/blob/master/LICENSE) ，请自由地享受和参与开源。