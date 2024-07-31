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

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/rn-emoji-keyboard Releases](https://github.com/react-native-oh-library/rn-emoji-keyboard/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/rn-emoji-keyboard@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/rn-emoji-keyboard@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/async-storage 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/async-storage 文档](/zh-cn/react-native-async-storage-async-storage.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/rn-emoji-keyboard Releases](https://github.com/react-native-oh-library/rn-emoji-keyboard/releases)

## 属性
详细请查看 [rn-emoji-keyboard 的文档介绍](https://github.com/TheWidlarzGroup/rn-emoji-keyboard)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                            | Description                                                                                                                                                                                                                                            | Type                                                                     | Required | Platform    | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------ | -------- | ----------- | ----------------- |
| `open`                          | Required props which indicates whether the modal should be displayed on the screen.(dafault:false)                                                                                                                                                     | boolean                                                                  | yes      | iOS/Android | yes               |
| `onClose`                       | Callback fired when the component is to be closed.(dafault:undefined)                                                                                                                                                                                  | () => void                                                               | yes      | iOS/Android | yes               |
| `onEmojiSelected`               | Callback fired when the emoji is selected. The passed function expose an object with selected emoji data. It also returns alreadySelected boolean indicating whether pressed emoji is already selected or not (see selectedEmojis).(dafault:undefined) | (emoji: { emoji, name, slug, unicode_version, alreadySelected }) => void | yes      | iOS/Android | yes               |
| `allowMultipleSelections`       | Allow select multiple emoji without dismiss keyboard.(default:false)                                                                                                                                                                                   | boolean                                                                  | no       | iOS/Android | yes               |
| `categoryPosition`              | Allow to change the position of available emoji categories container.(default:floating)                                                                                                                                                                | floating \| top \| bottom                                                | no       | iOS/Android | yes               |
| `categoryOrder`                 | Allow to change order of available emoji categories container.(default:[])                                                                                                                                                                             | CategoryTypes[]                                                          | no       | iOS/Android | yes               |
| `defaultHeight`                 | Specify collapsed container height. It can be either a number in points or a string in a percentage of the screen.(default:40%)                                                                                                                        | number \| string                                                         | no       | iOS/Android | yes               |
| `disabledCategories`            | Allow to hide specific categories by passing an array with their slugs.(default:[])                                                                                                                                                                    | CategoryTypes[]                                                          | no       | iOS/Android | yes               |
| `disableSafeArea`               | Allow to disable SafeAreaView inside the emoji keyboard.(default:false)                                                                                                                                                                                | Boolean                                                                  | no       | iOS/Android | yes               |
| `emojisByCategory`              | Set of emojis that can be displayed in the app. You can pass your own emojis set or use the one that we have prepared.(default:emojisByCategory)                                                                                                       | EmojisByCategory[]                                                       | no       | iOS/Android | yes               |
| `emojiSize`                     | Set size of the single emoji.(default:28)                                                                                                                                                                                                              | number                                                                   | no       | iOS/Android | yes               |
| `enableRecentlyUsed`            | Reveal extra category with recently used emojis.(default:false)                                                                                                                                                                                        | boolean                                                                  | no       | iOS/Android | yes               |
| `enableSearchBar`               | Reveal the search bar, used to find specific emoji.(default:false)                                                                                                                                                                                     | boolean                                                                  | no       | iOS/Android | yes               |
| `hideSearchBarClearIcon`        | Hide the search bar clear icon inside the search input.(default:false)                                                                                                                                                                                 | boolean                                                                  | no       | iOS/Android | yes               |
| `customButtons`                 | Inject custom buttons into the component.(default:null)                                                                                                                                                                                                | React.ReactNode                                                          | no       | iOS/Android | yes               |
| `enableCategoryChangeAnimation` | Allow to turn off FlatList scrolling animation when category is changed. Setting this to false will also overwrite enableSearchAnimation value.(default:true)                                                                                          | boolean                                                                  | no       | iOS/Android | yes               |
| `enableCategoryChangeGesture`   | Allow to use horizontal swipe gesture to change emoji category.(default:true)                                                                                                                                                                          | boolean                                                                  | no       | iOS/Android | yes               |
| `enableSearchAnimation`         | Allow to turn off FlatList scrolling animation when search results are updated.(default:true)                                                                                                                                                          | boolean                                                                  | no       | iOS/Android | yes               |
| `expandable`                    | Show knob and enable expand on swipe up.(default:true)                                                                                                                                                                                                 | boolean                                                                  | no       | iOS/Android | yes               |
| `expandedHeight`                | Specify expanded container height. It can be either a number in points or a string in a percentage of the screen.expandedHeight works only if expandable props is set to true.(default:80%)                                                            | number \| string                                                         | no       | iOS/Android | yes               |
| `hideHeader`                    | Hide labels with category names.(default:false)                                                                                                                                                                                                        | boolean                                                                  | no       | iOS/Android | yes               |
| `theme`                         | This is the name of property that has every component styles inside.(default:defaultTheme)                                                                                                                                                             | Record<string, string \| object>                                         | no       | iOS/Android | yes               |
| `styles`                        | This is the name of property that has every component styles inside.(default:{})                                                                                                                                                                       | Record<string, ViewStyle>                                                | no       | iOS/Android | yes               |
| `onCategoryChangeFailed`        | Callback fired when the category change failed.(default:warn(info))                                                                                                                                                                                    | ( info: {index, highestMeasuredFrameIndex, averageItemLength} ) => void  | no       | iOS/Android | yes               |
| `onRequestClose`                | Callback fired when emoji keyboard is closing.(default:undefined)                                                                                                                                                                                      | () => void                                                               | no       | iOS/Android | yes               |
| `selectedEmojis`                | Array of currently selected emojis. It must contain emoji's name.(default:undefined)                                                                                                                                                                   | emoji.name[]                                                             | no       | iOS/Android | yes               |

### Full list of theme properties

| Name                       | Description                                                                                   | Type   | Required | Platform    | HarmonyOS Support |
| -------------------------- | --------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| `backdrop`                 | Set background-color of the modal backdrop.(default:#00000055)                                | string | no       | iOS/Android | yes               |
| `knob`                     | Set background-color of the modal knob.(default:#ffffff)                                      | string | no       | iOS/Android | yes               |
| `container`                | Set background-color of the whole modal container.(default:#ffffff)                           | string | no       | iOS/Android | yes               |
| `header`                   | Set category name text color.(default:#00000099)                                              | string | no       | iOS/Android | yes               |
| `skinTonesContainer`       | Set background-color of the skin tones container.(default:#e3dbcd)                            | string | no       | iOS/Android | yes               |
| `category.icon`            | color of the icon.(default:#000000)                                                           | string | no       | iOS/Android | yes               |
| `category.iconActive`      | color of the icon if it's active.(default:#005b96)                                            | string | no       | iOS/Android | yes               |
| `category.container`       | background-color of the categories container.(default:#e3dbcd)                                | string | no       | iOS/Android | yes               |
| `category.containerActive` | background-color of the currently active category.(default:#ffffff)                           | string | no       | iOS/Android | yes               |
| `search.text`              | color of the search bar text.(default:#000000cc)                                              | string | no       | iOS/Android | yes               |
| `search.placeholder`       | color of the search bar placeholder text.(default:#00000055)                                  | string | no       | iOS/Android | yes               |
| `search.icon`              | color of the search bar icon.(default:#00000055)                                              | string | no       | iOS/Android | yes               |
| `search.background`        | background-color of the search bar.(default:#00000011)                                        | string | no       | iOS/Android | yes               |
| `emoji.selected`           | color of the selected emoji background.Works only with selectedEmojis prop. (default:#e3dbcd) | string | no       | iOS/Android | yes               |

### Full list of styles properties

| Name        | Description                                                                                                                               | Type                                      | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------- | -------- | ----------- | ----------------- |
| `container` | Set styles of the whole modal container.(default:{})                                                                                      | ViewStyle                                 | no       | iOS/Android | yes               |
| `header`    | Set styles of header text. Header is the component containing category name.(default:{})                                                  | TextStyle                                 | no       | iOS/Android | yes               |
| `knob`      | Set styles of the modal knob.Works only in the modal mode with knob enabled.(default:{})                                                  | ViewStyle                                 | no       | iOS/Android | yes               |
| `category`  | SSet styles of the category component. You can pass different styles for the container and the icon.(default:{ container: {}, icon: {} }) | { container: ViewStyle, icon: TextStyle } | no       | iOS/Android | yes               |
| `searchBar` | Set styles of the searchBar component. You can pass different styles for the container and the text.(default:{ container: {}, text: {} }) | { container: ViewStyle, text: TextStyle } | no       | iOS/Android | yes               |
| `emoji`     | Set styles of the emoji component. You can pass styles for selected state.(default:{ selected: {} })                                      | { selected: ViewStyle }                   | no       | iOS/Android | yes               |

### Full list of EmojisByCategory type

| Name  | Description | Type          | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------------- | -------- | ----------- | ----------------- |
| title | EmojisByCategory  title       | CategoryTypes | yes      | iOS/Android | yes               |
| data  | EmojisByCategory emoji data        | JsonEmoji[]   | yes      | iOS/Android | yes               |

### Full list of CategoryTypes type

| Name  | Description | Type          | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------------- | -------- | ----------- | ----------------- |
| `CategoryTypes` | CategoryTypes type | "search" \| "smileys_emotion" \| "people_body" \| "animals_nature" \| "food_drink" \| "travel_places" \| "activities" \| "objects" \| "symbols" \| "flags" \| "recently_used" | no       | iOS/Android | yes               |

### Full list of JsonEmoji type

| Name        | Description | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ----------- | -------- | -------- | ----------- | ----------------- |
| emoji       | JsonEmoji   emoji      | string   | yes      | iOS/Android | yes               |
| name        | JsonEmoji     name    | string   | yes      | iOS/Android | yes               |
| v           | JsonEmoji   version     | string   | yes      | iOS/Android | yes               |
| toneEnabled | JsonEmoji    toneEnabled     | boolean  | yes      | iOS/Android | yes               |
| keywords    | JsonEmoji  keywords       | string[] | no      | iOS/Android | yes               |

### Full list of EmojiType type

| Name        | Description | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ----------- | -------- | -------- | ----------- | ----------------- |
| emoji       | EmojiType   emoji      | string   | yes      | iOS/Android | yes               |
| name        | EmojiType     name    | string   | yes      | iOS/Android | yes               |
| slug           | EmojiType   slug     | string   | yes      | iOS/Android | yes               |
| unicode_version | EmojiType   version     | string  | yes      | iOS/Android | yes               |
| toneEnabled    | EmojiType  toneEnabled       | boolean | yes      | iOS/Android | yes               |
| alreadySelected    | EmojiType alreadySelected     | boolean | no      | iOS/Android | yes               |

## 静态方法

### useRecentPicksPersistence

The library gives you the possibility to persists recent emoji picks by your own. This mean that you can use for that reason whatever you want.

Async storage? - sure. Backend as store - no problem. Choose how you want to handle it, we only require a Promise

> [!TIP] This functionality requires to enable enableRecentlyUsed in your emoji keyboard component

> [!TIP] This hook will have impact on every rn-emoji-keyboard instance used in app that have enabled recent picks.

> [!TIP] To ensure smooth experience we recommend that you use it as high as possible in the React structure. eg. App.tsx file

| Name             | Description                                                                                                | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `initialization` | This property is used at the very beginning to restore previous state.                                     | Function | yes      | iOS/Android | yes               |
| `onStateChange`  | This property is used every time when user selects emoji and keyboard has enabled enableRecentlyUsed props | Function | yes      | iOS/Android | yes               |

## 遗留问题

- [ ] rn-emoji-keyboard 的键盘弹出后回弹默认高度表情键盘无法点击: [issue#1](https://github.com/react-native-oh-library/rn-emoji-keyboard/issues/1)
- [ ] rn-emoji-keyboard 展开旋钮动画卡顿: [issue#2](https://github.com/react-native-oh-library/rn-emoji-keyboard/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/TheWidlarzGroup/rn-emoji-keyboard/blob/master/LICENSE) ，请自由地享受和参与开源。
