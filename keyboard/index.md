# 键盘SDK文档

由于浏览器安全机制问题在调用sdk时候需要走的是hid协议，所以在最开始需要进行浏览器授权，授权成功后才能调用sdk。

## 开始

### 引入

```bash

pnpm add  @sparklinkplayjoy/sdk-keyboard

```

## 搭建项目

### 项目引用

1. 引入

```js

import Keyboard from '@sparklinkplayjoy/sdk-keyboard'
const ServiceKeyboard = new Keyboard();

```

2. 获取授权

```js
// 得到当前的设置列表
const devices = await ServiceKeyboard.getDevices({
  configs: [{ vendorId: 7331, productId: 2049, usagePage: 65440, usage: 1 }],
  usage: 1,
  usagePage: 65440,
})

// 新增hid过滤设备configs
// usage 和 usagePage 表示
```

3. 初始化设备

```js
// 从当前设备列表中获取其中一个设备
const { id } = devices[0]
const result = await ServiceKeyboard.init(id)
```

4. 监听hid拔插事件

```js
import { UsbDetect } from '@sparklinkplayjoy/sdk-keyboard';

const listener = async ({ device, type }) => {
// 例子
  if (type === 'connect') {
    if (device.collections.usage === usage && device.collections.usagePage === usagePage) { // 对应设备的 usage、 usagePage,
      setTimeout(async () => {
        await ServiceKeyboard.reconnection(device, this.device.id);
      }, 100);
    }
  }
};

UsbDetect.on('change', listener);


UsbDetect.off('change',listener) // 移除监听
```
