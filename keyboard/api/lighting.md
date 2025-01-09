
# 键盘灯光

## 关闭灯光

```js
const result = await ServiceKeyboard.closedLighting()
// 关闭成功会返回true
```

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

## 获取自定义灯光颜色

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
const result = await ServiceKeyboard.getCustomLighting(key)
```

## 设置自定义灯光

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

**R**: R值

**G**: G值

**B**: B值

```js
const result = await ServiceKeyboard.customSetLighting({ key, R, G, B })
```
