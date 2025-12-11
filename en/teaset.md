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

Theme is the component style definition object for Teaset, used to define the default styles for Teaset components.

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

Label component is used for text display, generally for a small amount of single-line text.

- Label component inherits all properties of **[Text](https://reactnative.dev/docs/text.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Label type (default, title, detail, danger). | string | no | iOS/Android | yes |
| size | Display size (xl, lg, md, sm, xs). | string | no | iOS/Android | yes |
| text | Text content. | string/number | no | iOS/Android | yes |
| numberOfLines | Number of display lines (Inherited from Text component and modified default value). | number | no | iOS/Android | yes |

### 3. Button

Button component defines a button that is visible, touchable, and has touch feedback.

- Button component inherits all properties and events of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Button type (default, primary, secondary, danger, link). | string | no | iOS/Android | yes |
| size | Display size (xl, lg, md, sm, xs). | string | no | iOS/Android | yes |
| title | Button title. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title (Invalid when title type is element). | style | no | iOS/Android | yes |
| disabled | Disable the button (When true, the component is displayed as semi-transparent and not touchable). | bool | no | iOS/Android | yes |
| onPress | Press handler. | function | no | iOS/Android | yes |

### 4. Checkbox

Checkbox component defines a checkbox with two states: checked and unchecked.

- Checkbox component inherits all properties and events of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| checked | Whether the checkbox is selected. | bool | no | iOS/Android | yes |
| defaultChecked | Default selection state. | bool | no | iOS/Android | yes |
| size | Display size (lg, md, sm). | string | no | iOS/Android | yes |
| title | Title text. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title (Invalid when title type is element). | style | no | iOS/Android | yes |
| checkedIcon | Custom icon for the checked state. | element | no | iOS/Android | yes |
| checkedIconStyle | Style for the checked icon. | ImageStyle | no | iOS/Android | yes |
| uncheckedIcon | Custom icon for the unchecked state. | element | no | iOS/Android | yes |
| uncheckedIconStyle | Style for the unchecked icon. | ImageStyle | no | iOS/Android | yes |
| disabled | Disable the checkbox (Inherited from TouchableOpacity, when true, the component is displayed as semi-transparent and not touchable). | bool | no | iOS/Android | yes |
| hitSlop | Extend the touchable area (Inherited from TouchableOpacity and modified default value). | object | no | iOS/Android | yes |
| onChange | State change handler. | function | no | iOS/Android | yes |

### 5. Input

Input component defines an input edit box.

- Input component inherits all properties and events of **[TextInput](https://reactnative.dev/docs/textinput.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| size | Display size (xl, lg, md, sm). | string | no | iOS/Android | yes |
| disabled | Disable the input (When true, the component is displayed as semi-transparent and not focusable). | bool | no | iOS/Android | yes |
| underlineColorAndroid | Underline color on Android (Inherited from TextInput and modified default value). | string/'rgba(0, 0, 0, 0)' | no | Android | yes |
| onChangeText | Text change handler. | function | no | iOS/Android | yes |

### 6. Select

Select component defines a selection box.

- Select component inherits all properties of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| size | Display size (xl, lg, md, sm). | string | no | iOS/Android | yes |
| value | Selected value. | any | no | iOS/Android | yes |
| valueStyle | Style for the selected text. | style | no | iOS/Android | yes |
| items | Items in the dropdown. | array | no | iOS/Android | yes |
| getItemValue | Function to retrieve item value (Get the value of the items array element, passed parameters are (item, index), item = items[index], default uses item directly). | function | no | iOS/Android | yes |
| getItemText | Function to retrieve item label (Get the display text or React Native component of the items array element, passed parameters are (item, index), item = items[index], default uses item directly). | function | no | iOS/Android | yes |
| pickerType | Picker type (auto, pull, popover). | string | no | iOS/Android | yes |
| pickerTitle | PullPicker title. | string | no | iOS/Android | yes |
| editable | Whether the value is editable. | bool | no | iOS/Android | yes |
| icon | Right-side indicator icon (none: no icon, default: default icon). | string/ImageSource/element | no | iOS/Android | yes |
| iconTintColor | Icon tint color. | string | no | iOS/Android | yes |
| placeholder | Placeholder text. | string | no | iOS/Android | yes |
| placeholderTextColor | Placeholder text color (Displayed when value is empty). | string | no | iOS/Android | yes |
| disabled | Disable the select. | bool | no | iOS/Android | yes |
| onSelected | Selection handler (Called when an item in the items array is selected, item = items[index]). | function | no | iOS/Android | yes |

### 7. Stepper

Stepper component defines a stepper.

- Stepper component inherits all properties and events of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| defaultValue | Default value (Used only once when the component is initialized. If you do not want to pass value and listen to onChange to maintain state synchronization, you can use defaultValue instead). | number | no | iOS/Android | yes |
| value | Current value. | number | no | iOS/Android | yes |
| step | Step size (Integer or decimal). | number | no | iOS/Android | yes |
| max | Maximum value (No limit by default). | number | no | iOS/Android | yes |
| min | Minimum value (No limit by default). | number | no | iOS/Android | yes |
| valueStyle | Style for the value display. | style | no | iOS/Android | yes |
| valueFormat | Value formatting function (Passed parameter is value, default uses value directly). | function | no | iOS/Android | yes |
| subButton | "Minus" button. | string/element | no | iOS/Android | yes |
| addButton | "Plus" button. | string/element | no | iOS/Android | yes |
| showSeparator | Show separators (Set to false if you need to fully customize the component style). | bool | no | iOS/Android | yes |
| disabled | Disable the stepper (When true, the component is displayed as semi-transparent and not touchable). | bool | no | iOS/Android | yes |
| editable | Allow text editing. | bool | no | iOS/Android | yes |
| onChange | Value change handler (Called when the value changes). | function | no | iOS/Android | yes |

### 8. SearchInput

SearchInput component defines a search input box. The difference from Input is that it has a magnifying glass icon, which is displayed in the center when the content is empty and not in the editing state, otherwise it is left-aligned.

- SearchInput component inherits all properties and events of **[TextInput](https://reactnative.dev/docs/textinput.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Component style (Style of the component's container View). | ViewStyle | no | iOS/Android | yes |
| inputStyle | Style for the input field. | style | no | iOS/Android | yes |
| iconSize | Magnifying glass icon size (Default value is set in Theme). | number | no | iOS/Android | yes |
| disabled | Disable the input (When true, the component is displayed as semi-transparent and not touchable). | bool | no | iOS/Android | yes |
| underlineColorAndroid | Underline color on Android (Inherited from TextInput and modified default value). | string/'rgba(0, 0, 0, 0)' | no | Android | yes |
| onChangeText|  Text change handler | function | no | iOS/Android | yes |

### 9. Badge

Badge component defines a badge, which can be used to display numbers, letters, dots, etc. on the corner of an icon, or to display other content.

- Badge component inherits all properties of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Badge type (capsule, square, dot). | string | no | iOS/Android | yes |
| count | Badge display number. | string/number | no | iOS/Android | yes |
| countStyle | Style for the badge display number. | style | no | iOS/Android | yes |
| maxCount | Maximum display number (When count is greater than this value, it is displayed as maxCount followed by a plus sign, e.g., '99+'. Invalid when count is not a number). | number | no | iOS/Android | yes |

### 10. Popover

Popover component defines a popover, which is a rounded rectangular container with a triangular arrow that can be displayed at any position on the border, commonly used for chat message display or pop-up prompts.

- Popover component inherits all properties of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| arrow | Arrow position (none, topLeft, top, topRight, rightTop, right, rightBottom, bottomRight, bottom, bottomLeft, leftBottom, left, leftTop). | string | no | iOS/Android | yes |
| paddingCorner | Distance between the triangular arrow and the corner (Related to the arrow value, e.g., when arrow = 'topLeft', it represents the distance between the triangular arrow and the top left corner. Default value is set in Theme). | number | no | iOS/Android | yes |

### 11. NavigationBar

NavigationBar component defines a page navigation bar, used to display the page title and buttons at the top of the page.

- NavigationBar component inherits all properties of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Navigation bar style type (auto, ios, android, harmony). | string | no | iOS/Android | yes |
| title | Navigation bar title (Rendered using <NavigationBar.Title /> component when passing a string). | string/element | no | iOS/Android | yes |
| titleStyle | Style for the navigation bar title (Invalid when title type is element). | style | no | iOS/Android | yes |
| leftView | Navigation bar left view. | element | no | iOS/Android | yes |
| rightView | Navigation bar right view. | element | no | iOS/Android | yes |
| tintColor | Text and image color for left and right views of the navigation bar (Default value is set in Theme). | string | no | iOS/Android | yes |
| background | Navigation bar background view. | element | no | iOS/Android | yes |
| hidden | Whether to hide the navigation bar. | bool | no | iOS/Android | yes |
| animated | Whether to have animation effect when showing/hiding navigation bar and status bar. | bool | no | iOS/Android | yes |
| statusBarStyle | System status bar style (default, light-content, dark-content). | string | no | iOS/Android | yes |
| statusBarColor | Navigation bar background color (Default value is set in Theme). | string | no | iOS/Android | yes |
| statusBarHidden | Whether to hide the system status bar. | bool | no | iOS/Android | yes |
| statusBarInsets | Whether to automatically add status bar placeholder space. | bool | no | iOS | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Title | Navigation bar title component. | class | no | iOS/Android | yes |
| Button | Navigation bar button component. | class | no | iOS/Android | yes |
| LinkButton | Navigation bar link button component, inherits from NavigationBar.Button. | class | no | iOS/Android | yes |
| IconButton | Navigation bar icon button component, inherits from NavigationBar.Button. | class | no | iOS/Android | yes |
| BackButton | Navigation bar back button component, inherits from NavigationBar.Button. | class | no | iOS/Android | yes |

**NavigationBar.Title**

- NavigationBar.Title component inherits all properties of **[Text](https://reactnative.dev/docs/text.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | Display text. | string/number | no | iOS/Android | yes |
| numberOfLines | Number of lines (Inherited from Text component and modified default value). | number | no | iOS/Android | yes |
| allowFontScaling | Allow system font scaling (Inherited from Text component and modified default value). | bool | no | iOS | yes |

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

- NavigationBar.Button component inherits all properties of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| hitSlop | Extend the touchable area (Inherited from TouchableOpacity component and modified default value). | object | no | iOS/Android | yes |

**NavigationBar.LinkButton**

- NavigationBar.LinkButton component inherits all properties of **[NavigationBar.Button](#navigationbar-button-props)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Button title | string/number | no | iOS/Android | yes |

**NavigationBar.IconButton**

- NavigationBar.IconButton component inherits all properties of **[NavigationBar.Button](#navigationbar-button-props)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| icon | Button icon | ImageSource | no | iOS/Android | yes |

**NavigationBar.BackButton**

- NavigationBar.BackButton component inherits all properties of **[NavigationBar.Button](#navigationbar-button-props)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title text (Default value is set in Theme). | string/number | no | iOS/Android | yes |
| icon | Button icon. | ImageSource | no | iOS/Android | yes |

<a id="listrow"></a>
### 12. ListRow

ListRow component is used to display a list row, defining a series of easy-to-use element properties, making it possible to quickly develop applications based on ListView and ScrollView.

- ListRow component inherits all properties and events of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| detail | Detail content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title (Invalid when title type is element). | style | no | iOS/Android | yes |
| detailStyle | Style for the detail text (Invalid when detail type is element). | style | no | iOS/Android | yes |
| detailMultiLine | Allow multiline detail text (Default is true when titlePlace = 'top', otherwise false). | bool | no | iOS/Android | yes |
| icon | Left icon. | element/ImageSource | no | iOS/Android | yes |
| accessory | Right indicator icon (**none**: None;<br/>**auto**: Automatic, 'indicator' when onPress property is set, otherwise 'none';<br/>**empty**: Empty, does not display indicator icon, but occupies the space of 'check' or 'indicator';<br/>**check**: Check icon, generally used to indicate that the row is selected;<br/>**indicator**: Greater than sign icon, generally used to indicate clicking this row to open a new page;). | string/element/ImageSource | no | iOS/Android | yes |
| topSeparator | Top separator (none, full, indent) (Indent separator only indents on the left). | string/element | no | iOS/Android | yes |
| bottomSeparator | Bottom separator (none, full, indent) (Indent separator only indents on the left). | string/element | no | iOS/Android | yes |
| titlePlace | Title position (left, top, none). | string | no | iOS/Android | yes |
| swipeActions | List of action buttons displayed when swiping left (Recommended to use ListRow.SwipeActionButton component). | array | no | iOS/Android | yes |
| activeOpacity | Opacity on press (Inherited from TouchableOpacity and modified default value, default is 0.2 when onPress is passed, otherwise 1). | number | no | iOS/Android | yes |
| onPress | Press handler. | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| SwipeActionButton | Swipe action button component. | class | no | iOS/Android | yes |

**ListRow.SwipeActionButton**

- SwipeActionButton component inherits all properties of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Display style type (default, danger). | string | no | iOS/Android | yes |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title (Invalid when title type is element). | style | no | iOS/Android | yes |

### 13. Carousel

Carousel component defines a carousel component, generally used for image or information page rotation, and can also be used for content pagination display.

- Carousel component inherits all properties and events of **[ScrollView](https://reactnative.dev/docs/scrollview.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| carousel | Whether to enable carousel (When false, stop carousel, you can call scrollToPage or scrollToNextPage method to scroll to the page). | bool | no | iOS/Android | yes |
| interval | Interval time per page (Unit is milliseconds, valid when carousel = true). | number | no | iOS/Android | yes |
| direction | Play direction (Valid when carousel = true) <br/>**forward**: Forward carousel, page scrolls from right to left;<br/>**backward**: Backward carousel, page scrolls from left to right. | string | no | iOS/Android | yes |
| startIndex | Initial page index. | number | no | iOS/Android | yes |
| cycle | Whether to loop playback (Valid when carousel = true). | bool | no | iOS/Android | yes |
| control | Page indicator (When true, display default page controller, you can also pass custom page controller, recommended to use Carousel.Control component). | bool/element | no | iOS/Android | yes |
| horizontal | Horizontal scrolling (Inherited from ScrollView and modified default value). | bool | no | iOS/Android | yes |
| pagingEnabled | Enable paging (Inherited from ScrollView and modified default value). | bool | no | iOS/Android | yes |
| showsHorizontalScrollIndicator | Show horizontal scroll indicator (Inherited from ScrollView and modified default value). | bool | no | iOS/Android | yes |
| showsVerticalScrollIndicator | Show vertical scroll indicator (Inherited from ScrollView and modified default value). | bool | no | iOS/Android | yes |
| alwaysBounceHorizontal | Always allow horizontal bounce (Inherited from ScrollView and modified default value). | bool | no | iOS/Android | yes |
| alwaysBounceVertical | Always allow vertical bounce (Inherited from ScrollView and modified default value). | bool | no | iOS/Android | yes |
| bounces | Enable bounce effect (Inherited from ScrollView and modified default value). | bool | no | iOS/Android | yes |
| automaticallyAdjustContentInsets | Auto-adjust content insets (Inherited from ScrollView and modified default value). | bool | no | iOS/Android | yes |
| scrollEventThrottle | Scroll event throttle interval (Inherited from ScrollView and modified default value). | number | no | iOS/Android | yes |
| onChange | Page change handler. | function | no | iOS/Android | yes |
| scrollToPage | Scroll to a specific page. | function | no | iOS/Android | yes |
| scrollToNextPage | Scroll to the next page. | function | no | iOS/Android | yes |

**Carousel.Control Component:**

- Carousel.Control component inherits all properties of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| dot | Page indicator dot element. | element | no | iOS/Android | yes |
| activeDot | Active page indicator element. | element | no | iOS/Android | yes |

### 14. Projector

Projector component defines a projector component, which is a multi-page display component that automatically maintains state and has view caching function. Switching pages is like switching projector films, the content and state of the original page will not disappear, and it will be presented as is when switching back to this page without re-rendering.

- Projector component inherits all properties of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| index | Current film (page) index. | number | no | iOS/Android | yes |
| slideStyle | Film (page) style. | ViewStyle | no | iOS/Android | yes |

### 15. SegmentedBar

SegmentedBar component defines a segmented toolbar component, which can be used with <Carousel /> or <Projector /> to achieve segmented display of multiple contents on the same page.

- SegmentedBar component inherits all properties and events of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| justifyItem | Item layout mode. (<br/>**fixed**: Fixed position equal width arrangement;<br/>**scrollable**: Scrollable, use this mode when there are many Items and they cannot be displayed on one screen). | string | no | iOS/Android | yes |
| indicatorType | Active indicator type. (<br/>**none**: None<br/>**boxWidth**: Equal division interval width<br/>**itemWidth**: Item content width<br/>**customWidth**: Specified width). | string | no | iOS/Android | yes |
| indicatorPosition | Active indicator position (top, bottom). | string | no | iOS/Android | yes |
| indicatorLineColor | Indicator line color (Default value is set in Theme). | string | no | iOS/Android | yes |
| indicatorLineWidth | Indicator line height (Default value is set in Theme). | number | no | iOS/Android | yes |
| indicatorWidth | Active indicator line width (Effective when indicatorType is customWidth). | number | no | iOS/Android | yes |
| indicatorPositionPadding | Distance between active indicator and top or bottom border (Default value is set in Theme). | number | no | iOS/Android | yes |
| animated | Whether there is animation effect when changing active Item. | bool | no | iOS/Android | yes |
| autoScroll | Whether to automatically scroll active Item to the center of the container (Valid only when justifyItem is 'scrollable'). | bool | no | iOS/Android | yes |
| activeIndex | Active Item index. | number | no | iOS/Android | yes |
| onChange | Selection change handler. | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | SegmentedBar item component. | class | no | iOS/Android | yes |

**SegmentedBar.Item Properties:**

- SegmentedBar.Item component inherits all properties of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title (Invalid when title type is element). | style | no | iOS/Android | yes |
| activeTitleStyle | Style for the active title (Invalid when title type is element). | style | no | iOS/Android | yes |
| badge | Badge content (Rendered using `<Badge />` component when it is string or number). | string/number/element | no | iOS/Android | yes |
| active | Whether the item is active. | bool | no | iOS/Android | yes |

### 16. SegmentedView

SegmentedView component defines a segmented container component, generally used for segmented display of multiple contents on the same page.<br/>SegmentedView component is an easy-to-use encapsulated composite component of `<SegmentedBar />`, `<Projector />` / `<Carousel />`.

- SegmentedView component inherits all properties and events of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | SegmentedView type. (<br/>**projector**: Projector, content page is rendered using `<Projector />` component<br/>**carousel**: Carousel, content page is rendered using `<Carousel />` component). | string | no | iOS/Android | yes |
| barPosition | Segmented toolbar position (top, bottom). | string | no | iOS/Android | yes |
| barStyle | Segmented toolbar style. | style | no | iOS/Android | yes |
| justifyItem | Item layout mode. (<br/>**fixed**: Fixed position equal width arrangement;<br/>**scrollable**: Scrollable, use this mode when there are many Items and they cannot be displayed on one screen). | string | no | iOS/Android | yes |
| indicatorType | Segmented toolbar active indicator type. (<br/>**none**: None<br/>**boxWidth**: Equal division interval width<br/>**itemWidth**: Item content width). | string | no | iOS/Android | yes |
| indicatorPosition | Segmented toolbar active indicator position (top, bottom). | string | no | iOS/Android | yes |
| indicatorLineColor | Active indicator color (Default value is set in Theme). | string | no | iOS/Android | yes |
| indicatorLineWidth | Active indicator line width (Default value is set in Theme). | number | no | iOS/Android | yes |
| indicatorPositionPadding | Distance between active indicator and top or bottom border (Default value is set in Theme). | number | no | iOS/Android | yes |
| animated | Whether there is animation effect when changing active Item in segmented toolbar. | bool | no | iOS/Android | yes |
| autoScroll | Whether to automatically scroll active Item to the center of the container in segmented toolbar (Valid only when justifyItem is 'scrollable'). | bool | no | iOS/Android | yes |
| activeIndex | Segmented toolbar active Item index. | number | no | iOS/Android | yes |
| onChange | Page change handler. | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Sheet | SegmentedView sheet component. | class | no | iOS/Android | yes |

**SegmentedView.Sheet Properties:**

- SegmentedView.Sheet component inherits all properties of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title (Invalid when title type is element). | style | no | iOS/Android | yes |
| activeTitleStyle | Style for the active title (Invalid when title type is element). | style | no | iOS/Android | yes |
| badge | Badge content (Rendered using `<Badge />` component when it is string or number). | string/number/element | no | iOS/Android | yes |

### 17. TabView

TabView component defines a tab page component, used to display multiple sub-pages on one page, switching sub-pages through the TabBar at the bottom of the page.

- TabView component inherits all properties and events of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Tab page type. (<br/>**projector**: Projector, sub-page is rendered using `<Projector />` component<br/>**carousel**: Carousel, sub-page is rendered using `<Carousel />` component). | string | no | iOS/Android | yes |
| barStyle | TabBar toolbar style. | style | no | iOS/Android | yes |
| activeIndex | Active Sheet index. | number | no | iOS/Android | yes |
| onChange | Page change handler (Called when changing the current page, index is the current Sheet index). | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Sheet | Tab page Sheet component. | class | no | iOS/Android | yes |
| Button | Tab page button component (This component is automatically rendered by the Sheet component, no need to explicitly declare in code, but you can modify TabView.Button to a custom class to change the tab page button component). | class | no | iOS/Android | yes |

**TabView.Sheet Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Sheet type (sheet, button). | string | no | iOS/Android | yes |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| icon | Active state button icon. | ImageSource/element | no | iOS/Android | yes |
| activeIcon | Active icon content. | ImageSource/element | no | iOS/Android | yes |
| badge | Badge content (Rendered using `<Badge />` component when it is string or number). | string/number/element | no | iOS/Android | yes |
| onPress | Press handler. | function | no | iOS/Android | yes |

**TabView.Button Properties:**

- TabView.Button component inherits all properties of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| titleStyle | Style for the title (Invalid when title type is element). | style | no | iOS/Android | yes |
| activeTitleStyle | Style for the active title (Invalid when title type is element). | style | no | iOS/Android | yes |
| icon | Button icon. | ImageSource/element | no | iOS/Android | yes |
| activeIcon | Active state button icon. | ImageSource/element | no | iOS/Android | yes |
| badge | Badge content (Rendered using `<Badge />` component when it is string or number). | string/number/element | no | iOS/Android | yes |
| active | Active state. | bool | no | iOS/Android | yes |

### 18. TransformView

TransformView component defines a transformable view, supporting pinch-to-zoom and single-finger pan gestures.

- TransformView component inherits all properties and events of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| containerStyle | Internal container style. | style | no | iOS/Android | yes |
| maxScale | Maximum zoom scale. | number | no | iOS/Android | yes |
| minScale | Minimum zoom scale. | number | no | iOS/Android | yes |
| magnetic | Magnetic edges (Automatically zoom in to view size when the size after zooming is smaller than the view size). | bool | no | iOS/Android | yes |
| tension | Drag tension coefficient (Resistance effect when dragging the image edge inside the view). | number | no | iOS/Android | yes |
| onWillTransform | Transform starts (Three parameters are x coordinate, y coordinate, zoom scale). | function | no | iOS/Android | yes |
| onTransforming | Transform in progress (Three parameters are x coordinate, y coordinate, zoom scale). | function | no | iOS/Android | yes |
| onDidTransform | Transform ends (Three parameters are x coordinate, y coordinate, zoom scale). | function | no | iOS/Android | yes |
| onWillMagnetic | Called before magnetic border effect starts (Return true to allow magnetic border effect, otherwise prevent it, valid when magnetic = true). | function | no | iOS/Android | yes |
| onDidMagnetic | Called when magnetic border effect ends (Three parameters are x coordinate, y coordinate, zoom scale). | function | no | iOS/Android | yes |
| onPress | Click event (Called when touch ends, consistent with TouchableOpacity.onPress). | function | no | iOS/Android | yes |
| onLongPress | Long press event (Called when pressing the component for more than 500ms, consistent with TouchableOpacity.onLongPress). | function | no | iOS/Android | yes |

### 19. AlbumView

AlbumView component defines an album view, supporting multi-image left-right switching display, pinch-to-zoom, and single-finger pan gestures.

- AlbumView component inherits all properties and events of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| images | Album image array (Array elements are ImageSource or React Native components). | array | yes | iOS/Android | yes |
| thumbs | Album thumbnail array (Array elements are ImageSource). | array | no | iOS/Android | yes |
| index | Display image index (Setting this property requires listening to onChange event and maintaining state yourself). | number | no | iOS/Android | yes |
| defaultIndex | Default display image index. | number | no | iOS/Android | yes |
| maxScale | Maximum zoom scale. | number | no | iOS/Android | yes |
| space | Spacing between album images. | number | no | iOS/Android | yes |
| control | Page controller (When true, display default page controller, you can also pass custom page controller, recommended to use Carousel.Control component). | element | no | iOS/Android | yes |
| onWillChange | Called before changing the current page (index is the current page index value, newIndex is the page index value to be changed). | function | no | iOS/Android | yes |
| onChange | Called after changing the current page (index is the changed page index value, oldIndex is the page index value before change). | function | no | iOS/Android | yes |
| onPress | Click event (Called when touch ends). | function | no | iOS/Android | yes |
| onLongPress | Long press event (Called when pressing the component for more than 500ms). | function | no | iOS/Android | yes |
| onWillLoadImage | Called before loading image. | function | no | iOS/Android | yes |
| onLoadImageSuccess | Called when image loads successfully. | function | no | iOS/Android | yes |
| onLoadImageFailure | Called when image fails to load. | function | no | iOS/Android | yes |

### 20. Wheel

Wheel component defines a wheel, which can be used for wheel-style selectors.

- Wheel component inherits all properties and events of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | Options list (Array elements can be strings, numbers, or React Native components). | array | yes | iOS/Android | yes |
| itemStyle | Style for items (Invalid when items array elements are React Native components). | style | no | iOS/Android | yes |
| holeStyle | Style for the active window (Need to specify height property). | style | no | iOS/Android | yes |
| maskStyle | Style for the masking areas (top and bottom). | style | no | iOS/Android | yes |
| holeLine | Divider for the active window. | number/element | no | iOS/Android | yes |
| index | Current index (Setting this property requires listening to onChange event and maintaining state yourself). | number | no | iOS/Android | yes |
| defaultIndex | Default current item index value (Used only once when the component is created. If you do not want to set index and maintain state, you can pass the initial item index value in this property). | number | no | iOS/Android | yes |
| onChange | Called after changing the current item (index is the changed current item index value). | function | no | iOS/Android | yes |

<a id="overlay"></a>
### 21. Overlay

Overlay is a static class for floating layers, which is a very important part of Teaset.

Generally speaking, the content display page is a two-dimensional plane structure. There are some auxiliary UI interfaces, such as menus, prompt boxes, selection list boxes, etc., which are not part of the main content, but are indispensable. A lot of time needs to be invested in developing this part of the code during development, and this part of the code will be mixed with the code of the main content, increasing the complexity of code maintenance.

Overlay makes React Native development change from two-dimensional to three-dimensional. You can cover any layer of floating layers on the page, and the floating layer interface uses function methods to activate display. You can completely separate the floating layer code from the JSX of the page main content.

In addition, Overlay supports a variety of animation effects, such as fade in and fade out, pop up, drawer effect, etc., making your interaction vivid.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show an overlay view (Input parameter overlayView is the overlay view, recommended to use Overlay.View component, returns a unique overlay key value). | function | yes | iOS/Android | yes |
| hide | Hide an overlay view (Input parameter key is the overlay key value). | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| View | Overlay view component (Components passed to Overlay.show function should be Overlay.View component or components inherited from Overlay.View. Overlay.View is the root component of the overlay, you can display any content on it). | class | yes | iOS/Android | yes |
| PullView | Overlay with pull effect (Inherits from Overlay.View, has a drawer-like pull effect). | class | no | iOS/Android | yes |
| PopView | Overlay with pop effect (Inherits from Overlay.View). | class | no | iOS/Android | yes |
| PopoverView | Overlay with popover effect (Inherits from Overlay.View). | class | no | iOS/Android | yes |

<a id="overlay-view"></a>
**Overlay.View**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Overlay style. | style | no | iOS/Android | yes |
| modal | Whether it is a modal overlay (Non-modal overlay can be closed by clicking the translucent area outside the content, modal overlay needs to be closed manually by code). | bool | no | iOS/Android | yes |
| animated | Whether to support animation effect. | bool | no | iOS/Android | yes |
| overlayOpacity | Overlay non-content area opacity (Value from 0 to 1, opacity from fully transparent to opaque. Default value is set in Theme). | number | no | iOS/Android | yes |
| overlayPointerEvents | Background pointer events (auto, none). | string | no | iOS/Android | yes |
| autoKeyboardInsets | Whether to automatically reduce keyboard height space when keyboard pops up. | bool | no | iOS/Android | yes |
| onAppearCompleted | Called when the overlay display is complete. | function | no | iOS/Android | yes |
| onDisappearCompleted | Called after the overlay is hidden. | function | no | iOS/Android | yes |
| onCloseRequest | Overlay close request event (Called when clicking the translucent area outside the content, if this value is set, modal will be invalid). | function | no | iOS/Android | yes |

<a id="overlay-pullview"></a>
**Overlay.PullView**

- Overlay.PullView component inherits all properties and events of **[Overlay.View](#overlay-view)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| side | Drawer popup direction (top, bottom, left, right). | string | no | iOS/Android | yes |
| containerStyle | Drawer container style. | style | no | iOS/Android | yes |
| rootTransform | Root component transform animation when overlay pops up (<br/>**none**: No transform<br/>**translate**: Displacement transform, move the root component in the direction of overlay popup<br/>**scale**: Scale transform, scale factor is defined in Theme<br/>**Transform** currently supports translateX, translateY, scaleX, scaleY, type definition:<br/>type Transform {<br/>&ensp;&ensp;translateX: number,<br/>&ensp;&ensp;translateY: number,<br/>&ensp;&ensp;scaleX: number,<br/>&ensp;&ensp;scaleY: number,<br/>}<br/>). | string/array | no | iOS/Android | yes |
| animated | Whether to support animation effect (Inherited from Overlay.View and modified default property). | style | no | iOS/Android | yes |

**Overlay.PopView**

- Overlay.PopView component inherits all properties and events of **[Overlay.View](#overlay-view)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Popup effect. (<br/>**zoomOut**: Zoom out, popup box zooms in and then animates to original size<br/>**zoomIn**: Zoom in, popup box zooms out and then animates to original size<br/>**custom**: Custom, popup box animates from customBounds position and size to original size). | string | no | iOS/Android | yes |
| containerStyle | Popup box container style. | style | no | iOS/Android | yes |
| customBounds | Popup box animation transition start position and size (Valid when type = 'custom'.<br/>type Rect {<br/>&ensp;&ensp;x: number,<br/>&ensp;&ensp;y: number,<br/>&ensp;&ensp;width: number,<br/>&ensp;&ensp;height: number,<br/>}). | object | no | iOS/Android | yes |
| animated | Whether to support animation effect (Inherited from Overlay.View and modified default property). | style | no | iOS/Android | yes |

<a id="overlay-popoverview"></a>
**Overlay.PopoverView**

Overlay.PopoverView component inherits all properties and events of **[Overlay.View](#overlay-view)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| popoverStyle | Popover style. | style | no | iOS/Android | yes |
| fromBounds | Popup bubble source component bounds, the bubble arrow will point to this component.<br/>type Rect {<br/>&ensp;&ensp;x: number,<br/>&ensp;&ensp;y: number,<br/>&ensp;&ensp;width: number,<br/>&ensp;&ensp;height: number,<br/>} | object | yes | iOS/Android | yes |
| direction | Arrow direction (up, down, left, right). | string | no | iOS/Android | yes |
| autoDirection | Whether to automatically adjust popup direction (When true, if there is not enough screen space in the popup direction, it will pop up in the opposite direction. For example, when direction = 'down', if there is not enough space below fromBounds, it will pop up above.). | bool | no | iOS/Android | yes |
| directionInsets | Distance between bubble and popup component fromBounds. | number | no | iOS/Android | yes |
| align | Alignment of bubble and popup component fromBounds. (<br/>**start**: Start alignment, top or left<br/>**center**: Center alignment<br/>**end**: End alignment, bottom or right). | string | no | iOS/Android | yes |
| alignInsets | Alignment direction offset. | number | no | iOS/Android | yes |
| showArrow | Whether to show bubble arrow. | bool | no | iOS/Android | yes |
| paddingCorner | Distance between arrow and alignment corner (Default value is set in Theme). | number | no | iOS/Android | yes |
| overlayOpacity | Bubble opacity (Inherited from Overlay.View and modified default value). | number | no | iOS/Android | yes |

### 22. Toast

Toast is a static class for lightweight notifications, similar to Android's Toast.
Toast is implemented based on [Overlay](#overlay){}.

- Toast inherits all static methods of **[Overlay](#overlay)**.

**Static Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show a toast, overrides the function of the same name in Overlay{}, input parameter options is a collection of duration and [ToastView](#toasttoastview--props) properties, returns a unique overlay key value.<br/>**Generally not called directly** | function | no | iOS/Android | yes |
| message | Show a plain text toast message. (<br/>duration defaults to 'short', position defaults to 'bottom'.<br/>Default values can be modified via Toast.messageDefaultDuration, Toast.messageDefaultPosition). | function | no | iOS/Android | yes |
| success | Show a success toast, with a check icon in the prompt box. (<br/>duration defaults to 'short', position defaults to 'center'.<br/>Default values can be modified via Toast.defaultDuration, Toast.defaultPosition)<br/>**Same below** | function | no | iOS/Android | yes |
| fail | Show a failure toast, with a cross icon in the prompt box. | function | no | iOS/Android | yes |
| smile | Show a smile toast, with a smile face icon in the prompt box. | function | no | iOS/Android | yes |
| sad | Show a sad toast, with a sad face icon in the prompt box. | function | no | iOS/Android | yes |
| info | Show an info toast, with an Info icon in the prompt box. | function | no | iOS/Android | yes |
| stop | Show a stop toast, with a stop icon in the prompt box. | function | no | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|ToastView| Toast content display component | class | yes | iOS/Android | yes |
| defaultDuration | Default value for duration parameter of success, fail, smile, sad, info, stop functions, toast display duration. (<br/>**short**: 2000ms<br/>**long**: 3500ms). | string | no | iOS/Android | yes |
| defaultPosition | Default value for position parameter of success, fail, smile, sad, info, stop functions, toast display position (See [Toast.ToastView](#toasttoastview--props)). | string | no | iOS/Android | yes |
| messageDefaultDuration | Default value for duration parameter of message function. | string | no | iOS/Android | yes |
| messageDefaultPosition | Default value for position parameter of message function. | string | no | iOS/Android | yes |

<a id="toasttoastview--props"></a>
**Toast.ToastView**

- Toast.ToastView component inherits all properties of **[View](https://reactnative.dev/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | Toast text. | string/number/element | no | iOS/Android | yes |
| icon | Icon (<br/>**none**: No icon<br/>**success**: Success, check icon<br/>**fail**: Failure, cross icon<br/>**smile**: Smile face icon<br/>**sad**: Sad face icon<br/>**info**: Info, letter "i" in a circle<br/>**stop**: Stop, exclamation mark "!" in a circle). | string/ImageSource/element | no | iOS/Android | yes |
| position | Toast display position (<br/>**top**: Top of the window<br/>**bottom**: Bottom of the window<br/>**center**: Center of the window<br/>top, bottom positions can be set in Theme). | string | no | iOS/Android | yes |

### 23. ActionSheet

ActionSheet is a static class for action sheets, generally used to trigger a multi-item sub-operation for user selection, presented as a drawer dragged out from the bottom of the screen.
ActionSheet is implemented based on [Overlay](#overlay){}.

**Static Methods:**

- ActionSheet inherits all static methods of **[Overlay](#overlay)**.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show an action sheet, overrides the function of the same name in Overlay{}, input parameter items is the list of action sheet items, cancelItem (nullable) is the cancel action item, options (nullable) is other properties of ActionSheet.ActionSheetView, parameter types see [ActionSheetView](#actionsheetactionsheetview--props).<br/>Returns a unique overlay key value. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ActionSheetView | ActionSheet content display component. | class | no | iOS/Android | yes |

<a id="actionsheetactionsheetview--props"></a>
**ActionSheet.ActionSheetView**

- ActionSheet.ActionSheetView component inherits all properties of **[Overlay.PullView](#overlay-pullview)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | List of action sheet items (Array element type is:<br/>type ActionSheetItem {<br/>&ensp;&ensp;title: string,<br/>&ensp;&ensp;onPress: func,<br/>&ensp;&ensp;disabled: bool,<br/>}). | array | yes | iOS/Android | yes |
| cancelItem | Cancel action item (<br/>type ActionSheetItem {<br/>&ensp;&ensp;title: string,<br/>&ensp;&ensp;onPress: func,<br/>&ensp;&ensp;disabled: bool,<br/>}). | object | no | iOS/Android | yes |

**ActionSheet.ActionSheetView Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Action sheet item component. | class | no | iOS/Android | yes |

**ActionSheet.ActionSheetView.Item**

- ActionSheet.ActionSheetView.Item component inherits all properties of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| type | Item type. | string | no | iOS/Android | yes |
| title | Title text. | string/number/element | yes | iOS/Android | yes |
| topSeparator | Top separator (none, full, indent) (Indent separator only indents on the left). | string/element | no | iOS/Android | yes |
| bottomSeparator | Bottom separator (none, full, indent) (Indent separator only indents on the left). | string/element | no | iOS/Android | yes |
| disabled | Disable the item (Inherited from TouchableOpacity, when true, the component is displayed as semi-transparent and not touchable). | bool | no | iOS/Android | yes |

### 24. ActionPopover

ActionPopover is a static class for action popovers, generally used to trigger a multi-item sub-operation for user selection, presented as a bubble popped up from the trigger source component.
ActionPopover is implemented based on [Overlay](#overlay){}.

**Static Methods:**

- ActionPopover inherits all static methods of **[Overlay](#overlay)**.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show an action popover, overrides the function of the same name in Overlay{}, input parameter fromBounds is the popup bubble source component bounds, items is the list of action items, options (nullable) is other properties of ActionPopover.ActionPopoverView, parameter types see [ActionPopoverView](#actionpopoveractionpopoverview--props).<br/>Returns a unique overlay key value. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ActionPopoverView | ActionPopover content display component. | class | yes | iOS/Android | yes |

<a id="actionpopoveractionpopoverview--props"></a>
**ActionPopover.ActionPopoverView**

- ActionPopover.ActionPopoverView component inherits all properties of **[Overlay.PopoverView](#overlay-popoverview)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | List of action items (Array element type is:<br/>type ActionPopoverItem {<br/>&ensp;&ensp;title: string,<br/>&ensp;&ensp;onPress: func,<br/>}). | array | yes | iOS/Android | yes |
| direction | Bubble direction (up, down, left, right) (Inherited from Overlay.PopoverView and modified default value). | string | no | iOS/Android | yes |
| align | Alignment (start, center, end) (Inherited from Overlay.PopoverView and modified default value). | string | no | iOS/Android | yes |
| showArrow | Show arrow (Inherited from Overlay.PopoverView and modified default value). | bool | no | iOS/Android | yes |

**ActionPopover.ActionPopoverView Static Properties**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Action popover item component. | class | yes | iOS/Android | yes |

**ActionPopover.ActionPopoverView.Item Properties:**

- ActionPopover.ActionPopoverView.Item component inherits all properties of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Item title. | string/number/element | yes | iOS/Android | yes |
| leftSeparator | Show left separator. | bool | no | iOS/Android | yes |
| rightSeparator | Show right separator. | bool | no | iOS/Android | yes |

### 25. PullPicker

PullPicker is a static class for pull-up selectors, generally used to trigger the display of a data list for user selection, presented as a drawer dragged out from the bottom of the screen.
PullPicker is implemented based on [Overlay](#overlay){}.

**Static Methods:**

- PullPicker inherits all static methods of **[Overlay](#overlay)**.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show a pull-up selector, overrides the function of the same name in Overlay{}, input parameter title is the list title, items is the list of selectable items, selectedIndex is the selected item index, onSelected is the callback function when an item is selected, options (nullable) is other properties of PullPicker.PullPickerView, parameter types see [PullPickerView](#pullpickerpullpickerview--props).<br/>Returns a unique overlay key value. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| PullPickerView | PullPicker content display component. | class | yes | iOS/Android | yes |

<a id="pullpickerpullpickerview--props"></a>
**PullPicker.PullPickerView**

- PullPicker.PullPickerView component inherits all properties and events of **[Overlay.PullView](#overlay-pullview)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | List title. | string | no | iOS/Android | yes |
| items | Available items list. | array | yes | iOS/Android | yes |
| selectedIndex | Current selected item index. | number | no | iOS/Android | yes |
| getItemText | Get the display text of items array element, passed parameters are (item, index), item = items[index], default uses item directly. | function | no | iOS/Android | yes |
| onSelected | Called when an item in the items array is selected, item = items[index]. | function | no | iOS/Android | yes |

**PullPicker.PullPickerView Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Pull picker item component. | class | no | iOS/Android | yes |

**PullPicker.PullPickerView.Item Properties**

- PullPicker.PullPickerView.Item component inherits all properties of **[ListRow](#listrow)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| selected | Selected state. | bool | no | iOS/Android | yes |

### 26. PopoverPicker

PopoverPicker is a static class for bubble selectors, generally used to trigger the display of a data list for user selection, presented as a bubble popped up from the trigger source component.
PopoverPicker is implemented based on [Overlay](#overlay){}.

**Static Methods:**

- PopoverPicker inherits all static methods of **[Overlay](#overlay)**.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show a bubble selector, overrides the function of the same name in Overlay{}, input parameter fromBounds is the popup bubble source component bounds, items is the list of selectable items, selectedIndex is the selected item index, onSelected is the callback function when an item is selected, options (nullable) is other properties of PopoverPicker.PopoverPickerView, parameter types see [PopoverPickerView](#popoverpickerpopoverpickerview--props).<br/>Returns a unique overlay key value. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| PopoverPickerView | PopoverPicker content display component. | class | yes | iOS/Android | yes |

<a id="popoverpickerpopoverpickerview--props"></a>
**PopoverPicker.PopoverPickerView Properties**

- PopoverPicker.PopoverPickerView component inherits all properties and events of **[Overlay.PopoverView](#overlay-popoverview)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | Options array. | array | yes | iOS/Android | yes |
| selectedIndex | Current selected item index. | number | no | iOS/Android | yes |
| getItemText | Get the display text of items array element, passed parameters are (item, index), item = items[index], default uses item directly. | function | no | iOS/Android | yes |
| shadow | Show shadow. | bool | no | iOS | yes |
| direction | Arrow direction (up, down, left, right) (Inherited from Overlay.PopoverView and modified default value). | string | no | iOS/Android | yes |
| align | Alignment (start, center, end) (Inherited from Overlay.PopoverView and modified default value). | string | no | iOS/Android | yes |
| showArrow | Show arrow (Inherited from Overlay.PopoverView and modified default value). | bool | no | iOS/Android | yes |
| onSelected | Called when an item in the items array is selected, item = items[index]. | function | no | iOS/Android | yes |

**PopoverPicker.PopoverPickerView Static Properties**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Popover picker item component. | class | no | iOS/Android | yes |

**PopoverPicker.PopoverPickerView.Item Properties**

- PopoverPicker.PopoverPickerView.Item component inherits all properties of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title content. | string/number/element | no | iOS/Android | yes |
| selected | Selected state. | bool | no | iOS/Android | yes |

### 27. Menu

Menu is a static class for menus, used to trigger the display of a popup menu for user selection, presented as a bubble popped up from the trigger source component.
Menu is implemented based on [Overlay](#overlay){}.

**Static Methods:**

- Menu inherits all static methods of **[Overlay](#overlay)**.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Show a popup menu, overrides the function of the same name in Overlay{}, input parameter fromBounds is the popup menu source component bounds, items is the list of menu items, options (nullable) is other properties of Menu.MenuView, parameter types see [MenuView](#menumenuview--props).<br/>Returns a unique overlay key value. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| MenuView | Menu content display component. | class | no | iOS/Android | yes |

<a id="menumenuview--props"></a>
**Menu.MenuView Properties:**

- Menu.MenuView component inherits all properties of **[Overlay.PopoverView](#overlay-popoverview)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| items | Menu items list (Array element type is: <br/>type MenuViewItem {<br/>&ensp;&ensp;title: string,<br/>&ensp;&ensp;icon: any,<br/>&ensp;&ensp;onPress: func,<br/>}<br/>icon detailed type see [Menu.MenuView.Item](#menumenuviewitem--props)). | array | no | iOS/Android | yes |
| shadow | Show shadow. | bool | no | iOS | yes |
| direction | Arrow direction (up, down, left, right) (Inherited from Overlay.PopoverView and modified default value). | string | no | iOS/Android | yes |
| align | Alignment (start, center, end) (Inherited from Overlay.PopoverView and modified default value). | string | no | iOS/Android | yes |
| showArrow | Show arrow (Inherited from Overlay.PopoverView and modified default value). | bool | no | iOS/Android | yes |

**Menu.MenuView Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Item | Menu item component. | class | no | iOS/Android | yes |

<a id="menumenuviewitem--props"></a>
**Menu.MenuView.Item Properties:**

- Menu.MenuView.Item component inherits all properties of **[TouchableOpacity](https://reactnative.dev/docs/touchableopacity.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Item title. | string/number/element | no | iOS/Android | yes |
| icon | Icon (<br/>**none**: No icon<br/>**empty**: Empty icon, displayed as blank and occupies the space of icon display size). | element/ImageSource | no | iOS/Android | yes |

### 28. Drawer

Drawer is a static class for drawers, the internal view is a simple encapsulation of [Overlay.PullView](#overlay-pullview) for ease of use.
Drawer is implemented based on [Overlay](#overlay){}.

**Static Methods:**

- Drawer inherits all static methods of **[Overlay](#overlay)**.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| open | Open a drawer. Parameter description:<br/>**view**: Drawer internal view content<br/>**side**: Drawer pull-out side, default is 'left'<br/>**rootTransform**: Root component transform animation, default is 'none'<br/>**options**: Other properties of Drawer.DrawerView, parameter types see [DrawerView](#drawerdrawerview--props)<br/>Return value is an object, object property description:<br>**key**: Overlay unique key value<br/>**close**: Close drawer function, calling this function will close the drawer. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| DrawerView | Drawer content display component. | class | no | iOS/Android | yes |

<a id="drawerdrawerview--props"></a>
**Drawer.DrawerView Properties**

- Drawer.DrawerView component inherits all properties and events of **[Overlay.PullView](#overlay-pullview)** component.

### 29. ModalIndicator

ModalIndicator is a static class for modal indicators, generally used when user operations need to be blocked, such as submitting data, presented as a modal indicator covering the full screen.
ModalIndicator is implemented based on **[Overlay](#overlay)**.

**Static Methods:**

- ModalIndicator inherits all static methods of **[Overlay](#overlay)**.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show | Pop up modal indicator, overrides the function of the same name in Overlay{}, input parameter text is the text displayed under the modal indicator. If the modal indicator is already displayed before calling this function, only the text is replaced. | function | yes | iOS/Android | yes |
| hide | Hide the indicator. | function | yes | iOS/Android | yes |

**Static Properties:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| IndicatorView | Content component for the modal indicator. | class | no | iOS/Android | yes |

**ModalIndicator.IndicatorView Parameters:**

- ModalIndicator.IndicatorView component inherits all properties of **[View](https://facebook.github.io/react-native/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| text | Message text. | string/number/element | no | iOS/Android | yes |
| position | Display position. <br/>**top**: Top of the window<br/>**bottom**: Bottom of the window<br/>**center**: Center of the window<br/>top, bottom positions can be set in Theme. | string | no | iOS/Android | yes |
| size | Indicator size. | string | no | iOS/Android | yes |
| color | Indicator color (Default value is set in Theme). | string | no | iOS/Android | yes |

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

BasePage defines a base page component, which is an abstract encapsulation of Page, needs to derive new classes to use, providing a series of easy-to-use overridable methods.

- BasePage component inherits all properties of **[View](https://facebook.github.io/react-native/docs/view.html)** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| scene | Transition effects. | object | no | iOS/Android | yes |
| autoKeyboardInsets | Whether to automatically insert keyboard occupation space when the keyboard pops up, the purpose of inserting keyboard occupation space is to avoid page content being covered by the keyboard. | bool | no | iOS/Android | yes |
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
| navigator | Navigator object (Read-only property variable). | object | yes | iOS/Android | yes |
| didMount | Whether the page mounted. | bool | yes | iOS/Android | yes |
| isFocused | Whether the page is focused. | bool | yes | iOS/Android | yes |

**Lifecycle Methods:**

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onWillFocus | Will focus on this page, called before page transition animation starts.<br/>Override this function in derived class to perform required operations. | function | no | iOS/Android | yes |
| onDidFocus | Has focused on this page, called after page transition animation ends.<br/>Override this function in derived class to perform required operations.<br/>If there are time-consuming operations in page initialization, it is easy to cause page transition animation lag during initialization, it is recommended to put complex initialization code in this function. | function | no | iOS/Android | yes |
| onHardwareBackPress | Called when the user presses the back button (physical key, Android only). | function | no | Android | no |
| renderPage | Page render function, all derived classes of BasePage should override this function to render the interface, instead of render function. | function | yes | iOS/Android | yes |

### 32. NavigationPage

NavigationPage defines a navigation page component, inheriting from BasePage, adding a NavigationBar navigation bar on the basis of BasePage.

- NavigationPage component inherits all properties of **BasePage** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Navigation bar title. | string | no | iOS/Android | yes |
| showBackButton | Show the back button. | bool | no | iOS/Android | yes |
| navigationBarInsets | Whether to add navigation bar occupation space for content area. (This property defaults to true, so that the content is not covered by the navigation bar. If the page content uses ScrollView and you need to control the display/hide of the NavigationBar yourself, you need to set this property to false and add the navigation bar occupation space in the ScrollView container yourself, so that the top space can be utilized after the navigation bar is hidden). | bool | no | iOS/Android | yes |
| scene | Transition effects (Inherited from BasePage and modified default value). | object | no | iOS/Android | yes |

**Methods:**

- NavigationPage component inherits all methods of **BasePage** component.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| renderNavigationTitle | Navigation bar title render function. | function | no | iOS/Android | yes |
| renderNavigationLeftView | Navigation bar left button render function, default returns NavigationBar.BackButton component instance based on this.props.showBackButton value, otherwise returns null.<br/>Note: You can modify the default title of the back button through Theme. | function | no | iOS/Android | yes |
| renderNavigationRightView | Navigation bar right button render function. | function | no | iOS/Android | yes |
| renderNavigationBar | Navigation bar render function (Generally should override the above three functions instead of this function). | function | no | iOS/Android | yes |

## Known Issues


## Others


## License

This project is based on [The MIT License (MIT)](https://github.com/react-native-oh-library/teaset/blob/master/LICENSE). Feel free to enjoy and contribute to open source.
