# 高级键

## 获取dks

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

**DksType**: Layout_DKS1/Layout_DKS2/Layout_DKS3/Layout_DKS4

```js
const result = await ServiceKeyboard.getDks(key,DksType)
// result 返回值{ dks: value }

```

## 获取dks全部

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
const result = await ServiceKeyboard.getDksAll(key)
// result 返回值{ dks: value }

```

## 获取dks触发点的参数

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
const result = await ServiceKeyboard.getTrps(key)
// result 返回值{ trps: value }

```

## 获取dks触发点的全部参数

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
const result = await ServiceKeyboard.getTrpsAll(key)
// result 返回值{ trps: value }

```

## 获取延时

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
const result = await ServiceKeyboard.getMtorTgl(key)
// result 返回值{ trps: value }
```

## 设置DKS的数据

**参数：**

| 名称 |  类型 | 说明 | 数组最大长度 | 备注 |
| ---- | ---- | ---- | ---- | ---- |
| key | number | 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值 |  | 必填 |
| dks | number[] | 需要注意这里的dks 指的是getDksAll返回的数据 | 4 | 必填 |
| trps | number[] | 需要注意这里的trps 指的是getTrpsAll返回的数据 | 4 | 必填 |
| dbs | number[] | 需要注意这里的dbs 指的是getMtorTgl返回的数据 | 2 | 必填 |

```js
const result = await ServiceKeyboard.setDKS({
  key: number;
  dks: number[];
  trps: number[];
  dbs: number[];
})

```

## 设置MPT

**参数：**

| 名称 |  类型 | 说明 | 数组最大长度 | 备注 |
| ---- | ---- | ---- | ---- | ---- |
| key | number | 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值 |  | 必填 |
| dks | number[] | 需要注意这里的dks 指的是getDksAll返回的数据 | 3 | 必填 |
| dbs | number[] | 需要注意这里的dbs 指的是getMtorTgl返回的数据 | 3 | 必填 |

```js
const result = await ServiceKeyboard.setMPT({
  key: number;
  dks: number[];
  trps: number[];
  dbs: number[];
})

```

## 设置MT

**参数：**

| 名称 |  类型 | 说明 | 数组最大长度 | 备注 |
| ---- | ---- | ---- | ---- | ---- |
| key | number | 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值 |  | 必填 |
| dks | number[] | 需要注意这里的dks 指的是getDksAll返回的数据 | 2 | 必填 |
| delay | number[] |  |  | 必填 |

```js
const result = await ServiceKeyboard.setMT({
  key: number;
  dks: number[];
  delay:number;
})

```

## 设置TGL

**参数：**

| 名称 |  类型 | 说明 |  备注 |
| ---- | ---- | ---- | ---- |
| key | number | 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值 |  必填 |
| dks | number | 需要注意这里的dks 指的是getDksAll返回的数据 |  必填 |
| delay | number | getMtorTgl返回的数据 | 必填 |

```js
const result = await ServiceKeyboard.setTGL({
  key: number;
  dks: number;
  delay: number;
})

```

## 设置END

**参数：**

| 名称 |  类型 | 说明 |  备注 |
| ---- | ---- | ---- | ---- |
| key | number | 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值 |  必填 |
| dks | number | 需要注意这里的dks 指的是getDksAll返回的数据 |  必填 |

```js
const result = await ServiceKeyboard.setEND({key: number;dks: number;})

```

## 获取Socd

**参数：**

| 名称 |  类型 | 说明 |  备注 |
| ---- | ---- | ---- |  ---- |
| key | number | 原键值 |   必填 |

```js
const result = await ServiceKeyboard.getSocd({ key })
// {
//     pos1: number;
//     pos2: number;
//     key1: number;
//     key2: number;
//     type: number;
//     mode: number;
// }

```

## 设置Socd

**参数：**

| 名称 |  类型 | 说明 |  备注 |
| ---- | ---- | ---- |  ---- |
| pos1 | number | 原键值 |   必填 |
| pos2 | number | 原键值 |   必填 |
| key1 | number | 发送键值 |   必填 |
| key2 | number | 发送键值 |   必填 |
| type | number | 发送键值类型； |  0=按pos发送键值，1=按Key发送键值，默认:0 |
| mode | number | 表示键值的发送模式， | mode表示键值的发送模式，共有四种模式：0=后覆盖，1=a优先，2=b优先，3=中性,默认:0 |

```js
const result = await ServiceKeyboard.setSocd({
  pos1,
  pos2,
  key1,
  key2,
  type,
  mode,
})
```

## 设置RS

**参数：**

| 名称 |  类型 | 说明 |   备注 |
| ---- | ---- | ---- | ---- |
| key | number | 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值 |  必填 |
| dks | number | 是覆盖的键值 |   必填 |

```js
const result = await ServiceKeyboard.setRS({
  key: number;
  dks: number;
})
```
