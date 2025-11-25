> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-progress</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-progress">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-progress/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-progress)

| 三方库版本 |   包 名  |   仓库地址  | 发布信息 | 支持RN版本 |
| -------- | -------- | --------- |---------|----------|
| 5.0.1    | @react-native-oh-tpl/react-native-progress |[Github](https://github.com/react-native-oh-library/react-native-progress) | [Github Releases](https://github.com/react-native-oh-library/react-native-progress/releases) | 0.72       |
| 5.1.0    | @react-native-ohos/react-native-progress |[GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-progress) |[GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-progress/releases) | 0.77   |

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-progress Releases](https://github.com/react-native-oh-library/react-native-progress/releases)。



进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# V0.72
npm install @react-native-oh-tpl/react-native-progress

# V0.77
npm install @react-native-ohos/react-native-progress
```

#### **yarn**

```bash
# V0.72
yarn install @react-native-oh-tpl/react-native-progress

# V0.77
yarn install @react-native-ohos/react-native-progress
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useEffect } from "react";
import { StyleSheet, View, Text } from "react-native";
import * as Progress from "react-native-progress";

const ProgressExample = () => {
  const [progress, setProgress] = React.useState(0);
  const [indeterminate, setIndeterminate] = React.useState(true);

  useEffect(() => {
    let interval: ReturnType<typeof setInterval>;
    const timer = setTimeout(() => {
      setIndeterminate(false);
      interval = setInterval(() => {
        setProgress((prevProgress) => {
          if (prevProgress >= 1) {
            return 0;
          }
          return Math.min(1, prevProgress + Math.random() / 5);
        });
      }, 500);
    }, 1500);
    return () => {
      clearTimeout(timer);
      clearInterval(interval);
    };
  }, []);

  return (
    <View>
      <Text style={styles.welcome}>Progress Example</Text>
      <Progress.Bar
        style={styles.progress}
        progress={progress}
        indeterminate={indeterminate}
      />
      <View style={styles.circles}>
        <Progress.Circle
          style={styles.progress}
          progress={progress}
          indeterminate={indeterminate}
        />
        <Progress.Pie
          style={styles.progress}
          progress={progress}
          indeterminate={indeterminate}
        />
        <Progress.Circle
          style={styles.progress}
          progress={progress}
          indeterminate={indeterminate}
          direction="counter-clockwise"
        />
      </View>
      <View style={styles.circles}>
        <Progress.CircleSnail style={styles.progress} />
        <Progress.CircleSnail
          style={styles.progress}
          color={["#F44336", "#2196F3", "#009688"]}
        />
      </View>
    </View>
  );
};
export default ProgressExample;

