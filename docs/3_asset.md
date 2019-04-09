---
id: asset
title: Asset API
sidebar_label: Bytom.Asset.API
---

## creat-asset

创建资产定义，准备发行资产。

#### 参数

- `Array of String` - *root_xpubs*, 公钥集合
- `String` - *alias*, 资产名称
- `Integer` - *quorum*, 默认值是`1`, 交易必需签名用来支出由账户控制的资产单位的密钥阀值

可选

- `Object` - *definition*, 资产定义.
- `String` - *access_token*, 如果在本地创建资产时是可选的.但是，如果您想远程创建资产，它是必需要填写的.

#### 返回

- `String` - *id*, 资产id.
- `String` - *alias*, 资产名称.
- `String` - *issuance_program*, 资产发行控制方案.
- `Array of Object` - *keys*, 资产公钥信息.
- `String` - *definition*, 资产定义.
- `Integer` - *quorum*, 交易必需签名用来支出由账户控制的资产单位的密钥阀值.

#### 例子

```php
BytomClient::createAsset($root_xpubs = [], $alias, $quorum = 1);
```

```json
// Result
{
  "id": "3c1cf4c9436e3f942cb2f1d70a584f1c61df3697698dacccdc89e46f46a003d0",
  "alias": "GOLD",
  "issuance_program": "766baa209683b893483c0a5a317bf9868a8e2a09691f8aa8c1f3e2a7bb62b157e76712e05151ad696c00c0",
  "keys": [
    {
      "root_xpub": "f6a16704f745a168642712060e6c5a69866147e21ec2447ae628f87d756bb68cc9b91405ad0a95f004090e864fde472f62ba97053ea109837bc89d63a64040d5",
      "asset_pubkey": "9683b893483c0a5a317bf9868a8e2a09691f8aa8c1f3e2a7bb62b157e76712e012bd443fa7d56a0627df0a29dffcdc52641672a0f5cba54d104ad76ebeb8dfc3",
      "asset_derivation_path": [
        "000200000000000000"
      ]
    }
  ],
  "quorum": 1,
  "definition": {}
}
```

## get-asset

按assetID查询详细信息资产。

#### 参数

- `String` - *id*, 资产id

#### 返回

- `String` - *id*, 资产id

- `String` - *issuance_program*，资产发行控制方案，智能合约

- `Integer` - *quorum* , 交易必需签名用来支出由账户控制的资产单位的密钥阀值

- `Array of Object` - *xpubs*, 公钥数组

- `String` - *type*,资产类型

- `Integer` - *vm_version*, 虚拟机版本

- `String` - *raw_definition_byte*, 资产定义的字节

- `Object` - *definition*, 资产描述

#### 例子
```php
BytomClient::getAsset($asset_id);
```

```json
// Result
{
  "alias": "SILVER",
  "definition": null,
  "id": "50ec80b6bc48073f6aa8fa045131a71213c33f3681203b15ddc2e4b81f1f4730",
  "issue_program": "ae2029cd61d9ef31d40af7541f9a50831d6317fdb0870249d0564fcfa9a8f843589c5151ad",
  "key_index": 1,
  "quorum": 1,
  "raw_definition_byte": "",
  "type": "asset",
  "vm_version": 1,
  "xpubs": [
    "34b16ee500615cd325f8b84099f83c1ebecaca67977c5dc9b71ae32ceaf18207f996b0a9725b901d3792689b2babcb60febe3b81a684d9b56b65f67f307d453d"
  ]
}
```

## list-assets

返回所有可用资产的列表。

#### 参数

none

#### 返回

- `Array of Object`，资产数组
  - `String` - *id*，资产id
  - `String` - *alias*，资产名称
  - `String` - *issuance_program*, 资产发行控制程序
  - `Integer` - *key_index*, 公钥索引
  - `Integer` - *quorum*, 交易必需签名用来支出由账户控制的资产单位的密钥阀值
  - `Array of Object` - *xpubs*, 公钥数组
  - `String` - *type*, 资产类型
  - `Integer` - *vm_version*, 虚拟机版本
  - `String` - *raw_definition_byte*, 资产定义的字节
  - `Object` - *definition*, 资产的描述

#### 例子

```php
BytomClient::listAssets();
```

```json
// Result
[
  {
    "alias": "BTM",
    "definition": {
      "decimals": 8,
      "description": "Bytom Official Issue",
      "name": "BTM",
      "symbol": "BTM"
    },
    "id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
    "issue_program": "",
    "key_index": 0,
    "quorum": 0,
    "raw_definition_byte": "7b0a202022646563696d616c73223a20382c0a2020226465736372697074696f6e223a20224279746f6d204f6666696369616c204973737565222c0a2020226e616d65223a202262746d222c0a20202273796d626f6c223a202262746d220a7d",
    "type": "internal",
    "vm_version": 1,
    "xpubs": null
  },
  {
    "alias": "SILVER",
    "definition": null,
    "id": "50ec80b6bc48073f6aa8fa045131a71213c33f3681203b15ddc2e4b81f1f4730",
    "issue_program": "ae2029cd61d9ef31d40af7541f9a50831d6317fdb0870249d0564fcfa9a8f843589c5151ad",
    "key_index": 1,
    "quorum": 1,
    "raw_definition_byte": "",
    "type": "asset",
    "vm_version": 1,
    "xpubs": [
      "34b16ee500615cd325f8b84099f83c1ebecaca67977c5dc9b71ae32ceaf18207f996b0a9725b901d3792689b2babcb60febe3b81a684d9b56b65f67f307d453d"
    ]
  }
]
```

