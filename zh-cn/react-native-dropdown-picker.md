模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-dropdown-picker</code> </h1>
</p>

请到三方库的 Releases 发布地址查看配套的版本信息：

| Version    | Support RN version |
| ---------- | ----------         |
| 5.4.6      | 0.72/0.77          |


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-dropdown-picker@5.4.6
```

#### **yarn**

```bash
yarn add react-native-dropdown-picker@5.4.6
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text } from "react-native";
import DropDownPicker from "react-native-dropdown-picker";

export default function App() {
  const [open, setOpen] = useState(false);
  const [value, setValue] = useState(null);
  const [items, setItems] = useState([
    { label: "Apple", value: "apple" },
    { label: "Banana", value: "banana" },
    { label: "Pear", value: "pear" },
  ]);

  return (
    <View style={{ flex: 1 }}>
      <View
        style={{
          flex: 1,
          alignItems: "center",
          justifyContent: "center",
          paddingHorizontal: 15,
        }}
      >
        <DropDownPicker
          open={open}
          value={value}
          items={items}
          setOpen={setOpen}
          setValue={setValue}
          setItems={setItems}
          placeholder={"Choose a fruit."}
        />
      </View>

      <View
        style={{
          flex: 1,
          alignItems: "center",
          justifyContent: "center",
        }}
      >
        <Text>Chosen fruit: {value === null ? "none" : value}</Text>
      </View>
    </View>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25 (API Version 12 Canary4); IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Description                                                                                                      | Type                                                               | Required | Platform | HarmonyOS Support |
|----------------------------|------------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------|----------|----------|-------------------|
| items                      | 保存项目的状态变量。                                                                             | array                                                              | yes      | All      | yes               |
| value                      | 指定所选项目值的状态变量。对于多项选择器，它是一个值数组。 | string\|string[]                                                   | yes      | All      | yes               |
| open                       | 指定选择器是否打开的状态变量。                                                        | boolean                                                            | yes      | All      | yes               |
| props                      | 为容器TouchableOpacity添加原生属性。                                                            | object                                                             | no       | All      | yes               |
| itemProps                  | 为每个项目的TouchableOpacity添加原生属性。                                                         | object                                                             | no       | All      | yes               |
| containerProps             | 为容器添加原生属性。                                                                             | object                                                             | no       | All      | yes               |
| labelProps                 | 为所选项目的Text元素添加原生属性。                                                     | object                                                             | no       | All      | yes               |
| multiple                   | 可以选择多个项目                                                                                    | boolean                                                            | no       | All      | yes               |
| min                        | 指定项目的最小数量。                                                                           | number                                                             | no       | All      | yes               |
| max                        | 指定项目的最大数量。                                                                           | number                                                             | no       | All      | yes               |
| disabled                   | 禁用选择器。                                                                                             | boolean                                                            | no       | All      | yes               |
| maxHeight                  | 下拉框的最大高度。                                                                                 | number                                                             | no       | All      | yes               |
| disableBorderRadius        | 禁止打开时更改边框半径。                                                                | boolean                                                            | no       | All      | yes               |
| stickyHeader               | 使分类粘在屏幕顶部，直到下一个分类将其推离。                                | boolean                                                            | no       | All      | yes               |
| autoScroll                 | 自动滚动到第一个选定的项目。                                                                | boolean                                                            | no       | All      | yes               |
| testID                     | 用于在端到端测试中定位选择器。                                                                   | string                                                             | no       | All      | yes               |
| zIndex                     | 指定堆叠顺序。                                                                                       | number                                                             | no       | All      | yes               |
| zIndexInverse              | 指定反向堆叠顺序。                                                                               | number                                                             | no       | All      | yes               |
| setOpen                    | 当用户按下选择器时调用的状态回调。                                                  | (open: boolean) => void                                            | yes      | All      | yes               |
| setItems                   | 调用以修改或添加新项目的状态回调。                                                        | (callback: SetStateAction[]) => void                               | no       | All      | yes               |
| setValue                   | 当值改变时调用的状态回调。                                                            | (callback: SetStateAction) => void                                 | yes      | All      | yes               |
| onChangeValue              | 返回当前值的回调。                                                                         | (value: ValueType) => void \| (value: ValueType[]) => void \| null | no       | All      | yes               |
| onSelectItem               | 返回所选项目/项目的回调。                                                                 | (item: ItemType) => void \| (items: ItemType[]) => void \| null    | no       | All      | yes               |
| onPress                    | 用户按下选择器时立即调用的回调。                                                  | (open: boolean) => void                                            | no       | All      | yes               |
| onOpen                     | 用户打开选择器时调用的回调。                                                          | () => void                                                         | no       | All      | yes               |
| onClose                    | 用户关闭选择器时调用的回调。                                                         | () => void                                                         | no       | All      | yes               |
| style                      | 设置样式                                                                                                        | object                                                             | no       | All      | yes               |
| containerStyle             | 设置容器样式                                                                                               | object                                                             | no       | All      | yes               |
| disabledStyle              | 设置禁用样式                                                                                                | object                                                             | no       | All      | yes               |
| textStyle                  | 设置文本样式                                                                                                    | object                                                             | no       | All      | yes               |
| labelStyle                 | 设置标签样式                                                                                                   | object                                                             | no       | All      | yes               |
| placeholder                | 占位符文本。                                                                                                | string                                                             | no       | All      | yes               |
| placeholderStyle           | 占位符样式                                                                                                 | object                                                             | no       | All      | yes               |
| showArrowIcon              | 指定箭头图标是否可见。                                                                  | boolean                                                            | no       | All      | yes               |
| showTickIcon               | 指定勾选图标是否可见。                                                                    | boolean                                                            | no       | All      | yes               |
| hideSelectedItemIcon       | 隐藏所选项目的图标。                                                                             | boolean                                                            | no       | All      | yes               |
| ArrowUpIconComponent       | 更改向上箭头图标。                                                                                       | function                                                           | no       | All      | yes               |
| ArrowDownIconComponent     | 更改向下箭头图标。                                                                                     | function                                                           | no       | All      | yes               |
| TickIconComponent          | 更改勾选图标。                                                                                           | function                                                           | no       | All      | yes               |
| CloseIconComponent         | 更改关闭图标。                                                                                          | function                                                           | no       | All      | yes               |
| arrowIconStyle             | 设置箭头图标样式                                                                                               | object                                                             | no       | All      | yes               |
| tickIconStyle              | 设置勾选图标样式                                                                                                | object                                                             | no       | All      | yes               |
| closeIconStyle             | 设置关闭图标样式                                                                                               | object                                                             | no       | All      | yes               |
| iconContainerStyle         | 设置图标容器样式                                                                                           | object                                                             | no       | All      | yes               |
| arrowIconContainerStyle    | 设置箭头图标容器样式                                                                                      | object                                                             | no       | All      | yes               |
| tickIconContainerStyle     | 设置勾选图标容器样式                                                                                       | object                                                             | no       | All      | yes               |
| closeIconContainerStyle    | 设置关闭图标容器样式                                                                                      | object                                                             | no       | All      | yes               |
| loading                    | 当项目尚未加载时显示活动指示器。                                                  | boolean                                                            | no       | All      | yes               |
| ActivityIndicatorComponent | 自定义活动指示器。                                                                                | function                                                           | no       | All      | yes               |
| activityIndicatorColor     | 更改活动指示器的默认颜色。                                                              | string                                                             | no       | All      | yes               |
| activityIndicatorSize      | 更改活动指示器的默认大小。                                                               | number                                                             | no       | All      | yes               |
| searchable                 | 启用下拉菜单/模态框中的搜索功能。                                                        | boolean                                                            | no       | All      | yes               |
| searchTextInputProps       | 为文本输入添加原生属性。                                                                            | object                                                             | no       | All      | yes               |
| searchWithRegionalAccents  | 允许在不输入本地重音符号的情况下进行搜索。                                                                   | boolean                                                            | no       | All      | no               |
| disableLocalSearch         | 禁用本地项目之间的搜索。这对于远程搜索很有用。                                      | boolean                                                            | no       | All      | yes               |
| addCustomItem              | 当没有内容可显示时，将搜索的文本显示为项目。                                                 | boolean                                                            | no       | All      | yes               |
| searchPlaceholder          | 更改文本输入的占位符文本。以下两个属性都可用。                  | string                                                             | no       | All      | yes               |
| onChangeSearchText         | 文本输入中的文本更改时调用的回调。                                                 | function                                                           | no       | All      | yes               |
| searchContainerStyle       | 设置搜索容器样式                                                                                         | object                                                             | no       | All      | yes               |
| searchTextInputStyle       | 设置搜索文本输入样式                                                                                         | object                                                             | no       | All      | yes               |
| searchPlaceholderTextColor | 设置搜索占位符文本颜色                                                                                   | string                                                             | no       | All      | yes               |
| customItemContainerStyle   | 设置自定义项目容器样式                                                                                     | object                                                             | no       | All      | yes               |
| customItemLabelStyle       | 设置自定义项目标签样式                                                                                         | object                                                             | no       | All      | yes               |
| categorySelectable         | 指定分类是否可选择。                                                                     | boolean                                                            | no       | All      | yes               |
| listParentContainerStyle   | 设置列表父容器样式                                                                                     | object                                                             | no       | All      | yes               |
| listParentLabelStyle       | 设置列表父标签样式                                                                                         | object                                                             | no       | All      | yes               |
| listChildContainerStyle    | 设置列表子容器样式                                                                                      | object                                                             | no       | All      | yes               |
| listChildLabelStyle        | 设置列表子标签样式                                                                                          | object                                                             | no       | All      | yes               |
| mode                       | 模式显示选定的项目。                                                                                    | 'DEFAULT'\|'SIMPLE'\|'BADGE'                                       | no       | All      | yes               |
| showBadgeDot               | 在徽章中显示点。                                                                                        | boolean                                                            | no       | All      | yes               |
| badgeProps                 | 为徽章容器TouchableOpacity添加原生属性。                                                      | object                                                             | no       | All      | yes               |
| extendableBadgeContainer   | 允许徽章在多行中展开。                                                                    | boolean                                                            | no       | All      | yes               |
| renderBadgeItem            | 渲染选定的项目。                                                                                      | function                                                           | no       | All      | yes               |
| badgeStyle                 | 设置徽章样式                                                                                                   | object                                                             | no       | All      | yes               |
| badgeTextStyle             | 设置徽章文本样式                                                                                               | object                                                             | no       | All      | yes               |
| badgeDotStyle              | 设置徽章点样式                                                                                                | object                                                             | no       | All      | yes               |
| badgeSeparatorStyle        | 设置徽章分隔符样式                                                                                          | object                                                             | no       | All      | yes               |
| badgeColors                | 根据值为徽章提供背景颜色。                                                            | object, string                                                     | no       | All      | yes               |
| badgeDotColors             | 根据值为徽章点提供背景颜色。                                                        | object, string                                                     | no       | All      | yes               |
| dropDownDirection          | 指定下拉菜单应打开的方向。                                                        | 'DEFAULT'\|'TOP'\|'BOTTOM'\|'AUTO'                                 | no       | All      | yes               |
| bottomOffset               | 指定最大底部偏移量。要使用此属性，您需要dropDownDirection="AUTO"。                         | number                                                             | no       | All      | yes               |
| onDirectionChanged         | 方向更改时调用的回调。                                                              | function                                                           | no       | All      | yes               |
| dropDownContainerStyle     | 设置下拉容器样式                                                                                       | object                                                             | no       | All      | yes               |
| itemKey                    | 指定应作为键使用的项目键。                                                                | string                                                             | no       | All      | yes               |
| closeAfterSelecting        | 选择项目后关闭选择器。                                                                       | boolean                                                            | no       | All      | yes               |
| closeOnBackPressed         | 按下返回按钮后关闭选择器。                                                                | boolean                                                            | no       | All      | yes               |
| itemSeparator              | 指定项目分隔符是否可见。                                                               | boolean                                                            | no       | All      | yes               |
| renderListItem             | 自定义renderListItem。                                                                                   | function                                                           | no       | All      | yes               |
| ListEmptyComponent         | 更改默认的ListEmptyComponent。                                                                          | function                                                           | no       | All      | yes               |
| listItemContainerStyle     | 设置列表项目容器样式                                                                                       | object                                                             | no       | All      | yes               |
| listItemLabelStyle         | 设置列表项目标签样式                                                                                           | object                                                             | no       | All      | yes               |
| selectedItemContainerStyle | 设置所选项目容器样式                                                                                   | object                                                             | no       | All      | yes               |
| selectedItemLabelStyle     | 设置所选项目标签样式                                                                                       | object                                                             | no       | All      | yes               |
| disabledItemContainerStyle | 设置禁用项目容器样式                                                                                   | object                                                             | no       | All      | yes               |
| disabledItemLabelStyle     | 设置禁用项目标签样式                                                                                       | object                                                             | no       | All      | yes               |
| listMessageContainerStyle  | 设置列表消息容器样式                                                                                    | object                                                             | no       | All      | yes               |
| listMessageTextStyle       | 设置列表消息文本样式                                                                                         | object                                                             | no       | All      | yes               |
| itemSeparatorStyle         | 设置项目分隔符样式                                                                                           | object                                                             | no       | All      | yes               |
| listMode                   | 选择列表模式时有3个选项。                                                                  | 'DEFAULT'\|'FLATLIST'\|'SCROLLVIEW'\|'MODAL'                       | no       | All      | yes               |
| flatListProps              | 为FlatList添加原生属性。                                                                              | object                                                             | no       | All      | yes               |
| scrollViewProps            | 为ScrollView添加原生属性。                                                                            | object                                                             | no       | All      | yes               |
| modalProps                 | 为Modal添加原生属性。                                                                                 | object                                                             | no       | All      | yes               |
| modalTitle                 | 设置模态框标题。listMode="MODAL"和searchable={false}是必需的。                                           | string                                                             | no       | All      | yes               |
| modalAnimationType         | 此属性控制模态框的动画方式。                                                                       | 'slide'\|'fade'\|'none'                                            | no       | All      | yes               |
| modalContentContainerStyle | 设置模态框内容容器样式                                                                                   | object                                                             | no       | All      | yes               |
| modalTitleStyle            | 设置模态框标题样式                                                                                              | object                                                             | no       | All      | yes               |
| rtl                        | 使组件从右到左。                                                                               | boolean                                                            | no       | All      | yes               |


## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                           | Type     | Required | Platform | HarmonyOS Support |
|-------------------|-------------------------------------------------------|----------|----------|----------|-------------------|
| setLanguage       | 您也可以全局更改默认语言。    | function | no       | All      | yes               |
| addTranslation    | 您可以向包中添加新的翻译。 | function | no       | All      | yes               |
| modifyTranslation | 修改现有翻译                        | function | no       | All      | yes               |
| addTheme          | 添加主题                                           | function | no       | All      | yes               |
| setTheme          | 更改默认主题                             | function | no       | All      | yes               |
## 遗留问题

- [ ] 方法String.prototype.normalize('NFD')在RN框架下有问题，导致属性searchWithRegionalAccents不生效。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/hossein-zare/react-native-dropdown-picker/blob/5.x/LICENSE) ，请自由地享受和参与开源。
