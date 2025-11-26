> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-intersection-observer</code> </h1>
</p>

本项目基于 [react-native-intersection-observer@0.2.0](https://github.com/zhbhun/react-native-intersection-observer/tree/0.2.0) 开发。

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 | 
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.2.0  | [@react-native-oh-tpl/react-native-intersection-observer Releases](https://github.com/react-native-oh-library/react-native-intersection-observer/releases) | 0.72       |
| 0.3.0   | [@react-native-ohos/react-native-intersection-observer Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-intersection-observer/releases)     | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72 
npm install @react-native-oh-tpl/react-native-intersection-observer

# 0.77 
npm install @react-native-ohos/react-native-intersection-observer
```

#### **yarn**

```bash
# 0.72 
yarn add @react-native-oh-tpl/react-native-intersection-observer

# 0.77 
yarn add @react-native-ohos/react-native-intersection-observer
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useRef } from "react";
import { Text } from "react-native";
import {
  IOScrollView,
  IOScrollViewController,
  InView,
} from "react-native-intersection-observer";

function App() {
  const scrollViewRef = useRef<IOScrollViewController>(null);
  return (
    <IOScrollView ref={scrollViewRef}>
      <Text
        onPress={() => {
          scrollViewRef.current?.scrollToEnd();
        }}
      >
        Scroll to bottom
      </Text>
      <InView onChange={(inView: boolean) => console.log("Inview:", inView)}>
        <Text>
          Plain children are always rendered. Use onChange to monitor state.
        </Text>
      </InView>
    </IOScrollView>
  );
}

export default App;
```

## 约束与限制

#### 兼容性

本文档内容基于以下环境验证通过：

1. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请查看[react-native-intersection-observer](https://github.com/zhbhun/react-native-intersection-observer/blob/master/README.md)

#### **IOScrollView** **组件**

属性: 继承自 [ScrollView Props](https://reactnative.dev/docs/scrollview#props)

| Name       | Description   | Type                                                         | Required | HarmonyOS Support |
| ---------- | ------------- | ------------------------------------------------------------ | -------- | ----------------- |
| rootMargin | 根元素边距 | { top: number; left: number; right: number; bottom: number } | false    | yes               |

方法：继承自 [ScrollView Methods](https://reactnative.dev/docs/scrollview#methods)

#### **IOFlatList** **组件**

属性: 继承自 [FlatList Props](https://reactnative.dev/docs/flatlist#props)

| Name       | Description   | Type                                                         | Required | HarmonyOS Support |
| ---------- | ------------- | ------------------------------------------------------------ | -------- | ----------------- |
| rootMargin | 根元素边距 | { top: number; left: number; right: number; bottom: number } | false    | yes               |

方法：继承自 [FlatList Methods](https://reactnative.dev/docs/flatlist#methods)

#### **InView** **组件**

| Name        | Description                                                  | Type                        | Required | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | --------------------------- | -------- | ----------------- |
| as          | 指定组件渲染的包装元素类型。默认为 `View` | `ComponentType`             | false    | yes               |
| children    | 子元素期望一个普通子元素，由 `<InView />` 处理包装元素 | ReactNode                   | true     | yes               |
| triggerOnce | 仅触发此方法一次                               | boolean                     | false    | yes               |
| onChange    | 每当可视状态发生变化时调用此函数。它将接收 `inView` 布尔值，以及当前的`IntersectionObserverEntry` | `(inView: boolean) => void` | false    | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/zhbhun/react-native-intersection-observer/blob/master/LICENSE) ，请自由地享受和参与开源。
