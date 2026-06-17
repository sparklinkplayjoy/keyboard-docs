# 运行时与协议内部模块

以下 API 主要供协议包内部使用；业务侧优先调用上面的 `client.*` 方法。

## 兼容解析导出

这些函数从业务模块中导出，主要用于兼容旧代码中“直接解包”的调用方式。新业务通常不需要直接使用。

| 方法                               | 作用                   | 传参                                                      | 返回值                     | 示例                                  |
| ---------------------------------- | ---------------------- | --------------------------------------------------------- | -------------------------- | ------------------------------------- |
| `GFSConfigSwitchListRecData(data)` | 解析配置档位响应数据。 | `Uint8Array \| number[] \| Array<Uint8Array \| number[]>` | `GlobalFeatureConfigParam` | `GFSConfigSwitchListRecData(payload)` |
| `KRMQueryButtonRecData(data)`      | 解析按键映射查询响应。 | `Uint8Array`                                              | `KeyRemappingResult`       | `KRMQueryButtonRecData(payload)`      |
| `KRMSetButtonRecData(data)`        | 解析按键映射写入响应。 | `Uint8Array`                                              | `KeyRemappingResult`       | `KRMSetButtonRecData(payload)`        |

## `resolveMouseProtocolOptions(options?)`

作用：补齐 mouse 协议配置默认值。

传参：

| 参数                    | 类型     | 必填 | 说明                                              |
| ----------------------- | -------- | ---- | ------------------------------------------------- |
| `options.targetAddress` | `number` | 否   | 目标设备地址。不传时使用 `SoftwareFrame.destId`。 |

返回值：`ResolvedMouseProtocolOptions`。

调用示例：

```ts
const options = resolveMouseProtocolOptions({
  targetAddress: 0x05,
});
```

## `createMouseRuntimeContext(device, options?)`

作用：创建 runtime 上下文，封装请求排队、发送、响应匹配、订阅未匹配帧等能力。

传参：

| 参数      | 类型                   | 必填 | 说明             |
| --------- | ---------------------- | ---- | ---------------- |
| `device`  | `ProtocolDeviceIO`     | 是   | 设备 IO。        |
| `options` | `MouseProtocolOptions` | 否   | mouse 协议配置。 |

返回值：`MouseRuntimeContext`。

常用方法：

| 方法                          | 作用                                      |
| ----------------------------- | ----------------------------------------- |
| `query(packet, definition)`   | 发送请求并等待单个响应。                  |
| `collect(packet, definition)` | 发送请求并按 `collect` 条件收集多个响应。 |
| `send(packet, options?)`      | 只发送，不要求响应。                      |
| `subscribe(handler)`          | 订阅未匹配的输入帧，返回取消订阅函数。    |

调用示例：

```ts
const context = createMouseRuntimeContext(deviceIO);

const unsubscribe = context.subscribe((packet) => {
  console.log(packet.mainCmd, packet.subCmd);
});

unsubscribe();
```

## `createMouseOperation(runtime)`

作用：把 runtime 能力包装为模块层使用的帧操作 API。模块层只负责组帧和解析，发送、排队和超时交给 runtime。

传参：

| 参数      | 类型                  | 必填 | 说明                   |
| --------- | --------------------- | ---- | ---------------------- |
| `runtime` | `MouseRuntimeContext` | 是   | mouse runtime 上下文。 |

返回值：`MouseOperation`。

方法：

| 方法                                 | 作用                                                                  |
| ------------------------------------ | --------------------------------------------------------------------- |
| `queryFrame(frame, parse, options?)` | 发送业务帧并解析响应 payload。可通过 `expectedResponses` 收集多响应。 |
| `sendFrame(frame, options?)`         | 发送业务帧并返回原始 payload。                                        |
| `sendFrameNoResponse(frame)`         | 发送业务帧，不等待响应。                                              |

调用示例：

```ts
const operation = createMouseOperation(context);

const result = await operation.queryFrame([0x01, 0x05], (payload) => payload);
```

## `RequestRuntime`

作用：底层请求执行器，负责队列、重试、超时、响应匹配、延迟响应处理。

构造参数：

| 参数               | 类型                     | 必填 | 说明       |
| ------------------ | ------------------------ | ---- | ---------- |
| `options.deviceIO` | `ProtocolDeviceIO`       | 是   | 设备 IO。  |
| `options.parser`   | `ProtocolParser<TFrame>` | 是   | 帧解析器。 |

方法：

