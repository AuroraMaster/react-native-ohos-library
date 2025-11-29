模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-image-pan-zoom</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/ascoders/react-native-image-zoom/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ascoders/react-native-image-zoom/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-zoom)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                   | Package Name                                  | Repository                                                                                | Release                                                                                                     | RN version |
| ------------------------- | --------------------------------------------- | ----------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------- | ---------- |
| 2.1.12 | @react-native-ohos/react-native-image-pan-zoom | [Github](https://github.com/react-native-oh-library/react-native-image-zoom) | [Github Releases](https://github.com/react-native-oh-library/react-native-image-zoom/releases) | 0.72 |
| 2.2.0  | @react-native-ohos/react-native-image-pan-zoom   | [Github](https://github.com/react-native-oh-library/react-native-image-zoom) | [Github Releases](https://github.com/react-native-oh-library/react-native-image-zoom/releases)   | 0.77 |


对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
#0.72
npm install @react-native-oh-tpl/react-native-image-pan-zoom

#0.77
npm install @react-native-ohos/react-native-image-pan-zoom
```

#### **yarn**

```bash
#0.72
yarn add @react-native-oh-tpl/react-native-image-pan-zoom
#0.77
yarn add @react-native-ohos/react-native-image-pan-zoom
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React from "react"
import { Image, Text, Button } from "react-native"
import ImageZoom from "react-native-image-pan-zoom"
export default function () {
  const [cropWidth, setCropWidth] = React.useState<number>(300)
  const [cropHeight, setCropHeight] = React.useState<number>(300)
  const [imageWidth, setImageWidth] = React.useState<number>(600)
  const [imageHeight, setImageHeight] = React.useState<number>(600)
  const [panToMove, setPanToMove] = React.useState<boolean>(false)

  return (
    <>
      <Text>{`panToMove value: ${panToMove} `}</Text>
      <ImageZoom
        cropWidth={cropWidth}
        cropHeight={cropHeight}
        imageWidth={imageWidth}
        imageHeight={imageHeight}
        enableDoubleClickZoom={false}
        panToMove={panToMove}
        enableCenterFocus={false}
        pinchToZoom={false}
      >
        <Image
          style={{
            width: imageWidth,
            height: imageHeight,
          }}
          source={{
            uri: "https://img0.baidu.com/it/u=3570889183,2260151218&fm=253&fmt=auto&app=138&f=JPEG?w=800&h=500",
          }}
        />
      </ImageZoom>
      <Button
        title="change panToMove value"
        onPress={() => setPanToMove(!panToMove)}
      />
    </>
  )
}
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-image-zoom](https://github.com/ascoders/react-native-image-zoom)

ImageZoom

| Name   | Description          | Type          | Required | Platform | HarmonyOS Support |   
| ---- | ------------------ | ----------------------- | -------- | -------- | ----------------- | 
| **cropWidth**   | 操作区域宽度              | number      | YES      | ALL      | YES    |           
| **cropHeight**           | 操作区域高度                                                                                                                                                 | number                                                                                                                             | YES      | ALL      | YES               |                                                                                            
| **imageWidth**           | 图片宽度                                                                                                                                                         | number                                                                                                                             | YES      | ALL      | YES                                                                                                           
| **imageHeight**          | 图片高度                                                                                                                                                        | number                                                                                                                             | YES      | ALL      | YES                                                                                                           |
| `onClick`                          | 点击事件                                                                                                                                                               | (eventParams: [IOnClick](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts))=>void | NO       | ALL      | YES                                                                                                           |
| `onDoubleClick`                    | 双击事件                                                                                                                                                         | (eventParams: IOnClick)=>void                                                                                                      | NO       | ALL      | YES               |                                                                                            
| `panToMove`                        | 支持单指移动图片                                                                                                                                | boolean                                                                                                                            | NO       | ALL      | YES               |                                                                                            
| `pinchToZoom`                      | 支持双指缩放                                                                                                                                       | boolean                                                                                                                            | NO       | ALL      | YES               |                                                                                            
| `enableDoubleClickZoom`            | 支持双击放大                                                                                                                                         | boolean                                                                                                                            | NO       | ALL      | YES               |                                                                                            
| `clickDistance`                    | 多少指移动仍可触发 onClick 事件                                                                                                                  | number                                                                                                                             | NO       | ALL      | YES               |                                                                                            
| `horizontalOuterRangeOffset`       | 当水平滑动距离超出阈值时，将触发父组件的图片切换功能。您可监听此函数，待触发时执行切换操作。 | (offsetX?: number)=>void                                                                                                           | NO       | ALL      | YES               |                                                                                            
| `onDragLeft`                       | 当左滑速度超过阈值时，触发图表向左切换功能                                                               | ()=>void                                                                                                                           | NO       | \        | NO                | 
| `responderRelease`                 | 释放未取消                                                                                                                                              | (vx: number)=>void                                                                                                                 | NO       | ALL      | YES               |                                                                                            
| `maxOverflow`                      | 最大滑动阈值                                                                                                                                             | number                                                                                                                             | NO       | ALL      | YES               |                                                                                            
| `longPressTime`                    | 长按阈值                                                                                                                                                  | number                                                                                                                             | NO       | ALL      | YES               |                                                                                            
| `onLongPress`                      | 长按事件处理函数                                                                                                                                                          | (eventParams: [IOnClick](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts))=>void | NO       | ALL      | YES               |                                                                                            
| `doubleClickInterval	`              | 判断为双击事件的二次点击时间容限                                                                                                  | number                                                                                                                             | NO       | ALL      | YES               |                                                                                            
| `onMove`                           | 上报移动位置数据（可用于构建叠加层）                                                                                                            | ( position: [IOnMove](https://github.com/ascoders/react-native-image-zoom/blob/master/src/image-zoom/image-zoom.type.ts) )=>void   | NO       | ALL      | YES               |                                                                                            
| `centerOn`                         | 若提供此参数，地图将自动平移缩放至指定位置                                                                                              | { x: number, y: number, scale: number, duration: number }                                                                          | NO       | ALL      | YES               |                                                                                            
| `enableSwipeDown`                  | 用于在用户无需时启用垂直移动功能                                                                                                                | boolean                                                                                                                            | NO       | ALL      | YES               |                                                                                            
| `enableCenterFocus`                | 用于在用户无需时禁用图像居中聚焦功能                                                                                                           | boolean                                                                                                                            | NO       | ALL      | YES               |                                                                                            
| `onSwipeDown`                      | 用户下滑时触发的回调函数                                                                                                                             | () => void                                                                                                                         | NO       | ALL      | YES               |                                                                                            
| `swipeDownThreshold`               | 触发下滑功能的阈值                                                                                                                              | number                                                                                                                             | NO       | ALL      | YES               |                                                                                            
| `minScale`                         | 最小缩放比例                                                                                                                                                    | number                                                                                                                             | NO       | ALL      | YES               |                                                                                            
| `maxScale`                         | 最大缩放比例                                                                                                                                                    | number                                                                                                                             | NO       | ALL      | YES               |                                                                                            
| `useNativeDriver`                  | 是否使用 [`useNativeDriver`](https://reactnative.dev/docs/animations#using-the-native-driver)                                                         | boolean                                                                                                                            | NO       | ALL      | YES               |                                                                                            
| `onStartShouldSetPanResponder`     | 重写 onStartShouldSetPanResponder 行为                                                                                                                        | () => boolean                                                                                                                      | NO       | ALL      | YES               |                                                                                            
| `onMoveShouldSetPanResponder`      | 重写 onMoveShouldSetPanResponder 行为                                                                                                                         | () => boolean                                                                                                                      | NO       | ALL      | YES               |                                                                                            
| `onPanResponderTerminationRequest` | 重写 onPanResponderTerminationRequest 行为                                                                                                                    | () => boolean                                                                                                                      | NO       | ALL      | YES               |                                                                                            
| `useHardwareTextureAndroid`        | 用于禁用Android硬件纹理渲染                                                                                                                | boolean                                                                                                                            | NO       | Android  | NO                |                                                                      


| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| reset      | 重置图片位置与缩放比例     | () => void  | NO      | iOS/Android | YES               |
| resetScale      |  重置图片缩放比例   | () => void  | NO      | iOS/Android | YES               |
| centerOn      | 将图像居中定位至指定坐标。ICenterOn={ x: 数值, y: 数值, 缩放比例: 数值, 持续时间: 数值 }    | ICenterOn | NO      | iOS/Android | YES               |



## 遗留问题

- [x] 双指缩放在 harmony 框架侧不支持使用 [issues#1](https://github.com/react-native-oh-library/react-native-image-zoom/issues/1)

- [x] 长按图片后，rn 框架图片拖拽属性导致程序崩溃 [issues#2](https://github.com/react-native-oh-library/react-native-image-zoom/issues/2)

- [x] onPanResponderTerminationRequest 方法，harmony 端与 android 端表现不一致 [issues#3](https://github.com/react-native-oh-library/react-native-image-zoom/issues/3)


## 其他

- 下滑图片，然后双击放大，再次下滑表现异常，已在源库基础上修改[上库地址](https://github.com/react-native-oh-library/react-native-image-zoom)，源库已被存档，不能新建 issue，特此记录

- onDragLeft 此回调函数源码未实现，详见:[issues#103](https://github.com/ascoders/react-native-image-zoom/issues/103)

- useHardwareTextureAndroid 此属性仅 Android 生效

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ascoders/react-native-image-zoom/blob/master/LICENSE) ，请自由地享受和参与开源。
