# 全局设置

源码位置：`src/modules/global-setting/*`

模块作用：读取和写入鼠标全局配置。调用入口为 `client.globalSetting`。

## `client.globalSetting.factoryReset(callback?)`

作用：恢复出厂设置。

传参：

| 参数       | 类型                                                              | 必填 | 说明                                                                   |
| ---------- | ----------------------------------------------------------------- | ---- | ---------------------------------------------------------------------- |
| `callback` | `(status: { status: 'pending' \| 'success' \| 'error' }) => void` | 否   | 状态回调。发送前回调 `pending`，成功回调 `success`，异常回调 `error`。 |

返回值：`Promise<boolean>`，成功为 `true`，失败为 `false`。

调用方式：

```ts
const ok = await client.globalSetting.factoryReset(callback);
```

调用示例：

```ts
const ok = await client.globalSetting.factoryReset(({ status }) => {
  console.log('factory reset status:', status);
});
```

## `client.globalSetting.getConfigs()`

作用：读取配置档位列表和当前配置索引。

传参：无。

返回值：`Promise<GlobalFeatureConfigParam>`。

返回字段：

| 字段         | 类型       | 说明                                         |
| ------------ | ---------- | -------------------------------------------- |
| `total`      | `number`   | 配置总数。                                   |
| `currentIdx` | `number`   | 当前配置索引。                               |
| `configs`    | `string[]` | 配置名称列表。每个名称协议侧按 32 字节处理。 |

调用方式：

```ts
const configs = await client.globalSetting.getConfigs();
```

调用示例：

```ts
const configs = await client.globalSetting.getConfigs();
console.log(configs.currentIdx, configs.configs);
```

## `client.globalSetting.setConfigs(param)`

作用：写入配置档位列表和当前配置索引。

传参：

| 参数               | 类型       | 必填 | 说明                                                              |
| ------------------ | ---------- | ---- | ----------------------------------------------------------------- |
| `param.total`      | `number`   | 是   | 配置总数。                                                        |
| `param.currentIdx` | `number`   | 是   | 当前配置索引。                                                    |
| `param.configs`    | `string[]` | 是   | 配置名称列表。写入时单个名称会按 UTF-8 截断到 32 字节以内并补零。 |

返回值：`Promise<GlobalFeatureConfigParam>`，返回设备确认后的配置数据。

调用方式：

```ts
const result = await client.globalSetting.setConfigs(param);
```

调用示例：

```ts
const result = await client.globalSetting.setConfigs({
  total: 4,
  currentIdx: 0,
  configs: ['Default', 'FPS', 'Office', 'Game'],
});
```

## `client.globalSetting.getDPI()`

作用：读取 DPI 设置。

传参：无。

返回值：`Promise<GlobalFeatureDPIParam>`。

返回字段：

| 字段                  | 类型       | 说明                  |
| --------------------- | ---------- | --------------------- |
| `currentDPI`          | `number`   | 当前 DPI。            |
| `maxDPI`              | `number`   | 最大 DPI。            |
| `maxDPISteps`         | `number`   | 最大 DPI 档位数。     |
| `dpiStepCount`        | `number`   | 当前有效 DPI 档位数。 |
| `dpiValues`           | `number[]` | DPI 档位值。          |
| `currentDPIStepIndex` | `number`   | 当前 DPI 档位索引。   |

调用方式：

```ts
const dpi = await client.globalSetting.getDPI();
```

调用示例：

```ts
const dpi = await client.globalSetting.getDPI();
console.log(dpi.currentDPI, dpi.dpiValues);
```

## `client.globalSetting.setDPI(param)`

作用：写入 DPI 设置。

传参：

