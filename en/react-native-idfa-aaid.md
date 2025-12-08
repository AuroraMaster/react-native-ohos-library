> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-idfa-aaid</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-idfa-aaid)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                                                                                                    | Supported RN Version |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| <=1.2.0-0.0.1@deprecated | [@react-native-oh-tpl/react-native-idfa-aaid Releases(deprecated)](https://github.com/react-native-oh-library/react-native-idfa-aaid/releases) | 0.72       |
| 1.2.1      | [@react-native-ohos/react-native-idfa-aaid Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-idfa-aaid/releases)                        | 0.72       |
| 1.3.0      | [@react-native-ohos/react-native-idfa-aaid Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-idfa-aaid/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-idfa-aaid
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-idfa-aaid
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```
import React, { useEffect } from 'react';
import type { PropsWithChildren } from 'react';
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
} from 'react-native';

import {
  Colors,
  DebugInstructions,
  Header,
  LearnMoreLinks,
  ReloadInstructions,
} from 'react-native/Libraries/NewAppScreen';

import ReactNativeIdfaAaid, {
  AdvertisingInfoResponse,
} from 'react-native-idfa-aaid';

type SectionProps = PropsWithChildren<{
  title: string;
}>;

function Section({ children, title }: SectionProps): React.JSX.Element {
  const isDarkMode = useColorScheme() === 'dark';

  useEffect(() => {
    ReactNativeIdfaAaid.getAdvertisingInfo()
      .then((res: AdvertisingInfoResponse) =>
        console.log('Advertising info', res)
      )
      .catch(err => {
        console.log(err);
      });
  }, []);

  return (
    <View style={styles.sectionContainer}>
      <Text
        style={[
          styles.sectionTitle,
          {
            color: isDarkMode ? Colors.white : Colors.black,
          },
        ]}>
        {title}
      </Text>
      <Text
        style={[
          styles.sectionDescription,
          {
            color: isDarkMode ? Colors.light : Colors.dark,
          },
        ]}>
        {children}
      </Text>
    </View>
  );
}

function App(): React.JSX.Element {
  const isDarkMode = useColorScheme() === 'dark';

  const backgroundStyle = {
    backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
  };
  return (
    <SafeAreaView style={backgroundStyle}>
      <StatusBar
        barStyle={isDarkMode ? 'light-content' : 'dark-content'}
        backgroundColor={backgroundStyle.backgroundColor}
      />
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={backgroundStyle}>
        <Header />
        <View
          style={{
            backgroundColor: isDarkMode ? Colors.black : Colors.white,
          }}>
          <Section title="Step One">
            Edit <Text style={styles.highlight}>App.tsx</Text> to change this
            screen and then come back to see your edits.
          </Section>
          <Section title="See Your Changes">
            <ReloadInstructions />
          </Section>
          <Section title="Debug">
            <DebugInstructions />
          </Section>
          <Section title="Learn More">
            Read the docs to discover what to do next:
          </Section>
          <LearnMoreLinks />
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: '600',
  },
  sectionDescription: {
    marginTop: 8,
    fontSize: 18,
    fontWeight: '400',
  },
  highlight: {
    fontWeight: '700',
  },
});

export default App;
```

## Use Codegen

Version >= @react-native-ohos/react-native-idfa-aaid@1.2.1, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-idfa-aaid@1.2.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1. Use the HAR file(recommended)；
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-idfa-aaid": "file:../../node_modules/@react-native-ohos/react-native-idfa-aaid/harmony/getOaid.har"
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


### 3. Introducing GetOaidPackage Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
  
+  import { GetOaidPackage } from "@react-native-ohos/react-native-idfa-aaid/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GetOaidPackage(ctx),
  ];
}
```
### 4.Configuring CMakeLists and Introducing  IdfaAaidPackage

> If you are using version <=1.2.0-0.0.1, please skip this chapter。

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-idfa-aaid/src/main/cpp" ./getOaid)

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
+ target_link_libraries(rnoh_app PUBLIC rnoh_getOaid)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "IdfaAaidPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<IdfaAaidPackage>(ctx)
    };
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

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

The following combinations have been verified:

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### Permission Requirements (If Any)

[!TIP] 

"ohos.permission.APP_TRACKING_CONSENT"，the permission level of"ohos.permission.APP_TRACKING_CONSENT" is <B>normal</B>，and the granting method is <B>user_grant</B>[Configuration guide for using ACL signatures](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

#### Include applicable permissions in the module.json5 file within the entry directory.
在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

+    "requestPermissions":[
+      {
+        "name" : "ohos.permission.APP_TRACKING_CONSENT",
+        "reason": "$string:page_show",
+        "usedScene": {
+          "abilities": [
+            "FormAbility"
+          ],
+          "when":"always"
+        }
+     }
+    ]
  }
}
```
#### Apply the reasons for applicable permission in the entry directory.

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "page_show",
+      "value": "page from npm package"
+    }
  ]
}
```
 当前的 HarmonyOS 版本中，当用户请求 APP_TRACKING_CONSENT 权限时，系统并不会弹出授权提示框，而是默认禁止该应用获取 OAID 的权限.为了引导用户手动开启此权限，应用端可以自主设计并展示弹窗，指引用户前往设置界面进行相应的操作。此外，应用应严格按照 user_grant 权限的申请流程来提交请求，具体申请细节请参考： [user_grant （用户授权）权限列表](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/permissions-for-all-V5#user_grant%E7%94%A8%E6%88%B7%E6%8E%88%E6%9D%83%E6%9D%83%E9%99%90%E5%88%97%E8%A1%A8) 

## Static Methods (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getAdvertisingInfo  |Check the permission, apply for the permission, and obtain the OAID.         | Function  | yes | iOS/Android      | yes |
| getAdvertisingInfoAndCheckAuthorization  | The function is the same as above, and is used to keep the porting uniform.         | Function  | no | iOS/Android      | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid/blob/main/LICENSE)