> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-swipe-list-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jemise111/react-native-swipe-list-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jemise111/react-native-swipe-list-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-swipe-list-view)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-swipe-list-view Releases](https://github.com/react-native-oh-library/react-native-swipe-list-view/releases/).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install --save @react-native-oh-tpl/react-native-swipe-list-view
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-swipe-list-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import { SwipeListView } from 'react-native-swipe-list-view';

//... note: your data array objects MUST contain a key property
//          or you must pass a keyExtractor to the SwipeListView to ensure proper functionality
//          see: https://reactnative.dev/docs/flatlist#keyextractor

  this.state.listViewData = Array(20)
    .fill("")
    .map((_, i) => ({ key: `${i}`, text: `item #${i}` }));

//...
render() {
    return (
        <SwipeListView
            data={this.state.listViewData}
            renderItem={ (data, rowMap) => (
                <View style={styles.rowFront}>
                    <Text>I am {data.item.text} in a SwipeListView</Text>
                </View>
            )}
            renderHiddenItem={ (data, rowMap) => (
                <View style={styles.rowBack}>
                    <Text>Left</Text>
                    <Text>Right</Text>
                </View>
            )}
            leftOpenValue={75}
            rightOpenValue={-75}
        />
    )
}
```

Complete usage example:

```jsx
import React, { useState } from "react";
import {
  StyleSheet,
  Text,
  TouchableOpacity,
  TouchableHighlight,
  View,
} from "react-native";

import { SwipeListView } from "react-native-swipe-list-view";

export default function Basic() {
  const [listData, setListData] = useState(
    Array(20)
      .fill("")
      .map((_, i) => ({ key: `${i}`, text: `item #${i}` })),
  );

  const closeRow = (rowMap, rowKey) => {
    if (rowMap[rowKey]) {
      rowMap[rowKey].closeRow();
    }
  };

  const deleteRow = (rowMap, rowKey) => {
    closeRow(rowMap, rowKey);
    const newData = [...listData];
    const prevIndex = listData.findIndex((item) => item.key === rowKey);
    newData.splice(prevIndex, 1);
    setListData(newData);
  };

  const onRowDidOpen = (rowKey) => {
    console.log("This row opened", rowKey);
  };

  const renderItem = (data) => (
    <TouchableHighlight
      onPress={() => console.log("You touched me")}
      style={styles.rowFront}
      underlayColor={"#AAA"}
    >
      <View>
        <Text>I am {data.item.text} in a SwipeListView</Text>
      </View>
    </TouchableHighlight>
  );

  const renderHiddenItem = (data, rowMap) => (
    <View style={styles.rowBack}>
      <Text>Left</Text>
      <TouchableOpacity
        style={[styles.backRightBtn, styles.backRightBtnLeft]}
        onPress={() => closeRow(rowMap, data.item.key)}
      >
        <Text style={styles.backTextWhite}>Close</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={[styles.backRightBtn, styles.backRightBtnRight]}
        onPress={() => deleteRow(rowMap, data.item.key)}
      >
        <Text style={styles.backTextWhite}>Delete</Text>
      </TouchableOpacity>
    </View>
  );

  return (
    <View style={styles.container}>
      <SwipeListView
        data={listData}
        renderItem={renderItem}
        renderHiddenItem={renderHiddenItem}
        leftOpenValue={75}
        rightOpenValue={-150}
        previewRowKey={"0"}
        previewOpenValue={-40}
        previewOpenDelay={3000}
        onRowDidOpen={onRowDidOpen}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: "white",
    flex: 1,
  },
  backTextWhite: {
    color: "#FFF",
  },
  rowFront: {
    alignItems: "center",
    backgroundColor: "#CCC",
    borderBottomColor: "black",
    borderBottomWidth: 1,
    justifyContent: "center",
    height: 50,
  },
  rowBack: {
    alignItems: "center",
    backgroundColor: "#DDD",
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    paddingLeft: 15,
  },
  backRightBtn: {
    alignItems: "center",
    bottom: 0,
    justifyContent: "center",
    position: "absolute",
    top: 0,
    width: 75,
  },
  backRightBtnLeft: {
    backgroundColor: "blue",
    right: 75,
  },
  backRightBtnRight: {
    backgroundColor: "red",
    right: 0,
  },
});
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-swipe-list-view Releases](https://github.com/react-native-oh-library/react-native-swipe-list-view/releases/)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                 | Description                                                                                                                                                                                                                                                                                                                                                                                      | Type     | Required | Platform      | HarmonyOS Support |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ------------- | ----------------- |
| data                                 | List of objects to be passed into the `renderItem` and `renderHiddenItem` functions. Each item must include a unique `key` property or `keyExtractor` must be implemented to ensure full functionality.                                                                                                                                                                                          | array    | YES      | Android iOS | YES               |
| useSectionList                       | Render list using React Native's `SectionList`                                                                                                                                                                                                                                                                                                                                                   | bool     | NO       | Android iOS | YES               |
| renderItem                           | How to render a row in a FlatList. Should return a valid React Element.                                                                                                                                                                                                                                                                                                                          | func     | YES      | Android iOS | YES               |
| renderHiddenItem                     | How to render a hidden row in a FlatList (renders behind the row). Should return a valid React Element. This is required unless `renderItem` returns a `<SwipeRow>` (see [Per Row Behavior](https://github.com/jemise111/react-native-swipe-list-view/blob/master/docs/per-row-behavior.md)).                                                                                                    | func     | YES      | Android iOS | YES               |
| leftOpenValue                        | TranslateX value for opening the row to the left (positive number)                                                                                                                                                                                                                                                                                                                               | number   | NO       | Android iOS | YES               |
| rightOpenValue                     | TranslateX value for opening the row to the right (negative number)                                                                                                                                                                                                                                                                                                                              | number | NO       | Android iOS | YES               |
| leftActivationValue                | TranslateX value for firing onLeftActionStatusChange (positive number)                                                                                                                                                                                                                                                                                                                           | number | NO       | Android iOS  | NO                |
| rightActivationValue               | TranslateX value for firing onRightActionStatusChange (negative number)                                                                                                                                                                                                                                                                                                                          | number | NO       | Android iOS | YES               |
| rightActionValue                   | TranslateX value for right action to which the row will be shifted after gesture release                                                                                                                                                                                                                                                                                                         | number | NO       | Android iOS | YES               |
| initialLeftActionState             | Initial value for left action state (default is false)                                                                                                                                                                                                                                                                                                                                           | bool   | NO       | Android iOS | YES               |
| initialRightActionState            | Initial value for right action state (default is false)                                                                                                                                                                                                                                                                                                                                          | bool   | NO       | Android iOS | YES               |
| closeOnRowPress                    | Should open rows be closed when a row is pressed                                                                                                                                                                                                                                                                                                                                                 | bool   | NO       | Android iOS | YES               |
| closeOnRowOpen                     | Should open rows be closed when another row is opened                                                                                                                                                                                                                                                                                                                                            | bool   | NO       | Android iOS | YES               |
| closeOnRowBeginSwipe               | Should open rows be closed when a row begins to swipe open                                                                                                                                                                                                                                                                                                                                       | bool   | NO       | Android iOS | YES               |
| closeOnScroll                      | Should open rows be closed when the listView begins scrolling                                                                                                                                                                                                                                                                                                                                    | bool   | NO       | Android iOS | YES               |
| disableLeftSwipe                   | Disable ability to swipe the row left                                                                                                                                                                                                                                                                                                                                                            | bool   | NO       | Android iOS | YES               |
| disableRightSwipe                  | Disable ability to swipe the row right                                                                                                                                                                                                                                                                                                                                                           | bool   | NO       | Android iOS | YES               |
| stopLeftSwipe                      | TranslateX value for stop the row to the left (positive number). This number is the stop value corresponding to the leftOpenValue (while the row is swiping in the right direction)                                                                                                                                                                                                            | number | NO       | Android iOS | YES               |
| stopRightSwipe                     | TranslateX value for stop the row to the right (negative number). This number is the stop value corresponding to the rightOpenValue (while the row is swiping in the left direction)                                                                                                                                                                                                           | number | NO       | Android iOS | YES               |
| directionalDistanceChangeThreshold | Change the sensitivity of the row                                                                                                                                                                                                                                                                                                                                                                | number | NO       | Android iOS | YES               |
| swipeToOpenPercent                 | What % of the left/right openValue does the user need to swipe past to trigger the row opening.                                                                                                                                                                                                                                                                                                  | number | NO       | Android iOS | YES               |
| swipeToClosePercent                | What % of the left/right openValue does the user need to swipe past to trigger the row closing.                                                                                                                                                                                                                                                                                                  | number | NO       | Android iOS | YES               |
| swipeToOpenVelocityContribution    | Describes how much the ending velocity of the gesture affects whether the swipe will result in the item being closed or open. A velocity factor of 0 (the default) means that the velocity will have no bearing on whether the swipe settles on a closed or open position and it'll just take into consideration the swipeToOpenPercent. Ideal values for this prop tend to be between 5 and 15. | number | NO       | Android iOS | YES               |
| recalculateHiddenLayout            | Enable hidden row onLayout calculations to run always. By default, hidden row size calculations are only done on the first onLayout event for performance reasons. Passing true here will cause calculations to run on every onLayout event. You may want to do this if your rows' sizes can change. One case is a SwipeListView with rows of different heights and an options to delete rows.   | bool   | NO       | Android iOS | YES               |
| swipeGestureBegan                  | Called when a swipe row is animating swipe                                                                                                                                                                                                                                                                                                                                                       | func   | NO       | Android iOS | YES               |
| swipeGestureEnded                  | Called when user has ended their swipe gesture                                                                                                                                                                                                                                                                                                                                                   | func   | NO       | Android iOS | YES               |
| onRowOpen                          | Called when a swipe row is animating open. This has a param of toValue which is the new X value the row (after it has opened). This can be used to calculate which direction the row has been swiped open.                                                                                                                                                                                       | func   | NO       | Android iOS | YES               |
| onRowDidOpen                       | Called when a swipe row has animated open                                                                                                                                                                                                                                                                                                                                                        | func   | NO       | Android iOS | YES               |
| onRowClose                         | Called when a swipe row is animating closed                                                                                                                                                                                                                                                                                                                                                      | func   | NO       | Android iOS | YES               |
| onRowDidClose                      | Called when a swipe row has animated closed                                                                                                                                                                                                                                                                                                                                                      | func   | NO       | Android iOS | YES               |
| onLeftActionStatusChange           | Called once when swipe value crosses the leftActivationValue                                                                                                                                                                                                                                                                                                                                     | func   | NO       | Android iOS | YES               |
| onRightActionStatusChange          | Called once when swipe value crosses the rightActivationValue                                                                                                                                                                                                                                                                                                                                    | func   | NO       | Android iOS | YES               |
| onLeftAction                       | Called when row shifted to leftActivationValue                                                                                                                                                                                                                                                                                                                                                   | func   | NO       | Android iOS | YES               |
| onRightAction                      | Called when row shifted to rightActivationValue                                                                                                                                                                                                                                                                                                                                                  | func   | NO       | Android iOS | YES               |
| onScrollEnabled                    | Called when scrolling has been enabled/disabled                                                                                                                                                                                                                                                                                                                                                  | func   | NO       | Android iOS | YES               |
| swipeRowStyle                      | Styles for the parent wrapper View of the SwipeRow                                                                                                                                                                                                                                                                                                                                               | object | NO       | Android iOS | YES               |
| listViewRef                        | Called when the ListView ref is set and passes a ref to the ListView. e.g. listViewRef={ ref => this._swipeListViewRef = ref }                                                                                                                                                                                                                                                                   | func   | NO       | Android iOS | YES               |
| previewRowKey                      | Should the row with this key do a slide out preview to show that the list is swipeable                                                                                                                                                                                                                                                                                                           | string | NO       | Android iOS | YES               |
| previewDuration                    | Duration of the slide out preview animation                                                                                                                                                                                                                                                                                                                                                      | number | NO       | Android iOS | YES               |
| previewRepeat                      | Should the animation repeat                                                                                                                                                                                                                                                                                                                                                                      | bool   | NO       | Android iOS | YES               |
| previewRepeatDelay                 | Delay between each preview repeat in milliseconds                                                                                                                                                                                                                                                                                                                                                | number | NO       | Android iOS | YES               |
| previewOpenValue                   | TranslateX value for the slide out preview animation.                                                                                                                                                                                                                                                                                                                                            | number | NO       | Android iOS | YES               |
| previewOpenDelay                   | Add some delay before opening the preview row. Can be useful when you have enter animation.                                                                                                                                                                                                                                                                                                      | number | NO       | Android iOS | YES               |
| friction                           | Friction for the open / close animation. Controls "bounciness"/overshoot.                                                                                                                                                                                                                                                                                                                        | number | NO       | Android iOS | YES               |
| tension                            | Tension for the open / close animation. Controls speed                                                                                                                                                                                                                                                                                                                                           | number | NO       | Android iOS | YES               |
| restSpeedThreshold                 | RestSpeedThreshold for the open / close animation. Controls speed.                                                                                                                                                                                                                                                                                                                               | number | NO       | Android iOS | YES               |
| restDisplacementThreshold          | RestDisplacementThreshold for the open / close animation. Controls speed.                                                                                                                                                                                                                                                                                                                        | number | NO       | Android iOS | YES               |
| onSwipeValueChange                 | Callback invoked any time the translateX value of a row changes                                                                                                                                                                                                                                                                                                                                  | func   | NO       | Android iOS | YES               |
| renderListView                     | To render a custom ListView component, if you don't want to use ReactNative one. Note: This will call renderRow, not renderItem                                                                                                                                                                                                                                                                  | func   | NO       | Android iOS | YES               |
| shouldItemUpdate                   | Callback to determine whether component should update                                                                                                                                                                                                                                                                                                                                            | func   | NO       | Android iOS | YES               |
| useNativeDriver                    | useNativeDriver: true for all animations                                                                                                                                                                                                                                                                                                                                                         | bool   | NO       | Android iOS | YES               |
| onPreviewEnd                       | Callback that runs after row swipe preview is finished                                                                                                                                                                                                                                                                                                                                           | func   | NO       | Android iOS | YES               |

**SwipeRow**

| Name                                 | Description                                                                                                                                                                                                                                                                                                                                                                                      | Type     | Required | Platform      | HarmonyOS Support |
|:------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------:|:--------:|:-------------:| ----------------- |
| closeOnRowPress                    | Should the row be closed when it is tapped                                                                                                                                                                                                                                                                                                                                                       | bool   | NO       | Android iOS | YES               |
| directionalDistanceChangeThreshold | Change the sensitivity of the row                                                                                                                                                                                                                                                                                                                                                                | number | NO       | Android iOS | YES               |
| friction                           | Friction for the open / close animation. Controls "bounciness"/overshoot. https://facebook.github.io/react-native/docs/animated#spring                                                                                                                                                                                                                                                           | number | NO       | Android iOS | YES               |
| tension                            | Tension for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring                                                                                                                                                                                                                                                                             | number | NO       | Android iOS | YES               |
| restSpeedThreshold                 | RestSpeedThreshold for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring                                                                                                                                                                                                                                                                  | number | NO       | Android iOS | YES               |
| restDisplacementThreshold          | RestDisplacementThreshold for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring                                                                                                                                                                                                                                                           | number | NO       | Android iOS | YES               |
| leftOpenValue                      | TranslateX value for opening the row to the left (positive number)                                                                                                                                                                                                                                                                                                                               | number | YES      | Android iOS | YES               |
| rightOpenValue                     | TranslateX value for opening the row to the right (negative number)                                                                                                                                                                                                                                                                                                                              | number | YES      | Android iOS | YES               |
| leftActivationValue                | TranslateX value for firing onLeftActionStatusChange (positive number)                                                                                                                                                                                                                                                                                                                           | number | NO       | Android iOS | YES               |
| rightActivationValue               | TranslateX value for firing onRightActionStatusChange (negative number)                                                                                                                                                                                                                                                                                                                          | number | NO       | Android iOS | YES               |
| initialLeftActionState             | Initial value for left action state (default is false)                                                                                                                                                                                                                                                                                                                                           | bool   | NO       | Android iOS | YES               |
| initialRightActionState`           | Initial value for right action state (default is false)                                                                                                                                                                                                                                                                                                                                          | bool   | NO       | Android iOS | YES               |
| leftActionValue                    | TranslateX value for left action to which the row will be shifted after gesture release                                                                                                                                                                                                                                                                                                          | number | NO       | Android iOS | YES               |
| rightActionValue                   | TranslateX value for right action to which the row will be shifted after gesture release                                                                                                                                                                                                                                                                                                         | number | NO       | Android iOS | YES               |
| stopLeftSwipe                      | TranslateX value for stop the row to the left (positive number). This number is the stop value corresponding to the leftOpenValue (while the row is swiping in the right direction)                                                                                                                                                                                                            | number | NO       | Android iOS | YES               |
| stopRightSwipe                     | TranslateX value for stop the row to the right (negative number). This number is the stop value corresponding to the rightOpenValue (while the row is swiping in the left direction)                                                                                                                                                                                                           | number | NO       | Android iOS | YES               |
| onRowPress                         | Called when row is pressed.                                                                                                                                                                                                                                                                                                                                                                      | func   | NO       | Android iOS | YES               |
| onRowOpen                          | Called when row is animating open. Used by the SwipeListView to keep references to open rows.                                                                                                                                                                                                                                                                                                    | func   | NO       | Android iOS | YES               |
| onRowDidOpen                       | Called when row has animated open                                                                                                                                                                                                                                                                                                                                                                | func   | NO       | Android iOS | YES               |
| onRowClose                         | Called when row is animating closed                                                                                                                                                                                                                                                                                                                                                              | func   | NO       | Android iOS | YES               |
| onRowDidClose                      | Called when a swipe row has animated closed                                                                                                                                                                                                                                                                                                                                                      | func   | NO       | Android iOS | YES               |
| onLeftActionStatusChange           | Called once when swipe value crosses the leftActivationValue                                                                                                                                                                                                                                                                                                                                     | func   | NO       | Android iOS | YES               |
| onRightActionStatusChange          | Called once when swipe value crosses the rightActivationValue                                                                                                                                                                                                                                                                                                                                    | func   | NO       | Android iOS | YES               |
| onLeftAction                       | Called when row shifted to leftActivationValue                                                                                                                                                                                                                                                                                                                                                   | func   | NO       | Android iOS | YES               |
| onRightAction                      | Called when row shifted to rightActivationValue                                                                                                                                                                                                                                                                                                                                                  | func   | NO       | Android iOS | YES               |
| swipeToOpenPercent                 | What % of the left/right openValue does the user need to swipe past to trigger the row opening.                                                                                                                                                                                                                                                                                                  | number | NO       | Android iOS | YES               |
| swipeToClosePercent                | What % of the left/right openValue does the user need to swipe past to trigger the row closing.                                                                                                                                                                                                                                                                                                  | number | NO       | Android iOS | YES               |
| setScrollEnabled                   | Used by the SwipeListView to close rows on scroll events. You shouldn't need to use this prop explicitly.                                                                                                                                                                                                                                                                                        | func   | NO       | Android iOS | YES               |
| disableLeftSwipe                   | Disable ability to swipe the row left                                                                                                                                                                                                                                                                                                                                                            | bool   | NO       | Android iOS | YES               |
| disableRightSwipe                  | Disable ability to swipe the row right                                                                                                                                                                                                                                                                                                                                                           | bool   | NO       | Android iOS | YES               |
| recalculateHiddenLayout            | Enable hidden row onLayout calculations to run always                                                                                                                                                                                                                                                                                                                                            | bool   | NO       | Android iOS | YES               |
| style                              | Styles for the parent wrapper View of the SwipeRow                                                                                                                                                                                                                                                                                                                                               | object | YES      | Android iOS | YES               |
| preview                            | Should the row do a slide out preview to show that it is swipeable                                                                                                                                                                                                                                                                                                                               | bool   | NO       | Android iOS | YES               |
| previewDuration                    | Duration of the slide out preview animation                                                                                                                                                                                                                                                                                                                                                      | number | NO       | Android iOS | YES               |
| previewRepeat                      | Should the animation repeat                                                                                                                                                                                                                                                                                                                                                                      | bool   | NO       | Android iOS | YES               |
| previewRepeatDelay                 | Delay between each preview repeat in milliseconds                                                                                                                                                                                                                                                                                                                                                | number | NO       | Android iOS | YES               |
| previewOpenValue                   | TranslateX value for the slide out preview animation                                                                                                                                                                                                                                                                                                                                             | number | NO       | Android iOS | YES               |
| onSwipeValueChange                 | Callback invoked any time the translateX value of the row changes                                                                                                                                                                                                                                                                                                                                | func   | NO       | Android iOS | YES               |
| swipeGestureBegan                  | Called when the row is animating swipe                                                                                                                                                                                                                                                                                                                                                           | func   | NO       | Android iOS | YES               |
| swipeGestureEnded                  | Called when user has ended their swipe gesture                                                                                                                                                                                                                                                                                                                                                   | func   | NO       | Android iOS | YES               |
| swipeToOpenVelocityContribution    | Describes how much the ending velocity of the gesture affects whether the swipe will result in the item being closed or open. A velocity factor of 0 (the default) means that the velocity will have no bearing on whether the swipe settles on a closed or open position and it'll just take into consideration the swipeToOpenPercent. Ideal values for this prop tend to be between 5 and 15. | number | NO       | Android iOS | YES               |
| shouldItemUpdate                   | Callback to determine whether component should update                                                                                                                                                                                                                                                                                                                                            | func   | NO       | Android iOS | YES               |
| forceCloseToLeftThreshold          | TranslateX amount(not value!) threshold that triggers force-closing the row to the Left End (positive number)                                                                                                                                                                                                                                                                                    | number | NO       | Android iOS | YES               |
| forceCloseToRightThreshold         | TranslateX amount(not value!) threshold that triggers force-closing the row to the Right End (positive number)                                                                                                                                                                                                                                                                                   | number | NO       | Android iOS | YES               |
| onForceCloseToLeft                 | Callback invoked when row is force closing to the Left End                                                                                                                                                                                                                                                                                                                                       | func   | NO       | Android iOS | YES               |
| onForceCloseToRight                | Callback invoked when row is force closing to the Right End                                                                                                                                                                                                                                                                                                                                      | func   | NO       | Android iOS | YES               |
| onForceCloseToLeftEnd              | Callback invoked when row has finished force closing to the Left End                                                                                                                                                                                                                                                                                                                             | func   | NO       | Android iOS | YES               |
| onForceCloseToRightEnd             | Callback invoked when row has finished force closing to the Right End                                                                                                                                                                                                                                                                                                                            | func   | NO       | Android iOS | YES               |
| useNativeDriver                    | useNativeDriver: true for all animations                                                                                                                                                                                                                                                                                                                                                       | bool   | NO       | Android iOS | YES               |
| swipeKey                           | Optional key to identify a standalone row, used in the onSwipeValueChange callback                                                                                                                                                                                                                                                                                                             | string | NO       | Android iOS | YES               |
| onPreviewEnd                       | Callback that runs after row swipe preview is finished                                                                                                                                                                                                                                                                                                                                           | func   | NO       | Android iOS | YES               |

## Known Issues

- [ ] The leftActivationValue property is not adapted in HarmonyOS for the time being [issue#4](https://github.com/react-native-oh-library/react-native-swipe-list-view/issues/4) 

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/jemise111/react-native-swipe-list-view/blob/master/LICENSE).
