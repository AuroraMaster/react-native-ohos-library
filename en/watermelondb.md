> Template version：v0.3.0

<p align="center">
  <h1 align="center"> <code>watermelondb</code> </h1>
</p>

This project is developed based on [watermelondb@[v0.28.1-0](https://github.com/Nozbe/WatermelonDB)].

Please go to the Releases page of the third-party library to check the matching version information: ([@react-native-ohos/watermelondb Releases](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/tags)). For older versions that have not been released to npm, please refer to the Installation [Install Guide](/zh-cn/tgz-usage.md)。

information:


| Third-party library version | Release information                                                                                    | Supported RN version |
| --------------------------- | ------------------------------------------------------------------------------------------------------ | -------------------- |
| v0.28.2                     | [@react-native-ohos/watermelondb Releases](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/tags) | 0.72/0.77            |

## 1. Installation and Usage

Go to the project directory and execute the following instruction：

#### npm

```bash
npm install @react-native-ohos/watermelondb
```

#### yarn

```bash
yarn add @react-native-ohos/watermelondb
```

The following code demonstrates the basic usage scenarios of this library:

> [!WARNING] The library name imported remains unchanged during usage.

### watermelondb example

```js
// jsi: false
import React, { useState } from "react";
import { View, Text, Button, StyleSheet, ScrollView } from "react-native";
import {
  appSchema,
  tableSchema,
  tableName,
  columnName,
  validateColumnSchema,
} from "@nozbe/watermelondb/Schema";
import { Database } from "@nozbe/watermelondb";
import SQLiteAdapter from "@nozbe/watermelondb/adapters/sqlite";
import { schemaMigrations } from "@nozbe/watermelondb/Schema/migrations";

const userTable = tableName("users");

const userColumns = {
  name: columnName("name"),
  email: columnName("email"),
  age: columnName("age"),
};

const userTableSchema = tableSchema({
  name: userTable,
  columns: [
    { name: userColumns.name, type: "string" },
    { name: userColumns.email, type: "string", isIndexed: true },
    { name: userColumns.age, type: "number", isOptional: true },
  ],
});

const userInfoTable = tableName("user_info");
const userInfoColumns = {
  userId: columnName("user_id"),
  address: columnName("address"),
  phone: columnName("phone"),
};
const userInfoTableSchema = tableSchema({
  name: userInfoTable,
  columns: [
    { name: userInfoColumns.userId, type: "string", isIndexed: true },
    { name: userInfoColumns.address, type: "string" },
    { name: userInfoColumns.phone, type: "string", isOptional: true },
  ],
});

const orderTable = tableName("order");
const orderTableSchema = tableSchema({
  name: orderTable,
  columns: [
    { name: columnName("order_no"), type: "string", isIndexed: true },
    { name: columnName("user_id"), type: "string", isIndexed: true },
    { name: columnName("amount"), type: "number" },
    { name: columnName("status"), type: "string", defaultValue: "pending" },
  ],
});

const productTable = tableName("product");
const productTableSchema = tableSchema({
  name: productTable,
  columns: [
    { name: columnName("product_name"), type: "string" },
    { name: columnName("price"), type: "number" },
    { name: columnName("stock"), type: "number", defaultValue: 0 },
  ],
});

const tableSchemaMap = {
  tableName: userTableSchema,
  columnName: userInfoTableSchema,
  tableSchema: orderTableSchema,
  appSchema: productTableSchema,
};

const getAppDatabaseSchema = (tableSchema) => {
  return appSchema({
    version: 1,
    tables: [tableSchema],
  });
};

const validateUserColumns = () => {
  const results = [];
  userTableSchema.columnArray.forEach((column) => {
    try {
      validateColumnSchema(column);
      results.push({ column: column.name, valid: true });
    } catch (error) {
      results.push({ column: column.name, valid: false, error: error.message });
    }
  });
  console.log(results);
  return results;
};

const initializeDatabase = async (tableType) => {
  const targetTableSchema = tableSchemaMap[tableType] || userTableSchema;
  const adapter = new SQLiteAdapter({
    dbName: `watermelon_${tableType}_db`,
    schema: getAppDatabaseSchema(targetTableSchema),
    jsi: false,
    migrations: schemaMigrations({ migrations: [] }),
  });

  await adapter.initializingPromise;
  return new Database({ adapter, modelClasses: [] });
};

const SchemaExample = () => {
  const [validationResult, setValidationResult] = useState(null);
  const [createResult, setCreateResult] = useState(null);
  const [database, setDatabase] = useState({});
  const handleValidateSchema = () => {
    const results = validateUserColumns();
    setValidationResult(results);
    setCreateResult(null);
  };

  const handleCreateTables = async (tableType) => {
    try {
      if (database[tableType]) {
        const tableName = tableSchemaMap[tableType]?.name || userTable;
        setCreateResult({
          success: true,
          message: `The database (${tableType}) already exists`,
          tables: [tableName],
        });
        return;
      }

      const db = await initializeDatabase(tableType);
      setDatabase({ ...database, [tableType]: db });
      const tableName = tableSchemaMap[tableType]?.name || userTable;
      setCreateResult({
        success: true,
        message: `The database table (${tableType}) has been created successfully`,
        tables: [tableName],
      });
    } catch (error) {
      setCreateResult({
        success: false,
        message: `The database table (${tableType}) failed to be created`,
        error: error.message,
      });
    }
  };

  const handleClear = () => {
    setValidationResult(null);
    setCreateResult(null);
    setDatabase({});
  };

  return (
    <ScrollView style={styles.container}>
      <Text style={styles.title}>WatermelonDB Table Creation Example</Text>

      <View style={styles.buttons}>
        <Button
          title="Create the user table using ${tableName}"
          onPress={() => handleCreateTables("tableName")}
          color="#4CAF50"
        />
        <Button
          title="Create the user table using ${columnName}"
          onPress={() => handleCreateTables("columnName")}
          color="#4CAF50"
        />
        <Button
          title="Create the user table using ${tableSchema}"
          onPress={() => handleCreateTables("tableSchema")}
          color="#4CAF50"
        />
        <Button
          title="Create the user table using ${appSchema}"
          onPress={() => handleCreateTables("appSchema")}
          color="#4CAF50"
        />
        <Button
          title="Validate field definitions using validateColumnSchema"
          onPress={handleValidateSchema}
          color="#2196F3"
        />
        <Button title="Clear state" onPress={handleClear} color="#f44336" />
      </View>

      {validationResult && (
        <View style={styles.result}>
          <Text style={styles.resultTitle}>Field Validation Result</Text>
          {validationResult.every((r) => r.valid) ? (
            <Text style={styles.success}>All field definitions are valid</Text>
          ) : (
            <View>
              <Text style={styles.error}>Invalid field definitions found</Text>
              <Text style={styles.error}>
                WatermelonDB version is too old, the validateColumnSchema
                function is not exported in this version (this function is only
                exposed in newer versions)
              </Text>
            </View>
          )}
          {validationResult.map((item, i) => (
            <View key={i} style={styles.validationItem}>
              <Text>
                Field {item.column}:{" "}
                {item.valid ? "Valid" : `Invalid (${item.error})`}
              </Text>
            </View>
          ))}
        </View>
      )}

      {createResult && (
        <View style={styles.result}>
          <Text
            style={[
              styles.resultTitle,
              { color: createResult.success ? "green" : "red" },
            ]}
          >
            {createResult.success ? "Operation Successful" : "Operation Failed"}
          </Text>
          <Text>{createResult.message}</Text>
          {createResult.error && (
            <Text style={styles.error}>{createResult.error}</Text>
          )}
          {createResult.tables && (
            <View>
              <Text>Created tables:</Text>
              {createResult.tables.map((table, i) => (
                <Text key={i}>- {table}</Text>
              ))}
            </View>
          )}
        </View>
      )}
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: "#f5f5f5",
  },
  title: {
    fontSize: 18,
    fontWeight: "bold",
    marginBottom: 20,
    textAlign: "center",
  },
  buttons: {
    flexDirection: "row",
    gap: 10,
    marginBottom: 20,
    flexWrap: "wrap",
  },
  result: {
    padding: 15,
    backgroundColor: "white",
    borderRadius: 8,
    elevation: 2,
    marginBottom: 20,
  },
  resultTitle: {
    fontSize: 16,
    fontWeight: "bold",
    marginBottom: 10,
  },
  validationItem: {
    marginVertical: 4,
    padding: 4,
    borderBottomWidth: 1,
    borderBottomColor: "#eee",
  },
  success: {
    color: "green",
    marginBottom: 10,
  },
  error: {
    color: "red",
  },
});

export default SchemaExample;
```

```js
//  jsi: ture
// jsi: true
import React, { useState } from "react";
import { View, Text, Button, StyleSheet, ScrollView } from "react-native";
import {
  appSchema,
  tableSchema,
  tableName,
  columnName,
  validateColumnSchema,
} from "@nozbe/watermelondb/Schema";
import { Database } from "@nozbe/watermelondb";
import SQLiteAdapter from "@nozbe/watermelondb/adapters/sqlite";
import { schemaMigrations } from "@nozbe/watermelondb/Schema/migrations";

const userTable = tableName("users");

const userColumns = {
  name: columnName("name"),
  email: columnName("email"),
  age: columnName("age"),
};

const userTableSchema = tableSchema({
  name: userTable,
  columns: [
    { name: userColumns.name, type: "string" },
    { name: userColumns.email, type: "string", isIndexed: true },
    { name: userColumns.age, type: "number", isOptional: true },
  ],
});

const userInfoTable = tableName("user_info");
const userInfoColumns = {
  userId: columnName("user_id"),
  address: columnName("address"),
  phone: columnName("phone"),
};
const userInfoTableSchema = tableSchema({
  name: userInfoTable,
  columns: [
    { name: userInfoColumns.userId, type: "string", isIndexed: true },
    { name: userInfoColumns.address, type: "string" },
    { name: userInfoColumns.phone, type: "string", isOptional: true },
  ],
});

const orderTable = tableName("order");
const orderTableSchema = tableSchema({
  name: orderTable,
  columns: [
    { name: columnName("order_no"), type: "string", isIndexed: true },
    { name: columnName("user_id"), type: "string", isIndexed: true },
    { name: columnName("amount"), type: "number" },
    { name: columnName("status"), type: "string", defaultValue: "pending" },
  ],
});

const productTable = tableName("product");
const productTableSchema = tableSchema({
  name: productTable,
  columns: [
    { name: columnName("product_name"), type: "string" },
    { name: columnName("price"), type: "number" },
    { name: columnName("stock"), type: "number", defaultValue: 0 },
  ],
});

const tableSchemaMap = {
  tableName: userTableSchema,
  columnName: userInfoTableSchema,
  tableSchema: orderTableSchema,
  appSchema: productTableSchema,
};

const getAppDatabaseSchema = (tableSchema) => {
  return appSchema({
    version: 1,
    tables: [tableSchema],
  });
};

const validateUserColumns = () => {
  const results = [];
  userTableSchema.columnArray.forEach((column) => {
    try {
      validateColumnSchema(column);
      results.push({ column: column.name, valid: true });
    } catch (error) {
      results.push({ column: column.name, valid: false, error: error.message });
    }
  });
  console.log(results);
  return results;
};

const initializeDatabase = (tableType) => {
  const targetTableSchema = tableSchemaMap[tableType] || userTableSchema;
  const adapter = new SQLiteAdapter({
    dbName: `watermelonT_${tableType}_db`,
    schema: getAppDatabaseSchema(targetTableSchema),
    jsi: true,
    migrations: schemaMigrations({ migrations: [] }),
  });

  adapter.initializingPromise;
  return new Database({ adapter, modelClasses: [] });
};

const SchemaExampleT = () => {
  const [validationResult, setValidationResult] = useState(null);
  const [createResult, setCreateResult] = useState(null);
  const [database, setDatabase] = useState({});

  const handleValidateSchema = () => {
    const results = validateUserColumns();
    setValidationResult(results);
    setCreateResult(null);
  };

  const handleCreateTables = (tableType) => {
    try {
      if (database[tableType]) {
        const tableName = tableSchemaMap[tableType]?.name || userTable;
        setCreateResult({
          success: true,
          message: `The database (${tableType}) already exists`,
          tables: [tableName],
        });
        return;
      }

      const db = initializeDatabase(tableType);
      setDatabase({ ...database, [tableType]: db });
      const tableName = tableSchemaMap[tableType]?.name || userTable;
      setCreateResult({
        success: true,
        message: `The database table (${tableType}) has been created successfully`,
        tables: [tableName],
      });
    } catch (error) {
      setCreateResult({
        success: false,
        message: `The database table (${tableType}) failed to be created`,
        error: error.message,
      });
    }
  };

  const handleClear = () => {
    setValidationResult(null);
    setCreateResult(null);
    setDatabase({});
  };

  return (
    <ScrollView style={styles.container}>
      <Text style={styles.title}>WatermelonDB Table Creation Example</Text>

      <View style={styles.buttons}>
        <Button
          title="Create the user table using ${tableName}"
          onPress={() => handleCreateTables("tableName")}
          color="#4CAF50"
        />
        <Button
          title="Create the user table using ${columnName}"
          onPress={() => handleCreateTables("columnName")}
          color="#4CAF50"
        />
        <Button
          title="Create the user table using ${tableSchema}"
          onPress={() => handleCreateTables("tableSchema")}
          color="#4CAF50"
        />
        <Button
          title="Create the user table using ${appSchema}"
          onPress={() => handleCreateTables("appSchema")}
          color="#4CAF50"
        />
        <Button
          title="Validate field definitions using validateColumnSchema"
          onPress={handleValidateSchema}
          color="#2196F3"
        />
        <Button title="Clear state" onPress={handleClear} color="#f44336" />
      </View>

      {validationResult && (
        <View style={styles.result}>
          <Text style={styles.resultTitle}>Field Validation Result</Text>
          {validationResult.every((r) => r.valid) ? (
            <Text style={styles.success}>All field definitions are valid</Text>
          ) : (
            <View>
              <Text style={styles.error}>Invalid field definitions found</Text>
              <Text style={styles.error}>
                WatermelonDB version is too old, the validateColumnSchema
                function is not exported in this version (this function is only
                exposed in newer versions)
              </Text>
            </View>
          )}
          {validationResult.map((item, i) => (
            <View key={i} style={styles.validationItem}>
              <Text>
                Field {item.column}:{" "}
                {item.valid ? "Valid" : `Invalid (${item.error})`}
              </Text>
            </View>
          ))}
        </View>
      )}

      {createResult && (
        <View style={styles.result}>
          <Text
            style={[
              styles.resultTitle,
              { color: createResult.success ? "green" : "red" },
            ]}
          >
            {createResult.success ? "Operation Successful" : "Operation Failed"}
          </Text>
          <Text>{createResult.message}</Text>
          {createResult.error && (
            <Text style={styles.error}>{createResult.error}</Text>
          )}
          {createResult.tables && (
            <View>
              <Text>Created tables:</Text>
              {createResult.tables.map((table, i) => (
                <Text key={i}>- {table}</Text>
              ))}
            </View>
          )}
        </View>
      )}
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: "#f5f5f5",
  },
  title: {
    fontSize: 18,
    fontWeight: "bold",
    marginBottom: 20,
    textAlign: "center",
  },
  buttons: {
    flexDirection: "row",
    gap: 10,
    marginBottom: 20,
    flexWrap: "wrap",
  },
  result: {
    padding: 15,
    backgroundColor: "white",
    borderRadius: 8,
    elevation: 2,
    marginBottom: 20,
  },
  resultTitle: {
    fontSize: 16,
    fontWeight: "bold",
    marginBottom: 10,
  },
  validationItem: {
    marginVertical: 4,
    padding: 4,
    borderBottomWidth: 1,
    borderBottomColor: "#eee",
  },
  success: {
    color: "green",
    marginBottom: 10,
  },
  error: {
    color: "red",
  },
});

export default SchemaExampleT;
```

## 2.Manual Link

This step is a guide for manually configuring native dependencies.
First, you need to open the HarmonyOS project harmony in the project using DevEco Studio.

### 1.Add overrides field to oh-package.json in the project root directory

In order to make the project depend on the same version of the RN SDK, you need to add an overrides field to the oh-package.json5 file in the root directory of the project, which points to the version of the RN SDK required by the project. The version to be replaced can be either a specific version number, a version range, or a locally existing HAR package or source code directory.
For the function of this field, please refer to the official documentation.(https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)：

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
  }
}
```

### 2. There are currently two methods:

There are currently two methods available:

1. Import via HAR package (This method will be deprecated after the IDE-related features are fully implemented, but it is the preferred method at present);
2. Directly link to the source code.

Method 1: Import via har package (recommended)

> [!TIP] The HAR package can be found in the harmony subfolder of the third-party library's installation directory.

Open the entry/oh-package.json5 file and append the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "0.72.32",
    "@react-native-ohos/watermelondb": "file:../../node_modules/@react-native-ohos/watermelondb/harmony/watermelondb.har"
  }
```

