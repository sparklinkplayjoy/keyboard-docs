
# 基础的设备信息

:::tip 注意

建议使用最新的1.0.2-beta.4版本，因为1.0.2-beta.3设置DB的接口一直是0

:::

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

## 获取设备信息APi

```js
const result = await ServiceKeyboard.getApi(type)
```

:::tip type 类型查询

[查看getApi的type类型](/keyboard/type#getApi)

:::

## 重连设备reconnection

```js
const result = await ServiceKeyboard.reconnection(device, this.device.id);
```
