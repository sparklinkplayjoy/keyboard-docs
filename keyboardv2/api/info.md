# 基础的设备信息

## 获取设备列表

ServiceKeyboard.getDevices()

**简要描述:**
获取连接到系统的设备列表。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<Device[]>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个 `Device` 对象数组。每个 `Device` 对象代表一个已连接的键盘设备。
* **解析对象结构 (`Device`):**

| 字段名称 | 类型 | 描述 | 示例值 |
|---------|------|------|--------|
| `data` | `object` | 设备数据对象 | - |
| `data.id` | `string` | 设备ID | `"b1545667-777b-4a8a-9640-1c000a56b5e7"` |
| `id` | `string` | 设备唯一标识符 | `"b1545667-777b-4a8a-9640-1c000a56b5e7"` |
| `usage` | `number` | 设备用途值 | `1` |
| `usagePage` | `number` | 设备用途页值 | `65440` |
| `vendorId` | `number` | 厂商ID | `7331` |
| `productId` | `number` | 产品ID | `2049` |
| `productName` | `string` | 产品名称 | `"ET65 HE"` |

---

### 使用示例

```js
async function fetchDevices() {
  try {
    const devices = await ServiceKeyboard.getDevices();
    console.log('发现的设备:', devices);
    if (devices.length > 0) {
      // 对设备列表进行操作，例如选择第一个设备进行初始化
      // const firstDevice = devices[0];
      // await ServiceKeyboard.init(firstDevice.id);
    } else {
      console.log('未检测到设备。');
    }
  } catch (error) {
    console.error('获取设备列表失败:', error);
  }
}

fetchDevices();
```

## 初始化指定的键盘设备

ServiceKeyboard.init()

**简要描述:**
初始化指定的键盘设备，以便后续进行交互。

---

### 参数

| 参数名称 | 类型     | 描述                     | 是否必需 | 默认值 |
|----------|----------|--------------------------|----------|--------|
| `id`     | `string` | 要初始化的设备的唯一标识符。可从`ServiceKeyboard.getDevices()`获取 | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<Device | null>`
* **描述:** 返回一个 `Promise`。
  * **Promise 解析 (Resolves):** `Device` - 设备初始化成功时，解析为该设备的 `Device` 对象。
  * **Promise 解析 (Resolves):** `null` - 设备初始化失败或未找到指定设备时，解析为 `null`。
* **解析对象结构 (`Device`):**
  * 关于 `Device` 对象的详细结构，请 [查看Device的类型](/keyboard/model#设备)。

---

### 使用示例

```js
async function initializeDevice(deviceId: string) {
  try {
    const device = await ServiceKeyboard.init(deviceId);
    if (device) {
      console.log('设备初始化成功:', device);
      // 现在可以使用 device 对象与设备进行交互
      // const deviceInfo = await ServiceKeyboard.getDevicesInfo(); 
    } else {
      console.log('设备初始化失败或未找到设备。');
    }
  } catch (error) {
    console.error('初始化设备时发生错误:', error);
  }
}

// deviceId 是从 getDevices() 获取到的
// const exampleDeviceId = "some_device_id_string";
// initializeDevice(exampleDeviceId);
```

## 获取设备的基础硬件和固件信息

ServiceKeyboard.getDevicesInfo()

**简要描述:**
获取当前已初始化设备的基础硬件和固件信息。

---

### 参数

此方法不需要参数 (通常在成功调用 `ServiceKeyboard.init()` 后使用)。

---

### 返回值

* **总体类型:** `Promise<BaseInfo>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含设备基础信息的 `BaseInfo` 对象。
* **解析对象结构 (`BaseInfo`):**

| 字段名称          | 类型     | 描述                     | 示例值  |
|-------------------|----------|--------------------------|---------------|
| `type`            | `number` | 设备类型。               | `1`           |
| `subType`         | `number` | 设备子类型。             | `0`           |
| `boardId`         | `number` | 板卡ID。                 | `3145729`     |
| `appVersion`      | `string` | 固件的应用版本号。       | `'1.0.1.0'`   |
| `pcbVersion`      | `string` | PCB版本号。              | `'1-0-0-0'`   |
| `runModeVersion`  | `number` | 运行模式版本。           | `0`           |
| `sn`              | `string` | 键盘的序列号。           | `'54817806657765148212547'` |
| `timestamp`       | `string` | 时间戳。                 | `'2025052215:4'` |

---

### 使用示例