| 参数                        | 类型       | 必填 | 说明                                       |
| --------------------------- | ---------- | ---- | ------------------------------------------ |
| `param.currentDPI`          | `number`   | 是   | 当前 DPI。                                 |
| `param.maxDPI`              | `number`   | 是   | 最大 DPI。                                 |
| `param.maxDPISteps`         | `number`   | 是   | 最大 DPI 档位数。                          |
| `param.dpiStepCount`        | `number`   | 是   | 有效 DPI 档位数。                          |
| `param.currentDPIStepIndex` | `number`   | 是   | 当前 DPI 档位索引。                        |
| `param.dpiValues`           | `number[]` | 是   | DPI 档位值。长度应与 `dpiStepCount` 一致。 |

返回值：`Promise<GlobalFeatureDPIParam>`，返回设备确认后的 DPI 设置。

调用方式：

```ts
const result = await client.globalSetting.setDPI(param);
```

调用示例：

```ts
const dpi = await client.globalSetting.getDPI();

const result = await client.globalSetting.setDPI({
  ...dpi,
  currentDPI: 1600,
  currentDPIStepIndex: 1,
  dpiValues: [800, 1600, 3200, 6400],
  dpiStepCount: 4,
});
```

## `client.globalSetting.getReportSettings()`

作用：读取回报率设置。

传参：无。

返回值：`Promise<GlobalFeatureReportParam>`。

返回字段：

| 字段          | 类型                              | 说明                                        |
| ------------- | --------------------------------- | ------------------------------------------- |
| `reportTotal` | `number`                          | 支持的回报率数量。                          |
| `reportIndex` | `number`                          | 当前回报率在 `reports` 中的索引。           |
| `reports`     | `GlobalFeatureRateOfReturnType[]` | 支持的回报率枚举键，例如 `R1KHz`、`R8KHz`。 |

调用方式：

```ts
const report = await client.globalSetting.getReportSettings();
```

调用示例：

```ts
const report = await client.globalSetting.getReportSettings();
console.log(report.reportIndex, report.reports);
```

## `client.globalSetting.setReportSettings(reportIndex)`

作用：写入当前回报率索引。

传参：

| 参数          | 类型     | 必填 | 说明                           |
| ------------- | -------- | ---- | ------------------------------ |
| `reportIndex` | `number` | 是   | 回报率索引，不是 Hz 数值本身。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用方式：

```ts
const ok = await client.globalSetting.setReportSettings(reportIndex);
```

调用示例：

```ts
const report = await client.globalSetting.getReportSettings();
const nextIndex = report.reports.indexOf('R1KHz');

if (nextIndex >= 0) {
  await client.globalSetting.setReportSettings(nextIndex);
}
```

## `client.globalSetting.getKeyPressScan()`

作用：读取按键扫描率设置。

传参：无。

返回值：`Promise<GlobalFeatureKeyPressScanParam>`。

返回字段：

| 字段                 | 类型       | 说明                   |
| -------------------- | ---------- | ---------------------- |
| `currentScanRate`    | `number`   | 当前按键扫描率。       |
| `supportedScanRates` | `number[]` | 支持的按键扫描率列表。 |

调用方式：

```ts
const scan = await client.globalSetting.getKeyPressScan();
```

调用示例：

```ts
const scan = await client.globalSetting.getKeyPressScan();
console.log(scan.currentScanRate, scan.supportedScanRates);
```

## `client.globalSetting.setKeyPressScan(scanRate)`

作用：写入按键扫描率。

传参：

| 参数       | 类型     | 必填 | 说明                                                                                  |
| ---------- | -------- | ---- | ------------------------------------------------------------------------------------- |
| `scanRate` | `number` | 是   | 要写入的按键扫描率。建议使用 `getKeyPressScan()` 返回的 `supportedScanRates` 中的值。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用方式：

```ts
const ok = await client.globalSetting.setKeyPressScan(scanRate);
```

调用示例：

```ts
const scan = await client.globalSetting.getKeyPressScan();
await client.globalSetting.setKeyPressScan(scan.supportedScanRates[0]);
```

## `client.globalSetting.getSensorScan()`

作用：读取传感器扫描率设置。

传参：无。

返回值：`Promise<GlobalFeatureSensorScanParam>`。

返回字段：

