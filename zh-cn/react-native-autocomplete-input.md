> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-autocomplete-input</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/byteburgers/react-native-autocomplete-input">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/byteburgers/react-native-autocomplete-input/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/byteburgers/react-native-autocomplete-input)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：
| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 5.5.6     | [react-native-autocomplete-input release](https://github.com/byteburgers/react-native-autocomplete-input/releases) | 0.72/0.77       |

<!-- tabs:start -->
进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install --save react-native-autocomplete-input@5.5.6
```

#### **yarn**

```bash
yarn add react-native-autocomplete-input@5.5.6
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { Component } from 'react';
import { View, Text, StyleSheet, TouchableOpacity} from 'react-native';
import AutocompleteInput from 'react-native-autocomplete-input';


const styles = StyleSheet.create({
    containerStyle: {
        borderColor: "#e0494e",
        borderWidth: 5,
        borderRadius: 15,
        width: '100%'
    },
    inputContainerStyle: {
        borderWidth: 3,
        borderColor: "green",

    },
    listContainerStyle: {
        backgroundColor: "yellow"
    },
    itemText: {
        paddingTop: 10,
        paddingBottom: 10,

    },

});

interface AutocompleteItem {
    id: number;
    value: string;
}

const testArray: AutocompleteItem[] = [{ id: 1, value: 'Aabbbbbbb' }, { id: 2, value: 'BBFFFFF' }, { id: 3, value: 'ccccccbbb' }]

function filterData(query: string): AutocompleteItem[] {
    if (query) {
        const filteredItems = testArray.filter(item => item.value.toLowerCase().includes(query.toLowerCase()));
        return filteredItems;
    } else {
        return [];
    }
}

function compare(selectName: string, value: string): boolean {
    return selectName === value;
}

class App extends Component {
    state = {
        query: '', 
        isVisible: true,
        selectName: ''
    };

    render() {
        const { query, isVisible } = this.state;
        const data = filterData(query);
        return (
            <View style={{ backgroundColor: '#d1f8f7', height: '100%' ,paddingTop:100}}>
                <AutocompleteInput
                    containerStyle={styles.containerStyle} 
                    inputContainerStyle={styles.inputContainerStyle} 
                    listContainerStyle={styles.listContainerStyle}
                    data={data.length === 1 && compare(this.state.selectName, data[0].value) ? [] : data} 
                    value={query} 
                    onChangeText={(text) => {

                        if (text.trim() !== this.state.selectName.trim()) {
                            this.setState({
                                isVisible: false,
                                selectName: text
                            });
                        } else {
                            this.setState({
                                isVisible: false,
                                selectName: text
                            });
                        }
                        this.setState({ query: text});
                        console.log("--------onChangeText--++++isVisible:" + isVisible)
                    }} 

                    onShowResults={() => { console.log("--------+++++++++ onShowResults "); }} 
                    
                    hideResults={isVisible} 

                    flatListProps={{
                        keyExtractor: (_, idx) => String(idx),
                        keyboardShouldPersistTaps: 'always', 
                        renderItem: ({ item }) => {
                            return (
                                <TouchableOpacity onPress={() => {
                                    this.setState({ query: item.value, isVisible: true, selectName: item.value });
                                    console.log("--------onPress--++++isVisible:" + isVisible)
                                }}>
                                    <Text style={styles.itemText}>{item.value}</Text>
                                </TouchableOpacity>
                            )
                        },
                    }} 
                />
            </View>
        );
    }
}



export default App;
```
## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## 属性
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| containerStyle      | 这些样式将应用于环绕自动完成组件的容器 | style    | no       | Android/iOS | yes               |
| hideResults         | 设置为 `true` 以隐藏建议列表 | bool     | no       | Android/iOS | yes               |
| data                | 包含要在 `renderItem({ item, i })` 中渲染的建议项的数组。任何长度 > 0 的数组将打开建议列表，任何长度 < 1 的数组将隐藏列表 | array    | no       | Android/iOS | yes               |
| inputContainerStyle | 这些样式将应用于环绕文本输入组件的容器 | style    | no       | Android/iOS | yes               |
| listContainerStyle  | 这些样式将应用于环绕结果列表的容器 | style    | no       | Android/iOS | yes               |
| onShowResults       | 当自动完成建议出现或消失时将被调用 | function | no       | Android/iOS | yes               |
| renderTextInput     | 渲染自定义文本输入组件。所有属性都传递给此函数 | function | no       | Android/iOS | yes               |
| flatListProps       | 传递给 FlatList 的自定义属性 | object   | no       | Android/iOS | yes               |
| renderResultList    | 渲染自定义结果列表。可用于替换 FlatList。所有属性都传递给此函数 | function | no       | Android/iOS | yes               |

## 遗留问题

- [ ] 源库5.5.2版本在 HarmonyOS NEXT 上打字时键盘会隐藏: [issue#1](https://github.com/byteburgers/react-native-autocomplete-input/issues/328)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/byteburgers/react-native-autocomplete-input/blob/main/LICENSE) ，请自由地享受和参与开源。