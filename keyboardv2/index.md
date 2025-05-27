# 键盘SDK文档

由于浏览器安全机制问题在调用sdk时候需要走的是hid协议，所以在最开始需要进行浏览器授权，授权成功后才能调用sdk。

## 开始

### 引入

```bash
pnpm add  @sparklinkplayjoy/sdk-keyboard-v2

```

## 搭建项目

### 项目引用

1. 引入

```js
import Keyboard from '@sparklinkplayjoy/sdk-keyboard'
const vendorId = 00 // you vid 
const productId = 00 // you pid 
const ServiceKeyboard = new Keyboard({
  configs: [{ vendorId, productId, usagePage: 0xffb0, usage: 0x01 }],
  usage: 0x01,
  usagePage: 0xffb0,
});
```

2. 获取授权

```js
// 得到当前的设置列表
const devices = await ServiceKeyboard.getDevices()
```

3. 初始化设备

```js
// 从当前设备列表中获取其中一个设备
const { id } = devices[0]
const result = await ServiceKeyboard.init(id)
```

4. 监听hid拔插事件

```js
import { UsbDetect } from '@sparklinkplayjoy/sdk-keyboard-v2';

 // 检测到设备拔插
UsbDetect.startMonitoring();

const listener = async ({ device, type }) => {
  if (type === 'disconnect') {
  } 
  if (type === 'connect') {
    if (device?.collections?.length) {
      try {
        // 通过usage和usagePage找到对应的连接设备
        const targetCollection = device.collections.find(
          (collection) => collection.usage === 1 && collection.usagePage === 65440,
        );
        if (targetCollection) {
          // 如果只需要执行一次重连
          await services.reconnection(device, this.device.id);

        }
      } catch (error) {
        console.error(error);
      }
    } 
  }
}

UsbDetect.on('change', listener);

UsbDetect.off('change',listener) // 移除监听
```