## update-asset-alias

按assetID更新资产别名。

#### 参数

- `String` - *id*, 资产id
- `String` - *alias*, 资产的新别名

#### 返回

如果资产别名更新成功，则为none。

##### 例子

```php
BytomClient::updateAssetAlias($asset_id, $alias);
```

```json
// Request
curl -X POST update-asset-alias -d '{"id":"50ec80b6bc48073f6aa8fa045131a71213c33f3681203b15ddc2e4b81f1f4730", "alias":"GOLD"}'

// Result
```

## list-balances

返回所有可用帐户余额的列表。

#### 参数

none

#### 返回

- `Array of Object`，账户里面所有可用的余额
    - `String` - *account_id*, 账户id
    - `String` - *account_alias*,账户名称
    - `String` - *asset_id*, 资产id
    - `String` - *asset_alias*, 资产名称
    - `Integer` - *amount*, 指定的帐户资产余额

#### 例子

列出所有可用的帐户余额。

```js
// Request
curl -X POST list-balances -d {}

// Result
[
    {
      "account_alias": "default",
      "account_id": "0BDQ9AP100A02",
      "amount": 35508000000000,
      "asset_alias": "BTM",
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
    },
    {
      "account_alias": "alice",
      "account_id": "0BDQARM800A04",
      "amount": 60000000000,
      "asset_alias": "BTM",
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"
    }
]
```

## list-unspent-outputs

返回钱包中所有帐户的所有未花费事务输出。

#### 参数

- `String` - *id*, 未花费的输出id

##### 返回

- `Array of Object`, 未花费的输出数组
    - `String` - *account_id*, 账户id
    - `String` - *account_alias*,账户名称
    - `String` - *asset_id*, 资产id
    - `String` - *asset_alias*, 资产名字
    - `Integer` - *amount*, 指定的帐户资产余额
    - `String` - *address*, 账户地址
    - `Boolean` - *change*, 账户地址是否改变
    - `String` - *id*, 未花费的输出id
    - `String` - *program*, 账户程序
    - `String` - *control_program_index*, 控制程序索引
    - `String` - *source_id*, 未花费的输出源id
    - `String` - *source_pos*, 位花费的输出源id在区块中的位置
    - `String` - *valid_height*, 有效高度

##### 例子

列出所有可用的未使用输出：
```php
BytomClient::listUnspentOutPuts($id);
```

```json
// Result
[
  {
    "account_alias": "alice",
    "account_id": "0BKBR6VR00A06",
    "address": "bm1qv3htuvug7qdv46ywcvvzytrwrsyg0swltfa0dm",
    "amount": 2000,
    "asset_alias": "GOLD",
    "asset_id": "1883cce6aab82cf9af8cd085a3115dd4a92cdb8e6a9152acd73d7ae4adb9030a",
    "change": false,
    "control_program_index": 2,
    "id": "58f29f0f85f7bd2a91088bcbe536dee41cd0642dfb1480d3a88589bdbfd642d9",
    "program": "0014646ebe3388f01acae88ec318222c6e1c0887c1df",
    "source_id": "5988c1630c1f325e69bb92cb4b19af14286aa107311bc64b8f1a54629a33e0f4",
    "source_pos": 2,
    "valid_height": 0
  },
  {
    "account_alias": "default",
    "account_id": "0BKBR2D2G0A02",
    "address": "bm1qx7ylnhszg24995d5e0nftu9e87kt9vnxcn633r",
    "amount": 624000000000,
    "asset_alias": "BTM",
    "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
    "change": false,
    "control_program_index": 12,
    "id": "5af9d3c9b69470983377c1fc0c9125c4ac3bfd32c8d505f2a6042aade8503bc9",
    "program": "00143789f9de0242aa52d1b4cbe695f0b93facb2b266",
    "source_id": "233d1dd49e591980f98e11f333c6c28a867e78448e272011f045131df5aa260b",
    "source_pos": 0,
    "valid_height": 12
  }
]
```
列出与给定id匹配的未使用的输出：
```php
$id = "58f29f0f85f7bd2a91088bcbe536dee41cd0642dfb1480d3a88589bdbfd642d9"
BytomClient::listUnspentOutPuts($id);
```
```js
// Request
curl -X POST list-unspent-outputs -d '{"id": "58f29f0f85f7bd2a91088bcbe536dee41cd0642dfb1480d3a88589bdbfd642d9"}'

// Result
{
  "account_alias": "alice",
  "account_id": "0BKBR6VR00A06",
  "address": "bm1qv3htuvug7qdv46ywcvvzytrwrsyg0swltfa0dm",
  "amount": 2000,
  "asset_alias": "GOLD",
  "asset_id": "1883cce6aab82cf9af8cd085a3115dd4a92cdb8e6a9152acd73d7ae4adb9030a",
  "change": false,
  "control_program_index": 2,
  "id": "58f29f0f85f7bd2a91088bcbe536dee41cd0642dfb1480d3a88589bdbfd642d9",
  "program": "0014646ebe3388f01acae88ec318222c6e1c0887c1df",
  "source_id": "5988c1630c1f325e69bb92cb4b19af14286aa107311bc64b8f1a54629a33e0f4",
  "source_pos": 2,
  "valid_height": 0
}
```