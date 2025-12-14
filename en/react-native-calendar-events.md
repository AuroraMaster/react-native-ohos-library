> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-calendar-events</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wmcmahan/react-native-calendar-events">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/wmcmahan/react-native-calendar-events/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-calendar-events)

## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <=2.2.0-0.0.4@deprecated | [@react-native-oh-tpl/react-native-calendar-events Releases(deprecated)](https://github.com/react-native-oh-library/react-native-calendar-events/releases) | 0.72       |
| 2.2.1            | [@react-native-ohos/react-native-calendar-events Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-calendar-events/releases) | 0.72       |
| 2.3.0            | [@react-native-ohos/react-native-calendar-events Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-calendar-events/releases) | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-calendar-events
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-calendar-events
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js

import React from 'react';
import {
    SafeAreaView,
    StyleSheet,
    ScrollView,
    View,
    Text,
    StatusBar,
    Button,
    Alert,
    Platform,
} from 'react-native';
import {Header, Colors} from 'react-native/Libraries/NewAppScreen';
import RNCalendarEvents from 'react-native-calendar-events';

const sourceStruct = {
    /** The Account name */
    name: "testName",
    /** The Account type */
    type: "testTyoe",
}

//saveEvent
const calendarOptions = {
    title: 'test1',
    type: 'local',
    displayName: "testSaveCalendar"
};

//saveEvent
const location = {
    location: "nanjin",
    longitude: 118,
    latitude: 31,
}
const eventService = {
    type: 'Meeting',
    uri: "",
    description: "testEventService",
}
const attendees = {
    name: "testAttendees",
    email: "testEmail",
}
const recurrenceRuleHarmony = {
    recurrenceFrequency: 2,
    expire: 0,
}
const eventDetails = {
    id: 1,
    type: 0,
    title: 'testEvent',
    location: location,
    startTime: new Date().getTime() + 60 * 60 * 1000 * 3,
    endTime: new Date().getTime() + 60 * 60 * 1000 * 10,
    isAllDay: false,
    attendee: [attendees],
    timeZone: "beijing",
    reminderTime: [new Date().getTime()],
    recurrenceRule: recurrenceRuleHarmony,
    description: "test",
    service: eventService,
};