```js
async function fetchBaseDeviceInfo() {
  try {
    // 确保设备已初始化
    // await ServiceKeyboard.init(deviceId);
    const baseInfo = await ServiceKeyboard.getDevicesInfo();
    console.log('设备基础信息:', baseInfo);
    // console.log('固件版本:', baseInfo.appVersion);
  } catch (error) {
    console.error('获取设备基础信息失败:', error);
  }
}

// fetchBaseDeviceInfo(); // 需在设备初始化后调用
```

## 获取协议版本

ServiceKeyboard.getProtocolVersion()

**简要描述:**
获取键盘设备的协议版本信息。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<ProtocolVersion>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含协议版本信息的对象。
* **解析对象结构 (`ProtocolVersion`):**

| 字段名称          | 类型     | 描述                     | 示例值  |
|-------------------|----------|--------------------------|---------|
| `mainVersion`     | `number` | 主版本号。               | `1`     |
| `subVersion`      | `number` | 子版本号。               | `0`     |
| `hardwareVersion` | `number` | 硬件版本号。             | `1`     |
| `softwareVersion` | `number` | 软件版本号。             | `0`     |

---

### 使用示例

```js
async function fetchProtocolVersion() {
  try {
    const versionInfo = await ServiceKeyboard.getProtocolVersion();
    console.log('协议版本信息:', versionInfo);
  } catch (error) {
    console.error('获取协议版本信息失败:', error);
  }
}

// fetchProtocolVersion();
```

## 获取配置列表

ServiceKeyboard.getConfigList()

**简要描述:**
获取键盘可用的配置列表信息。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<ConfigList>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含配置列表信息的对象。
* **解析对象结构 (`ConfigList`):**

| 字段名称 | 类型     | 描述                     | 示例值  |
|----------|----------|--------------------------|---------|
| `total`  | `number` | 配置总数。               | `4`     |
| `list`   | `string[]` | 配置名称列表。         | `['Config1', 'Config2', 'Config3', 'Config4']` |

---

### 使用示例

```js
async function fetchConfigList() {
  try {
    const configList = await ServiceKeyboard.getConfigList();
    console.log('配置列表:', configList);
    console.log('配置总数:', configList.total);
    console.log('配置名称列表:', configList.list);
  } catch (error) {
    console.error('获取配置列表失败:', error);
  }
}

// fetchConfigList();
```

## 获取当前配置

ServiceKeyboard.getConfig()

**简要描述:**
获取键盘当前使用的配置信息。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<Config>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个包含当前配置信息的对象。
* **解析对象结构 (`Config`):**

| 字段名称 | 类型     | 描述                     | 示例值  |
|----------|----------|--------------------------|---------|
| `key`    | `string` | 当前配置的名称。         | `'Config2'` |
| `value`  | `number` | 当前配置的索引值。       | `1`     |

---

### 使用示例

```js
async function fetchCurrentConfig() {
  try {
    const config = await ServiceKeyboard.getConfig();
    console.log('当前配置名称:', config.key);
    console.log('当前配置索引:', config.value);
  } catch (error) {
    console.error('获取当前配置失败:', error);
  }
}

// fetchCurrentConfig();
```

## 设置当前配置

ServiceKeyboard.setConfig()

**简要描述:**
设置键盘当前使用的配置。

---

### 参数

| 参数名称 | 类型     | 描述                     | 是否必需 | 默认值 |
|----------|----------|--------------------------|----------|--------|
| `config` | `string` | 要设置的配置名称。       | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<void>`
* **描述:** 返回一个 `Promise`。操作成功完成时，`Promise` 解析，无特定返回值。如果设置失败，`Promise` 会拒绝并返回一个错误。

---

### 使用示例

```js
async function setCurrentConfig(configName) {
  try {
    await ServiceKeyboard.setConfig(configName);
    console.log(`已切换到配置: ${configName}`);
  } catch (error) {
    console.error('设置配置失败:', error);
  }
}

// 示例：切换到 Config1
// setCurrentConfig('Config1');
```

### 注意事项

::: tip

* `index`: 配置索引值必须在1到4之间。
* 切换配置后，建议监听 `getCmd` 事件来获取配置切换的结果。
* 在收到配置切换成功的通知后，通常需要重新获取以下数据：
  * 键盘配置信息
  * 灯光设置
  * 按键映射
  * 其他相关设置
* 建议在配置切换过程中显示加载状态，以提供更好的用户体验。
:::

## 获取配置名称

ServiceKeyboard.getConfigName(index)

**简要描述:**
根据配置索引获取配置名称。

---

### 参数

| 参数名称 | 类型     | 描述               | 是否必需 | 默认值 |
|----------|----------|--------------------|----------|--------|
| `index`  | `number` | 配置索引（1-4）。  | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<string>`
* **描述:** 返回该索引对应的配置名称。

