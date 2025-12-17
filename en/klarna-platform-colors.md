> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@klarna/platform-colors</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/klarna-incubator/platform-colors">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/klarna-incubator/platform-colors/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/platform-colors)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 0.4.0-0.0.1@deprecated  | [@react-native-oh-tpl/platform-colors Releases(deprecated)](https://github.com/react-native-oh-library/platform-colors/releases) | 0.72       |
| 0.4.1             | [@react-native-ohos/platform-colors Releases](https://gitcode.com/openharmony-sig/rntpc_platform-colors/releases)   | 0.72       |
| 0.5.0             | [@react-native-ohos/platform-colors Releases](https://gitcode.com/openharmony-sig/rntpc_platform-colors/releases)   | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/platform-colors
```

#### **yarn**

```bash
yarn add @react-native-ohos/platform-colors
```

Generate resource files:

```bash
npx @react-native-ohos/platform-colors
```

> [!TIP] The first time you run the command it will prompt you which platforms you want to generate files for which will create a file with the following format:

```js
// platform-colors.config.js
module.exports = {
  prefix: "rnpc_",
  colors: {
    background: {
      light: "#000000",
      dark: "#ffffff",
    },
    text: "#696969",
    accent: "pink",
    contrasted: "#FFF0F5",
  },
  javascript: {
    typescript: true,
    outputDirectory: "src/colors/",
  },
  ios: {
    outputDirectory: "ios/app_name/Images.xcassets/",
  },
  android: {
    outputDirectory: "android/app/src/main/res/",
  },
  harmony: {
    outputDirectory: "harmony/AppScope/resources/",
  },
};
```

Now go ahead and inspect your android, ios and web folders. You should have your color definitions on each platform.

You need to re-run the command after each change to the config to update the generated files.

After generating the resource files, it is necessary to copy the two color files generated in Harmony/AppScope/resources/to the corresponding directory of the Harmony project:
- Copy harmony/AppScope/resources/base/element/color.json to harmony/entry/src/main/resources/base/element/color.json.
- Copy harmony/AppScope/resources/dark/element/color.json to harmony/entry/src/main/resources/dark/element/color.json.

```bash
npx @react-native-ohos/platform-colors
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```ts
import React from "react";
import {
  View,
  Text,
  StyleSheet,
  ScrollView,
  Image,
  ColorValue,
} from "react-native";
import { resolveColor, resolveColorSync } from "@klarna/platform-colors";
import { PlatformColor } from "react-native";

const accent = PlatformColor("rnpc_accent");

export const PlatformColorsTest = () => {
  const [asyncColor, setAsyncColor] = React.useState<ColorValue | undefined>(
    undefined
  );
  const syncColor = resolveColorSync(accent);
  React.useEffect(() => {
    resolveColor(accent).then((color) => setAsyncColor(color));
  }, []);

  return (
    <View style={{ top: 48, flex: 1 }}>
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={styles.scrollView}
      >
        <ColorRow
          label="show color of id: rnpc_background"
          color={PlatformColor("rnpc_background")}
        />
        <ColorRow
          label="get 'ohos_id_color_warning' color by resolveColor api"
          color={asyncColor}
        />
        <ColorRow
          label="get 'ohos_id_color_warning' color by resolveColorSync api"
          color={syncColor}
        />
      </ScrollView>
    </View>
  );
};
const ColorRow = ({ label, color }: { label: string; color?: ColorValue }) => (
  <View style={styles.colorRow}>
    <View
      style={[
        styles.colorSample,
        {
          backgroundColor: color,
        },
      ]}
    />
    <Text style={styles.colorLabel}>{label}</Text>
  </View>
);
const styles = StyleSheet.create({
  scrollView: {
    flex: 1,
    paddingHorizontal: 10,
  },
  colorRow: {
    paddingHorizontal: 10,
    marginVertical: 10,
    flexDirection: "row",
    alignItems: "center",
  },
  colorSample: {
    width: 50,
    height: 50,
    borderRadius: 25,
    marginRight: 10,
    shadowOpacity: 0.2,
    shadowColor: "#999",
    shadowRadius: 1,
    shadowOffset: { width: 0, height: 0 },
  },
});
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~0.5.0                               |  No                   |  0.77                |
| ~0.4.1                               |  Yes                  |  0.72                |
| <= 0.4.0-0.0.1@deprecated            |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

If the version you use supports Autolink and the project has been connected to Autolink, skip the ManualLink configuration.
<details>
  <summary>ManualLink: this step is a guide to manually configure native dependencies.</summary>

First, use DevEco Studio to open the HarmonyOS project `harmony` in the project directory.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/platform-colors": "file:../../node_modules/@react-native-ohos/platform-colors/harmony/platform_colors.har"
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

### 3. Introducing RNPlatformColorsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNPlatformColorsPackage } from '@react-native-ohos/platform-colors/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNPlatformColorsPackage(ctx)
  ];
}
```

### 4. Configure CMakeLists and import RNPlatformColorsPackage

> If you are using version <= 0.4.0-0.0.1, please skip this chapter.

open `entry/src/main/cpp/CMakeLists.txt`，add：

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/platform-colors/src/main/cpp" ./platform_colors)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_platform_colors)
# RNOH_END: manual_package_linking_2
```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNPlatformColorsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNPlatformColorsPackage>(ctx)
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

## Properties

### platform-colors.config.js configuration files Properties

> details [@klarna/platform-colors documentation](https://github.com/klarna-incubator/platform-colors)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name       | Description                                                                                                                                                                           | Type   | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| prefix     | We prefix all colors with rnpc\_ by default, you can override that with this option.                                                                                                  | String | No       | iOS/Android | Yes               |
| colors     | An object where the key is the color name, and the value is either a string or an object containing light and optionally highContrastLight, dark & highContrastDark properties.       | Object | Yes      | iOS/Android | Yes               |
| ios        | An object containing outputDirectory which should be an .xcassets directory.                                                                                                          | Object | No       | iOS/Android | Yes               |
| android    | An object containing outputDirectory which should be an Android res directory.                                                                                                        | Object | No       | iOS/Android | Yes               |
| harmony    | An object containing outputDirectory which should be an Harmony res directory.                                                                                                        | Object | No       | --          | Yes               |
| css        | An object containing outputDirectory and filename which should be a directory where you store CSS files and if you want to change the default filename from colors.css.               | Object | No       | iOS/Android | Yes               |
| javascript | An object containing outputDirectory which should be a directory where you store your Type/JavaScript files and typescript which is set to true if you want the output in TypeScript. | Object | No       | iOS/Android | Yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description                          | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------ | -------- | -------- | ----------- | ----------------- |
| resolveColorSync | Getting hex value from dynamic color | Function | No       | iOS/Android | Yes               |
| resolveColor     | Getting hex value from dynamic color | Function | No       | iOS/Android | Yes               |

### resolveColorSync

```js
resolveColorSync(color: ColorValue): string;
```

| Name  | Description                                                                                                        | Type             | Required | Platform    | HarmonyOS Support |
| ----- | ------------------------------------------------------------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| color | Color value obtained through the PlatformColor interface.<br>Example: resolveColorSync(PlatformColor('coloeName')) | React.ColorValue | Yes      | iOS/Android | Yes               |

### resolveColor

```js
resolveColor(color: ColorValue): Promise<string>;
```

| Name  | Description                                                                                                    | Type             | Required | Platform    | HarmonyOS Support |
| ----- | -------------------------------------------------------------------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| color | Color value obtained through the PlatformColor interface.<br>Example: resolveColor(PlatformColor('coloeName')) | React.ColorValue | Yes      | iOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [Apache License 2.0](https://github.com/klarna-incubator/platform-colors/blob/master/LICENSE).
