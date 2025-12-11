> Template Version: v0.2.2
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

> [!TIP] [Github Address](https://github.com/margelo/react-native-graph)

## Installation and Usage

Please check the corresponding version information in the third-party library's Releases:

| Third-party Library Version | Release Information | Supported RN Version |
| --------------------------- | ------------------- | -------------------- |
| 1.1.0                       | [react-native-graph release](https://github.com/margelo/react-native-graph/releases) | 0.72/0.77            |

For older versions not published to npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Navigate to your project directory and enter the following commands:

#### **npm**

```bash
npm install react-native-graph@1.1.0
```

#### **yarn**

```bash
yarn add react-native-graph@1.1.0
```

The following code demonstrates basic usage scenarios of this library:

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

### Config CMakeLists

Open `entry/src/main/cpp/CMakeLists.txt`, add：

```diff
project(rnapp)
+ cmake_minimum_required(VERSION 3.5)
set(CMAKE_SKIP_BUILD_RPATH TRUE)

## Link

The HarmonyOS implementation of this library depends on the native code of react-native-reanimated, react-native-gesture-handler, and react-native-skia. If these libraries have already been introduced in your HarmonyOS project, you do not need to introduce them again and can skip this section to start using directly.

If not introduced, please refer to:
- [react-native-reanimated Documentation](/zh-cn/react-native-reanimated.md)
- [react-native-gesture-handler Documentation](/zh-cn/react-native-gesture-handler.md)  
- [react-native-skia Documentation](/zh-cn/react-native-skia.md)

## Constraints and Limitations

### Compatibility

To use this library, you need to use the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified in the following versions:

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library for this property.

> [!TIP] "HarmonyOS Support" being yes means the property is supported on HarmonyOS platform; no means not supported; partially means partially supported. The usage method is consistent across platforms, with effects benchmarked against iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
|------|-------------|------|----------|----------|-------------------|
| `animated` | Whether to enable animation effects when data changes | Boolean | yes | iOS/Android | yes |
| `points` | All points to be marked in the graph. Coordinate system will adjust to scale automatically | GraphPoint[] | yes | iOS/Android | yes |
| `color` | Color of the graph line (path) | String | yes | iOS/Android | yes |
| `enableFadeInMask` | Enable the Fade-In Gradient Effect at the beginning of the Graph | Boolean | no | iOS/Android | yes |
| `lineThickness` | The width of the graph line (path) | Number | no | iOS/Android | yes |
| `gradientFillColors` | (Optional) Colors for the fill gradient below the graph line | Color[] | no | iOS/Android | yes |
| `range` | Range of the graph's x and y-axis. The range must be greater than the range given by the points | GraphRange | no | iOS/Android | yes |
| `enablePanGesture` | Whether to enable the pan gesture (animated Property must be true) | Boolean | no | iOS/Android | yes |
| `horizontalPadding` | Horizontal padding applied to graph, so the pan gesture dot doesn't get cut off horizontally (animated Property must be true) | Number | no | iOS/Android | yes |
| `verticalPadding` | Vertical padding applied to graph, so the pan gesture dot doesn't get cut off vertically (animated Property must be true) | Number | no | iOS/Android | yes |
| `enableIndicator` | Enables an indicator which is displayed at the end of the graph (animated Property must be true) | Boolean | no | iOS/Android | yes |
| `indicatorPulsating` | Let's the indicator pulsate (animated GraphEnableIndicator Property must be true) | Boolean | no | iOS/Android | yes |
| `panGestureDelay` | Delay after which the pan gesture starts (animated enablePanGesture Property must be true) | Number | no | iOS/Android | yes |
| `onPointSelected` | Called for each point while the user is scrubbing/panning through the graph (animated enablePanGesture Property must be true) | (point: GraphPoint) => void | no | iOS/Android | yes |
| `onGestureStart` | Called once the user starts scrubbing/panning through the graph (animated enablePanGesture Property must be true) | () => void | no | iOS/Android | yes |
| `onGestureEnd` | Called once the user stopped scrubbing/panning through the graph (animated enablePanGesture Property must be true) | () => void | no | iOS/Android | yes |
| `SelectionDot` | The element that renders the selection dot (animated enablePanGesture Property must be true) | React.ComponentType\<SelectionDotProps> \| null | no | iOS/Android | yes |
| `TopAxisLabel` | The element that gets rendered above the Graph (usually the "max" point/value of the Graph) (animated Property must be true) | React.ReactElement \| null | no | iOS/Android | yes |
| `BottomAxisLabel` | The element that gets rendered below the Graph (usually the "min" point/value of the Graph) (animated Property must be true) | React.ReactElement \| null | no | iOS/Android | yes |

## Known Issues

- [ ] For third-party libraries that depend on the gesture library, after clicking on the graph, there is a BUG where the gesture indicator point appears, causing the page to freeze and unable to click buttons in the component. It returns to normal after clicking again. This needs to be fixed after the gesture library is updated [issues#38](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/issues/38)

## Others

- The animated property of react-native-graph currently has issues in the original library code. Whether false or true, data changes are static without animation effects. Users have raised issues and PRs in the original library. Animation will work normally only after the corresponding PR code is merged [issue#111](https://github.com/margelo/react-native-graph/pull/111)

## License

This project is based on [The MIT License (MIT)](https://github.com/margelo/react-native-graph/blob/main/LICENSE). Feel free to enjoy and participate in open source.