---

### 使用示例

```js
async function fetchConfigName(index) {
  // 需协议版本 >= v1.0.3.0（可通过 ServiceKeyboard.getProtocolVersion 校验）
  const name = await ServiceKeyboard.getConfigName(index);
  console.log('配置名称:', name);
  return name;
}
```

---

### 注意事项

:::: tip

* 需要设备协议版本至少为 `v1.0.3.0`。
* 协议版本可通过 `ServiceKeyboard.getProtocolVersion()` 获取。
* `index` 建议传入有效范围（通常 1-4）。
::::

## 设置配置名称

ServiceKeyboard.setConfigName(index, name)

**简要描述:**
设置指定配置索引的配置名称。

---

### 参数

| 参数名称 | 类型     | 描述               | 是否必需 | 默认值 |
|----------|----------|--------------------|----------|--------|
| `index`  | `number` | 配置索引（1-4）。  | 是       | 无     |
| `name`   | `string` | 要设置的配置名称。 | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<void>`
* **描述:** 设置成功解析为 `void`，失败时抛出错误。

---

### 使用示例

```js
async function updateConfigName(index, name) {
  // 需协议版本 >= v1.0.3.0（可通过 ServiceKeyboard.getProtocolVersion 校验）
  await ServiceKeyboard.setConfigName(index, name);
  console.log(`已设置配置 ${index} 的名称为: ${name}`);
}
```

---

### 注意事项

:::: tip

* 需要设备协议版本至少为 `v1.0.3.0`。
* 建议对 `name` 做长度与字符集校验，避免设备端写入失败。
* 设置后可调用 `ServiceKeyboard.getConfigName(index)` 读取校验。
::::

## 回报率列表查询

ServiceKeyboard.getRateOfReturnList()

**简要描述:**
获取设备支持的回报率列表。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<{ list: string[] }>`
* **描述:** 返回包含回报率字符串列表，如 `['R8','R16', ...]`。

---

### 使用示例

```js
async function fetchRateOfReturnList() {
  // 需协议版本 >= v1.0.7.0
  const { list } = await ServiceKeyboard.getRateOfReturnList();
  // 若需要下拉使用，可转成 {label,value,key}
  return list.map((rate, index) => ({ label: rate.replace('R', ''), value: index, key: rate }));
}
```

---

### 注意事项

:::: tip

* 需要设备协议版本至少为 `v1.0.7.0`。
* 列表项通常以 `R` 加速率数字的形式返回，例如 `R8KHz`。
::::

## 获取当前回报率

ServiceKeyboard.getRateOfReturn()

**简要描述:**
获取设备当前使用的回报率索引。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<{ value: number }>`
* **描述:** 返回当前回报率对应的索引。

---

### 使用示例

```js
async function fetchCurrentRateOfReturn() {
  // 需协议版本 >= v1.0.7.0
  const { value } = await ServiceKeyboard.getRateOfReturn();
  return value;
}
```

---

### 注意事项

:::: tip

* 需要设备协议版本至少为 `v1.0.7.0`。
* 可结合 `getRateOfReturnList()` 将索引映射到实际显示名称。
::::

## 设置回报率

ServiceKeyboard.setRateOfReturn(value)

**简要描述:**
设置设备回报率。

---

### 参数

| 参数名称 | 类型     | 描述                                 | 是否必需 | 默认值 |
|----------|----------|--------------------------------------|----------|--------|
| `value`  | `number` | 目标回报率索引（来自列表的 value 字段）。 | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<void>`
* **描述:** 设置成功解析为 `void`，失败时抛出错误。

---

### 使用示例

```js
async function updateRateOfReturn(value) {
  // 需协议版本 >= v1.0.7.0
  await ServiceKeyboard.setRateOfReturn(value);
}
```

---

### 注意事项

:::: tip

* 需要设备协议版本至少为 `v1.0.7.0`。
* 建议在设置后再次调用 `getRateOfReturn()` 校验结果，或根据需要刷新 UI。
::::

## 获取 RT 精度

ServiceKeyboard.getRtPrecision()

