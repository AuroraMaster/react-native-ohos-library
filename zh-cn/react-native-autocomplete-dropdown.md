> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-autoComplete-dropdown</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/onmotion/react-native-autocomplete-dropdown">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/onmotion/react-native-autocomplete-dropdown/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/onmotion/react-native-autocomplete-dropdown)

## 安装与使用

| 三方库版本 | 支持RN版本 |
| ---------- | ---------- |
| 4.0.0      | 0.72       |
| 4.3.1      | 0.77       |

<!-- tabs:start -->

####  npm

```bash
# V4.0.0
npm install react-native-autocomplete-dropdown@4.0.0

# V4.3.1
npm install react-native-autocomplete-dropdown@4.3.1
```

#### yarn

```bash
# V4.0.0
yarn add react-native-autocomplete-dropdown@4.0.0

# V4.3.1
yarn add react-native-autocomplete-dropdown@4.3.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

1. Wrap your root component in AutocompleteDropdownContextProvider from react-native-autocomplete-dropdown

```jsx
import { AutocompleteDropdownContextProvider } from 'react-native-autocomplete-dropdown';
import { AppRegistry } from 'react-native'

AppRegistry.setWrapperComponentProvider(appParams => {
  return ({ children }) => (
      <AutocompleteDropdownContextProvider >
        {children}
      </AutocompleteDropdownContextProvider>
  );
});


```

2. Example with local Dataset

```jsx
import React, { memo, useState } from 'react'
import { Text, View } from 'react-native'
import type { TAutocompleteDropdownItem } from 'react-native-autocomplete-dropdown'
import { AutocompleteDropdown } from 'react-native-autocomplete-dropdown'

const ItemSeparatorComponent = () => <View style={{ height: 1, width: '100%', backgroundColor: '#d8e1e6' }} />

