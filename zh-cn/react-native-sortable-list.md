> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sortable-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gitim/react-native-sortable-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/gitim/react-native-sortable-list/blob/master/LICENSE"/>
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-sortable-list)

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ---------- |
| 0.0.25 | @react-native-oh-tpl/react-native-sortable-list | [Github](https://github.com/react-native-oh-library/react-native-sortable-list) | [Github Releases](https://github.com/react-native-oh-library/react-native-sortable-list/releases) | 0.72 |
| 0.1.0                        | @react-native-ohos/react-native-sortable-list       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-sortable-list) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sortable-list/releases) | 0.77 |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
#v0.72
npm install @react-native-oh-tpl/react-native-sortable-list
#v0.77
npm install @react-native-ohos/react-native-sortable-list
```

#### **yarn**

```bash
#v0.72
yarn add @react-native-oh-tpl/react-native-sortable-list
#v0.77
yarn add @react-native-ohos/react-native-sortable-list
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 */

import React, {
  useCallback,
  useEffect,
  useMemo,
  useRef,
  useState,
} from "react";
import {
  Animated,
  Easing,
  StyleSheet,
  Text,
  Image,
  View,
  Dimensions,
  Platform,
  ScrollView,
  TextInput,
  Button,
} from "react-native";
import SortableList from "react-native-sortable-list";

const window = Dimensions.get("window");

const data = {
  0: {
    text: "Chloe （0）",
  },
  1: {
    text: "Jasper （1）",
  },
  2: {
    text: "Pepper （2）",
  },
  3: {
    text: "Oscar （3）",
  },
};

export default function SortDemo() {
  const renderRow = useCallback(({ data, active }) => {
    return <Row data={data} active={active} />;
  }, []);
  return (
    <View style={{ height: 600 }}>
      <SortableList style={styles.list} data={data} renderRow={renderRow} />
    </View>
  );
}

function Row(props) {
  const { active, data } = props;

  const activeAnim = useRef(new Animated.Value(0));
  const style = useMemo(
    () => ({
      ...Platform.select({
        ios: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          shadowRadius: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 10],
          }),
        },

        android: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          elevation: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 6],
          }),
        },
        harmony: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          elevation: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 6],
          }),
        },
      }),
    }),
    []
  );
  useEffect(() => {
    Animated.timing(activeAnim.current, {
      duration: 300,
      easing: Easing.bounce,
      toValue: Number(active),
      useNativeDriver: true,
    }).start();
  }, [active]);

  return (
    <Animated.View style={[styles.row, style]}>
      <Text style={styles.text}>{data.text}</Text>
    </Animated.View>
  );
}