Click the sync button at the top right corner.

Or run this command in the terminal:

```bash
cd entry
ohpm install
```

Method 2: Link the source code directly

> [!TIP] For direct source code linking, refer to [Direct Source Code Linking Instructions](/zh-cn/link-source-code.md)

### 3.Configure CMakeLists and import WatermelonDBPackage

open `entry/src/main/cpp/CMakeLists.txt`，add：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules/@rnoh/react-native-openharmony/src/main/cpp")
set(RNOH_GENERATED_DIR "${CMAKE_CURRENT_SOURCE_DIR}/generated")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "${CMAKE_CURRENT_SOURCE_DIR}/generated/*.cpp") # this line is needed by codegen v1

+ add_subdirectory("${OH_MODULES}/@react-native-ohos/watermelondb/src/main/cpp" ./watermelondb)



add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_watermelondb)


# RNOH_END: manual_package_linking_2
```

open `entry/src/main/cpp/PackageProvider.cpp`，add：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "WatermelondbPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(
    Package::Context ctx) {
  return {
      std::make_shared<RNOHGeneratedPackage>(ctx), // generated by codegen v1
+         std::make_shared<WatermelondbPackage>(ctx)
  };
}
```

### 4. Import the watermelondb module on the ArkTS side

open `entry/src/main/ets/RNPackagesFactory.ets`，add：