**简要描述:**
获取设备支持的RT最小精度（步进最小值）。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<{ min: number }>`
* **描述:** 返回最小步进精度，单位与设备定义一致（例如毫秒）。

**返回值示例:**

```js
{
  "min": 0.001
}
```

---

### 使用示例

```js
async function fetchRtPrecision() {
  const { min } = await ServiceKeyboard.getRtPrecision();
  console.log('RT精度最小步进:', min);
  return min;
}
```

## 获取系统睡眠时间（分钟）

ServiceKeyboard.getLightingSleepTime()

**简要描述:**
获取键盘系统睡眠时间（单位：分钟）。0 表示永不休眠，1 表示 1 分钟，2 表示 2 分钟，依次类推。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<number>`
* **描述:** 返回系统睡眠时间（分钟）。

**返回值示例:**

```js
3 // 表示 3 分钟
```

---

### 使用示例

```js
async function fetchLightingSleepTime() {
  // 需协议版本 >= v1.0.4.0
  const minutes = await ServiceKeyboard.getLightingSleepTime();
  console.log('系统睡眠时间(分钟):', minutes);
  return minutes;
}
```

---

### 注意事项

:::: tip

* 需要设备协议版本至少为 `v1.0.4.0`。
* 0 表示永不休眠；正整数表示分钟数。
::::

## 设置系统睡眠时间（分钟）

ServiceKeyboard.setLightingSleepTime(time)

**简要描述:**
设置键盘系统睡眠时间（单位：分钟）。0 表示永不休眠，1 表示 1 分钟，2 表示 2 分钟，依次类推。

---

### 参数

| 参数名称 | 类型     | 描述                 | 是否必需 | 默认值 |
|----------|----------|----------------------|----------|--------|
| `time`   | `number` | 睡眠时间（分钟）。   | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<void>`
* **描述:** 设置成功解析为 `void`，失败时抛出错误。

---

### 使用示例

```js
async function updateLightingSleepTime(time) {
  // 需协议版本 >= v1.0.4.0
  await ServiceKeyboard.setLightingSleepTime(time);
  console.log('已设置系统睡眠时间(分钟):', time);
}
```

---

### 注意事项

:::: tip

* 需要设备协议版本至少为 `v1.0.4.0`。
* 0 表示永不休眠；建议根据需求限制为合理的分钟数范围。
::::

## 关闭当前设备

ServiceKeyboard.closeDevice()

**简要描述:**
关闭当前已初始化并连接的设备，会释放与该设备的会话。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<void>`
* **描述:** 操作成功解析为 `void`；如关闭失败会抛出错误。

---

### 使用示例

```js
async function closeCurrentDevice() {
  try {
    await ServiceKeyboard.closeDevice();
    console.log('当前设备已关闭');
  } catch (error) {
    console.error('关闭设备失败:', error);
  }
}

// closeCurrentDevice();
```

## 重新连接设备

ServiceKeyboard.reconnection()

**简要描述:**
尝试重新连接到指定的设备。

---

### 参数

| 参数名称   | 类型     | 描述                           | 是否必需 | 默认值 |
|------------|----------|--------------------------------|----------|--------|
| `device`   | `Device` | 要重新连接的 `Device` 对象实例。 | 是       | 无     |
| `deviceId` | `string` | 要重新连接的设备的唯一标识符。   | 是       | 无     |

---

### 返回值

* **总体类型:** `Promise<void>`
* **描述:** 返回一个 `Promise`。操作成功完成时，`Promise` 解析，无特定返回值。如果重连失败，`Promise` 会拒绝并返回一个错误。

---

### 使用示例

```js

const listener = async ({ device, type }) => {
  if (type === 'disconnect') {
    // 设备断开连接
    if (device?.collections?.length) {
      try {
        const targetCollection = device.collections.find(
          (collection) => collection.usage === 1 && collection.usagePage === 0xffb0,
        );
        if (targetCollection) {
          // 处理设备断开连接后的逻辑
        }
      } catch (error) {
        console.error('设备断开连接处理失败:', error);
      }
    }
  } 
  
  if (type === 'connect') {
    if (device?.collections?.length) {
      try {
        const targetCollection = device.collections.find(
          (collection) => collection.usage === 1 && collection.usagePage === 0xffb0,
        );
        if (targetCollection) {
          // 处理设备连接后的逻辑
        }
      } catch (error) {
        console.error('设备连接处理失败:', error);
      }
    }
  }
}

ServiceKeyboard.on('usbChange', listener);

// 移除监听
ServiceKeyboard.off('usbChange', listener);

// 在插拔事件、恢复出厂、升级结束后需要重连
```

## 设备插拔事件

