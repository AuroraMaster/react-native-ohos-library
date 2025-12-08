Template Version: v0.3.0

<p align="center">
	<h1 align="center"> <code>teaset</code> </h1>
</p>

This project is based on [teaset@0.7.5](https://github.com/rilyu/teaset).

Please go to the Releases release address of the third-party library to view the supporting version information: [@react-native-ohos/teaset Releases](https://github.com/react-native-oh-library/teaset/releases). For older versions that are not published to npm, install the tgz package by referring to the [Installation Guide](/en/tgz-usage-en.md).

| Version              | Releases info                                     |  Support RN version                |
| ------------------------- | ------------------------------------------------- |  -------------------------- |
| 0.7.6                 | [@react-native-ohos/teaset Releases](https://github.com/react-native-oh-library/teaset/releases)  | 0.72/0.77 |

## Installation and Usage

Run the following command in your project directory:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/teaset

# 0.72
npm install @react-navigation/native-stack@6.9.26
npm install @react-navigation/native@^6.1.7
npm install @react-native-oh-tpl/react-native-screens

# 0.77
npm install @react-navigation/native-stack@7.2.0
npm install @react-navigation/native@7.1.17
npm install @react-native-ohos/react-native-screens

```

#### **yarn**

```bash
yarn add @react-native-ohos/teaset

# 0.72
yarn add @react-navigation/native-stack@6.9.26
yarn add @react-navigation/native@6.1.7
yarn add @react-native-oh-tpl/react-native-screens

# 0.77
yarn add @react-navigation/native-stack@7.2.0
yarn add @react-navigation/native@7.1.17
yarn add @react-native-ohos/react-native-screens
```

<!-- tabs:end -->

The sample below demonstrates a basic usage scenario:

**Hello world**  
Import components from the teaset package and use them directly:
```
import React, {Component} from 'react';
import {View, AppRegistry} from 'react-native';

import {Label} from 'teaset';

class HelloWorldApp extends Component {
	render() {
		return (
			<View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
				<Label size='xl' text='Hello world!' />
			</View>
		);
	}
}

AppRegistry.registerComponent('HelloWorldApp', () => HelloWorldApp);
```
**On-demand import**  
Import individual components for on-demand usage:
```
import Label from 'teaset/components/Label/Label';
```

## Link

The HarmonyOS implementation of this library depends on the native code of react-native-screens . If the library are already integrated into your HarmonyOS project, you can skip this section.

If not, follow the guidance in [react-native-screens documentation](/en/react-native-screens.md) to integrate it.

## Constraints and Limitations

### Compatibility

The content in this document has been verified under the following environment:

1. RNOH: 0.72.x/0.77.x; SDK: HarmonyOS 6.0.0.47 (API Version 20 Release); IDE: DevEco Studio 6.0.0 Release; ROM: 6.0.0.108 SP6;

## Components

> [!TIP] The "Platform" column reflects platform support in the original third-party library.

> [!TIP] The "HarmonyOS Support" column shows HarmonyOS support status: yes, no, or partially. Usage is cross-platform; effects match iOS or Android.

### 1. Theme

Theme provides global styling configuration to unify the application's visual design.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| set | Configure the theme palette. Accepts a complete theme object or partial overrides. | function | yes | iOS/Android | yes |
| themes | Retrieve all built-in theme palettes (default, black, violet). | object | yes | iOS/Android | yes |

**Theme Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isLandscape | Whether the device is in landscape orientation. | bool | no | iOS/Android | yes |
| statusBarHeight | Status bar height. | number | no | iOS/Android | yes |
| screenInset | Screen content inset values. | object | no | iOS/Android | yes |

### 2. Label

Label displays text content with multiple preset styles.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Label type (default, title, detail, danger). | string | no | iOS/Android | yes |
| size | Font size (lg, md, sm, xs). | string | no | iOS/Android | yes |
| text | Text content. | string/number | no | iOS/Android | yes |
| numberOfLines | Number of display lines. | number | no | iOS/Android | yes |

### 3. Button

Button offers multiple button styles.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Button type (default, primary, secondary, danger, link). | string | no | iOS/Android | yes |
| size | Button size (lg, md, sm, xs). | string | no | iOS/Android | yes |
| title | Button title. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title. | style | no | iOS/Android | yes |
| disabled | Disable the button. | bool | no | iOS/Android | yes |
| onPress | Press handler. | function | no | iOS/Android | yes |

### 4. Checkbox

Checkbox supports single or multiple selection.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| checked | Whether the checkbox is selected. | bool | no | iOS/Android | yes |
| defaultChecked | Default selection state. | bool | no | iOS/Android | yes |
| size | Icon size (lg, md, sm). | string | no | iOS/Android | yes |
| title | Title text. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title. | style | no | iOS/Android | yes |
| checkedIcon | Custom icon for the checked state. | element | no | iOS/Android | yes |
| checkedIconStyle | Style for the checked icon. | ImageStyle | no | iOS/Android | yes |
| uncheckedIcon | Custom icon for the unchecked state. | element | no | iOS/Android | yes |
| uncheckedIconStyle | Style for the unchecked icon. | ImageStyle | no | iOS/Android | yes |
| disabled | Disable the checkbox. | bool | no | iOS/Android | yes |
| hitSlop | Extend the touchable area. | object | no | iOS/Android | yes |
| onChange | State change handler. | function | no | iOS/Android | yes |

### 5. Input

Input handles single-line or multiline text input.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| size | Input size (xl, lg, md, sm). | string | no | iOS/Android | yes |
| disabled | Disable the input. | bool | no | iOS/Android | yes |
| underlineColorAndroid | Underline color on Android. | string/'rgba(0, 0, 0, 0)' | no | Android | yes |
| onChangeText | Text change handler. | function | no | iOS/Android | yes |

### 6. Select

Select behaves like an HTML select dropdown.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| size | Select size (xl, lg, md, sm). | string | no | iOS/Android | yes |
| value | Selected value. | any | no | iOS/Android | yes |
| valueStyle | Style for the selected text. | style | no | iOS/Android | yes |
| items | Items in the dropdown. | array | no | iOS/Android | yes |
| getItemValue | Function to retrieve item value. | function | no | iOS/Android | yes |
| getItemText | Function to retrieve item label. | function | no | iOS/Android | yes |
| pickerType | Picker type (auto, pull, popover). | string | no | iOS/Android | yes |
| pickerTitle | Picker title. | string | no | iOS/Android | yes |
| editable | Whether the value is editable. | bool | no | iOS/Android | yes |
| icon | Right-side icon. | element | no | iOS/Android | yes |
| iconTintColor | Icon tint color. | string | no | iOS/Android | yes |
| placeholder | Placeholder text. | string | no | iOS/Android | yes |
| placeholderTextColor | Placeholder text color. | string | no | iOS/Android | yes |
| disabled | Disable the select. | bool | no | iOS/Android | yes |
| onSelected | Selection handler. | function | no | iOS/Android | yes |

### 7. Stepper

Stepper provides numeric increment and decrement controls.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| defaultValue | Default value. | number | no | iOS/Android | yes |
| value | Current value. | number | no | iOS/Android | yes |
| step | Step size. | number | no | iOS/Android | yes |
| max | Maximum value. | number | no | iOS/Android | yes |
| min | Minimum value. | number | no | iOS/Android | yes |
| valueStyle | Style for the value text. | style | no | iOS/Android | yes |
| valueFormat | Value formatting function. | function | no | iOS/Android | yes |
| subButton | Custom decrement button. | element | no | iOS/Android | yes |
| addButton | Custom increment button. | element | no | iOS/Android | yes |
| showSeparator | Show separators. | bool | no | iOS/Android | yes |
| disabled | Disable the stepper. | bool | no | iOS/Android | yes |
| editable | Allow text editing. | bool | no | iOS/Android | yes |
| onChange | Value change handler. | function | no | iOS/Android | yes |

### 8. SearchInput

SearchInput is an input field with a search icon.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Component style. | ViewStyle | no | iOS/Android | yes |
| inputStyle | Style for the input field. | style | no | iOS/Android | yes |
| iconSize | Icon size. | number | no | iOS/Android | yes |
| disabled | Disable the input. | bool | no | iOS/Android | yes |
| underlineColorAndroid | Underline color on Android. | string/'rgba(0, 0, 0, 0)' | no | Android | yes |
| onChangeText|  Text change handler | function | no | iOS/Android | yes |

### 9. Badge

Badge displays notification counts or status indicators.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Badge type (capsule, square, dot). | string | no | iOS/Android | yes |
| count | Number to display. | number | no | iOS/Android | yes |
| countStyle | Style for the count text. | style | no | iOS/Android | yes |
| maxCount | Maximum number before showing a plus sign. | number | no | iOS/Android | yes |

### 10. Popover

Popover displays contextual bubbles.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| arrow | Arrow position (none, topLeft, top, topRight, rightTop, right, rightBottom, bottomRight, bottom, bottomLeft, leftBottom, left, leftTop). | string | no | iOS/Android | yes |
| paddingCorner | Distance between arrow and corners. | number | no | iOS/Android | yes |

### 11. NavigationBar

NavigationBar renders a top navigation bar.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Navigation bar type (auto, ios, android, harmony). | string | no | iOS/Android | yes |
| title | Title content. | string/element | no | iOS/Android | yes |
| titleStyle | Style for the title. | style | no | iOS/Android | yes |
| leftView | Left-side content. | element | no | iOS/Android | yes |
| rightView | Right-side content. | element | no | iOS/Android | yes |
| tintColor | Tint color for left and right buttons. | string | no | iOS/Android | yes |
| background | Background element. | element | no | iOS/Android | yes |
| hidden | Hide the navigation bar. | bool | no | iOS/Android | yes |
| animated | Animate hide/show. | bool | no | iOS/Android | yes |
| statusBarStyle | Status bar style (default, light-content, dark-content). | string | no | iOS/Android | yes |
| statusBarColor | Status bar color. | string | no | iOS/Android | yes |
| statusBarHidden | Hide the status bar. | bool | no | iOS/Android | yes |
| statusBarInsets | Reserve space for the status bar. | bool | no | iOS | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Title | Title component for the navigation bar. | class | no | iOS/Android | yes |
| Button | Button component for the navigation bar. | class | no | iOS/Android | yes |
| LinkButton | Link-style button component. | class | no | iOS/Android | yes |
| IconButton | Icon button component. | class | no | iOS/Android | yes |
| BackButton | Back button component. | class | no | iOS/Android | yes |

**NavigationBar.Title**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | Display text. | string/number | no | iOS/Android | yes |
| numberOfLines | Number of lines. | number | no | iOS/Android | yes |
| allowFontScaling | Allow system font scaling. | bool | no | iOS | yes |

The **allowFontScaling** property depends on the application’s configuration.For the detailed configuration method, refer to [How to configure whether the in-app font size follows the system setting](https://developer.huawei.com/consumer/cn/doc/architecture-guides/common-v1_26-ts_20-0000002298448781) or follow the steps below:

- 1.Create a new configuration file: AppScope/resources/base/profile/configuration.json
```
{
  "configuration": {
    // nonFollowSystem: does not follow system changes; followSystem: follows system changes
    "fontSizeScale": "followSystem",
    "fontSizeMaxScale": "3.2"
  }
}

```
- 2.Reference this configuration in AppScope/app.json5
```
{
  "app": {
    "bundleName": "com.example.temp_demo",
    "vendor": "example",
    "versionCode": 1000000,
    "versionName": "1.0.0",
    "icon": "$media:app_icon",
    "label": "$string:app_name",
    // Reference here
    "configuration": "$profile:configuration"
  },
}
```

**NavigationBar.Button**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| hitSlop | Extend the touchable area. | object | no | iOS/Android | yes |

**NavigationBar.LinkButton**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Button title | string/number | no | iOS/Android | yes |

**NavigationBar.IconButton**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| icon | Button icon | ImageSource | no | iOS/Android | yes |

**NavigationBar.BackButton**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title text. | string/number | no | iOS/Android | yes |
| icon | Button icon. | ImageSource | no | iOS/Android | yes |

### 12. ListRow

ListRow displays list items, commonly used on settings screens.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| detail | Detail content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title. | style | no | iOS/Android | yes |
| detailStyle | Style for the detail text. | style | no | iOS/Android | yes |
| detailMultiLine | Allow multiline detail text. | bool | no | iOS/Android | yes |
| icon | Left icon. | element/ImageSource | no | iOS/Android | yes |
| accessory | Right accessory (none, auto, empty, indicator, check). | string/element | no | iOS/Android | yes |
| topSeparator | Top separator (none, full, indent). | string | no | iOS/Android | yes |
| bottomSeparator | Bottom separator (none, full, indent). | string | no | iOS/Android | yes |
| titlePlace | Title position (left, top, none). | string | no | iOS/Android | yes |
| swipeActions | Swipe action buttons. | array | no | iOS/Android | yes |
| onPress | Press handler. | function | no | iOS/Android | yes |
| activeOpacity | Opacity on press. | number | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| SwipeActionButton | Swipe action button component. | class | no | iOS/Android | yes |

**ListRow.SwipeActionButton**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Display style (default, danger). | string | no | iOS/Android | yes |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title. | style | no | iOS/Android | yes |

### 13. Carousel

Carousel provides an image slideshow.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| carousel | Enable auto-play. | bool | no | iOS/Android | yes |
| interval | Auto-play interval in milliseconds. | number | no | iOS/Android | yes |
| direction | Play direction (forward, backward). | string | no | iOS/Android | yes |
| startIndex | Initial page index. | number | no | iOS/Android | yes |
| cycle | Loop playback. | bool | no | iOS/Android | yes |
| control | Page indicator. | bool/element | no | iOS/Android | yes |
| horizontal | Horizontal scrolling. | bool | no | iOS/Android | yes |
| pagingEnabled | Enable paging. | bool | no | iOS/Android | yes |
| showsHorizontalScrollIndicator | Show horizontal scroll indicator. | bool | no | iOS/Android | yes |
| showsVerticalScrollIndicator | Show vertical scroll indicator. | bool | no | iOS/Android | yes |
| alwaysBounceHorizontal | Always allow horizontal bounce. | bool | no | iOS/Android | yes |
| alwaysBounceVertical | Always allow vertical bounce. | bool | no | iOS/Android | yes |
| bounces | Enable bounce effect. | bool | no | iOS/Android | yes |
| automaticallyAdjustContentInsets | Auto-adjust content insets. | bool | no | iOS/Android | yes |
| scrollEventThrottle | Scroll event throttle interval. | number | no | iOS/Android | yes |
| onChange | Page change handler. | function | no | iOS/Android | yes |
| scrollToPage | Scroll to a specific page. | function | no | iOS/Android | yes |
| scrollToNextPage | Scroll to the next page. | function | no | iOS/Android | yes |

**Carousel.Control Component:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| dot | Page indicator dot element. | element | no | iOS/Android | yes |
| activeDot | Active page indicator element. | element | no | iOS/Android | yes |

### 14. Projector

Projector displays multi-page content with view caching.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| index | Current index. | number | no | iOS/Android | yes |
| slideStyle | Slide style. | ViewStyle | no | iOS/Android | yes |

### 15. SegmentedBar

SegmentedBar renders a segmented toolbar.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| justifyItem | Item layout (fixed, scrollable). | string | no | iOS/Android | yes |
| indicatorType | Indicator type (none, boxWidth, itemWidth, customWidth). | string | no | iOS/Android | yes |
| indicatorPosition | Indicator position (top, bottom). | string | no | iOS/Android | yes |
| indicatorLineColor | Indicator line color. | string | no | iOS/Android | yes |
| indicatorLineWidth | Indicator line height. | number | no | iOS/Android | yes |
| indicatorWidth | indicator width. | number | no | iOS/Android | yes |
| indicatorPositionPadding | Indicator position padding. | number | no | iOS/Android | yes |
| animated | Enable animation. | bool | no | iOS/Android | yes |
| autoScroll | Auto-scroll to center. | bool | no | iOS/Android | yes |
| activeIndex | Active index. | number | no | iOS/Android | yes |
| onChange | Selection change handler. | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | SegmentedBar item component. | class | no | iOS/Android | yes |

**SegmentedBar.Item Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title. | style | no | iOS/Android | yes |
| activeTitleStyle | Style for the active title. | style | no | iOS/Android | yes |
| badge | Badge content. | string/number/element | no | iOS/Android | yes |
| active | Whether the item is active. | bool | no | iOS/Android | yes |

### 16. SegmentedView

SegmentedView is a segmented container.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | SegmentedView type (projector, carousel). | string | no | iOS/Android | yes |
| barPosition | Toolbar position (top, bottom). | string | no | iOS/Android | yes |
| barStyle | Toolbar style. | style | no | iOS/Android | yes |
| justifyItem | Item width distribution (fixed, scrollable). | string | no | iOS/Android | yes |
| indicatorType | Indicator type (none, boxWidth, itemWidth). | string | no | iOS/Android | yes |
| indicatorPosition | Indicator position (top, bottom). | string | no | iOS/Android | yes |
| indicatorLineColor | Indicator line color. | string | no | iOS/Android | yes |
| indicatorLineWidth | Indicator line height. | number | no | iOS/Android | yes |
| indicatorPositionPadding | Indicator position padding. | number | no | iOS/Android | yes |
| animated | Enable animation. | bool | no | iOS/Android | yes |
| autoScroll | Enable auto-scroll. | bool | no | iOS/Android | yes |
| activeIndex | Active index. | number | no | iOS/Android | yes |
| onChange | Page change handler. | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Sheet | SegmentedView sheet component. | class | no | iOS/Android | yes |

**SegmentedView.Sheet Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title. | style | no | iOS/Android | yes |
| activeTitleStyle | Style for the active title. | style | no | iOS/Android | yes |
| badge | Badge content. | string/number/element | no | iOS/Android | yes |

### 17. TabView

TabView provides bottom tab navigation.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | TabView type (projector, carousel). | string | no | iOS/Android | yes |
| barStyle | TabBar style. | style | no | iOS/Android | yes |
| activeIndex | Active sheet index. | number | no | iOS/Android | yes |
| onChange | Page change handler. | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Sheet | TabView sheet component. | class | no | iOS/Android | yes |
| Button | TabView button component. | class | no | iOS/Android | yes |

**TabView.Sheet Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Sheet type (sheet, button). | string | no | iOS/Android | yes |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| icon | Icon content. | ImageSource/element | no | iOS/Android | yes |
| activeIcon | Active icon content. | ImageSource/element | no | iOS/Android | yes |
| badge | Badge content. | string/number/element | no | iOS/Android | yes |
| onPress | Press handler. | function | no | iOS/Android | yes |

**TabView.Button Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title. | style | no | iOS/Android | yes |
| activeTitleStyle | Style for the active title. | style | no | iOS/Android | yes |
| icon | Icon content. | ImageSource/element | no | iOS/Android | yes |
| activeIcon | Active icon content. | ImageSource/element | no | iOS/Android | yes |
| badge | Badge content. | string/number/element | no | iOS/Android | yes |
| active | Active state. | bool | no | iOS/Android | yes |

### 18. TransformView

TransformView supports zooming and dragging.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| containerStyle | Container style. | style | no | iOS/Android | yes |
| maxScale | Maximum scale. | number | no | iOS/Android | yes |
| minScale | Minimum scale. | number | no | iOS/Android | yes |
| magnetic | Magnetic edges. | bool | no | iOS/Android | yes |
| tension | Drag tension coefficient. | number | no | iOS/Android | yes |
| onWillTransform | Event before transform starts. | function | no | iOS/Android | yes |
| onTransforming | Event during transform. | function | no | iOS/Android | yes |
| onDidTransform | Event after transform ends. | function | no | iOS/Android | yes |
| onWillMagnetic | Event before magnetic effect. | function | no | iOS/Android | yes |
| onDidMagnetic | Event after magnetic effect. | function | no | iOS/Android | yes |
| onPress | Press handler. | function | no | iOS/Android | yes |
| onLongPress | Long-press handler. | function | no | iOS/Android | yes |

### 19. AlbumView

AlbumView provides an image gallery experience.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| images | Image array. | array | yes | iOS/Android | yes |
| thumbs | Thumbnail array. | array | no | iOS/Android | yes |
| index | Current index. | number | no | iOS/Android | yes |
| defaultIndex | Default index. | number | no | iOS/Android | yes |
| maxScale | Maximum zoom scale. | number | no | iOS/Android | yes |
| space | Spacing between images. | number | no | iOS/Android | yes |
| control | Page indicator. | element | no | iOS/Android | yes |
| onWillChange | Event before page change. | function | no | iOS/Android | yes |
| onChange | Page change handler. | function | no | iOS/Android | yes |
| onPress | Press handler. | function | no | iOS/Android | yes |
| onLongPress | Long-press handler. | function | no | iOS/Android | yes |
| onWillLoadImage | Event before loading an image. | function | no | iOS/Android | yes |
| onLoadImageSuccess | Event when an image loads successfully. | function | no | iOS/Android | yes |
| onLoadImageFailure | Event when an image fails to load. | function | no | iOS/Android | yes |

### 20. Wheel

Wheel is a picker with a wheel interface.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | Options array. | array | yes | iOS/Android | yes |
| itemStyle | Style for items. | style | no | iOS/Android | yes |
| holeStyle | Style for the active window. | style | no | iOS/Android | yes |
| maskStyle | Style for the masking areas. | style | no | iOS/Android | yes |
| holeLine | Divider style for the active window. | string | no | iOS/Android | yes |
| index | Current index. | number | no | iOS/Android | yes |
| defaultIndex | Default index. | number | no | iOS/Android | yes |
| onChange | Selection change handler. | function | no | iOS/Android | yes |

### 21. Overlay

Overlay displays floating layers.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show an overlay view. | function | yes | iOS/Android | yes |
| hide | Hide the overlay view. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| View | Overlay view component. | class | yes | iOS/Android | yes |
| PullView | Overlay with pull effect. | class | no | iOS/Android | yes |
| PopView | Overlay with pop effect. | class | no | iOS/Android | yes |
| PopoverView | Overlay with popover effect. | class | no | iOS/Android | yes |

**Overlay.View**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Overlay style. | style | no | iOS/Android | yes |
| modal | Modal overlay. | bool | no | iOS/Android | yes |
| animated | Enable animation. | bool | no | iOS/Android | yes |
| overlayOpacity | Background opacity. | number | no | iOS/Android | yes |
| overlayPointerEvents | Background pointer events (auto, none). | string | no | iOS/Android | yes |
| autoKeyboardInsets | Auto-adjust for keyboard. | bool | no | iOS/Android | yes |
| onAppearCompleted | Event after appearing finishes. | function | no | iOS/Android | yes |
| onDisappearCompleted | Event after disappearing finishes. | function | no | iOS/Android | yes |
| onCloseRequest | Close request handler(Called when tapping the translucent area outside the content). | function | no | iOS/Android | yes |

**Overlay.PullView**

Inherits all Overlay.View properties and adds:

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| side | Drawer direction (top, bottom, left, right). | string | no | iOS/Android | yes |
| containerStyle | Container style. | style | no | iOS/Android | yes |
| rootTransform | Root transform (none, translate, scale). | string/array | no | iOS/Android | yes |

**Overlay.PopView**

Inherits all Overlay.View properties and adds:

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Display type (zoomOut, zoomIn, custom). | string | no | iOS/Android | yes |
| containerStyle | Container style. | style | no | iOS/Android | yes |
| customBounds | Custom bounds. | object | no | iOS/Android | yes |

**Overlay.PopoverView**

Inherits all Overlay.View properties and adds:

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| popoverStyle | Popover style. | style | no | iOS/Android | yes |
| fromBounds | Origin bounds. | object | yes | iOS/Android | yes |
| direction | Arrow direction (up, down, left, right). | string | no | iOS/Android | yes |
| autoDirection | Auto-adjust direction. | bool | no | iOS/Android | yes |
| directionInsets | Direction offset. | number | no | iOS/Android | yes |
| align | Alignment (start, center, end). | string | no | iOS/Android | yes |
| alignInsets | Alignment offset. | number | no | iOS/Android | yes |
| showArrow | Show arrow. | bool | no | iOS/Android | yes |
| paddingCorner | Corner padding. | number | no | iOS/Android | yes |
| overlayOpacity | Popover opacity. | number | no | iOS/Android | yes |

### 22. Toast

Toast shows lightweight notifications.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show a toast. | function | no | iOS/Android | yes |
| message | Show a message toast. | function | no | iOS/Android | yes |
| success | Show a success toast. | function | no | iOS/Android | yes |
| fail | Show a failure toast. | function | no | iOS/Android | yes |
| smile | Show a smile toast. | function | no | iOS/Android | yes |
| sad | Show a sad toast. | function | no | iOS/Android | yes |
| info | Show an info toast. | function | no | iOS/Android | yes |
| stop | Show a stop toast. | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|ToastView| Toast content display component | class | yes | iOS/Android | yes |
| defaultDuration | Default toast duration. | string | no | iOS/Android | yes |
| defaultPosition | Default toast position. | string | no | iOS/Android | yes |
| messageDefaultDuration | Default duration for the message function. | string | no | iOS/Android | yes |
| messageDefaultPosition | Default position for the message function. | string | no | iOS/Android | yes |

**Toast.ToastView**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | Toast text. | string/number/element | no | iOS/Android | yes |
| icon | Icon (none, success, fail, smile, sad, info, stop). | string/ImageSource/element | no | iOS/Android | yes |
| position | Toast position (top, bottom, center). | string | no | iOS/Android | yes |

### 23. ActionSheet

ActionSheet shows a bottom action sheet.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show the action sheet. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ActionSheetView | Content component for the action sheet. | class | no | iOS/Android | yes |

**ActionSheet.ActionSheetView**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | Array of actions. | array | yes | iOS/Android | yes |
| cancelItem | Cancel button. | object | no | iOS/Android | yes |

**ActionSheet.ActionSheetView Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Action sheet item component. | class | no | iOS/Android | yes |

**ActionSheet.ActionSheetView.Item**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Item type. | string | no | iOS/Android | yes |
| title | Title text. | string/number/element | yes | iOS/Android | yes |
| topSeparator | Top separator (none, full, indent). | string/element | no | iOS/Android | yes |
| bottomSeparator | Bottom separator (none, full, indent). | string/element | no | iOS/Android | yes |
| disabled | Disable the item. | bool | no | iOS/Android | yes |

### 24. ActionPopover

ActionPopover displays an action menu in a bubble.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show the action popover. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ActionPopoverView | Content component for the action popover. | class | yes | iOS/Android | yes |

**ActionPopover.ActionPopoverView**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | Array of action items. | array | yes | iOS/Android | yes |
| direction | Bubble direction (up, down, left, right). | string | no | iOS/Android | yes |
| align | Alignment (start, center, end). | string | no | iOS/Android | yes |
| showArrow | Show arrow. | bool | no | iOS/Android | yes |

**ActionPopover.ActionPopoverView Static Properties**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Action popover item component. | class | yes | iOS/Android | yes |

**ActionPopover.ActionPopoverView.Item Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Item title. | string/number/element | yes | iOS/Android | yes |
| leftSeparator | Show left separator. | bool | no | iOS/Android | yes |
| rightSeparator | Show right separator. | bool | no | iOS/Android | yes |

### 25. PullPicker

PullPicker shows a bottom pull-up selector.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show the picker. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| PullPickerView | Content component for the pull picker. | class | yes | iOS/Android | yes |

**PullPicker.PullPickerView**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | List title. | string | no | iOS/Android | yes |
| items | Available items. | array | yes | iOS/Android | yes |
| selectedIndex | Selected index. | number | no | iOS/Android | yes |
| getItemText | Source of item text. | function | no | iOS/Android | yes |
| onSelected | Callback when an item is selected. | function | no | iOS/Android | yes |

**PullPicker.PullPickerView Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Pull picker item component. | class | no | iOS/Android | yes |

**PullPicker.PullPickerView.Item Properties**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| selected | Selected state. | bool | no | iOS/Android | yes |

### 26. PopoverPicker

PopoverPicker displays a bubble selector.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show the picker. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| PopoverPickerView | Content component for the popover picker. | class | yes | iOS/Android | yes |

**PopoverPicker.PopoverPickerView Properties**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | Options array. | array | yes | iOS/Android | yes |
| selectedIndex | Selected index. | number | no | iOS/Android | yes |
| getItemText | Source of item text. | function | no | iOS/Android | yes |
| shadow | Show shadow. | bool | no | iOS | yes |
| direction | Arrow direction (up, down, left, right). | string | no | iOS/Android | yes |
| align | Alignment (start, center, end). | string | no | iOS/Android | yes |
| showArrow | Show arrow. | bool | no | iOS/Android | yes |
| onSelected | Selection handler. | function | no | iOS/Android | yes |

**PopoverPicker.PopoverPickerView Static Properties**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Popover picker item component. | class | no | iOS/Android | yes |

**PopoverPicker.PopoverPickerView.Item Properties**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| selected | Selected state. | bool | no | iOS/Android | yes |

### 27. Menu

Menu displays a popup menu.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show the menu. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| MenuView | Content component for the menu. | class | no | iOS/Android | yes |

**Menu.MenuView Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | Menu items. | array | no | iOS/Android | yes |
| shadow | Show shadow. | bool | no | iOS | yes |
| direction | Arrow direction (up, down, left, right). | string | no | iOS/Android | yes |
| align | Alignment (start, center, end). | string | no | iOS/Android | yes |
| showArrow | Show arrow. | bool | no | iOS/Android | yes |

**Menu.MenuView Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Menu item component. | class | no | iOS/Android | yes |

**Menu.MenuView.Item Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Item title. | string/number/element | no | iOS/Android | yes |
| icon | Icon content. | element/ImageSource | no | iOS/Android | yes |

### 28. Drawer

Drawer provides a side drawer.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| open | Open the drawer. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| DrawerView | Content component for the drawer. | class | no | iOS/Android | yes |

**Drawer.DrawerView Properties**

DrawerView inherits all properties and events from Overlay.PullView.

### 29. ModalIndicator

ModalIndicator displays a modal loading indicator.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show the indicator. | function | yes | iOS/Android | yes |
| hide | Hide the indicator. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| IndicatorView | Content component for the modal indicator. | class | no | iOS/Android | yes |

**ModalIndicator.IndicatorView Parameters:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | Message text. | string/number/element | no | iOS/Android | yes |
| position | Display position. | string | no | iOS/Android | yes |
| size | Indicator size. | string | no | iOS/Android | yes |
| color | Indicator color. | string | no | iOS/Android | yes |

### 30. TeaNavigator

TeaNavigator is the root navigator component.

**Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| rootView | Root component. | element | yes | iOS/Android | yes |

**Context:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| navigator | Return the navigator component. | function | yes | iOS/Android | yes |

### 31. BasePage

BasePage is the base page component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| scene | Transition effects. | object | no | iOS/Android | yes |
| autoKeyboardInsets | Auto-adjust for keyboard. | bool | no | iOS/Android | yes |
| keyboardTopInsets | Keyboard top inset. | number | no | iOS/Android | yes |

For the **autoKeyboardInsets** property, **the soft keyboard on HarmonyOS automatically avoids input fields by default**. If you want to disable the system’s default soft keyboard avoidance behavior, refer to [Soft Keyboard Layout Adaptation](https://developer.huawei.com/consumer/en/doc/best-practices/bpta-keyboard-layout-adapt#section15829951124116) or follow the steps below:

- Add the following configuration in harmony/entry/src/main/ets/pages/Index.ets:
```diff
...
+ import { KeyboardAvoidMode } from '@kit.ArkUI';
...

  aboutToAppear() {
    ...
+   this.getUIContext().setKeyboardAvoidMode(KeyboardAvoidMode.NONE);
    ...
  }
```

**Variables:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| navigator | Navigator object. | object | yes | iOS/Android | yes |
| didMount | Whether the page mounted. | bool | yes | iOS/Android | yes |
| isFocused | Whether the page is focused. | bool | yes | iOS/Android | yes |

**Lifecycle Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onWillFocus | Triggered before the page gains focus. | function | no | iOS/Android | yes |
| onDidFocus | Triggered after the page gains focus. | function | no | iOS/Android | yes |
| onHardwareBackPress | Hardware back button handler. | function | no | Android/Harmony | yes |
| renderPage | Render function for the page. | function | yes | iOS/Android | yes |

### 32. NavigationPage

NavigationPage extends BasePage and includes a navigation bar.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Navigation bar title. | string | no | iOS/Android | yes |
| showBackButton | Show the back button. | bool | no | iOS/Android | yes |
| navigationBarInsets | Reserve space for the navigation bar. | bool | no | iOS/Android | yes |
| scene | Transition effects. | object | no | iOS/Android | yes |

**Overridable Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| renderNavigationTitle | Render the navigation bar title. | function | no | iOS/Android | yes |
| renderNavigationLeftView | Render the left view of the navigation bar. | function | no | iOS/Android | yes |
| renderNavigationRightView | Render the right view of the navigation bar. | function | no | iOS/Android | yes |
| renderNavigationBar | Render the navigation bar. | function | no | iOS/Android | yes |

## Known Issues


## Others


## License

This project is based on [The MIT License (MIT)](https://github.com/react-native-oh-library/teaset/blob/master/LICENSE). Feel free to enjoy and contribute to open source.
