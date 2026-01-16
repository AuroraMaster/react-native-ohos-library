> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-localize</code></h1>
</p>
<p align="center">
    <a href="https://github.com/zoontek/react-native-localize">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-localize/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-localize)

Find the matching version information in the release address of a third-party library:

| Version                        | Package Name                                  | Repository                                                   | Release                                                      | RN Version |
| ------------------------------ | --------------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------------------- |
| <= 3.1.0-0.0.1@deprecated | @react-native-oh-tpl/react-native-localize | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-localize) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-localize/releases) | 0.72 |
| 3.1.0 | @react-native-ohos/react-native-localize | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-localize) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/releases) | 0.72 |
| 3.4.2                        | @react-native-ohos/react-native-localize       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-localize) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/releases) | 0.77 |
| 3.6.2                        | @react-native-ohos/react-native-localize       | [GitCode](https://gitcode.com/openharmony-sig/rntpc_react-native-localize) | [GitCode Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/releases) | 0.82 |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

## Installation and Usage

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-localize
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-localize
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```jsx
import * as React from "react";
import {
  I18nManager,
  Platform,
  SafeAreaView,
  ScrollView,
  StyleSheet,
  Text,
  View,
} from "react-native";
import * as RNLocalize from "react-native-localize";

const styles = StyleSheet.create({
  safeArea: {
    backgroundColor: "white",
    flex: 1,
  },
  container: {
    padding: 16,
    alignItems: "flex-start",
  },
  block: {
    marginBottom: 16,
    alignItems: "flex-start",
  },
  name: {
    textDecorationLine: "underline",
    fontWeight: "500",
    marginBottom: 8,
    color: "black",
  },
  value: {
    textAlign: "left",
    color: "black",
  },
});

const Line = ({ name, value }: { name: string; value: unknown }) => (
  <View style={styles.block}>
    <Text style={styles.name}>{name}</Text>
    <Text style={styles.value}>{JSON.stringify(value, null, 2)}</Text>
  </View>
);
function LocalizeDemo() {
  return (
    <SafeAreaView style={styles.safeArea}>
      <ScrollView contentContainerStyle={styles.container}>
        <Line name="RNLocalize.getLocales()" value={RNLocalize.getLocales()} />

        <Line name="RNLocalize.getCurrencies()" value={RNLocalize.getCurrencies()} />

        <Line name="RNLocalize.getCountry()" value={RNLocalize.getCountry()} />

        <Line name="RNLocalize.getCalendar()" value={RNLocalize.getCalendar()} />

        <Line name="RNLocalize.getTimeZone()" value={RNLocalize.getTimeZone()} />

        <Line name="RNLocalize.uses24HourClock()" value={RNLocalize.uses24HourClock()} />

        <Line
          name="RNLocalize.findBestLanguageTag(['en-US', 'en', 'fr', 'zh'])"
          value={RNLocalize.findBestLanguageTag(["en-US", "en", "fr", 'zh'])}
        />
      </ScrollView>
    </SafeAreaView>
  );
}
export default LocalizeDemo;
```

## Use Codegen

Version > @react-native-ohos/react-native-localize@3.1.0, compatible with codegen-lib for generating bridge code.

This repository has been adapted to `Codegen`. You need to actively execute the generation of third-party library bridge code before using it. For details, see [Codegen Usage Guide](/en/codegen.md).

**Note:** 0.77 does not require Codegen execution.

## Link

Version > @react-native-ohos/react-native-localize@3.1.0 now supports Autolink without requiring manual configuration.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

Version <= @react-native-oh-tpl/react-native-localize@3.1.0-0.0.1@deprecated does not support AutoLink. Therefore, you need to manually configure the linking.

First, open the `harmony` directory of the HarmonyOS project in DevEco Studio.

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
    "@react-native-ohos/react-native-localize": "file:../../node_modules/@react-native-ohos/react-native-localize/harmony/rn_localize.har"
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

### 3. Configuring CMakeLists and Introducing RNLocalizePackage (Only for 0.77)

```diff
...

project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-localize/src/main/cpp" ./rn_localize)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_localize)
# RNOH_BEGIN: manual_package_linking_2
```

Open the `entry/src/main/cpp/PackageProvider.cpp` file and add:

```diff
#include "RNOH/PackageProvider.h"
+ #include "RNLocalizePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<RNLocalizePackage>(ctx)
}
```

### 4. Introducing RNLocalizePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNLocalizePackage } from '@react-native-ohos/react-native-localize/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNLocalizePackage(ctx)
  ];
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

The following versions have been verified:

1. RNOH:0.72.28; SDK:HarmonyOS NEXT DB2; IDE:DevEco Studio 5.0.3.500; ROM:3.0.0.28;
2. RNOH: 0.77.1;SDK:HarmonyOS  5.1.1.208 (API Version 19 Release) ;IDE:DevEco Studio:5.1.1.830; ROM: HarmonyOS 6.0.0.112 SP12;
3. RNOH: 0.82.1; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0 Release; ROM:6.0.0.858;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                                     | Description                                                  | Required | Platform | HarmonyOS Support |
| ---------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| getLocales()                             | Returns the user preferred locales, in order.                | No       | All      | yes               |
| getNumberFormatSettings()                | Returns number formatting settings.                          | No       | All      | yes               |
| getCurrencies()                          | Returns the user preferred currency codes, in order.         | No       | All      | yes               |
| getCountry()                             | Returns the user current country code (based on its device locale, not on its position). | No       | All      | yes               |
| getCalendar()                            | Returns the user preferred calendar format.                  | No       | All      | yes               |
| getTemperatureUnit()                     | Returns the user preferred temperature unit.                 | No       | All      | No                |
| getTimeZone()                            | Returns the user preferred timezone (based on its device settings, not on its position). | No       | All      | yes               |
| uses24HourClock()                        | Returns true if the user prefers 24h clock format, false if they prefer 12h clock format. | No       | All      | yes               |
| usesMetricSystem()                       | Returns true if the user prefers metric measure system, false if they prefer imperial. | No       | All      | No                |
| usesAutoDateAndTime()                    | Tells if the automatic date & time setting is enabled on the phone. Android only | No       | Android  | No                |
| usesAutoTimeZone()                       | Tells if the automatic time zone setting is enabled on the phone. Android only | No       | Android  | No                |
| findBestLanguageTag()                    | Returns the best language tag possible and its reading direction | No       | All      | yes               |
| openAppLanguageSettings<sup>3.4.2+</sup> | Open the application language settings              | No       | Android  | No                |
| ServerLanguagesProvider() | Server-side language configuration provider component, used to inject language lists in server-side rendering scenarios              | No       | Web  | No                |
| useLocalize() | Return the API collection related to localization              | No       | All  | yes                |

## Known Issues
- [ ]  Temperature and length units cannot be obtained in HarmonyOS  [issue#2](https://github.com/react-native-oh-library/react-native-localize/issues/2)
- [ ]  SSR (Web-only) features (`ServerLanguagesProvider`/SSR logic of `useLocalize`) are not supported on HarmonyOS[issue#13](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/issues/13)
- [ ]  Expo config plugin for react-native-localize is not supported on HarmonyOS. HarmonyOS does not integrate with Expo's build/config system[issue#14](https://gitcode.com/openharmony-sig/rntpc_react-native-localize/issues/14)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/zoontek/react-native-localize/blob/master/LICENSE).