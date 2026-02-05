> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@shopify/flash-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Shopify/flash-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Shopify/flash-list/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" /> 
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/flash-list)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Name | Version   | Release Information                                                                         | Supported RN Version | Supported Autolink | Compile API Version | Community Baseline Version | npm Address                      
| ------------ |--------|---------------------------------------------------------------------------------------------|----------------------|--------------------|---------|--------|----------------------------------|
|@react-native-ohos/flash-list| ~2.1.1 | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_flash-list/releases) | 0.82.*                | 否                  | API12+  | 2.1.0  | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/flash-list)|
|@react-native-ohos/flash-list| ~1.8.3 | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_flash-list/releases) | 0.77.*               | 否                  | API12+  | 1.8.2  | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/flash-list)|
|@react-native-ohos/flash-list| ~1.6.4 | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_flash-list/releases) | 0.72.*               | 否                  | API12+  | 1.6.3  | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/flash-list) |
|@react-native-oh-tpl/flash-list| 1.6.3-0.2.9@deprecated  | [Github Releases](https://github.com/react-native-oh-library/flash-list/releases) | 0.72       | 否                  | API12+  | 1.6.3  | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/flash-list) |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install @react-native-ohos/flash-list
```

#### **yarn**

```bash
yarn add @react-native-ohos/flash-list
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View, Text } from "react-native";
import { FlashList } from "@shopify/flash-list";

const DATA = [
  {
    title: "First Item",
  },
  {
    title: "Second Item",
  },
];

const MyList = () => {
  return (
    <FlashList
      data={DATA}
      renderItem={({ item }) => <Text>{item.title}</Text>}
    />
  );
};
```

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~2.1.1                               |  No              |  0.82     |
| ~1.8.3                               |  No                   |  0.77                |
| ~1.6.4                              |  Yes                  |  0.72                |
| <= 1.6.3-0.2.9@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.77.86" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2. Introducing Native Code

> [!TIP] version>=v2.1.1 does not involve native code and this step can be skipped.

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/flash-list": "file:../../node_modules/@react-native-ohos/flash-list/harmony/flash_list.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing FlashListPackage

> If you are using version <= 1.6.3-0.2.9, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/flash-list/src/main/cpp" ./flash-list)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_flash_list)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "FlashListPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<FlashListPackage>(ctx)
    };
}
```

</details>

## Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM:6.0.0.130 SP8;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| contentContainerStyle<sup>deprecated  from 2.1.1</sup>                  | You can use contentContainerStyle to apply padding that will be applied to the whole content itself.                                                                                                                                                           | ContentStyle        | No       | All      | Yes                |
| estimatedListSize<sup>deprecated  from 2.1.1</sup>                      | Estimated visible height and width of the list. It is not the scroll content size. Defining this prop will enable the list to be rendered immediately. Without it, the list first needs to measure its size, leading to a small delay during the first render. | object              | No       | All      | Yes                |
| horizontal                             | If true, renders items next to each other horizontally instead of stacked vertically. Default is false.                                                                                                                                                        | boolean             | No       | All      | Yes |
| keyExtractor                           | Used to extract a unique key for a given item at the specified index. Key is used for optimizing performance.                                                                                                                                                  | function            | No       | All      | Yes                |
| numColumns                             | Multiple columns can only be rendered with horizontal={false} and will zig-zag like a flexWrap layout. Items should all be the same height - masonry layouts are not supported.                                                                                | number              | No       | All      | Yes                |
| extraData                              | A marker property for telling the list to re-render (since it implements PureComponent)                                                                                                                                                                        | any                 | No       | All      | Yes                |
| drawDistance                           | Draw distance for advanced rendering (in dp/px).                                                                                                                                                                                                               | number              | No       | All      | Yes                |
| estimatedItemSize<sup>deprecated  from 2.1.1</sup>                      | estimatedItemSize is a single numeric value that hints FlashList about the approximate size of the items before they're rendered.                                                                                                                              | number              | No       | All      | Yes                |
| viewabilityConfig                      | viewabilityConfig is a default configuration for determining whether items are viewable.                                                                                                                                                                       | object              | No       | All      | Yes                |
| renderItem<sup>changed in 2.1.1</sup>                             | Takes an item from data and renders it into the list. In v2, the `Measurement` value in the `target` parameter is deprecated.                                                                                                                                                                                                          | function            | Yes      | All      | Yes                |
| data                                   | For simplicity, data is a plain array of items of a given type.                                                                                                                                                                                                | ItemT[]             | Yes      | All      | Yes                |
| CellRendererComponent                  | Each cell is rendered using this element. Can be a React Component Class, or a render function                                                                                                                                                                 | JXS Element         | No       | All      | Yes                |
| ListFooterComponent                    | Rendered at the bottom of all the items                                                                                                                                                                                                                        | JXS Element         | No       | All      | Yes                |
| ListHeaderComponent                    | Rendered at the top of all the items                                                                                                                                                                                                                           | JXS Element         | No       | All      | Yes                |
| refreshControl                         | A custom refresh control element.                                                                                                                                                                                                                              | JXS Element         | No       | All      | Yes                |
| renderScrollComponent                  | Rendered as the main scrollview.                                                                                                                                                                                                                               | JXS Element         | No       | All      | Yes                |
| onEndReached                           | Called once when the scroll position gets within onEndReachedThreshold of the rendered content.                                                                                                                                                                | callback            | No       | All      | Yes                |
| onEndReachedThreshold                  | How far from the end (in units of visible length of the list) the bottom edge of the list must be from the end of the content to trigger the onEndReached callback                                                                                             | number              | No       | All      | Yes                |
| onViewableItemsChanged                 | Called when the viewability of rows changes, as defined by the viewabilityConfig prop.                                                                                                                                                                         | callback            | No       | All      | Yes                |
| getItemType                            | Allows developers to specify item types.                                                                                                                                                                                                                       | function            | No       | All      | Yes                |
| overrideItemLayout<sup>changed in 2.1.1</sup>                     | Used to change item column span. In v1, supports both `layout.span` and `layout.size`; in v2, only `layout.span` is supported, size estimates are no longer read.                                                                                                                                                                   | function            | No       | All      | Yes                |
| ItemSeparatorComponent                 | Rendered in between each item, but not at the top or bottom.                                                                                                                                                                                                   | JXS Element         | No       | All      | Yes                |
| ListEmptyComponent                     | Rendered when the list is empty                                                                                                                                                                                                                                | JXS Element         | No       | All      |Yes               |
| ListFooterComponentStyle               | Styling for internal View for ListFooterComponent.                                                                                                                                                                                                             | React.ComponentType | No       | All      | Yes                |
| ListHeaderComponentStyle               | Styling for internal View for ListHeaderComponent.                                                                                                                                                                                                             | StyleProp           | No       | All      | Yes                |
| disableAutoLayout<sup>deprecated  from 2.1.1</sup>                      | FlashList applies some fixes to layouts of its children which can conflict with custom CellRendererComponent implementations. You can disable this behavior by setting this to true.                                                                           | boolean             | No       | All      | Yes                |
| disableHorizontalListHeightMeasurement<sup>deprecated  from 2.1.1</sup> | When set to true the list's rendered size needs to be deterministic (i.e., height and width greater than 0) as FlashList will skip rendering the extra item for measurement. Default value is false.                                                           | boolean             | No       | All      | Yes                |
| estimatedFirstItemOffset<sup>deprecated  from 2.1.1</sup>               | estimatedFirstItemOffset specifies how far the first item is drawn from start of the list window or offset of the first item of the list (not the header).                                                                                                     | number              | No       | All      | Yes               |
| initialScrollIndex                     | Instead of starting at the top with the first item, start at initialScrollIndex                                                                                                                                                                                | number              | No       | All      | Yes               |
| inverted<sup>deprecated  from 2.1.1</sup>                               | Reverses the direction of scroll. Uses scale transforms of -1.                                                                                                                                                                                                 | boolean             | No       | All      | Yes                |
| onBlankArea<sup>deprecated  from 2.1.1</sup>                            | FlashList computes blank space that is visible to the user during scrolling or the initial loading of the list.                                                                                                                                                | callback            | No       | All      | Yes                 |
| onLoad                                 | This event is raised once the list has drawn items on the screen.                                                                                                                                                                                              | callback            | No       | All      | Yes               |
| onRefresh                              | If provided, a standard RefreshControl will be added for "Pull to Refresh" functionality. Make sure to also set the refreshing prop correctly.                                                                                                                 | callback            | No       | All      | Yes                |
| onScroll                               | Fires at most once per frame during scrolling. Inherited from ScrollView.           | callback            | No       | All      | Yes                |
| overrideProps                          | We do not recommend using this prop for anything else than debugging. Internal props of the list will be overriden with the provided values.                                                                                                                   | object              | No       | All      | Yes               |
| progressViewOffset                     | Set this when offset is needed for the loading indicator to show correctly.                                                                                                                                                                                    | number              | No       | Android       | Yes                |
| refreshing                             | Set this true while waiting for new data from a refresh.                                                                                                                                                                                                       | boolean             | No       | All      | Yes                 |
| viewabilityConfigCallbackPairs         | List of ViewabilityConfig/onViewableItemsChanged pairs. A specific onViewableItemsChanged will be called when its corresponding ViewabilityConfig's conditions are met.                                                                                        | object              | No       | All      | Yes                 |
| ContentStyle<sup>deprecated  from 2.1.1</sup> | Type for defining the style of the list content container | object | No | All | Yes |
| CellContainer<sup>deprecated  from 2.1.1</sup> | Cell container component | React.Component | No | All | Yes |
| useOnNativeBlankAreaEvents<sup>deprecated  from 2.1.1</sup> | Hook for listening to native blank area events, triggers callback when blank areas appear in the list | function | No | All | Yes |
| BlankAreaEventHandler<sup>deprecated  from 2.1.1</sup> | Type for blank area event handler function | function | No | All | Yes |
| BlankAreaEvent<sup>deprecated  from 2.1.1</sup> | Blank area event object | object | No | All | Yes |
| useBlankAreaTracker<sup>deprecated  from 2.1.1</sup> | Hook for tracking visible blank areas in the list for production environments | function | No | All | Yes |
| BlankAreaTrackerResult<sup>deprecated  from 2.1.1</sup> | Blank area tracker result object | object | No | All | Yes |
| BlankAreaTrackerConfig<sup>deprecated  from 2.1.1</sup> | Configuration options for the blank area tracker | object | No | All | Yes |
| MasonryFlashList<sup>deprecated  from 2.1.1</sup> | Masonry (waterfall) layout variant of FlashList component | React.Component | No | All | Yes |
| MasonryFlashListProps<sup>deprecated  from 2.1.1</sup> | Props type for the masonry list component | object | No | All | Yes |
| MasonryFlashlistScrollEvent<sup>deprecated  from 2.1.1</sup> | Scroll event type for masonry list | object | No | All | Yes |
| MasonryFlashListRef<sup>deprecated  from 2.1.1</sup> | Ref type for masonry list | object | No | All | Yes |
| MasonryListItem<sup>deprecated  from 2.1.1</sup> | Wrapper type for masonry list item | object | No | All | Yes |
| MasonryListRenderItem<sup>deprecated  from 2.1.1</sup> | Render function type for masonry list item | function | No | All | Yes |
| MasonryListRenderItemInfo<sup>deprecated  from 2.1.1</sup> | Render info for masonry list item | object | No | All | Yes |
| FlashListRef <sup>2.1.1</sup>| Provides a reference to the FlashList instance, enabling direct list manipulation. | React.RefObject<FlashList<T>> | No | All | Yes |
| onStartReached<sup>2.1.1</sup>| Callback triggered once when the scroll position gets close to the content start position. | callback | No | All | Yes |
| onStartReachedThreshold<sup>2.1.1</sup>| Threshold distance between the top edge of the list and the content start position (in units of visible length of the list) when triggering the onStartReached callback. | number | No | All | Yes |
| maintainVisibleContentPosition<sup>2.1.1</sup>| Configuration for maintaining scroll position when content changes. Supports configuring sub-properties like `disabled`, `autoscrollToTopThreshold`, `autoscrollToBottomThreshold`, `animateAutoScrollToBottom`, and `startRenderingFromBottom`. | object | No | All | Yes |
| masonry<sup>2.1.1</sup>| Enable masonry (waterfall) layout mode. | boolean | No | All | Yes |
| maxItemsInRecyclePool<sup>2.1.1</sup>| Maximum number of items cached in the recycle pool. Items are cached in the recycle pool when scrolled off-screen. Setting to 0 will disable the recycle pool, and items will be unmounted directly after scrolling off-screen. | number | No | All | Yes |
| onCommitLayoutEffect<sup>2.1.1</sup>| Callback invoked when layout commit is complete. | function | No | All | Yes |
| LayoutCommitObserver<sup>2.1.1</sup>| Component for observing when FlashList commits layout. | React.Component | No | All | Yes |
| LayoutCommitObserverProps<sup>2.1.1</sup>| Define the properties of LayoutCommitObserver, including the callback function. | object | No | All | Yes |
| initialScrollIndexParams<sup>2.1.1</sup>| Additional configuration for `initialScrollIndex`. Use `viewOffset` to apply an offset to the initial scroll position. Only takes effect when `initialScrollIndex` is set. | object | No | All | Yes |
| optimizeItemArrangement<sup>2.1.1</sup>| When enabled, MasonryFlashList will reduce column height differences by adjusting item order. Only available in masonry layout mode. | boolean | No | All | Yes |
| style<sup>2.1.1</sup>| Style for the RecyclerView parent container. | StyleProp<ViewStyle> | No | All | Yes |
| props2.1.1 | Get access to current props. | RecyclerViewProps<T> | No | All | Yes |

