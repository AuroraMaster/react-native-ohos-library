Template version: v0.2.2

<p align="center">
  <h1 align="center"> 
    <code>@op-engineering/op-sqlite</code> 
  </h1>
</p>

<p align="center">
    <a href="https://github.com/OP-Engineering/op-sqlite">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/OP-Engineering/op-sqlite/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/op-sqlite)


## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information       | Supported RN Version |
| ---------- | ------------------------------------------------------------ | ---------- |
| <= 8.0.2-0.0.3@deprecated  | [@react-native-oh-tpl/op-sqlite Releases(deprecated)](https://github.com/react-native-oh-library/op-sqlite/releases) | 0.72       |
| 8.0.3                | [@react-native-ohos/op-sqlite Releases](https://gitcode.com/openharmony-sig/rntpc_op-sqlite/releases)   | 0.72       |
| 14.0.1                | [@react-native-ohos/op-sqlite Releases](https://gitcode.com/openharmony-sig/rntpc_op-sqlite/releases)   | 0.77       |

For older versions not published on npm, please refer to the [Installation Guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/op-sqlite
```

#### **yarn**

```bash
yarn add @react-native-ohos/op-sqlite
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.


```js

import React, { useEffect, useState } from 'react';
import {
    SafeAreaView,
    Text,
    TouchableOpacity,
    View,
} from 'react-native';

import {
    open,
    type DB,
    Scalar,
    HARMONY_DATABASE_PATH
} from '@op-engineering/op-sqlite';

export default function OpSqliteExample() {
    
    return (
        <SafeAreaView style={{ flex: 1, backgroundColor: '#fff' }}>
            <View style={{ flex: 1, backgroundColor: '#fff' }}>
                <TouchableOpacity
                    style={{ padding: 5 }}
                    onPress={() => {
                        let db:DB = open({
                            name: 'helloDb.sqlite',
                            encryptionKey: 'test',
                            location: HARMONY_DATABASE_PATH
                        });
                    }}>
                    <Text style={{ color: 'red' }}>
                       tap to {'openDB'}
                    </Text>
                </TouchableOpacity>
            </View>

        </SafeAreaView>
    );
}


```


For details, see [Source Repository Document Address](https://ospfranco.notion.site/OP-SQLite-Documentation-a279a52102464d0cb13c3fa230d2f2dc?pvs=4)


## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~14.0.1                              |  No                   |  0.77                |
| ~8.0.3                               |  Yes                  |  0.72                |
| <= 8.0.2-0.0.3@deprecated            |  No                   |  0.72                |

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

### 2. Introducing Native Code

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-ohos/op-sqlite": "file:../../node_modules/@react-native-ohos/op-sqlite/harmony/rn_op_sqlite.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3. Configuring CMakeLists and Introducing RNOpSqlitePackage

> If you are using version <= 8.0.2-0.0.3, please skip this chapter.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/op-sqlite/src/main/cpp" ./rn_op_sqlite)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_rn_op_sqlite)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNOpSqlitePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNOpSqlitePackage>(ctx)
    };
}
```

### 4. Introducing RNOpSqlitePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import { RNOpSqlitePackage } from '@react-native-ohos/op-sqlite/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNOpSqlitePackage(ctx),
  ];
}
```
</details>

## Necessary configuration items

> [!TIP] The content of this module cannot be automatically generated by autolink and must always be manually configured.

### 1. Create a `package.json` file in the root directory of your IDE project and configure the parameters.(This module always requires manual configuration)

```json
{
...
  "op-sqlite": {
    ...
    "sqlcipher": false,
    "libsql": false, //Here, if it is set to "true", it represents the remote database mode.
  },
}
```

### 2. Introducing opSqlitePlugin to ArkTS(This module always requires manual configuration)

Open the `entry/hvigorfile.ts` file and add the following code:

```diff
+ import { hapTasks, OhosHapContext, OhosPluginId, Target } from '@ohos/hvigor-ohos-plugin';
+ import { HvigorPlugin, HvigorNode, getNode } from '@ohos/hvigor';
+ import { opSqlitePlugin } from './oh_modules/@react-native-ohos/op-sqlite/hvigorfile.ts';

+const path = require('path');
+const rootRNPackagePath = path.join(__dirname, '../package.json'); //The configuration is based on the actual package path

export default {
    system: hapTasks,
+   plugins: [opSqlitePlugin(rootRNPackagePath)]
}
```

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


### Permission Requirements

#### Include applicable permissions in the module.json5 file within the entry directory.

Open the `YourProject/entry/src/main/module.json5` file and add the following code:

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+     { "name": "ohos.permission.INTERNET" },
    ]
  }
}
```


## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getConstants  | Return the corresponding database/file storage sandbox path.         |  () => {IOS_DOCUMENT_PATH,IOS_LIBRARY_PATH,ANDROID_DATABASE_PATH,ANDROID_FILES_PATH,ANDROID_EXTERNAL_FILES_PATH,HARMONY_DATABASE_PATH,HARMONY_FILES_PATH,}  | no | all      | yes |
| openSync  | Synchronize the local database to the remote database and open the database.         | (options: {url: string;authToken: string;name: string;location?: string;}) => DB; | no | all      | yes |
| openRemote  | Open the remote database. | (options: { url: string; authToken: string }) => DB;  | no | all      | yes |
| open  | Open the database.encryptionKey indicates the key string required for using sqlcipher.After sqlcipher is enabled, encryptionKey is supported.         | (options: {name: string;location?: string;encryptionKey?: string;}) => DB;  | no | all      | yes |
| isSQLCipher  | Whether SQL cipher is enabled.(SQLCipher is an open source SQLite extension that provides transparent 256-bit AES full database encryption.)         | () => boolean;  | no | all      | yes |
| isLibsql  | Indicates whether to enable isLibsql. After isLibsql is enabled, the remote database and database synchronization interface can be enabled         | () => boolean;  | no | all      | yes |
| moveAssetsDatabase  | Copy the database to the specified path.         | async (args: {filename: string;path?: string;overwrite?: boolean;}) => Promise<boolean>  | no | all      | yes |

### DB

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| close  | Shut down the database.         | () => void;  | no | all      | yes |
| delete  | Deleting a database         | (location?: string) => void;  | no | all      | yes |
| attach  | Attaching other databases to the primary database by aliasing          | (mainDbName: string,dbNameToAttach: string,alias: string,location?: string) => void;  | no | all      | yes |
| detach  | Detaching Other Databases from the Primary Database by Alias         | (mainDbName: string, alias: string) => void;  | no | all      | yes |
| transaction  | Operate through database transactions         | (fn: (tx: Transaction) => Promise<void>) => Promise<void>;  | no | all      | yes |
| execute  | Execute SQL statements in the database.         | (query: string, params?: any[]) => QueryResult;  | no | all      | yes |
| executeWithHostObjects  | The database query statement is used to quickly query a large amount of data. However, the return attribute access speed is slow.         | (query: string,params?: any[]) => Promise<QueryResult>;  | no | all      | yes |
| executeBatch  | Query and execute a large number of statements.         | (commands: SQLBatchTuple[]) => BatchQueryResult;  | no | all      | yes |
| loadFile  | Load the local SQL file.         | (location: string) => Promise<FileLoadResult>;  | no | all      | yes |
| updateHook  | Database update hook callback         | (callback?:((params: \{table: string;operation: UpdateHookOperation;row?: any;rowId: number;}) => void) \| null) => void;  | no | all      | yes |
| commitHook  | Database commit hook callback.         | (callback?: (() => void) \| null) => void;  | no | all      | yes |
| rollbackHook  | Database rollback hook callback.         | (callback?: (() => void) \| null) => void;  | no | all      | yes |
| prepareStatement  | You can reuse a query statement, use bind to change parameters, and execute the execution result.        | (query: string) => PreparedStatementObj;  | no | all      | yes |
| loadExtension  | Load SQL extension.         | (path: string, entryPoint?: string) => void;  | no | all      | yes |
| executeRaw  | If you do not care about the key, you can use this API to simplify the execution and return a component array.This should be much faster than the normal operation because you don't need to create objects with the same key.         | (query: string,params?: any[]) => Promise<any[]>;  | no | all      | yes |
| getDbPath  | Obtaining the Database Path.         | (location?: string) => string;  | no | all      | yes |
| reactiveExecute  | Responsive statement query         | (params: {query: string;arguments: any[];fireOn: {table: string;ids?: number[];}[];callback: (response: any) => void;}) => () => void;  | no | all      | yes |
| sync  | Database synchronization operation, which is supported after isLibsql is enabled.         | () => void | no | all      | yes |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/OP-Engineering/op-sqlite/blob/main/LICENSE)
