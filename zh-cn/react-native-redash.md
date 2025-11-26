> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-redash</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wcandillon/react-native-redash">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wcandillon/react-native-redash/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/wcandillon/react-native-redash/tree/v18.1.3)

| Version   | Support RN version |
| ------------ | ---------- |
| 18.1.3       | 0.72/0.77   |

## 安装与使用

#### **yarn**

```bash
yarn add react-native-redash@18.1.3
```

#### **npm**

```bash
npm install react-native-redash@18.1.3
```

下面的代码展示了这个库的基本使用场景：

```js
import { mix,
    round,
    bin,
    cubicBezier,
    clamp,
    between,
    avg,
    toRad,
    toDeg} from 'react-native-redash/src/Math';
  import {
    canvas2Cartesian,
    canvas2Polar,
    cartesian2Canvas,
    cartesian2Polar,
    polar2Canvas,
    polar2Cartesian
  } from 'react-native-redash/src/Coordinates';
  import * as redash from 'react-native-redash';
  import React, { useState } from 'react';
  import { Button, ScrollView, StyleSheet, Text, View } from 'react-native';
  export default function RadashDemo() {
    const [text, setText] = useState('');
  
    const onMix = () => {
        const mixre = mix(0, 10, 20);
        setText(mixre.toString())
    }
  
    const onRoundre = () => {
        const roundre = round(5.123, 0);
        setText(roundre.toString())
    }
  
    const onBinre = () => {
        const binre = bin(true);
        setText(binre.toString())
    }
  
    const onBetweenre = () => {
        const betweenre = between(-1, 0, 100);
        setText(betweenre.toString())
    }
  
    const onToRadre = () => {
        const toRadre = toRad(180);
        setText(toRadre.toString())
    }
  
    const onToDegre = () => {
        const toDegre = toDeg(Math.PI);
        setText(toDegre.toString())
    }
  
    const onClampre = () => {
        const clampre = clamp(-1, 0, 100)
        setText(clampre.toString())
    }
  
    const avgre = () => {
        const values: number[] = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
        const avgs = avg(values)
        setText(avgs.toString())
    }
  
    const cubicBezires = () => {
        const cubicBezire = cubicBezier(1, 0, 0.1, 0.1, 1)
        setText(cubicBezire.toString())
    }
  
    const handleCreatePath = () => {
        const vector = {
            x: 10,
            y: 20
        };
        setText(JSON.stringify(redash.createPath(vector)))
    }
  
    const handleAddCurvePath = () => {
        const vector = {
            x: 200,
            y: 100
        };
        const path = redash.createPath(vector);
        redash.addCurve(path, { c1: { x: 50, y: 50 }, c2: { x: 150, y: 50 }, to: { x: 150, y: 150 } });
        setText(JSON.stringify(path))
    }
  
    const handleClosePath = () => {
        const vector = {
            x: 200,
            y: 100
        };
        const path = redash.createPath(vector);
        redash.addCurve(path, { c1: { x: 50, y: 50 }, c2: { x: 150, y: 50 }, to: { x: 150, y: 150 } });
        redash.close(path);
        setText(JSON.stringify(path))
    }
  
    const handleSerializePath = () => {
        const vector = {
            x: 200,
            y: 100
        };
        const path = redash.createPath(vector);
        redash.addCurve(path, { c1: { x: 50, y: 50 }, c2: { x: 150, y: 50 }, to: { x: 150, y: 150 } });
        redash.close(path);
        const serializePath = redash.serialize(path);
        setText(serializePath)
    }
  
    const handleParsePath = () => {
        const vector = {
            x: 200,
            y: 100
        };
        const path = redash.createPath(vector);
        redash.addCurve(path, { c1: { x: 50, y: 50 }, c2: { x: 150, y: 50 }, to: { x: 150, y: 150 } });
        redash.close(path);
        const serializePath = redash.serialize(path);
        const parsePath = redash.parse(serializePath);
        setText(JSON.stringify(parsePath))
    }
  
    const handleInterpolatePath = () => {
        const inputRange = [0, 1];
        const outputRange = [
            {
                move: { x: 0, y: 0 },
                curves: [{ c1: { x: 1, y: 1 }, c2: { x: 2, y: 2 }, to: { x: 3, y: 3 } }],
                close: false,
            },
            {
                move: { x: 1, y: 1 },
                curves: [{ c1: { x: 2, y: 2 }, c2: { x: 3, y: 3 }, to: { x: 4, y: 4 } }],
                close: false,
            },
        ];
        const value = 0.5;
        const interpolatePath = redash.interpolatePath(value, inputRange, outputRange);
        setText(JSON.stringify(interpolatePath))
    }
  
    const handleCanvas2Cartesian = () => {
        const point = canvas2Cartesian({ x: 500, y: 200 }, { x: 500, y: 200 });
        setText(JSON.stringify(point))
    }
    const handleCartesian2Canvas = () => {
        const point = cartesian2Canvas({ x: -500, y: 200 }, { x: 500, y: 200 });
        setText(JSON.stringify(point))
    }
    /** 用于处理笛卡尔坐标转换为极坐标 */
    const handleCartesian2Polar = () => {
        const x = 0;
        const y = 100;
        const center = { x: 100, y: 100 };
        const { theta, radius } = cartesian2Polar(canvas2Cartesian({ x, y }, center));
        setText('theta ==' + theta + "  radius==" + radius);
    }
  
    const handlePolar2Cartesian = () => {
        const x = 0;
        const y = 100;
        const center = { x: 100, y: 100 };
        const { theta, radius } = cartesian2Polar(canvas2Cartesian({ x, y }, center));
        const { x: x1, y: y1 } = cartesian2Canvas(
            polar2Cartesian({ theta, radius }),
            center
        );
        setText('x1 ==' + x1 + "  Math.round(y1)==" + Math.round(y1));
    }
  
    const handlePolar2Canvas = () => {
        const x = 0;
        const y = 100;
        const center = { x: 100, y: 100 };
        const { theta, radius } = cartesian2Polar(canvas2Cartesian({ x, y }, center));
        const point = polar2Canvas({ theta, radius }, center)
        setText(JSON.stringify(point))
    }
  
    const handleCanvas2Polar = () => {
        const { theta, radius } = canvas2Polar({ x: -500, y: 200 }, { x: 500, y: 200 });
        setText('theta ==' + theta + "  radius==" + radius);
    }
  
    return (
      <View style={styles.container}>
        <View style={styles.inputArea}>
            <Text style={styles.baseText}>
                {text}
            </Text>
        </View>
        <ScrollView style={styles.scrollView}>
          <View style={{ flexDirection: 'column' }}>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>mix(0, 10, 20)</Text>
                <Button title='start' color='#841584' onPress={onMix}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>round(5.123, 0)</Text>
                <Button title='start' color='#841584' onPress={onRoundre}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>bin(true)</Text>
                <Button title='start' color='#841584' onPress={onBinre}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>between(-1, 0, 100)</Text>
                <Button title='start' color='#841584' onPress={onBetweenre}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>toRad(180)</Text>
                <Button title='start' color='#841584' onPress={onToRadre}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>avg([1,2,3,4,5,6,7,8,9,10])</Text>
                <Button title='start' color='#841584' onPress={avgre}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>cubicBezier(1, 0, 0.1, 0.1, 1)</Text>
                <Button title='start' color='#841584' onPress={cubicBezires}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>toDeg(Math.PI)</Text>
                <Button title='start' color='#841584' onPress={onToDegre}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>clamp(-1, 0, 100)</Text>
                <Button title='start' color='#841584' onPress={onClampre}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>mix(0, 10, 20)</Text>
                <Button title='start' color='#841584' onPress={handleCreatePath}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>addCurvePath</Text>
                <Button title='start' color='#841584' onPress={handleAddCurvePath}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>closePath</Text>
                <Button title='start' color='#841584' onPress={handleClosePath}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>serializePath</Text>
                <Button title='start' color='#841584' onPress={handleSerializePath}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>parsePath</Text>
                <Button title='start' color='#841584' onPress={handleParsePath}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>interpolatePath</Text>
                <Button title='start' color='#841584' onPress={handleInterpolatePath}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>canvas2Cartesian</Text>
                <Button title='start' color='#841584' onPress={handleCanvas2Cartesian}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>cartesian2Canvas</Text>
                <Button title='start' color='#841584' onPress={handleCartesian2Canvas}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>cartesian2Polar</Text>
                <Button title='start' color='#841584' onPress={handleCartesian2Polar}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>polar2Cartesian</Text>
                <Button title='start' color='#841584' onPress={handlePolar2Cartesian}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>polar2Canvas</Text>
                <Button title='start' color='#841584' onPress={handlePolar2Canvas}></Button>
            </View>
            <View style={styles.baseArea}>
                <Text style={{ flex: 1 }}>canvas2Polar</Text>
                <Button title='start' color='#841584' onPress={handleCanvas2Polar}></Button>
            </View>
          </View>
        </ScrollView>
      </View>
    );
  }
  
  const styles = StyleSheet.create({
    container: {
        width: '100%',
        flexDirection: 'column',
        alignItems: 'center',
        backgroundColor: '#F1F3F5',
    },
    baseText: {
        fontWeight: 'bold',
        textAlign: 'center',
        fontSize: 16
    },
  
    titleArea: {
        alignItems: 'center',
        flexDirection: 'row',
    },
  
    title: {
        width: '90%',
        color: '#000000',
        textAlign: 'left',
        fontSize: 30,
    },
  
    scrollView: {
        width: '90%',
        marginHorizontal: 20,
    },
  
    inputArea: {
        width: '90%',
        height: 30,
        borderWidth: 2,
        borderColor: '#000000',
        marginTop: 8,
        justifyContent: 'center',
        alignItems: 'center',
    },
  
    baseArea: {
        width: '100%',
        height: 60,
        borderRadius: 4,
        borderColor: '#000000',
        marginTop: 8,
        backgroundColor: '#FFFFFF',
        flexDirection: 'row',
        alignItems: 'center',
        paddingLeft: 8,
        paddingRight: 8
    }
  });
```