```diff
...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+ import { WatermelonDBPackage } from '@react-native-ohos/watermelondb';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new WatermelonDBPackage(ctx)
  ];
 }
...
...
```

### 5.Run

Click the sync button in the upper right corner.

Alternatively, execute the following command in the terminal:

```bash
cd entry
ohpm install
```

Then compile and run the project.

## 3.Constraints and Limitations

### Compatibility Support

The content of this document has been verified based on the following versions：

1. RNOH：0.72.90; SDK：HarmonyOS NEXT Developer DB3; IDE: DevEco Studio: 5.0.5.220; ROM：NEXT.0.0.105;
2. RNOH：0.77.18; SDK：HarmonyOS 6.0.0 Release; IDE: DevEco Studio 6.0.0.858; ROM：6.0.0.112;

### Permission Requirements

#### Add the reason for applying for the above permissions in the entry directory

Open `entry/src/main/resources/base/element/string.json`，add：

```diff
...
{
  "string": [
+    {
+      "name": "module_desc",
+      "value": "moudle description"
+    },
+    {
+      "name": "EntryAbility_desc",
+      "value": "description"
+    },
+    {
+      "name": "EntryAbility_label",
+      "value": "WatermelonDB"
+    },
  ]
}
```

## 4.Properties

> [!TIP] "Platform"This column shows which platforms the property supports in the original third-party library。

