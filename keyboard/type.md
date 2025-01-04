# 类型查询

## getApi

```js type 目前支持类型
  // 获取协议版本
  ORDER_TYPE_PROTOCOL_VERSION

  // 读取键盘名字
  ORDER_TYPE_KEYBOARD_NAME

  // 设置回报率, h_arg / s_arg = 0[8KHz], 1[4KHz], 2[2KHz], 3[1KHz], 4[500Hz], 5[250Hz]，6[125Hz], 无效，只可用于获取当前的回报率
  ORDER_TYPE_ROES
  
   // 8bit精度+16bit最小行程度+16bit最大行程。以um为单位，如10精度(10um)为0.01mm,50精度(50um)为0.05mm。行程范围0~4000um。
  ORDER_TYPE_PRECISION_STROKE
  
  // 查询是否为 Win 模式
  ORDER_TYPE_QUERY_WIN_MODEL

  // query, 查询是否为 Mac 模式
  ORDER_TYPE_QUERY_MAC_MODEL

```
