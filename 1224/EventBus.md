模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>EventBus</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/krasimir/EventBus">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/krasimir/EventBus)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm i eventbusjs@0.2.0
```

#### **yarn**

```bash
yarn add eventbusjs@0.2.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```tsx
import {useState} from 'react';
import {View, Button, StyleSheet, ScrollView, Text} from 'react-native';
import EventBus from 'eventbusjs';
const TAG = 'EventBus';
const styles = StyleSheet.create({
  main: {
    height: '100%',
  },
  mainItem: {
    marginTop: 20,
  },
  container: {
    paddingTop: 10,
    paddingBottom: 10,
    paddingLeft: 20,
    paddingRight: 20,
  },
  box: {
    marginTop: 10,
    marginBottom: 10,
    marginLeft: 20,
    marginRight: 20,
    height: 100,
    borderWidth: 1,
    borderColor: '#000',
  },
  title: {
    fontSize: 14,
    fontWeight: 'bold',
  },
});

function eventTest() {
  console.log(`${TAG},成功执行test_event类型的eventTest事件`);
}
var TestKeep1 = function (this: any) {
  this.className = 'TestKeep1';
  this.callback = function (event: Event) {
    console.log(
      `${TAG},className=${this.className},event=${JSON.stringify(event)}`,
    );
  };
};
var TestKeep2 = function (this: any) {
  this.className = 'TestKeep2';
  this.dispatchOurEvent = function () {
    EventBus.dispatch('callback_event', this);
  };
};
var t1 = new (TestKeep1 as any)();
var t2 = new (TestKeep2 as any)();

var TestParamsClass1 = function (this: any) {
  this.className = 'TestParamsClass1';
  this.doSomeThing = function (event: Event, param1: number, param2: string) {
    console.log(
      `${TAG},className=${this.className},event=${JSON.stringify(event)},param1=${param1},param=${param2}`,
    );
  };
};
var TestParamsClass2 = function (this: any) {
  this.className = 'TestParamsClass2';
  this.ready = function () {
    EventBus.dispatch('custom_event', this, 100, 'hello');
  };
};
var p1 = new (TestParamsClass1 as any)();
var p2 = new (TestParamsClass2 as any)();

function EventBusDemo() {
  const [msg, setMsg] = useState('');
  const [msgKeep, setMsgKeep] = useState('');
  const [msgParams, setMsgParams] = useState('');

  function handleAdd() {
    const has = EventBus.addEventListener('test_event', eventTest, 0);
    if (has) {
      setMsg('eventBus中已经存在test_evnt类型的eventTest事件');
    } else {
      EventBus.addEventListener('test_event', eventTest, 0);
      setMsg('成功添加test_event类型的eventTest事件');
    }
  }

  function handleHas() {
    let has = EventBus.hasEventListener('test_event', eventTest, 0);
    setMsg(
      has
        ? '已存在test_event类型的eventTest事件'
        : '不存在test_event类型的eventTest事件',
    );
  }

  function handleRemove() {
    EventBus.removeEventListener('test_event', eventTest, 0);
    setMsg('已删除test_event类型的eventTest事件');
  }

  function handleDispatch() {
    let has = EventBus.hasEventListener('test_event', eventTest, 0);
    if (has) {
      EventBus.hasEventListener('test_event');
      setMsg('成功执行test_event类型的eventTest事件');
    } else {
      setMsg('test_event类型的eventTest事件已被删除');
    }
  }

  function handleGet() {
    setMsg(`${JSON.stringify(EventBus.getEvents())}`);
  }

  function handleAddKeep() {
    let has = EventBus.hasEventListener('callback_event', t1.callback, t1);
    if (has) {
      setMsgKeep('eventBus中已存在callback_event类型的t1.callback事件');
    } else {
      EventBus.addEventListener('callback_event', t1.callback, t1);
       setMsgKeep('成功添加callback_event类型的t1.callback事件');
    }
  }

  function handleDispatchKeep() {
    t2.dispatchOurEvent();
    setMsgKeep('成功执行callback_event类型的t1.callback事件');
  }

  function handleAddForParams() {
    let has = EventBus.hasEventListener('custom_event', p1.doSomeThing, p1);
    if (has) {
      setMsgParams('eventBus中已存在custom_event类型的p1.doSomeThing事件');
    } else {
      EventBus.addEventListener('custom_event', p1.doSomeThing, p1);
      setMsgParams('成功添加custom_event类型的p1.doSomeThing事件');
    }
  }
  function handleDispatchForParams() {
    p2.ready();
    setMsgParams(
      '成功执行custom_event类型的p1.doSomeThing事件，param1=100，param2=hello',
    );
  }

  return (
    <>
      <ScrollView style={styles.main}>
        <View style={styles.mainItem}>
          <Text style={styles.title}>基础使用</Text>
          <View style={styles.container}>
            <Button title="添加" onPress={handleAdd}></Button>
          </View>
          <View style={styles.container}>
            <Button title="执行" onPress={handleDispatch}></Button>
          </View>
          <View style={styles.container}>
            <Button title="删除" onPress={handleRemove}></Button>
          </View>
          <View style={styles.container}>
            <Button title="是否存在" onPress={handleHas}></Button>
          </View>
          <View style={styles.container}>
            <Button title="获取" onPress={handleGet}></Button>
          </View>
          <View style={styles.box}>
            <Text style={{color: 'blue'}}>{msg}</Text>
          </View>
        </View>
        <View style={styles.mainItem}>
          <Text style={styles.title}>Keeping the scope</Text>
          <View style={styles.container}>
            <Button title="添加" onPress={handleAddKeep}></Button>
          </View>
          <View style={styles.container}>
            <Button title="执行" onPress={handleDispatchKeep}></Button>
          </View>
          <View style={styles.box}>
            <Text style={{color: 'blue'}}>{msgKeep}</Text>
          </View>
        </View>
        <View style={styles.mainItem}>
          <Text style={styles.title}>Passing additional parameters</Text>
          <View style={styles.container}>
            <Button title="添加" onPress={handleAddForParams}></Button>
          </View>
          <View style={styles.container}>
            <Button title="执行" onPress={handleDispatchForParams}></Button>
          </View>
          <View style={styles.box}>
            <Text style={{color: 'blue'}}>{msgParams}</Text>
          </View>
        </View>
      </ScrollView>
    </>
  );
}
export default EventBusDemo;
```

## 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：204.1.0.59;

## 方法

详情见 [EventBus](https://github.com/krasimir/EventBus/blob/master/README.md)

| Name                | Description        | Required | HarmonyOS Support |
|---------------------|--------------------|----------|-------------------|
| addEventListener    | -                  |-         | YES               |
| removeEventListener | -                  |-         | YES               |
| hasEventListener    | -                  |-         | YES               |
| dispatch            | -                  |-         | YES               |
| getEvents           | -                  |-         | YES               |


## 遗留问题

## 其他