const styles = StyleSheet.create({
  list: {
    flex: 1,
    backgroundColor: "#AAE",
  },
  contentContainer: {
    width: window.width - 100,
    ...Platform.select({
      ios: {
        paddingHorizontal: 30,
      },
      android: {
        paddingHorizontal: 0,
      },
      harmony: {
        paddingHorizontal: 0,
      },
    }),
  },
  row: {
    flexDirection: "row",
    alignItems: "center",
    backgroundColor: "#fff",
    padding: 16,
    height: 80,
    flex: 1,
    marginTop: 10,
    ...Platform.select({
      ios: {
        width: window.width - 60 * 2,
        shadowColor: "rgba(0,0,0,0.2)",
        shadowOpacity: 1,
        shadowOffset: { height: 2, width: 2 },
        shadowRadius: 2,
      },
      android: {
        width: window.width - 60 * 2,
        elevation: 0,
        marginHorizontal: 30,
      },
      harmony: {
        width: window.width - 60 * 2,
        elevation: 0,
        marginHorizontal: 30,
        shadowColor: "rgba(0,0,0,0.2)",
        shadowOpacity: 1,
        shadowOffset: { height: 2, width: 2 },
        shadowRadius: 2,
      },
    }),
  },
  text: {
    fontSize: 18,
    color: "#222222",
  },
});
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); DevEco Studio  6.0.0.868; ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| 属性名 | 描述 | **类型** | 是否必填 | 支持平台 | HarmonyOS 支持 |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | -------- | -------- | ----------------- |
| data                           | 数据源对象                                                                                                                                                                    | Object        | 是       | 全平台      | 是               |
| order                          | data 中键值数组，该数组顺序将用于初始化行顺序                                                                                                                                | Array         | 否       | 全平台      | 是               |
| style                          | 外层 View 的样式                                                                                                                                                              | Object, Array | 否       | 全平台      | 是               |
| contentContainerStyle          | 应用于内部 ScrollView 内容容器的样式                                                                                                                                          | Object, Array | 否       | 全平台      | 是               |
| innerContainerStyle            | 应用于内部 ScrollView 内容容器（不含头尾组件）的样式                                                                                                                         | Object, Array | 否       | 全平台      | 是               |
| horizontal                     | 为 true 时按行横向排列子组件，默认为 false 纵向排列                                                                                                                          | boolean       | 否       | 全平台      | 是               |
| showsVerticalScrollIndicator   | 为 false 时隐藏纵向滚动条，默认 true                                                                                                                                        | boolean       | 否       | 全平台      | 是               |
| showsHorizontalScrollIndicator | 为 false 时隐藏横向滚动条，默认 true                                                                                                                                          | boolean       | 否       | 全平台      | 是               |
| sortingEnabled                 | 为 false 时禁用排序功能，默认 true                                                                                                                                            | boolean       | 否       | 全平台      | 是               |
| scrollEnabled                  | 为 false 时禁用滚动，默认 true                                                                                                                                               | boolean       | 否       | 全平台      | 是               |
| keyboardShouldPersistTaps      | 控制点击后键盘是否保持可见，默认值为 'never'                                                                                                                                  | string        | 否       | 全平台      | 是               |
| manuallyActivateRows           | 是否通过 toggleRowActive 手动激活行而非内置方案                                                                                                                              | bool          | 否       | 全平台      | 是               |
| autoscrollAreaSize             | 触发自动滚动的顶部/底部（或左右）区域尺寸，垂直列表为高度，水平列表为宽度，默认 60                                                                                           | number        | 否       | 全平台      | 是               |
| rowActivationTime              | 行被长按后变为激活状态的延迟时间（毫秒），默认 200                                                                                                                            | number        | 否       | 全平台      | 是               |
| refreshControl                 | 与 ScrollView refreshControl 相同用法的下拉刷新组件                                                                                                                          | element       | 否       | 全平台      | 是               |
| renderRow                      | 接收行 key、索引、数据和状态（禁用/激活），返回一行要渲染的组件                                                                                                              | function      | 是       | 全平台      | 是               |
| renderHeader                   | 渲染列表顶部头部组件                                                                                                                                                          | function      | 否       | 全平台      | 是               |
| renderFooter                   | 渲染列表底部尾部组件                                                                                                                                                          | function      | 否       | 全平台      | 是               |
| onChangeOrder                  | 行重新排序后回调，返回新的行 key 顺序数组                                                                                                                                     | bool          | 否       | 全平台      | 是               |
| onActivateRow                  | 某一行被激活（长按）时触发                                                                                                                                                   | function      | 否       | 全平台      | 是               |
| onReleaseRow                   | 激活行释放时触发，返回该行 key 以及新的顺序                                                                                                                                    | function      | 否       | 全平台      | 是               |
| onPressRow                     | 某一行被点击时触发                                                                                                                                                           | function      | 否       | 全平台      | 是               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| 属性名 | 描述 | **类型** | 是否必填 | 支持平台 | HarmonyOS 支持 |
| -------------- | --------------------------------------------------------------------------- | -------------- | -------- | -------- | ----------------- |
| scrollBy       | 按给定纵向偏移滚动，可立即执行或平滑动画执行 | dy?, animated? | 否       | 全平台      | 是               |
| scrollTo       | 滚动到指定纵向偏移，可立即执行或平滑动画执行 | y?, animated?  | 否       | 全平台      | 是               |
| scrollToRowKey | 滚动到指定行 key，可立即执行或平滑动画执行 | key, animated? | 否       | 全平台      | 是               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/react-native-oh-library/react-native-sortable-list/blob/sig/LICENSE) ，请自由地享受和参与开源。
