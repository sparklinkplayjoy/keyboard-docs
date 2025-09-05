# 布局/改建

## 获取指定层的按键布局

ServiceKeyboard.getKeyLayout()

**简要描述:**
获取指定层和行的键盘布局数据。

---

### 参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `params` | `object` |  | 描述键盘层数和行数的对象 |
| `params.layer` | `number` | 是 | 键盘层数，从0开始 |
| `params.row` | `number` | 是 | 行号，从0开始 |

---

### 返回值

* **总体类型:** `Promise<IGetKeyLayoutInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含指定层和行的键盘布局信息的对象。
* **解析对象结构 (`IGetKeyLayoutInfo`):**

| 字段名称 | 类型 | 描述 | 示例值 |
|---------|------|------|--------|
| `layer` | `number` | 键盘层数 | `0` |
| `row` | `number` | 行号 | `2` |
| `keyboardLayout` | `number[]` | 该行的按键值数组 | `[43, 20, 26, ...]` |

**返回值示例:**

```js
{
    "layer": 0,
    "row": 2,
    "keyboardLayout": [
        43,
        20,
        26,
        8,
        21,
        23,
        28,
        24,
        12,
        18,
        19,
        47,
        48,
        49,
        0,
        0,
        0,
        0,
        0,
        0,
        0
    ]
}
```

---

### 使用示例

```typescript
async function getKeyboardLayout() {
  try {
    const layout = await ServiceKeyboard.getKeyLayout({
      layer: 0,
      row: 2
    });
    console.log('键盘布局:', layout);
  } catch (error) {
    console.error('获取键盘布局失败:', error);
  }
}

getKeyboardLayout();
```

## 获取按键编码

ServiceKeyboard.getKeyCode()

**简要描述:**
获取指定位置按键的编码值。

---

### 参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `params` | `object` | 是 | 描述按键位置的对象 |
| `params.layer` | `number` | 是 | 键盘层数，从0开始 |
| `params.row` | `number` | 是 | 行号，从0开始 |
| `params.col` | `number` | 是 | 列号，从0开始 |

---

### 返回值

* **总体类型:** `Promise<IGetKeyCodeInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含按键编码信息的对象。
* **解析对象结构 (`IGetKeyCodeInfo`):**

| 字段名称 | 类型 | 描述 | 示例值 |
|---------|------|------|--------|
| `layer` | `number` | 键盘层数 | `0` |
| `row` | `number` | 行号 | `3` |
| `col` | `number` | 列号 | `7` |
| `keycode` | `number` | 按键编码值 | `13` |

**返回值示例:**

```js
{
    "layer": 0,
    "row": 3,
    "col": 7,
    "keycode": 13
}
```

---

### 使用示例

```typescript
async function getKeyCode() {
  try {
    const result = await ServiceKeyboard.getKeyCode({
      layer: 0,
      row: 3,
      col: 7
    });
    console.log('获取按键编码结果:', result);
  } catch (error) {
    console.error('获取按键编码失败:', error);
  }
}

getKeyCode();
```
## 设置按键编码

ServiceKeyboard.setKeyCode()

**简要描述:**
设置指定位置按键的编码值。

---

### 参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `params` | `object` | 是 | 描述按键位置和编码的对象 |
| `params.layer` | `number` | 是 | 键盘层数，从0开始 |
| `params.row` | `number` | 是 | 行号，从0开始 |
| `params.col` | `number` | 是 | 列号，从0开始 |
| `params.keycode` | `number` | 是 | 要设置的按键编码值 |

---

### 返回值

* **总体类型:** `Promise<ISetKeyCodeInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含设置结果的对象。
* **解析对象结构 (`ISetKeyCodeInfo`):**

| 字段名称 | 类型 | 描述 | 示例值 |
|---------|------|------|--------|
| `layer` | `number` | 键盘层数 | `0` |
| `row` | `number` | 行号 | `3` |
| `col` | `number` | 列号 | `3` |
| `keycode` | `number` | 设置后的按键编码值 | `0` |

**返回值示例:**

```js
{
    "layer": 0,
    "row": 3,
    "col": 3,
    "keycode": 0
}
```

---

### 使用示例

```typescript
async function setKeyCode() {
  try {
    const result = await ServiceKeyboard.setKeyCode({
      layer: 0,
      row: 3,
      col: 3,
      keycode: 21
    });
    console.log('设置按键编码结果:', result);
  } catch (error) {
    console.error('设置按键编码失败:', error);
  }
}

setKeyCode();
```

## 获取默认按键布局

ServiceKeyboard.getDefaultKeyLayout()

**简要描述:**
获取指定行、功能层和系统的默认键盘布局数据。

**版本要求:** 从 1.0.6.0 版本开始支持

---

### 参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `params` | `object` | 是 | 描述键盘行数、功能层和系统的对象 |
| `params.row` | `number` | 是 | 行号，从0开始 |
| `params.fn` | `number` | 是 | 功能层，取值范围 0-3 |
| `params.system` | `number` | 是 | 系统类型，0 表示 Windows，1 表示 macOS |

---

### 返回值

* **总体类型:** `Promise<IGetDefaultKeyLayoutInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含指定行、功能层和系统的默认键盘布局信息的对象。
* **解析对象结构 (`IGetDefaultKeyLayoutInfo`):**

