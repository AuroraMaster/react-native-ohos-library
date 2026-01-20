> Template Version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-wifi-reborn</code> </h1>
</p>

Please check the release information of the corresponding version at the third-party library's Releases page:

| Third-Party Library Version | Release Information                                              | Supported RN Version |
| --------------------------- | --------------------------------------------------------------- | -------------------- |
| 0.6.1                       | [@react-native-ohos/react-native-wifi-reborn Releases](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-wifi-reborn) | 0.72                 |
| 0.7.0                       | [@react-native-ohos/react-native-wifi-reborn Releases](https://gitcode.com/OpenHarmony-RN/rntpc_react-native-wifi-reborn) | 0.77                 |

> [!TIP] [GitHub Address](https://github.com/react-native-oh-library/react-native-wifi-reborn)

## Installation and Usage

Navigate to the project directory and enter the following command:

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-wifi-reborn
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-wifi-reborn
```

<!-- tabs:end -->

The following code demonstrates the basic usage scenarios of this library:

> [!WARNING] The library name used in the import remains unchanged.

> [!TIP] # The demo uses third-party library permissions: [react-native-permissions](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-permissions.md)

### wifi-reborn example

```js
import React, { useState } from 'react';
import { ScrollView, StyleSheet, Text, TouchableOpacity, View, TextInput, Alert } from 'react-native';
import { Tester, TestSuite, TestCase } from '@rnoh/testerino';
import WifiManager from 'react-native-wifi-reborn';
import RTNPermissions, { Permission } from "react-native-permissions";

const permissionNormal: Permission[] = [
    'ohos.permission.GET_WIFI_INFO',
    'ohos.permission.SET_WIFI_INFO',
    'ohos.permission.LOCATION',
    'ohos.permission.APPROXIMATELY_LOCATION',
];

const COLORS = {
    primary: '#007AFF',
    secondary: '#5856D6',
    success: '#4CD964',
    background: '#F2F2F7',
    card: '#FFFFFF',
    text: '#000000',
    subText: '#8E8E93',
    border: '#C7C7CC',
    error: '#FF3B30',
};

const CustomButton = ({ title, onPress, color = COLORS.primary }: { title: string, onPress: () => void, color?: string }) => (
    <TouchableOpacity style={[styles.button, { backgroundColor: color }]} onPress={onPress}>
        <Text style={styles.buttonText}>{title}</Text>
    </TouchableOpacity>
);

const ResultArea = ({ text }: { text: string }) => {
    if (!text) return null;
    return (
        <View style={styles.resultContainer}>
            <Text style={styles.resultLabel}>Result:</Text>
            <Text style={styles.resultText}>{text}</Text>
        </View>
    );
};

const Description = ({ text }: { text: string }) => (
    <Text style={styles.descriptionText}>{text}</Text>
);

export const TurboLogDemoTest = () => {
    const [wifiList, setWifiList] = useState<any[]>([]);
    const [ssid, setSsid] = useState('');
    const [password, setPassword] = useState('');
    const [log, setLog] = useState('');
    const [results, setResults] = useState<{ [key: string]: string }>({});

    const addLog = (msg: string) => {
        console.info(msg);
        setLog(prev => msg + '\n' + prev);
    };

    const updateResult = (key: string, value: string) => {
        setResults(prev => ({ ...prev, [key]: value }));
        addLog(`${key}: ${value}`);
    };

    const safeStringify = (val: any) => {
        if (typeof val === 'string') return val;
        try {
            return JSON.stringify(val, null, 2);
        } catch (e) {
            return String(val);
        }
    };

      return (
        <Tester style={{ paddingBottom: 80, backgroundColor: COLORS.background }}>
            <ScrollView stickyHeaderIndices={[0]}>
                <View style={styles.headerContainer}>
                    <Text style={styles.headerTitle}>Wifi Manager Demo</Text>
                    <View style={styles.inputCard}>
                        <TextInput
                            style={styles.input}
                            placeholder="Enter SSID"
                            placeholderTextColor={COLORS.subText}
                            value={ssid}
                            onChangeText={setSsid}
                        />
                        <TextInput
                            style={styles.input}
                            placeholder="Enter Password"
                            placeholderTextColor={COLORS.subText}
                            value={password}
                            onChangeText={setPassword}
                            secureTextEntry
                        />
                    </View>
                </View>

                <TestSuite name="Permissions">
                    <TestCase title="Request Permissions">
                        <View style={styles.testCaseContent}>
                            <Description text="Request the necessary permissions (location, WiFi) for the application to run." />
                            <CustomButton
                                title="Request Permissions"
                                onPress={async () => {
                                    try {
                                        let requestMultiple = await RTNPermissions.requestMultiple(permissionNormal);
                                        updateResult("Permissions", safeStringify(requestMultiple));
                                    } catch (e) {
                                        updateResult("Permissions", "Error: " + safeStringify(e));
                                    }
                                }}
                            />
                            <ResultArea text={results["Permissions"]} />
                        </View>
                    </TestCase>
                </TestSuite>

                <TestSuite name="loadWifiList">
                    <TestCase title="loadWifiList">
                        <View style={styles.testCaseContent}>
                            <Description text="Return a list of nearby WiFi networks." />
                            <CustomButton
                                title="loadWifiList"
                                onPress={() => {
                                    WifiManager.loadWifiList().then((list: any) => {
                                        updateResult("loadWifiList", "Loaded " + list.length + " networks");
                                        setWifiList(list);
                                    }).catch((err: any) => updateResult("loadWifiList", "Error: " + safeStringify(err)));
                                }}
                            />
                            <ResultArea text={results["loadWifiList"]} />
                        </View>
                    </TestCase>
                    {wifiList.length > 0 && (
                        <View style={styles.wifiListContainer}>
                            <Text style={styles.sectionTitle}>Available Networks</Text>
                            {wifiList.map((item, index) => (
                                <TouchableOpacity
                                    key={index}
                                    style={styles.wifiItem}
                                    onPress={() => {
                                        setSsid(item.SSID);
                                        addLog("Selected SSID: " + item.SSID);
                                    }}
                                >
                                    <View style={styles.wifiItemHeader}>
                                        <Text style={styles.wifiSSID}>{item.SSID || '<Hidden>'}</Text>
                                        <Text style={styles.wifiLevel}>{item.level} dBm</Text>
                                    </View>
                                    <Text style={styles.wifiBSSID}>{item.BSSID}</Text>
                                    <Text style={styles.wifiDetails}>{item.capabilities}</Text>
                                </TouchableOpacity>
                            ))}
                        </View>
                    )}
                </TestSuite>

                <TestSuite name="Connection">
                    <TestCase title="connectToProtectedSSID">
                        <View style={styles.testCaseContent}>
                            <Description text="Connect to a protected SSID" />
                            <CustomButton
                                title="connectToProtectedSSID"
                                onPress={() => {
                                    addLog(`Connecting to ${ssid}...`);
                                    if (password.length < 8) {
                                        Alert.alert('Password must be greater than 8 characters')
                                        return
                                    } else {
                                        WifiManager.connectToProtectedSSID(ssid, password, false, false)
                                            .then(() => updateResult("connectToProtectedSSID", "Connected to " + ssid))
                                            .catch((err: any) => updateResult("connectToProtectedSSID", "Error: " + safeStringify(err)));
                                    }

                                }}
                            />
                            <ResultArea text={results["connectToProtectedSSID"]} />
                        </View>
                    </TestCase>
                </TestSuite>

                <TestSuite name="Disconnect">
                    <TestCase title="disconnect">
                        <View style={styles.testCaseContent}>
                            <Description text="Disconnect the currently connected WiFi network." />
                            <CustomButton
                                title="Disconnect"
                                color={COLORS.error}
                                onPress={() => {
                                    WifiManager.disconnect()
                                        .then((res: any) => updateResult("disconnect", "Disconnect: " + safeStringify(res)))
                                        .catch((err: any) => updateResult("disconnect", "Error: " + safeStringify(err)));
                                }}
                            />
                            <ResultArea text={results["disconnect"]} />
                        </View>
                    </TestCase>
                </TestSuite>

            </ScrollView>
        </Tester>
    );
};

const styles = StyleSheet.create({
    headerContainer: {
        backgroundColor: COLORS.background,
        padding: 10,
        borderBottomWidth: 1,
        borderBottomColor: COLORS.border,
        elevation: 2,
        zIndex: 100,
    },
    headerTitle: {
        fontSize: 20,
        fontWeight: 'bold',
        color: COLORS.text,
        marginBottom: 10,
        textAlign: 'center',
    },
    inputCard: {
        backgroundColor: COLORS.card,
        borderRadius: 10,
        padding: 10,
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 2 },
        shadowOpacity: 0.1,
        shadowRadius: 4,
        elevation: 3,
    },
    input: {
        height: 44,
        borderColor: COLORS.border,
        borderWidth: 1,
        borderRadius: 8,
        marginBottom: 10,
        paddingHorizontal: 12,
        backgroundColor: '#FAFAFA',
        fontSize: 16,
        color: COLORS.text,
    },
    testCaseContent: {
        padding: 10,
    },
    button: {
        paddingVertical: 12,
        paddingHorizontal: 20,
        borderRadius: 8,
        alignItems: 'center',
        justifyContent: 'center',
        elevation: 2,
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 1 },
        shadowOpacity: 0.2,
        shadowRadius: 2,
    },
    buttonText: {
        color: 'white',
        fontSize: 16,
        fontWeight: '600',
    },
    resultContainer: {
        marginTop: 10,
        padding: 10,
        backgroundColor: '#F8F9FA',
        borderRadius: 6,
        borderLeftWidth: 4,
        borderLeftColor: COLORS.secondary,
    },
    resultLabel: {
        fontSize: 12,
        color: COLORS.subText,
        marginBottom: 4,
        fontWeight: '600',
    },
    resultText: {
        fontSize: 14,
        color: COLORS.text,
        fontFamily: 'monospace',
    },
    descriptionText: {
        fontSize: 13,
        color: '#666',
        marginBottom: 10,
        lineHeight: 18,
        fontStyle: 'italic',
    },
    wifiListContainer: {
        padding: 10,
        backgroundColor: COLORS.background,
    },
    sectionTitle: {
        fontSize: 18,
        fontWeight: 'bold',
        color: COLORS.text,
        marginBottom: 10,
        marginLeft: 5,
    },
    wifiItem: {
        padding: 15,
        backgroundColor: COLORS.card,
        borderRadius: 10,
        marginBottom: 8,
        shadowColor: '#000',
        shadowOffset: { width: 0, height: 1 },
        shadowOpacity: 0.1,
        shadowRadius: 2,
        elevation: 2,
    },
    wifiItemHeader: {
        flexDirection: 'row',
        justifyContent: 'space-between',
        alignItems: 'center',
        marginBottom: 4,
    },
    wifiSSID: {
        fontSize: 16,
        fontWeight: 'bold',
        color: COLORS.text,
    },
    wifiLevel: {
        fontSize: 14,
        color: COLORS.success,
        fontWeight: '600',
    },
    wifiBSSID: {
        fontSize: 12,
        color: COLORS.subText,
        marginBottom: 2,
    },
    wifiDetails: {
        fontSize: 11,
        color: COLORS.subText,
        fontStyle: 'italic',
    },
});
```

## Link

This step provides guidance for manually configuring native dependencies.

First, use DevEco Studio to open the HarmonyOS project `harmony` in your project.

### 1. Add the `overrides` field to the `oh-package.json` file in the root directory of the project.

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
  ...
}
```

