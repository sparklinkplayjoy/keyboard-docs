## 轴体版本识别（无限轴体）

**简要描述:**
通过轴体列表判断设备轴体体系版本：当 `getAxisList().list.length === 0` 时，代表为“无限轴体（v2）”。

---

### 使用示例

```typescript
async function getAxisVersion(): Promise<number[]> {
  const result = await ServiceKeyboard.getAxisList();
  const { list } = result;
  const isAxisStatus = list.length === 0 ? 'v2' : 'v1';
  return isAxisStatus === 'v1' ? list : [];
}
```

---

### 注意事项

:::: tip

* `list.length === 0` 表示为“无限轴体（v2）”。
* 在 v2 模式下，请在 `getPerformance` 中读取并在 `setPerformance` 中设置以下三项：
  * `axisV2Id`
  * `axisRangeMax`
  * `axisCoefficient`
::::

---

# 键盘性能设置

## 获取按键性能配置

ServiceKeyboard.getPerformance()

**简要描述:**
获取指定按键的所有性能相关配置信息，包括模式、行程值、死区等参数。

---

### 参数

| 参数名称 | 类型     | 描述                                                                 | 是否必需 | 默认值 |
|----------|----------|----------------------------------------------------------------------|----------|--------|
| `params` | `object` | 一个包含按键位置信息的对象。                                             | 是       | 无     |
| `params.row` | `number` | 按键在键盘矩阵中的行号。                                               | 是       | 无     |
| `params.col` | `number` | 按键在键盘矩阵中的列号。                                               | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<IPerformanceInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含按键所有性能配置信息的对象。
* **解析对象结构 (`IPerformanceInfo`):**

| 字段名称            | 类型     | 描述                     | 示例值  |
|---------------------|----------|--------------------------|---------|
| `mode`              | `number` | 触发方式                 | `0`     |
| `normalPress`       | `number` | 普通触发按下行程         | `2`     |
| `normalRelease`     | `number` | 普通触发释放行程         | `2`     |
| `rtFirstTouch`      | `number` | RT触发首次触发行程       | `0.5`   |
| `rtPress`           | `number` | RT首次触发按下行程       | `0.3`   |
| `rtRelease`         | `number` | RT首次触发释放行程       | `0.3`   |
| `pressDeadStroke`   | `number` | 按下死区                 | `0.2`   |
| `releaseDeadStroke` | `number` | 抬起死区                 | `0.2`   |
| `axis`              | `number` | 获取的轴体列表索引（v1） | `0`     |
| `calibrate`         | `number` | 校准标志                 | `0`     |
| `axisV2Id`          | `number` | 轴体ID（v2，无限轴体时有效） | `0` |
| `axisRangeMax`      | `number` | 轴体最大行程范围（v2）   | `4`     |
| `axisCoefficient`   | `number` | 轴体系数（v2）           | `1`     |

**返回值示例:**

```js
// v1（有限轴体）：含 axis（索引），不含 v2 字段
{
    "mode": 0,
    "normalPress": 2,
    "normalRelease": 2,
    "rtFirstTouch": 0.5,
    "rtPress": 0.3,
    "rtRelease": 0.3,
    "pressDeadStroke": 0.2,
    "releaseDeadStroke": 0.2,
    "axis": 0,
    "calibrate": 0
}

// v2（无限轴体）：不含 axis（索引），增加 v2 三项
{
    "mode": 0,
    "normalPress": 2,
    "normalRelease": 2,
    "rtFirstTouch": 0.5,
    "rtPress": 0.3,
    "rtRelease": 0.3,
    "pressDeadStroke": 0.2,
    "releaseDeadStroke": 0.2,
    "axisV2Id": 1001,
    "axisRangeMax": 4,
    "axisCoefficient": 1,
    "calibrate": 0
}
```

---

### 使用示例

```typescript
async function getKeyPerformance(row: number, col: number) {
  try {
    const result = await ServiceKeyboard.getPerformance({ row, col });
    console.log('按键性能配置:', result);
  } catch (error) {
    console.error('获取按键性能配置失败:', error);
  }
}

// 示例：获取第5行第14列的按键性能配置
getKeyPerformance(5, 14);
```

---

### 注意事项

:::: tip

* v1：通过 `axis`（索引）指向 `getAxisList().list` 中的某个轴体。
* v2（无限轴体）：不再使用 `axis` 索引，改为使用 `axisV2Id`、`axisRangeMax`、`axisCoefficient` 三项描述轴体。
::::

---

## 设置按键性能配置

ServiceKeyboard.setPerformance()

