> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-emoji-keyboard</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/TheWidlarzGroup/rn-emoji-keyboard">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/TheWidlarzGroup/rn-emoji-keyboard/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/rn-emoji-keyboard)

## 安装与使用
请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 1.7.0 | [@react-native-oh-tpl/rn-emoji-keyboard Releases](https://gitcode.com/openharmony-sig/rntpc_rn-emoji-keyboard/releases) | 0.72 |
| 1.8.0 | [@react-native-ohos/rn-emoji-keyboard Releases](https://gitcode.com/openharmony-sig/rntpc_rn-emoji-keyboard/releases) | 0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
//0.72
npm install @react-native-oh-tpl/rn-emoji-keyboard
//0.77
npm install @react-native-ohos/rn-emoji-keyboard
```

#### **yarn**

```bash
//0.72
yarn add @react-native-oh-tpl/rn-emoji-keyboard
//0.77
yarn add @react-native-ohos/rn-emoji-keyboard
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] 本示例依赖@react-native-async-storage/async-storage库，参照[@react-native-async-storage/async-storage文档](/zh-cn/react-native-async-storage-async-storage.md)进行引入
```ts
import React from "react";
import { StyleSheet, Button, Text } from "react-native";
import EmojiPicker, {
  emojisByCategory,
  type EmojiType,
  type EmojisByCategory,
  useRecentPicksPersistence,
} from "rn-emoji-keyboard";
import AsyncStorage from "@react-native-async-storage/async-storage";

type CurrentlySelected = {
  name: EmojiType["name"];
  emoji: EmojiType["emoji"];
};

export default function () {
  const [isOpen, setIsOpen] = React.useState<boolean>(false);
  const [currentlySelected, setCurrentlySelected] = React.useState<
    CurrentlySelected[]
  >([]);

  const STORAGE_KEY = "RN-EMOJI-KEYBOARD_RECENT";

  useRecentPicksPersistence({
    initialization: () =>
      AsyncStorage.getItem(STORAGE_KEY).then((value) =>
        JSON.parse(value || "[]")
      ),
    onStateChange: (next) =>
      AsyncStorage.setItem(STORAGE_KEY, JSON.stringify(next)),
  });

  const getCustomEmojis = () => {
    const newEmojiSet: EmojisByCategory[] = [];
    for (const [, value] of Object.entries(emojisByCategory)) {
      if (
        value.title === "smileys_emotion" &&
        !value.data.some((emoji) => emoji.name == "banana")
      ) {
        value.data.push({
          emoji: "🍌",
          name: "banana",
          v: "11",
          toneEnabled: false,
        });
      }

      newEmojiSet.push({
        title: value.title,
        data: value.data,
      });
    }

    return newEmojiSet;
  };
  const handlePick = (e: EmojiType) => {
    if (e.alreadySelected) {
      setCurrentlySelected((prev) =>
        prev.filter((item) => item.name !== e.name)
      );
    } else {
      setCurrentlySelected((prev) => [
        ...prev,
        { name: e.name, emoji: e.emoji },
      ]);
    }
  };
  const currSelectedEmojis = currentlySelected.map((item) => item.emoji);

  return (
    <>
      <Text style={styles.textIcon}>{currSelectedEmojis.join(" ")}</Text>
      <Button onPress={() => setIsOpen(true)} title="open emoji" />
      <EmojiPicker
        emojisByCategory={getCustomEmojis()}
        enableRecentlyUsed
        onEmojiSelected={handlePick}
        open={isOpen}
        onClose={() => setIsOpen(false)}
      />
    </>
  );
}

const styles = StyleSheet.create({
  textIcon: {
    marginHorizontal: 16,
    marginVertical: 32,
    textAlign: "center",
    fontSize: 42,
    color: "#000",
  },
});
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性
详细请查看 [rn-emoji-keyboard 的文档介绍](https://github.com/TheWidlarzGroup/rn-emoji-keyboard)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

你说得对，我需要保持完整格式。让我重新翻译描述列的内容：

| Name                            | Description                                                                                                                                                                                                                                            | Type                                                                     | Required | Platform    | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------ | -------- | ----------- | ----------------- |
| `open`                          | 必需属性，指示模态框是否应在屏幕上显示（默认：false）                                                                                                                                                                                                 | boolean                                                                  | yes      | iOS/Android | yes               |
| `onClose`                       | 组件关闭时触发的回调函数（默认：undefined）                                                                                                                                                                                                          | () => void                                                               | yes      | iOS/Android | yes               |
| `onEmojiSelected`               | 选择表情时触发的回调函数。传递的函数会接收包含所选表情数据的对象，并返回 alreadySelected 布尔值，指示按下的表情是否已被选择（参见 selectedEmojis）（默认：undefined）                                                                                   | (emoji: { emoji, name, slug, unicode_version, alreadySelected }) => void | yes      | iOS/Android | yes               |
| `allowMultipleSelections`       | 允许在不关闭键盘的情况下选择多个表情（默认：false）                                                                                                                                                                                                   | boolean                                                                  | no       | iOS/Android | yes               |
| `categoryPosition`              | 允许更改可用表情分类容器的位置（默认：floating）                                                                                                                                                                                                      | floating \| top \| bottom                                                | no       | iOS/Android | yes               |
| `categoryOrder`                 | 允许更改可用表情分类容器的顺序（默认：[]）                                                                                                                                                                                                            | CategoryTypes[]                                                          | no       | iOS/Android | yes               |
| `defaultHeight`                 | 指定折叠状态容器高度。可以是点数（points）或屏幕百分比字符串（默认：40%）                                                                                                                                                                             | number \| string                                                         | no       | iOS/Android | yes               |
| `disabledCategories`            | 允许通过传递分类slug数组来隐藏特定分类（默认：[]）                                                                                                                                                                                                    | CategoryTypes[]                                                          | no       | iOS/Android | yes               |
| `disableSafeArea`               | 允许禁用表情键盘内的安全区域视图（默认：false）                                                                                                                                                                                                       | Boolean                                                                  | no       | iOS/Android | yes               |
| `emojisByCategory`              | 可在应用中显示的表情集合。可以传递自定义表情集或使用我们已准备好的集合（默认：emojisByCategory）                                                                                                                                                     | EmojisByCategory[]                                                       | no       | iOS/Android | yes               |
| `emojiSize`                     | 设置单个表情的大小（默认：28）                                                                                                                                                                                                                        | number                                                                   | no       | iOS/Android | yes               |
| `enableRecentlyUsed`            | 显示包含最近使用表情的额外分类（默认：false）                                                                                                                                                                                                         | boolean                                                                  | no       | iOS/Android | yes               |
| `enableSearchBar`               | 显示搜索栏，用于查找特定表情（默认：false）                                                                                                                                                                                                           | boolean                                                                  | no       | iOS/Android | yes               |
| `hideSearchBarClearIcon`        | 隐藏搜索输入框内的清除图标（默认：false）                                                                                                                                                                                                             | boolean                                                                  | no       | iOS/Android | yes               |
| `customButtons`                 | 向组件注入自定义按钮（默认：null）                                                                                                                                                                                                                    | React.ReactNode                                                          | no       | iOS/Android | yes               |
| `enableCategoryChangeAnimation` | 允许在分类更改时关闭FlatList滚动动画。设置为false也会覆盖enableSearchAnimation值（默认：true）                                                                                                                                                        | boolean                                                                  | no       | iOS/Android | yes               |
| `enableCategoryChangeGesture`   | 允许使用水平滑动手势更改表情分类（默认：true）                                                                                                                                                                                                        | boolean                                                                  | no       | iOS/Android | yes               |
| `enableSearchAnimation`         | 允许在搜索结果更新时关闭FlatList滚动动画（默认：true）                                                                                                                                                                                                | boolean                                                                  | no       | iOS/Android | yes               |
| `expandable`                    | 显示拖动柄并启用向上滑动展开功能（默认：true）                                                                                                                                                                                                        | boolean                                                                  | no       | iOS/Android | yes               |
| `expandedHeight`                | 指定展开状态容器高度。可以是点数（points）或屏幕百分比字符串。仅当expandable属性设置为true时生效（默认：80%）                                                                                                                                         | number \| string                                                         | no       | iOS/Android | yes               |
| `hideHeader`                    | 隐藏包含分类名称的标签（默认：false）                                                                                                                                                                                                                 | boolean                                                                  | no       | iOS/Android | yes               |
| `theme`                         | 包含每个组件样式的属性名称（默认：defaultTheme）                                                                                                                                                                                                      | Record<string, string \| object>                                         | no       | iOS/Android | yes               |
| `styles`                        | 包含每个组件样式的属性名称（默认：{}）                                                                                                                                                                                                                | Record<string, ViewStyle>                                                | no       | iOS/Android | yes               |
| `onCategoryChangeFailed`        | 分类更改失败时触发的回调函数（默认：warn(info)）                                                                                                                                                                                                      | ( info: {index, highestMeasuredFrameIndex, averageItemLength} ) => void  | no       | iOS/Android | yes               |
| `onRequestClose`                | 表情键盘关闭时触发的回调函数（默认：undefined）                                                                                                                                                                                                       | () => void                                                               | no       | iOS/Android | yes               |
| `selectedEmojis`                | 当前已选表情的数组。必须包含表情的name属性（默认：undefined）                                                                                                                                                                                         | emoji.name[]                                                             | no       | iOS/Android | yes               |

### Full list of theme properties

| Name                       | Description                                                                                   | Type   | Required | Platform    | HarmonyOS Support |
| -------------------------- | --------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| `backdrop`                 | 设置模态框背景的背景色（默认：#00000055）                                                     | string | no       | iOS/Android | yes               |
| `knob`                     | 设置模态框拖动柄的背景色（默认：#ffffff）                                                     | string | no       | iOS/Android | yes               |
| `container`                | 设置整个模态框容器的背景色（默认：#ffffff）                                                   | string | no       | iOS/Android | yes               |
| `header`                   | 设置分类名称文本颜色（默认：#00000099）                                                       | string | no       | iOS/Android | yes               |
| `skinTonesContainer`       | 设置肤色选择容器的背景色（默认：#e3dbcd）                                                     | string | no       | iOS/Android | yes               |
| `category.icon`            | 分类图标的颜色（默认：#000000）                                                               | string | no       | iOS/Android | yes               |
| `category.iconActive`      | 活动分类图标的颜色（默认：#005b96）                                                           | string | no       | iOS/Android | yes               |
| `category.container`       | 分类容器的背景色（默认：#e3dbcd）                                                             | string | no       | iOS/Android | yes               |
| `category.containerActive` | 当前活动分类的背景色（默认：#ffffff）                                                         | string | no       | iOS/Android | yes               |
| `search.text`              | 搜索栏文本颜色（默认：#000000cc）                                                             | string | no       | iOS/Android | yes               |
| `search.placeholder`       | 搜索栏占位符文本颜色（默认：#00000055）                                                       | string | no       | iOS/Android | yes               |
| `search.icon`              | 搜索栏图标颜色（默认：#00000055）                                                             | string | no       | iOS/Android | yes               |
| `search.background`        | 搜索栏背景色（默认：#00000011）                                                               | string | no       | iOS/Android | yes               |
| `emoji.selected`           | 已选表情的背景颜色。仅在使用selectedEmojis属性时生效（默认：#e3dbcd）                          | string | no       | iOS/Android | yes               |

### Full list of theme properties

| Name                       | Description                                                                                   | Type   | Required | Platform    | HarmonyOS Support |
| -------------------------- | --------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| `backdrop`                 | 设置模态框背景的背景色（默认：#00000055）                                                     | string | no       | iOS/Android | yes               |
| `knob`                     | 设置模态框拖动柄的背景色（默认：#ffffff）                                                     | string | no       | iOS/Android | yes               |
| `container`                | 设置整个模态框容器的背景色（默认：#ffffff）                                                   | string | no       | iOS/Android | yes               |
| `header`                   | 设置分类名称文本颜色（默认：#00000099）                                                       | string | no       | iOS/Android | yes               |
| `skinTonesContainer`       | 设置肤色选择容器的背景色（默认：#e3dbcd）                                                     | string | no       | iOS/Android | yes               |
| `category.icon`            | 分类图标的颜色（默认：#000000）                                                               | string | no       | iOS/Android | yes               |
| `category.iconActive`      | 活动分类图标的颜色（默认：#005b96）                                                           | string | no       | iOS/Android | yes               |
| `category.container`       | 分类容器的背景色（默认：#e3dbcd）                                                             | string | no       | iOS/Android | yes               |
| `category.containerActive` | 当前活动分类的背景色（默认：#ffffff）                                                         | string | no       | iOS/Android | yes               |
| `search.text`              | 搜索栏文本颜色（默认：#000000cc）                                                             | string | no       | iOS/Android | yes               |
| `search.placeholder`       | 搜索栏占位符文本颜色（默认：#00000055）                                                       | string | no       | iOS/Android | yes               |
| `search.icon`              | 搜索栏图标颜色（默认：#00000055）                                                             | string | no       | iOS/Android | yes               |
| `search.background`        | 搜索栏背景色（默认：#00000011）                                                               | string | no       | iOS/Android | yes               |
| `emoji.selected`           | 已选表情的背景颜色。仅在使用selectedEmojis属性时生效（默认：#e3dbcd）                          | string | no       | iOS/Android | yes               |

### Full list of styles properties

| Name        | Description                                                                                                                               | Type                                      | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- | -------- | ----------- | ----------------- |
| `container` | 设置整个模态框容器的样式（默认：{}）                                                                                                       | ViewStyle                                 | no       | iOS/Android | yes               |
| `header`    | 设置标题文本的样式。标题是包含分类名称的组件（默认：{}）                                                                                   | TextStyle                                 | no       | iOS/Android | yes               |
| `knob`      | 设置模态框拖动柄的样式。仅在使用启用拖动柄的模态模式时生效（默认：{}）                                                                     | ViewStyle                                 | no       | iOS/Android | yes               |
| `category`  | 设置分类组件的样式。可以为容器和图标传递不同的样式（默认：{ container: {}, icon: {} }）                                                   | { container: ViewStyle, icon: TextStyle } | no       | iOS/Android | yes               |
| `searchBar` | 设置搜索栏组件的样式。可以为容器和文本传递不同的样式（默认：{ container: {}, text: {} }）                                                 | { container: ViewStyle, text: TextStyle } | no       | iOS/Android | yes               |
| `emoji`     | 设置表情组件的样式。可以为选中状态传递样式（默认：{ selected: {} }）                                                                       | { selected: ViewStyle }                   | no       | iOS/Android | yes               |

### Full list of EmojisByCategory type

| Name  | Description | Type          | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------------- | -------- | ----------- | ----------------- |
| title | EmojisByCategory 标题       | CategoryTypes | yes      | iOS/Android | yes               |
| data  | EmojisByCategory 表情数据        | JsonEmoji[]   | yes      | iOS/Android | yes               |

### Full list of CategoryTypes type

| Name  | Description | Type          | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------------- | -------- | ----------- | ----------------- |
| `CategoryTypes` | CategoryTypes 类型 | "search" \| "smileys_emotion" \| "people_body" \| "animals_nature" \| "food_drink" \| "travel_places" \| "activities" \| "objects" \| "symbols" \| "flags" \| "recently_used" | no       | iOS/Android | yes               |

### Full list of JsonEmoji type

| Name        | Description | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ----------- | -------- | -------- | ----------- | ----------------- |
| emoji       | JsonEmoji 表情      | string   | yes      | iOS/Android | yes               |
| name        | JsonEmoji 名称    | string   | yes      | iOS/Android | yes               |
| v           | JsonEmoji 版本     | string   | yes      | iOS/Android | yes               |
| toneEnabled | JsonEmoji 启用色调     | boolean  | yes      | iOS/Android | yes               |
| keywords    | JsonEmoji 关键词       | string[] | no      | iOS/Android | yes               |

### Full list of EmojiType type

| Name        | Description | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ----------- | -------- | -------- | ----------- | ----------------- |
| emoji       | EmojiType 表情      | string   | yes      | iOS/Android | yes               |
| name        | EmojiType 名称    | string   | yes      | iOS/Android | yes               |
| slug           | EmojiType 标识符     | string   | yes      | iOS/Android | yes               |
| unicode_version | EmojiType 版本     | string  | yes      | iOS/Android | yes               |
| toneEnabled    | EmojiType 启用色调       | boolean | yes      | iOS/Android | yes               |
| alreadySelected    | EmojiType 已选择状态     | boolean | no      | iOS/Android | yes               |

## 静态方法

### useRecentPicksPersistence

该库提供了通过自定义方式持久化最近使用表情的可能性。这意味着您可以使用任何您想要的方式来实现此功能。

异步存储？——当然可以。后端作为存储？——没问题。选择您想要的处理方式，我们只需要一个Promise

> [!TIP] This functionality requires to enable enableRecentlyUsed in your emoji keyboard component

> [!TIP] This hook will have impact on every rn-emoji-keyboard instance used in app that have enabled recent picks.

> [!TIP] To ensure smooth experience we recommend that you use it as high as possible in the React structure. eg. App.tsx file

| Name             | Description                                                                                                | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `initialization` | 此属性在初始阶段用于恢复之前的状态                                                                         | Function | yes      | iOS/Android | yes               |
| `onStateChange`  | 当用户选择表情且键盘启用了 enableRecentlyUsed 属性时，每次都会使用此属性                                   | Function | yes      | iOS/Android | yes               |

## 遗留问题

- [x] rn-emoji-keyboard 的键盘弹出后回弹默认高度表情键盘无法点击: [issue#1](https://github.com/react-native-oh-library/rn-emoji-keyboard/issues/1)
- [ ] rn-emoji-keyboard 展开旋钮动画卡顿: [issue#2](https://github.com/react-native-oh-library/rn-emoji-keyboard/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/TheWidlarzGroup/rn-emoji-keyboard/blob/master/LICENSE) ，请自由地享受和参与开源。
