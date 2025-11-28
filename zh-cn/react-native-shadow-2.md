> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-shadow-2</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/SrBrahma/react-native-shadow-2">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/SrBrahma/react-native-shadow-2/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/ftzi/react-native-shadow-2/tree/c9b373a4f46472a73f728c10a85d44aedba79793)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 7.0.8      | 0.72       |
| 7.1.1      | 0.77       |

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install react-native-shadow-2@7.0.8

# 0.77
npm install react-native-shadow-2@7.1.1
```

#### **yarn**

```bash
# 0.72
yarn add react-native-shadow-2@7.0.8

# 0.77
yarn add react-native-shadow-2@7.1.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import {Text, ScrollView, View, StyleSheet} from 'react-native';
import {Shadow} from 'react-native-shadow-2';
import React from 'react';

export function Shadow2Demo() {
  return (
    <ScrollView>
      <View style={styles.container}>
        <Text style={styles.title}>shadow2测试</Text>
        <View style={styles.sliders}>
          <Text style={styles.title}>base</Text>
          <Shadow>
            <Text style={styles.box}>base</Text>
          </Shadow>

          <Text style={styles.title}>startColor</Text>
          <Shadow startColor={'#eb9066d8'}>
            <Text style={styles.box}>startColor</Text>
          </Shadow>

          <Text style={styles.title}>endColor</Text>
          <Shadow endColor={'#ff00ff10'}>
            <Text style={styles.box}>endColor</Text>
          </Shadow>

          <Text style={styles.title}>distance</Text>
          <Shadow distance={50}>
            <Text style={styles.box}>distance</Text>
          </Shadow>

          <Text style={styles.title}>offset</Text>
          <Shadow offset={[50, 4]}>
            <Text style={styles.box}>offset</Text>
          </Shadow>

          <Text style={styles.title}>paintInside</Text>
          <Shadow style={styles.shadow} paintInside startColor={'#eb9066d8'}>
            <Text style={styles.box}>paintInside</Text>
          </Shadow>

          <Text style={styles.title}>sides</Text>
          <Shadow
            style={styles.shadow}
            sides={{start: false, end: true, top: false, bottom: false}}
            startColor={'#eb9066d8'}>
            <Text style={styles.box}>sides</Text>
          </Shadow>

          <Text style={styles.title}>corners</Text>
          <Shadow
            style={styles.shadow}
            distance={20}
            corners={{
              topStart: false,
              topEnd: false,
              bottomStart: true,
              bottomEnd: false,
            }}
            startColor={'red'}>
            <Text style={styles.box}>corners</Text>
          </Shadow>

          <Text style={styles.title}>style</Text>
          <Shadow style={{backgroundColor: 'red'}}>
            <Text style={styles.box}>style</Text>
          </Shadow>

          <Text style={styles.title}>containerStyle</Text>
          <Shadow containerStyle={{backgroundColor: 'red'}}>
            <Text style={styles.box}>containerStyle</Text>
          </Shadow>

          <Text style={styles.title}>stretch</Text>
          <Shadow stretch>
            <Text style={styles.box}>stretch</Text>
          </Shadow>

          <View style={{width: 200, height: 200}}>
            <Text style={styles.title}>safeRender</Text>
            <Shadow distance={10} safeRender={true}>
              <Text
                style={{width: '100%', height: '80%', backgroundColor: 'red'}}>
                shadow
              </Text>
            </Shadow>
          </View>

          <Text style={styles.title}>disabled</Text>
          <Shadow disabled>
            <Text style={styles.box}>disabled</Text>
          </Shadow>
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'column',
    justifyContent: 'center',
    alignItems: 'center',
  },
  sliders: {
    margin: 20,
    width: 280,
  },
  shadow: {
    marginBottom: 20,
  },
  text: {
    alignSelf: 'center',
    paddingVertical: 20,
  },
  title: {
    fontSize: 30,
    marginTop: 20,
  },
  box: {
    margin: 20,
    fontSize: 16,
  },
  sliderOne: {
    flexDirection: 'row',
    justifyContent: 'space-around',
  },
});

```

## Link

本库HarmonyOS侧实现依赖 react-native-svg 的原生端代码，如已在HarmonyOS工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-svg 文档](/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25 (API Version 12 Canary4); IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| startColor | 阴影的起始渐变色。 | string | no | All | yes |
| endColor | 阴影的结束渐变色。 | string | no | All | yes |
| distance | 阴影的延伸距离。 | number | no | All | yes |
| offset | 移动阴影。负x值使其向左/起点移动，负y值使其向上移动。接受 'x%' 格式的百分比值。设置此属性会将 `paintInside` 的默认值设为 true，因为这通常是期望的行为。 | [x: string \| number, y: string \| number] | no | All | yes |
| paintInside | 将阴影应用于内容的下方/内部。`startColor` 将被用作无渐变的填充色。当使用 `offset` 属性或子组件包含透明区域时，此属性很有用。 | boolean | no | All | yes |
| sides | 指定将要绘制阴影的边。不包括角落。未定义的边将默认设为 true。 | Record<'start' \| 'end' \| 'top' \| 'bottom', boolean> | no | All | yes |
| corners | 指定将要绘制阴影的角。未定义的角将默认设为 true。 | Record<'topStart' \| 'topEnd' \| 'bottomStart' \| 'bottomEnd', boolean> | no | Android | yes |
| style | 包裹子组件的视图（View）的样式。 | StyleProp<ViewStyle> | no | All | yes |
| containerStyle | 包裹阴影和子组件的视图的样式。对于设置外边距（margins）很有用。 | StyleProp<ViewStyle> | no | All | yes |
| stretch | 使子组件占据所有可用的水平空间。 | boolean | no | All | yes |
| safeRender | 在首次渲染时不使用相对尺寸和定位，而是在后续渲染中采用 `onLayout` 返回的精确尺寸。当处理半径大于边尺寸（如圆形）的场景时，此属性可用于避免首次渲染时出现视觉瑕疵。 | boolean | no | All | yes |
| disabled | 禁用阴影效果。当某些场景下不需要阴影时，此属性便于组件的复用。`containerStyle` 和 `style` 属性仍然会生效。 | boolean | no | All | yes |

## 遗留问题

目前可使用的属性，具体见上面已列出。

- [x] 由于react-native-shadow-2强依赖[`react-native-svg`](https://react-native-oh-library.gitee.io/usage-docs/#/zh-cn/react-native-svg)库，但react-native-svg目前仅实现少部分属性，其余还未实现HarmonyOS化， 导致属性offset、paintInside、corners不可用问题: [issue#5](https://github.com/react-native-oh-library/react-native-svg/issues/5)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/SrBrahma/react-native-shadow-2/blob/main/LICENSE) ，请自由地享受和参与开源。