> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-text-size</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/aMarCruz/react-native-text-size">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/aMarCruz/react-native-text-size/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-BSD-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-text-size)

## Installation and Usage

Find the matching version information in the release address of a third-party library:

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 4.0.0-0.0.11@deprecated     | [@react-native-oh-tpl/react-native-text-size Releases(deprecated)](https://github.com/react-native-oh-library/react-native-text-size/releases) | 0.72       |
| 4.0.1                | [@react-native-ohos/react-native-text-size Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-text-size/releases) | 0.72       |
| 4.1.0                | [@react-native-ohos/react-native-text-size Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-text-size/releases) | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-text-size
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-text-size
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from 'react';
import {
  ScrollView,
  Text,
  View,
  Dimensions,
  TextInput
} from 'react-native';

import RTNTextSize, { TSFontSpecs, TSFontInfo } from 'react-native-text-size'

export default function TextSizeExample() {
  const [res, setRes] = useState<string[]>([])
  const [res2, setRes2] = useState<string[]>([])
  const fontFamily = 'HarmonyOS Sans SC'
  const [texts, setTexts] = useState<string>('I rnTextSize ❤️')
  const [texts3, setTexts3] = useState<string>('')
  const [width, setWidth] = useState<number>();
  const [height, setHeight] = useState<number>();
  const fontSpecs: TSFontSpecs = {
    fontFamily: undefined,
    fontSize: 20,
    fontStyle: 'normal',
    fontWeight: '700',
  }
  type State = { heights2: number[] }
  const [texts2, setTexts2] = useState(['I ❤️ rnTextSize', 'I ❤️ rnTextSize using flatHeights', 'Thx for flatHeights', 'test123',])
  const [heights2, setHeights2] = useState<number[]>([]);
  const fontSpecs2: TSFontSpecs = {
    fontFamily: undefined,
    fontSize: 20,
    fontStyle: 'italic',
    fontWeight: 'bold',
  }
  const [key, setKey] = useState({})
  const [info, setInfo] = useState<TSFontInfo>()
  const fontSpecs3: TSFontSpecs = {
    fontFamily: 'harmony',
    textBreakStrategy: 'balanced',
  }

  useEffect(() => {
    const myFun = async () => {
      const resp = await RTNTextSize.fontFamilyNames();
      setRes(resp)

      const resp2 = await RTNTextSize.fontNamesForFamilyName(fontFamily);
      setRes2(resp2)

      setTexts(texts)
      const width = Dimensions.get('window').width * 0.8
      const newHeights = await RTNTextSize.measure({
        text: texts,      // array of texts to measure, can include symbols
        width: width,            // max-width of the "virtual" container
        ...fontSpecs,     // RN font specification
      })
      setHeight(newHeights.height);
      setWidth(newHeights.width)

      setTexts2(texts2)
      const width2 = Dimensions.get('window').width * 0.8
      const newHeights2 = await RTNTextSize.flatHeights({
        text: texts2,      // array of texts to measure, can include symbols
        width: width2,            // max-width of the "virtual" container
        ...fontSpecs2,     // RN font specification
      })
      setHeights2(newHeights2);

      const keyp = await RTNTextSize.specsForTextStyles();
      setKey(keyp)

      const infos = await RTNTextSize.fontFromSpecs(fontSpecs3);
      setInfo(infos)
    }
    myFun()
  }, [])

  return (
    <ScrollView style={{ flexGrow: 1 }}>
      <View style={{ paddingLeft: 12, paddingRight: 12 }}>
        <Text>
         measure:[fontFamily: undefined,fontSize: 20,fontStyle: 'normal', fontWeight: '700']
        </Text>
        <Text style={{
          width: width,
          height: height,
          ...fontSpecs
        }}>
          {texts}
        </Text>
        <TextInput
          value={texts}
          onChangeText={value => { setTexts(value) }}
          style={{ width: '100%', height: 28, borderWidth: 2, borderColor: 'black' }}
        />

        <Text>
          flatHeights:[fontFamily: undefined,fontSize: 20,fontStyle: 'italic', fontWeight: 'bold']
        </Text>
        {texts2.map(
          (texts2, index) => (
            <Text key = {index} style={{ height: heights2[index], ...fontSpecs2 }}>
              {texts2}
            </Text>
          )
        )}
        <TextInput
          value = {texts3}
          onChangeText={value => {
            let value2 =value.split(",");
            setTexts3(value)
            setTexts2(value2)
          }}
          style={{ width: '100%', height: 28, borderWidth: 2, borderColor: 'black' }}
        />
        <Text>
          specsForTextStyles: Obtains the default font information.
        </Text>
        <Text>
          {JSON.stringify(key)}
        </Text>
        <Text>
          fontFamilyNames: Obtains the default fonts.
        </Text>
        <Text>
          {res}
        </Text>
        <Text>
          fontNamesForFamilyName: Obtains the property of the system font.
        </Text>
        <Text>
          {res2}
        </Text>
        <Text>
          fontFromSpecs: Returns the font features obtained from the given specification.
        </Text>
        <Text>
          {JSON.stringify(info)}
        </Text>
      </View>
    </ScrollView>
  )
}
```

## Link

|                            | is supporte autolink  | Supported RN Version |
|----------------------------|-----------------------|----------------------|
| ~4.1.0                     |  No                   |  0.77                |
| ~4.0.1                     |  Yes                  |  0.72                |
| <= 4.0.0-0.0.11@deprecated |  No                   |  0.72                |

Using AutoLink need to be configured according to this document, Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md.

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
    "@react-native-ohos/react-native-text-size": "file:../../node_modules/@react-native-ohos/react-native-text-size/harmony/text_size.har"
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

### 3. Configuring CMakeLists and Introducing RNTextSizePackage

> If you are using version <= 4.0.0-0.0.11, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-text-size/src/main/cpp" ./text_size)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_text_size)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
...
+ #include "RNTextSizePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      ...
+     std::make_shared<RNTextSizePackage>(ctx)
    };
}
```

### 4.Introducing RNTextSizePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNTextSizePackage } from '@react-native-ohos/react-native-text-size/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    ...
+   new RNTextSizePackage(ctx)
  ];
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


## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!TIP] 参数信息查看 [Github 地址](https://github.com/aMarCruz/react-native-text-size?tab=readme-ov-file#api)

| Name                   | Description                                                                     | Type                            | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------- | ------------------------------- | -------- | -------- | ----------------- |
| measure                | Measurement Text                                                                | TSMeasureResult                 | No       | All      | partially               |
| flatHeights            | Measurement Text                                                                | number[]                        | No       | All      | yes               |
| specsForTextStyles     | Get system font information for the running OS                                  | {[key: string]: TSFontForStyle} | No       | All      | yes               |
| fontFromSpecs          | Returns the characteristics of the font obtained from the given specifications. | TSFontInfo                      | No       | All      | yes               |
| fontFamilyNames        | Returns a Promise for an array of font family names available on the system     | string[]                        | No       | All      | yes               |
| fontNamesForFamilyName | Return the data of the corresponding font according to the name                 | string[]                        | No       | All      | yes               |


## Known Issues

- [ ] **fontFamilyNames** and **fontNamesForFamilyName** issues: The JSON file in the **font** directory of the mobile phone is required. Currently, the JSON file is not preset in the mobile phone directory, which will cause the API call to return null. This issue will be resolved on the bottom-layer framework side: [issue#1](https://github.com/react-native-oh-library/react-native-text-size/issues/1)
- [ ] The **measure** method does not return **lineInfo**: [issue#2](https://github.com/react-native-oh-library/react-native-text-size/issues/8).

## Others

## License

This project is licensed under [The BSD 2-Clause License（BSD）](https://github.com/aMarCruz/react-native-text-size/blob/master/LICENSE).
