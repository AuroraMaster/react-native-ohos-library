> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-immersive</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mockingbot/react-native-immersive">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20hormony-blue
" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mockingbot/react-native-immersive/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-immersive)

Find the matching version information in the release address of the third-party library:：

| version | Package name                              | Releases info                                                | Support RN version |
| ------- | ----------------------------------------- | ------------------------------------------------------------ | ------------------ |
| 2.1.0   | @react-native-ohos/react-native-immersive | [@react-native-ohos/react-native-immersive Releases](https://github.com/react-native-oh-library/react-native-immersive/releases) | 0.72/0.77          |

Go to the project directory and execute the following instruction:

## Installation and Usage



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-immersive
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-immersive
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from 'react'
import { AppRegistry, StyleSheet, Text, View, Button, TextInput, Alert, Modal } from 'react-native'
import { Immersive } from 'react-native-immersive'

class testReactNative extends Component {
  constructor (props) {
    super(props)
    
    Immersive.getImmersive().then((immersiveState) => {
        console.log('init [getImmersiveState]', immersiveState)
        this.setState({ immersiveState,isImmersive: immersiveState.isImmersiveOn })
        if(immersiveState.isImmersiveOn){
          Immersive.on()
        }
      }).catch((err) => {
        console.error('[getImmersiveState] error', err)
   })

    this.setImmersiveOn = () => {
      let startTime = Date.now();
      Immersive.on()
      let endTime = Date.now();
      console.log("react-native-immersive on time:", endTime - startTime, "ms");
      this.setState({ isImmersive: true })
    }
    this.setImmersiveOff = () => {
      let startTime = Date.now();
      Immersive.off()
      let endTime = Date.now();
      console.log("react-native-immersive off time:", endTime - startTime, "ms");
      this.setState({ isImmersive: false })
    }
    this.setImmersiveTrue = () => {
      let startTime = Date.now();
      Immersive.setImmersive(true)
      let endTime = Date.now();
      console.log("react-native-immersive setImmersive time:", endTime - startTime, "ms");
      this.setState({ isImmersive: true })
    }
    this.setImmersiveFalse = () => {
      Immersive.setImmersive(false)
      this.setState({ isImmersive: false })
    }
    this.addImmersiveListener = () => {
      if(!this.state.isAddListener){
        console.log("Immersive---------> addImmersiveListener",this.restoreImmersive);
        let startTime = Date.now();
        Immersive.addImmersiveListener(this.restoreImmersive)
        let endTime = Date.now();
        console.log("react-native-immersive addImmersiveListener time:", endTime - startTime, "ms");
        this.setState({ isAddListener: true })
      }
    }
    this.removeImmersiveListener = () => {
      if(this.state.isAddListener){
        console.log("Immersive---------> removeImmersiveListener",this.restoreImmersive);
        let startTime = Date.now();
        Immersive.removeImmersiveListener(this.restoreImmersive)
        let endTime = Date.now();
        console.log("react-native-immersive removeImmersiveListener time:", endTime - startTime, "ms");
        this.setState({ isAddListener: false })
      }
    }

  
    this.getImmersiveState = () => {
      let startTime = Date.now();
      Immersive.getImmersive().then((immersiveState) => {
        let endTime = Date.now();
        console.log("react-native-immersive getImmersive time:", endTime - startTime, "ms");
        console.log('[getImmersiveState]', immersiveState)
        this.setState({ immersiveState })
      }).catch((err) => {
        console.error('[getImmersiveState] error', err)
      })
    }

    this.restoreImmersive = () => {
      Alert.alert("Callback","The registered listener callback has been invoked")
    }

    this.state = {
      isAddListener: false,
      isImmersive: false,
      isRestoreImmersive: true,
      immersiveState: null
    }
  }

  render () {
    const { isImmersive, immersiveState } = this.state
    return (
      <View style={{margin: 16}}>
            <Button onPress={this.addImmersiveListener} title="addImmersiveListener" />
            <View style={{ marginTop: 10, marginBottom: 10 }}>
                <Button style={{marginTop: 10, marginBottom: 10}} onPress={this.removeImmersiveListener} title="removeImmersiveListener" />
            </View>
            <Button onPress={isImmersive ? this.setImmersiveOff : this.setImmersiveOn} title="on/off" />
            <Text style={styles.text}>isImmersive: {JSON.stringify(isImmersive)}</Text>
            <View style={{ marginTop: 10, marginBottom: 10 }}>
              <Button onPress={isImmersive ? this.setImmersiveFalse : this.setImmersiveTrue} title="setImmersive" />
            <Text style={styles.text}>isImmersive: {JSON.stringify(isImmersive)}</Text>
            </View>
            <Button onPress={this.getImmersiveState} title="getImmersive" />
            <Text style={styles.text}>immersiveState: {JSON.stringify(immersiveState)}</Text>
      </View>
    )
  }
}

const styles = StyleSheet.create({
  container: { flex: 1, padding: 24 },
  containerTest: { alignItems: 'stretch', justifyContent: 'center', flex: 1 },
  text: { textAlign: 'center', fontSize: 14 }
})

export default testReactNative;
AppRegistry.registerComponent('testReactNative', () => testReactNative)
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
   ...
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-immersive": "file:../../node_modules/@react-native-ohos/react-native-immersive/harmony/immersive.har",
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

### 3. Configuring CMakeLists and Introducing RNCVideoPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-immersive/src/main/cpp" ./rnoh_immersive)

# RNOH_BEGIN: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_immersive)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNImmersivePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNImmersivePackage>(ctx)
    };
}
```

### 4.Introducing RNCVideoPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNImmersivePackage } from '@react-native-ohos/react-native-immersive/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImmersivePackage(ctx)
  ];
}
```

### 5.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 6.Constraints

Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.79; SDK: HarmonyOS 5.1.1 Release SDK; IDE: DevEco Studio 5.1.1 Release; ROM: 5.0.1.120;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;


## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of Android.

| Name                      | Description             | Type     | Required | Platform | HarmonyOS Support |
| ------------------------- | ----------------------- | -------- | -------- | -------- | ----------------- |
| `on()`                    | Set to full screen      | function | No       | Android  | yes               |
| `off()`                   | Turn off full screen    | function | No       | Android  | yes               |
| `setImmersive()`          | Set to full-screen mode | function | No       | Android  | yes               |
| `getImmersive()`          | Get full-screen status  | function | No       | Android  | yes               |
| `addImmersiveListener()`  | Add listening           | function | No       | Android  | yes               |
| removeImmersiveListener() | Cancel monitoring       | function | No       | Android  | yes               |

## Known Issues

## Others

## License

This project is licensed under  [The MIT License (MIT)](https://github.com/mockingbot/react-native-immersive/blob/master/LICENSE) .