> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>beeshell</code> </h1>
</p>

This project is based on [beeshell@2.0.11](https://github.com/Meituan-Dianping/beeshell).

Please go to the Releases release address of the third-party library to view the supporting version information: [@react-native-ohos/beeshell Releases](https://github.com/react-native-oh-library/beeshell/releases). For older versions that are not published to npm, install the tgz package by referring to the [Installation Guide](/en/tgz-usage-en.md).

| Version              | Releases info                                     |  Support RN version                |
| ------------------------- | ------------------------------------------------- |  -------------------------- |
| 2.0.12                 | [@react-native-ohos/beeshell Releases](https://github.com/react-native-oh-library/beeshell/releases)  | 0.72/0.77 |

## Installation and Usage

Run the following command in your project directory:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/beeshell
```

#### **yarn**

```bash
yarn add @react-native-ohos/beeshell
```

<!-- tabs:end -->

The sample below demonstrates a basic usage scenario:

**Hello world**  
Import components from the beeshell package and use them directly:
```
import React, { Component } from 'react';
import { View, AppRegistry } from 'react-native';
import { Button } from 'beeshell';

class HelloWorldApp extends Component {
  render() {
    return (
      <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
        <Button type="primary" size="md" textColorInverse>primary</ Button>
        <Button type="primary" size="md">
          <View>
            <Text>customized</Text>
            <Text>components</Text>
          </View>
        </Button>
        <Button type='info' size='sm' disabled>
          info
        </Button>
      </View>
    );
  }
}

AppRegistry.registerComponent('HelloWorldApp', () => HelloWorldApp);
```
**On-demand import**  
Import individual components for on-demand usage:
```
import Label from 'beeshell/components/Button';
```
## Constraints and Limitations

### Compatibility

The content in this document has been verified under the following environment:

1. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Components

> [!TIP] The "Platform" column reflects platform support in the original third-party library.

> [!TIP] The "HarmonyOS Support" column shows HarmonyOS support status: yes, no, or partially. Usage is cross-platform; effects match iOS or Android.

### 1. Actionsheet - Bottom Action Menu Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| header | Header/title content at the top, can be a string or a custom React element | string/ReactElement | no | iOS/Android | yes |
| footer | Footer content, usually the cancel button text or a custom element | string/ReactElement | no | iOS/Android | yes |
| data | List of option data. Each item can be a string or an object containing a label field | Array | yes | iOS/Android | yes |
| cancelable | Whether the menu disappears when the overlay mask is tapped | boolean | no | iOS/Android | yes |
| maxShowNum | Maximum number of options to display before scrolling starts. Set to null for unlimited | number | no | iOS/Android | yes |
| renderItem | Custom function to render each option. Receives (item, index) | Function | no | iOS/Android | yes |
| onPressCancel | Callback function triggered when the cancel button is pressed | Function | no | iOS/Android | yes |
| onPressConfirm | Callback function triggered when an option is selected. Receives (item, index) | Function | no | iOS/Android | yes |
| useSafeAreaView | Whether to enable SafeAreaView to adapt to the bottom safe area | boolean | no | iOS/Android | yes |

### 2. Badge - Badge Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Custom styles for the badge container | ViewStyle | no | iOS/Android | yes |
| label | Text or number content displayed on the badge | string \| number | no | iOS/Android | yes |
| labelStyle | Custom styles for the badge text | TextStyle | no | iOS/Android | yes |

### 3. BottomModal - Bottom Modal Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| titleContainer | Custom content for the title area | ReactElement | no | iOS/Android | yes |
| title | Text content for the title | string | no | iOS/Android | yes |
| titleStyle | Custom styles for the title text | TextStyle | no | iOS/Android | yes |
| rightLabel | Custom element for the button on the right side | ReactElement | no | iOS/Android | yes |
| rightLabelText | Text content for the button on the right side | string | no | iOS/Android | yes |
| rightLabelTextStyle | Custom styles for the right button text | TextStyle | no | iOS/Android | yes |
| rightCallback | Callback function triggered when the right button is pressed | Function | no | iOS/Android | yes |
| leftLabel | Custom element for the button on the left side | ReactElement | no | iOS/Android | yes |
| leftLabelText | Text content for the button on the left side | string | no | iOS/Android | yes |
| leftLabelTextStyle | Custom styles for the left button text | TextStyle | no | iOS/Android | yes |
| leftCallback | Callback function triggered when the left button is pressed | Function | no | iOS/Android | yes |

### 4. Button - Button Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Custom styles for the button container | ViewStyle | no | iOS/Android | yes |
| textStyle | Custom styles for the button's inner text | TextStyle | no | iOS/Android | yes |
| textColorInverse | Whether the button text is black. Controls the text color to be either black or white | boolean | no | iOS/Android | yes |
| type | Specifies the predefined button style. Options:  'default' 'primary' 'success' 'info' 'warning' 'danger' 'text' | string | yes | iOS/Android | yes |
| size | Size. Options: 'lg' 'md' 'sm' | 	string | no | iOS/Android | yes |
| children | Child elements, can be a string or ReactElement | any | no | iOS/Android | yes |
| disabled | Whether the button is clickable | boolean | no | iOS/Android | yes |
| onPress | Callback function triggered when the button is pressed | Function | no | iOS/Android | yes |

### 5. Calendar - Calendar Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Custom styles for the calendar container | any | no | iOS/Android | yes |
| date | The currently selected date | string | no | iOS/Android | yes |
| startDate | The start date of the selectable range (format must match format) | string | no | iOS/Android | yes |
| endDate | The end date of the selectable range (format must match format) | string | no | iOS/Android | yes |
| onChange | Callback function triggered when the date changes. Parameter is the formatted date string | Function | no | iOS/Android | yes |
| renderItem | Custom function to render a date cell, used to override the default cell style | Function | no | iOS/Android | yes |

### 6. Cascader - Cascading Selector Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Custom styles for the component container | any | no | iOS/Android | yes |
| data | Data source, a tree structure. Supports child-table notation (default parent-child via children) and parent-pointer notation (default via id, pId) | any[] | yes | iOS/Android | yes |s
| value | Selected value(s), an array (single selection has one element, multi-select not yet supported). Array elements are the unique identifier values of data source items | any[] | no | iOS/Android | yes |
| fieldKeys | Custom key names for data source properties: labelKey for display, idKey for unique ID, pIdKey for parent ID (parent-pointer notation), childrenKey for child array (child-table notation), activeKey for active state to open children, checkedKey for checked, disabledKey for disabled | any | no | iOS/Android | yes |
| proportion | Width ratio of data columns. Default is 1 for each column | number[] | no | iOS/Android | yes |
| isLeafNode | Custom logic function to determine leaf nodes | Function | no | iOS/Android | yes |
| onChange | Callback after an item is selected. Parameters include value (array, currently single select only) and info (selected item and its ancestor nodes) | Function | no | iOS/Android | yes |
| renderItem | Custom rendering function for items. Parameters include item and index | Function | no | iOS/Android | yes |

### 7. Checkbox - Checkbox Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ------------ | ---- | -------- | -------- | ------------------ |
| style | Styles | 	ViewStyle | no | iOS/Android | yes |
| value | Selected state value | any | no | iOS/Android | yes |
| iconPosition | Icon position（'left'\|'right'） | string | no | iOS/Android | yes |
| onChange | Callback when selection state changes | Function | no | iOS/Android | yes |
| children | Checkbox child items | ReactChild[] \| ReactChild | no | iOS/Android | yes |
| showAllCheck | Show "Select All" option | 	boolean | no | iOS/Android | yes |
| checkedIcon | Icon for the checked state | 	ReactElement<any> | no | iOS/Android | yes |
| uncheckedIcon | Icon for the unchecked state | 	ReactElement<any> | no | iOS/Android | yes |

#### Checkbox.Item - Checkbox Sub-Item

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | 	ViewStyle | no | iOS/Android | yes |
| label | Option text | string | yes | iOS/Android | yes |
| value | Value representing the selected state | any   | yes | iOS/Android | yes |
| disabled | Disabled state | boolean | no | iOS/Android | yes |
| renderItem | Custom function to define the option | 	Function |  no | iOS/Android | yes |

### 8. DatePicker - Date Picker Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| startYear | The starting year  | number | yes | iOS/Android | yes |
| proportion | UI style width ratio for each data column | number[] | no | iOS/Android | yes |
| numberOfYears | Number of years to display forward | number | yes | iOS/Android | yes |
| date | The preset date string, in 'YYYY-MM-DD' format | string | no | iOS/Android | yes |
| onChange | Callback function to listen for value changes | Function | no | iOS/Android | yes |


### 9. Dialog - Dialog Component

Used for system prompts, operation confirmations, custom content, etc. Supports multiple style customizations and flexible interaction.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title | Title | string | no | iOS/Android | yes |
| titleStyle | Title style | TextStyle | no | iOS/Android | yes |
| bodyText | Content text | string | no | iOS/Android | yes |
| bodyTextStyle | Content text style | TextStyle | no | iOS/Android | yes |
| header | Custom header rendering area | any | no | iOS/Android | yes |
| body | Custom content rendering area | any | no | iOS/Android | yes |
| cancelLabelText | Cancel button text | string | no | iOS/Android | yes |
| cancelLabelTextStyle | Cancel button text style | TextStyle | no | iOS/Android | yes |
| confirmLabelText | Confirm button text | string | no | iOS/Android | yes |
| confirmLabelTextStyle | Confirm button text style | TextStyle | no | iOS/Android | yes |
| cancelLabel | Custom cancel button rendering area | any | no | iOS/Android | yes |
| confirmLabel | Custom confirm button rendering area | any| no | iOS/Android | yes |
| cancelCallback | Callback for cancel button click | Function | no | iOS/Android | yes |
| confirmCallback | Callback for confirm button click | Function | no | iOS/Android | yes |
| operations | Custom bottom operation button group | Array | no | iOS/Android | yes |
| operationsLayout | Layout for operation buttons. Supports 'row', 'column' | string | no | iOS/Android | yes |

### 10. Form - Form Component

Form Container Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Form styles | ViewStyle | no | iOS/Android | yes |


Form.Item Form Item Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ | 
| style | Form item styles | ViewStyle | no | iOS/Android | yes | 
| label | Form item label | string\ReactElement | no | iOS/Android | yes | 
| labelWidth | Width of the form item label | number | no | iOS/Android | yes | 
| hasLine | Whether to show a bottom divider line | boolean | no | iOS/Android | yes | 
| children | Form control content | ReactChild[]\|ReactChild | no | iOS/Android | yes |


### 11. Icon - Icon Component

Implemented using the Image element and used within other components of this library. Because the tintColor property is not supported on the Android platform, its usage scenarios are very limited. Please use according to your actual situation. It is recommended to integrate font file functionality in your own projects.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | 	ImageStyle | no | iOS/Android | yes |
| type | Icon type| string | yes | iOS/Android | yes |
| size | Icon size |number| no | iOS/Android | yes |
| tintColor | Icon color | string | no | iOS | yes |
| source | 	Custom image | 	ImageSourcePropType | no | iOS/Android | yes |

### 12. Input - Input Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | 	ViewStyle | no | iOS/Android | yes |
| inputStyle | Styles for the input text | TextStyle | no | iOS/Android | yes |
| value | Value | 	string | no | iOS/Android | yes |
| onChange | Callback when input content changes (parameter is the input value) | Function | no | iOS/Android | yes |

### 13. Longlist - Long List Component

Long list component based on FlatList. Supports pull-down refresh and pull-up load more.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data | 	Data source | 	Array | yes | iOS/Android | yes |
| total | Total length of data | 	number | no | iOS/Android | yes |
| renderItem | Function to render each item | Function | 	yes | iOS/Android | yes |
| onEndReached | Called when the list is scrolled within onEndReachedThreshold distance from the bottom. No parameters, must return a Promise | 	Function | yes | iOS/Android | yes |
| onRefresh | Pull-down refresh callback. No parameters, must return a Promise | 	Function | no | iOS/Android | yes |
| renderFooter | Custom function to render footer content. Parameters: loading state, data source, total length. Must return a ReactElement | 	Function | no | iOS/Android | yes |
| scrollToIndex | Function to scroll to a specified position | 	Function | no | iOS/Android | yes |

scrollToIndex

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| animated | Whether to animate the scroll. Default: true | 	boolean | no | iOS/Android | yes |
| index | Index of the list item to scroll to (starting from 0) | number | yes | iOS/Android | yes |
| viewOffset | Pixel offset for the final target position | number | yes | iOS/Android | yes |
| viewPosition | Position of the target item in the view: 0 = top, 1 = bottom, 0.5 = center (default) | number | yes | iOS/Android | yes |

### 14. Modal - Modal Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| containerStyle | Style for the modal container | ViewStyle | no | iOS/Android | yes |
| style | Style for the modal itself | ViewStyle | no | iOS/Android | yes | 
| cancelable | Whether clicking the backdrop closes the modal | boolean | no | iOS/Android | yes | 
| scrollable | Whether content is scrollable when overflowing | boolean | no | iOS/Android | yes | 
| backdropColor | Color of the backdrop | string | no | iOS/Android | yes | 
| screenWidth | Screen width, used for layout calculations | number | no | iOS/Android | yes | 
| screenHeight | Screen height, used for layout calculations | number | no | iOS/Android | yes | 
| offsetX | X-axis offset | number | no | iOS/Android | yes | 
| offsetY | Y-axis offset | number | no | iOS/Android | yes | 
| animatedTranslateX | X-axis coordinate for the pop-up position. Defaults to popping from screen center | number | no | iOS/Android | yes | 
| animatedTranslateY | Y-axis coordinate for the pop-up position. Defaults to popping from screen center | number | no | iOS/Android | yes | 
| onOpen | Callback when the modal starts to open | Function | no | iOS/Android | yes | 
| onOpened | Callback after the modal is opened | Function | no | iOS/Android | yes | 
| onClose | Callback when the modal starts to close | Function | no | iOS/Android | yes | 
| onClosed | Callback after the modal is closed | Function | no | iOS/Android | yes |
| open | Function to open the modal | Function | no | iOS/Android | yes |
| close | Function to close the modal | Function | no | iOS/Android | yes |

### 15. NavigationBar - Navigation Bar Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Custom styles | ViewStyle |no| iOS/Android | yes | 
| titleContainer | Content to display in the center area | ReactElement | no | iOS/Android | yes | 
| title | Title for the center area | string | no | iOS/Android | yes |
| backLabel | Content to display in the left area | ReactElement |	no | iOS/Android | yes | 
| backLabelText | Text for the left area | string |	no | iOS/Android | yes | 
| backLabelTextStyle | Text style for the left area | TextStyle |	no | iOS/Android | yes |  
| backLabelIcon | Icon for the left area | ReactElement |	no | iOS/Android | yes | 
| forwardLabel | Content to display in the right area | ReactElement |	no | iOS/Android | yes |
| forwardLabelText | Text for the right area | string |	no | iOS/Android | yes | 
| forwardLabelTextStyle | Text style for the right area | TextStyle |	no | iOS/Android | yes |   
| onPressBack | Callback for clicking the left area | Function |	no | iOS/Android | yes | 
| onPressForward | Callback for clicking the right area | Function |	no | iOS/Android | yes | 
| proportion | Layout proportion for rendering areas | number[] |	no | iOS/Android | yes |
| renderItem | Custom function to render each area | Function | no | iOS/Android | yes |

### 16. Picker - Filter Picker Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
 | style | Styles | ViewStyle | no | iOS/Android | yes | 
 | label | Content displayed on the button. Can be a string or a function | string/Function |	no | iOS/Android | yes | 
 | activeIcon | Icon for the active state | ReactElement |	no | iOS/Android | yes | 
 | inactiveIcon | Icon for the inactive state | ReactElement |	no | iOS/Android | yes | 
 | disabled | Whether it is disabled | boolean |	no | iOS/Android | yes | 
 | cancelable | Whether clicking the backdrop closes the picker | boolean |	no | iOS/Android | yes | 
 | onToggle | Callback when the active state toggles | Function |	no | iOS/Android | yes | 
 | open | Function to open. Returns a Promise | Function | no | iOS/Android | yes |
 | close | Function to close. Returns a Promise | Function | no | iOS/Android | yes |

### 17. Progress - Progress Bar Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles for the outer container | 	ViewStyle | no | iOS/Android | yes |
| barStyle | Styles for the progress bar itself | ViewStyle | no | iOS/Android | yes |
| percent | Progress (0-100 range) | number | no | iOS/Android | yes |
| easing | Whether animation is needed | boolean | no | iOS/Android | yes |
| duration | Animation duration (ms) | 	number | no | iOS/Android | yes |


### 18. Radio - Radio Component

Radio component similar to HTML radio.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| iconPosition | Icon position. Supports 'left', 'right' | string | no | iOS/Android | yes |
| checkedIcon | Icon for the checked state | ReactElement | no | iOS/Android | yes |
| uncheckedIcon | Icon for the unchecked state | ReactElement | no | iOS/Android | yes |
| value | Selected value, corresponds to the value prop of Radio.Item | any | no | iOS/Android | yes |
| children | Child elements | ReactChild[] \| ReactChild | no | iOS/Android | yes |
| onChange | Callback function when the value changes | Function | no | iOS/Android | yes |

Radio.Item Props
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles for the radio option | ViewStyle | no | iOS/Android | yes |
| label | Option text | string | yes | iOS/Android | yes |
| value | Option value | any | yes | iOS/Android | yes |
| disabled | Whether the option is disabled | boolean | no | iOS/Android | yes |
| renderItem | Custom rendering function for the option | Function | no | iOS/Android | yes |


### 19. Rate - Rating Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Custom styles  | ViewStyle | no | iOS/Android | yes |
| value | Score | number | no | iOS/Android | yes |
| total | Total score | number | no | iOS/Android | yes |
| icons | con element collection { <br/>&nbsp;&nbsp; empty: ReactElement\<any> <br/>&nbsp;&nbsp; full: ReactElement\<any> <br/>&nbsp;&nbsp; half?: ReactElement\<any> <br/> } | object | no | iOS/Android | yes |
| iconSize | Size of the icons | number | yes | iOS/Android | yes |
| iconSpace | Spacing between icons | number | yes | iOS/Android | yes |
| enableHalf | Whether to enable half-star selection | boolean | no | iOS/Android | yes |
| onChange | Callback function when the rating changes | Function | no | iOS/Android | yes |

### 20. Scrollpicker - Scroll Picker Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| list |  Data source, a 2D array. First level represents columns, second level represents selectable items. Items can be objects (must contain a label property) or string/number | Array | yes | iOS/Android | yes |
| value | Selected data, a 1D array. Index corresponds to the list column, value corresponds to the list row. Its length must match the data source list | Array | no | iOS/Android | yes |
| proportion | Column width ratio. Ensure its length matches the data source list | Array| no | iOS/Android | yes |
| offsetCount | Number of items offset from the top for the selected item | number | no | iOS/Android | yes |
| onChange | Callback for data change. Provides two index parameters: column index and row index | Function | no | iOS/Android | yes |
| renderItem | Custom rendering function for items | Function | no | iOS/Android | yes |

### 21. SlideModal - Slide Modal Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| styles | Custom styles for each layer element | { root: ViewStyle, container: ViewStyle, backdrop: ViewStyle, content: ViewStyle } | no | iOS/Android | yes |
| offsetX | X-axis coordinate for the pop-up position | number | no | iOS/Android | yes |
| offsetY | Y-axis coordinate for the pop-up position | number | no | iOS/Android | yes |
| direction | Animation direction. Value can be 'up', 'down', 'left', 'right', or an array like ['up', 'left'], etc | string/string[]| no | iOS/Android | yes |
| align | Position of the content part | string | no | iOS/Android | yes |
| fullScreenPatch | Full-screen patch, configuring which areas are click-through | boolean[] | no | iOS/Android | yes |
| children | Modal content | ReactChild/ReactChild[] | yes | iOS/Android | yes |

### 22. Slider - Slider Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| value | Current value | number | no | iOS/Android | yes |
| min | Minimum value | number | no | iOS/Android | yes |
| max | Maximum value | number| no | iOS/Android | yes |
| disabled | Whether it is disabled | boolean | no | iOS/Android | yes |
| step | Minimum sliding unit (step) | number | no | iOS/Android | yes |
| marks | Mark values corresponding to ticks | string[] / ReactElement[] | no | iOS/Android | yes |
| maxTrackColor | Color of the maximum part of the track | string | no | iOS/Android | yes |
| minTrackColor | Color of the minimum part of the track | string | no | iOS/Android | yes |
| midTrackColor | Color of the middle part of the track | string | no | iOS/Android | yes |
| onChange | Callback when the value changes | Function | no | iOS/Android | yes |
| showTip | Whether to show a tooltip bubble | boolean | no | iOS/Android | yes |
| renderTip | Custom function to render the tooltip content. Callback parameter isOther identifies which thumb | Function | no | iOS/Android | yes |
| renderThumb | Custom function to render the thumb (slider handle). Callback parameter isOther identifies which thumb | Function | no | iOS/Android | yes |

### 23. Stepper - Stepper/Counter Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles  | ViewStyle | no | iOS/Android | yes |
| operatorStyle | Styles for the operator buttons | ViewStyle | no | iOS/Android | yes |
| operatorIconColor | Color for the operator button icons | string | no | iOS/Android | yes |
| max | Maximum value | number| no | iOS/Android | yes |
| min | Minimum value | number | no | iOS/Android | yes |
| value | Current value | number | no | iOS/Android | yes |
| step | Step size | number | no | iOS/Android | yes |
| editable | Allows direct input | boolean | no | iOS/Android | yes |
| onChange | Callback when the value changes | Function | yes | iOS/Android | yes |

### 24. Switch - Switch Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| value | State value | boolean | no | iOS/Android | yes |
| disabled | Whether the state can be toggled | boolean | no | iOS/Android | yes |
| rockerSize | Size of the thumb/slider. Supports 'lg' 'sm'| string| no | iOS/Android | yes |
| activeColor | Color for the "ON" state | string | no | iOS/Android | yes |
| onChange | Callback when the value changes | Function | no | iOS/Android | yes |

### 25. Tab - 标签页组件

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| dataContainerStyle | Styles for the data source container | ViewStyle | no | iOS/Android | yes |
| dataItemContainerStyle | Container styles for each data source item | ViewStyle | no | iOS/Android | yes |
| dataItemStyle | Styles for each data source item itself | ViewStyle| no | iOS/Android | yes |
| activeColor | Color for the active state | string | no | iOS/Android | yes |
| data | Data source. Array elements are objects that must contain label and value properties | Array | yes | iOS/Android | yes |
| value | Value of the active item, which should equal the value of a data source item | any | no | iOS/Android | yes |
| onChange | Callback when the active state changes. Parameters are the data source option and its index | Function | no | iOS/Android | yes |
| renderItem | Custom rendering function for items. Function parameters: item, index, active | Function | no | iOS/Android | yes |

Methods
.scrollTo(index: number)
Scrolls to the option specified by the index.

### 26. Tag - Tag Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| textStyle | Text styles | TextStyle | no | iOS/Android | yes |
| type | Type. Supports 'default' 'primary' 'danger' 'info' 'success' 'warning'| string | no | iOS/Android | yes |
| textColorInverse | Text inverse color mode | boolean | no | iOS/Android | yes |

### 27. Timepicker - Time Picker Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| hourStep | Hour step | number | no | iOS/Android | yes |
| minuteStep | Minute step | number | no | iOS/Android | yes |
| secondStep | Second step | number| no | iOS/Android | yes |
| value | The selected time string, in 'HH:mm:ss' format | string| no | iOS/Android | yes |
| onChange | Callback for data change | Function| no | iOS/Android | yes |

### 28. Tip - Tip Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| body | Tip content  | string/ReactElement | no | iOS/Android | yes |
| duration | Display duration | number | no | iOS/Android | yes |
| position | Display position | string/string[] | no | iOS/Android | yes |

Methods
.show(msg: string, duration?: number, cancelable?: boolean, position?: string | string[])
This is a class method (static method).
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| msg	 | Text message to display | string | no | iOS/Android | yes |
| duration | How many milliseconds before it automatically disappears | number | no | iOS/Android | yes |
| cancelable | Whether clicking the blank area closes the tip | boolean | no | iOS/Android | yes |
| position | Display position of the tip. Supports strings or arrays, e.g., 'top', 'center', ['top', 'left'], etc | string/string[] | no | iOS/Android | yes |

### 29. Topview - Top View Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| add | Method to add an element | Function | no | iOS/Android | yes |
| remove | Method to remove an element | Function | no | iOS/Android | yes | 

### 30. TreeView - Tree View Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| activeIcon | Icon for the active state (expanded) | ReactElement | no | iOS/Android | yes |
| inactiveIcon | Icon for the inactive state (collapsed) | ReactElement | no | iOS/Android | yes |
| data | Data source, supporting both nested and flattened tree structures | any[]| no | iOS/Android | yes |
| dataStructureType | Data structure type. Supports 'nested'\|'flattened'| string| no | iOS/Android | yes |
| fieldKeys | Custom key names for data item properties, including idKey, pIdKey, childrenKey, activeKey | any| no | iOS/Android | yes |
| onPress | Callback when an item is pressed. Parameter is the pressed item | Function| no | iOS/Android | yes |

### 31. Ruler - Ruler Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| direction | Ruler orientation. Supports 'vertical'\|'horizontal' | string | no | iOS/Android | yes |

### 32. Popover - Popover Component

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| offsetX | X-axis coordinate for the pop-up position | number | no | iOS/Android | yes |
| offsetY | Y-axis coordinate for the pop-up position | number | no | iOS/Android | yes |
| direction | Pop-up direction | string/string[] | no | iOS/Android | yes |
| align | Position of the content part | string | no | iOS/Android | yes |
| children | Popover display content | string/ReactChild/ReactChild[] | yes | iOS/Android | yes |

### 33. Dropdown - Dropdown Select Component
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| style | Styles | ViewStyle | no | iOS/Android | yes |
| direction | Dropdown direction | string | no | iOS/Android | yes |
| checkedIcon | Icon for the checked/selected state | ReactElement | no | iOS/Android | yes |
| uncheckedIcon | Icon for the unchecked/unselected state | ReactElement | no | iOS/Android | yes |
| data | Data source | Array | yes | iOS/Android | yes |
| value | Value of the selected item | any | no | iOS/Android | yes |
| onOpen | Callback when the dropdown layer opens | Function | no | iOS/Android | yes |
| onClose | Callback when the dropdown layer closes | Function | no | iOS/Android | yes |
| onChange | Callback when the selected item changes | Function | no | iOS/Android | yes |

## Known Issues


## Others


## License

This project is based on [The MIT License (MIT)](https://github.com/react-native-oh-library/teaset/blob/master/LICENSE). Feel free to enjoy and contribute to open source.
