> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-multiple-select</code> </h1>
</p>

> [!TIP] [ GitHub address](https://github.com/toystars/react-native-multiple-select)

请到三方库的 Releases发布地址查看配套的版本信息：

| 三方库版本 | 支持RN版本 |
| ----------| ---------- |
| 0.5.12    |  0.72/0.77 |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-multiple-select@0.5.12
```

#### **yarn**

```bash
yarn add react-native-multiple-select@0.5.12
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import { FlatList, Text, View } from 'react-native';
import MultiSelect from 'react-native-multiple-select';

const items = [{
    id: '92iijs7yta',
    name: 'Ondo'
  }, {
    id: 'a0s0a8ssbsd',
    name: 'Ogun'
  }, {
    id: '16hbajsabsd',
    name: 'Calabar'
  }, {
    id: 'nahs75a5sg',
    name: 'Lagos'
  }, {
    id: '667atsas',
    name: 'Maiduguri'
  }, {
    id: 'hsyasajs',
    name: 'Anambra'
  }, {
    id: 'djsjudksjd',
    name: 'Benue'
  }, {
    id: 'sdhyaysdj',
    name: 'Kaduna'
  }, {
    id: 'suudydjsjd',
    name: 'Abuja'
    }
];

export default class MultiSelectExample extends Component {

  state = {
    selectedItems : []
  };

  onSelectedItemsChange = (selectedItems: any) => {
    this.setState({ selectedItems });
  };

  multiSelect!: MultiSelect | any;

  render() {
    const { selectedItems } = this.state;

    return (
      <View style={{ flex: 1 }}>
        <MultiSelect
          hideTags
          items={items}
          uniqueKey="id"
          ref={(component) => { this.multiSelect = component }}
          onSelectedItemsChange={this.onSelectedItemsChange}
          selectedItems={selectedItems}
          selectText="Pick Items"
          searchInputPlaceholderText="Search Items..."
          onChangeInput={ (text)=> console.log(text)}
          altFontFamily="ProximaNova-Light"
          tagRemoveIconColor="#CCC"
          tagBorderColor="#CCC"
          tagTextColor="#CCC"
          selectedItemTextColor="#CCC"
          selectedItemIconColor="#CCC"
          itemTextColor="#000"
          displayKey="name"
          searchInputStyle={{ color: '#CCC' }}
          submitButtonColor="#CCC"
          submitButtonText="Submit"
        />
        <View>
          {this.multiSelect&&this.multiSelect.getSelectedItemsExt(selectedItems)}
        </View>
      </View>
    );
  }
}


export {MultiSelectExample}


```
## 约束与限制

### 注意事项

本库 HarmonyOS 侧需要引入字体包，如下所示。如已引用，则无需再次引入，可跳过本章节步骤，直接使用。

在HarmonyOS工程中的entry/src/main/ets/pages/index.ets中添加如下代码：

```diff
  ...
RNApp({
    rnInstanceConfig: {
+    fontResourceByFontFamily: {
+      'Pacifico-Regular': $rawfile("fonts/Pacifico-Regular.ttf"),
+    }
    },
})
```
### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK: HarmonyOS NEXT Developer Beta6; IDE: DevEco Studio 5.0.3.706; ROM: 3.0.0.61;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `altFontFamily`  | 搜索输入框占位符文本的字体族 |  String | no     | All  | yes      |
| `canAddItems`  | 默认为"false"。这允许用户向提供的项目列表中添加项目。您需要在onAddItem函数属性中处理添加新项目。可以使用本机键盘上的回车键添加项目| Boolean  |  no     | All   | yes      |
| `displayKey`  | 默认为"name"。此字符串将用于选择在items数组中显示对象的键| String  |  no     | All   | yes      |
| `fixedHeight`  | 默认为false。指定选择下拉菜单是采用内容高度还是带滚动条的固定高度（当组件嵌套在ScrollView中时，此行为存在问题，滚动事件只会分派给父ScrollView，选择组件将不可滚动）。有关更多信息，请参见此问题| Boolean  |  no     | All   | yes      |
| `filterMethod`  | 默认为"partial"。选项：["partial", "full"] 选择系统根据搜索词过滤项目的逻辑。partial：检查所有单独的单词，如果至少有一个单词匹配，则包含该项目。full：检查以确保项目按顺序包含搜索词的完整子字符串，不包括任何前导或尾随空格| String  |  no     | All   | yes      |
| `flatListProps`  | FlatList的属性。传递下拉菜单FlatList所需的任何属性| Object  |  no     | All   | yes      |
| `fontFamily`  | 组件中使用的自定义字体族（影响除上述searchInputPlaceholderText之外的所有文本）| String  |  no     | All   | yes      |
| `fontSize`  | 多选中标记显示的选定项目名称的字体大小。| Number  |  no     | All   | yes      |
| `hideDropdown`  | 默认为false。隐藏带有取消按钮的下拉菜单，使用返回箭头| Boolean  |  no     | All   | yes      |
| `hideSubmitButton`  | 默认为false。从下拉菜单中隐藏提交按钮，而是在搜索字段中使用箭头按钮| Boolean  |  no     | All   | yes      |
| `hideTags`  | 默认为false。隐藏标记化的选定项目，以防选定项目在视图中的其他位置显示（请查看下面的更多信息）| Boolean  |  no     | All   | yes      |
| `searchIcon`  | 更改搜索图标的元素或功能组件| Element, Object, boolean, Function |  no     | All   | yes      |
| `itemFontFamily`  | 多选下拉菜单中每个未选定项目的字体族| String  |  no     | All   | yes      |
| `itemFontSize`  | 多选下拉菜单中每个项目的字体大小| Number  |  no     | All   | yes      |
| `itemTextColor`  | 多选下拉菜单中每个未选定项目的文本颜色| String  |  no     | All   | yes      |
| `items`  | 在多选组件中显示的项目列表。JavaScript对象数组。每个对象必须包含名称和唯一标识符（请查看上面的示例）| Array, control prop  |  	yes     | All   | yes      |
| `noItemsText`  | 替换默认"没有要显示的项目"的文本| String  |  no     | All   | yes      |
| `onAddItem`  | 作为参数传入的JavaScript函数。每次添加新项目时都会调用该函数，并接收整个项目列表。在这里，您应该确保将新项目添加到您提供的项目列表中，以及处理添加新项目的其他后果| function  |  no     | All   | yes      |
| `onChangeInput`  | 作为参数传入的JavaScript函数。每次TextInput更改时都会调用该函数，并传递值| function  |  no     | All   | yes      |
| `onClearSelector`  | 作为参数传入的JavaScript函数。每次按下返回按钮时都会调用该函数| function  |  no     | All   | yes      |
| `onSelectedItemsChange`  | 作为参数传入的JavaScript函数。该函数需要定义一个参数（selectedItems）。当点击提交按钮（多选）或点击项目（单选）时触发。（请查看上面的示例）| function  |  yes     | All   | yes      |
| `onToggleList`  | 作为参数传入的JavaScript函数。每次按下多选组件时都会调用该函数| function  |  no     | All   | yes      |
| `searchInputPlaceholderText`  | 多选过滤器输入框中显示的占位符文本| String  |  no     | All   | yes      |
| `searchInputStyle`  | 多选输入元素的样式对象| Object  |  no     | All   | yes      |
| `selectText`  | 主组件中显示的文本| String  |  no     | All   | yes      |
| `selectedText`  | 选择项目时显示的文本，可以替换为任何字符串| String  |  no     | All   | yes      |
| `selectedItemFontFamily`  | 多选下拉菜单中每个选定项目的字体族| String  |  no     | All   | yes      |
| `selectedItemIconColor`  | 多选下拉菜单中每个选定项目的选中复选图标的颜色| String  |  no     | All   | yes      |
| `selectedItemTextColor`  | 多选下拉菜单中每个选定项目的文本颜色| String  |  no     | All   | yes      |
| `single`  | 在单选和多选之间切换选择组件| Boolean  |  no     | All   | yes      |
| `styleDropdownMenu`  | 设置下拉菜单视图的样式| Style  |  no     | All   | yes      |
| `styleDropdownMenuSubsection`  | 设置下拉菜单内部视图的样式| Style  |  no     | All   | yes      |
| `styleIndicator`  | 设置指示器图标的样式| Style  |  no     | All   | yes      |
| `styleInputGroup`  | 设置文本输入组容器的样式| Style  |  no     | All   | yes      |
| `styleItemsContainer`  | 设置列表中显示的项目容器的样式| Style  |  no     | All   | yes      |
| `styleListContainer`  | 设置主列表容器的样式| Style  |  no     | All   | yes      |
| `styleMainWrapper`  | 设置多选器主容器的样式| Style  |  no     | All   | yes      |
| `styleRowList`  | 设置显示在您之后的行的样式| Style  |  no     | All   | yes      |
| `styleSelectorContainer`  | 设置用户点击下拉菜单时选择器容器的样式| Style  |  no     | All   | yes      |
| `styleTextDropdown`  | 设置下拉菜单文本的样式| Text Style  |  no     | All   | yes      |
| `styleTextDropdownSelected`  | 设置选定下拉菜单文本的样式| Text Style  |  no     | All   | yes      |
| `styleTextTag`  | 设置标签文本的样式| Text Style  |  no     | All   | yes      |
| `submitButtonColor`  | 提交按钮的背景颜色| String  |  no     | All   | yes      |
| `submitButtonText`  | 提交按钮上显示的文本| String  |  no     | All   | yes      |
| `tagBorderColor`  | 每个选定项目的边框颜色| String  |  no     | All   | yes      |
| `tagContainerStyle`  | 设置标签视图容器的样式| Style  |  no     | All   | yes      |
| `tagRemoveIconColor`  | 选定项目列表中用于移除图标的颜色| String  |  no     | All   | yes      |
| `tagTextColor`  | 选定项目列表的文本颜色| String  |  no     | All   | yes      |
| `textColor`  | 多选中标记显示的选定项目名称的颜色| String  |  no     | All   | yes      |
| `textInputProps`  | 文本输入的属性。传递文本输入所需的任何属性| Object  |  no     | All   | yes      |
| `uniqueKey`  | 每个项目属性中的唯一标识符。在内部用作识别每个项目的手段（请查看下面的示例）| String  |  yes     | All   | yes      |
| `selectedItems`  | 选定项目键的列表。JavaScript字符串数组，可以与组件一起实例化| Array, control prop  |  no     | All   | yes      |
| `removeSelected`  | 从列表中过滤选定的项目以在列表中显示| Boolean  |  no     | All   | yes      |


## 遗留问题

## 其他

## 开源协议
本项目基于 [The MIT License (MIT)](https://github.com/toystars/react-native-multiple-select/blob/master/LICENSE) ，请自由地享受和参与开源。