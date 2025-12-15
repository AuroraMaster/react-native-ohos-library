> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>mixpanel-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mixpanel/mixpanel-react-native/tree/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mixpanel/mixpanel-react-native/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/mixpanel-react-native)

## Installation and Usage

Find the matching version information in the release address of a third-party library:

| Third-party Library Version | Release Information                                                                                                                  | Supported RN Version |
|----------------------------|--------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| <= 3.0.5-0.1.1@deprecated| [@react-native-oh-tpl/mixpanel-react-native Releases(deprecated)](https://github.com/react-native-oh-library/mixpanel-react-native/releases) | 0.72       |
| 3.0.6         | [@react-native-ohos/mixpanel-react-native Releases](https://github.com/react-native-oh-library/mixpanel-react-native/releases)                | 0.72       |
| 3.2.0         |  [@react-native-ohos/mixpanel-react-native Releases](https://github.com/react-native-oh-library/mixpanel-react-native/releases)               | 0.77       |


For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/mixpanel-react-native
```


#### **yarn**

```bash
yarn add @react-native-ohos/mixpanel-react-native
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.
> [!WARNING] The token value used in the code needs to be obtained from the project settings on the[ Mixpanel website](https://mixpanel.com),After an event is sent, you can view the corresponding data in the project analytics on the[ Mixpanel website](https://mixpanel.com)

```js
import React from 'react';
import {Button, SafeAreaView} from 'react-native';
import {Mixpanel} from 'mixpanel-react-native';

const trackAutomaticEvents = false;
const token = 'Your Project Token';
const mixpanel = new Mixpanel(token, trackAutomaticEvents);
mixpanel.init();

export default function MixpanelDemo() {
    return (
    <SafeAreaView>
        <Button
    title="Select Premium Plan"
    onPress={() => mixpanel.track('Plan Selected', {Plan: 'Premium'})}
/>
    </SafeAreaView>
);
}
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~3.2.0                               |  No                   |  0.77                |
| ~3.0.6                               |  Yes                  |  0.72                |
| <= 3.0.5-0.1.1@deprecated            |  No                   |  0.72                |

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

### 2.Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
"@rnoh/react-native-openharmony": "file:../react_native_openharmony",
"@react-native-ohos/mixpanel-react-native": "file:../../node_modules/@react-native-ohos/mixpanel-react-native/harmony/mixpanel.har"
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

### 3.Configuring CMakeLists and Introducing UnistylesPackage

> If you are using version <=  3.0.5-0.1.1, please skip this chapter.

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/mixpanel-react-native/src/main/cpp" ./mixpanel)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_mixpanel)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
+ #include "MixpanelPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<MixpanelPackage>(ctx)
}
```

### 4.Introducing RNUnistylesPackage to ArkTS

Open `entry/src/main/ets/RNPackagesFactory.ts`，add：

```diff
  ...
+ import { MixpanelPackage } from '@react-native-ohos/mixpanel-react-native/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new MixpanelPackage(ctx)
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

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### Mixpanel

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- |----------| -------- |-------------------|
| init(): void; | Initialize a Mixpanel instance. | function | yes      | iOS,Android | yes               |
| setServerURL(serverURL: string): void; | Set the base URL for Mixpanel API requests. | function | no       | iOS,Android | yes               |
| setLoggingEnabled(loggingEnabled: boolean): void; | Enable or disable logging. | function | no       | iOS,Android | yes               |
| setFlushOnBackground(flushOnBackground: boolean): void; | On iOS, allow or disable Mixpanel from flushing events when the app enters the background. | function | no       | iOS | no                |
| setUseIpAddressForGeolocation(useIpAddressForGeolocation: boolean): void; | Enable or disable sending the IP address as a basis for geolocation. | function | no       | iOS,Android | yes               |
| setFlushBatchSize(flushBatchSize: number): void; | Set the number of events to send in a single network request to Mixpanel. | function | no       | iOS,Android | yes               |
| hasOptedOutTracking(): Promise<boolean>; | Check if a user has opted out of tracking. | function | no       | iOS,Android | yes               |
| optInTracking(): void; | User has opted to be tracked. | function | no       | iOS,Android | yes               |
| optOutTracking(): void; | User has opted out of tracking. | function | no       | iOS,Android | yes               |
| identify(distinctId: string): Promise<void>; | Associate future track calls with the following user identifier. | function | no       | iOS,Android | yes               |
| alias(alias: string, distinctId: string): void; | Create a mapping to associate a new identifier with the user's original distinct_id. | function | no       | iOS,Android | yes               |
| track(eventName: string, properties?: MixpanelProperties): void; | Send an event. | function | yes      | iOS,Android | yes               |
| getPeople(): People; | Obtain a People instance. | function | no       | iOS,Android | yes               |
| trackWithGroups(eventName: string, properties?: MixpanelProperties, groups?: MixpanelProperties): void; | Track events specific to a group of people. | function | no       | iOS,Android | no                |
| setGroup(groupKey: string, groupID: MixpanelType): void; | Set the group that a user belongs to. | function | no       | iOS,Android | no                |
| getGroup(groupKey: string, groupID: MixpanelType): MixpanelGroup; | Obtain a Group instance. | function | no       | iOS,Android | yes               |
| addGroup(groupKey: string, groupID: MixpanelType): void; | Add a group. | function | no       | iOS,Android | no                |
| removeGroup(groupKey: string, groupID: MixpanelType): void; | Remove a group. | function | no       | iOS,Android | no                |
| deleteGroup(groupKey: string, groupID: MixpanelType): void; | Delete a group. | function | no       | iOS,Android | no                |
| registerSuperProperties(properties: MixpanelProperties): void; | Register global properties that are common to all users.| function | no       | iOS,Android | yes               |
| registerSuperPropertiesOnce(properties: MixpanelProperties): void; | Register global properties that are common to all users without overwriting existing properties.| function | no       | iOS,Android | yes               |
| unregisterSuperProperty(propertyName: string): void; | Delete a specified registered global property. | function | no       | iOS,Android | yes               |
| getSuperProperties(): Promise<MixpanelProperties>; | Retrieve registered global properties. | function | no       | iOS,Android | yes               |
| clearSuperProperties(): void; | Delete all registered global properties. | function | no       | iOS,Android | yes               |
| timeEvent(eventName: string): void; | Send a timing event. | function | no       | iOS,Android | yes               |
| eventElapsedTime(eventName: string): Promise<number>; | Get the current timing for a specified event. | function | no       | iOS,Android | yes               |
| reset(): void; | Reset a user's related information. | function | no       | iOS,Android | yes               |
| getDistinctId(): Promise<string>; | Get the unique identifier. | function | no       | iOS,Android | yes               |
| getDeviceId(): Promise<string>; | Get the device identifier. | function | no       | iOS,Android | yes               |
| flush(): void; | Push all events and user information to the server. | function | no       | iOS,Android | yes               |


#### People

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| set(prop: string, to: MixpanelType): void; | Set a user's property. | function | no | iOS,Android | yes |
| set(properties: MixpanelProperties): void; | Set a user's property. | function | no | iOS,Android | yes |
| setOnce(prop: string, to: MixpanelType): void; | Set a user's property without overwriting an existing value.| function | no | iOS,Android | yes |
| setOnce(properties: MixpanelProperties): void; | Set a user's property without overwriting an existing value.| function | no | iOS,Android | yes |
| increment(prop: string, by: number): void; | Increment the value of a numerical user property, typically used for counting or accumulating occurrences of a behavior. | function | no | iOS,Android | yes |
| increment(properties: MixpanelProperties): void; | Increment the value of a numerical user property, typically used for counting or accumulating occurrences of a behavior. | function | no | iOS,Android | yes |
| append(name: string, value: MixpanelType): void; | Add a value to a user's property, appending it to the existing value if the property already exists. | function | no | iOS,Android | yes |
| union(name: string, value: Array<MixpanelType>): void; | Add a value to a user's property, merging the newly added data with the existing value if the property already has a value. | function | no | iOS,Android | yes |
| remove(name: string, value: MixpanelType): void; | Remove a specified value from a user's property. | function | no | iOS,Android | yes |
| unset(name: string): void; | Delete a user's property and its value. | function | no | iOS,Android | yes |
| trackCharge(charge: number, properties: MixpanelProperties): void; | Track a user's transaction. | function | no | iOS,Android | yes |
| clearCharges(): void; | Permanently clear a user's historical transaction records. | function | no | iOS,Android | yes |
| deleteUser(): void; | Permanently delete a user from People analytics. | function | no | iOS,Android | yes |


#### MixpanelGroup

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| set(prop: string, to: MixpanelType): void; | Set a group's property. | function | no | iOS,Android | no |
| setOnce(prop: string, to: MixpanelType): void; | Set a group's property without overwriting an existing value. | function | no | iOS,Android | no |
| unset(prop: string): void; | Delete a group's property. | function | no | iOS,Android | no |
| remove(name: string, value: MixpanelType): void; | Remove a specified value from a group's property. | function | no | iOS,Android | no |
| union(name: string, value: MixpanelType): void; | Add a value to a group's property, merging the newly added data with the existing value | function | no | iOS,Android | no |


## Known Issues
- [ ] Some interfaces have not been developed yet: [issue#5](https://github.com/react-native-oh-library/mixpanel-react-native/issues/5)

## Others

## License

This project is licensed under [Apache License2.0](https://github.com/mixpanel/mixpanel-react-native/blob/master/LICENSE.md).

