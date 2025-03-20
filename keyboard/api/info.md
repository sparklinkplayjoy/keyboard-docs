
# 基础的设备信息

## 获取设备列表
ServiceKeyboard.getDevices()
- 返回值
```ts
() => Promise<Device[]>
```
[查看Device的类型](/keyboard/model#设备)
- 用法
```ts
const devices = await ServiceKeyboard.getDevices()
```

## 初始化设备
ServiceKeyboard.init()

- 参数
```ts
id: string
```
- 返回值
```ts
() => Promise<Device | null>
```
[查看Device的类型](/keyboard/model#设备)
- 用法
```ts
const device = ServiceKeyboard.init(id)
```

## 获取设备的基础信息

- 返回值
```ts
() => Promise<BaseInfo>
```
[查看BaseInfo的类型](/keyboard/model#基础信息)
- 用法
```ts
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


## 获取设备信息APi
- 参数
```ts
{
  type: number;
  hArgs?: number[];
  is8bit?: boolean;
}
```
- 返回值
```ts
() => Promise<Api>
```
[查看Api的类型](/keyboard/model#设备)
- 用法
```ts
const result = await ServiceKeyboard.getApi(type)
```

:::tip type 类型查询

[查看getApi的type类型](/keyboard/type#getApi)

:::

## 重连设备

ServiceKeyboard.reconnection()

- 参数  
```ts
device: Device
deviceId: string
```
- 返回值
```ts
() => Promise<void>
```
- 用法
```ts
const result = await ServiceKeyboard.reconnection(device, deviceId);
```
[查看回报率类型](/keyboard/type#getApi)
## 回报率设置

ServiceKeyboard.setRateOfReturn()

- 参数  
```ts
value: number
```

- 返回值
```ts
() => Promise<void>
```
- 用法
```ts
const result = await ServiceKeyboard.setRateOfReturn(value)
```
## 开始校准

ServiceKeyboard.calibrationStart()

- 返回值  
```ts
() => Promise<Calibration>
```
- 用法
```ts
const result = await ServiceKeyboard.calibrationStart()
```

[查看Calibration的类型](/keyboard/model#设备)

## 结束校准

ServiceKeyboard.calibrationEnd()

- 返回值  
```ts
() => Promise<Calibration>
```
- 用法
```ts
const result = await ServiceKeyboard.calibrationEnd()
```

[查看Calibration的类型](/keyboard/model#设备)

## 擦除固件

ServiceKeyboard.toBoot()

- 用法
```ts
await ServiceKeyboard.toBoot();
```
:::tip 注意

擦除后，需要重新连接设备

:::

## 更新固件

ServiceKeyboard.updateBin(buffer, callback)   
更新固件，需要先擦除固件
- 参数
```ts
buffer: ArrayBuffer
callback: (data: {current: number, total: number}) => void
```
- 返回值
```ts
Promise<{ success: boolean }>
```
- 用法
```ts
const { success } = await ServiceKeyboard.updateBin(buffer, ({current, total}) => {
  ...
})
```
:::tip 注意

更新后，需要重新连接设备

:::