ServiceKeyboard.on('usbChange', callback)

**简要描述:**
监听设备的插拔事件，包括普通连接/断开、升级过程中的连接/断开等状态变化。

---

### 参数

| 参数名称   | 类型     | 描述                           | 是否必需 | 默认值 |
|------------|----------|--------------------------------|----------|--------|
| `eventName`| `string` | 事件名称，固定为 'usbChange'    | 是       | 无     |
| `callback` | `function` | 事件回调函数，接收设备状态变化信息 | 是     | 无     |

---

### 回调函数参数

| 参数名称 | 类型     | 描述                           |
|----------|----------|--------------------------------|
| `data`   | `object` | 包含设备状态变化信息的对象      |
| `data.type` | `string` | 事件类型，可能的值包括：<br>- 'connect': 设备连接<br>- 'disconnect': 设备断开<br>- 'isUpgrading_connect': 升级过程中设备连接<br>- 'isUpgrading_disconnect': 升级过程中设备断开 |
| `data.device` | `Device` | 设备对象，包含设备信息 |
| `data.updateFail` | `boolean` | 是否是在更新写入数据中更新失败了，比如在更新中过程中拔掉了键盘 |
| `data.reconnect` | `boolean` | 是否已经重新连接成功 |

---

### 使用示例

```js
ServiceKeyboard.on('usbChange', (data) => {
  console.log('USB设备变化:', data);
  const { device } = data;
  
  if (data.updateFail) {
    // 处理更新失败的情况
  }
  
  if (data.type === 'disconnect' || data.type === 'isUpgrading_disconnect') {
    // 设备断开连接
    if (device?.collections?.length) {
      try {
        const targetCollection = device.collections.find(
          (collection) => collection.usage === 1 && collection.usagePage === 0xffb0,
        );
        if (targetCollection) {
          // 处理设备断开连接后的逻辑
        }
      } catch (error) {
        console.error('设备断开连接处理失败:', error);
      }
    }
  }

  if (data.type === 'connect' || (data.type === 'isUpgrading_connect' && data.reconnect)) {
    if (device?.collections?.length) {
      try {
        const targetCollection = device.collections.find(
          (collection) => collection.usage === 1 && collection.usagePage === 0xffb0,
        );
        if (targetCollection) {
          // 处理设备连接后的逻辑
        }
      } catch (error) {
        console.error('设备连接处理失败:', error);
      }
    }
  }
});
```

---

### 注意事项

::: tip

* 在恢复出厂设置、固件升级等操作后，会多次触发设备的插拔事件。
* 建议在设备连接后重新获取设备信息、配置信息等数据。
* 在升级过程中的设备断开和重连需要特殊处理，确保升级流程的完整性。
* 可以通过 `data.updateFail` 判断是否在写入数据中更新失败，进行相应的错误处理。
* 在插拔事件里已经处理好了设备的自动重连，不需要再调用重连接口了
:::

## 进入Bootloader模式

ServiceKeyboard.appToBoot()

**简要描述:**
使设备进入 Bootloader 模式，通常用于擦除或准备更新固件。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<void>`
* **描述:** 返回一个 `Promise`。操作成功完成时，`Promise` 解析，无特定返回值。如果操作失败，`Promise` 会拒绝并返回一个错误。

---

### 使用示例

```js
async function enterBootloaderMode() {
  try {
    // 确保设备已初始化
    // await ServiceKeyboard.init(deviceId);
    console.log('正在尝试使设备进入 Bootloader 模式...');
    await ServiceKeyboard.appToBoot();
    console.log('设备已成功进入 Bootloader 模式或相关指令已发送。');
    // 此时设备可能已断开连接，需要重新扫描或等待设备以 Bootloader 模式出现
  } catch (error) {
    console.error('使设备进入 Bootloader 模式失败:', error);
  }
}

// enterBootloaderMode();
```

---

### 注意事项

::: tip

* 执行此操作后，设备通常会断开连接并以 Bootloader 模式重新枚举（如果支持）。您可能需要重新扫描设备或使用特定的 Bootloader 工具进行后续操作（如固件更新）。
* tip: 擦除后，需要重新连接设备,调用重连接口`ServiceKeyboard.reconnection`。
:::

## 从Bootloader模式返回应用模式

ServiceKeyboard.bootToApp()

**简要描述:**
使设备从 Bootloader 模式返回到应用模式。

---

### 参数

此方法不需要参数。

---

### 返回值

* **总体类型:** `Promise<void>`
* **描述:** 返回一个 `Promise`。操作成功完成时，`Promise` 解析，无特定返回值。如果操作失败，`Promise` 会拒绝并返回一个错误。

---

### 使用示例

```js
async function returnToAppMode() {
  try {
    console.log('正在尝试使设备从 Bootloader 模式返回到应用模式...');
    await ServiceKeyboard.bootToApp();
    console.log('设备已成功返回到应用模式。');
    // 此时设备可能已断开连接，需要重新扫描或等待设备以应用模式出现
  } catch (error) {
    console.error('使设备返回到应用模式失败:', error);
  }
}