> [!TIP] "HarmonyOS Support"A value of "yes" in this column means the HarmonyOS platform supports the property; "no" means it does not; "partially" means partial support. The usage method is consistent across platforms, and the effect is comparable to that on iOS or Android。

**Collection class**


| Name                      | Description                                                                    | Type     | Required | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| db                        | Get the reference to the database instance that this collection belongs to     | function | no       | iOS/Android | yes               |
| find                      | Query for matching records in the collection based on specified conditions     | function | yes      | iOS/Android | yes               |
| findAndObserve            | Query records and establish responsive observation to monitor data changes     | function | yes      | iOS/Android | yes               |
| create                    | Create and save new records in the collection                                  | function | yes      | iOS/Android | yes               |
| prepareCreate             | Pre - create a record object without immediately persisting it to the database | function | yes      | iOS/Android | yes               |
| prepareCreateFromDirtyRaw | Pre - create a record object from raw unvalidated data                         | function | yes      | iOS/Android | yes               |
| disposableFromDirtyRaw    | Create a one - time temporary record based on raw dirty data                   | function | yes      | iOS/Android | yes               |
| table                     | Get the name of the database table corresponding to this collection            | function | no       | iOS/Android | yes               |
| \_fetchQuery              | Execute the SQL query statement and return the complete result set             | function | no       | iOS/Android | no                |
| \_fetchIds                | Get the list of all record IDs that match the query criteria                   | function | no       | iOS/Android | no                |
| \_fetchCount              | Count the total number of records that satisfy the query criteria              | function | no       | iOS/Android | no                |
| \_unsafeFetchRaw          | Bypass the security checks to directly obtain the raw record data              | function | no       | iOS/Android | no                |
| \_fetchRecord             | Get the complete data content of a single record                               | function | no       | iOS/Android | no                |
| \_applyChangesToCache     | Apply the data changes to the in-memory cache system                           | function | no       | iOS/Android | no                |
| \_notify                  | Notify all registered observers that the data has changed                      | function | no       | iOS/Android | no                |
| schema                    | Get the data table structure definition corresponding to this collection       | function | no       | iOS/Android | yes               |
| experimentalSubscribe     | Subscribe to collection - level data change notifications                      | function | yes      | iOS/Android | yes               |

