> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-network-info</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/pusherman/react-native-network-info">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/pusherman/react-native-network-info/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-network-info)

## Installation and Usage

Find the matching version information in the release address of a third-party library:

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 5.2.1-0.0.1@deprecated     | [@react-native-oh-tpl/react-native-network-info Releases(deprecated)](https://github.com/react-native-oh-library/react-native-network-info/releases) | 0.72       |
| 5.2.2                | [@react-native-ohos/react-native-network-info Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-network-info/releases) | 0.72       |
| 5.3.0                | [@react-native-ohos/react-native-network-info Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-network-info/releases) | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-network-info
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-network-info
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, {useState} from 'react';
import {
  View,
  Text,
  StyleSheet,
  ScrollView,
  TouchableOpacity,
} from 'react-native';
import {NetworkInfo} from 'react-native-network-info';

interface NetworkInfoState {
  ipAddress: string | null;
  ipv4Address: string | null;
  broadcast: string | null;
  ssid: string | null;
  bssid: string | null;
  subnet: string | null;
  defaultGateway: string | null;
  frequency: number | null;
}

export default NetworkInfoDemo(): JSX.Element {
  const [info, setInfo] = useState<NetworkInfoState>({
    ipAddress: '',
    ipv4Address: '',
    broadcast: '',
    ssid: '',
    bssid: '',
    subnet: '',
    defaultGateway: '',
    frequency: 0,
  });

  return (
    <ScrollView style={styles.container}>
      <View style={styles.infoContainer}>
        <TouchableOpacity
          onPress={async () => {
            const value = await NetworkInfo.getIPAddress();
            setInfo({...info, ipAddress: value});
          }}>
          <Text style={styles.button}>ipAddress</Text>
        </TouchableOpacity>
        <Text style={styles.infoText}>{`${info.ipAddress}`}</Text>
      </View>

      <View style={styles.infoContainer}>
        <TouchableOpacity
          onPress={async () => {
            const value = await NetworkInfo.getIPV4Address();
            setInfo({...info, ipv4Address: value});
          }}>
          <Text style={styles.button}>ipv4Address</Text>
        </TouchableOpacity>
        <Text style={styles.infoText}>{`${info.ipv4Address}`}</Text>
      </View>

      <View style={styles.infoContainer}>
        <TouchableOpacity
          onPress={async () => {
            const value = await NetworkInfo.getBroadcast();
            setInfo({...info, broadcast: value});
          }}>
          <Text style={styles.button}>broadcast</Text>
        </TouchableOpacity>
        <Text style={styles.infoText}>{`${info.broadcast}`}</Text>
      </View>

      <View style={styles.infoContainer}>
        <TouchableOpacity
          onPress={async () => {
            const value = await NetworkInfo.getSSID();
            setInfo({...info, ssid: value});
          }}>
          <Text style={styles.button}>ssid</Text>
        </TouchableOpacity>
        <Text style={styles.infoText}>{`${info.ssid}`}</Text>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
  },
  infoContainer: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginBottom: 10,
  },
  infoText: {
    fontSize: 16,
  },
  button: {
    paddingVertical: 6,
    paddingHorizontal: 12,
    backgroundColor: 'hsl(193, 95%, 68%)',
    borderWidth: 2,
    borderColor: 'hsl(193, 95%, 30%)',
    borderRadius: 4,
  },
});

```

## Use Codegen

Version >= @react-native-ohos/react-native-network-info@5.2.2, compatible with codegen-lib for generating bridge code.

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Version >= @react-native-ohos/react-native-network-info@5.2.2 now supports Autolink without requiring manual configuration, currently only supports 72 frameworks.
Autolink Framework Guide Documentation: https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md

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

### 2.  Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-network-info": "file:../../node_modules/@react-native-ohos/react-native-network-info/harmony/rn_network_info.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configure CMakeLists and Introduce RNOrientationPackage

> If you are using version <= 5.2.1-0.0.1, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt`，Add：  

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-network-info/src/main/cpp" ./rn_network_info)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_network_info)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp`，Add：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "NetworkInfoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<NetworkInfoPackage>(ctx),
    };
}
```

### 4. In ArkTs, Introduce RNNetworkInfoPackage

Open `entry/src/main/ets/RNPackagesFactory.ts`，Add：

```diff
  ...
+  import { RNNetworkInfoPackage } from '@react-native-ohos/react-native-network-info/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNNetworkInfoPackage(ctx)
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

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### Permission Requirements

Add permissions for WiFi and network information in the module.json5 file under the entry directory.

Open the `entry/src/main/module.json5` file and add the following code:

```json
...
"requestPermissions": [
    {
    "name" : "ohos.permission.GET_WIFI_INFO"
    },
    {
    "name": "ohos.permission.GET_NETWORK_INFO"
    }
]
```

## Static Methods

> [!TIP]The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP]If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                         | Type     | Required | Platform | HarmonyOS Support |
| ------------------- | --------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| getSSID             | Get SSID                                            | Function | no       | All      | yes               |
| getBSSID            | Get BSSID                                           | Function | no       | All      | yes               |
| getBroadcast        | Get Broadcast                                       | Function | no       | All      | yes               |
| getIPAddress        | Get Local IP                                        | Function | no       | All      | yes               |
| getIPV4Address      | Get IPv4 IP (priority: WiFi first, cellular second) | Function | no       | All      | yes               |
| getSubnet           | Get Subnet                                          | Function | no       | All      | yes               |
| getGatewayIPAddress | Get Default Gateway IP                              | Function | no       | All      | yes               |
| getFrequency        | Get frequency                                       | Function | no       | Android  | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/pusherman/react-native-network-info/blob/master/LICENSE).
