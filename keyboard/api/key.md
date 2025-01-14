# 布局/改建

## 初始化布局

获取当前键盘的布局会得到一个布局样式的二维数组的初始化布局模型
  
```js
const result = await ServiceKeyboard.defKey()
// result 返回值
// [
//   IDefKeyInfo[],
//   IDefKeyInfo[],
//   IDefKeyInfo[],
//   IDefKeyInfo[],
//   IDefKeyInfo[],
//   IDefKeyInfo[],
// ]
```

:::tip IDefKeyInfo 模型

[查看IDefKeyInfo的模型](/keyboard/model#单键的布局模型)

:::

## 获取布局

1. **key**: 这里的key 需要注意这里指defKey返回IDefKeyInfo中keyValue的值

2. **layout**: 指的是Fn的布局 目前支持的布局有只有四种分别为
   - Fn1的布局值为0
   - Fn2的布局值为1
   - Fn3的布局值为2
   - Fn4的布局值为3

```js
const result = await ServiceKeyboard.getLayoutKeyInfo({ key, layout })
```

## 改键

**参数：**

1. **key**: 这里的key 需要注意这里指defKey返回IDefKeyInfo中keyValue的值

2. **layout**: 指的是Fn的布局 目前支持的布局有只有四种分别为
   - Fn1的布局值为0
   - Fn2的布局值为1
   - Fn3的布局值为2
   - Fn4的布局值为3

3. **value**: 需要改的键值

```js
const result = await ServiceKeyboard.setKey({{ key, layout, value }})
// result 返回值
// {
//     key: number; // 键值
//     layout: number; // 布局
//     value: number; // 值
// }
```
