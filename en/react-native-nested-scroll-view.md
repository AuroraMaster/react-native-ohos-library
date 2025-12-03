> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-nested-scroll-view</code> </h1>
</p>

Please visit the Release release address of the third-party library to view the corresponding version information:

| Version                        | Package Name                             | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -----------
| 9.0.0 | @react-native-oh-tpl/react-native-nested-scroll-view  | [Github](https://github.com/react-native-oh-library/react-native-nested-scroll-view) | [Github Releases](https://github.com/react-native-oh-library/react-native-nested-scroll-view/releases) | 0.72  |
| 9.1.0 | @react-native-ohos/react-native-nested-scroll-view  | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-nested-scroll-view) | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-nested-scroll-view/releases) | 0.77  |

## Installation and Usage

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-nested-scroll-view
# 0.77
npm install @react-native-ohos/react-native-nested-scroll-view
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-nested-scroll-view
# 0.77
yarn add @react-native-ohos/react-native-nested-scroll-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { View, ScrollView, Text, StyleSheet } from 'react-native';
import NestedScrollView from 'react-native-nested-scroll-view';

const NestedScrollViewExample = () => {
  return (
    <NestedScrollView style={{ flex: 1 }}>
      <ScrollView contentContainerStyle={styles.scrollViewContent}>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map((item) => (
          <View key={item} style={styles.itemContainer}>
            <Text style={styles.itemTitle}>Item {item}</Text>
            <ScrollView horizontal showsHorizontalScrollIndicator={false}>
              {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map((subItem) => (
                <View key={subItem} style={styles.subItem}>
                  <Text>content {subItem}</Text>
                </View>
              ))}
            </ScrollView>
          </View>
        ))}
      </ScrollView>
    </NestedScrollView>
  );
};

const styles = StyleSheet.create({
  scrollViewContent: {
    paddingVertical: 20,
    paddingHorizontal: 10,
  },
  itemContainer: {
    marginBottom: 20,
    padding: 10,
    backgroundColor: '#f0f0f0',
    borderRadius: 10,
  },
  itemTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  subItem: {
    width: 100,
    height: 100,
    backgroundColor: '#b0e0e6',
    justifyContent: 'center',
    alignItems: 'center',
    marginHorizontal: 5,
  },
});

