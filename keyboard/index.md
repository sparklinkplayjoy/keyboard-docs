# 键盘SDK文档

## 授权

## 初始化

### 初始化SDK设备

## 灯光API

### 灯光模型

```ts

// custom 模型
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
  type?: LightModeType;
  // LightModeType = 'static' | 'custom' | 'dynamic';   
  // type的类型：custom 自定义模式，static 静态模式，dynamic 动态模式
};

// custom 模型
type CustomLightMode = {
    
}

```

### getLighting

#### 说明

获取灯光的配置信息

#### 参数

无

#### 返回值

默认返回一个 promise 对象，返回的结构如下：

 ```ts
const result = getLighting() // 返回整个灯光模型 LightMode 结构如下:
// result =  {
//   open: boolean; // 是否开启灯光
//   direction: boolean; // 方向 true 正向 false 反向
//   superResponse: boolean; // 超强响应
//   speed: number; // 灯光速度
//   colors: string[]; // 颜色组
//   mode: number; // 0 关闭, 1-20表示效果，21 自定义
//   luminance: number; // 亮度
//   sleepDelay: number; // 灯光休眠时间
//   staticColor: number; // 静态灯光颜色模式
//   type?: string;
// }
 ```

### setLighting

#### 说明

 设置灯光配置信息

#### 参数

```ts
setLighting(lightMode: LightMode) // LightMode 灯光模型

```

#### 返回值

### customSetLighting

#### 说明

 设置自定义灯光配置信息，

#### 参数

```ts
setLighting(lightMode: LightMode) // LightMode 灯光模型

```

#### 返回值
