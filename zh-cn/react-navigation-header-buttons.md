> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-navigation-header-buttons</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vonovak/react-navigation-header-buttons">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vonovak/react-navigation-header-buttons/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/vonovak/react-navigation-header-buttons)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 12.0.0     | 0.72       |
| 13.0.0     | 0.77       |

<!-- tabs:start -->

<!-- tabs:start -->
进入到工程目录并输入以下命令：

#### **npm**

```bash
# V12.0.0
npm i react-navigation-header-buttons@12.0.0

# V13.0.0
npm i react-navigation-header-buttons@13.0.0
```

#### **yarn**

```bash
# V12.0.0
yarn add react-navigation-header-buttons@12.0.0

# V13.0.0
yarn add react-navigation-header-buttons@13.0.0
```


在tsconfig.json文件中添加如下代码:
```json
"compilerOptions": {
  ...
    "paths": {
    ...
      "react-navigation-header-buttons":[
        "./node_modules/react-navigation-header-buttons/lib/module/index.js"
      ]
    },
  }

```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import MaterialIcons from 'react-native-vector-icons/MaterialIcons';
import {
  HeaderButtons,
  Item,
  HiddenItem,
  OverflowMenu,
  Divider,
  ItemProps,
  HiddenItemProps,
  HeaderButtonProps,
  HeaderButton,
} from 'react-navigation-header-buttons/lib/module';
import { Text } from 'react-native';

const MaterialHeaderButton = (props: HeaderButtonProps) => (
  <HeaderButton IconComponent={MaterialIcons} iconSize={23} {...props} />
);

const EditItem = ({ onPress }: Pick<ItemProps, 'onPress'>) => {
  return <Item title="edit" onPress={onPress} />;
};

const ReusableHiddenItem = ({ onPress }: Pick<HiddenItemProps, 'onPress'>) => (
  <HiddenItem title="hidden2" onPress={onPress} disabled />
);

export function UsageWithIcons({ navigation }) {
  React.useLayoutEffect(() => {
    navigation.setOptions({
      title: 'Demo',
      headerRight: () => (
        <HeaderButtons HeaderButtonComponent={MaterialHeaderButton}>
          <Item
            title="search"
            iconName="search"
            onPress={() => alert('search')}
          />
          <EditItem onPress={() => alert('Edit')} />
          <OverflowMenu
            OverflowIcon={({ color }) => (
              <MaterialIcons name="more-horiz" size={23} color={color} />
            )}
          >
            <HiddenItem title="hidden1" onPress={() => alert('hidden1')} />
            <Divider />
            <ReusableHiddenItem onPress={() => alert('hidden2')} />
          </OverflowMenu>
        </HeaderButtons>
      ),
    });
  }, [navigation]);

  return <Text>demo!</Text>;
}
```

## Link

本库依赖以下三方库，请查看对应文档：

- [@react-navigation/native](/zh-cn/react-navigation-native.md)
- [@react-navigation/elements](/zh-cn/react-navigation-elements.md)
- [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

如已在鸿蒙工程中引入过该库，则无需再次引入，未引入请参照[@react-navigation/native 文档](/zh-cn/react-navigation-native.md)、[@react-navigation/elements 文档](/zh-cn/react-navigation-elements.md)、[@react-native-oh-library/react-native-safe-area-context 文档](/zh-cn/react-native-safe-area-context.md)进行引入 

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.26; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.300SP2; ROM:3.0.0.24(Canary3);
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

## 属性

### HeaderButtons

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `HeaderButtonComponent` | 渲染按钮的组件，默认为 HeaderButton | `ComponentType` | no | iOS/Android | yes |
| `children` | 你想要在内部渲染的任何内容 | `ReactNode` | yes | iOS/Android | yes |
| `left` | 是否添加边距距离 | boolean | no | iOS/Android | yes |
| `preset` | 标题通常在 Stack Navigator 中渲染，但你也可以在 Tab Navigator 标题中渲染它们。如果缺少按钮边距，请传递 'tabHeader'。 | `’tabHeader’/‘stackHeader’` | no | iOS/Android | yes |

### Item

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `title` | 按钮的标题，必填 | string | no | iOS/Android | yes |
| `onPress` | 按下时调用的函数 | function | no | iOS/Android | yes |
| `iconName` | 图标名称，与 IconComponent 属性一起使用 | string | no | iOS/Android | yes |
| `style` | 应用于包裹按钮的可触摸元素的样式 | `ViewStyle` | no | iOS/Android | yes |
| `buttonStyle` | 应用于文本/图标的样式 | `ViewStyle` | no | iOS/Android | yes |

### OverflowMenu

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `OverflowIcon` | 溢出图标的 React 元素或组件 | `ReactElement / ComponentType` | no | iOS/Android | yes |
| `style` | 溢出按钮的可选样式 | `ViewStyle` | no | iOS/Android | yes |
| `onPress` | 当按下溢出菜单时调用的函数。 | function | no | iOS/Android | yes |
| `left` | 是否添加边距距离 | boolean | no | iOS/Android | yes |
| `children` | 溢出项 | `ReactNode` | yes | iOS/Android | yes |
| `preset` | 标题通常在 Stack Navigator 中渲染，但你也可以在 Tab Navigator 标题中渲染它们。如果缺少按钮边距，请传递 'tabHeader'。 | ` 'tabHeader' / 'stackHeader'` | no | iOS/Android | yes |

### HiddenItem

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `title` | 按钮的标题，必填 | string | no | iOS/Android | yes |
| `style` | 应用于包裹文本的可触摸元素的样式 | `ViewStyle` | no | iOS/Android | yes |
| `titleStyle` | 应用于文本的样式 | `TextStyle` | no | iOS/Android | yes |
| `onPress` | 按下时调用的函数 | function | no | iOS/Android | yes |
| `disabled` | 禁用的“项目”会变灰，且触摸时不会调用 onPress | boolean | no | iOS/Android | yes |


### HeaderButton

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `title` | 按钮的标题，必填 | string | no | iOS/Android | yes |
| `style` | 应用于包裹文本的可触摸元素的样式 | `ViewStyle` | no | iOS/Android | yes |
| `onPress` | 按下时调用的函数 | function | no | iOS/Android | yes |
| `renderButton` | 你可以使用 renderButton 完全自定义 PlatformPressable 内部渲染的内容 | ReactNode | no | iOS/Android | yes |

## 遗留问题

## 其他

- left属性描述错误 [issue#248](https://github.com/vonovak/react-navigation-header-buttons/issues/248)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/vonovak/react-navigation-header-buttons/blob/master/LICENSE) ，请自由地享受和参与开源。