# 模型

## 设备

```ts
type Device = {
   data: device, // 设备信息
   id: string, // 设备id
   usage: number, // usage
   usagePage: number, // usagePage
   vendorId: number, // vendorId
   productId: number, // productId
   productName: string, // productName
}
```

## 布局模型

```ts
[
  IDefKeyInfo[],
  IDefKeyInfo[],
  IDefKeyInfo[],
  IDefKeyInfo[],
  IDefKeyInfo[],
  IDefKeyInfo[],

]
```

## 单键的布局模型

```ts
type IDefKeyInfo = {
  keyValue: number; // 键值
  location: {
    row: number; // 行
    col: number; // 列
  };
}
```

## 灯光

```ts

// 灯光模型
type LightMode = {
  open: boolean; // 是否开启灯光
  direction: boolean; // 方向 true 正向 false 反向
  superResponse: boolean; // 超强响应
  speed: number; // 灯光速度
  colors: string[]; // 颜色组
  mode: number; // 0 关闭, 1-20表示效果，21 自定义
  luminance: number; // 亮度
  sleepDelay: number; // 灯光休眠时间
  staticColor: number; // 静态灯光颜色模式
  type: LightModeType;
  // LightModeType = 'static' | 'custom' | 'dynamic';   
  // type的类型：custom 自定义模式，static 静态模式，dynamic 动态模式
};

// 灯光Type
type LightModeType = 'custom' | 'static' | 'dynamic';

```

## 布局

## 高级键

## 宏

```js
// DB命令查询是获取到 全局触发的信息
// DB0 单键触发 RT按下 RT抬起 死区的按下/抬起  单键释放 单键轴体
```
