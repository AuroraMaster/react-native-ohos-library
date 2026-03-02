> Template version: v0.4.0

<p align="center">
  <h1 align="center"> <code>@react-native-picker/picker</code> </h1>
</p>

This project is based on[@react-native-picker/picker](https://github.com/react-native-picker/picker).

This third-party library has been migrated to Gitcode and is now available for direct download from npm, the new package name is: `@react-native-ohos/picker`, The version correspondence details are as follows:

| Name                        | Version             | Release Information                                          | Supported RN Version | Supported Autolink | Compile API Version | Community Baseline Version | npm Address                                                  |
| --------------------------- | ------------------- | ------------------------------------------------------------ | -------------------- | ------------------ | ------------------- | -------------------------- | ------------------------------------------------------------ |
| @react-native-ohos/picker   | ~ 2.12.0            | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_picker/releases) | 0.82.*               | No                 | API12+              | 2.11.4                     | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/picker) |
| @react-native-ohos/picker   | ~2.11.2             | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_picker/releases) | 0.77.*               | No                 | API12+              | 2.11.1                     | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/picker) |
| @react-native-ohos/picker   | ~ 2.6.4             | [Gitcode Releases](https://gitcode.com/openharmony-sig/rntpc_picker/releases) | 0.72.*               | Yes                | API12+              | 2.6.1                      | [Npm Address](https://www.npmjs.com/package/@react-native-ohos/picker) |
| @react-native-oh-tpl/picker | <= 2.6.3@deprecated | [Github Releases(deprecated)](https://github.com/react-native-oh-library/picker) | 0.72.*               | No                 | API12+              | 2.6.1                      | [Npm Address](https://www.npmjs.com/package/@react-native-oh-tpl/picker) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/picker
```

#### **yarn**

```bash
yarn add @react-native-ohos/picker
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import { Picker } from "picker";
import { View } from "react-native";

export const PickerExample = ()=>{
  const [selectedLanguage, setSelectedLanguage] = React.useState();

  return (
    <View style={{backgroundColor:"#fff",padding:40}}>
      <Picker
        selectedValue={selectedLanguage}
        onValueChange={(itemValue, itemIndex) => setSelectedLanguage(itemValue)}>
        <Picker.Item label="Java" value="java" />
        <Picker.Item label="JavaScript" value="js" />
      </Picker>
    </View>
  )
}
```

## 2. Link

|                                | Supported Autolink | Supported RN Version |
|--------------------------------|-----------------------|----------------------|
| ~2.12.0 | No | 0.82 |
| ~2.11.2                        |  No                   |  0.77           |
| ~2.6.4                         |  Yes                  |  0.72                |
| <= 2.6.3@deprecated            |  No                   |  0.72                |

Projects using AutoLink need to be configured according to this document, AutoLink framework guide.：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you are using supports Autolink and the project has integrated Autolink, you can skip the ManualLink configuration.

<details>
  <summary>ManualLink: This step provides guidance for manually configuring native dependencies.</summary>

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/picker": "file:../../node_modules/@react-native-ohos/picker/harmony/picker.har",
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

### 2.3 Configuring CMakeLists and Introducing PickerPackage

> If you are using version <= 2.6.3, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/picker/src/main/cpp" ./picker)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_picker)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "PickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<PickerPackage>(ctx)
    };
}
```

### 2.4. Introducing picker Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNCPicker, PICKER_TYPE } from "@react-native-ohos/picker"

 @Builder
 export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === PICKER_TYPE) {
+   RNCPicker({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
+ PICKER_TYPE
  ];
```

### 2.5 Introducing RNCPickerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNCPickerPackage } from '@react-native-ohos/picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNCPickerPackage(ctx)
  ];
}
```

</details>

### 2.6 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
4. RNOH: 0.82.1; SDK: HarmonyOS 6.0.1 Release SDK; IDE: DevEco Studio 6.0.1 Release; ROM: 6.0.0.120 SP7;

## 4. Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### PickerProps

| Name                      | Description                                                                                       | Type                                                         | Required | Platform              | HarmonyOS Support |
|---------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------|----------|-----------------------|-------------------|
| `onValueChange`           | Callback for when an item is selected.                                                            | function                                                     | No       | All                   | Yes               |
| `selectedValue`           | Value matching value of one of the items. Can be a string or an integer.                          | any                                                          | No       | All                   | Yes               |
| `style`                   | NA                                                                                                | pickerStyleType                                              | No       | All                   | Yes               |
| `testID`                  | Used to locate this view in end-to-end tests.                                                     | string                                                       | No       | All                   | Yes               |
| `enabled`                 | If set to false, the picker will be disabled, i.e. the user will not be able to make a selection. | boolean                                                      | No       | Android, Web, Windows | Yes               |
| `mode`                    | On Android, specifies how to display the selection items when the user taps on the picker         | enum('dialog', 'dropdown')                                   | No       | Android               | No                |
| `dropdownIconColor`       | On Android, specifies color of dropdown triangle.                                                 | ColorValue                                                   | No       | Android               | No                |
| `dropdownIconRippleColor` | On Android, specifies ripple color of dropdown triangle.                                          | ColorValue                                                   | No       | Android               | No                |
| `prompt`                  | Prompt string for this picker, used on Android in dialog mode as the title of the dialog.         | string                                                       | No       | Android               | No                |
| `itemStyle`               | Style to apply to each of the item labels.                                                        | [text styles](https://reactnative.dev/docs/text-style-props) | No       | iOS, Windows          | partially         |
| `numberOfLines`           | On Android & iOS, used to truncate the text with an ellipsis after computing the text layout.     | number                                                       | No       | Android, iOS          | No                |
| `onBlur`                  | NA                                                                                                | function                                                     | No       | Android               | No                |
| `onFocus`                 | NA                                                                                                | function                                                     | No       | Android               | No                |
| `selectionColor`          | Color to apply to the selection indicator.                                                        | ColorValue                                                   | No       | iOS                   | Yes               |
| `themeVariant`            | NA                                                                                                | enum('light', 'dark')                                        | No       | iOS                   | No                |

### PickerItemProps

| Name                 | Description                                                                                              | Type          | Required | Platform | HarmonyOS Support |
|----------------------|----------------------------------------------------------------------------------------------------------|---------------|----------|----------|-------------------|
| `label`              | Displayed value on the Picker Item.                                                                      | string        | Yes      | All      | Yes               |
| `value`              | Actual value on the Pickmodeler Item.                                                                    | number,string | Yes      | All      | Yes               |
| `color`              | Displayed color on the Picker Item.                                                                      | ColorValue    | No       | All      | No                |
| `fontFamily`         | Displayed fontFamily on the Picker Item.                                                                 | string        | No       | All      | No                |
| `style`              | Style to apply to individual item labels.                                                                | ViewStyleProp | No       | Android  | No                |
| `enabled`            | If set to false, the specific item will be disabled, i.e. the user will not be able to make a selection. | boolean       | No       | Android  | No                |
| `contentDescription` | Sets the content description to the Picker Item.                                                         | string        | No       | Android  | No                |

## 5. Static Methods


| Name    | Description                     | Type     | Required | Platform | HarmonyOS Support |
|---------|---------------------------------|----------|----------|----------|-------------------|
| `blur`  | Programmatically closes picker. | function | No       | Android  | No                |
| `focus` | Programmatically opens picker.  | function | No       | Android  | No                |

## 6. APIs

## 7. Known Issues

- [ ] The `numberOfLines` property is not supported.[issue#2](https://github.com/react-native-oh-library/picker/issues/2)
- [ ] `color` and `fontFamily` in `PickerItemProps` are not supported.(OpenHarmony's Picker component does not support styling individual `PickerItem` separately.) [issue#21](https://github.com/react-native-oh-library/picker/issues/21)
- [ ] The `themeVariant` property is not supported. [issue#22](https://github.com/react-native-oh-library/picker/issues/22)
- [ ] `itemStyle` does not support setting `textAlign`.(Not supported by OpenHarmony's Picker.)[issue#23](https://github.com/react-native-oh-library/picker/issues/23)

## 8. Others

## 9. License

This project is licensed under [The MIT License (MIT)](https://gitcode.com/openharmony-sig/rntpc_picker/blob/master/LICENSE).