| 字段名称 | 类型 | 描述 | 示例值 |
|---------|------|------|--------|
| `row` | `number` | 行号 | `2` |
| `fn` | `number` | 功能层 | `1` |
| `system` | `number` | 系统类型 | `0` |
| `keyCodes` | `number[]` | 该行的默认按键编码值数组 | `[43, 20, 26, ...]` |

**返回值示例:**

```js
{
    "system": 0,
    "fn": 0,
    "row": 2,
    "keyCodes": [
        43,
        20,
        26,
        8,
        21,
        23,
        28,
        24,
        12,
        18,
        19,
        47,
        48,
        49,
        0,
        0,
        0,
        0,
        0,
        0,
        0
    ]
}
```

---

### 使用示例

```typescript
async function getDefaultKeyboardLayout() {
  try {
    const layout = await ServiceKeyboard.getDefaultKeyLayout({
      row: 2,
      fn: 1,
      system: 0  // 0 表示 Windows 系统
    });
    console.log('默认键盘布局:', layout);
  } catch (error) {
    console.error('获取默认键盘布局失败:', error);
  }
}

getDefaultKeyboardLayout();
```

---

### 批量获取示例

```typescript
async function getAllDefaultLayouts() {
  const systems = [0, 1];      // 0: Windows, 1: macOS
  const fnLayers = [0, 1, 2, 3];  // 功能层 0-3
  const rowCount = 5;          // 假设有5行
  
  const allLayouts = [];
  
  for (const system of systems) {
    for (const fn of fnLayers) {
      for (let i = 0; i < rowCount; i++) {
        try {
          // eslint-disable-next-line no-await-in-loop
          const res = await ServiceKeyboard.getDefaultKeyLayout({
            row: i,
            fn,
            system
          });
          
          allLayouts.push({
            system: system === 0 ? 'Windows' : 'macOS',
            fnLayer: `fn${fn}`,
            row: i,
            keyCodes: res.keyCodes
          });
          
          console.log(`已获取 ${system === 0 ? 'Windows' : 'macOS'} fn${fn} 第 ${i} 行布局`);
        } catch (error) {
          console.error(`获取失败: system=${system}, fn=${fn}, row=${i}`, error);
        }
      }
    }
  }
  
  return allLayouts;
}

getAllDefaultLayouts();
```

## 获取按键状态

ServiceKeyboard.getKeyStatus()

**简要描述:**
获取指定行的按键状态信息，包括按键行程和状态数据。

**版本要求:** 从 1.1.0.0 版本开始支持

---

### 参数

| 参数名 | 类型 | 必填 | 描述 |
|--------|------|------|------|
| `params` | `object` | 是 | 描述键盘行数的对象 |
| `params.row` | `number` | 是 | 行号，从0开始 |

---

### 返回值

* **总体类型:** `Promise<IGetKeyStatusInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含指定行按键状态信息的对象。
* **解析对象结构 (`IGetKeyStatusInfo`):**

| 字段名称 | 类型 | 描述 | 示例值 |
|---------|------|------|--------|
| `data` | `number[]` | 该行所有按键的状态数据数组 | `[0, 1, 0, 1, ...]` |

**返回值示例:**

```js
{
    "data": [0, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 0, 1, 0]
}
```

---

### 使用示例

```typescript
async function getKeyStatusForRow() {
  try {
    const status = await ServiceKeyboard.getKeyStatus({
      row: 2
    });
    console.log('按键状态:', status.data);
    
    // 处理状态数据
    status.data.forEach((status, index) => {
      console.log(`第 ${index} 个按键状态: ${status === 1 ? '按下' : '未按下'}`);
    });
  } catch (error) {
    console.error('获取按键状态失败:', error);
  }
}

getKeyStatusForRow();
```

### 批量获取示例

```typescript
async function getAllKeyStatus() {
  const keyboardStore = useKeyboardStore();
  const { keyboard } = storeToRefs(keyboardStore);
  
  const travels = [];
  const keyStatus = [];
  
  const rowCount = keyboard.value.length;
  
  // 并行获取所有行的路由和状态数据
  const tasks = Array.from({ length: rowCount }, (_, i) => {
    return Promise.all([
      ServiceKeyboard.getRoute({ row: i }), 
      ServiceKeyboard.getKeyStatus({ row: i })
    ]);
  });
  
  const results = await Promise.all(tasks);
  
  // 处理返回数据
  for (let i = 0; i < rowCount; i++) {
    const [routeRes, statusRes] = results[i];
    travels.push(routeRes.data);
    keyStatus.push(statusRes.data);
  }
  
  // 更新键盘数据
  for (let row = 0; row < rowCount; row++) {
    for (let col = 0; col < keyboard.value[row].length; col++) {
      const key = keyboard.value[row][col].performance;
      key.travels = travels[row][col];
      key.keyStatus = keyStatus[row][col];
    }
  }
  
  console.log('所有按键状态已更新');
  return { travels, keyStatus };
}

getAllKeyStatus();
```

