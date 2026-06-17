# 工具模块

源码位置：`src/utils/*`

这些方法主要服务于协议组包、字节转换、颜色转换、宏动作编码和旧版发送辅助。

## 字节与协议工具

| 方法                                                        | 作用                                                              | 传参                                  | 返回值                       | 示例                                                          |
| ----------------------------------------------------------- | ----------------------------------------------------------------- | ------------------------------------- | ---------------------------- | ------------------------------------------------------------- |
| `bitReadWrite(value = true)`                                | 把读写布尔值转为协议位，`true` 为读 `0x00`，`false` 为写 `0x01`。 | `boolean`                             | `number`                     | `bitReadWrite(true)`                                          |
| `getLightBitmap(lightSwitch, reverseEffect, superResponse)` | 生成灯光开关、反向效果、超级响应的 bitmap。                       | `boolean, boolean, boolean`           | `number`                     | `getLightBitmap(true, false, true)`                           |
| `getSomeBits(num = 1, bit = 0x00)`                          | 生成指定长度、指定填充值的数组。                                  | `number, number`                      | `number[]`                   | `getSomeBits(4, 0xff)`                                        |
| `lowByte(value)`                                            | 取低 8 位。                                                       | `number`                              | `number`                     | `lowByte(0x1234)`                                             |
| `highByte(value)`                                           | 取第 2 个字节。                                                   | `number`                              | `number`                     | `highByte(0x1234)`                                            |
| `highByte16(value)`                                         | 取第 3 个字节。                                                   | `number`                              | `number`                     | `highByte16(0x123456)`                                        |
| `highByte24(value)`                                         | 取第 4 个字节。                                                   | `number`                              | `number`                     | `highByte24(0x12345678)`                                      |
| `computeHighLowByte(value)`                                 | 拆成小端低/高字节。                                               | `number`                              | `number[]`                   | `computeHighLowByte(1000)`                                    |
| `u8ToU16(low, high)`                                        | 两个 8 位小端字节合成 16 位数。                                   | `number, number`                      | `number`                     | `u8ToU16(0xe8, 0x03)`                                         |
| `calcDoubleLowToSingleHigh(doubleLow)`                      | `Uint8Array` 每两个小端字节合成 `Uint16Array`。                   | `Uint8Array`                          | `Uint16Array`                | `calcDoubleLowToSingleHigh(new Uint8Array([1, 0]))`           |
| `calcSingleHightoDoubleLow(singleHight)`                    | `Uint16Array` 拆成小端 `Uint8Array`。                             | `Uint16Array`                         | `Uint8Array`                 | `calcSingleHightoDoubleLow(new Uint16Array([256]))`           |
| `createProtocol(data, len = 64)`                            | 把业务帧包装为 HID 包；超过 `len - 2` 时自动拆多包。              | `number[], number?`                   | `Uint8Array \| Uint8Array[]` | `createProtocol([0x01, 0x05])`                                |
| `splitUint32ToUint8(value)`                                 | 32 位数拆成大端 4 字节。                                          | `number`                              | `number[]`                   | `splitUint32ToUint8(0x12345678)`                              |
| `splitUint8ToUint32LittleEndian(value)`                     | 32 位数拆成小端 4 字节。                                          | `number`                              | `number[]`                   | `splitUint8ToUint32LittleEndian(0x12345678)`                  |
| `combineUint8ToUint32(a, b, c, d)`                          | 4 个字节合成 32 位数。                                            | `number, number, number, number`      | `number`                     | `combineUint8ToUint32(0x12, 0x34, 0x56, 0x78)`                |
| `splitUint24ToUint8(value)`                                 | 24 位数拆成 3 字节。                                              | `number`                              | `number[]`                   | `splitUint24ToUint8(0x123456)`                                |
| `combineUint8ToUint24(a, b, c)`                             | 3 个字节合成 24 位数。                                            | `number, number, number`              | `number`                     | `combineUint8ToUint24(0x12, 0x34, 0x56)`                      |
| `convertTwoBytesToThreeSegments(data)`                      | 每 2 字节转换为 row、col、ratio 三段布局数据。                    | `Uint8Array`                          | `Uint8Array`                 | `convertTwoBytesToThreeSegments(data)`                        |
| `calculateCRC32(bytes)`                                     | 计算 CRC32 并返回低 16 位数值。                                   | `number[] \| Uint8Array`              | `number`                     | `calculateCRC32([0x01, 0x05])`                                |
| `packageHead(params)`                                       | 按软件帧格式拼接帧头、长度、CRC 和数据。                          | `{ crcData, distinguishHeader, len }` | `number[]`                   | `packageHead({ crcData, distinguishHeader: 0x55aa, len: 1 })` |
| `toNumber(value)`                                           | 空值或 0 归一为 0，否则返回原值。                                 | `number`                              | `number`                     | `toNumber(value)`                                             |
| `computeHighLowByteToNumber(value)`                         | 空值或 0 返回 `[0, 0]`，否则返回小端低/高字节。                   | `number`                              | `number[]`                   | `computeHighLowByteToNumber(1000)`                            |

