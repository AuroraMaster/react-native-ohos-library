> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sqlite-storage</code> </h1>
</p>  
<p align="center">
    <a href="https://github.com/andpor/react-native-sqlite-storage">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/andpor/react-native-sqlite-storage/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-sqlite-storage)


## Installation and Usage

Please refer to the Releases page of the third-party library for the corresponding version information

| Third-party Library Version | Release Information                                                                                                                                    | Supported RN Version |
|-----------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------| ---------- |
| <= 6.0.1-0.1.1@deprecated      | [@react-native-oh-tpl/react-native-sqlite-storage Releases(deprecated)](https://github.com/react-native-oh-library/react-native-sqlite-storage/releases) | 0.72       |
| 6.0.2      | [@react-native-ohos/react-native-sqlite-storage Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sqlite-storage/releases)                        | 0.72       |
| 6.1.0      | [@react-native-ohos/react-native-sqlite-storage Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-sqlite-storage/releases)                        | 0.77       |

For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-sqlite-storage
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-sqlite-storage
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
/**
 * @format
 */
import React, {Component} from 'react';
import { StyleSheet, Text, View, FlatList} from 'react-native';
import SQLite from 'react-native-sqlite-storage';
SQLite.DEBUG(true);
SQLite.enablePromise(false);

const database_name = 'Test.db';
const database_version = '1.0';
const database_displayname = 'SQLite Test Database';
const database_size = 200000;
let db: any;
const Item = (props: any) => {
  const { title } = props;
  return(
    <View>
      <Text>{title}</Text>
    </View>
  )
};

interface SQLiteDemo {
  progress: string[]
}

interface State {
  progress: string[]
}

interface rowsType {
  item: any,
  length: number
}

interface ResultType {
  rows: rowsType
}

class SQLiteDemo extends Component<{}, State> {
  constructor(props: any) {
    super(props);
    this.progress = [];
    this.state = {
      progress: [],
    };
  }

  updateProgress = (text: string, resetState?: boolean) => {
    let progress: string[] = [];
    if (!resetState) {
      progress = [...this.progress];
    }
    progress.push(text);
    this.progress = progress;
    this.setState({
      progress,
    });
  };

  componentWillUnmount = () => {
    this.closeDatabase();
  };

  errorCB = (err: any) => {
    console.log('error: ', err);
    this.updateProgress('Error: ' + (err.message || err));
    return false;
  };

  successCB = () => {
    console.log('SQL executed ...');
  };

  openCB = () => {
    this.updateProgress('Database OPEN');
  };

  closeCB = () => {
    this.updateProgress('Database CLOSED');
  };

  deleteCB = () => {
    console.log('Database DELETED');
    this.updateProgress('Database DELETED');
  };

  // eslint-disable-next-line no-shadow
  populateDatabase = (db: any) => {
    this.updateProgress('Database integrity check');
    db.executeSql(
      'SELECT 1 FROM Version LIMIT 1',
      [],
      () => {
        this.updateProgress('Database is ready ... executing query ...');
        db.transaction(this.queryEmployees, this.errorCB, () => {
          this.updateProgress('Processing completed');
        });
      },
      (error: any) => {
        console.log('received version error:', error);
        this.updateProgress('Database not yet ready ... populating data');
        db.transaction(this.populateDB, this.errorCB, () => {
          this.updateProgress('Database populated ... executing query ...');
          db.transaction(this.queryEmployees, this.errorCB, () => {
            console.log('Transaction is now finished');
            this.updateProgress('Processing completed');
            // this.closeDatabase();
          });
        });
      },
    );
  };

  populateDB = (tx: any) => {
    this.updateProgress('Executing DROP stmts');

    tx.executeSql('DROP TABLE IF EXISTS Employees;');
    tx.executeSql('DROP TABLE IF EXISTS Offices;');
    tx.executeSql('DROP TABLE IF EXISTS Departments;');

    this.updateProgress('Executing CREATE stmts');

    tx.executeSql(
      'CREATE TABLE IF NOT EXISTS Version( ' +
        'version_id INTEGER PRIMARY KEY NOT NULL); ',
      [],
      this.successCB,
      this.errorCB,
    );

    tx.executeSql(
      'CREATE TABLE IF NOT EXISTS Departments( ' +
        'department_id INTEGER PRIMARY KEY NOT NULL, ' +
        'name VARCHAR(30) ); ',
      [],
      this.successCB,
      this.errorCB,
    );

    tx.executeSql(
      'CREATE TABLE IF NOT EXISTS Offices( ' +
        'office_id INTEGER PRIMARY KEY NOT NULL, ' +
        'name VARCHAR(20), ' +
        'longtitude FLOAT, ' +
        'latitude FLOAT ) ; ',
      [],
      this.successCB,
      this.errorCB,
    );

    tx.executeSql(
      'CREATE TABLE IF NOT EXISTS Employees( ' +
        'employe_id INTEGER PRIMARY KEY NOT NULL, ' +
        'name VARCHAR(55), ' +
        'office INTEGER, ' +
        'department INTEGER, ' +
        'custom_info TEXT DEFAULT "",' +
        'FOREIGN KEY ( office ) REFERENCES Offices ( office_id ) ' +
        'FOREIGN KEY ( department ) REFERENCES Departments ( department_id ));',
      [],
    );

    this.updateProgress('Executing INSERT stmts');

    tx.executeSql(
      'INSERT INTO Departments (name) VALUES ("Client Services");',
      [],
    );
    tx.executeSql(
      'INSERT INTO Departments (name) VALUES ("Investor Services");',
      [],
    );
    tx.executeSql('INSERT INTO Departments (name) VALUES ("Shipping");', []);
    tx.executeSql(
      'INSERT INTO Departments (name) VALUES ("Direct Sales");',
      [],
    );

    tx.executeSql(
      'INSERT INTO Offices (name, longtitude, latitude) VALUES ("ZhangSan", 59.8,  34.);',
      [],
    );
    tx.executeSql(
      'INSERT INTO Offices (name, longtitude, latitude) VALUES ("Lisi", 15.7, 54.);',
      [],
    );
    tx.executeSql(
      'INSERT INTO Offices (name, longtitude, latitude) VALUES ("Wangwu", 35.3, 12.);',
      [],
    );
    tx.executeSql(
      'INSERT INTO Offices (name, longtitude, latitude) VALUES ("Zhaoliu", 10.7, 14.);',
      [],
    );

    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("haha", 2, 4, \'{"known": true}\')',
      [],
    );
    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("yueyue", 2, 4, \'{"known": true}\')',
      [],
    );
    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("linlin", 3, 4, \'{"known": true}\')',
      [],
    );
    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("huahua", 3, 3, \'{"known": true}\')',
      [],
    );
    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("yangyang", 1, 3, \'{"known": false}\')',
      [],
    );
    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("zaza", 1, 3, \'{"known": true}\')',
      [],
    );
    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("lulu", 2, 4, \'{"known": true, "impeached": true}\')',
      [],
    );
    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("luoluo", 2, 2, \'{"known": true}\')',
      [],
    );
    tx.executeSql(
      'INSERT INTO Employees (name, office, department, custom_info) VALUES ("bubu", 2, 1, \'{"known": true}\')',
      [],
    );

    console.log('all config SQL done');
  };

  queryEmployees = async (tx: any) => {
    console.log('Executing JSON1 queries...');

    // 1. JSON_OBJECT
    await tx.executeSql(
      "SELECT JSON_OBJECT('name', e.name, 'office_id', e.office, 'department_id', e.department) AS data FROM Employees e",
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 2. JSON_ARRAY
    // Expected: [1,2,"3",4]
    await tx.executeSql(
      "SELECT JSON_ARRAY(1, 2, '3', 4) AS data ",
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 3. JSON_ARRAY_LENGTH
    // Expected: 4
    await tx.executeSql(
      "SELECT JSON_ARRAY_LENGTH('[1, 2, 3, 4]') AS data",
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 4. JSON_EXTRACT
    await tx.executeSql(
      "SELECT JSON_EXTRACT(e.custom_info, '$.known')  AS data FROM Employees e",
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 5. JSON_INSERT
    // Expected: {"a":1,"b":2,"c":3}
    await tx.executeSql(
      'SELECT JSON_INSERT(\'{"a": 1, "b": 2}\', \'$.c\', 3)  AS data',
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 6. JSON_REPLACE
    // Expected: {"a":1,"b":3}
    await tx.executeSql(
      'SELECT JSON_REPLACE(\'{"a": 1, "b": 2}\', \'$.b\', 3)  AS data',
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 7. JSON_SET
    // Expected: {"a":1,"b":123}
    await tx.executeSql(
      'SELECT JSON_SET(\'{"a": 1, "b": 2}\', \'$.b\', 123)  AS data',
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 8. JSON_REMOVE
    // Expected: {"a":1"}
    await tx.executeSql(
      'SELECT JSON_REMOVE(\'{"a": 1, "b": 2}\', \'$.b\')  AS data',
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 9. JSON_TYPE
    // Expected: integer
    await tx.executeSql(
      'SELECT JSON_TYPE(\'{"a": 1, "b": 2}\', \'$.a\')  AS data',
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 10. JSON_VALID
    // Expected: 0
    await tx.executeSql(
      'SELECT JSON_VALID(\'{"a": 1, "b": 2\')  AS data',
      [],
      this.querySuccess,
      this.errorCB,
    );

    // 11. JSON_QUOTE
    // Expected: "value"
    await tx.executeSql(
      "SELECT JSON_QUOTE('value')  AS data",
      [],
      this.querySuccess,
      this.errorCB,
    );
  };

  querySuccess = (tx: any, results: ResultType) => {
    this.updateProgress('Query completed');
    var len = results.rows.length;
    for (let i = 0; i < len; i++) {
      let row = results.rows.item(i);
      this.updateProgress(`${row.data}`);
    }
  };

  loadAndQueryDB = () => {
    this.updateProgress('Opening database ...', true);
    this.updateProgress('Database OPEN');
    db = SQLite.openDatabase(
      database_name,
      database_version,
      database_displayname,
      database_size,
      this.openCB,
      this.errorCB,
    );
    this.populateDatabase(db);
  };

  deleteDatabase = () => {
    this.updateProgress('Deleting database');
    SQLite.deleteDatabase(database_name, this.deleteCB, this.errorCB);
  };

  closeDatabase = () => {
    if (db) {
      console.log('Closing database ...');
      this.updateProgress('Closing database');
      db.close(this.closeCB, this.errorCB);
    } else {
      this.updateProgress('Database CLOSE callback function error');
      // this.updateProgress('Database was not OPENED');
    }
  };

  runDemo = () => {
    this.updateProgress('Starting SQLite Callback Demo', true);
    this.loadAndQueryDB();
  };

  attachDatabase = () =>{
    if (db!=null) {
      this.updateProgress('Attach database ...');
      let dbMaster = SQLite.openDatabase('test2.db',database_version,database_displayname,database_size,
        () => {
          dbMaster.attach( database_name, database_displayname, () => console.log("Database attached successfully"), () => console.log("ERROR"))
          this.updateProgress('Attach database successfully');
        },
        this.errorCB,
      );
    } else {
      this.updateProgress('Database not open');
    } 

  }

  render = () => {
    return (
      <View style={styles.mainContainer}>
        <View style={styles.toolbar}>
          <Text style={styles.toolbarButton} onPress={this.runDemo}>
            Run Demo
          </Text>
          <Text style={styles.toolbarButton} onPress={this.attachDatabase}>
            Attach DB
          </Text>
          <Text style={styles.toolbarButton} onPress={this.closeDatabase}>
            Close DB
          </Text>
          <Text style={styles.toolbarButton} onPress={this.deleteDatabase}>
            Delete DB
          </Text>
        </View>
        <FlatList
          data={this.state.progress}
          renderItem={({item}) => <Item title={item} />}
          keyExtractor={(item: any )=> item.i}
        />
      </View>
    );
  };
}

var listStyles = StyleSheet.create({
  li: {
    borderBottomColor: '#c8c7cc',
    borderBottomWidth: 0.5,
    paddingTop: 15,
    paddingRight: 15,
    paddingBottom: 15,
  },
  liContainer: {
    backgroundColor: '#fff',
    flex: 1,
    paddingLeft: 15,
  },
  liIndent: {
    flex: 1,
  },
  liText: {
    color: '#333',
    fontSize: 17,
    fontWeight: '400',
    marginBottom: -3.5,
    marginTop: -3.5,
  },
});

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
  toolbar: {
    backgroundColor: '#51c04d',
    paddingTop: 30,
    paddingBottom: 10,
    flexDirection: 'row',
  },
  toolbarButton: {
    color: 'blue',
    textAlign: 'center',
    flex: 1,
  },
  mainContainer: {
    flex: 1,
  },
});
export default SQLiteDemo;

```

## Use Codegen

This library has been adapted for `Codegen`. Before using it, you need to proactively generate the bridge code for the third-party library. For details, please refer to the [Codegen Usage Documentation](/en/codegen.md).

## Link

|                                      | Is supported autolink | Supported RN Version |
|--------------------------------------|-----------------------|----------------------|
| ~6.1.0                               |  No                   |  0.77                |
| ~6.0.2                               |  Yes                  |  0.72                |
| <= 6.0.1-0.1.1@deprecated            |  No                   |  0.72                |

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

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-sqlite-storage": "file:../../node_modules/@react-native-ohos/react-native-sqlite-storage/harmony/sqlite_storage.har"
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

### 3. Configure CMakeLists and import SQLitePluginPackage

> If you are using version <= 6.0.1-0.1.1, please skip this chapter.

Open the `entry/src/main/cpp/CMakeLists.txt` file and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-sqlite-storage/src/main/cpp" ./sqlite_storage)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_sqlite_storage)
# RNOH_BEGIN: manual_package_linking_2
```

Open the `entry/src/main/cpp/PackageProvider.cpp` file and add the following code:

```diff
#include "RNOH/PackageProvider.h"
+ #include "SQLitePluginPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+        std::make_shared<SQLitePluginPackage>(ctx)
}
```

### 4. Introducing SQLitePluginPackage to ArkTS

Open the  `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {SQLitePluginPackage} from '@react-native-ohos/react-native-sqlite-storage/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SQLitePluginPackage(ctx)
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

## Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Verified in the following versions.

1. RNOH: 0.72.96; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;
2. RNOH: 0.72.33; SDK: HarmonyOS NEXT B1; IDE: DevEco Studio: 5.0.3.900; ROM: Next.0.0.71;
3. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio 6.0.0.858; ROM: 6.0.0.112;

## Static Methods

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| openDatabase  | Opens or initializes        | void  | yes |All     |  yes |
| transaction  | SQL transaction distribution        | void  | yes |All     |  yes |
| close  |Closes or releases a previously opened resource      | void  |  yes |All     |  yes |
| deleteDatabase  |Deletes a resource       |void   |  yes | All   |  yes |
| attach  | Connects or associates with an external resource or database  |  void  |  yes | All   |  yes|
| executeSql  |Executes a batch of SQL statements in the background without blocking the current thread or process | void   |  yes |All     |  yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/andpor/react-native-sqlite-storage/blob/master/LICENSE).