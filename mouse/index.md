# Mouse 模块方法梳理

本文档梳理 `mouse` 主要模块的可调用方法，包含作用、传参、调用方式和调用示例。

业务侧推荐通过协议定义创建 `client`，再调用挂载在 `client` 上的模块：

```ts
import { mouseProtocolDefinition } from '@sparklinkplayjoy/protocol-mouse';

const client = session.createClient(mouseProtocolDefinition);

await client.device.getProtocolVersion();
await client.globalSetting.getDPI();
await client.globalSetting.getRadioFrequencyMode();
await client.keyRemapping.queryButtons();
await client.macro.getMacroMode({ macroId: 1 });
await client.upload.downloadInit();
```

如需指定目标设备地址，可使用工厂函数创建带配置的协议定义：

```ts
import { createMouseProtocolDefinition } from '@sparklinkplayjoy/protocol-mouse';

const mouseProtocol = createMouseProtocolDefinition({
  targetAddress: 0x05,
});

const client = session.createClient(mouseProtocol);
```

## 入口模块

源码位置：

- `index.ts`
- `src/protocol.ts`
- `src/client.ts`

### `createMouseProtocolDefinition(options?)`

作用：创建 mouse 协议定义对象，供 `session.createClient(...)` 使用。

传参：

| 参数                    | 类型                   | 必填 | 说明                                              |
| ----------------------- | ---------------------- | ---- | ------------------------------------------------- |
| `options`               | `MouseProtocolOptions` | 否   | mouse 协议配置。                                  |
| `options.targetAddress` | `number`               | 否   | 目标设备地址。不传时使用 `SoftwareFrame.destId`。 |

返回值：协议定义对象，内部会创建 `MouseClient`。

调用方式：

```ts
const protocol = createMouseProtocolDefinition(options);
const client = session.createClient(protocol);
```

调用示例：

```ts
import { createMouseProtocolDefinition } from '@sparklinkplayjoy/protocol-mouse';

const protocol = createMouseProtocolDefinition({
  targetAddress: 0x05,
});

const client = session.createClient(protocol);
```

### `mouseProtocolDefinition`

作用：默认 mouse 协议定义对象，适合多数业务直接使用。

传参：无。

返回值：协议定义对象。

调用方式：

```ts
const client = session.createClient(mouseProtocolDefinition);
```

调用示例：

```ts
import { mouseProtocolDefinition } from '@sparklinkplayjoy/protocol-mouse';

const client = session.createClient(mouseProtocolDefinition);
```

### `createMouseClient(device, options?)`

作用：直接基于 `ProtocolDeviceIO` 创建 mouse client。通常由 `session.createClient(...)` 间接调用，业务侧一般不需要直接调用。

传参：

| 参数      | 类型                   | 必填 | 说明                                                         |
| --------- | ---------------------- | ---- | ------------------------------------------------------------ |
| `device`  | `ProtocolDeviceIO`     | 是   | 协议设备 IO，由 `@sparklinkplayjoy/protocol-contract` 提供。 |
| `options` | `MouseProtocolOptions` | 否   | mouse 协议配置。                                             |

返回值：`MouseClient`，包含 `device`、`globalSetting`、`keyRemapping`、`macro`、`performance`、`upload` 六个业务模块。

调用方式：

```ts
const client = createMouseClient(device, options);
```

调用示例：

```ts
import { createMouseClient } from '@sparklinkplayjoy/protocol-mouse';

const client = createMouseClient(deviceIO, {
  targetAddress: 0x05,
});
```