### 2. Introduce Native Code

Currently, there are two methods:

1. Import via har package (this method will be deprecated after the IDE improves related features; currently, it is the preferred method);
2. Directly link the source code.

Method 1: Import via har package (Recommended)

> [!TIP] The har package is located in the `harmony` folder under the third-party library installation path.

Open `entry/oh-package.json5` and add the following dependencies.

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-wifi-reborn": "file:../../node_modules/@react-native-ohos/react-native-wifi-reborn/harmony/wifi_reborn.har"
  }
```

Click the `sync` button in the top right corner

Or execute in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link the source code

> [!TIP] If you need to use direct source code linking, refer to [Direct Source Code Linking Instructions](/zh-cn/link-source-code.md)

### 3. Configure CMakeLists and introduce turbo_log

Open `entry/src/main/cpp/CMakeLists.txt` and add:

```diff
include(FetchContent)
# BOOST
set(BOOST_ENABLE_CMAKE On)
FetchContent_Declare(
 Boost
 URL /7277/boost-1.82.0.tar.xz
 OVERRIDE_FIND_PACKAGE)
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)


add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-wifi-reborn/src/main/cpp" ./wifi_reborn)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp") # this line is needed by codegen v1
add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_wifi_reborn)
# RNOH_END: manual_package_linking_2
```

Import the TurboLogPackage on the ArkTS side

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "WifiRebornPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<WifiRebornPackage>(ctx),
    };
}
```