| 方法                  | 作用                               | 调用方式                                 |
| --------------------- | ---------------------------------- | ---------------------------------------- |
| `execute(definition)` | 执行一次请求定义。                 | `await runtime.execute(definition)`      |
| `subscribe(handler)`  | 订阅未匹配帧。                     | `const off = runtime.subscribe(handler)` |
| `destroy()`           | 销毁 runtime，取消订阅并重置状态。 | `runtime.destroy()`                      |

调用示例：

```ts
const runtime = new RequestRuntime({
  deviceIO,
  parser: mouseParser,
});

const response = await runtime.execute({
  key: 'example.query',
  encode: () => packet,
});

runtime.destroy();
```

## `ResponseRouter`

作用：把解析后的输入帧路由给当前活跃请求；未匹配帧或超时后迟到帧会进入孤帧存储。

构造参数：

| 参数     | 类型                              | 必填 | 说明           |
| -------- | --------------------------------- | ---- | -------------- |
| `device` | `DeviceInfo`                      | 是   | 当前设备信息。 |
| `frame$` | `Observable<FramedInput<TFrame>>` | 是   | 已解析帧流。   |

方法：

| 方法                          | 作用                                             | 调用方式                                   |
| ----------------------------- | ------------------------------------------------ | ------------------------------------------ |
| `activateRequest(binding)`    | 激活一个请求绑定，后续匹配帧会进入该请求响应流。 | `router.activateRequest(binding)`          |
| `completeActiveRequest()`     | 完成当前活跃请求。                               | `router.completeActiveRequest()`           |
| `cancelActiveRequest()`       | 取消当前活跃请求。                               | `router.cancelActiveRequest()`             |
| `markActiveRequestTimedOut()` | 标记当前请求超时，并记录迟到响应匹配器。         | `router.markActiveRequestTimedOut()`       |
| `observeUnmatched()`          | 订阅未匹配帧。                                   | `router.observeUnmatched().subscribe(...)` |
| `destroy()`                   | 销毁路由器并清理订阅。                           | `router.destroy()`                         |

## `SessionStream`

作用：把设备输入 chunk 通过 parser 转换为共享的帧流。

构造参数：

| 参数     | 类型                             | 必填 | 说明         |
| -------- | -------------------------------- | ---- | ------------ |
| `input$` | `Observable<ProtocolInputChunk>` | 是   | 设备输入流。 |
| `parser` | `ProtocolParser<TFrame>`         | 是   | 协议解析器。 |

属性与方法：

| 名称        | 作用               | 调用方式                       |
| ----------- | ------------------ | ------------------------------ |
| `frame$`    | 解析后的共享帧流。 | `stream.frame$.subscribe(...)` |
| `destroy()` | 重置 parser 状态。 | `stream.destroy()`             |

## `OrphanFrameStore`

作用：存储和分发未匹配帧、迟到响应帧，并管理迟到响应匹配器。

方法：

| 方法                                | 作用                                                       | 调用方式                                |
| ----------------------------------- | ---------------------------------------------------------- | --------------------------------------- |
| `observe()`                         | 订阅孤帧事件。                                             | `store.observe().subscribe(...)`        |
| `push(frame, reason)`               | 推入孤帧，`reason` 为 `late-response` 或 `unmatched`。     | `store.push(frame, 'unmatched')`        |
| `rememberLateMatcher(match, ttlMs)` | 暂存一个迟到响应匹配器。                                   | `store.rememberLateMatcher(match, 200)` |
| `routeLateFrame(frame, context)`    | 判断输入帧是否命中迟到匹配器，命中时推入 `late-response`。 | `store.routeLateFrame(frame, context)`  |
| `destroy()`                         | 清空匹配器并关闭事件流。                                   | `store.destroy()`                       |

## `XshidPacketParser`

作用：把连续字节流解析为 `MousePacket`。会查找 `0xaa 0x55` 帧头、读取长度和 CRC，并产出通过 CRC 校验的包。

方法：

| 方法             | 作用                           | 传参                     | 返回值          |
| ---------------- | ------------------------------ | ------------------------ | --------------- |
| `pushData(data)` | 推入一段字节并尝试解析完整包。 | `Uint8Array \| number[]` | `MousePacket[]` |
| `reset()`        | 清空解析缓冲和状态。           | 无                       | `void`          |

调用示例：

```ts
const parser = new XshidPacketParser();
const packets = parser.pushData(inputBytes);
parser.reset();
```

## `mouseParser`

作用：基于 `XshidPacketParser` 包装出的 `ProtocolParser<MousePacket>`，供 runtime 消费。

调用示例：

```ts
const decoder = mouseParser.createDecoder();
const packets = decoder.push(hidChunk);
decoder.reset?.();
```
