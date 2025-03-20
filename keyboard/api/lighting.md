
# 键盘灯光

## 关闭灯光

ServiceKeyboard.closedLighting()

- 返回值
```ts
() => Promise<boolean>
```
- 用法
```ts
const result = await ServiceKeyboard.closedLighting()
```

## 获取灯光配置

ServiceKeyboard.getLighting()

- 返回值  
```ts
() => Promise<LightMode>
```
:::tip lightMode 模型

[查看lightMode的模型](/keyboard/model#灯光)

:::
- 用法
```ts
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

ServiceKeyboard.setLighting()

- 参数  
```ts
lightMode: LightMode
```
:::tip lightMode 模型

[查看lightMode的模型](/keyboard/model#灯光)

:::
- 用法
```ts
await ServiceKeyboard.setLighting(lightMode)
```
## 获取logo灯光配置

ServiceKeyboard.getLogoLighting()

- 返回值  
```ts
() => Promise<LightMode>
```
:::tip lightMode 模型

[查看lightMode的模型](/keyboard/model#灯光)

:::
- 用法
```ts
const result = await ServiceKeyboard.getLogoLighting()
// result 返回值
// {
//     open: boolean; // 是否开启灯光
//     direction: boolean; // 方向 true|正向 false|反向
//     superResponse: boolean; // 超强响应
//     speed: number; // 灯光速度
//     colors: string[]; // 颜色组
//     mode: number; // 动态灯效[1-4]
//     luminance: number; // 亮度
//     sleepDelay: number; // 灯光休眠时间
//     staticColor: number; // 静态灯光颜色模式
//     type: LightModeType;
// }

```

## 设置logo灯光配置

ServiceKeyboard.setLogoLighting()

- 参数  
```ts
lightMode: LightMode
```
:::tip lightMode 模型

[查看lightMode的模型](/keyboard/model#灯光)

:::
- 用法
```ts
await ServiceKeyboard.setLogoLighting(lightMode)
```

## 获取自定义灯光颜色

ServiceKeyboard.getCustomLighting()

- 参数  
```ts
key: number
```
:::tip 注意

**key**: 这里 key 指的是defKey返回IDefKeyInfo中keyValue的值

::: 
- 返回值  
```ts
() => Promise<{ key: number; R: number; G: number; B: number }>
``` 
- 用法
```ts
const result = await ServiceKeyboard.getCustomLighting(key)
```

## 设置自定义灯光

ServiceKeyboard.customSetLighting()

- 参数  
```ts
data: { key: number; R: number; G: number; B: number }
```
:::tip 注意
**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值
:::
- 返回值  
```ts
(data: { key: number; R: number; G: number; B: number }) => Promise<void>
```

- 用法
```ts
const result = await ServiceKeyboard.customSetLighting({ key, R, G, B })
```