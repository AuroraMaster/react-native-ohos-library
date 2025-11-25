> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-picker-select</code> </h1>
</p>

本项目基于 [react-native-picker-select@9.3.1](https://github.com/react-native-oh-library/react-native-picker-select) 开发。


请到三方库的 Releases 发布地址查看配套的版本信息：
| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 9.3.1     | [@react-native-oh-tpl/react-native-picker-select Releases](https://github.com/react-native-oh-library/react-native-picker-select/releases) | 0.72       |
| 9.4.0     | [@react-native-ohos/react-native-picker-select Releases]()     | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
# 0.72 
npm install @react-native-oh-tpl/react-native-picker-select

# 0.77 
npm install @react-native-ohos/react-native-picker-select
```

#### **yarn**

```bash
# 0.72 
yarn add @react-native-oh-tpl/react-native-picker-select

# 0.77 
yarn add @react-native-ohos/react-native-picker-select
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useRef, useState } from 'react';
import { StyleSheet, Text, View, TextInput, ScrollView } from 'react-native';
import RNPickerSelect from 'react-native-picker-select';

const sports = [
  {
    label: 'Football',
    value: 'football',
    key: 'football'
  },
  {
    label: 'Baseball',
    value: 'baseball',
    key: 'baseball'
  },
  {
    label: 'Hockey',
    value: 'hockey',
    key: 'hockey'
  },
];
const placeholder = {
  label: 'Select a sport...',
  value: null,
  color: '#9EA0A4',
};

export function PickerSelectExample() {
  const firstTextInputRef = useRef<TextInput | null>(null);
  const favSport0Ref = useRef<RNPickerSelect | null>(null);
  const favSport1Ref = useRef<RNPickerSelect | null>(null);

  const [stateval, setStateval] = useState({
    favSport0: undefined,
    favSport1: undefined,
    favSport2: undefined
  });

  return (
    <ScrollView style={{ flex: 1, backgroundColor: "#fff", }}>
      <Text>Standard TextInput</Text>
      <TextInput
        ref={firstTextInputRef}
        returnKeyType="next"
        enablesReturnKeyAutomatically
        onSubmitEditing={() => {
          favSport0Ref.current!.togglePicker(true, () => {
            console.log('togglePicker');
          });
        }}
        style={styles.inputAndroid}
        blurOnSubmit={false}
      />

      <View style={styles.paddingView} />

      <Text>useNativeAndroidPickerStyle (default)</Text>
      <RNPickerSelect
        ref={favSport0Ref}
        style={styles}
        placeholder={placeholder}
        items={sports}
        onValueChange={value => {
          setStateval({ ...stateval, favSport0: value });
        }}
        onUpArrow={() => {
          firstTextInputRef.current!.focus();
        }}
        onDownArrow={() => {
          favSport1Ref.current!.togglePicker();
        }}
        value={stateval.favSport0}
      />

      <View style={styles.paddingView} />

      <Text>set useNativeAndroidPickerStyle to false</Text>
      <RNPickerSelect
        ref={favSport1Ref}
        style={styles}
        placeholder={placeholder}
        items={sports}
        onValueChange={value => {
          setStateval({ ...stateval, favSport1: value });
        }}
        value={stateval.favSport1}
        useNativeAndroidPickerStyle={false}
      />

      <Text>example</Text>
      <RNPickerSelect
        style={styles}
        placeholder={placeholder}
        onValueChange={(value) => console.log(value)}
        items={[
          { label: 'Football', value: 'football' },
          { label: 'Baseball', value: 'baseball' },
          { label: 'Hockey', value: 'hockey' },
        ]}
      />
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#f8f9fa",
    alignItems: "center",
    justifyContent: "center"
  },
  paddingView: {
    margin: 10,
  },
  inputIOS: {
    fontSize: 16,
    paddingVertical: 12,
    paddingHorizontal: 10,
    borderWidth: 1,
    borderColor: 'gray',
    borderRadius: 4,
    color: 'black',
    paddingRight: 30, // to ensure the text is never behind the icon
  },
  inputAndroid: {
    width: 200,
    fontSize: 16,
    paddingHorizontal: 10,
    paddingVertical: 8,
    borderWidth: 0.5,
    borderColor: 'purple',
    borderRadius: 8,
    color: 'black',
    paddingRight: 30, // to ensure the text is never behind the icon
  },
});
```

## Link

本库依赖@react-native-oh-tpl/@react-native-picker/picker，如已在鸿蒙工程中引入过该库，则无需再次引入。

如未引入请参照[@react-native-oh-tpl/@react-native-picker/picker 文档](<https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-picker-picker(nocodegen).md>)进行引入。

## 约束与限制

### 兼容性

本文档内容基于以下环境验证通过：

1. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Default | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| onValueChange | 选中值变更回调函数，返回 `value， index`参数。 | function | null | yes | All | yes |
| items |  组件要渲染的选项数据。<br> - 选项的数据格式：<br>`{label: 'Orange', value: 'orange', key: 'orange', color: 'orange', inputLabel: 'Orange!', testID: 'e2e-orange'}`<br>- `label` 和 `value` 为必需字段<br>- `key`， `color`， `testID`， 和 `inputLabel` 为可选字段<br>- 未设置 `key` 时默认使用 `label` 值<br>- `value` 支持任意数据类型<br>- 设置 `inputLabel` 时输入框将显示该值替代`label` | array | null | yes | All | yes |
| placeholder | - 自定义占位符配置，默认显示 `Select an item...` ，值为 `null`。<br>- 可以使用空对象来禁用占位符。 | object | null | no | All | yes |
| disabled | 禁用与组件的交互。 | boolean | false | no | All | yes |
| value | 通过匹配 `items` 数组中项的 `value` 属性来选择当前选中项。找到匹配项时更新组件显示状态，未找到时默认选中首项。 **WARNING:** 在 iOS 平台，如需支持用户通过 `Picker` 交互动态更新选中值， 建议使用 `itemKey` 属性替代。 | any | null | no | All | yes |
| itemKey | 通过匹配 `items` 数组中项的 `key` 属性来定位选中项。若找到匹配的 `key` ，则更新组件显示对应项为选中状态；若未找到匹配的 `key` ，则回退至 `value` 匹配逻辑。 | string, number | undefined | no | All | yes |
| style | 组件样式覆盖配置。<br>_详见 [styling](https://github.com/lawnstarter/react-native-picker-select?tab=readme-ov-file#styling)_. | object | {} | no | All | yes |
| darkTheme | 启用选择器深色主题。 | boolean | false | no | iOS | yes |
| pickerProps | 传递给选择器的附加属性（部分属性涉及核心功能逻辑，请谨慎使用）。 | object | {} | no | All | yes |
| Icon | 自定义图标组件。<br>_详见 [styling](https://github.com/lawnstarter/react-native-picker-select?tab=readme-ov-file#示例项目 )_. | Component | null | no | All | yes |
| textInputProps | 透传给 TextInput 组件的附加属性（部分属性涉及核心功能逻辑，请谨慎使用）。默认仅 iOS 平台生效，除非设置 `useNativeAndroidPickerStyle={false}`。 | object | {} | no | All | yes |
| touchableWrapperProps | 传递给文本输入框包装容器的附加属性（部分属性涉及核心功能逻辑，请谨慎使用）。 | object | {} | no | All | yes |
| onOpen() | 选择器打开前立即触发的回调。<br>_使用 `useNativeAndroidPickerStyle={true}`时不支持。_  | function | null | no | All | yes |
| useNativeAndroidPickerStyle | 组件默认在未选中状态使用原生 Android 选择器样式。设置为 `false` 时将模拟 iOS 默认表现，显示可点击的文本输入框。<br>_详见 [styling](https://github.com/lawnstarter/react-native-picker-select?tab=readme-ov-file#styling)_. | boolean | true | no | Android | no |
| fixAndroidTouchableBug | 修复 [#354](https://github.com/lawnstarter/react-native-picker-select/issues/354). | boolean | false | no | Android | no |
| InputAccessoryView | 用于替换选择器顶部 InputAcessoryView 区域（包含选项卡箭头和完成按钮的工具栏）的自定义组件。可返回 `null` 完全隐藏该区域。虽然此类工具栏在 web `select` 元素中常见，但  [interface guidelines](https://developer.apple.com/ios/human-interface-guidelines/controls/pickers/) 未包含此设计。查看  [示例项目 ](https://snack.expo.io/@lfkwtz/react-native-picker-select) 了解自定义实现方式。 | Component | null | no | iOS | yes |
| doneText | 模态框中"Done"按钮的默认文本，支持自定义覆盖。 | string | "Done" | no | iOS | yes |
| onUpArrow() \/ onDownArrow() | 设置此回调函数启用对应方向箭头功能：<br>- 关闭选择器<br>- 执行提供的回调逻辑 | function | null | no | iOS | yes |
| onDonePress() | 点击完成按钮时触发的回调函数。 | function | null | no | iOS | yes |
| onClose(Bool) | 选择器关闭前立即触发的回调函数，包含一个布尔参数标识是否通过完成按钮关闭。 | function | null | no | iOS | yes |
| modalProps | 透传给 Modal 组件的附加属性（部分属性涉及核心功能逻辑，请谨慎使用）。 | function | null | no | iOS | yes |
| touchableDoneProps | 透传给完成按钮 Touchable 组件的附加属性（部分属性涉及核心功能逻辑，请谨慎使用）。 | function | null | no | iOS | yes |

## 遗留问题

- [ ] 属性useNativeAndroidPickerStyle在HarmonyOS中暂不支持 [issue#3](https://github.com/react-native-oh-library/react-native-picker-select/issues/3)
- [ ] 属性fixAndroidTouchableBug在HarmonyOS中暂不支持 [issue#4](https://github.com/react-native-oh-library/react-native-picker-select/issues/4)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lawnstarter/react-native-picker-select/blob/master/LICENSE) ，请自由地享受和参与开源。