export const LocalDataSetExample = memo(() => {
  const [selectedItem, setSelectedItem] = useState<TAutocompleteDropdownItem | null>(null)

  return (
    <>
      <AutocompleteDropdown
        clearOnFocus={false}
        closeOnBlur={true}
        showClear={false}
        initialValue={{ id: '2' }} // or just '2'
        onSelectItem={item => setSelectedItem(item)}
        dataSet={[
          { id: '1', title: 'Alpha' },
          { id: '2', title: 'Beta' },
          { id: '3', title: 'Gamma' },
        ]}
        ignoreAccents
      />
      <Text style={{ color: '#668', fontSize: 13 }}>Selected item: {JSON.stringify(selectedItem)}</Text>
    </>
  )
}

```

## Link

本库 HarmonyOS 侧实现依赖react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[react-native-svg 文档](/zh-cn/react-native-svg-capi.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0.47 (API Version 20); IDE：DevEco Studio 6.0.0.858; ROM：6.0.0.107;

   
## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `dataSet` | 列表项的集合 | array | no | iOS/Android | yes |
| `initialValue` | 字符串（id）或包含 id 的对象 | object \| string | no | iOS/Android | yes |
| `loading` | 加载状态 | boolean | no | iOS/Android | yes |
| `useFilter` | 是否使用基于 dataSet 的本地过滤（对于远程过滤，设置为 false 很有用，以防止重复渲染） | boolean | no | iOS/Android | yes |
| `showClear` | 显示清除按钮 | boolean | no | iOS/Android | yes |
| `showChevron` | 显示箭头（展开/关闭）按钮 | boolean | no | iOS/Android | yes |
| `closeOnSubmit` | 设置最大描边线宽 | boolean | no | iOS/Android | yes |
| `clearOnFocus` | 聚焦时是否清除已输入的文本 | boolean | no | iOS/Android | yes |
| `caseSensitive` | 是否执行区分大小写的搜索 | boolean | no | iOS/Android | yes |
| `ignoreAccents` | 忽略变音符号 | boolean | no | iOS/Android | yes |
| `trimSearchText` | 去除搜索文本的首尾空格 | boolean | no | iOS/Android | yes |
| `editable` | textInput 是否可编辑 | boolean | no | iOS/Android | yes |
| `debounce` | 调用 onChangeText 前等待的毫秒数 | number | no | iOS/Android | yes |
| `suggestionsListMaxHeight` | 下拉列表的最大高度 | number | no | iOS/Android | yes |
| `direction` | "up"（向上）或 "down"（向下） | up \| down | no | iOS/Android | yes |
| `matchFrom` | 是从标题开头匹配建议，还是在标题任意位置匹配。可能的值为 "any" 或 "start" | any \| start | no | iOS/Android | yes |
| `onChangeText` | textInput 的 onChangeText 事件 | function | no | iOS/Android | yes |
| `onSelectItem` | onSelectItem 事件 | function | no | iOS/Android | yes |
| `onOpenSuggestionsList` | onOpenSuggestionsList 事件 | function | no | iOS/Android | yes |
| `onChevronPress` | onChevronPress 事件 | function | no | iOS/Android | yes |
| `onClear` | 清除按钮按下时的事件 | function | no | iOS/Android | yes |
| `onSubmit` | 键盘提交按钮按下时的事件 | function | no | iOS/Android | yes |
| `onBlur` | 文本输入失去焦点时触发的事件 | function | no | iOS/Android | yes |
| `onFocus` | 文本输入获得焦点时的事件 | function | no | iOS/Android | yes |
| `renderItem` | 用于渲染列表项的 JSX (item, searchText) => JSX | function | no | iOS/Android | yes |
| `controller` | 返回模块控制器的引用，包含方法 close, open, toggle, clear, setInputText, setItem | function | no | iOS/Android | yes |
| `containerStyle` | 容器样式 | ViewStyle | no | iOS/Android | yes |
| `inputContainerStyle` | 自定义输入框容器样式 | ViewStyle | no | iOS/Android | yes |
| `rightButtonsContainerStyle` | 右侧按钮容器样式 | ViewStyle | no | iOS/Android | yes |
| `suggestionsListContainerStyle` | 建议列表容器样式 | ViewStyle | no | iOS/Android | yes |
| `suggestionsListTextStyle` | 建议列表文本样式 | TextStyle | no | iOS/Android | yes |
| `rightIconComponent` | 自定义箭头图标 | React.Component | no | iOS/Android | yes |
| `ChevronIconComponent` | 自定义箭头图标 | React.Component | no | iOS/Android | yes |
| `ClearIconComponent` | 自定义清除图标 | React.Component | no | iOS/Android | yes |
| `EmptyResultComponent` | 替换结果为空时的默认组件 | React.Component | no | iOS/Android | yes |
| `InputComponent` | 输入元素组件 | React.ComponentType | no | iOS/Android | yes |
| `emptyResultText` | 替换结果为空时的默认文本 "Nothing found" | string | no | iOS/Android | yes |
| `textInputProps` | 文本输入属性 | TextInputProps | no | iOS/Android | yes |
| `flatListProps` | 传递给 `FlatList` 组件的属性 | FlatListProps | no | iOS/Android | yes |
| `caseSensitive`<sup>4.3.1+</sup> | 是否执行区分大小写的搜索 | bool | no | iOS/Android | yes |
| `editable`<sup>4.3.1+</sup> | textInput 是否可编辑 | bool | no | iOS/Android | yes |


## 遗留问题

- [ ] TextInput在页面底部时，键盘弹起会导致View标签measure方法计算pageY错误,导致dropdown位置不正确,RN框架问题。

## 其他

- closeOnBlur、bottomOffset属性在4.0.0-rc5版本不支持，源码组件入口props中不接收这两个属性 [源码：index.tsx](https://github.com/onmotion/react-native-autocomplete-dropdown/blob/main/src/index.tsx#L59)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/onmotion/react-native-autocomplete-dropdown/blob/main/LICENSE) ，请自由地享受和参与开源。