## 枚举与布局工具

| 方法                               | 作用                                                                          | 传参            | 返回值                             | 示例                                                    |
| ---------------------------------- | ----------------------------------------------------------------------------- | --------------- | ---------------------------------- | ------------------------------------------------------- |
| `getKeyByValue(obj, value)`        | 根据枚举/对象值反查 key。                                                     | `object, value` | `key \| undefined`                 | `getKeyByValue(GlobalFeatureRateOfReturn, 1000)`        |
| `getEnumValueByKey(enumType, key)` | 根据 key 读取枚举值。                                                         | `object, key`   | `value \| undefined`               | `getEnumValueByKey(GlobalFeatureRateOfReturn, 'R1KHz')` |
| `getFormatLabel(enumObj, value)`   | 根据枚举值获取枚举 key，不存在时抛错。                                        | `enum, number`  | `keyof enum`                       | `getFormatLabel(GlobalFeatureRateOfReturn, 1000)`       |
| `keycodeToLayout(keycodes)`        | 把 keycode 数组转换为布局数组。                                               | `Uint16Array`   | `number[]`                         | `keycodeToLayout(keycodes)`                             |
| `keycodeToLayoutStyle(keyStyle)`   | 每 3 字节转换为 `{ row, col, ratio, type }`。`ratio === 12` 时类型为 `knob`。 | `Uint8Array`    | `Array<{ row; col; ratio; type }>` | `keycodeToLayoutStyle(styleBytes)`                      |

## 宏工具

| 方法                                       | 作用                                                                                    | 传参                     | 返回值                       | 示例                                       |
| ------------------------------------------ | --------------------------------------------------------------------------------------- | ------------------------ | ---------------------------- | ------------------------------------------ |
| `buildMacroAction(status, delay, keyCode)` | 把宏动作编码为 4 字节小端数据。`delay` 不能超过 `0x7fff`，`keyCode` 不能超过 `0xffff`。 | `number, number, number` | `number[]`                   | `buildMacroAction(1, 20, 0x0004)`          |
| `decodeMacroBytesArrayLE(bytes)`           | 把 4 字节小端宏动作解码为 `{ status, delay, keyCode }`。                                | `number[]`               | `{ status, delay, keyCode }` | `decodeMacroBytesArrayLE([4, 0, 20, 128])` |

## 颜色工具

