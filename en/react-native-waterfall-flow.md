> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-waterfall-flow</code> </h1>
</p>
<p align="center">
    <a href="https://www.npmjs.com/package/react-native-waterfall-flow">       
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/axerjs/react-native-waterfall-flow/blob/HEAD/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/axerjs/react-native-waterfall-flow)

## Installation and Usage

| version  |  Support RN version |
| ---------- | ---------- |
| 1.1.5      | 0.72/0.77      |

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install react-native-waterfall-flow@1.1.5
```

#### **yarn**

```bash
yarn add react-native-waterfall-flow@1.1.5
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { useState, useRef } from "react";
import {
  View,
  Text,
  StyleSheet,
  Button,
  RefreshControl,
  Alert,
} from "react-native";
import WaterfallFlow from "react-native-waterfall-flow";

const App = () => {
  const item = [
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
    "Item",
  ].map((l, i) => ({ id: l, text: i + ` ${l}` }));
  const [data, setData] = useState(item);
  const [refreshing, setRefreshing] = useState(false);
  const waterfallRef = useRef(null);

  const renderItem = ({ item }) => {
    return (
      <View style={styles.item}>
        <Text>{item.text}</Text>
      </View>
    );
  };

  const onRefresh = () => {
    setRefreshing(true);
    setTimeout(() => {
      setData([...item]);
      setRefreshing(false);
    }, 2000);
  };

  const onEndReached = () => {
    setData([
      ...data,
      { id: `${data.length + 1}`, text: `${data.length + 1} Item` },
      { id: `${data.length + 2}`, text: `${data.length + 2} Item` },
    ]);
  };

  return (
    <View style={styles.container}>
      <View style={{ flex: 1 }}>
        <WaterfallFlow
          ref={waterfallRef}
          renderItem={renderItem}
          data={data}
          numColumns={2}
          ListHeaderComponent={
            <Text style={styles.header}>Header Component</Text>
          }
          ListFooterComponent={
            <Text style={styles.footer}>Footer Component</Text>
          }
          ListEmptyComponent={
            <Text style={styles.empty}>No Data Available</Text>
          }
          onEndReached={onEndReached}
          onRefresh={onRefresh}
          refreshing={refreshing}
          style={styles.waterfall}
          contentContainerStyle={styles.contentContainer}
          refreshControl={
            <RefreshControl refreshing={refreshing} onRefresh={onRefresh} />
          }
        />
      </View>
      <View style={styles.buttonsContainer}>
        <Button
          title="Scroll to End"
          onPress={() => waterfallRef.current.scrollToEnd({ animated: true })}
        />
        <Button
          title="Scroll to Index"
          onPress={() => {
            data.length >= 20
              ? waterfallRef.current.scrollToIndex({
                  animated: true,
                  index: 20,
                  viewPosition: 0,
                })
              : false;
          }}
        />
        <Button
          title="Scroll to Offset"
          onPress={() => waterfallRef.current.scrollToOffset({ offset: 0 })}
        />
      </View>
      <View style={styles.buttonDelete}>
        <Button
          title="Delete Data"
          onPress={() => {
            setData([]);
          }}
        />
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  waterfall: {
    flex: 1,
  },
  contentContainer: {
    padding: 10,
  },
  item: {
    backgroundColor: "#ccc",
    margin: 5,
    padding: 10,
    borderRadius: 5,
  },
  header: {
    padding: 10,
    fontSize: 18,
    textAlign: "center",
  },
  footer: {
    padding: 10,
    fontSize: 16,
    textAlign: "center",
  },
  empty: {
    padding: 10,
    fontSize: 16,
    textAlign: "center",
  },
  buttonsContainer: {
    flexDirection: "row",
    justifyContent: "space-around",
    padding: 10,
  },
  buttonDelete: {
    marginBottom: 20,
  },
});

export default App;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.29; SDK: HarmonyOS NEXT Developer Beta6; IDE: DevEco Studio 5.0.3.706; ROM: NEXT.0.0.65;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
3. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
4. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                    | Description                                                                                                                                                                            | Type                  | Required | Platform | HarmonyOS Support |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------- | -------- | -------- | ----------------- |
| `renderItem`            | Used to render the current item into the list                                                                                                                                                           | function              | Yes      | All      | yes               |
| `data`                  | Waterfall flow data source, which can be an array of any type of content.                                                                                                                                                     | array                 | Yes      | All      | yes               |
| `numColumns`            | The number of columns in the waterfall flow, default is 2 (i.e., two columns).                                                                                                                                                         | number                | No       | All      | yes               |
| `ListHeaderComponent`   | Header component. Can be a React Component or a render function.                                                                                                                                      | component`, `function | No       | All      | yes               |
| `ListFooterComponent`   | Footer component. Can be a React Component or a render function.                                                                                                                                      | component`, `function | No       | All      | yes               |
| `ListEmptyComponent`    | Component to render when the list is empty. Can be a React Component or a render function.                                                                                                                            | component`, `function | No       | All      | yes               |
| `onEndReached`          | Called when the list is scrolled to the bottom.                                                                                                                                                                 | function              | No       | All      | yes               |
| `onRefresh`             | If this option is set, a standard[`RefreshControl`](https://www.react-native.cn/docs/refreshcontrol) component will be added to the list header to enable pull-to-refresh functionality. You must also set the refreshing property correctly. | function              | No       | All      | yes               |
| `refreshing`            | Set this property to true while waiting for new data to load, and the list will display a loading indicator.                                                                                                                | boolean               | No       | All      | yes               |
| `style`                 | Used to set the outer container style of the waterfall flow. By default, it has the style { flex: 1 }, meaning it fills the height of the parent container.                                                                                                                  | object                | No       | All      | yes               |
| `contentContainerStyle` | Waterfall flow content container style.                                                                                                                                                                     | object                | No       | All      | yes               |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                                                                                                                     | Type   | Required | Platform | HarmonyOS Support |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | ----------------- |
| `scrollToEnd([params])`    | Scroll to the bottom of the waterfall flow list.                                                                                                                          | object | No       | All      | yes               |
| `scrollToIndex([params])`  | Scrolls the element at the specified position to a defined location within the visible area. When viewPosition is 0, it scrolls to the top of the screen; when 1, it scrolls to the bottom of the screen; and when 0.5, it scrolls to the center of the screen. | object | Yes      | All      | yes               |
| `scrollToOffset([params])` | Scrolls the list to the specified offset (in pixels), equivalent to the scrollTo method of ScrollView.                                                                      | object | Yes      | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/axerjs/react-native-waterfall-flow/blob/HEAD/LICENSE).
