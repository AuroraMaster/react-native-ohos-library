> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-slider</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jeanregisser/react-native-slider">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jeanregisser/react-native-slider/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/jeanregisser-react-native-slider/tree/sig)

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-slider`，具体版本所属关系如下：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.11.0     | [@react-native-oh-tpl/react-native-slider Releases](https://github.com/react-native-oh-library/jeanregisser-react-native-slider/releases) | 0.72       |
| 0.12.0     | [@react-native-ohos/react-native-slider Releases]()          | 0.77       |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
#0.72
npm i @react-native-oh-tpl/react-native-slider

#0.77
npm i @react-native-ohos/react-native-slider
```

#### **yarn**

```bash
#0.72
yarn add @react-native-oh-tpl/react-native-slider

#0.77
yarn add @react-native-ohos/react-native-slider
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState} from 'react';
import {Button, View, StyleSheet, Text } from 'react-native';
import Slider from 'react-native-slider';


export function SliderExample() {
    const [isCheckerboardVisible, setIsCheckerboardVisible] = useState(false);
    const [value, setValue] = useState(0.200);
    return (
        <View style={styles.sectionContainer}>
        <Text>default style</Text>
        <Slider value={0.2}/>

        <Text>with min,max and custom tints</Text>
        <Slider
         value={0.2}
         minimumTrackTintColor = '#1A9274'
         maximumTrackTintColor = '#D3D3D3'
         thumbTintColor = '#1A9274'
         />

        <Text>with style,thumbStyle,thumbStyle</Text>
        <Slider
         value={0.2}
         minimumTrackTintColor = '#1073FF'
         thumbTintColor = '#FFFFFF'
         style = {styles.style}
         trackStyle = {styles.trackStyle}
         thumbStyle = {styles.thumbStyle}
         />

        <Text>with thumbTouchSize,event</Text>
        <Slider
            value={0.2}
            thumbTintColor = '#1A9FF4'
            thumbTouchSize = {{width: 40, height: 40}}
            onValueChange={(val: number) => {
                console.log('===Slider onValueChange: ' + value);
            }}

            onSlidingStart={() => {
                console.log('===Slider onSlidingStart');
            }}

            onSlidingComplete={() => {
                console.log('===Slider onSlidingComplete');
            }}
        />

        <Text>with thumbImage</Text>
        <Slider
            value={0.2}
            thumbTouchSize = {{width: 40, height: 40}}
            thumbStyle = {styles.thumbStyle}
            thumbImage = {require('./resources/slider.png')}
        />

        <Text>with animateTransitions</Text>
        <Slider
            value={value}
            thumbTouchSize = {{width: 40, height: 40}}
            trackStyle = {styles.trackStyle}
            thumbStyle = {styles.thumbStyle}
          // thumbImage = {{uri: 'https://developer.harmonyos.com/assets/image/diqiu.png'}}
            animateTransitions = {true}
            animationType = 'timing'
            animationConfig = {{
              toValue: 1,
              duration: 1500,
              useNativeDriver: false,
            }}
        />

        <Button onPress={()=>{
            setValue(0.9);
        }}
        title="动画测试"
        color="#841584"
        />
        </View>
    );
}

const styles = StyleSheet.create({
    sectionContainer: {
        marginTop: 32,
        paddingHorizontal: 24,
    },
    style: {
        backgroundColor: '#EECBA8',
    },
    trackStyle: {
        backgroundColor: '#D2D2D2',
        height:3
    },
    thumbStyle: {
        backgroundColor: '#F3F3F3',
        width: 30,
        height: 30,
        borderRadius: 15,
    }
  });
```

## 约束与限制

### 兼容性

在下述版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release SDK；IDE：DevEco Studio  6.0.0.868; ROM：6.0.0.112; 

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。
>
> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| value                 | 滑块的初始值。                                               | number                                                       | No       | iOS Android | yes               |
| disabled              | 如果为 true，用户将无法移动滑块。                            | bool                                                         | No       | iOS Android | yes               |
| minimumValue          | 滑块的初始最小值。                                           | number                                                       | No       | iOS Android | yes               |
| maximumValue          | 滑块的初始最大值。                                           | number                                                       | No       | iOS Android | yes               |
| step                  | 滑块的步长值。该值应在 0 到 (maximumValue - minimumValue) 之间。 | number                                                       | No       | iOS Android | yes               |
| minimumTrackTintColor | 滑块按钮左侧轨道的颜色。                                     | string                                                       | No       | iOS Android | yes               |
| maximumTrackTintColor | 滑块按钮右侧轨道的颜色。                                     | string                                                       | No       | iOS Android | yes               |
| thumbTintColor        | 滑块按钮（thumb）的颜色。                                    | string                                                       | No       | iOS Android | yes               |
| thumbTouchSize        | 允许移动滑块按钮的触摸区域大小。触摸区域的中心与可见的滑块按钮相同。这使得滑块按钮在视觉上可以很小，同时仍允许用户轻松移动它。 | object                                                       | No       | iOS Android | yes               |
| onValueChange         | 当用户拖动滑块时持续调用的回调函数。                         | function                                                     | No       | iOS Android | yes               |
| onSlidingStart        | 当用户开始更改值时调用的回调函数（例如，当滑块被按下时）。   | function                                                     | No       | iOS Android | yes               |
| onSlidingComplete     | 当用户完成更改值时调用的回调函数（例如，当滑块被释放时）。   | function                                                     | No       | iOS Android | yes               |
| style                 | 应用于滑块容器的样式。                                       | [style](http://facebook.github.io/react-native/docs/view.html#style) | No       | iOS Android | yes               |
| trackStyle            | 应用于轨道的样式。                                           | [style](http://facebook.github.io/react-native/docs/view.html#style) | No       | iOS Android | yes               |
| thumbStyle            | 应用于滑块按钮的样式。                                       | [style](http://facebook.github.io/react-native/docs/view.html#style) | No       | iOS Android | yes               |
| thumbImage            | 为滑块按钮设置一张图片。                                     | [source](http://facebook.github.io/react-native/docs/image.html#source) | No       | iOS Android | yes               |
| debugTouchArea        | 设置为 true 可以在视觉上看到绿色的滑块按钮触摸矩形区域。     | bool                                                         | No       | iOS Android | yes               |
| animateTransitions    | 如果希望使用默认的'spring' 动画，请设置为 true。             | bool                                                         | No       | iOS Android | yes               |
| animationType         | 设置为'spring' 或 'timing'，以使用这两种动画类型之一，并使用默认的 [动画属性](https://facebook.github.io/react-native/docs/animations.html)。 | string                                                       | No       | iOS Android | yes               |
| animationConfig       | 用于配置动画参数。这些参数与 [Animated 库](https://facebook.github.io/react-native/docs/animations.html) 中的参数相同。 | object                                                       | No       | iOS Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jeanregisser/react-native-slider/blob/master/LICENSE) ，请自由地享受和参与开源。