动画演示示例

1.位置移动演示动画，通过snapPoint运行指定的位置地点

```js
import { View, Button, StyleSheet } from 'react-native';
import { snapPoint } from "react-native-redash/src/Physics";
import {
  useSharedValue,
  withSequence,
  withTiming,
  withRepeat,
  useAnimatedStyle,
  cancelAnimation,
} from "@react-native-oh-tpl/react-native-reanimated";

export default function RadashDemo() {
  const offset = useSharedValue(0);

  const translateAnimatedStyles = useAnimatedStyle(() => {
    return {
      transform: [
        {
          translateX: offset.value * 2,
        },
      ],
    };
  });

  const translate = () => {
    offset.value = withSequence(
      withTiming(-snapPoint(96, 600, [0, 125, 393]), { duration: 1000 }),
      withRepeat(
        withTiming(snapPoint(96, 600, [0, 125, 393]), { duration: 1000 }),
        60,
        true,
      ),
      withTiming(0, { duration: 50 }),
    );
  };

  return (
    <View style={styles.container}>
      <View style={styles.baseArea}>
        <View>
            <Animated.View style={[styles.box, translateAnimatedStyles]} />
        </View>
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            <View style={{ marginRight: 10 }}>
                <Button color='#841584' onPress={() => translate()} title="snapPoint start" />
            </View>
            <View>
                <Button color='#841584' onPress={() => cancelAnimation(offset)} title="back" />
            </View>
        </View>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    flexDirection: 'column',
    alignItems: 'center',
    backgroundColor: '#F1F3F5',
  },
  baseArea: {
    width: '100%',
    height: 60,
    borderRadius: 4,
    borderColor: '#000000',
    marginTop: 8,
    backgroundColor: '#FFFFFF',
    flexDirection: 'row',
    justifyContent: 'space-between',
    paddingLeft: 8,
    paddingRight: 8
  },
  box: {
    height: 40,
    width: 40,
    marginBottom: 20,
    backgroundColor: '#b58df1',
    borderRadius: 5,
  }
});
```