| 字段                 | 类型       | 说明                     |
| -------------------- | ---------- | ------------------------ |
| `currentScanRate`    | `number`   | 当前传感器扫描率。       |
| `supportedScanRates` | `number[]` | 支持的传感器扫描率列表。 |

调用方式：

```ts
const scan = await client.globalSetting.getSensorScan();
```

调用示例：

```ts
const scan = await client.globalSetting.getSensorScan();
console.log(scan.currentScanRate, scan.supportedScanRates);
```

## `client.globalSetting.setSensorScan(scanRate)`

作用：写入传感器扫描率。

传参：

| 参数       | 类型     | 必填 | 说明                                                                                  |
| ---------- | -------- | ---- | ------------------------------------------------------------------------------------- |
| `scanRate` | `number` | 是   | 要写入的传感器扫描率。建议使用 `getSensorScan()` 返回的 `supportedScanRates` 中的值。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用方式：

```ts
const ok = await client.globalSetting.setSensorScan(scanRate);
```

调用示例：

```ts
const scan = await client.globalSetting.getSensorScan();
await client.globalSetting.setSensorScan(scan.supportedScanRates[0]);
```

## `client.globalSetting.getPerformanceMode()`

作用：读取性能模式。

传参：无。

返回值：`Promise<GlobalFeaturePerformanceModeParam>`。

返回字段：

| 字段   | 类型     | 说明             |
| ------ | -------- | ---------------- |
| `mode` | `number` | 当前性能模式值。 |

调用方式：

```ts
const performance = await client.globalSetting.getPerformanceMode();
```

调用示例：

```ts
const performance = await client.globalSetting.getPerformanceMode();
console.log(performance.mode);
```

## `client.globalSetting.setPerformanceMode(mode)`

作用：写入性能模式。

传参：

| 参数   | 类型     | 必填 | 说明         |
| ------ | -------- | ---- | ------------ |
| `mode` | `number` | 是   | 性能模式值。 |

返回值：`Promise<GlobalFeaturePerformanceModeParam>`，返回设备确认后的模式。

调用方式：

```ts
const result = await client.globalSetting.setPerformanceMode(mode);
```

调用示例：

```ts
const result = await client.globalSetting.setPerformanceMode(1);
console.log(result.mode);
```

## `client.globalSetting.getSleepTime()`

作用：读取睡眠时间设置。

传参：无。

返回值：`Promise<GlobalFeatureSleepTimeParam>`。

返回字段：

| 字段         | 类型     | 说明             |
| ------------ | -------- | ---------------- |
| `sleepTime1` | `number` | 第一段睡眠时间。 |
| `sleepTime2` | `number` | 第二段睡眠时间。 |

调用方式：

```ts
const sleep = await client.globalSetting.getSleepTime();
```

调用示例：

```ts
const sleep = await client.globalSetting.getSleepTime();
console.log(sleep.sleepTime1, sleep.sleepTime2);
```

## `client.globalSetting.setSleepTime(param)`

作用：写入睡眠时间设置。

传参：

| 参数               | 类型     | 必填 | 说明             |
| ------------------ | -------- | ---- | ---------------- |
| `param.sleepTime1` | `number` | 是   | 第一段睡眠时间。 |
| `param.sleepTime2` | `number` | 是   | 第二段睡眠时间。 |

返回值：`Promise<GlobalFeatureSleepTimeParam>`，返回设备确认后的睡眠时间设置。

调用方式：

```ts
const result = await client.globalSetting.setSleepTime(param);
```

调用示例：

```ts
await client.globalSetting.setSleepTime({
  sleepTime1: 60,
  sleepTime2: 300,
});
```

## 新增全局设置方法

### `client.globalSetting.getKeyDebounceTime()`