**简要描述:**
设置指定按键的所有性能相关配置信息，包括触发方式、行程值、死区等参数。

---

### 参数

| 参数名称 | 类型     | 描述                                                                 | 是否必需 | 默认值 |
|----------|----------|----------------------------------------------------------------------|----------|--------|
| `params` | `object` | 一个包含按键性能配置信息的对象。                                         | 是       | 无     |
| `params.row` | `number` | 按键在键盘矩阵中的行号 | 是 | 无 |
| `params.col` | `number` | 按键在键盘矩阵中的列号 | 是 | 无 |
| `params.mode` | `number` | 触发方式 | 是 | 无 |
| `params.normalPress` | `number` | 普通触发按下行程 | 是 | 无 |
| `params.normalRelease` | `number` | 普通触发释放行程 | 是 | 无 |
| `params.rtFirstTouch` | `number` | RT触发首次触发行程 | 是 | 无 |
| `params.rtPress` | `number` | RT首次触发按下行程 | 是 | 无 |
| `params.rtRelease` | `number` | RT首次触发释放行程 | 是 | 无 |
| `params.pressDeadStroke` | `number` | 按下死区 | 是 | 无 |
| `params.releaseDeadStroke` | `number` | 抬起死区 | 是 | 无 |
| `params.axis` | `number` | 轴体索引（v1 时必填；v2 不使用） | 否 | 无 |
| `params.axisV2Id` | `number` | 轴体ID（v2 时必填；v1 不使用） | 否 | 无 |
| `params.axisRangeMax` | `number` | 轴体最大行程范围（v2 时必填） | 否 | 无 |
| `params.axisCoefficient` | `number` | 轴体系数（v2 时必填） | 否 | 无 |
| `params.axis` | `number` | 获取的轴体列表索引 | 是 | 无 |
| `params.calibrate` | `number` | 校准标志 | 是 | 无 |

**参数示例:**

```js
// v1（有限轴体）示例
{
  "row": 4,
  "col": 5,
  "mode": 0,
  "normalPress": 1.506,
  "normalRelease": 1.506,
  "rtFirstTouch": 0.5,
  "rtPress": 0.3,
  "rtRelease": 0.3,
  "pressDeadStroke": 0.2,
  "releaseDeadStroke": 0.2,
  "axis": 0,
  "calibrate": 0
}

// v2（无限轴体）示例
{
  "row": 4,
  "col": 5,
  "mode": 0,
  "normalPress": 1.506,
  "normalRelease": 1.506,
  "rtFirstTouch": 0.5,
  "rtPress": 0.3,
  "rtRelease": 0.3,
  "pressDeadStroke": 0.2,
  "releaseDeadStroke": 0.2,
  "axisV2Id": 1001,
  "axisRangeMax": 4,
  "axisCoefficient": 1,
  "calibrate": 0
}
```

---

### 返回值

* **总体类型:** `Promise<IPerformanceInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含设置后的按键性能配置信息的对象。
* **解析对象结构 (`IPerformanceInfo`):** 同“获取按键性能配置”的返回结构，v1/v2 字段含义一致。

**返回值示例:**

```js
{
  row: number;
  col: number;
  mode: number; // 触发方式
  normalPress: number; // 普通触发按下行程
  normalRelease: number; // 普通触发释放行程
  rtFirstTouch: number; // RT触发首次触发行程
  rtPress: number; // RT首次触发按下行程
  rtRelease: number; // RT首次触发释放行程
  pressDeadStroke: number; // 按下死区
  releaseDeadStroke: number; // 抬起死区
  axis?: number; // v1 有效
  axisV2Id?: number; // v2 有效
  axisRangeMax?: number; // v2 有效
  axisCoefficient?: number; // v2 有效
  calibrate: number; // 校准标志
}
```

---

### 使用示例

```typescript
async function setKeyPerformance() {
  try {
    // v1 或 v2 请根据 getAxisList().list.length 判断，并填入对应字段
    const params = {
      row: 4,
      col: 5,
      mode: 0,
      normalPress: 1.506,
      normalRelease: 1.506,
      rtFirstTouch: 0.5,
      rtPress: 0.3,
      rtRelease: 0.3,
      pressDeadStroke: 0.2,
      releaseDeadStroke: 0.2,
      // v1: axis: 0,
      // v2: axisV2Id: 1001, axisRangeMax: 4, axisCoefficient: 1,
      calibrate: 0,
    } as any;
    const result = await ServiceKeyboard.setPerformance(params);
    console.log('设置按键性能配置结果:', result);
  } catch (error) {
    console.error('设置按键性能配置失败:', error);
  }
}

