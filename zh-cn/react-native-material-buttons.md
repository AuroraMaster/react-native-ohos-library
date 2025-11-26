> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-material-buttons</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/n4kz/react-native-material-buttons">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/n4kz/react-native-material-buttons/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-material-buttons)

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 0.6.0 | @react-native-oh-tpl/react-native-material-buttons | [Github](https://github.com/react-native-oh-library/react-native-material-buttons) | [Github Releases](https://github.com/react-native-oh-library/react-native-material-buttons/releases) | 0.72 |
| 0.7.0                        | @react-native-ohos/react-native-material-buttons       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-material-buttons) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-material-buttons/releases) | 0.77 |


## 安装与使用


对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
#v0.72
npm install @react-native-oh-tpl/react-native-material-buttons
npm install deprecated-react-native-prop-types
#v0.77
npm install @react-native-ohos/react-native-material-buttons
npm install deprecated-react-native-prop-types
```

#### **yarn**

```bash
#v0.72
yarn add @react-native-oh-tpl/react-native-material-buttons
yarn add deprecated-react-native-prop-types
#v0.77
yarn add @react-native-ohos/react-native-material-buttons
yarn add deprecated-react-native-prop-types
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import React, { Component } from 'react';
import { AppRegistry, Text, ScrollView, View, SafeAreaView } from 'react-native';
import { TextButton, RaisedTextButton } from 'react-native-material-buttons';

interface Styles {
  scroll: object;
  container: object;
  safeContainer: object;
  column: object;
  row: object;
  card: object;
  button: object;
  display: object;
  text: object;
  content: object;
  bold: object;
}

let styles: Styles = {
  scroll: {
    padding: 4,
    paddingTop: 24,
    backgroundColor: '#E8EAF6',
  },
  container: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    marginBottom: 8,
    backgroundColor: 'rgba(0,0,0,.05)',
  },
  safeContainer: {
    flex: 1,
    backgroundColor: '#E8EAF6',
  },
  column: {
    justifyContent: 'center',
    marginBottom: 8,
    backgroundColor: 'rgba(0,0,0,.05)',
  },
  row: {
    marginBottom: 8,
  },
  card: {
    borderRadius: 2,
    padding: 8,
    margin: 4,
    backgroundColor: 'rgba(255, 255, 255, 1)',
    minHeight: 76,
    justifyContent: 'space-between',
    shadowOpacity: 0.54,
    shadowRadius: 1,
    shadowOffset: { width: 0, height: 1 },
    elevation: 1,
  },
  button: {
    margin: 4,
  },
  display: {
    paddingHorizontal: 8,
    fontSize: 17,
    fontWeight: '500',
    color: 'rgba(0, 0, 0, .87)',
  },
  text: {
    padding: 8,
    fontSize: 15,
    color: 'rgba(0, 0, 0, .54)',
  },
  content: {
    flex: 1,
    paddingVertical: 16,
  },
  bold: {
    fontWeight: 'bold',
  },
};

/* eslint-disable react/prop-types */
let Strong: React.FC<{ children: React.ReactNode }> = ({ children, ...props }) => (
  <Text style={styles.bold} {...props}>
    {children}
  </Text>
);
/* eslint-enable */

