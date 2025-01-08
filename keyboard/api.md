# API

## 获取设备列表

```js
const devices = await ServiceKeyboard.getDevices()
```

## 初始化设备

```js
const result = await ServiceKeyboard.init(id)
```

## 获取设备的基础信息

```js
const result = await ServiceKeyboard.getBaseInfo()
// result 返回值
// {
//  BoardID: 0,
//  KeyboardLayout: 0, 键盘布局
//  KeyType: 0, // 轴体
//  CustomerID: 0,
//  ProductionId: 0,
//  KeyboardRunMode: 0, // 键盘运行模式
//  KeyboardSN: '', // 获取键盘SN
//  firewareSpaceSize: 0,
//  appVersion: '', // 获取固件版本
//  appBuildDate: '', //  获取固件编译日期
//  versionString: '', // 版本信息
// }
```

## 获取设备信息

```js
const result = await ServiceKeyboard.getDeviceInfo(type)
```

:::tip type 类型查询

[查看getDeviceInfo的type类型](/keyboard/type#getDeviceInfo)

:::

## 设置设备信息

```js
const result = await ServiceKeyboard.setDeviceInfo(type, value)
```

:::tip type 类型查询

[查看setDeviceInfo的type类型](/keyboard/type#setDeviceInfo)

:::

## 获取设备基础信息

```js
const result = await ServiceKeyboard.getBaseInfo()
```

:::tip type 类型查询

[查看getBaseInfo的type类型](/keyboard/type#getBaseInfo)

:::

const result = await ServiceKeyboard.getBaseInfo()

## 获取设备信息APi

```js
const result = await ServiceKeyboard.getApi(type)
```

:::tip type 类型查询

[查看getApi的type类型](/keyboard/type#getApi)

:::

## 获取灯光配置

```js
const result = await ServiceKeyboard.getLighting()
// result 返回值
// {
//     open: boolean; // 是否开启灯光
//     direction: boolean; // 方向 true 正向 false 反向
//     superResponse: boolean; // 超强响应
//     speed: number; // 灯光速度
//     colors: string[]; // 颜色组
//     mode: number; // 0 关闭, 1-20表示效果，21 自定义
//     luminance: number; // 亮度
//     sleepDelay: number; // 灯光休眠时间
//     staticColor: number; // 静态灯光颜色模式
//     type: LightModeType;
// }

```

## 设置灯光配置

```js
const result = await ServiceKeyboard.setLighting(lightMode)
```

:::tip lightMode 模型

[查看lightMode的模型](/keyboard/model#灯光)

:::

## 自定义灯光配置

```js
const result = await ServiceKeyboard.customSetLighting(lightMode)
```

 ```js
const result = await ServiceKeyboard.getLighting() // 返回整个灯光模型 LightMode 结构如下:

 ```

## 布局

获取当前键盘的布局会得到一个布局样式的二维数组的初始化布局模型
  
```js
const result = await ServiceKeyboard.defKey()
// result 返回值
// [
//   IDefKeyInfo[],
//   IDefKeyInfo[],
//   IDefKeyInfo[],
//   IDefKeyInfo[],
//   IDefKeyInfo[],
//   IDefKeyInfo[],
// ]
```

:::tip IDefKeyInfo 模型

[查看IDefKeyInfo的模型](/keyboard/model#单键的布局模型)

:::

## 改键

### 参数

1. **key**: 这里的key 需要注意这里指的defKey返回的IDefKeyInfo中的keyValue的值

2. **layout**: 指的是Fn的布局 目前支持的布局有只有四种分别为
   - Fn1的布局值为0
   - Fn2的布局值为1
   - Fn3的布局值为2
   - Fn4的布局值为3

3. **value**: 需要改的键值

```js
const result = await ServiceKeyboard.updateKey({{ key, layout, value }})
// result 返回值
// {
//     key: number; // 键值
//     layout: number; // 布局
//     value: number; // 值
// }
```

## 获取全局死区

```js
const result = await ServiceKeyboard.getGlobalTouchTravel()
// result 返回值
// {
//     globalTouchTravel: number, // 全局触发行程
//     pressDead: number, // 全局按压死区
//     releaseDead: number // 全局抬起死区
// }
```

## 获取性能模式 / 高级键模式

### 参数

1. **key**: 这里的key 需要注意这里指的defKey返回的IDefKeyInfo中的keyValue的值

```js
// 
const result = await ServiceKeyboard.getPerformanceMode(key)
// result 返回值
// {
//     "touchMode": "single", // 性能模式，single 单击，rt模式，global 全局
//     "advancedKeyMode": 0 // 高级键的模式
// }
```

## 获取首次触发行程 / 单键触发行程

### 参数

1. **key**: 这里的key 需要注意这里指的defKey返回的IDefKeyInfo中的keyValue的值
2. **decimal**: 小数位数，默认2

```js
// 
const result = await ServiceKeyboard.getSingleTravel(key,decimal)
// result 返回值 number 当前的行程值
```

## RT模式下的行程值

### 参数

1. **Key**: 这里的key 需要注意这里指的defKey返回的IDefKeyInfo中的keyValue的值

```js
// 
const result = await ServiceKeyboard.getRtTravel(key)
// result 返回值{pressTravel: number, releaseTravel: number}
```

## 死区的获取

### 参数

1. **Key**: 这里的key 需要注意这里指的defKey返回的IDefKeyInfo中的keyValue的值

```js
// 
const result = await ServiceKeyboard.getDpDr(key)
// result 返回值{ pressDead: dp, releaseDead: dr }
```

:::tip
注意这里有一个版本的判断
:::

## 轴体查询

### 参数

1. **Key**: 这里的key 需要注意这里指的defKey返回的IDefKeyInfo中的keyValue的值

```js
// 
const result = await ServiceKeyboard.getAxis(key)
// result 返回值{ axis:  }
```

:::tip
注意这里有一个版本的判断
:::

## 高级键

## 宏