2.颜色渐变动画演示，通过mixColor进行颜色渐变

```js
import { mixColor } from "react-native-redash/src/Colors";
import { useSharedValue } from "@react-native-oh-tpl/react-native-reanimated";

export default function RadashDemo() {
  const progress = useSharedValue(0);

  const colorAnimatedStyle = useAnimatedStyle(() => {
    return {
      backgroundColor: mixColor(progress.value, "#b58df1", "#38ffb3"),
    };
  });

  const handleColorPress = () => {
    progress.value = withRepeat(
      withTiming(1 - progress.value, { duration: 1000 }),
      60,
      true,
    );
  };


  return (
    <View style={styles.container}>
      <View style={styles.baseArea}>
        <View>
            <Animated.View style={[styles.box, translateAnimatedStyles]} />
        </View>
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            <View style={{ marginRight: 10 }}>
                <Button color='#841584' onPress={() => handleColorPress()} title="mixColor start" />
            </View>
        </View>
      </View>
    </View>
  );
}
```

3.redash目前有两个动画辅助方法：useTiming、useSpring。useTiming可以使用贝塞尔曲线来进行运动,useSpring可以不将持续时间作为参数，而是由sprin物理特性作为运动轨迹。

```js
import { useTiming, useSpring } from "react-native-redash/src/Transitions";
import Animated from "@react-native-oh-tpl/react-native-reanimated";

export default function RadashDemo() {
  const timing = useSpring(255, { duration: 1000 });
  const spring = useTiming(255, { duration: 1000 });

  const customSpringStyles = useAnimatedStyle(() => {
    return {
      transform: [
        {
          translateX: spring.value,
        },
      ],
    };
  });

  const customTimingStyles = useAnimatedStyle(() => {
    return {
      transform: [
        {
          translateX: timing.value,
        },
      ],
    };
  });

  return (
    <View>
      <Animated.View style={[styles.box, defaultSpringStyles]} />
      <Animated.View style={[styles.box, defaultTimingStyles]} />
    </View>
  );
}
```