const fetchAllEventStartTime: string = (new Date().getTime() + 60 * 60 * 1000).toString()
const fetchAllEventEndTime: string = (new Date().getTime() + 60 * 60 * 1000 * 15).toString()
function CalendarDemo() {
    return (
        <>
            <StatusBar barStyle="dark-content" />
            <SafeAreaView>
                <ScrollView
                    contentInsetAdjustmentBehavior="automatic"
                    style={styles.scrollView}>
                    <Header />
                    <View style={styles.engine}>
                        <Text style={styles.footer}>Engine: Hermes</Text>
                    </View>
    
                    <View style={styles.body}>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>Read/Write Auth</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="Request auth"
                                    onPress={() => {
                                        RNCalendarEvents.requestPermissions().then(
                                            (result) => {
                                                Alert.alert('Auth requested', result);
                                            },
                                            (result) => {
                                                console.error(result);
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>check auth</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="Check auth"
                                    onPress={() => {
                                        RNCalendarEvents.checkPermissions().then(
                                            (result) => {
                                                Alert.alert('Auth check', result);
                                            },
                                            (result) => {
                                                console.error(result);
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>Calendars</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="Find calendars"
                                    onPress={() => {
                                        RNCalendarEvents.findCalendars().then(
                                            (result) => {
                                                Alert.alert(
                                                    'Calendars',
                                                    result.reduce((acc: string[], cal) => {
                                                        acc.push(cal.title);
                                                        return acc;
                                                    }, []).join('\n'),
                                                );
                                            },
                                            (result) => {
                                                console.error(result);
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                    </View>
                </ScrollView>
            </SafeAreaView>
        </>
    );
};

const styles = StyleSheet.create({
    scrollView: {
        backgroundColor: Colors.lighter,
    },
    engine: {
        position: 'absolute',
        right: 0,
    },
    body: {
        backgroundColor: Colors.white,
    },
    sectionContainer: {
        marginTop: 32,
        paddingHorizontal: 24,
    },
    sectionTitle: {
        fontSize: 24,
        fontWeight: '600',
        color: Colors.black,
    },
    sectionDescription: {
        marginTop: 8,
        fontSize: 18,
        fontWeight: '400',
        color: Colors.dark,
    },
    highlight: {
        fontWeight: '700',
    },
    footer: {
        color: Colors.dark,
        fontSize: 12,
        fontWeight: '600',
        padding: 4,
        paddingRight: 12,
        textAlign: 'right',
    },
});

export default CalendarDemo;
```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).


## Link

|                                      | Is supported autolink  | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~2.3.0                               |  No                   |  0.77                |
| ~2.2.1                               |  Yes                  |  0.72                |
| <= 2.2.0-0.0.4@deprecated            |  No                   |  0.72                |

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
    "@react-native-ohos/react-native-calendar-events": "file:../../node_modules/@react-native-ohos/react-native-calendar-events/harmony/calendar_events.har"
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

### 3.Configure CMakeLists and Import CalendarEventPackage

> If you are using version <= 2.2.0-0.0.4, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add:

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-calendar-events/src/main/cpp" ./calendar_events)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_calendar_events)
# RNOH_BEGIN: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add:

```diff
#include "RNOH/PackageProvider.h"
+ #include "CalendarEventPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<CalendarEventPackage>(ctx)
}
```

### 4. Introducing  CalendarEventPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { CalendarEventPackage } from "@react-native-ohos/react-native-calendar-events/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CalendarEventPackage(ctx),
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

To use this library, you need to use the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### Permission Requirements

#### Add permissions in the module.json5 file under the entry directory.

Open `entry/src/main/module.json5`, add the following permission:

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.READ_CALENDAR",
+    "reason": "$string:Access_calendar",
+    "usedScene": {
+      "abilities": [
+        "FormAbility"
+      ],
+      "when":"inuse"
+    }
+  },
+  {
+    "name": "ohos.permission.WRITE_CALENDAR",
+    "reason": "$string:Access_calendar",
+    "usedScene": {
+      "abilities": [
+        "FormAbility"
+      ],
+      "when":"inuse"
+    }
+  }
]
```

#### Add the description for requiring calendar permissions in the entry directory

Open `entry/src/main/resources/base/element/string.json`, add the following content:

```diff
...
{
  "string": [
+    {
+      "name": "Access_calendar",
+      "value": "access calendar"
+    }
  ]
}
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                                                     | Type      | Required | Platform | HarmonyOS Support |
|-----------------------|-------------------------------------------------------------------------------------------------|-----------| -------- |----------|------------------|
| requestPermissions((readOnly = false))  | Request calendar authorization. Authorization must be granted before accessing calendar events. | function  | No       | All      | yes              |
| checkPermissions((readOnly = false))    | Get calendar authorization status.                                                              | function  | No       | All      | yes              |
| findCalendars()       | Finds all the calendars on the device.                                                          | function  | No       | All      | yes              |
| saveCalendar(calendar)        | Create a calendar.                                                                              | function  | No       | All      | yes              |
| removeCalendar(id)      | Removes a calendar.                                                                             | function  | No       | All      | yes              |
| findEventById(id)       | Find calendar  by id.                                                                           | function  | No       | All      | yes              |
| fetchAllEvents(startDate, endDate, calendars)      | Fetch all calendar events.                                                                      | function  | No       | All      | yes              |
| saveEvent(title, details, options)           | Creates or updates a calendar event. To update an event, the event id must be defined.          | function  | No       | All      | yes              |
| removeEvent(id, options)         | Removes calendar event.                                                                         | function  | No       | All      | yes              |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/wmcmahan/react-native-calendar-events/blob/master/LICENSE.md).
