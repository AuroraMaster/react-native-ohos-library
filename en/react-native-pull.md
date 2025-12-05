> Template Version: v0.2.2

<p align="center">
<h1 align="center"> <code>react-native-pull</code> </h1>
</p>
<p align="center">
 <a href="https://github.com/greatbsky/react-native-pull/blob/master">
     <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
 </a>
     <a href="https://github.com/greatbsky/react-native-pull/blob/master/LICENSE">
     <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
 </a>
</p>



> [!TIP] [Github Address](https://github.com/react-native-oh-library/react-native-pull)

## Installation & Usage

| Third-party Library Version | Release Information                                                  | Supported RN Version |
|-----------------------------| --------------------------------------------------------------------- | -------------------- |
| 2.0.4                       | [@react-native-oh-tpl/react-native-pull releases](https://github.com/react-native-oh-library/react-native-pull/releases) | 0.72                 |
| 2.1.0                       | [@react-native-ohos/react-native-pull Releases](https://gitcode.com/openharmony-sig/rntpc_react-native-pull/releases)   | 0.77                 |

For older versions not published to npm, please refer to the [Installation Guide](/zh-cn/tgz-usage.md) to install the tgz package.

Navigate to your project directory and enter the following commands:

<!-- tabs:start -->

#### **npm**

```bash
# 0.72
npm install @react-native-oh-tpl/react-native-pull
# 0.77
npm install @react-native-ohos/react-native-pull
```

#### **yarn**

```bash
# 0.72
yarn add @react-native-oh-tpl/react-native-pull
#0.77
yarn add @react-native-ohos/react-native-pull
```

<!-- tabs:end -->

The following demo code demonstrates basic usage scenarios of this library:

> [!WARNING] The import library name remains unchanged when using.

**PullViewDemo**

> Code Example

```js
import React, { Component, useState } from 'react';
import {
  StyleSheet,
  Text,
  View,
  ActivityIndicator,
  Dimensions,
} from 'react-native';

import { PullView } from 'react-native-pull';

interface testObjType {
  pulling: String,
  pullok: String,
  pullrelease: String,
  pushing: String,
  refresh: String,
  isPullEnd: String
}

const PullViewDemo = () => {

  const [count, setCount] = useState<string | number>(0);
  let testObj: testObjType = {
    pulling: '',
    pullok: '',
    pullrelease: '',
    pushing: '',
    refresh: '',
    isPullEnd: ''
  };
  const [data, setData] = useState(testObj);
  const onPulling = () => {
    testObj.pulling = 'pulling--------->'
    setData(testObj)
  };
  const onPullOk = () => {
    testObj.pullok = 'pullok--------->'
    setData(testObj)
  };
  const onPullRelease = (resolve: any) => {
    //do something
    testObj.pullrelease = 'pullrelease--------->'
    setData(testObj)
    setTimeout(() => {
      resolve();
    }, 3000);
  };
  const onPushing = (gesturePosition: any) => {
    testObj.pushing = 'x:' + gesturePosition.x + '------' + 'y：' + gesturePosition.y
    setData(testObj)
  };
  const topIndicatorRender = (pulling: any, pullok: any, pullrelease: any) => {
    if (pulling) {
      setCount('Pull to refresh pulling...')
    } else if (pullok) {
      setCount('Release to refresh pullok......')
    } else if (pullrelease) {
      setCount('Refreshing pullrelease......')
    }
    return (
      <View style={{ flexDirection: 'row', justifyContent: 'center', alignItems: 'center', height: 60 }}>
        <ActivityIndicator size="small" color="gray" />
        {pulling ? <Text>{count}</Text> : null}
        {pullok ? <Text>{count}</Text> : null}
        {pullrelease ? <Text>{count}</Text> : null}
      </View>
    );
  };

  return (
    <View style={[styles.container]}>
      <PullView style={{ width: Dimensions.get('window').width }}
        onPulling={onPulling}
        onPullOk={onPullOk}
        isPullEnd={true}
        onPullRelease={onPullRelease}
        onPushing={onPushing}
        topIndicatorRender={topIndicatorRender}
        topIndicatorHeight={60}>
        <View style={{ backgroundColor: '#eeeeee' }}>
          <Text>1***************</Text>
          <Text>onPulling:{testObj.pulling}</Text>
          <Text>3</Text>
          <Text>onPullOk:{testObj.pullok}</Text>
          <Text>5</Text>
          <Text>onPullRelease:{testObj.pullrelease}</Text>
          <Text>7</Text>
          <Text>onPushing:{testObj.pushing}</Text>
          <Text>9</Text>
        </View>
      </PullView>
    </View>
  );
};
export default PullViewDemo;
const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
});
```

**PullListDemo**

> Code Example

```jsx
import React, { useState } from 'react';
import {
  StyleSheet,
  Text,
  View,
  ActivityIndicator,
  Dimensions,
  RefreshControl
} from 'react-native';
import {PullList} from 'react-native-pull';

interface testObjType {
  pulling: String,
  pullok: String,
  pullrelease: String,
  pushing: String,
  refresh: String,
  isPullEnd: String
}

const PullListDemo = () => {
  let testObj: testObjType = {
    pulling:'',
    pullok:'',
    pullrelease:'',
    pushing:'',
    refresh:'',
    isPullEnd:''
   };

   const [count, setCount] = useState<string | number>(0);
   const [data, setData] = useState(testObj);
    const [stateList, setStateList] = useState(
         [
                 {
                   id: 1,
                   title: '------>Item1',
                 },
                 {
                   id: 2,
                   title: '------>Item2',
                 },
                 {
                   id: 3,
                   title: '------>Item3',
                 },
                 {
                   id: 4,
                   title: '------>Item4',
                 },
                 {
                   id: 5,
                   title: '------>Item5',
                 },
                 {
                   id: 6,
                   title: '------>Item6',
                 },
                 {
                   id: 7,
                   title: '------>Item7',
                 },
                 {
                   id: 8,
                   title: '------>Item8',
                 },
                 {
                   id: 9,
                   title: '------>Item9',
                 },
                  {
                    id: 10,
                    title: '------>Item10',
                  },
                  {
                    id: 11,
                    title: '------>Item11',
                  },
                  {
                    id: 12,
                    title: '------>Item12',
                  },
               ]
    );

   const onPulling = () => {
      testObj.pulling='pulling--------->'
      setData(testObj)
   };

   const onPullOk = () => {
      testObj.pullok='pullok--------->'
      setData(testObj)
   };

   const onPullRelease = (resolve: any) => {
        //do something
        testObj.pullrelease='pullrelease--------->'
        setData(testObj)
        setTimeout(() => {
         setStateList([
                                       {
                                         id: 1,
                                         title: '------>Item1',
                                       },
                                       {
                                         id: 2,
                                         title: '------>Item2',
                                       },
                                       {
                                         id: 3,
                                         title: '------>Item3',
                                       },
                                       {
                                         id: 4,
                                         title: '------>Item4',
                                       },
                                       {
                                         id: 5,
                                         title: '------>Item5',
                                       },
                                       {
                                         id: 6,
                                         title: '------>Item6',
                                       },
                                       {
                                         id: 7,
                                         title: '------>Item7',
                                       },
                                       {
                                         id: 8,
                                         title: '------>Item8',
                                       },
                                       {
                                         id: 9,
                                         title: '------>Item9',
                                       },
                                        {
                                          id: 10,
                                          title: '------>Item10',
                                        },
                                        {
                                          id: 11,
                                          title: '------>Item11',
                                        },
                                        {
                                          id: 12,
                                          title: '------>Item12',
                                        },
                                     ]);
            resolve();
        }, 3000);
    };


    const onPushing = (gesturePosition: any) => {
        testObj.pushing= 'x:' + gesturePosition.x + '------' + 'y：' + gesturePosition.y
        setData(testObj)
    };

    const topIndicatorRender = (pulling: any, pullok: any, pullrelease: any) => {
      if (pulling) {
          setCount('Current PullList Status: pulling...')
      } else if (pullok) {
          setCount('Current PullList Status: pullok......')
      } else if (pullrelease) {
          setCount('Current PullList Status: pullrelease......')
      }

  return (
      <View style={{flexDirection: 'row', justifyContent: 'center', alignItems: 'center', height: 60}}>
          <ActivityIndicator size="small" color="gray" />
          {pulling ? <Text>{count}</Text> : null}
          {pullok ? <Text>{count}</Text> : null}
          {pullrelease ? <Text>{count}</Text> : null}
      </View>
  );
};


    const renderHeader = () => {
      return (
          <View style={{height: 50, backgroundColor: '#eeeeee', alignItems: 'center', justifyContent: 'center'}}>
              <Text style={{fontWeight: 'bold'}}>This is header</Text>
          </View>
      );
    }

   const renderRow = ({item}: any) => {
      return (
          <View style={{height: 50, backgroundColor: '#fafafa', alignItems: 'center', justifyContent: 'center'}}>
              <Text>{item.title}</Text>
          </View>
      );
    }

   const renderFooter = () => {
      return (
          <View style={{height: 100}}>
              <ActivityIndicator />
          </View>
      );
    }

   const loadMore = () => {
      const list: { id: number; title: string }[] = []
      const num = stateList.length
        for(var i = 0; i < 5; i++) {
            list.push({
                id: (i + 1 + num),
                title: `------>Item${(i+num+1)}`,
            })
        }
       setTimeout(() => {
          setStateList([...stateList,...list]);
        }, 1000);
    }

    const [refreshing, setRefreshing] = useState(false)
    const onRefresh = () => {
      // Data loading logic
      setRefreshing(true)
      // After data loading is complete
      setTimeout(() => {
        setRefreshing(false)
      }, 2000); // Assuming data loading takes 2 seconds
    };
    const refreshControl = (
      <RefreshControl
        refreshing={refreshing}
        onRefresh={onRefresh}
        tintColor="#ff0000" // Optional, set refresh indicator color
        title="Loading..." // Optional, set text displayed during refresh
        colors={['#ff0000', '#00ff00', '#0000ff']} // Optional, set refresh indicator color array
        progressBackgroundColor="#ffffff" // Optional, set progress background color
      />
    );

    return (
      <View style={[styles.container]}>
      <PullList style={{width: Dimensions.get('window').width}}
            onPulling={onPulling}
            onPullOk={onPullOk}
            isPullEnd={true}
            onPullRelease={onPullRelease}
            onPushing={onPushing}
            topIndicatorRender={topIndicatorRender}
            topIndicatorHeight={60}
            pageSize={5}
            scrollViewProps={{
                scrollEventThrottle: 16, // Reduce scroll event delay, improve scroll responsiveness
              }}
            initialListSize={5}
            onEndReached={loadMore}
            onEndReachedThreshold={60}
            renderItem={renderRow}
            ListFooterComponent={renderFooter}
            ListHeaderComponent={renderHeader}
            data={stateList}
            keyExtractor={(item:any) => item.id}
          />
      </View>
    );
};

const styles = StyleSheet.create({
 container: {
    flex: 1,
    flexDirection: 'column',
    backgroundColor: '#F5FCFF',
    width:'100%',
    height:'100%',
    overflow: 'scroll'
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
});

export default PullListDemo;

```

## Constraints & Limitations

### Compatibility

To use this library, you need to use the correct React-Native and RNOH versions. Additionally, you need to use the matching DevEco Studio and phone ROM.

Verified in the following versions:

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Properties

> [!TIP] The "Platform" column indicates the platforms supported by the original third-party library.

> [!TIP] "HarmonyOS Support" column: yes means the property is supported on HarmonyOS platform; no means not supported; partially means partially supported. The usage method is cross-platform consistent, with effects benchmarked against iOS or Android effects.

**`PullView` & `PullList` Pull-to-refresh Properties**

| Name                 | Description                                                                                                                                                                | Type     | Required | Platform    | HarmonyOS Support |
| -------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `style`              | Set component styles, such as width/height/backgroundColor, etc.                                                                                                           | Style    | no       | android,ios | yes               |
| `onPulling`          | Method executed when in `pulling` state                                                                                                                                     | function | no       | android,ios | yes               |
| `onPullOk`           | Method executed when in `pullok` state                                                                                                                                      | function | no       | android,ios | yes               |
| `onPullRelease`      | Method executed when in `pullrelease` state, accepts one parameter: `resolve`, should call `resolve()` after completing operations.                                        | function | no       | android,ios | yes               |
| `onPushing`          | Method executed when pushing from bottom to top, accepts one parameter: `gesturePosition`. gesturePosition is a JSON format {x, y} object, gesturePosition.y > 0 when pulling from top to bottom, gesturePosition.y < 0 when pushing from bottom to top. | function | no       | android,ios | yes               |
| `topIndicatorRender` | Rendering method for top refresh indicator component, accepts 4 parameters: `ispulling`, `ispullok`, `ispullrelease`, `gesturePosition`, you can use `gesturePosition` to define animated header. | function | no       | android,ios | yes               |
| `topIndicatorHeight` | Height of top refresh indicator component, required if topIndicatorRender is defined                                                                                        | number   | no       | android,ios | yes               |
| `isPullEnd`          | Whether pull has ended, if true then hide top refresh indicator component, not required                                                                                     | boolean  | no       | android,ios | no              |
| `onRefresh`          | Method called when starting refresh                                                                                                                                         | function | no       | android,ios | yes               |
| `refreshing`         | Indicates whether refreshing is in progress                                                                                                                                 | function | no       | android,ios | yes               |

## Known Issues

## Others

- isPullEnd property not working; [issue#28](https://github.com/greatbsky/react-native-pull/issues/28)

## Open Source License

This project is based on [The MIT License (MIT)](https://github.com/greatbsky/react-native-pull/blob/master/LICENSE), feel free to enjoy and participate in open source.