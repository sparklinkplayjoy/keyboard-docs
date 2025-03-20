# 性能设置

## 获取全局死区
ServiceKeyboard.getGlobalTouchTravel()
- 返回值  
```ts
() => Promise<{ globalTouchTravel: number, pressDead: number, releaseDead: number }>
```
- 用法  
```ts
const result = await ServiceKeyboard.getGlobalTouchTravel()
// result 返回值
// {
//     globalTouchTravel: number, // 全局触发行程
//     pressDead: number, // 全局按压死区
//     releaseDead: number // 全局抬起死区
// }
```

## 设置键盘全局行程和死区
ServiceKeyboard.setDB()
- 参数  
```ts
{
  globalTouchTravel: number //全局触发行程,值范围 0x01 ~ 0xFA0
  pressDead: number //全局按压死区
  releaseDead: number //全局抬起死区
}
```

- 返回值  
```ts
() => Promise<void>
```

- 用法
```ts
await ServiceKeyboard.setDB({ globalTouchTravel, pressDead, releaseDead })
```

## 获取性能模式 / 高级键模式
ServiceKeyboard.getPerformanceMode()
**参数：**

- 参数
```ts
key: number
```
:::tip 注意

**key**: 这里的 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::
- 返回值  
```ts
() => Promise<{ touchMode: string, advancedKeyMode: number }>
// {
//     "touchMode": "single", // 性能模式，single 单击，rt模式，global 全局
//     "advancedKeyMode": 0 // 高级键的模式
// }
```
- 用法
```ts
const result = await ServiceKeyboard.getPerformanceMode(key)

```

## 设置性能模式 / 高级键模式
ServiceKeyboard.setPerformanceMode()
- 参数
```ts
{
  key: number
  mode: string // 只能传入 single单击，rt模式，global全局 三种参数
  advancedKeyMode: number // 高级键的模式
}
```

:::tip 注意

**key**: 这里的 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{
  touchMode: string, // 性能模式，single 单击，rt模式，global 全局
  advancedKeyMode: number // 高级键的模式
}>
```

- 用法
```ts
const result = await ServiceKeyboard.setPerformanceMode({key, mode,advancedKeyMode})
```

## 获取首次触发行程 / 单键触发行程
ServiceKeyboard.getSingleTravel()
- 参数
```ts
key: number,
decimal: number // 小数位数，默认2
```
:::tip 注意

**key**: 这里的 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<number> //   number 当前的行程值
```

- 用法
```ts

const result = await ServiceKeyboard.getSingleTravel(key, decimal)

```

## 设置首次触发行程 / 单键触发行程
ServiceKeyboard.setSingleTravel()
- 参数
```ts
{
  key: number
  value: number
  decimal: number // 小数位数，默认2
}
```
:::tip 注意

 **key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

 **value**: 行程值

 **decimal**: 小数位数，默认2

:::
- 返回值  
```ts
() => Promise<number> //   number 当前的行程值
```

- 用法
```ts
const result = await ServiceKeyboard.setSingleTravel(key, value, decimal)

```

## 获取RT模式下的行程值
ServiceKeyboard.getRtTravel()
- 参数
```ts
key: number
```
:::tip 注意

 **key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::
- 返回值  
```ts
() => Promise<{pressTravel: number, releaseTravel: number}> 
```

- 用法
```ts
const result = await ServiceKeyboard.getRtTravel(key)
```

## 设置RT按下的行程
ServiceKeyboard.setRtPressTravel()
- 参数
```ts
key: number,
value: number // value: 按下的行程值
```
:::tip 注意

 **key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ pressTravel: number }>
```

- 用法
```ts
const result = await ServiceKeyboard.setRtPressTravel(key, value)
```




## 设置RT释放行程
ServiceKeyboard.setRtReleaseTravel()
- 参数
```ts
key: number
value: number // value: 按下的行程值
```
:::tip 注意

**key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ releaseTravel: number }>
```

- 用法
```ts
const result = await ServiceKeyboard.setRtReleaseTravel(key, value)
// result 返回值{ releaseTravel:0 }
```

## 死区的获取
ServiceKeyboard.getDpDr()
- 参数
```ts
key: number
```
:::tip 注意

**key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ pressDead: number, releaseDead: number }>
```

- 用法
```ts
const result = await ServiceKeyboard.getDpDr(key)
// result 返回值{ pressDead: dp, releaseDead: dr }
```

## 设置按下的死区
ServiceKeyboard.setDp()
- 参数
```ts
key: number,
value: number // value: 死区值
```
:::tip 注意

**key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<number>
```

- 用法
```ts
const result = await ServiceKeyboard.setDp(key, value)
// result 返回值{ pressDead: dp, releaseDead: dr }
```

## 设置释放死区
ServiceKeyboard.setDr()
- 参数
```ts
key: number
value: number // value: 死区值
```
:::tip 注意

**key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**value**: 死区值

:::

- 返回值  
```ts
() => Promise<number>
```

- 用法
```ts
const result = await ServiceKeyboard.setDr(key, value)
// result 返回值{ releaseDead: dr }
```

:::tip
注意这里有一个版本的判断
:::

## 轴体查询
ServiceKeyboard.getAxis()
- 参数
```ts
key: number
```
:::tip 注意

**key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

  :::

- 返回值  
```ts
() => Promise<{ axis: number }>
```

- 用法
```ts
const result = await ServiceKeyboard.getAxis(key)
// result 返回值{ axis:axis  }
```

:::tip
注意这里有一个版本的判断
:::

## 轴体设置
ServiceKeyboard.setAxis()
- 参数
```ts
key: number,
value: number // value: 轴体值
```
:::tip 注意

**key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**value**: 轴体值

:::

- 返回值  
```ts
() => Promise<{ axis: number }>
```

- 用法
```ts
const result = await ServiceKeyboard.setAxis(key, value)
// result 返回值{ axis: axis }
```

## 行程测试
ServiceKeyboard.getRm6X21Travel() 

- 返回值  
```ts
() => Promise<{ status: number, travels: number[] }>
```
- 用法
```ts
const result = await ServiceKeyboard.getRm6X21Travel(key,value)

// result 返回值{ status: [] ,travels:[]}
// status数组表示当前触发的状态，什么按键触发状态，一版02表示按下状态
// travels数组表示按键触发的行程值

```

## 键盘校准
ServiceKeyboard.getRm6X21Calibration()

- 返回值  
```ts
() => Promise<{ calibrations: number[], travels: number[] }>
```

- 用法
```ts
const result = await ServiceKeyboard.getRm6X21Calibration(key,value)
// result 返回值{ calibrations: [] ,travels:[]}
// calibrations数组表示校准的随机值
// travels数组表示按键触发的行程值
```