const  MaterialButtons = () => {
      return (
        <SafeAreaView style={styles.safeContainer}>
          <ScrollView style={styles.scroll}>
            <View style={styles.card}>
              <View style={styles.content}>
                <Text style={styles.display}>default</Text>
                <Text style={styles.text}>
                  Buttons with default props, raised or flat, enabled or <Strong>disabled</Strong>
                </Text>
              </View>
              <RaisedTextButton style={{ marginVertical: 4 }} title="default button" />
              <RaisedTextButton style={{ marginVertical: 4 }} titleStyle={{ fontWeight: 'bold' }} title="disabled button" disabled />
              <TextButton style={{ marginVertical: 4 }} title="default flat button" />
              <TextButton style={{ marginVertical: 4 }}  disabledTitleColor="red" title="disabled flat button" disabled />
            </View>

            <View style={styles.card}>
              <View style={styles.content}>
                <Text style={styles.display}>raised</Text>
                <Text style={styles.text}>
                  Buttons with custom <Strong>color</Strong>, <Strong>titleColor</Strong>, increased{' '}
                  <Strong>rippleDuration</Strong> and <Strong>rippleOpacity</Strong>
                </Text>
              </View>
              <View style={{ flexDirection: 'row', justifyContent: 'flex-end' }}>
                <RaisedTextButton
                  style={styles.button}
                  rippleDuration={600}
                  rippleOpacity={0.54}
                  title="flat"
                  color="#039BE5"
                  titleColor="white"
                />
                <RaisedTextButton
                  style={styles.button}
                  rippleDuration={1000}
                  rippleOpacity={0.64}
                  title="is"
                  color="#0288D1"
                  titleColor="white"
                />
                <RaisedTextButton
                  style={styles.button}
                  titleStyle={{ fontWeight: 'bold' }}
                  rippleDuration={1500}
                  rippleOpacity={0.74}
                  title="boring"
                  color="#0277BD"
                  titleColor="white"
                />
              </View>
            </View>

            <View style={styles.card}>
              <View style={styles.content}>
                <Text style={styles.display}>flat</Text>
                <Text style={styles.text}>Buttons with custom <Strong>titleColor</Strong> and <Strong>color</Strong></Text>
              </View>
              <View style={{ flexDirection: 'row', justifyContent: 'flex-start' }}>
                <TextButton style={{ margin: 4, marginLeft: 0 }} titleColor="black" title="decline" />
                <TextButton titleStyle={{ fontWeight: 'bold' }} titleColor="pink" title="accept" />
              </View>
            </View>
          </ScrollView>
        </SafeAreaView>
      );
}

export default MaterialButtons;


```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); DevEco Studio  6.0.0.868; ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

### 此组件有以下属性:
## **API（TextButton ）**
>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|          属性名           |                    描述                    |                           类型                           | 是否必填 |  支持平台   | HarmonyOS 支持 |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **titleStyle**      |               按钮标题的样式对象                  |                         Object                           |    否    | iOS/Android |        是        |
|        **title**        |                      按钮标题                     |                         String                           |    是    | iOS/Android |        是        |
|     **titleColor**      |                    按钮标题颜色                   |                         String                           |    否    | iOS/Android |        是        |
| **disabledTitleColor**  |                按钮禁用状态的标题颜色              |                         String                           |    否    | iOS/Android |        是        |

## **API（RaisedTextButton）**
>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|          属性名           |                    描述                    |                           类型                           | 是否必填 |  支持平台   | HarmonyOS 支持 |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|    **rippleOpacity**    |               水波纹效果的不透明度                |                         Number                           |    否    | iOS/Android |        是        |
|   **rippleDuration**    |              水波纹效果持续时间（毫秒）            |                         Number                           |    否    | iOS/Android |        是        |

## **API（Common）**
>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|          属性名           |                    描述                    |                           类型                           | 是否必填 |  支持平台   | HarmonyOS 支持 |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|    **color**    |                 按钮颜色                 |                         String                           |    否    | iOS/Android |        是        |
|   **disabledColor**    |             按钮禁用状态的颜色             |                         String                           |    否    | iOS/Android |        是        |
|   **shadeColor**    |             按钮聚焦状态的阴影颜色           |                         String                           |    否    | iOS/Android |        是        |
|   **shadeOpacity**    |           按钮聚焦状态阴影透明度            |                         Number                           |    否    | iOS/Android |        是        |
|   **shadeBorderRadius**    |               按钮阴影圆角                |                         Number                           |    否    | iOS/Android |        是        |
|   **focusAnimation**    |                 聚焦动画状态               |                         Animated.Value                           |    否    | iOS/Android |        是        |
|   **disableAnimation**    |               禁用状态动画状态               |                         Animated.Value                           |    否    | iOS/Android |        是        |
|   **focusAnimationDuration**    |         聚焦状态动画持续时间（毫秒）         |                         Number                           |    否    | iOS/Android |        是        |
|   **disableAnimationDuration**    |        禁用状态动画持续时间（毫秒）         |                         Number                           |    否    | iOS/Android |        是        |
|   **disabled**    |                  按钮可用性               |                         Boolean                           |    否    | iOS/Android |        是        |
|   **onPress**    |                  抬起回调                 |                         Function                           |    否    | iOS/Android |        是        |
|   **payload**    |            onPress 回调的负载对象           |                         Any                           |    否    | iOS/Android |        是        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/n4kz/react-native-material-buttons/blob/master/license.txt) ，请自由地享受和参与开源。 