作用：读取按键消抖时间。
传参：无。
返回值：`Promise<GlobalFeatureKeyDebounceTimeParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `debounceTime` | `number` | 当前按键消抖时间，单位 ms。 |

调用示例：

```ts
const debounce = await client.globalSetting.getKeyDebounceTime();
console.log(debounce.debounceTime);
```

### `client.globalSetting.setKeyDebounceTime(debounceTime)`

作用：写入按键消抖时间。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `debounceTime` | `number` | 是 | 按键消抖时间，单位 ms。0~10ms |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用示例：

```ts
const ok = await client.globalSetting.setKeyDebounceTime(5);
```

### `client.globalSetting.getLODHeight()`

作用：读取 LOD 高度档位。
传参：无。
返回值：`Promise<GlobalFeatureLODHeightParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `lodHeight` | `number` | 当前 LOD 档位。 |

调用示例：

```ts
const lod = await client.globalSetting.getLODHeight();
console.log(lod.lodHeight);
```

### `client.globalSetting.setLODHeight(lodHeight)`

作用：写入 LOD 高度档位。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `lodHeight` | `number` | 是 | LOD 档位: `0` 表示0.7mm，`1` 表示1mm, `2` 表示2mm。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用示例：

```ts
const ok = await client.globalSetting.setLODHeight(1);
```

### `client.globalSetting.getStraightLineCorrection()`

作用：读取直线修正模式。
传参：无。
返回值：`Promise<GlobalFeatureStraightLineCorrectionParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `mode` | `number` | 当前状态，`0` 表示关闭，`1` 表示开启。 |

调用示例：

```ts
const correction = await client.globalSetting.getStraightLineCorrection();
console.log(correction.mode);
```

### `client.globalSetting.setStraightLineCorrection(mode)`

作用：写入直线修正模式。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `mode` | `number` | 是 | `0` 表示关闭，`1` 表示开启。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用示例：

```ts
const ok = await client.globalSetting.setStraightLineCorrection(1);
```

### `client.globalSetting.getBattery()`

作用：读取当前电量百分比。
传参：无。
返回值：`Promise<GlobalFeatureBatteryParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `batteryPercentage` | `number` | 当前电量百分比。 |

调用示例：

```ts
const battery = await client.globalSetting.getBattery();
console.log(battery.batteryPercentage);
```

### `client.globalSetting.getMotorVibrationStrength(key)`

作用：读取指定键位的马达震动强度档位。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `key` | `number` | 是 | 要查询的键位。 |

返回值：`Promise<GlobalFeatureMotorVibrationParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `key` | `number` | 当前查询的键位。 |
| `strengthLevel` | `number` | 当前强度档位。 |
| `supportedLevelCount` | `number` | 支持的档位数量。 |
| `triggerMode` | `number` | 触发方式，`0` 按下触发，`1` 抬起触发，`2` 按下和抬起均触发。 |

调用示例：

```ts
const vibration = await client.globalSetting.getMotorVibrationStrength(1);
console.log(vibration.strengthLevel, vibration.triggerMode);
```

### `client.globalSetting.setMotorVibrationStrength(param)`

作用：写入指定键位的马达震动强度档位。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `param.key` | `number` | 是 | 要设置的键位。 |
| `param.strengthLevel` | `number` | 是 | 强度档位。 |
| `param.triggerMode` | `number` | 是 | 触发方式，`0` 按下触发，`1` 抬起触发，`2` 按下和抬起均触发。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用示例：

```ts
const ok = await client.globalSetting.setMotorVibrationStrength({
  key: 1,
  strengthLevel: 2,
  triggerMode: 0,
});
```

### `client.globalSetting.getHighPerformance20KScanMode()`

作用：读取 20K 高性能帧扫描模式。
传参：无。
返回值：`Promise<GlobalFeatureHighPerformance20KScanModeParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `mode` | `number` | 当前状态，`0` 表示关闭，`1` 表示开启。 |

调用示例：

```ts
const mode = await client.globalSetting.getHighPerformance20KScanMode();
console.log(mode.mode);
```

### `client.globalSetting.setHighPerformance20KScanMode(mode)`

作用：写入 20K 高性能帧扫描模式。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `mode` | `number` | 是 | `0` 表示关闭，`1` 表示开启。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用示例：

```ts
const ok = await client.globalSetting.setHighPerformance20KScanMode(1);
```