### 4. Import the WifiRebornPackage component on the ArkTS side.

open `entry/src/main/ets/RNPackagesFactory.ets`，add：

```diff
...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+ import { WifiRebornPackage } from '@react-native-ohos/react-native-wifi-reborn';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
return [
+    new WifiRebornPackage(ctx)
  ];
 }
...
...
```

### 5. Run

Click the `sync` button in the top right corner.

Or execute the following in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run.

## Constraints and Limitations

### Compatibility

The content of this document has been verified with the following versions:

1. RNOH: 0.72.90; SDK: HarmonyOS NEXT Developer DB3; IDE: DevEco Studio: 5.0.5.220; ROM: NEXT.0.0.105;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### Permission requirements

Among the following permissions, there is a 'system_masic' permission, while the default application permission is' normal ', which can only be used at the' normal 'level. Therefore, when installing the HAP package, an error may occur * * 9568289 * *, please refer to the [document]( https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/bm-tool-V5#ZH -CN_TOPIC_0000001884757326__%E5%AE%89%E8%A3%85hap%E6%97%B6%E6%8F%90%E7%A4%BAcode9568289-error-install-failed-due-to-grant-request-permissions-failed)  Change the application level to 'system_masic'`

#### Add permissions to module.json5 in the entry directory

Open 'entry/src/main/module. json5' and add:

```diff
...
"requestPermissions": [
			{
				"name": "ohos.permission.GET_WIFI_INFO",
				"reason": "$string:wifi_info_reason",
				"usedScene": {
					"abilities": [],
					"when": "inuse"
				}
			},
			{
				"name": "ohos.permission.SET_WIFI_INFO",
				"reason": "$string:wifi_set_reason",
				"usedScene": {
					"abilities": [],
					"when": "inuse"
				}
			},
			{
				"name": "ohos.permission.LOCATION",
				"reason": "$string:location_reason",
				"usedScene": {
					"abilities": [],
					"when": "inuse"
				}
			},
			{
				"name": "ohos.permission.APPROXIMATELY_LOCATION",
				"reason": "$string:location_approx_reason",
				"usedScene": {
					"abilities": [],
					"when": "inuse"
				}
			}
		],
```

#### Add the reason for applying for the above permissions in the entry directory

Open 'entry/src/main/resources/base/element/string. json' and add:

```diff
...
{
  "string": [
    {
      "name": "wifi_info_reason",
      "value": "Need to obtain WiFi information to display the current network status of the connection"
    },
    {
      "name": "wifi_set_reason",
      "value": "Need to configure WiFi network to connect to the specified wireless network"
    },
    {
      "name": "location_reason",
      "value": "Location permission is required to scan nearby WiFi networks (system requirement)"
    },
    {
      "name": "location_approx_reason",
      "value": "Need approximate location permission to scan WiFi networks"
    }
  ]
}
```

## Attributes

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library.

> [!TIP] The "HarmonyOS Support" column shows "yes" if the attribute is supported on the HarmonyOS platform, "no" if not supported, and "partially" if partially supported. The usage method is consistent across platforms, and the effect aligns with that of iOS or Android.

**wifi-reborn**：A third-party library for WiFi management in React Native, mainly used to implement various operations related to device WiFi functionality in applications.

| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| connectToProtectSSID | Connect to a protected SSID     | function | no       | Android/IOS | yes               |
| suggestWifiNetwork | Recommend/prompt the specified visible WIFI network to the mobile device system    | function | no       | Android/IOS | yes               |
| connectToProtectedWifiSSID | Connect to the protected WIFI named SSID     | function | no       | Android/IOS | yes               |
| getCurrentWifiSSID | Return the SSID of the current WiFi network     | function | no       | Android/IOS | yes               |
| connectToSSID | Connect to SSID     | function | no       | IOS | yes               |
| connectToSSIDPrefix | Connect to SSID with a specific prefix     | function | no       | IOS | yes               |
| disconnectFromSSID | Disconnect from SSID     | function | no       | IOS | yes               |
| connectToProtectedSSIDOnce | Connect to the protected SSID once     | function | no       |  IOS | no               |
| connectToProtectedSSIDPrefix | Connect to a protected SSID with a specific prefix     | function | no       | IOS | yes               |
| connectToProtectedSSIDPrefixOnce | Connect to a protected SSID with a specific prefix once     | function | no       | IOS | no               |
| loadWifiList | Return to the list of nearby WIFI networks     | function | no       | Android | yes               |
| reScanAndLoadWifiList | Rescan visible WiFi networks in the surrounding area and load and return the complete WiFi list data     | function | no       | Android | yes               |
| isEnabled | Check if WIFI is turned on     | function | no       | Android | yes               |
| setEnabled | Set WIFI on or off on the device     | function | no       | Android | yes               |
| connectionStatus | The current device is connected to WIFI and has been connected, returning true     | function | no       | Android | yes               |
| disconnect | Disconnect the current WIFI connection     | function | no       | Android | yes               |
| getBSSID | Return the BSSID of the current WIFI connection     | function | no       | Android | yes               |
| getCurrentSignalStrength | Return the RSSI (signal strength) of the current WIFI connection     | function | no       | Android | yes               |
| getFrequency | Return the signal frequency of the currently connected WIFI     | function | no       | Android | yes               |
| getIP | Return the IP address of the current WIFI connection     | function | no       | Android | yes               |
| isRemoveWifiNetwork | Remove the specified WiFi network with saved configuration from the device     | function | no       | Android | yes               |
| forceWifiUsage | Force the current application's network requests to go through the WIFI channel that the device is already connected to, ignoring mobile data     | function | no       | Android | yes               |
| forceWifiUsageWithOptions | Force the current application's network requests to go through the WIFI channel that the device is already connected to, ignoring mobile data (which can be passed into the configuration object)     | function | no       | Android | yes               |

## Static method

## outstanding issues

## other

•The connectToProtectdSSIDOnce and connectToProtectdSSIDPriorityOnce methods cannot be implemented. These two methods are specifically designed for the iOS platform and use the NEHotspotConfiguring Manager to pass the joinOnce parameter in the iOS system to achieve one-time connection functionality. However, HarmonyOS does not support this feature.
•setEnabled HarmonyOS only supports jumping to the Wi-Fi settings page

## open source license

This project is based on [The MIT License (MIT)]（ https://github.com/JuanSeBestia/react-native-wifi-reborn/blob/master/LICENSE ）Please enjoy and participate freely in open source.