| 方法                                          | 作用                                                        | 传参                                       | 返回值                | 示例                                                                |
| --------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------ | --------------------- | ------------------------------------------------------------------- |
| `hexToRgb(hex)`                               | 十六进制颜色转 RGB 对象。                                   | `string`                                   | `{ r, g, b } \| null` | `hexToRgb('#FF00AA')`                                               |
| `rgbToHex(r, g, b)`                           | RGB 数值转十六进制颜色字符串。                              | `number, number, number`                   | `string`              | `rgbToHex(255, 0, 170)`                                             |
| `hexToRgbArray(hex)`                          | 十六进制颜色转 RGB 数组。                                   | `string`                                   | `number[] \| null`    | `hexToRgbArray('#FF00AA')`                                          |
| `getLittleEndianColorArray(hexColor, format)` | 颜色字符串按灯光格式转小端字节。                            | `string, LightingDataMode`                 | `number[]`            | `getLittleEndianColorArray('#FF00AA', LightingDataMode.RGB888_U24)` |
| `getLittleEndianRgbArray(r, g, b, format)`    | RGB 数值按灯光格式转小端字节。                              | `number, number, number, LightingDataMode` | `number[]`            | `getLittleEndianRgbArray(255, 0, 170, LightingDataMode.RGB888_U24)` |
| `u32ToHex(bytes)`                             | U32 小端颜色字节转 hex。                                    | `number[]`                                 | `string`              | `u32ToHex([0xaa, 0x00, 0xff, 0x00])`                                |
| `u24ToHex(bytes)`                             | U24 小端颜色字节转 hex。                                    | `number[]`                                 | `string`              | `u24ToHex([0xaa, 0x00, 0xff])`                                      |
| `u16ToHex(bytes)`                             | RGB565 U16 小端颜色字节转 hex。                             | `number[]`                                 | `string`              | `u16ToHex([0x1f, 0xf8])`                                            |
| `u8ToHex(bytes)`                              | 单色灰度字节转 hex。                                        | `number[]`                                 | `string`              | `u8ToHex([128])`                                                    |
| `pixelDataToHex(bytes, format)`               | 根据灯光格式把像素字节转 hex。                              | `number[], LightingDataMode`               | `string`              | `pixelDataToHex(bytes, LightingDataMode.RGB888_U24)`                |
| `pixelDataToRgb(bytes, format)`               | 当前实现等同于 `pixelDataToHex`，返回 hex 字符串或 `null`。 | `number[], LightingDataMode`               | `string \| null`      | `pixelDataToRgb(bytes, LightingDataMode.RGB888_U24)`                |

## 精确计算工具

| 方法                                                     | 作用                               | 传参                                                                     | 返回值   | 示例                                        |
| -------------------------------------------------------- | ---------------------------------- | ------------------------------------------------------------------------ | -------- | ------------------------------------------- |
| `preciseCalculate(operation, num1, num2, precision = 3)` | 基于 `decimal.js` 做精确加减乘除。 | `'add' \| 'subtract' \| 'multiply' \| 'divide', number, number, number?` | `number` | `preciseCalculate('multiply', 0.1, 0.2, 4)` |

## 旧版协议发送辅助

源码位置：`src/utils/protocol.ts`

这些 API 依赖旧版 `DeviceBase`，新业务优先使用 `client.*` 模块方法。

| 方法                                                                             | 作用                                       | 传参                                                         | 返回值               | 示例                                                                             |
| -------------------------------------------------------------------------------- | ------------------------------------------ | ------------------------------------------------------------ | -------------------- | -------------------------------------------------------------------------------- |
| `createProtocolHelper(deviceBase)`                                               | 创建 `ProtocolHelper` 实例。               | `DeviceBase`                                                 | `ProtocolHelper`     | `const helper = createProtocolHelper(deviceBase)`                                |
| `ProtocolHelper.sendProtocol(buildProtocol, parseResult?, options?)`             | 发送单个或多个协议包，取首个响应并可解析。 | `() => Uint8Array \| Uint8Array[], parser?, { timeout? }?`   | `Promise<T \| null>` | `await helper.sendProtocol(build, parse)`                                        |
| `ProtocolHelper.sendProtocolMulti(buildProtocol, parseResult?, options?)`        | 发送多个协议包并解析多个响应。             | `() => Uint8Array[], parser?, { timeout? }?`                 | `Promise<T[]>`       | `await helper.sendProtocolMulti(build)`                                          |
| `ProtocolHelper.sendProtocolMultiResponse(buildProtocol, parseResult?, options)` | 发送单个协议包并等待多个响应。             | `() => Uint8Array, parser?, { expectedResponses, timeout? }` | `Promise<T[]>`       | `await helper.sendProtocolMultiResponse(build, parse, { expectedResponses: 2 })` |
| `ProtocolHelper.sendProtocolNoResponse(buildProtocol)`                           | 发送协议包且不等待响应。                   | `() => Uint8Array`                                           | `Promise<void>`      | `await helper.sendProtocolNoResponse(build)`                                     |
| `sendProtocol(deviceBase, buildProtocol, parseResult?, options?)`                | 函数式单包发送辅助。                       | `DeviceBase, () => Uint8Array, parser?, { timeout? }?`       | `Promise<T \| null>` | `await sendProtocol(deviceBase, build, parse)`                                   |
| `sendProtocolNoResponse(deviceBase, buildProtocol)`                              | 函数式无响应发送辅助。                     | `DeviceBase, () => Uint8Array`                               | `Promise<void>`      | `await sendProtocolNoResponse(deviceBase, build)`                                |