**Database class**


| Name                       | Description                                                                      | Type     | Required | Platform    | HarmonyOS Support |
| -------------------------- | -------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| get&lt;T extends Model&gt; | Retrieve a specific record from the database according to the model class and ID | function | yes      | iOS/Android | yes               |
| localStorage               | Get the local storage adapter of the database for key - value pair data          | function | yes      | iOS/Android | yes               |
| batch                      | Create batch operations to efficiently perform multiple database writes          | function | yes      | iOS/Android | yes               |
| write&lt;T&gt;             | Perform database modification operations in a write transaction                  | function | yes      | iOS/Android | yes               |
| read&lt;T&gt;              | Perform database query operations in a read - only transaction                   | function | yes      | iOS/Android | yes               |
| action&lt;T&gt;            | Perform database actions that require read and write permissions                 | function | yes      | iOS/Android | yes               |
| withChangesForTables       | Create an observer that monitors data changes in specified tables                | function | yes      | iOS/Android | yes               |
| experimentalSubscribe      | Subscribe to database - level change notifications                               | function | yes      | iOS/Android | yes               |
| unsafeResetDatabase        | Completely reset the database and clear all data                                 | function | no       | iOS/Android | yes               |
| \_ensurelnWtiter           | Ensure that the current operation is executed in the write thread                | function | yes      | iOS/Android | yes               |
| \_fataError                | Handle database fatal errors and terminate the connection                        | function | yes      | iOS/Android | yes               |