## HOOKS

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| useLayoutState<sup>2.1.1</sup>| A custom Hook that combines state management with RecyclerView layout updates. State changes automatically trigger layout recalculation. Returns the current state value and a setter function that optionally skips parent layout updates. | Hook | No | All | Yes |
| useRecyclingState<sup>2.1.1</sup>| A state management Hook with automatic reset functionality. Similar to useState, but automatically resets state when specified dependencies change. Useful for scenarios where state needs to be reset during item recycling, avoiding extra setState calls and improving performance. | Hook | No | All | Yes |
| useMappingHelper<sup>2.1.1</sup>| Returns a helper function for creating mapping keys. Used when performing .map operations on items to create component lists. | Hook | No | All | Yes |
| useFlashListContext<sup>2.1.1</sup>| Hook for accessing the current FlashList context. Provides access to methods like `layout()`, `getRef()`, `getParentRef()`, `getScrollViewRef()`, and `getParentScrollViewRef()`. | Hook | No | All | Yes |

## Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| prepareForLayoutAnimationRender | Run this method before running layout animations, such as when animating an element when deleting it.                                                         | function | No       | All      | Yes               |
| recordInteraction               | Tells the list an interaction has occurred, which should trigger viewability calculations, e.g. if waitForInteractions is true and the user has not scrolled. | function | No       | All      | Yes              |
| scrollToEnd                     | Scrolls to the end of the content.                                                                                                                            | function | No       | All      | Yes               |
| scrollToIndex                   | Scroll to a given index.                                                                                                                                      | function | No       | All      | Yes               |
| scrollToItem                    | Scroll to a given item.                                                                                                                                       | function | No       | All      | Yes              |
| scrollToOffset                  | Scroll to a specific content pixel offset in the list.                                                                                                        | function | No       | All      | Yes              |
| recomputeViewableItems<sup>1.8.3 2.1.1</sup> | Retriggers viewability calculations. Useful to imperatively trigger viewability calculations. | function | No | All | Yes |
| getLayout | Gets layout information for the item at the specified index, including x, y coordinates and dimensions. Returns an RVLayout object. | function | No | All | Yes |
| getChildContainerDimensions | Returns the dimensions of the child container, containing `width` and `height` properties. | function | No | All | Yes |
| getScrollableNode | Returns the underlying scrollable node. | function | No | All | Yes |
| getFirstItemOffset | Returns the offset of the first item (including header/padding). | function | No | All | Yes |
| getWindowSize | Returns the current viewport dimensions, containing `width` and `height` properties. | function | No | All | Yes |
| getFirstVisibleIndex | Returns the index of the first visible item. | function | No | All | Yes |
| getAbsoluteLastScrollOffset | Returns the absolute offset of the last scroll. | function | No | All | Yes |
| clearLayoutCacheOnUpdate | Clears the layout cache on update. | function | No | All | Yes |
| computeVisibleIndices<sup>2.1.1</sup> | Returns the index range of currently visible items, containing `startIndex` and `endIndex` properties. | function | No | All | Yes |
| flashScrollIndicators<sup>2.1.1</sup> | Briefly flashes the scroll indicators. | function | No | All | Yes |
| getNativeScrollRef<sup>2.1.1</sup> | Returns the underlying native scroll view reference. | function | No | All | Yes |
| getScrollResponder<sup>2.1.1</sup> | Returns the scroll responder reference. | function | No | All | Yes |
| scrollToTop<sup>2.1.1</sup> | Scrolls to the top (or start position) of the list. Supports the `animated` parameter to control whether to use animation. | function | No | All | Yes |

## Known Issues

- [ ] RNOH's `maintainVisibleContentPosition` implementation does not account for FlashList's element recycling mechanism, causing list scrolling jumps.[Issue#19](https://gitcode.com/openharmony-sig/rntpc_flash-list/issues/19)
## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/Shopify/flash-list/blob/main/LICENSE.md).