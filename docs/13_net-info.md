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
```php
BytomClient::netInfo();
```
```js
// Result
{
  "listening": true,
  "syncing": true,
  "mining": true,
  "peer_count": 0,
  "current_block": 627,
  "highest_block": 0,
  "network_id": "mainnet",
  "version": "0.5.0"
}
```