**Relation class**


| Name          | Description                                                                    | Type     | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| get id        | Get the unique identifier of the associated target model                       | function | no       | iOS/Android | yes               |
| set id        | Set the identifier value of the associated target model                        | function | no       | iOS/Android | yes               |
| fetch         | Asynchronously obtain the promise of complete data of the associated record    | function | no       | iOS/Android | yes               |
| then&lt;U&gt; | Support Promise chain calls to process asynchronously obtained associated data | function | no       | iOS/Android | yes               |
| set           | Establish an association relationship with another model instance              | function | no       | iOS/Android | yes               |
| observe       | Monitor real - time changes in associated model data                           | function | no       | iOS/Android | yes               |

**Model class**


| Name                                          | Description                                                                         | Type     | Required | Platform    | HarmonyOS Support |
| --------------------------------------------- | ----------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| associations                                  | Define the association relationship mapping between the model and other data tables | function | no       | iOS/Android | yes               |
| prepareMarkAsDeleted                          | Mark as deleted status                                                              | function | no       | iOS/Android | no                |
| \_getChanges                                  | Get the model change observation object                                             | function | no       | iOS/Android | yes               |
| get id                                        | Get the unique identifier of the instance                                           | function | no       | iOS/Android | yes               |
| get syncStatus                                | Get the data synchronization status                                                 | function | no       | iOS/Android | yes               |
| update                                        | Update the model and submit immediately                                             | function | no       | iOS/Android | yes               |
| prepareUpdate                                 | Prepare for update                                                                  | function | no       | iOS/Android | yes               |
| prepareDestroyPermanently                     | Prepare for permanent destruction without execution                                 | function | no       | iOS/Android | yes               |
| markAsDeleted                                 | Delete the model and submit                                                         | function | no       | iOS/Android | yes               |
| destroyPermanently                            | Permanently delete model records                                                    | function | no       | iOS/Android | yes               |
| experimentalMarkAsDeleted                     | Soft delete function                                                                | function | no       | iOS/Android | yes               |
| experimentalDestroyPermanently                | Permanent delete function                                                           | function | no       | iOS/Android | yes               |
| observe                                       | Monitor model data changes                                                          | function | no       | iOS/Android | yes               |
| collection                                    | Get the associated data set                                                         | function | no       | iOS/Android | yes               |
| get collections                               | Get all collection mappings                                                         | function | no       | iOS/Android | yes               |
| get database                                  | Get the database instance                                                           | function | no       | iOS/Android | yes               |
| get db                                        | Get the database instance                                                           | function | no       | iOS/Android | yes               |
| get asModel                                   | Return its own instance                                                             | function | no       | iOS/Android | yes               |
| callWriter&lt;T&gt;                           | Perform operations in the write thread                                              | function | yes      | iOS/Android | yes               |
| callReader&lt;T&gt;                           | Perform queries in the read thread                                                  | function | yes      | iOS/Android | yes               |
| subAction&lt;T&gt;                            | Perform sub - operations in a transaction                                           | function | yes      | iOS/Android | yes               |
| get table                                     | Get the corresponding data table name                                               | function | no       | iOS/Android | yes               |
| prepareCreate                                 | Prepare to create a model                                                           | function | yes      | iOS/Android | yes               |
| \_prepareCreateFromDirtyRaw                   | Create a model from dirty data                                                      | function | yes      | iOS/Android | yes               |
| \_disposableFromDirtyRaw                      | Create a one - time model                                                           | function | yes      | iOS/Android | yes               |
| experimentalSubscribe                         | Experimental subscription to model changes                                          | function | yes      | iOS/Android | yes               |
| \_notifyChanged                               | Internally notify model changes                                                     | function | no       | iOS/Android | yes               |
| \_notifyDestroyed                             | Internally notify model destruction                                                 | function | no       | iOS/Android | yes               |
| \_getRaw                                      | Internally get the original field value                                             | function | yes      | iOS/Android | yes               |
| \_setRaw                                      | Internally set field values and mark changes                                        | function | yes      | iOS/Android | yes               |
| \_dangerouslySetRawWithoutMarkingColumnChange | Internally unsafely set field values                                                | function | yes      | iOS/Android | yes               |
| \_ensureCanSetRaw                             | Internally ensure that raw values can be set                                        | function | no       | iOS/Android | yes               |
| \_ensureNotDisposable                         | Internally ensure non - disposable instances                                        | function | yes      | iOS/Android | yes               |

