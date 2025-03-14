# 宏  

## 获取宏

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
const result = await ServiceKeyboard.getMacro(key: number)
```

## 设置宏

**参数：**

**key**: 这里的key 需要注意这里指的**defKey**返回的**IDefKeyInfo**中的keyValue的值

```js
const result = await ServiceKeyboard.setMacro(param: IMacroMode, macros: MacroType[], touchMode: 'quick' | 'single')
```
