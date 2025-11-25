> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-action-sheet</code> </h1>
</p>

| Version |  Support RN version|
| ---------- |---------- |
| 4.0.1  | 0.72 |
| 4.1.1  | 0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
# 0.72 
npm install @expo/react-native-action-sheet@4.0.1

# 0.77 
npm install @expo/react-native-action-sheet@4.1.1
```

#### **yarn**

```bash
# 0.72 
yarn add @expo/react-native-action-sheet@4.0.1

# 0.77 
yarn add @expo/react-native-action-sheet@4.1.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import { ActionSheetProvider, connectActionSheet, ActionSheetProps } from '@expo/react-native-action-sheet';
import * as React from 'react';
import { useState } from 'react';
import { StyleSheet, Text, View, ScrollView, SafeAreaView } from 'react-native';
import ShowActionSheetButton from './ShowActionSheetButton';

type Props = ActionSheetProps & {
  useCustomActionSheet: boolean;
  setUseCustomActionSheet: (next: boolean) => void;
};

interface State {
  selectedIndex?: number | null;
  isModalOpen: boolean;
}

class App extends React.Component<Props, State> {
  state: State = {
    selectedIndex: null,
    isModalOpen: false,
  };

  _updateSelectionText = (selectedIndex?: number) => {
    this.setState({
      selectedIndex,
    });
  };

  _renderSelectionText = () => {
    const { selectedIndex } = this.state;
    const text =
      selectedIndex === null || selectedIndex === undefined
        ? 'No Option Selected'
        : `Option #${selectedIndex + 1} Selected`;
    return <Text style={styles.selectionText}>{text}</Text>;
  };

  _renderSectionHeader = (text: string) => {
    return <Text style={styles.sectionHeaderText}>{text}</Text>;
  };

  async _onShare() {
  }

  _renderButtons() {
    const { showActionSheetWithOptions } = this.props;
    return (
      <View
        style={{
          alignItems: 'center',
        }}>
        {this._renderSectionHeader('Android-Only Options')}
        <ShowActionSheetButton
          title="Icons"
          withIcons
          onSelection={this._updateSelectionText}
          showActionSheetWithOptions={showActionSheetWithOptions}
        />
        <ShowActionSheetButton
          title="Title, Message, & Icons"
          withTitle
          withMessage
          withIcons
          onSelection={this._updateSelectionText}
          showActionSheetWithOptions={showActionSheetWithOptions}
        />
        <ShowActionSheetButton
          title="Use Separators"
          withTitle
          withIcons
          withSeparators
          onSelection={this._updateSelectionText}
          showActionSheetWithOptions={showActionSheetWithOptions}
        />
        <ShowActionSheetButton
          title="Custom Styles"
          withTitle
          withMessage
          withIcons
          withCustomStyles
          onSelection={this._updateSelectionText}
          showActionSheetWithOptions={showActionSheetWithOptions}
        />
      </View>
    );
  }

  render() {
    return (
      <SafeAreaView style={styles.flex}>
        <ScrollView style={styles.flex} contentContainerStyle={styles.contentContainer}>
          {this._renderButtons()}
          {this._renderSelectionText()}
        </ScrollView>
      </SafeAreaView>
    );
  }
}

const ConnectedApp = connectActionSheet<any>(App);

export default function WrappedApp() {
  const [useCustomActionSheet, setUseCustomActionSheet] = useState(false);

  return (
    <ActionSheetProvider useCustomActionSheet={useCustomActionSheet}>
      <ConnectedApp
        useCustomActionSheet={useCustomActionSheet}
        setUseCustomActionSheet={setUseCustomActionSheet}
      />
    </ActionSheetProvider>
  );
}

const styles = StyleSheet.create({
  flex: {
    flex: 1,
  },
  contentContainer: {
    padding: 16,
    paddingVertical: 20,
  },
  headerText: {
    textAlign: 'center',
    fontSize: 16,
    marginBottom: 10,
  },
  notes: {
    marginTop: 32,
  },
  sectionHeaderText: {
    color: 'orange',
    textAlign: 'center',
    fontWeight: 'bold',
    fontSize: 20,
    marginTop: 20,
    marginBottom: 10,
  },
  selectionText: {
    textAlign: 'center',
    color: 'blue',
    fontSize: 16,
    marginTop: 20,
  },
});
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**showActionSheetWithOptions**

