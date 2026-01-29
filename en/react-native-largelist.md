> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-largelist</code> </h1>
</p>

Please visit the Release release address of the third-party library to view the corresponding version information:
| Name | Version | Release Information | Supported RN Version | Supported Autolink | Compile API Version | Community Baseline Version | npm Address     |
| --------------| -------------- | ------------------------------ | ------------- | ------------- |------------------------ | ------------- | ------------- |
| @react-native-ohos/react-native-largelist | 3.2.0    | [Gitcode](https://gitcode.com/openharmony-sig/rntpc_react-native-largelist) | 0.77/0.82 | no | API12+ | 3.1.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-largelist?activeTab=versions) | 
| @react-native-oh-tpl/react-native-largelist | 3.1.1    | [Github](https://github.com/react-native-oh-library/react-native-largelist) | 0.72 | yes | API12+ | 3.1.0 | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/react-native-largelist?activeTab=versions) | 



## Installation and Usage


Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-largelist
# 0.77
npm install @react-native-ohos/react-native-largelist
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-largelist
# 0.77
yarn add @react-native-ohos/react-native-largelist
```
<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
// Largelist
import React from "react";
import { StyleSheet, Text, View } from "react-native";
import { LargeList } from "react-native-largelist";

export class HeightEqualExample extends React.Component {
  _sectionCount = 10;
  _rowCount = 10;

  render() {
    const data = [];
    for (let section = 0; section < this._sectionCount; ++section) {
      const sContent = { items: [] };
      for (let row = 0; row < this._rowCount; ++row) {
        sContent.items.push(row);
      }
      data.push(sContent);
    }
    return (
      <LargeList
        style={styles.container}
        data={data}
        heightForSection={() => 50}
        renderSection={this._renderSection}
        heightForIndexPath={() => 50}
        renderIndexPath={this._renderIndexPath}
      />
    );
  }

  _renderSection = (section: number) => {
    return (
      <View style={styles.section}>
        <Text>
          Section {section}
        </Text>
      </View>
    );
  };

  _renderIndexPath = ({ section: section, row: row }) => {
    return (
      <View style={styles.row}>
        <Text>
          Section {section} Row {row}
        </Text>
        <View style={styles.line} />
      </View>
    );
  };
}

const styles = StyleSheet.create({
  container: {
    flex: 1
  },
  section: {
    flex: 1,
    backgroundColor: "gray",
    justifyContent: "center",
    alignItems: "center"
  },
  row: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center"
  },
  line: {
    position: "absolute",
    left: 0,
    right: 0,
    bottom: 0,
    height: 1,
    backgroundColor: "#EEE"
  }
});
```

For more examples, see [largelistExample](https://github.com/bolan9999/react-native-largelist/tree/master/Examples)

## Link

The implementation of this library depends on the native code of @react-native-ohos/react-native-spring-scrollview . If you have already included this library in your HarmonyOS project, you do not need to include it again. You can skip this section and  use the library directly.

If you have not included it, please refer to the [Linking section of the @react-native-ohos/react-native-spring-scrollview ](/zh-cn/react-native-spring-scrollview.md#link)

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
1. RNOH：0.72.79; SDK：HarmonyOS 5.0.0 Release SDK; IDE: DevEco Studio 5.0.7.210; ROM：5.0.0.135;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;
3. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM:6.0.0.120 SP7
## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Largelist:
| Name                           | Description                                                                                                                                                                                                                           | Type                                                                                                          | Required | Platform    | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| bounces                        | Whether the list can bounce elastically when scrolling beyond the content view (iOS & Android: if true, horizontal content view will not have elasticity unless it exceeds SpringScrollView, vertical direction always has elasticity)                                                                                 | boolean                                                                                                       | no       | Android/iOS | yes               |
| scrollEnabled                  | Whether scrolling is enabled                                                                                                                                                                                                          | boolean                                                                                                       | no       | Android/iOS | yes               |
| initialContentOffset           | Initial offset, only valid on first initialization, later changes are invalid (x direction is supported)                                                                                                                                                                           | {x:number, y:number}                                                                                          | no       | Android/iOS | yes               |
| showsVerticalScrollIndicator   | Show vertical scroll indicator                                                                                                                                                                                                    | boolean                                                                                                       | no       | Android/iOS | no               |
| showsHorizontalScrollIndicator | Show horizontal scroll indicator (only useful when content view exceeds LargeList viewport)                                                                                                                                                                                 | boolean                                                                                                       | no       | Android/iOS | no               |
| tapToHideKeyboard              | Whether to hide the keyboard when tapping LargeList                                                                                                                                                                                                             | boolean                                                                                                       | no       | Android/iOS | yes(rely on springscrollview 2.x version) |
| data                           | Data source for the list                                                                                                                                                                                                          | { items: any[] }[]                                                                                            | no       | Android/iOS | yes               |
| heightForSection               | Function that returns the height of each section header                                                                                                                                                                                                          | (section: number) => number                                                                                   | no       | Android/iOS | yes               |
| renderSection                  | Render function for each section header                                                                                                                                                                                                                | `(section: number) => React.ReactElement <any>`                                                               | no       | Android/iOS | yes               |
| heightForIndexPath             | Function that returns the height of each row in the list                                                                                                                                                                                                              | (indexPath: IndexPath) => number                                                                              | no       | Android/iOS | yes               |
| renderIndexPath                | Render function for each row, mediaWrapperParam is used for optimization options for large images or videos.                                                                                                                                                                     | `(indexPath: IndexPath, mediaWrapperParam:Object) => React.ReactElement <any>`                                | no       | Android/iOS | yes               |
| renderHeader                   | Header component function for the list                                                                                                                                                                                                                    | `()=> React.ReactElement <any>`                                                                               | no       | Android/iOS | yes               |
| renderFooter                   | Footer component function for the list                                                                                                                                                                                                                    | `()=> React.ReactElement <any>`                                                                               | no       | Android/iOS | yes               |
| inverted                       | Reverse scroll direction, suitable for chat apps                                                                                                                                                                                                             | boolean                                                                                                       | no       | Android/iOS | yes               |
| onRefresh                      | Callback function for pull-to-refresh, if set, a refresh header will be added to the top                                                                                                                                                                       | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| refreshHeader                  | Select the pull-to-refresh component. If the user does not want to customize, they can use NormalHeader directly. If deep customization is needed                                                                                                                                     | [RefreshHeader](https://github.com/bolan9999/react-native-spring-scrollview/blob/master/src/RefreshHeader.js) | no       | Android/iOS | yes               |
| onLoading                      | Callback function for pull-to-load, if set, a loading component will be added to the bottom                                                                                                                                                                         | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| allLoaded                      | Whether data loading is complete.                                                                                                                                                                                                    | boolean                                                                                                       | no       | Android/iOS | yes               |
| loadingFooter                  | Pull-to-load component. If the user does not want to customize, they can use NormalFooter. If deep customization is needed                                                                                                                                                         | [LoadingFooter](https://github.com/bolan9999/react-native-spring-scrollview/blob/master/src/LoadingFooter.js) | no       | Android/iOS | yes               |
| onScroll                       | Listen to list scrolling (JavaScript side)                                                                                                                                                                                                          | ({nativeEvent:{contentOffset:{x, y}}})=>any                                                                   | no       | Android/iOS | yes               |
| onNativeContentOffsetExtract   | Listen to scroll offset using native animation values, can be used for interpolation animation                                                                                                                                                                                          | {x?:Animated.Value, y?:Animated.Value}                                                                        | no       | Android/iOS | yes               |
| onTouchBegin                   | Callback when finger touches down                                                                                                                                                                                                        | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| onTouchEnd                     | Callback when finger lifts up                                                                                                                                                                                                        | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| onMomentumScrollBegin          | Callback when deceleration starts after releasing                                                                                                                                                                                                                  | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| onMomentumScrollEnd            | Callback when deceleration ends                                                                                                                                                                                                          | ()=>any                                                                                                       | no       | Android/iOS | yes               |
| textInputRefs                  | Pass TextInput references to let SpringScrollView automatically manage keyboard blocking issues.                                                                                                                                                                       | TextInput[]                                                                                                   | no       | Android/iOS | yes               |
| dragToHideKeyboard             | Whether to hide the keyboard when dragging the screen                                                                                                                                                                                                                | boolean                                                                                                       | no       | Android/iOS | yes(rely on springscrollview 3.x version) |
| inputToolBarHeight             | On different systems and different third-party input methods, the keyboard toolbar height is uncertain, and there is no official way to get the toolbar height. This property is used to allow users to slightly adjust the component offset position when the keyboard pops up                                                                                  | number                                                                                                        | no       | Android/iOS | yes               |
| groupCount                     | Optimization parameter. LargeList groups rows (not sections, independent groups). groupCount indicates rendering 4 groups total, each group renders at least groupMinHeight height. Larger values mean more pre-rendered rows, slower initialization. Note: groupCount * groupMinHeight must be greater than LargeList viewport height. | number                                                                                                        | no       | Android/iOS | yes               |
| groupMinHeight                 | Optimization parameter, height of each group                                                                                                                                                                                                                  | number                                                                                                        | no       | Android/iOS | yes               |
| updateTimeInterval             | Update delay. Smaller values mean higher update frequency, but React Native is asynchronous - too many updates may cause lag. Larger values make it easier for users to see new items replacing old items.                                                                                        | number                                                                                                        | no       | Android/iOS | yes               |


### WaterfallList:
| Name              | Description                                                                                                                                                                                       | Type                                                | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------- | -------- | ----------- | ----------------- |
| data              | Data source, the number of arrays determines the number of items                                                                                                                                                                | any[]                                               | no       | Android/iOS | yes               |
| heightForItem     | A height function to return the height of each item                                                                                                                                                              | (item:any,index:number)=> number                    | no       | Android/iOS | yes               |
| renderItem        | Render function for each item                                                                                                                                                                              | `(item:any,index:number)=> React.ReactElement<any>` | no       | Android/iOS | yes               |
| preferColumnWidth | Ideal width of each item. It affects the actual number of columns. Actual columns = WaterfallList width / ideal width (floor). Actual width = component width / actual columns (currently only supports equal-width items). (At least one of preferColumnWidth and numColumns must be specified.) | number                                              | no       | Android/iOS | yes               |
| numColumns        | Fixed number of columns. (At least one of preferColumnWidth and numColumns must be specified.)                                                                                                                                    | number                                              | no       | Android/iOS | yes               |
| renderHeader      | Header component function                                                                                                                                                                                      | `()=> React.ReactElement <any>	`                    | no       | Android/iOS | yes               |
| renderFooter      | Footer component function                                                                                                                                                                                      | `()=> React.ReactElement <any>	`                    | no       | Android/iOS | yes               |


### StickyForm:
| Name                   | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| ...LargeList           | Support all LargeList properties (including refresh and loading).                    | -       | no       | Android/iOS | yes               |
| directionalLockEnabled | When this property is true, it will try to lock scrolling to only horizontal or vertical direction. | boolean | no       | Android/iOS | no               |
| headerStickyEnabled    | Stick the header to the top of StickyForm, with the Section sticking below the header.       | boolean | no       | Android/iOS | no               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bolan9999/react-native-largelist/blob/master/LICENSE).
