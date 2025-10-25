> Template version：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-swiper-flatlist</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gusgard/react-native-swiper-flatlist">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/gusgard/react-native-swiper-flatlist/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [GitHub address](https://github.com/gusgard/react-native-swiper-flatlist)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-swiper-flatlist@3.2.5
```

#### **yarn**

```bash
yarn add react-native-swiper-flatlist@3.2.5
```

<!-- tabs:end -->

### Example

The following code demonstrates a use case of this library:

> [!WARNING] The import name of the library remains the same when in use.

```javascript
import React from 'react';
import { Text, Dimensions, StyleSheet, View } from 'react-native';
import { SwiperFlatList } from 'react-native-swiper-flatlist';

const colors = ['tomato', 'thistle', 'skyblue', 'teal'];

const App = () => (
  <View style={styles.container}>
    <SwiperFlatList
      autoplay
      autoplayDelay={2}
      autoplayLoop
      index={2}
      showPagination
      data={colors}
      renderItem={({ item }) => (
        <View style={[styles.child, { backgroundColor: item }]}>
          <Text style={styles.text}>{item}</Text>
        </View>
      )}
    />
  </View>
);

const { width, height } = Dimensions.get('window');
const styles = StyleSheet.create({
    container: { backgroundColor: 'white', height: height * 0.7 },
    child: { width, justifyContent: 'center', height: height * 0.5 },
    text: { fontSize: width * 0.5, textAlign: 'center' },
});