**Query class**


| Name                             | Description                                          | Type     | Required | Platform    | HarmonyOS Support |
| -------------------------------- | ---------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| pipe&lt;T&gt;                    | Perform chain conversion operations on query results | function | no       | iOS/Android | yes               |
| fetch                            | Execute the query immediately to get results         | function | no       | iOS/Android | yes               |
| then&lt;U&gt;                    | Support Promise chain calls for query results        | function | no       | iOS/Android | yes               |
| observe                          | Monitor real - time changes in query results         | function | no       | iOS/Android | yes               |
| observeWithColumns               | Monitor query results of specific field changes      | function | yes      | iOS/Android | yes               |
| fetchCount                       | Get the quantity statistics of query results         | function | yes      | iOS/Android | yes               |
| get count                        | Get the total number of query results                | function | no       | iOS/Android | yes               |
| observeCount                     | Monitor changes in the number of query results       | function | no       | iOS/Android | yes               |
| fetchIds                         | Get the ID list of query results                     | function | no       | iOS/Android | yes               |
| unsafeFetchRaw                   | Unsafely get raw query data                          | function | no       | iOS/Android | yes               |
| experimentalSubscribe            | Experimental query subscription function             | function | yes      | iOS/Android | yes               |
| experimentalSubscribeWithColumns | Experimental field change subscription               | function | yes      | iOS/Android | yes               |
| experimentalSubscribeToCount     | Experimental quantity change subscription            | function | yes      | iOS/Android | yes               |
| markAllAsDeleted                 | Mark all query results as soft deleted               | function | no       | iOS/Android | yes               |
| destroyAllPermanently            | Permanently delete all query results                 | function | no       | iOS/Android | yes               |
| get modelClass                   | Get the model class corresponding to the query       | function | no       | iOS/Android | yes               |
| get table                        | Get the main table name of the query                 | function | no       | iOS/Android | yes               |
| get secondaryTables              | Get the associated tables involved in the query      | function | no       | iOS/Android | yes               |
| get allTables                    | Get all tables related to the query                  | function | no       | iOS/Android | yes               |
| get associations                 | Get the association relationships of the query       | function | no       | iOS/Android | yes               |
| serialize                        | Serialize the query into a transferable format       | function | no       | iOS/Android | yes               |