4.redash提供能接受字符串动画节点属性的文本组件

```js
import { ReText } from "react-native-redash";
import { useSharedValue } from "@react-native-oh-tpl/react-native-reanimated";

export default function RadashDemo() {
  const price = useSharedValue(42);
  const formattedPrice = useDerivedValue(() => `${price.value}`.toLocaleString());

  return (
    <View>
      <ReText
        text={formattedPrice}
        style={{
          color: "black",
          backgroundColor: "#38ffb3",
        }}
      />
    </View>
  );
}
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-reanimated 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-reanimated 文档的 Link 章节](/zh-cn/react-native-reanimated.md#link)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过:

1. RNOH：0.72.28; SDK：HarmonyOS NEXT Developer Beta6 SDK 5.0.0.61; IDE：DevEco Studio 5.0.3.706; ROM：3.0.0.61;
2. RNOH：0.77.18; SDK：HarmonyOS 5.1.1 Release; IDE: DevEco Studio 5.1.1.830; ROM：NEXT 5.1.0.150; 

## 静态方法
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

如下是已验证接口展示:

### **Animations**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| withPause()                   | 使动画可暂停。动画的状态（暂停或未暂停）由布尔共享值控制。                  | function | No       | iOS/Android               | yes               |
| withBouncing()                | 为基于物理的动画添加弹跳行为。如果动画在其状态中包含速度，则该动画被定义为基于物理的动画。 | function | No       | iOS/Android               | yes               |
### **Coordinates**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| canvas2Cartesian() | 将平面坐标系转换为笛卡尔坐标系 | function | No       | iOS/Android               | yes               |
| cartesian2Canvas() | 将笛卡尔坐标系转换为平面坐标系 | function | No       | iOS/Android               | yes               |
| cartesian2Polar()  | 笛卡尔坐标系转换为极坐标系 | function | No       | iOS/Android               | yes               |
| polar2Cartesian()  | 将极坐标系转换为笛卡尔坐标系 | function | No       | iOS/Android               | yes               |
| polar2Canvas()     | 将极坐标系转换为平面坐标系 | function | No       | iOS/Android               | yes               |
| canvas2Polar()     | 将平面坐标系转换为极坐标系 | function | No       | iOS/Android               | yes               |
### **Strings**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| ReText | 该组件类似于 `<Text>`，但接受字符串动画节点作为属性。在幕后，`<ReText>` 使用带有一些默认样式的 `<TextInput>`。因此，与 `<Text>` 可能存在一些细微的不一致。 | function | No       | iOS/Android               | yes               |
### **Math**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| mix()              | mix 使用权重在 x 和 y 之间执行线性插值。返回值计算为 x * (1 - value) + y * value | function       | No       | iOS/Android               | yes               |
| bin()              | 将布尔值转换为数字。这在 reanimated 中可能很有用，因为 0 和 1 用于条件语句。 | function | No       | iOS/Android               | yes               |
| toRad()            | 将角度从度转换为弧度 | function | No       | iOS/Android               | yes               |
| toDeg()            | 将角度从弧度转换为度 | function | No       | iOS/Android               | yes               |
| clamp()            | 将节点限制在上下边界内 | function | No       | iOS/Android               | yes               |
| avg()              | 返回数组的平均值 | function | No       | iOS/Android               | yes               |
| between()          | 如果节点在 lowerBound 和 upperBound 范围内，则返回 true | function | No       | iOS/Android               | yes               |
| round()            | 计算动画节点四舍五入到指定精度 | function | No       | iOS/Android               | yes               |
| cubicBezier()      | 返回三次贝塞尔曲线的坐标。t 是从 0 到 1 的曲线长度。cubicBezier (0, p0, p1, p2, p3) 等于 p0，cubicBezier (1, p0, p1, p2, p3) 等于 p3。p0 和 p3 分别是曲线的起点和终点。p1 和 p2 是控制点。 | function | No       | iOS/Android               | yes               |
| cubicBezierYForX() | 给定一条三次贝塞尔曲线，返回 x 对应的 y 值 | function | No       | iOS/Android               | yes               |
### **Transitions**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| useTiming() | 过渡可以将动画值附加到 React 状态的变化上。 | function | No       | iOS/Android               | yes               |
| useSpring() | 过渡可以将动画值附加到 React 状态的变化上。 | function | No       | iOS/Android               | yes               |
### **Vectors**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| useVector() | 返回共享值的向量。 | function | No       | iOS/Android               | yes               |
### **Paths**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| createPath(path, {x, y})                             | 创建一个新路径 | function | No       | iOS/Android               | yes               |
| addCurve(path, {c1: {x, y}, c2: {x, y}, to: {x, y}}) | 向路径添加贝塞尔曲线命令 | function | No       | iOS/Android               | yes               |
| close(path)                                          | 向路径添加闭合命令 | function | No       | iOS/Android               | yes               |
| parse(path)                                          | 将 SVG 路径解析为一系列贝塞尔曲线。SVG 被规范化为具有绝对值，并近似为一系列贝塞尔曲线。 | function | No       | iOS/Android               | yes               |
| serialize(path)                                      | 将路径序列化为 SVG 路径字符串 | function | No       | iOS/Android               | yes               |
| interpolatePath()                                    | 在路径之间进行插值 | function | No       | iOS/Android               | yes               |
### **Physics**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| snapPoint() | 给定手势的值及其速度，选择动画应该吸附到的点。 | function | No       | iOS/Android               | yes               |
### **Colors**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| mixColor() | 与 interpolateColor () 相同，但动画值从 0 到 1。 | function | No       | iOS/Android               | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wcandillon/react-native-redash/blob/master/LICENSE) ，请自由地享受和参与开源。