### `client.globalSetting.getSensorFrameSyncMode()`

作用：读取传感器帧同步模式。
传参：无。
返回值：`Promise<GlobalFeatureSensorFrameSyncModeParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `mode` | `number` | 当前状态，`0` 表示关闭，`1` 表示开启。 |

调用示例：

```ts
const mode = await client.globalSetting.getSensorFrameSyncMode();
console.log(mode.mode);
```

### `client.globalSetting.setSensorFrameSyncMode(mode)`

作用：写入传感器帧同步模式。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `mode` | `number` | 是 | `0` 表示关闭，`1` 表示开启。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用示例：

```ts
const ok = await client.globalSetting.setSensorFrameSyncMode(1);
```

### `client.globalSetting.getDPILightEffect()`

作用：读取 DPI 档位灯效颜色。
传参：无。
返回值：`Promise<GlobalFeatureDPILightEffectParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `currentDPIStepIndex` | `number` | 当前 DPI 档位索引。 |
| `supportedDPIColorCount` | `number` | 支持的 DPI 档位颜色数量。 |
| `dpiColors` | `string[]` | DPI 档位灯效颜色列表，格式为 `#RRGGBB`。 |

调用示例：

```ts
const dpiLight = await client.globalSetting.getDPILightEffect();
console.log(dpiLight.currentDPIStepIndex, dpiLight.dpiColors);
```

### `client.globalSetting.setDPILightEffect(param)`

作用：写入指定 DPI 档位的灯效颜色。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `param.currentDPIStepIndex` | `number` | 是 | 要设置颜色的 DPI 档位索引。 |
| `param.dpiColor` | `string` | 是 | 要写入的颜色，格式为 `#RRGGBB`。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用示例：

```ts
const ok = await client.globalSetting.setDPILightEffect({
  currentDPIStepIndex: 1,
  dpiColor: '#32ff39',
});
```

### `client.globalSetting.getSensorAngle()`

作用：读取传感器角度。
传参：无。
返回值：`Promise<GlobalFeatureSensorAngleParam>`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `angle` | `number` | 当前传感器角度，范围按设备协议为 `-30` 到 `30` 度。 |

调用示例：

```ts
const sensorAngle = await client.globalSetting.getSensorAngle();
console.log(sensorAngle.angle);
```

### `client.globalSetting.setSensorAngle(angle)`

作用：设置传感器角度。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `angle` | `number` | 是 | 要设置的传感器角度，范围按设备协议为 `-30` 到 `30` 度。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。

调用示例：

```ts
const ok = await client.globalSetting.setSensorAngle(-10);
```

### `client.globalSetting.getRadioFrequencyMode()`

作用：读取射频模式。
传参：无。
返回值：`Promise<GlobalFeatureRadioFrequencyModeParam>`。
协议功能：`GlobalFeature.RadioFrequencyModeSetting = 0x12`，读写位为 `Read`。

返回字段：
| 字段 | 类型 | 说明 |
| --- | --- | --- |
| `mode` | `number` | 当前射频模式，`0` 表示智能射频，`1` 表示满格射频。 |

调用方式：

```ts
const rfMode = await client.globalSetting.getRadioFrequencyMode();
```

调用示例：

```ts
const rfMode = await client.globalSetting.getRadioFrequencyMode();
console.log(rfMode.mode);
```

### `client.globalSetting.setRadioFrequencyMode(mode)`

作用：设置射频模式。
传参：
| 参数 | 类型 | 必填 | 说明 |
| --- | --- | --- | --- |
| `mode` | `number` | 是 | `0` 表示智能射频，`1` 表示满格射频。 |

返回值：`Promise<boolean>`，设备返回成功码时为 `true`。
协议功能：`GlobalFeature.RadioFrequencyModeSetting = 0x12`，读写位为 `Write`。

调用方式：

```ts
const ok = await client.globalSetting.setRadioFrequencyMode(mode);
```

调用示例：

```ts
const ok = await client.globalSetting.setRadioFrequencyMode(1);
```
