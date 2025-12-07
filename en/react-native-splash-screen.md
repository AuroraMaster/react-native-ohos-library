> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-splash-screen</code> </h1>
</p>

 [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-splash-screen)

## 1. Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                                                                                                    | Supported RN Version |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| <= 3.3.0-0.0.2@deprecated            | [@react-native-oh-tpl/react-native-splash-screen Releases(deprecated)](https://github.com/react-native-oh-library/react-native-splash-screen/releases) | 0.72       |
| 3.3.1                       | [@react-native-ohos/react-native-splash-screen Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-splash-screen/releases)                | 0.72       |
| 3.4.0                       | [@react-native-ohos/react-native-splash-screen Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-splash-screen/releases)                | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-splash-screen
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-splash-screen
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.


##### **Create a launch page `SplashScreenPage.ets` in the entry/src/main/ets/pages directory**

```ets
import { SplashScreenView } from '@react-native-ohos/react-native-splash-screen/src/main/ets/SplashScreenView'

@Entry
@Component
export struct SplashScreenPage {
  build() {
    Row() {
      SplashScreenView();
    }
  }
}
```

##### **Add `pages/SplashScreenPage` in entry/src/resources/base/profile/main_pages.json**
```json
{
  "src": [
    "pages/SplashScreenPage"
  ]
}
```

##### **Open the `entry/src/main/ets/entryability/EntryAbility.ets` file and add the following code:**
```ets
import window from '@ohos.window';
import { SplashScreen } from '@react-native-ohos/react-native-splash-screen/src/main/ets/SplashScreen'

export default class EntryAbility extends RNAbility {
  onWindowStageCreate(windowStage: window.WindowStage): void {
    let startWindowIcon = $r('app.media.splashIcon'); // 启动页图片（用户改成自己 App 的启动图片，一般在 entry/src/main/resources/base/media 文件夹中）
    let startWindowBackground = "#FFFFFF"; // 启动页背景色
    let startPageUrl = 'pages/SplashScreenPage'; // 启动页
    SplashScreen.show(this.context, windowStage, startWindowIcon, startWindowBackground, startPageUrl).then(() => {
      super.onWindowStageCreate(windowStage);
    })
  }
}
```

##### Close the launch screen at the appropriate time (e.g., after initialization is complete).
```ets
import SplashScreen from 'react-native-splash-screen';
export default class WelcomePage extends Component {
    componentDidMount() {
        SplashScreen.hide(); // close launch screen
    }
}
```

## 2. Use Codegen

Version >= @react-native-ohos/react-native-splash-screen@3.3.1, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## 3. Manual Link

Version >= @react-native-ohos/react-native-splash-screen@3.3.1 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks. Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 3.1. Overrides RN SDK

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

### 3.2. Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/react-native-splash-screen": "file:../../node_modules/@react-native-ohos/react-native-splash-screen/harmony/splash_screen.har"
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

### 3.3. Configuring CMakeLists and Introducing SplashScreenPackage

> If you are using version <= 3.3.0-0.0.2, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:


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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-splash-screen/src/main/cpp" ./splash_screen)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_splash_screen)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
+ #include "SplashScreenPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<SplashScreenPackage>(ctx)
}
```

### 3.4. Introducing  SplashScreenPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {SplashScreenPackage} from '@react-native-ohos/react-native-splash-screen/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SplashScreenPackage(ctx)
  ];
}
```

### 3.5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

The following code demonstrates the basic usage scenario of this library:

```jsx
import React from 'react';
import { Text, View } from 'react-native';
import SplashScreen from 'react-native-splash-screen';

class App extends React.Component {
  componentDidMount() {
    SplashScreen.hide();
  }

  render() {
    return (
      <View style={{
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center'
      }}>
        <Text>Hello, world!</Text>
      </View>
    )
  }
}

export default App;

```

## 4. Constraints

### 4.1. Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## 5. API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name                                                                                                                                 | Description | Type | Required | Platform | HarmonyOS Support|
|--------------------------------------------------------------------------------------------------------------------------------------| ----- | ----- | ----- | ----- | -----|
|show()                                                                                                                               | 显示启动屏幕(原生方法) | function | Yes | iOS | No  |
|show(abilityContext: UIAbilityContext, windowStage: window.WindowStage, iconResource: any, backgroundColor: string, pageUrl: string) | 显示启动屏幕(原生方法) | function | Yes | iOS/Android | Yes  |
| hide()                                                                                                                               | 隐藏启动屏幕 | function | Yes | iOS/Android | Yes | 


> [!TIP] **show(abilityContext: UIAbilityContext, windowStage: window.WindowStage, iconResource: any, backgroundColor: string, pageUrl: string) 方法的参数说明：**

| Name                                                      | Description                                                                                                         | Type     |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- |
| abilityContext | 应用上下文 | UIAbilityContext |
| windowStage | 窗口管理器 | window.WindowStage |
| iconResource | 启动页图片 | Resource |
| backgroundColor | 启动页背景色 | string |
| pageUrl | 首页路由 | bool |

## 6. Known Issues

## 7. Others

- In iOS, the working principle of the show() method is as follows: In the entry application method, the home page of the App is first loaded, and then a while loop is used to keep the interface on the App's splash screen. During this time, the home page still loads asynchronously. Once the loading is complete, stopping the while loop will hide the splash screen and display the home page.
  In HarmonyOS, the home page is loaded by calling windowStage.loadContent in the entry onWindowStageCreate method. If a while loop is used at this point, the home page cannot be loaded asynchronously.

## 8. License

This project is licensed under [The MIT License (MIT)](https://github.com/crazycodeboy/react-native-splash-screen/blob/v3.3.0/LICENSE).