export default NestedScrollViewExample;
```

### Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

This document is verified based on the following versions:
1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Canary3 SP2; IDE: DevEco Studio: 5.0.3.300; ROM：3.0.0.22(Canary3);
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;

## Properties 

Android's ScrollView does not support nested scrolling like iOS's ScrollView. When using the native ScrollView directly to implement nested scrolling in React Native, there may be some scrolling issues, such as unsmooth nested scrolling or incorrect response to scrolling events. Therefore, Android uses react native nested scroll view to solve the problem of nested scrolling; IOS uses the ScrollView in React Native to implement nested scrolling, while HarmonyOS remains consistent with iOS and accepts all [React Native ScrollViews](https://reactnative.dev/docs/scrollview#props)Props of components

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| contentContainerStyle  | Set the style of the scroll view content container.  | ViewStyleProp  | no       | Android/IOS  | yes                |
| disableIntervalMomentum  | If true, the scroll view will stop at the next index regardless of how fast the gesture is (relative to the scroll position at release) | boolean | no | Android/IOS | yes  |
| decelerationRate  | Set the scroll deceleration rate. | ('fast' or 'normal' or number)  | no | Android/IOS  | yes  |
| horizontal  | Specifies whether the scroll view is horizontal, default is vertical. | boolean  | no   | Android/IOS  | yes                |
| invertStickyHeaders  | Whether sticky headers should stick to the bottom of the ScrollView instead of the top. | boolean  | no       | Android/IOS  | yes                |
| keyboardDismissMode  | Set keyboard dismiss mode, optional values are "none", "interactive" and "on-drag" | string  | no       | Android/IOS  | yes                |
| keyboardShouldPersistTaps  | Set whether the keyboard disappears when clicking outside the input box. Optional values are "never", "always" and "handled" | ('always' or 'never' or 'handled' or true or false)  | no | Android/IOS  | yes |
| onMomentumScrollBegin  | Callback function triggered when starting inertial scrolling | (event: ScrollEvent) => void  | no   | Android/IOS  | yes    |
| onMomentumScrollEnd  | Callback function triggered when ending inertial scrolling | (event: ScrollEvent) => void  | no       | Android/IOS  | yes                |
| onScroll  | Callback function triggered when scrolling   | (event: ScrollEvent) => void  | no       | Android/IOS  | yes                |
| onScrollBeginDrag  | Callback function triggered when starting to drag the scroll view | (event: ScrollEvent) => void  | no       | Android/IOS  | yes                |
| onScrollEndDrag  | Callback function triggered when ending dragging the scroll view  | (event: ScrollEvent) => void  | no       | Android/IOS  | yes                |
| onContentSizeChange  | Called when the scrollable content view of ScrollView changes. The handler passes content width and content height as parameters   | (contentWidth: number, contentHeight: number) => void  | no       | Android/IOS  | yes                |
| pagingEnabled  | When the value is true, the scroll bar will stop at integer multiples of the scroll view size  | boolean  | no | Android/IOS | yes               |
| scrollEnabled  | When the value is false, the content cannot scroll, the default value is true  | boolean | no | Android/IOS | yes               |
| showsVerticalScrollIndicator  | When this property is true, a vertical scroll bar is displayed | boolean  | no | Android/IOS | yes               |
| stickyHeaderIndices  | An array of sub-view indices used to determine which members will be fixed at the top of the screen after scrolling   | $ReadOnlyArray<number>  | no | Android/IOS | yes               |
| snapToInterval  | When this property is set, the scroll view will stop at multiples of snapToInterval after scrolling stops   | number  | no | Android/IOS | yes               |
| snapToOffsets  | Will cause the scroll view to stop at defined offsets. This can be used to page children of various sizes smaller than the scroll view  | $ReadOnlyArray<number>  | no | Android/IOS | yes               |
| snapToStart  | Used in conjunction with snapToOffsets. By default, the beginning of the list counts as a snap offset.   | boolean  | no | Android/IOS | yes               |
| snapToEnd  | Used in conjunction with snapToOffsets. By default, the end of the list counts as a snap offset         | boolean  | no | Android/IOS | yes               |
| removeClippedSubviews  | When this property is true, subviews outside the screen (the overflow style of subviews needs to be set to hidden) will be removed         | boolean  | no | Android/IOS | yes               |
| refreshControl  | Used to provide pull-to-refresh functionality for ScrollView. Can only be used for vertical views, i.e. horizontal cannot be true | React.Element<any>  | no | Android/IOS | yes               |


## API

Android's ScrollView does not support nested scrolling like iOS's ScrollView. When implementing nested scrolling directly with the native ScrollView in React Native, some scrolling issues will occur, such as unsmooth nested scrolling or inability to correctly respond to scrolling events. Therefore, Android uses react-native-nested-scroll-view to solve the nested scrolling problem; iOS uses the ScrollView in React Native to implement nested scrolling, and HarmonyOS is consistent with iOS, accepting all Methods of the [React Native ScrollView](https://reactnative.dev/docs/scrollview#methods) component

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| scrollTo  | This method is used to scroll to a specified position. The offset can be specified by the x and y parameters, and the animated parameter is used to specify whether to use animation effects. | function  | no       | Android/IOS  | yes        |
| scrollToEnd  | This method is used to scroll to the end of the content. The animated parameter can be used to specify whether to use animation effects. | function  | no       | Android/IOS  | yes                |
| flashScrollIndicators  | This method is used to display scroll indicators, typically used when you need to remind users that they can scroll. | function  | no       | Android/IOS  | yes                |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/cesardeazevedo/react-native-nested-scroll-view/blob/master/LICENSE).