setKeyPerformance();
```

---

### 注意事项

:::: tip

* 如果 `ServiceKeyboard.getAxisList().list.length === 0`，表示为 v2（无限轴体），`setPerformance` 需设置 `axisV2Id`、`axisRangeMax`、`axisCoefficient`。
* 如果为 v1，请设置 `axis`（索引）并忽略 v2 三项。
* 设置完成后，建议使用 `getPerformance` 校验配置是否生效。
::::

---

## 获取ADC采样数据

ServiceKeyboard.getADCSample()

**简要描述:**
获取指定行的ADC采样数据，用于分析按键的物理状态。

---

### 参数

| 参数名称 | 类型     | 描述                                                                 | 是否必需 | 默认值 |
|----------|----------|----------------------------------------------------------------------|----------|--------|
| `params` | `object` | 一个包含行号信息的对象。                                                 | 是       | 无     |
| `params.row` | `number` | 要获取ADC采样数据的行号。                                               | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<IADCSampleInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含ADC采样数据的对象。
* **解析对象结构 (`IADCSampleInfo`):**

| 字段名称 | 类型     | 描述                     | 示例值  |
|----------|----------|--------------------------|---------|
| `adc`    | `number` | ADC值                    | `0`     |
| `row`    | `number` | 行号                     | `3`     |
| `data`   | `number[]` | ADC采样数据数组，包含该行所有按键的采样值 | `[2715, 2700, ...]` |

**返回值示例:**

```js
{
    "adc": 0,
    "row": 3,
    "data": [
        2715,
        2700,
        2686,
        2693,
        2704,
        2772,
        2674,
        2688,
        2688,
        2684,
        2692,
        2680,
        0,
        2684,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
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
async function getADCSampleData(row: number) {
  try {
    const result = await ServiceKeyboard.getADCSample({
      row: row
    });
    console.log('ADC采样数据:', result);
    console.log('行号:', result.row);
    console.log('采样数据:', result.data);
  } catch (error) {
    console.error('获取ADC采样数据失败:', error);
  }
}

// 示例：获取第3行的ADC采样数据
getADCSampleData(3);
```

---

### 注意事项

::: tip

* `row` 的值需要根据键盘的实际矩阵布局来确定。
* `data` 数组中的值表示每个按键的ADC采样值，0表示该位置没有按键或无效数据。
* ADC采样值可用于分析按键的物理状态和触发情况。
:::

---

## 获取路由数据

ServiceKeyboard.getRoute()

**简要描述:**
获取指定行的按键按下的行程距离数据，用于分析按键的触发状态。

---

### 参数

| 参数名称 | 类型     | 描述                                                                 | 是否必需 | 默认值 |
|----------|----------|----------------------------------------------------------------------|----------|--------|
| `params` | `object` | 一个包含行号信息的对象。                                                 | 是       | 无     |
| `params.row` | `number` | 要获取路由数据的行号。                                                   | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<IRouteInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含按键按下的行程数据的对象。
* **解析对象结构 (`IRouteInfo`):**

| 字段名称 | 类型     | 描述                     | 示例值  |
|----------|----------|--------------------------|---------|
| `route`  | `number` | 路由值                   | `1`     |
| `row`    | `number` | 行号                     | `3`     |
| `data`   | `number[]` | 路由数据数组，包含该行所有按键的按下的行程距离 | `[0, 0, 0, ...]` |

**返回值示例:**

```js
{
    "route": 1,
    "row": 3,
    "data": [
        0,
        0,
        0,
        0,
        0,
        343,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
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
async function getRouteData(row: number) {
  try {
    const result = await ServiceKeyboard.getRoute({
      row: row
    });
    console.log('路由数据:', result);
    console.log('行号:', result.row);
    console.log('路由值:', result.route);
    console.log('数据:', result.data);
  } catch (error) {
    console.error('获取路由数据失败:', error);
  }
}

// 示例：获取第3行的路由数据
getRouteData(3);
```

---

### 注意事项

::: tip

* `row` 的值需要根据键盘的实际矩阵布局来确定。
* `data` 数组中的值表示每个按键的路由值，0表示该位置没有按键或无效数据。
* 路由值可用于分析按键的触发状态和信号传输情况。
:::

## 开始校准

ServiceKeyboard.calibrationStart

**简要描述:**
开始设备的校准流程。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<Calibration>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个 `Calibration` 对象，其中包含校准过程的状态或初始数据。

---

### 使用示例

```js
async function beginCalibration() {
  try {
    // 确保设备已初始化
    // await ServiceKeyboard.init(deviceId);
    const calibrationStatus = await ServiceKeyboard.calibrationStart();
    console.log('校准已开始:', calibrationStatus);
    // 根据 calibrationStatus 进行后续操作或UI更新
  } catch (error) {
    console.error('开始校准失败:', error);
  }
}

// beginCalibration();
```

## 结束校准

ServiceKeyboard.calibrationEnd

**简要描述:**
结束设备的校准流程。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<Calibration>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个 `Calibration` 对象，其中包含校准完成后的状态或最终数据。

---

### 使用示例

```js
async function finishCalibration() {
  try {
    // 确保设备已初始化且校准已开始
    // await ServiceKeyboard.init(deviceId);
    // await ServiceKeyboard.calibrationStart();
    const calibrationResult = await ServiceKeyboard.calibrationEnd();
    console.log('校准已结束:', calibrationResult);
    // 根据 calibrationResult 进行后续操作或UI更新
  } catch (error) {
    console.error('结束校准失败:', error);
  }
}

// finishCalibration();
```

## 获取校准状态

ServiceKeyboard.getCalibrationStatus()

**简要描述:**
获取指定行的按键校准状态信息。

---

### 参数

| 参数名称 | 类型     | 描述                                                                 | 是否必需 | 默认值 |
|----------|----------|----------------------------------------------------------------------|----------|--------|
| `params` | `object` | 一个包含行号信息的对象。                                                 | 是       | 无     |
| `params.row` | `number` | 要获取校准状态的行号。                                                   | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<ICalibrationStatusInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含校准状态信息的对象。
* **解析对象结构 (`ICalibrationStatusInfo`):**

| 字段名称    | 类型     | 描述                     | 示例值  |
|-------------|----------|--------------------------|---------|
| `calibrate` | `number` | 校准状态值               | `2`     |
| `row`       | `number` | 行号                     | `3`     |
| `data`      | `number[]` | 校准状态数组，包含该行所有按键的校准状态 | `[0, 0, 0, ...]` |

**返回值示例:**

```js
{
    "calibrate": 2,
    "row": 3,
    "data": [
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
        0,
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
async function getCalibrationStatusData(row: number) {
  try {
    const result = await ServiceKeyboard.getCalibrationStatus({
      row: row
    });
    console.log('校准状态:', result);
    console.log('行号:', result.row);
    console.log('校准状态值:', result.calibrate);
    console.log('状态数据:', result.data);
  } catch (error) {
    console.error('获取校准状态失败:', error);
  }
}

// 示例：获取第3行的校准状态
getCalibrationStatusData(3);
```

---

### 注意事项

::: tip

* `row` 的值需要根据键盘的实际矩阵布局来确定。
* `data` 数组中的值表示每个按键的校准状态，0表示该位置没有按键或未校准。
* 校准状态值可用于判断按键是否需要校准或校准是否完成。
:::

---

## 获取轴体列表

ServiceKeyboard.getAxisList()

**简要描述:**
获取键盘支持的所有轴体类型列表。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<IAxisListInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含轴体列表信息的对象。
* **解析对象结构 (`IAxisListInfo`):**

| 字段名称 | 类型     | 描述                     | 示例值  |
|----------|----------|--------------------------|---------|
| `total`  | `number` | 轴体类型总数             | `4`     |
| `list`   | `number[]` | 轴体类型ID数组，包含所有支持的轴体类型 | `[54, 24, 1, 69]` |

**返回值示例:**

```js
{
    "total": 4,
    "list": [
        54,
        24,
        1,
        69
    ]
}
```

---

### 使用示例

```typescript
async function getAxisListData() {
  try {
    const result = await ServiceKeyboard.getAxisList();
    console.log('轴体列表:', result);
    console.log('轴体总数:', result.total);
    console.log('轴体类型列表:', result.list);
  } catch (error) {
    console.error('获取轴体列表失败:', error);
  }
}

// 获取轴体列表
getAxisListData();
```

---

### 注意事项

::: tip

* 返回的轴体类型ID可用于设置按键的轴体类型。
* 不同的轴体类型ID代表不同的轴体型号或特性。
* 在使用 `setPerformance` 接口设置轴体时，应使用此列表中的有效ID。
:::

---

## 全局功能轴体库查询

**简要描述:**
键盘支持轴体库

### 注意事项

::: tip

* **轴体库的具体接口请联系我们获取。**
* 导入轴体库前，请确保数据格式正确。
:::