const styles = StyleSheet.create({
  welcome: {
    fontSize: 20,
    textAlign: "center",
    margin: 10,
  },
  bar: {
    flexDirection: "row",
    justifyContent: "center",
  },
  circles: {
    flexDirection: "row",
    justifyContent: "center",
  },
  progress: {
    margin: 10,
  },
});
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-svg-capi](/zh-cn/react-native-svg-capi.md) 进行引入 

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-progress Releases](https://github.com/react-native-oh-library/react-native-progress/releases)

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-progress](https://github.com/oblador/react-native-progress?tab=readme-ov-file#properties-for-all-progress-components)

### 属性，用于所有进度组件:

| Name                           | Description                                                                  | Type    | Required | Platform | HarmonyOS Support |
| ------------------------------ | ---------------------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| animated                       | 是否为“进度”添加动画。                            | boolean | No       | All      | Yes               |
| indeterminate                  | 如果设置为true，则指示器将旋转并且“progress”将被忽略。 | boolean | No       | All      | Yes               |
| indeterminateAnimationDuration | 当设置indeterminate时，以毫秒为单位设置动画持续时间。          | number  | No       | All      | Yes               |
| progress                       | 指标所显示的进度。0和1之间的数字。  | number  | No       | All      | Yes               |
| color                          | 指示灯的填充颜色。                                                | string  | No       | All      | Yes               |
| unfilledColor                  | 剩余进度的颜色。                                            | string  | No       | All      | Yes               |
| borderWidth                    | 外边框的宽度，设置为“0”以移除。                                | number  | No       | All      | Yes               |
| borderColor                    | 外边框的颜色。                                                     | string  | No       | All      | Yes               |

### `Progress.Bar`:

All of the props under _Properties_ in addition to the following:

| Name            | Description                                                                    | Type                            | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------------ | ------------------------------- | -------- | -------- | ----------------- |
| width           | 进度条的全宽度，设置为‘ null ’以使用自动伸缩大小。 | number \| null                  | No       | All      | Yes               |
| height          | 进度条的高度。                                                 | number                          | No       | All      | Yes               |
| borderRadius    | 圆角，设置为‘ 0 ’禁用。                                   | number                          | No       | All      | Yes               |
| useNativeDriver | 动画使用原生驱动。                                       | boolean                         | No       | All      | Yes               |
| animationConfig | 传入‘ Animated ’函数的配置。                            | function                        | No       | All      | Yes               |
| animationType   | 动画类型：`decay`， `timing`, `spring`。   | 'decay' \| 'timing' \| 'spring' | No       | All      | Yes               |

### `Progress.Circle`:

All of the props under _Properties_ in addition to the following:

| Name             | Description                                                                                                                  | Type                               | Required | Platform | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- | -------- | -------- | ----------------- |
| size             | 圆的直径。                                                                                                  | number                             | No       | All      | Yes               |
| endAngle         | 确定圆的endAngle。一个介于0和1之间的数字。最终的角度将是数字乘以2π| number                             | No       | All      | Yes               |
| thickness        | 内圆的厚度。                                                                                            | number                             | No       | All      | Yes               |
| showsText        | 是否显示当前进度的文本表示。                                                           | boolean                            | No       | All      | Yes               |
| formatText       | 返回要显示文本表示的字符串的一个函数。                                               | function                           | No       | All      | Yes               |
| textStyle        | 进度文本的样式，默认与circle相同的`color`， `fontSize`与`size` prop成比例。                   | TextStyle                          | No       | All      | Yes               |
| allowFontScaling | 是否遵守设备字体比例设置                                                                      | boolean                            | No       | All      | Yes               |
| direction        | 圆的方向顺时针或逆时针。                                                                | 'clockwise' \| 'counter-clockwise' | No       | All      | Yes               |
| strokeCap        | 圆形的笔画样式为‘ butt ’， ‘ square ’或‘ round ’。                                                               | 'butt' \| 'square' \| 'round'      | No       | All      | Yes               |
| fill             | 填充内圆的颜色。                                                                                            | string                             | No       | All      | Yes               |

### `Progress.Pie`:

All of the props under _Properties_ in addition to the following:

| Name | Description          | Type   | Required | Platform | HarmonyOS Support |
| ---- | -------------------- | ------ | -------- | -------- | ----------------- |
| size | 饼图的直径。 | number | No       | All      | Yes               |

### `Progress.CircleSnail`:

| Name             | Description                                                                               | Type                               | Required | Platform | HarmonyOS Support |
| ---------------- | ----------------------------------------------------------------------------------------- | ---------------------------------- | -------- | -------- | ----------------- |
| animating        | 是否有圆形动画                                                           | boolean                            | No       | All      | Yes               |
| hidesWhenStopped | 是否需要在动画结束时移除圆。                                     | boolean                            | No       | All      | Yes               |
| size             | 圆的直径。                                                                 | number                             | No       | All      | Yes               |
| color            | 圆圈的颜色,使用一组颜色的彩虹效果。                           | string \| string[]                 | No       | All      | Yes               |
| thickness        | 圆的厚度。                                                                 | number                             | No       | All      | Yes               |
| duration         | 动画持续时间。                                                                   | number                             | No       | All      | Yes               |
| spinDuration     | 自旋(轨道)动画的持续时间。                                                    | number                             | No       | All      | Yes               |
| strokeCap        | 圆形的笔画样式为‘ butt ’， ‘ square ’或‘ round ’。                            | 'butt' \| 'square' \| 'round'      | No       | All      | Yes               |
| direction        | 圆旋转的方向，“顺时针”或“逆时针”（默认）。 | 'clockwise' \| 'counter-clockwise' | No       | All      | Yes               |

## 遗留问题

- [x] 已解决：1、Progress.Circle 中的属性 fill 在 HarmonyOS 上默认显示黑色和默认无色不一致，定位是 svg 的属性配置有问题，当前通过修改 Circle.js 中默认 fill 的属性进行规避，后续 svg 修复该问题[issue#6](https://github.com/react-native-oh-library/react-native-svg/issues/6)后，修改的代码会移除。

- [x] 已解决：2、Progress.Circle中的属性color, unfilledColor,borderWith,borderColor中圆的颜色，在进行静态配置的时候颜色显示正常，在使用Button进行动态改变的时候，中间的圆会显示黑色和默认的颜色不一致，定位是svg的属性配置有问题，当前通过修改Circle.js中默认fill的属性进行规避，后续 svg 修复该问题[issue#7](https://github.com/react-native-oh-library/react-native-svg/issues/7)后，修改的代码会移除。

- [x] 已解决：3、Progress.pie中的属性color,borderWith,borderColor中内圆的颜色，在进行静态配置的时候颜色显示正常，在使用Button进行动态改变的时候，中间的圆会显示黑色和默认的颜色不一致，定位是svg的属性有问题，pie传入给svg的值是正常的，svg处理逻辑有问题，修改svg修复该问题[issue#8](https://github.com/react-native-oh-library/react-native-svg/issues/8)

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/oblador/react-native-progress/blob/master/LICENSE) ，请自由地享受和参与开源。
