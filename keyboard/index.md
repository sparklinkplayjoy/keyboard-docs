# 键盘SDK文档

由于浏览器安全机制问题在调用sdk时候需要走的是hid协议，所以在最开始需要进行浏览器授权，授权成功后才能调用sdk。

## 开始

### 引入

```bash
npm install @sparklinkplayjoy/sdk-keyboard 
# 或
yarn add @sparklinkplayjoy/sdk-keyboard
# 或
pnpm add @sparklinkplayjoy/sdk-keyboard
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
const devices = await ServiceKeyboard.getDevices()
```

3. 初始化设备

```js
// 从当前设备列表中获取其中一个设备
const { id } = devices[0]
const result = await ServiceKeyboard.init(id)
```
