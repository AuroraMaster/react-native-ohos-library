> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-graph</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/margelo/react-native-graph">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/margelo/react-native-graph/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/margelo/react-native-graph)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.1.0     | [react-native-graph release](https://github.com/margelo/react-native-graph/releases) | 0.72/0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。


进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install react-native-graph@1.1.0
```

#### **yarn**

```bash
yarn add react-native-graph@1.1.0
```

下面的代码展示了这个库的基本使用场景：

```ts
import React, {  useState } from 'react'
import { View, StyleSheet, Text, Button } from 'react-native'
import { LineGraph } from 'react-native-graph'
import { GestureHandlerRootView } from 'react-native-gesture-handler';

interface GraphPoint {
    value: number
    date: Date
  }
interface GraphXRange {
    min: Date;
    max: Date;
}
interface GraphYRange {
    min: number;
    max: number;
}
interface GraphPathRange {
    x: GraphXRange;
    y: GraphYRange;
}
type GraphRange = Partial<GraphPathRange>;
type Color = string | Float32Array | number | number[];

export default function() {
    const generateRandomGraphData=(length: number): GraphPoint[]=>{
        return Array<number>(length)
          .fill(0)
          .map((_, index) => ({
            date: new Date(
              new Date(2000, 0, 1).getTime() + 1000 * 60 * 60 * 24 * index
            ),
            value: Math.random()*10,
          }))
      }
    const POINT_COUNT=50
      const POINTS = generateRandomGraphData(POINT_COUNT)
      const [points, setPoints] = useState(POINTS)
      const [isAnimated, setIsAnimated] = useState(true)
      const [enablePanGesture, setEnablePanGesture] = useState(false)

      const color='#dd4400'
  
      
    return (
        <View style={{ flex: 1 }}>
    <GestureHandlerRootView style={{ flex: 1 }}>
        <Text>{`enablePanGesture value is ${enablePanGesture}`}</Text>
        <LineGraph 
        style={styles.graph}
        animated={isAnimated}
        color={color}
        points={points}
        enablePanGesture={enablePanGesture}
        />
        <Button title='change enablePanGesture' onPress={()=>setEnablePanGesture(!enablePanGesture)} />
     </GestureHandlerRootView>
    </View>
    )

}

const styles = StyleSheet.create({

    graph: {
        alignSelf: 'center',
        width: '100%',
        aspectRatio: 1.4,
        marginVertical: 20,
      },
})
```

### 配置 CMakeLists

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
+ cmake_minimum_required(VERSION 3.5)
set(CMAKE_SKIP_BUILD_RPATH TRUE)

## Link

本库 HarmonyOS 侧实现依赖react-native-reanimated , react-native-gesture-handler , react-native-skia 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-reanimated文档](/zh-cn/react-native-reanimated.md)、[react-native-gesture-handler文档](/zh-cn/react-native-gesture-handler.md)、[react-native-skia文档](/zh-cn/react-native-skia.md)、进行引入
## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                          | Description                                     | Type     | Required | Platform    | HarmonyOS Support |
| ----------------------------- | ----------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `animated` | 是否在数据变化时启用动画效果 | Boolean   | yes       | iOS/Android | yes               |
| `points` | 图表中要标记的所有点。坐标系会自动调整以适应缩放 | GraphPoint[]   | yes       | iOS/Android | yes               |
| `color`| 图表线条（路径）的颜色 | String   | yes       | iOS/Android | yes               |
| `enableFadeInMask` | 在图表开头启用淡入渐变效果 | Boolean| no       | iOS/Android | yes               |
| `lineThickness` | 图表线条（路径）的宽度 | Number | no       | iOS/Android | yes               |
| `gradientFillColors` | 图表线条下方填充渐变的颜色（可选） | Color[] | no       | iOS/Android | yes               |
| `range` | 图表x轴和y轴的范围。范围必须大于点给定的范围 | GraphRange | no       | iOS/Android | yes               |
| `enablePanGesture`| 是否启用手势拖拽（animated属性必须为true） | Boolean   | no       | iOS/Android | yes               |
| `horizontalPadding` | 应用于图表的水平内边距，防止拖拽点被水平截断（animated属性必须为true） | Number   | no       | iOS/Android | yes               |
| `verticalPadding`| 应用于图表的垂直内边距，防止拖拽点被垂直截断（animated属性必须为true） | Number  | no       | iOS/Android | yes               |
| `enableIndicator`| 启用显示在图表末端的指示器（animated属性必须为true） | Boolean  | no       | iOS/Android | yes               |
| `indicatorPulsating`  | 让指示器产生脉动效果（animated GraphEnableIndicator属性必须为true） | Boolean  | no       | iOS/Android | yes               |
| `panGestureDelay`| 拖拽手势开始前的延迟时间（animated enablePanGesture属性必须为true） | Number  | no       | iOS/Android | yes               |
| `onPointSelected`  | 当用户在图表中滑动/拖拽时，为每个点调用的回调函数（animated enablePanGesture属性必须为true） | (point: GraphPoint) => void | no       | iOS/Android | yes               |
| `onGestureStart` | 当用户开始在图表中滑动/拖拽时调用（animated enablePanGesture属性必须为true） | () => void | no       | iOS/Android | yes               |
| `onGestureEnd` | 当用户停止在图表中滑动/拖拽时调用（animated enablePanGesture属性必须为true） | () => void | no       | iOS/Android | yes               |
| `SelectionDot`| 渲染选择点的元素（animated enablePanGesture属性必须为true） | React.ComponentType\<SelectionDotProps> \| null | no       | iOS/Android | yes               |
| `TopAxisLabel` | 渲染在图表上方的元素（通常是图表的"最大"点/值）（animated属性必须为true） | React.ReactElement \| null | no       | iOS/Android | yes               |
| `BottomAxisLabel` | 渲染在图表下方的元素（通常是图表的"最小"点/值）（animated属性必须为true） | React.ReactElement \| null | no       | iOS/Android | yes               |



## 遗留问题

- [ ] 依赖手势库的三方库，单击图表后会出现手势指示点出现BUG的情况，会页面卡住无法点击组件中按钮再次点击回归正常，需要等待手势库更新后正常 [issues#38](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/issues/38)

## 其他
- react-native-graph 的animated属性 原库代码现在有问题 无论是false还是true，数据变化都是静态变化，没有动画效果，原库中有使用者提issue和PR，添加合入相应PR代码后才能动画正常[issue#111](https://github.com/margelo/react-native-graph/pull/111)
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/margelo/react-native-graph/blob/main/LICENSE) ，请自由地享受和参与开源。

