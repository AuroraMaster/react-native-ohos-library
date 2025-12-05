> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-aria</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gluestack/react-native-aria/tree/main">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/gluestack/react-native-aria/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/gluestack/react-native-aria/tree/main)

## 安装与使用
> [!TIP] 该库已经不再维护，如果执行总包命令，项目运行缺失模块，就需要卸载旧包，在命令后增加--legacy-peer-deps，然后再次下载包文件

请到三方库的 Releases 发布地址查看配套的版本信息：

| 三方库版本 | 发布信息                                                     | 支持RN版本 |
| ---------- | ------------------------------------------------------------ | ---------- |
| 0.2.4     | [react-native-aria release](https://github.com/gluestack/react-native-aria/releases) | 0.72/0.77       |

对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **yarn**

```bash
yarn add react-native-aria@0.2.4
```

<!-- tabs:end -->

#### **npm**

```bash
npm install react-native-aria@0.2.4
```

<!-- tabs:end -->

除了总包之外，我们还提供了一些单独包，如：@react-native-aria/button

#### **yarn**

```bash
yarn add @react-native-aria/button@0.2.7
```

<!-- tabs:end -->

#### **npm**

```bash
npm install @react-native-aria/button@0.2.7
```

<!-- tabs:end -->

下面的代码展示了useToggleButton的基本使用场景：

```js
import React from "react";
import { useToggleButton } from "@react-native-aria/button";
import { useToggleState } from "@react-stately/toggle";
import { Pressable, Text, View } from "react-native";
import { useRef } from "react";

export function ToggleButton(props: any) {
    const ref = useRef(null);
    let state = useToggleState(props);
    let { buttonProps, isPressed } = useToggleButton(props, state);

    return (
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            <Text>ToggleButton：</Text>
            <Pressable ref={ref} {...buttonProps}
                style={{
                    backgroundColor: state.isSelected ? "rgb(9, 90, 186)" : "#e1e1e1", borderRadius: 15,
                    padding: 5, width: 100, height: 30, justifyContent: 'center', alignItems: 'center'
                }}
            >
                <Text style={{ color: state.isSelected ? "#f1f1f1" : "#000" }} >点击切换</Text>
            </Pressable>
        </View>
    );
}

export default ToggleButton

```

下面的代码展示了useCheckbox与useCheckboxGroup的基本使用场景：

```javascript
import React, { useContext, useRef } from 'react';
import { Pressable, View, Text } from 'react-native';
import { useCheckbox, useCheckboxGroupItem, useCheckboxGroup } from '@react-native-aria/checkbox';
import { useToggleState } from '@react-stately/toggle';
import { useCheckboxGroupState } from "@react-stately/checkbox";
import { useFocusRing } from '@react-native-aria/focus';

let CheckboxGroupContext = React.createContext<any>(null);

const CheckboxItems = [{ key: 'soccer', value: '足球' }, { key: 'baseball', value: '棒球' }, { key: 'basketball', value: '篮球' }]
const findName = (value: string) => {
    const item = CheckboxItems.find(i => { return i.key === value; })
    return item && item.value
}

export function CheckboxGroup(props: any) {
    let { children, label } = props;
    let state = useCheckboxGroupState(props);
    let { groupProps, labelProps } = useCheckboxGroup(props, state);

    return (
        <View {...groupProps} style={{ flexDirection: 'row', alignItems: 'center' }}>
            {label && <Text {...labelProps}>{label}</Text>}
            <CheckboxGroupContext.Provider value={state}>
                {children}
            </CheckboxGroupContext.Provider>
            <View><Text>已经选择：</Text>{props.value.map(i=>{
                return <Text>{findName(i)}</Text>
            })}</View> 
        </View>
    );
}


export function Checkbox(props: any) {
    let groupState = useContext(CheckboxGroupContext);
    let inputRef = useRef<HTMLInputElement>(null);

    let { isFocusVisible, focusProps } = useFocusRing();

    let { inputProps } = groupState ? useCheckboxGroupItem(
        {
            ...props,
            isRequired: props.isRequired,
            validationState: props.validationState,
        },
        groupState,
        inputRef
    ) : useCheckbox(props, useToggleState(props), inputRef);

    return (
        <View style={isFocusVisible ? { borderWidth: 2 } : {}}>
            <Pressable {...inputProps} {...focusProps} >
                <View style={{ flexDirection: 'row', alignItems: 'center', marginRight: 5 }}>
                    {props.children}
                </View>
            </Pressable>
        </View>
    );
}

export const CheckboxExample = () => {
    const [state, setCheckbox] = React.useState([]);

    return (
        <CheckboxGroup
            label="CheckboxGroup："
            value={state}
            onChange={(val: any) => {
                setCheckbox(val);
            }}
        >
            {CheckboxItems.map(i => {
                return <Checkbox key={i.key} value={i.key}>
                    <Text>{i.value}</Text>
                </Checkbox>;
            })}
        </CheckboxGroup>
    );
};
export default CheckboxExample

```

下面的代码展示了useRadio与useRadioGroup的基本使用场景：

```javascript
import React from "react";
import { useRadioGroupState } from "@react-stately/radio";
import { useRadio, useRadioGroup } from "@react-native-aria/radio";
import { Pressable, Text, View } from "react-native";
import { useFocusRing } from "@react-native-aria/focus";

let RadioContext = React.createContext<any>({});

const radioItems = [{ key: 'dogs', value: '狗子' }, { key: 'cats', value: '猫儿' }]
const findName = (value: string) => {
    const item = radioItems.find(i => { return i.key === value; })
    return item && item.value
}

export function RadioGroup(props: any) {
    let { children, label } = props;
    let state = useRadioGroupState(props);
    let { radioGroupProps, labelProps } = useRadioGroup(props, state);

    return (
        <View {...radioGroupProps} style={{ flexDirection: 'row', alignItems: 'center' }}>
            <Text {...labelProps}>{label}</Text>
            <RadioContext.Provider
                value={{
                    isDisabled: props.isDisabled,
                    isReadOnly: props.isReadOnly,
                    state,
                }}
            >
                {children}
            </RadioContext.Provider>
            <Text>已经选择：{findName(state.selectedValue as string)}</Text>
        </View>
    );
}

export function Radio(props: any) {
    let { state, isReadOnly, isDisabled } = React.useContext(RadioContext);
    const inputRef = React.useRef(null);
    let { inputProps } = useRadio(
        { isReadOnly, isDisabled, ...props },
        state,
        inputRef
    );
    let { isFocusVisible, focusProps } = useFocusRing();

    return (
        <Pressable {...inputProps}{...focusProps} style={{ marginRight: 5 }}>
            <View style={[{ flexDirection: 'row', alignItems: 'center' }, isFocusVisible ? { borderWidth: 1 } : {},]}>
                <Text>{props.children}</Text>
            </View>
        </Pressable>
    );
}

export const RadioExample = () => {
    return (
        <View>
            <RadioGroup label="RadioGroup：">
                {radioItems.map(i => {
                    return <Radio key={i.key} value={i.key}>{i.value}</Radio>
                })}
            </RadioGroup>
        </View>
    );
};
export default RadioExample

```

下面的代码展示了useSwitch的基本使用场景：

```javascript
import { useToggleState } from "@react-stately/toggle";
import React, { useRef } from "react";
import { StyleSheet, Text, View, Animated, Pressable } from "react-native";
import { useSwitch } from "@react-native-aria/switch";
import { useFocusRing } from "@react-native-aria/focus";
import { VisuallyHidden } from "@react-aria/visually-hidden";

const calculateDimensions = (size: any) => {
    switch (size) {
        case "small":
            return {
                width: 40,
                padding: 10,
                circleWidth: 15,
                circleHeight: 15,
                translateX: 22,
            };
        case "large":
            return {
                width: 70,
                padding: 20,
                circleWidth: 30,
                circleHeight: 30,
                translateX: 38,
            };
        default:
            return {
                width: 46,
                padding: 12,
                circleWidth: 18,
                circleHeight: 18,
                translateX: 26,
            };
    }
};

const defaultProps = {
    isOn: false,
    onColor: "#4cd137",
    offColor: "#ecf0f1",
    size: "medium",
    labelStyle: {},
    thumbOnStyle: {},
    thumbOffStyle: {},
    trackOnStyle: {},
    trackOffStyle: {},
    icon: null,
    disabled: false,
    animationSpeed: 300,
    useNativeDriver: true,
    circleColor: "white",
};

export function Switch(origProps: any) {
    const props = {
        ...defaultProps,
        ...origProps,
    };

    const offsetX = useRef(new Animated.Value(0));
    const dimensions = useRef(calculateDimensions(props.size));

    const createToggleSwitchStyle = () => [
        {
            justifyContent: "center",
            width: dimensions.current.width,
            borderRadius: 20,
            padding: dimensions.current.padding,
            backgroundColor: props.isOn ? props.onColor : props.offColor,
        },
        props.isOn ? props.trackOnStyle : props.trackOffStyle,
    ];

    const createInsideCircleStyle = () => [
        {
            alignItems: "center",
            justifyContent: "center",
            margin: 4,
            left: 0,
            position: "absolute",
            backgroundColor: props.circleColor,
            transform: [{ translateX: offsetX.current }],
            width: dimensions.current.circleWidth,
            height: dimensions.current.circleHeight,
            borderRadius: dimensions.current.circleWidth / 2,
            shadowColor: "#000",
            shadowOffset: {
                width: 0,
                height: 2,
            },
            shadowOpacity: 0.2,
            shadowRadius: 2.5,
            elevation: 1.5,
        },
        props.isOn ? props.thumbOnStyle : props.thumbOffStyle,
    ];

    const { isOn, icon, label, labelStyle = {} } = props;

    const toValue = isOn
        ? dimensions.current.width - dimensions.current.translateX
        : 0;

    Animated.timing(offsetX.current, {
        toValue,
        duration: props.animationSpeed,
        useNativeDriver: props.useNativeDriver,
    }).start();

    return (
        <View style={{ flexDirection: 'row', alignItems: 'center' }}>
            {label && <Text style={labelStyle}>{label}</Text>}
            <View style={[...createToggleSwitchStyle(), { marginBottom: 5 }]}>
                <Animated.View style={createInsideCircleStyle()}>{icon}</Animated.View>
            </View>
            <Text style={{ marginLeft: 5 }}>{isOn ? "开" : "关"}</Text>
        </View>
    );
}

export function ControlledSwitch() {
    const state = useToggleState();
    const { isFocusVisible, focusProps } = useFocusRing();
    const inputRef = useRef(null);
    let { inputProps } = useSwitch(
        { "aria-label": "Example switch" },
        state,
        inputRef
    );

    return (
        <Pressable {...inputProps} {...focusProps} ref={inputRef}>
            <View style={isFocusVisible ? { borderWidth: 2 } : {}}>
                <Switch
                    isOn={state.isSelected}
                    onColor="green"
                    offColor="red"
                    label='Switch：'
                    size="large"
                    onToggle={state.toggle}
                />
            </View>
        </Pressable>
    );

}
export default ControlledSwitch

```

下面的代码展示了useOverlayPosition的基本使用场景：

```javascript
import React from "react";
import { useOverlayPosition, OverlayProvider, OverlayContainer } from "@react-native-aria/overlays";
import { useButton } from "@react-native-aria/button";
import { View, Text, Pressable, ScrollView, Modal } from "react-native";
import { useToggleState } from "@react-stately/toggle";

const positions = [
    "top",
    "left",
    "right",
    "bottom",
    "top left",
    "top right",
    "left top",
    "left bottom",
    "bottom right, bottom left",
    "right top",
    "right bottom",
];

export function TriggerWrapper() {
    const [placement, setPlacement] = React.useState<any>(-1);
    React.useEffect(() => {
        const id = setInterval(() => {
            setPlacement((prev) => (prev + 1) % positions.length);
        }, 2000);
        return () => clearInterval(id);
    }, []);

    return <Trigger placement={positions[placement]}></Trigger>;
}

const OverlayView = ({ targetRef, placement = 'top' }) => {
    let overlayRef = React.useRef();

    const { overlayProps } = useOverlayPosition({
        placement: placement as any,
        targetRef,
        overlayRef,
        offset: 10,
    });

    return (
        <ScrollView
            bounces={false}
            style={{
                position: "absolute",
                height: 400,
                backgroundColor: "lightgray",
                ...overlayProps.style,
            }}
            ref={(node) => overlayRef.current = node}
        >
            <View
                style={{
                    padding: 20,
                    height: 5000,
                }}
            >
                <Text>Hello world</Text>
            </View>
        </ScrollView>
    );
};

export function Trigger({ placement }: any) {
    let ref = React.useRef();
    const toggleState = useToggleState();

    let { buttonProps } = useButton({ onPress: toggleState.toggle }, ref);

    return (
        <View style={{ flexDirection: 'row', alignItems: "center" }} >
            <Text>useOverlayPosition：</Text>
            <Pressable
                {...buttonProps}
                ref={ref}
                role="button"
                aria-label="Click here to perform some actions"
            >
                <View
                    style={{
                        flexDirection: "row",
                        borderWidth: 1,
                        paddingHorizontal: 10,
                        paddingVertical: 10,
                    }}
                >
                    <Text>点我一下</Text>
                </View>
            </Pressable>
            <Modal visible={toggleState.isSelected} onRequestClose={toggleState.toggle}>
                <OverlayProvider>
                    <OverlayContainer>
                        <OverlayView targetRef={ref} placement={placement} />
                    </OverlayContainer>
                </OverlayProvider>
            </Modal>
        </View>
    );
}
export default TriggerWrapper

```

更多hooks请参考[react-native-aria官方文档](https://geekyants.github.io/react-native-aria/docs/)

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

在以下版本验证通过：

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;
2. RNOH: 0.77.18; SDK: HarmonyOS 6.0.0 Release SDK; IDE: DevEco Studio  6.0.0.868; ROM: 6.0.0.112;

## Hooks

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                                                                                                                                                                                   | Type     | Required | Platform    | HarmonyOS Support |
|--------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|-------------|-------------------|
| useToggleButton    | 为切换按钮组件提供行为和可访问性实现。切换按钮允许用户打开或关闭选择，例如在两种状态或模式之间切换。                                           | Function | No       | iOS,Android | Yes               |
| useCheckbox        | 为复选框组件提供行为和可访问性实现。复选框允许用户从单个项目列表中选择多个项目，或将单个项目标记为已选择。                                     | Function | No       | iOS,Android | Yes               |
| useCheckboxGroup   | 为复选框组组件提供行为和可访问性实现。复选框组允许用户从选项列表中选择多个项目。                                                               | Function | No       | iOS,Android | Yes               |
| useRadioGroup      | 为单选按钮组组件提供行为和可访问性实现。单选按钮组允许用户从互斥选项列表中选择单个项目。                                                       | Function | No       | iOS,Android | Yes               |
| useSwitch          | 为开关组件提供行为和可访问性实现。开关类似于复选框，但表示开/关值而不是选择。                                                                 | Function | No       | iOS,Android | Yes               |
| OverlayContainer   | 为 React Native 应用提供类似 React Portal 的功能，可用于显示绝对定位的组件，如菜单、工具提示、弹出框。                                         | Function | No       | iOS,Android | Yes               |
| useOverlayPosition | 处理相对于触发元素定位叠加层（如弹出框和菜单），并在窗口调整大小时更新位置。                                                                   | Function | No       | iOS,Android | Yes               |

## 遗留问题
1. 切换勾选状态后立刻触发朗读暂时不支持。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/gluestack/react-native-aria/blob/main/LICENSE)，请自由地享受和参与开源。
