# Mouse 模块方法梳理

本文档梳理 `protocol/mouse` 目录下主要模块的可调用方法，包含作用、传参、调用方式和调用示例。

业务侧推荐先通过设备插件打开物理设备，拿到这台设备对应的 `DeviceSession`，再通过协议定义创建 `client`。

这里的 `deviceSession.createClient(...)` 不是 `protocol/mouse` 包里直接导出的函数，而是设备会话对象提供的方法。它通常来自 `@sparklinkplayjoy/webhid-plugin` 的 `plugin.open(deviceId)` 返回值：

```ts
import { createWebHidPlugin } from '@sparklinkplayjoy/webhid-plugin';
import { mouseProtocolDefinition } from '@sparklinkplayjoy/protocol-mouse';

const plugin = createWebHidPlugin({
  filters: [
    {
      emptySummary: '未选择鼠标固件文件',
      key: 'mouse',
      label: '鼠标',
      productId: 0x1111,
      targetAddress: 0x03,
      usage: 0x01,
      usagePage: 0xffb0,
      vendorId: 0x2222,
    },
    {
      emptySummary: '未选择接收器固件文件',
      key: 'receiver',
      label: '接收器',
      productId: 0x3333,
      targetAddress: 0x05,
      usage: 0x01,
      usagePage: 0xffb0,
      vendorId: 0x6666,
    },
  ],
});

const devices = await plugin.getAuthorizedDevices();
const deviceSession = await plugin.open(devices[0].id);

const client = deviceSession.createClient(mouseProtocolDefinition);

// 调用示例
await client.device.getProtocolVersion();
await client.globalSetting.getDPI();
await client.globalSetting.getRadioFrequencyMode();
await client.keyRemapping.queryButtons();
await client.macro.getMacroMode({ macroId: 1 });
await client.upload.downloadInit();
```

可以把这条链路理解成：

1. `plugin.open(deviceId)` 打开设备，返回 `deviceSession`。
2. `deviceSession.createClient(mouseProtocolDefinition)` 把当前设备的 IO 能力交给 mouse 协议。
3. `mouseProtocolDefinition` 来自 `src/protocol.ts`，内部会调用 `createMouseClient(...)`。
4. `createMouseClient(...)` 来自 `src/client.ts`，负责把 `device`、`globalSetting`、`keyRemapping`、`macro`、`performance`、`upload` 等模块挂到最终的 `client` 上。

如需指定目标设备地址，可使用工厂函数创建带配置的协议定义：

```ts
import { createMouseProtocolDefinition } from '@sparklinkplayjoy/protocol-mouse';

const mouseProtocol = createMouseProtocolDefinition({
  targetAddress: 0x05,
});

const client = deviceSession.createClient(mouseProtocol);
```

## 入口模块

源码位置：

- `index.ts`
- `src/protocol.ts`
- `src/client.ts`

## 创建 mouse 协议定义对象

createMouseProtocolDefinition(options?)

**简要描述:**
创建 mouse 协议定义对象，供 `deviceSession.createClient(...)` 使用。

---

### 参数

| 参数                    | 类型                   | 是否必需 | 说明                                              |
| ----------------------- | ---------------------- | ---- | ------------------------------------------------- |
| `options`               | `MouseProtocolOptions` | 否   | mouse 协议配置。                                  |
| `options.targetAddress` | `number`               | 否   | 目标设备地址。不传时使用 `SoftwareFrame.destId`。 |

---

### 返回值

* **描述:** 协议定义对象，内部会创建 `MouseClient`。

---

### 使用示例

**调用方式:**

```ts
const protocol = createMouseProtocolDefinition(options);
const client = deviceSession.createClient(protocol);
```

**调用示例:**

```ts
import { createMouseProtocolDefinition } from '@sparklinkplayjoy/protocol-mouse';

const protocol = createMouseProtocolDefinition({
  targetAddress: 0x05,
});

const client = deviceSession.createClient(protocol);
```

## 使用默认 mouse 协议定义对象

mouseProtocolDefinition

**简要描述:**
默认 mouse 协议定义对象，适合多数业务直接使用。

---

### 参数

此方法使用mouseProtocolDefinition作为参数。

---

### 返回值

* **描述:** 协议定义对象。

---

### 使用示例

**调用方式:**

```ts
const client = deviceSession.createClient(mouseProtocolDefinition);
```

**调用示例:**

```ts
import { mouseProtocolDefinition } from '@sparklinkplayjoy/protocol-mouse';

const client = deviceSession.createClient(mouseProtocolDefinition);
```

## 创建 mouse client

createMouseClient(device, options?)

**简要描述:**
直接基于 `ProtocolDeviceIO` 创建 mouse client。通常由 `deviceSession.createClient(...)` 间接调用，业务侧一般不需要直接调用。

---

### 参数

| 参数      | 类型                   | 是否必需 | 说明                                                         |
| --------- | ---------------------- | ---- | ------------------------------------------------------------ |
| `device`  | `ProtocolDeviceIO`     | 是   | 协议设备 IO，由 `@sparklinkplayjoy/protocol-contract` 提供。 |
| `options` | `MouseProtocolOptions` | 否   | mouse 协议配置。 |
| `options.targetAddress` | `number` | 否 | 目标设备地址。不传时使用 `SoftwareFrame.destId`。 |

---

### 返回值

* **总体类型:** `MouseClient`
* **描述:** 包含 `device`、`globalSetting`、`keyRemapping`、`macro`、`performance`、`upload` 六个业务模块。

---

### 使用示例

**调用方式:**

```ts
const client = createMouseClient(device, options);
```

**调用示例:**

```ts
import { createMouseClient } from '@sparklinkplayjoy/protocol-mouse';

const client = createMouseClient(deviceIO, {
  targetAddress: 0x05,
});
```