export default App;
```

## Link

The HarmonyOS-side implementation of this library relies on the native code of @react-native-oh-tpl/react-native-safe-area-context and @react-native-oh-tpl/react-native-gesture-handler. If these libraries have already been introduced in your HarmonyOS project, there is no need to reintroduce them. You can skip the steps in this section and proceed directly to usage.

If you have not introduced react-native-safe-area-context, please refer to the [@react-native-oh-tpl/react-native-safe-area-context documentation](/en/react-native-safe-area-context.md) for installation instructions.

If you have not introduced react-native-gesture-handler, please refer to the [@react-native-oh-tpl/react-native-gesture-handler documentation](/en/react-native-gesture-handler.md) for installation instructions.


## Compatibility

This document is verified based on the following versions:

react-native-harmony：0.72.86; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

react-native-harmony：0.77.18; SDK：HarmonyOS 5.1.0.125; IDE：DevEco Studio 5.1.0.849; ROM：5.0.0.150;

## Props

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library.

> [!TIP] In the "HarmonyOS Support" column, `Yes` means the prop is supported on the HarmonyOS platform, `no` means it is not supported, and `partially` means it is partially supported. The usage is consistent across platforms, with the effect aiming to match the iOS or Android implementation.

### SwiperFlatList Props

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Data to use in renderItem | array | No | All | Yes |
| `children` | Children elements | node | No | All | Yes |
| `renderItem` | Takes an item from data and renders it into the list | FlatListProps<T>[renderItem] | No | All | Yes |
| `onMomentumScrollEnd` | Called after scroll end and the first parameter is the current index| (item: { index: number }, event: any) | No | All | Yes |
| `vertical` | Show vertical swiper | boolean | No | All | Yes |
| `index` | Index to start | number | No | All | Yes |
| `renderAll` | Edge/Corner's height. Default: 20 | boolean | No | All | Yes |
| `showPagination` | Showpagination | boolean | No | All | Yes |
| `onChangeIndex` | Executed every time the index change, the index change when the user reaches 60% of the next screen | ({ index: number, prevIndex: number}) => void | No | All | Yes |
| `PaginationComponent` | Overwrite Pagination component | node | No | All | Yes |
| `onViewableItemsChanged` | Native visible term changes in RN | FlatListProps<T>['onViewableItemsChanged'] | No | All | Yes |
| `autoplay` | Change index automatically | boolean | No | All | Yes |
| `autoplayDelay` | Delay between every page in seconds  | number | No | All | Yes |
| `autoplayLoop` | Continue playing after reach end | boolean | No | All | Yes |
| `autoplayLoopKeepAnimation` | Show animation when reach the end of the list | boolean | No | All | Yes |
| `autoplayInvertDirection` | Invert auto play direction | boolean | No | All | Yes |
| `disableGesture` | Disable swipe gesture | boolean | No | All | Yes |
| `e2eID` | TestID for automation testing | string | No | All | Yes |
| `viewabilityConfig` | TestID for automation testing | ViewabilityConfig | No | All | Yes |
| `useReactNativeGestureHandler` | Use react-native-gesture-handler FlatList instead of the native FlatList | boolean | No | All | Yes |
| `paginationAccessibilityLabels` | Accessibility labels for the pagination items.This is optional and used for screen readers. | string[] | No | All | No |

### SwiperFlatListWithGestureHandler Props
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `data` | Data to use in renderItem | array | No | All | Yes |
| `children` | Children elements | node | No | All | Yes |
| `renderItem` | Takes an item from data and renders it into the list | FlatListProps<T>[renderItem] | No | All | Yes |
| `onMomentumScrollEnd` | Called after scroll end and the first parameter is the current index| (item: { index: number }, event: any) | No | All | Yes |
| `vertical` | Show vertical swiper | boolean | No | All | Yes |
| `index` | Index to start | number | No | All | Yes |
| `renderAll` | Edge/Corner's height. Default: 20 | boolean | No | All | Yes |
| `showPagination` | Showpagination | boolean | No | All | Yes |
| `onChangeIndex` | Executed every time the index change, the index change when the user reaches 60% of the next screen | ({ index: number, prevIndex: number}) => void | No | All | Yes |
| `PaginationComponent` | Overwrite Pagination component | node | No | All | Yes |
| `onViewableItemsChanged` | Native visible term changes in RN | FlatListProps<T>['onViewableItemsChanged'] | No | All | Yes |
| `autoplay` | Change index automatically | boolean | No | All | Yes |
| `autoplayDelay` | Delay between every page in seconds  | number | No | All | Yes |
| `autoplayLoop` | Continue playing after reach end | boolean | No | All | Yes |
| `autoplayLoopKeepAnimation` | Show animation when reach the end of the list | boolean | No | All | Yes |
| `autoplayInvertDirection` | Invert auto play direction | boolean | No | All | Yes |
| `disableGesture` | Disable swipe gesture | boolean | No | All | Yes |
| `e2eID` | TestID for automation testing | string | No | All | Yes |
| `viewabilityConfig` | TestID for automation testing | ViewabilityConfig | No | All | Yes |
| `useReactNativeGestureHandler` | Use react-native-gesture-handler FlatList instead of the native FlatList | boolean | No | All | Yes |
| `paginationAccessibilityLabels` | Accessibility labels for the pagination items.This is optional and used for screen readers. | string[] | No | All | No |

### Pagination Props
> [!TIP] Pagination properties except 'paginationIndex' and 'size' SwiperFlatListWithGestureHandler and SwiperFlatList components can also be used.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `paginationDefaultColor` | Pagination Default color | string | No | All | Yes |
| `paginationActiveColor` | Pagination color | string | No | All | Yes |
| `paginationStyle` | Style object for the container | ViewStyle | No | All | Yes |
| `paginationStyleItem` | Style object for the item | ViewStyle | No | All | Yes |
| `paginationStyleItemActive` | Style object for the active item | ViewStyle | No | All | Yes |
| `paginationStyleItemInactive` | Style object for the inactive item | ViewStyle | No | All | Yes |
| `onPaginationSelectedIndex` | Executed when the user presses the pagination index, similar properties onChangeIndex | () => void | No | All | Yes |
| `size` | Size of pagination | number | Yes | All | Yes |
| `paginationIndex` | Selected pagination index | number | No | All | Yes |
| `e2eID` | TestID for automation testing | string | No | All | Yes |
| `paginationAccessibilityLabels` | Accessibility labels for the pagination items.This is optional and used for screen readers. | string[] | No | All | No |
| `paginationTapDisabled` | Prevents tapping pagination dots | boolean | No | All | Yes |

### SwiperFlatListWithGestureHandler Functions
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `scrollToIndex` | Scroll to the index | ({ item: ScrollToIndex}) => void | No | All | Yes |
| `getCurrentIndex` | Returns the current index | () => number | No | All | Yes |
| `getPrevIndex` | Returns the previous index | () => number | No | All | Yes |
| `goToFirstIndex` | Go to the first index | () => void | No | All | Yes |
| `goToLastIndex` | Go to the last index | () => void | No | All | Yes |

### SwiperFlatList Functions
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `scrollToIndex` | Scroll to the index | ({ item: ScrollToIndex}) => void | No | All | Yes |
| `getCurrentIndex` | Returns the current index | () => number | No | All | Yes |
| `getPrevIndex` | Returns the previous index | () => number | No | All | Yes |
| `goToFirstIndex` | Go to the first index | () => void | No | All | Yes |
| `goToLastIndex` | Go to the last index | () => void | No | All | Yes |

### Pagination Functions
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `scrollToIndex` | Scroll to the index | ({ index: number}) => void | Yes | All | Yes |

## Known Issues

## Others

paginationAccessibilityLabels: native platform test has no effect

## License
This project is licensed under [The MIT License (MIT)](https://github.com/gusgard/react-native-swiper-flatlist/blob/master/LICENSE).