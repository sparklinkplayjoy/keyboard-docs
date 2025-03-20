# 高级键

## 获取dks
ServiceKeyboard.getDks()
- 参数
```ts
key: number
DksType: DksType
```
:::tip 注意

**key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**DksType**: Layout_DKS1/Layout_DKS2/Layout_DKS3/Layout_DKS4

:::

- 返回值  
```ts
() => Promise<{ dks: number }>
```

- 用法
```ts
const result = await ServiceKeyboard.getDks(key, DksType)

```

## 获取dks全部
ServiceKeyboard.getDksAll()

- 参数
```ts
key: number
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{
  dks1: number,
  dks2: number,
  dks3: number,
  dks4: number
}>
```

- 用法
```ts
const result = await ServiceKeyboard.getDksAll(key)

```

## 获取dks触发点的参数

ServiceKeyboard.getTrps()

- 参数
```ts
key: number
type: TrpsLayoutType
```
[查看TrpsLayoutType的模型](/keyboard/model#高级键)

:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ trps: number }>
```

- 用法
```ts
const result = await ServiceKeyboard.getTrps(key)
// result 返回值{ trps: value }

```

## 获取dks触发点的全部参数

ServiceKeyboard.getTrpsAll()

- 参数
```ts
key: number
```
:::tip 注意

  **key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ 
  trps1: number,
  trps2: number,
  trps3: number,
  trps4: number
}>
```

- 用法
```ts
const result = await ServiceKeyboard.getTrpsAll(key)

```

## 获取延时
ServiceKeyboard.getMtorTgl()
- 参数
```ts
key: number
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<number>
```

- 用法    
```ts
const result = await ServiceKeyboard.getMtorTgl(key)
```

## 设置DKS的数据
ServiceKeyboard.setDKS()    
- 参数
```ts
{
  key: number;
  dks: number[]; // 数组最大长度4
  trps: number[]; // 数组最大长度4
  dbs: number[]; // 数组最大长度2
}
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**dks**: 这里的dks 指的是getDksAll返回的数据

**trps**: 这里的trps 指的是getTrpsAll返回的数据

**dbs**: 这里的dbs 指的是getMtorTgl返回的数据

:::
- 返回值  
```ts
() => Promise<{ dks: number }>
```

- 用法
```ts
const result = await ServiceKeyboard.setDKS({
  key,
  dks,
  trps,
  dbs,
})

```

## 获取MPT
ServiceKeyboard.getMpt()
- 参数
```ts
key: number
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ 
  dks: [number, number, number], // [dks1, dks2, dks3]
  dbs: [number, number, number], // [dbs1, dbs2, dbs3]
}>
```

- 用法
```ts
const result = await ServiceKeyboard.getMpt(key)

```

## 设置MPT
ServiceKeyboard.setMpt()
- 参数
```ts
{
  key: number,
  dks?: number[], // 数组最大长度3
  dbs?: number[], // 数组最大长度3
}
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**dks**: 这里的dks 指的是getDksAll返回的数据

**dbs**: 这里的dbs 指的是getMtorTgl返回的数据

:::

- 返回值  
```ts
() => Promise<{ 
  dks: [number, number, number], // [dks1, dks2, dks3]
  dbs: [number, number, number], // [dbs1, dbs2, dbs3]
}>
```

- 用法
```ts
const result = await ServiceKeyboard.setMpt({
  key,
  dks,
  dbs,
})

```

## 获取MT
ServiceKeyboard.getMT()
- 参数
```ts
key: number
```
:::tip 注意 

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ 
 [key: number]: {
  type: string, // 'mt'
  mt: {
    delay: number, // 单位 10ms
    dks：[number, number]， // [dks1, dks2]
  } 
  keyValue: number,
 }
}>
```

- 用法
```ts
const result = await ServiceKeyboard.getMT(key)

```

## 设置MT
ServiceKeyboard.setMT()
- 参数
```ts
{
  key: number
  dks: number[] // 数组最大长度2
  delay: number // 单位 10ms
}
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**dks**: 这里的dks 指的是getDksAll返回的数

:::

- 用法
```ts
await ServiceKeyboard.setMT({
  key,
  dks,
  delay, // 单位 10ms
})

```

## 获取TGL
ServiceKeyboard.getTGL()
**参数：**

-  参数
```ts
key: number
```
:::tip 注意

**key**: 这里的 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ 
  key: number,
  delay: number, // 单位 10ms
}>
```

- 用法
```ts
const result = await ServiceKeyboard.getTGL(key)

```

## 设置TGL
ServiceKeyboard.setTGL()
- 参数
```ts
{
  key: number
  dks?: number // 数组最大长度2
  delay?: number // 单位 10ms
}
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**dks**: 这里的dks 指的是getDksAll返回的数据

:::

- 返回值  
```ts
() => Promise<{ 
  key: number,
  delay: number, // 单位 10ms
}>
```

- 用法
```ts
const result = await ServiceKeyboard.setTGL({
  key,
  dks
})

```

## 获取END
ServiceKeyboard.getEND()
- 参数
```ts
key: number
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值  
```ts
() => Promise<{ 
  dks: number,
  delay: number,
}>
```

- 用法
```ts
const result = await ServiceKeyboard.getEND(key)

```

## 设置END
ServiceKeyboard.setEND()
- 参数
```ts
{
  key: number
  dks: number // 数组最大长度2
},
version: string // 固件版本
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**dks**: 这里的dks 指的是getDksAll返回的数据

**version**: 固件版本
:::

- 返回值  
```ts
() => Promise<{
  dks: number,
  delay: number,
}>
```

- 用法
```ts
const result = await ServiceKeyboard.setEND({ key, dks }, version)

```

## 获取Socd
ServiceKeyboard.getSocd()
- 参数
```ts
key: number,
version: string
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

**version**: 固件版本
:::

- 返回值  
```ts
version: 1.0.7
() => Promise<{
  pos1: number,
  pos2: number,
  key1: number,
  key2: number,
  type: number,
  mode: number,
  delay: number,
}>
verison: other
() => Promise<{
  pos: number,
  key: number,
  type: number,
  mode: number,
}>
```

- 用法
```ts
const result = await ServiceKeyboard.getSocd(key, version)
```

## 设置Socd
ServiceKeyboard.setSocd()
- 参数
```ts
params: ISOCDMode | ISOCDModeV2 | ISOCDModeV3,
version: string
```
[查看ISOCDMode、ISOCDModeV2、ISOCDModeV3的模型](/keyboard/model#高级键)

:::tip 注意

**version**: 固件版本

:::

```ts
const result = await ServiceKeyboard.setSocd(
{
  pos1,
  pos2,
  key1,
  key2,
  type,
  mode,
}, 
version
)
```

## 删除高级键
ServiceKeyboard.deleteKey()
- 参数
```ts
key: number
```
:::tip 注意

**key**: 这里的key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

::: 

- 返回值
```ts
() => Promise<void>
```

- 用法
```ts
await ServiceKeyboard.deleteKey(key)
```
