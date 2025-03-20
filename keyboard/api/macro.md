# 宏  

## 获取宏
ServiceKeyboard.getMacro()
- 参数  
```ts
key: number
```
:::tip 注意

**key**: 这里 key 指的是**defKey**返回的**IDefKeyInfo**中的keyValue的值

:::

- 返回值
```ts
() => Promise<IMacroMode>
```
[查看IMacroMode的模型](/keyboard/model#宏)
- 用法
```ts
const result = await ServiceKeyboard.getMacro(key)
```

## 设置宏

ServiceKeyboard.setMacro()

- 参数
```ts
param: IMacroMode, 
macros: MacroType[], 
touchMode: 'quick' | 'single'
```
[查看MacroType的模型](/keyboard/model#宏)
- 返回值
```ts
() => Promise<void>
```
- 用法
```ts
const result = await ServiceKeyboard.setMacro(param, macros, touchMode)
```