// returnToAppMode();
```

---

### 注意事项

::: tip

* 执行此操作后，设备通常会断开连接并以应用模式重新枚举。您需要重新扫描设备或等待设备重新连接。
* 建议在操作完成后重新连接设备，调用重连接口 `ServiceKeyboard.reconnection`。
:::

## Bin文件更新固件

ServiceKeyboard.upgrade()

**简要描述:**
向处于 Bootloader 模式的设备更新固件。

---

### 参数

| 参数名称   | 类型                                                  | 描述                                                           | 是否必需 | 默认值 |
|------------|-------------------------------------------------------|----------------------------------------------------------------|----------|--------|
| `buffer`   | `ArrayBuffer`                                         | 包含新固件二进制数据的 `ArrayBuffer`。                          | 是       | 无     |
| `callback` | `(data: {current: number, total: number, updateStatus: string}) => void` | 一个回调函数，用于报告固件更新的进度。`data.current` 是已传输的字节数，`data.total` 是总字节数，`data.updateStatus` 是当前更新状态。 | 否       | 无     |
| `options`  | `object`                                              | 更新过程中的配置选项。(可根据实际设备情况去调试)                                          | 否       | 有     |
| `options.toBootDelay` | `number`                                        | 进入 Bootloader 模式后的延迟时间（毫秒）。                      | 否       | 4000   |
| `options.writeDelay`  | `number`                                        | 写入数据时的延迟时间（毫秒）。                                  | 否       | 30     |
| `options.toAppDelay`  | `number`                                        | 返回应用模式时的延迟时间（毫秒）。                              | 否       | 4000   |

---

### 返回值

* **总体类型:** `Promise<{ success: boolean }>`
* **描述:** 返回一个 `Promise`，该 `Promise` 解析为一个对象，指明固件更新是否成功。
* **解析对象结构:**

| 字段名称  | 类型      | 描述             | 示例值  |
|-----------|-----------|------------------|---------|
| `success` | `boolean` | 指示更新是否成功。 | `true`  |

---

### 使用示例

```js
async function performFirmwareUpdate(firmwareBuffer: ArrayBuffer) {
  try {
    // 确保设备处于 Bootloader 模式
    // await ServiceKeyboard.toBoot();
    // 等待设备以 Bootloader 模式重新连接并获取其新的 deviceId/handle

    console.log('开始固件更新...');
    const update = () => {
      const reader = new FileReader();
      reader.readAsArrayBuffer(fileList.value[0].raw);
      reader.onload = async () => {
        loading.value = true;
        try {
          const res = await ServiceKeyboard.upgrade(
            reader.result,
            ({ current, total, updateStatus: status }) => {
              progress.current = current;
              progress.total = total;
              updateStatus.value = status;
            },
            {
              toBootDelay: 4000,
              writeDelay: 30,
              toAppDelay: 4000,
            }
          );
          afterUpdate();
        } catch (error) {
          console.log('error: ', error);
          visible.value = false;
          step.value = 1;
          progress.current = 0;
        }
        loading.value = false;
      };
    };
    // 更新后设备通常会重启
  } catch (error) {
    console.error('固件更新过程中发生错误:', error);
  }
}
// const myFirmwareArrayBuffer: ArrayBuffer = ...;
// performFirmwareUpdate(myFirmwareArrayBuffer);
```

---

### 注意事项

::: tip

* `callback` 函数中的 `updateStatus` 参数可以用来显示当前更新的具体状态。
* 可以通过 `options` 参数调整更新过程中的各个延迟时间，以适应不同的设备需求。
:::

## 恢复出厂设置

ServiceKeyboard.GFSRestore()

**简要描述:**
将键盘恢复到出厂默认设置。此操作会清除所有用户自定义的配置，包括灯光设置、按键映射、宏设置等。

### 参数

此方法不需要参数。

### 返回值

**类型:** `Promise<void>`

**描述:** 返回一个 `