| Name   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `icons`  | 为每个选项显示对应的图标。如通过 `require`提供图片源路径，系统将自动渲染图片。也可提供矢量图标、预渲染图片等元素组成的数组 | array of required images or icons  | no     | Android/Web  | yes      |
| `tintIcons`  | 图标着色配置。默认启用图标着色以匹配文本颜色，设为 false 时保留图标原始色彩，适用于多色图标场景。自定义图标元素需预先处理着色， `tintIcons` 仅对 `tintColor` 图片资源生效  | boolean            |  no     | Android/Web  | yes      |
| `textStyle`  | 选项文本样式配置。如同时设置 tintColor，其优先级高于文本样式中的颜色属性 | TextStyle    | no     | Android/Web    | yes      |
| `titleTextStyle`  | 标题文本样式配置 | TextStyle      |  no     | Android/Web   | yes      |
| `messageTextStyle`  | 消息文本样式配置    | TextStyle      |  no     | Android/Web   | yes      |
| `autoFocus`  | 自动聚焦配置。设为 `true`时，ActionSheet 显示时自动为首选项启用屏幕阅读器聚焦。iOS 平台此为原生默认行为。   | boolean    |  no     | Android/Web   | yes      |
| `showSeparators`              | 在选项间显示分隔符。iOS 平台分隔符始终显示，此属性无效    | boolean    |no     | Android/Web/ios   | yes      |
| `containerStyle`   | 应用于容器的视图样式属性，用于替代默认外观 (如深色模式) | ViewStyle | no     | Android/Web | yes      |
| `separatorStyle`   | 修改分隔符外观，用于替代默认样式  |ViewStyle  |no     | Android/Web | yes      |
| `useModal`         |  默认值为 `false` (当autoFocus 也为`true` 时的默认值为 `true`)。使用 Modal 包装 ActionSheet，以确保在其他已打开的 Modal 组件前方显示 ([issue reference](https://github.com/expo/react-native-action-sheet/issues/164)) |boolean   | no     | Android/Web | yes      |
| `destructiveColor` |  危险操作选项文本颜色。 默认 `#d32f2f` |string    | no     | Android/Web  | yes      |
| `options` | 操作选项列表（必填） |array of strings   | no     | All  | yes      |
| `cancelButtonIndex` |	取消按钮位置索引 |number | no     | All  | yes      |
| `cancelButtonTintColor` | 取消按钮文本颜色 |string | no     | All  | yes      |
| `destructiveButtonIndex` | 危险操作按钮位置索引 | number or array of numbers | no     | All  | yes      |
| `title` | Action Sheet 顶部标题 |  string| no     | All  | yes      |
| `message` | Action Sheet 描述信息 | string | no     | All  | yes      |
| `tintColor` | 标准操作按钮选项文本颜色 | string | no     | All  | yes      |
| `disabledButtonIndices` | 禁用选项索引列表 | array of numbers | no     | All  | yes      |

**ActionSheetProvider**

| Name               | Description                                     | Type            | Required | Platform | HarmonyOS Support |
| ------------------ | ----------------------------------------------- | --------------- | -------- | -------- | ----------------- |
| `useCustomActionSheet` | iOS 平台专用属性，使用自定义纯 JavaScript ActionSheet (Android/Web version) 替代原生ActionSheetIOS 组件。默认值为 false | boolean   | no     | ios  | yes      |
| `useNativeDriver` | Windows 平台专用选项，为面向 Windows 10 版本 1809（Build 10.0.17763.0）及更早版本的 React Native Windows 项目提供禁用原生动画驱动的选项。版本 1903 及更高版本支持 useNativeDriver，如项目面向这些版本则无需设置此属性 | boolean   | no     | Web  | yes      |
## 遗留问题

## 其他

## 开源协议
本项目基于 [The MIT License (MIT)](https://github.com/expo/react-native-action-sheet/blob/master/LICENSE) ，请自由地享受和参与开源。
