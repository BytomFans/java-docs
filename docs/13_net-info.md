---
id: net_info
title: Net_info API
sidebar_label: Bytom.New_info.API
---

## net-info

返回当前网络节点的信息。

#### 参数

none

#### 返回

`Object`:

- `Boolean` - *listening*, 节点是否正在监听.
- `Boolean` - *syncing*, 节点是否正在同步.
- `Boolean` - *mining*, 节点是否在挖矿.
- `Integer` - *peer_count*, 当前节点连接数.
- `Integer` - *current_block*, 当前节点中链的高度.
- `Integer` - *highest_block*, 当前节点的最新区块高度.
- `String` - *network_id*, 网络id.
- `String` - *version*, 比原版本.

#### 例子
```java
Client client = TestUtils.generateClient();
netInfo = CoreConfig.getNetInfo(client);
Assert.assertNotNull(netInfo);
```
```bash
// Result
{"listening":true,"syncing":false,"mining":false,"peer_count":4,"current_block":220923,"highest_block":220923,"network_id":"mainnet"}
```

