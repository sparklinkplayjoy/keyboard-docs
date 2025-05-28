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

