# 性能设置

## 获取全局死区

```js
const result = await ServiceKeyboard.getGlobalTouchTravel()
// result 返回值
// {
//     globalTouchTravel: number, // 全局触发行程
//     pressDead: number, // 全局按压死区
//     releaseDead: number // 全局抬起死区
// }
```

## 设置键盘全局行程和死区

**参数：**

**globalTouchTravel**: 全局触发行程,值范围 0x01 ~ 0xFA0

**pressDead**: 全局按压死区

**releaseDead**: 全局抬起死区

```js
const result = await ServiceKeyboard.setDB({ globalTouchTravel, pressDead, releaseDead })
```

## 获取性能模式 / 高级键模式

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
// 
const result = await ServiceKeyboard.getPerformanceMode(key)
// result 返回值
// {
//     "touchMode": "single", // 性能模式，single 单击，rt模式，global 全局
//     "advancedKeyMode": 0 // 高级键的模式
// }
```

## 设置性能模式 / 高级键模式

**参数：**

| 名称 |  类型 | 说明 | 备注 |
| ---- | ---- | ---- | ---- |
| key | number | 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值 |  |
| mode | string | 只能传入 single单击，rt模式，global全局 三种参数 |  |
| advancedKeyMode | number | 高级键的模式 |  |  |


```js
const result = await ServiceKeyboard.setPerformanceMode({key, mode,advancedKeyMode})
// result 返回值
// {
//     "touchMode": "single", // 性能模式，single 单击，rt模式，global 全局
//     "advancedKeyMode": 0 // 高级键的模式
// }
```

## 获取首次触发行程 / 单键触发行程

**参数：**

 **key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

 **decimal**: 小数位数，默认2

```js
// 
const result = await ServiceKeyboard.getSingleTravel(key,decimal)
// result 返回值 number 当前的行程值
```

## 设置首次触发行程 / 单键触发行程

**参数：**

 **key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

 **value**: 行程值

 **decimal**: 小数位数，默认2

```js
// 
const result = await ServiceKeyboard.setSingleTravel(key,value,decimal)
// result 返回值 number 当前的行程值
```

## 获取RT模式下的行程值

**参数：**

 **Key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
// 
const result = await ServiceKeyboard.getRtTravel(key)
// result 返回值{pressTravel: number, releaseTravel: number}
```

## 设置RT按下的行程

**参数：**

**Key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

**value**: 按下的行程值

```js
// 
const result = await ServiceKeyboard.setRtPressTravel(key,value)
// result 返回值{ pressTravel: rtpTravel }
```

## 设置RT释放行程

**参数：**

**Key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

**value**: 按下的行程值

```js
// 
const result = await ServiceKeyboard.setRtReleaseTravel(key,value)
// result 返回值{ releaseTravel:0 }
```

## 死区的获取

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
// 
const result = await ServiceKeyboard.getDpDr(key)
// result 返回值{ pressDead: dp, releaseDead: dr }
```

## 设置按下的死区

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

**value**: 死去值

```js
// 
const result = await ServiceKeyboard.setDp(key,value)
// result 返回值{ pressDead: dp, releaseDead: dr }
```

## 设置释放死区

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

**value**: 死去值

```js
// 
const result = await ServiceKeyboard.setDr(key,value)
// result 返回值{ releaseDead: dr }
```

:::tip
注意这里有一个版本的判断
:::

## 轴体查询

**参数：**

1. **key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
// 
const result = await ServiceKeyboard.getAxis(key)
// result 返回值{ axis:  }
```

:::tip
注意这里有一个版本的判断
:::

## 轴体设置

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

**value**: 轴体值

```js
// 
const result = await ServiceKeyboard.setAxis(key,value)
// result 返回值{ axis: axis }
```
