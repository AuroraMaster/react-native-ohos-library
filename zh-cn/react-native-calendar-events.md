> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-calendar-events)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 | 
| ---------- | ------------------------------------------------------------ | ---------- |
| <=2.2.0-0.0.4@deprecated | [@react-native-oh-tpl/react-native-calendar-events Releases(deprecated)](https://github.com/react-native-oh-library/react-native-calendar-events/releases) | 0.72       |
| 2.2.1            | [@react-native-ohos/react-native-calendar-events Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-calendar-events/releases) | 0.72       |
| 2.3.0            | [@react-native-ohos/react-native-calendar-events Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-calendar-events/releases) | 0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

|                                      | 是否支持autolink | RN框架版本 |
|--------------------------------------|-----------------|------------|
| ~2.3.0                               |  No              |  0.77     |
| ~2.2.1                              |  Yes             |  0.72     |
| <= 2.2.0-0.0.4@deprecated            |  No              |  0.72     |

使用AutoLink的工程需要根据该文档配置，Autolink框架指导文档：https://gitcode.com/openharmony-sig/ohos_react_native/blob/master/docs/zh-cn/Autolinking.md。

如您使用的版本支持 Autolink，并且工程已接入 Autolink，可跳过ManualLink配置。
<details>
  <summary>ManualLink: 此步骤为手动配置原生依赖项的指导</summary>

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。


### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```
### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-calendar-events": "file:../../node_modules/@react-native-ohos/react-native-calendar-events/harmony/calendar_events.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 CalendarEventPackage

> 若使用的是 <= 2.2.0-0.0.4 版本，请跳过本章。

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
+ #include "CalendarEventPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<CalendarEventPackage>(ctx)
}
```

### 4.在 ArkTs 侧引入 CalendarEventPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

## 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

### 权限要求

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

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

#### 在 entry 目录下添加申请日历权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

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

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wmcmahan/react-native-calendar-events/blob/master/LICENSE.md) ，请自由地享受和参与开源。
