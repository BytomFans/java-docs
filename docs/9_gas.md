---
id: gas
title: Gas_rate API
sidebar_label: Bytom.Gas.API
---

## gas-rate

gas消耗率。

#### 参数

none

#### 返回

- `Integer` - *gas_rate*, gas 费率.

##### 例子
```java
Client client = TestUtils.generateClient();
gasRate = CoreConfig.getGasRate(client);
Assert.assertNotNull(gasRate);
```
```bash
// Result
0    INFO  [2019-04-24 14:26:24]  gas-rate:
2    INFO  [2019-04-24 14:26:24]  200
```