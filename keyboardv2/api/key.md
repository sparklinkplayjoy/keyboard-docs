# 布局/改建

## 初始化布局

ServiceKeyboard.defKey()

**简要描述:**
获取当前键盘的初始化布局模型，返回一个代表键盘完整布局的二维数组。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<IDefKeyInfo[][]>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个二维数组 (`IDefKeyInfo[][]`)。数组中的每个 `IDefKeyInfo` 对象代表一个按键的布局信息。
* **解析对象结构 (`IDefKeyInfo`):**

| 字段名称 | 类型 | 描述 | 示例值 |
|---------|------|------|--------|
| `keyValue` | `number` | 按键的值 | `41` |
| `location` | `object` | 按键在键盘上的位置信息 | - |
| `location.row` | `number` | 按键所在的行号（从0开始） | `0` |
| `location.col` | `number` | 按键所在的列号（从0开始） | `0` |

**返回值示例:**

```js
[
    [   // 第0行
        {
            "keyValue": 41,
            "location": {
                "row": 1,
                "col": 0
            }
        },
        // ... 更多按键
    ],
    [   // 第1行
        {
            "keyValue": 43,
            "location": {
                "row": 2,
                "col": 0
            }
        },
        // ... 更多按键
    ],
    // ... 更多行
]
```

---

### 使用示例

```typescript
async function fetchInitialLayout() {
  try {
    const layoutGrid = await ServiceKeyboard.defKey();
    console.log('初始化键盘布局:', layoutGrid);
    if (layoutGrid.length > 0 && layoutGrid[0].length > 0) {
    }
  } catch (error) {
    console.error('获取初始化布局失败:', error);
  }
}

fetchInitialLayout();
```