**Schema class**


| Name                             | Description                                                         | Type     | Required | Platform    | HarmonyOS Support |
| -------------------------------- | ------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| tableName&lt;T extends Model&gt; | Define the name of the database table                               | function | yes      | iOS/Android | yes               |
| columnName                       | Define the name of the database field                               | function | yes      | iOS/Android | yes               |
| appSchema                        | Define the structural schema of the entire application database     | function | yes      | iOS/Android | yes               |
| validateColumnsSchema            | Verify the validity of the field schema definition                  | function | yes      | iOS/Android | yes               |
| tableSchema                      | Define the structure and field configuration of a single data table | function | yes      | iOS/Android | yes               |

## 5.Pending Issues

- [ ]  \_fetchQuery Some parameters of the interface are not supported on HarmonyOS. As an underlying method provided for other modules, it cannot be called directly. [issue#2](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/issues/2)
- [ ]  \_fetchIds Some parameters of the interface are not supported on HarmonyOS. As an underlying method provided for other modules, it cannot be called directly. [issue#2](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/issues/2)
- [ ]  \_fetchCount Some parameters of the interface are not supported on HarmonyOS. As an underlying method provided for other modules, it cannot be called directly. [issue#2](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/issues/2)
- [ ]  \_unsafeFetchRaw Some parameters of the interface are not supported on HarmonyOS. As an underlying method provided for other modules, it cannot be called directly. [issue#2](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/issues/2)
- [ ]  \_fetchRecord Some parameters of the interface are not supported on HarmonyOS. As an underlying method provided for other modules, it cannot be called directly. [issue#2](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/issues/2)
- [ ]  \_applyChangesToCache Some parameters of the interface are not supported on HarmonyOS. As an underlying method provided for other modules, it cannot be called directly. [issue#2](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/issues/2)
- [ ]  \_notify Some parameters of the interface are not supported on HarmonyOS. As an underlying method provided for other modules, it cannot be called directly. [issue#2](https://gitcode.com/OpenHarmony-RN/rntpc_watermelondb/issues/2)

## 6.Others

## 7.Open Source License

This project is based on [The MIT License (MIT)](https://github.com/Nozbe/WatermelonDB/blob/master/LICENSE) ，Feel free to enjoy and contribute to the open source project。
