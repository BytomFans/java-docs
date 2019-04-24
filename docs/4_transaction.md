---
id: transaction
title: Transaction API
sidebar_label: Bytom.Transaction.API
---

## get-transaction

按transaction ID查询与帐户相关的事务。

#### 参数

- `String` - *tx_id*, 交易 id, 交易hash.

#### 返回

- `String` - *tx_id*, 交易id, 交易hash.
- `Integer` - *block_time*, 响应请求时的unix时间戳.
- `String` - *block_hash*, 交易所在区块的hash值.
- `Integer` - *block_height*, 交易所在的区块高度.
- `Integer` - *block_index*, 交易所在区块的位置.
- `Integer` - *block_transactions_count*, 此区块中的所有交易.
- `Boolean` - *status_fail*, 交易请求的状态是否失败.
- `Integer` - *size*, 交易占的内存大小.
- `Array of Object` -  *inputs* , 交易的输入对象.
  - `String` - *type*, 输入类型,可选用的选项包括: 'spend'(), 'issue'(), 'coinbase'().
  - `String` - *asset_id*, 资产id.
  - `String` - *asset_alias*, 资产名字.
  - `Object` - *asset_definition*, 定义资产(json对象).
  - `Integer` - *amount*, 资产数量.
  - `Object` - *issuance_program*, 发行程序, 它仅仅当类型为'issue'时存在.
  - `Object` - *control_program*, 账户控制程序, 它仅仅存在当交易类型为'spend'时.
  - `String` - *address*, 账户地址, 它仅仅存在当交易类型为'spend'时.
  - `String` - *spent_output_id*, 在输入中前一笔交易的输出ID将被花费, 它仅仅存在当交易类型为'spend'时.
  - `String` - *account_id*, 账户id.
  - `String` - *account_alias*, 账户名称.
  - `Object` - *arbitrary*, 矿工可以设置任意信息, 只有当交易类型为 'coinbase'时存在.
- `Array of Object` - *outputs*, 交易的输出对象.
  - `String` - *type*, 输出动作类型, 可用选项包括: 'retire', 'control'.
  - `String` - *id*, 与utxo相关的输出id.
  - `Integer` - *position*, 交易输出的位置.
  - `String` - *asset_id*, 资产id.
  - `String` - *asset_alias*, 资产名称.
  - `Object` - *asset_definition*, 资产的定义(json对象).
  - `Integer` - *amount*, 资产数量.
  - `String` - *account_id*, 账户id.
  - `String` - *account_alias*, 账户名称.
  - `Object` - *control_program*, 账户的控制程序.
  - `String` - *address*, 账户地址.

#### 例子

```java
Client client = TestUtils.generateClient();
Transaction.QueryBuilder builder = new Transaction.QueryBuilder();
builder.setAccountId("0ER7MEFGG0A02");
Transaction tx = builder.get(client);
```

```js
// Result
{
  "block_hash": "1fa9bb389cf974a9b37b63ca38c0cf3453c30f394b9e8ae7f04f2d1b52c329b4",
  "block_height": 530,
  "block_index": 1,
  "block_time": 1528772056,
  "block_transactions_count": 2,
  "inputs": [
    {
      "account_alias": "default",
      "account_id": "0ER7MEFGG0A02",
      "address": "sm1q4pkg8msjumtep7ecsdzuct3tsuzk5pmnm3p8nr",
      "amount": 41250000000,
      "asset_alias": "BTM",
      "asset_definition": {
        "decimals": 8,
        "description": "Bytom Official Issue",
        "name": "BTM",
        "symbol": "BTM"
      },
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "0014a86c83ee12e6d790fb388345cc2e2b87056a0773",
      "spent_output_id": "002025b727148d04197cc7b9cf7eafd9986041f07641ca82dc0a1d9e227b52f6",
      "type": "spend"
    }
  ],
  "outputs": [
    {
      "account_alias": "default",
      "account_id": "0ER7MEFGG0A02",
      "address": "sm1qmt6jxrr8etssufr8qp98emyaly3lknxyndh5cj",
      "amount": 29450000000,
      "asset_alias": "BTM",
      "asset_definition": {
        "decimals": 8,
        "description": "Bytom Official Issue",
        "name": "BTM",
        "symbol": "BTM"
      },
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "0014daf5230c67cae10e2467004a7cec9df923fb4cc4",
      "id": "35a46dd36eb27b1ffdfdefbe5366175b6325e8f56e5bc3dd2aa1a47197e26e6c",
      "position": 0,
      "type": "control"
    },
    {
      "account_alias": "alice",
      "account_id": "0ER7OAK400A02",
      "address": "sm1qxe4jwhkekgnxkezu7xutu5gqnnpmyc8ppq98me",
      "amount": 11700000000,
      "asset_alias": "BTM",
      "asset_definition": {
        "decimals": 8,
        "description": "Bytom Official Issue",
        "name": "BTM",
        "symbol": "BTM"
      },
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "0014366b275ed9b2266b645cf1b8be51009cc3b260e1",
      "id": "ae791bbde0cc5b370e28a505933b85082d67be8db81bdcc56b8202f200b883e7",
      "position": 1,
      "type": "control"
    }
  ],
  "size": 332,
  "status_fail": false,
  "tx_id": "15b8d66e227feff47b3de0f278934ea16d6c828371ec6c13c8f84713dd11703b"
}
```

## list-transactions

返回所有与帐户相关的事务的列表。

#### 参数

`Object`:

可选:

- `String` - *id*, 交易id,交易hash.
- `String` - *account_id*, 账户id.
- `Boolean` - *detail* , 详细事务标志，默认为false（仅返回事务摘要).
- `Boolean` - *unconfirmed*, 确认事务的标志（查询结果包括所有已确认和未确认的事务），默认为false.

####  返回

- `Array of Object`, 交易数组.

可选:

- `Object`:(交易汇总)
  - `String` - *tx_id*, 交易id,交易hash.
  - `Integer` - *block_time*, 响应请求时的unix时间戳.
  - `Array of Object`- *inputs*, 交易的主要输入对象.
    - `String` - *type*, 输入操作的类型，可用选项包括：'spend'，'issue'，'coinbase'.
    - `String` - *asset_id*, 资产id.
    - `String` - *asset_alias*, 资产名称.
    - `Integer` - *amount*, 资产数量.
    - `String` - *account_id*, 账户id.
    - `String` - *account_alias*, 账户名字.
    - `Object` - *arbitrary*, arbitrary infomation can be set by miner, it only exist when type is 'coinbase'.

  - `Array of Object`- *outputs*, object of summary outputs for the transaction.
    - `String` - *type*, the type of output action, available option include: 'retire', 'control'.
    - `String` - *asset_id*, 资产id.
    - `String` - *asset_alias*, 资产名字.
    - `Integer` - *amount*, 资产数量.
    - `String` - *account_id*, 账户id.
    - `String` - *account_alias*, 账户名字.
    - `Object` - *arbitrary*, 矿工可以设置任意信息, 它仅存在当交易的输入类型'coinbase'(其他类型默认为空).
- `Object`:(交易详情)
  - `String` - *tx_id*, 交易id, 交易hash.
  - `Integer` - *block_time*, 请求的时间戳.
  - `String` - *block_hash*, 交易所在区块的hash.
  - `Integer` - *block_height*, 交易所在的区块高度.
  - `Integer` - *block_index*, 交易所在区块的索引.
  - `Integer` - *block_transactions_count*, 计算区块中的总交易笔数.
  - `Boolean` - *status_fail*, 交易的请求状态是否失败.
  - `Integer` - *size*, 交易所占内存大小.
  - `Array of Object` - *inputs*, 交易的输入对象.
    - `String` - *type*, the type of input action, available option include: 'spend', 'issue', 'coinbase'.
    - `String` - *asset_id*, 资产id.
    - `String` - *asset_alias*, 资产名字.
    - `Object` - *asset_definition*, 资产定义(json对象).
    - `Integer` - *amount*, 资产数量.
    - `Object` - *issuance_program*, issuance program, it only exist when type is 'issue'.
    - `Object` - *control_program*, control program of account, it only exist when type is 'spend'.
    - `String` - *address*, 帐户地址，仅当类型为“花费”时才存在.
    - `String` - *spent_output_id*, the front of outputID to be spent in this input, it only exist when type is 'spend'.
    - `String` - *account_id*, 账户id.
    - `String` - *account_alias*, 账户名字.
    - `Object` - *arbitrary*, 矿工可以设置任意信息, 它仅存在当交易的输入类型'coinbase'.
 - `Array of Object` - *outputs*, 交易的输出对象.
    - `String` - *type*, 输出动作的类型,可用选项包括：’retire‘，’control‘.
    - `String` - *id*, 与utxo相关的输出id.
    - `Integer` - *position*, 输出的位置.
    - `String` - *asset_id*, 资产id.
    - `String` - *asset_alias*, 资产名称.
    - `Object` - *asset_definition*, 资产的定义(json 对象).
    - `Integer` - *amount*, 资产数量.
    - `String` - *account_id*, 账户id.
    - `String` - *account_alias*, 账户名字.
    - `Object` - *control_program*, 账户的控制程序.
    - `String` - *address*, 账户地址.

#### 例子

列出所有可用的交易：
```java
Client client = TestUtils.generateClient();
Transaction.QueryBuilder transaction = new Transaction.QueryBuilder();
List<Transaction> transactionList = transaction.list(client);
```

```js
// Result
[
  {
    "block_time": 1521771059,
    "inputs": [
      {
        "arbitrary": "06",
        "asset_id": "0000000000000000000000000000000000000000000000000000000000000000",
        "type": "coinbase"
      }
    ],
    "outputs": [
      {
        "account_alias": "default",
        "account_id": "0BMHBOBVG0A02",
        "amount": 41250000000,
        "asset_alias": "BTM",
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "type": "control"
      }
    ],
    "tx_id": "c631a8de401913a512c338bcf4a61cb2de6cede12a7385d9d11637eaa6578f33"
  },
  {
    "block_time": 1521770515,
    "inputs": [
      {
        "account_alias": "default",
        "account_id": "0BMHBOBVG0A02",
        "amount": 41250000000,
        "asset_alias": "BTM",
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "type": "spend"
      }
    ],
    "outputs": [
      {
        "account_alias": "default",
        "account_id": "0BMHBOBVG0A02",
        "amount": 34649500000,
        "asset_alias": "BTM",
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "type": "control"
      },
      {
        "account_alias": "alice",
        "account_id": "0BMHDI1P00A04",
        "amount": 6600000000,
        "asset_alias": "BTM",
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "type": "control"
      }
    ],
    "tx_id": "1151ce5c7b32b8755b5e48109ec7ed956fb1783eaea9558bf5a2ad957825e4b7"
  }
]
```
列出与给定tx_id匹配的事务详细信息：
```js
// Result
[
  {
    "block_hash": "1b2d0efa025256603e9330273d37f5a900cd3dfb213e015ac53cf645e2315a6d",
    "block_height": 72,
    "block_index": 1,
    "block_time": 1528528584,
    "block_transactions_count": 2,
    "inputs": [
      {
        "account_alias": "default",
        "account_id": "0ER7MEFGG0A02",
        "address": "sm1q4pkg8msjumtep7ecsdzuct3tsuzk5pmnm3p8nr",
        "amount": 41250000000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "0014a86c83ee12e6d790fb388345cc2e2b87056a0773",
        "spent_output_id": "0072a2c1cee30a7c7b7b006ca08a48c2b479bc81c0ec6463fe4865ef37626ab6",
        "type": "spend"
      }
    ],
    "outputs": [
      {
        "account_alias": "default",
        "account_id": "0ER7MEFGG0A02",
        "address": "sm1qskj096x5w7ejcmk746g3djmv84dpxts62dewvd",
        "amount": 34649500000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "001485a4f2e8d477b32c6edeae9116cb6c3d5a132e1a",
        "id": "b08c9bfc816064ca33da8b569998229774fc9552da7d4f16870b2c5a8f645b3b",
        "position": 0,
        "type": "control"
      },
      {
        "account_alias": "alice",
        "account_id": "0ER7OAK400A02",
        "address": "sm1qxe4jwhkekgnxkezu7xutu5gqnnpmyc8ppq98me",
        "amount": 6600000000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "0014366b275ed9b2266b645cf1b8be51009cc3b260e1",
        "id": "0e8f8dc83a39b2b6d00a77759a797102d047f82f800fe21f5b1d80bb4d5e2e39",
        "position": 1,
        "type": "control"
      }
    ],
    "size": 333,
    "status_fail": false,
    "tx_id": "7e9f9b999381da936e3cae48b5bac2b9bc28bb56c6c862be6c110448f7e2f6b3"
  }
]
```

列出与给定account_id和未确认标志匹配的标签（未确认标签的block_hash，block_height和block_index默认为零）：

```js
// Result
[
  {
    "block_hash": "0000000000000000000000000000000000000000000000000000000000000000",
    "block_height": 0,
    "block_index": 0,
    "block_time": 1529032899,
    "inputs": [
      {
        "account_alias": "default",
        "account_id": "0F1L5Q3V00A02",
        "address": "sm1ql67n04pj8mfqzv3wjq8num3yrltdykemgrr45j",
        "amount": 41250000000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "0014febd37d4323ed201322e900f3e6e241fd6d25b3b",
        "spent_output_id": "00570443cbac4f68638ff565e8b04db2062800b9e23b7701913ddf6b190dbe65",
        "type": "spend"
      },
      {
        "account_alias": "default",
        "account_id": "0F1L5Q3V00A02",
        "address": "sm1ql67n04pj8mfqzv3wjq8num3yrltdykemgrr45j",
        "amount": 41250000000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "0014febd37d4323ed201322e900f3e6e241fd6d25b3b",
        "spent_output_id": "01df9011ca0bed4bb9b95dc84da4c5103fed06ca28c03d92d34ee3d61b945288",
        "type": "spend"
      }
    ],
    "outputs": [
      {
        "account_alias": "default",
        "account_id": "0F1L5Q3V00A02",
        "address": "sm1qdcfprk7wjy6flavkzhcjh3dxyrwlm935trrs5m",
        "amount": 41249100000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "00146e1211dbce91349ff59615f12bc5a620ddfd9634",
        "id": "09fabb1a2bac44c45054175453e23e81a764557147523d8df70d8a190cf2eb17",
        "position": 0,
        "type": "control"
      },
      {
        "account_alias": "default",
        "account_id": "0F1L5Q3V00A02",
        "address": "sm1qt92xx2f4ys63dyhy58jle87nttcf37zftweklh",
        "amount": 39150000000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "0014595463293524351692e4a1e5fc9fd35af098f849",
        "id": "6efae48663e872193e8a672eb85b8bbf29d8aee98e42816340fa0b2340cc355d",
        "position": 1,
        "type": "control"
      },
      {
        "account_alias": "alice",
        "account_id": "0F1MQVI500A02",
        "address": "sm1qum6ly8aq9u9k7xrkuck9pq64xg67gw40khnnxu",
        "amount": 2100000000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "0014e6f5f21fa02f0b6f1876e62c5083553235e43aaf",
        "id": "aca1ecc59d8bcf548e4f5afb8a97e38f0eb56e1387b17400fd3c693c074a703d",
        "position": 2,
        "type": "control"
      }
    ],
    "size": 1194,
    "status_fail": false,
    "tx_id": "9c28a6a2a039ed5bdebe81eea44cdb22a951c472bc25cb1e8188ae423a98f251"
  },
  {
    "block_hash": "474b9c28b225fba02278ad3b097d561bf8f5c562ff2a548226fc10fc1d75b7ed",
    "block_height": 255,
    "block_index": 1,
    "block_time": 1528963126,
    "block_transactions_count": 2,
    "inputs": [
      {
        "account_alias": "alice",
        "account_id": "0F1MQVI500A02",
        "address": "sm1qum6ly8aq9u9k7xrkuck9pq64xg67gw40khnnxu",
        "amount": 10000000000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "0014e6f5f21fa02f0b6f1876e62c5083553235e43aaf",
        "spent_output_id": "767649aafdfe2c22d46d641a5b74d934e2590330f7280b0fc55b978812a99a58",
        "type": "spend"
      },
      {
        "account_alias": "alice",
        "account_id": "0F1MQVI500A02",
        "address": "sm1qum6ly8aq9u9k7xrkuck9pq64xg67gw40khnnxu",
        "amount": 1000000000000,
        "asset_alias": "GOLD",
        "asset_definition": {
          "decimals": 8,
          "description": {},
          "name": "",
          "symobol": ""
        },
        "asset_id": "71deb74415f16a1f7bffb04c61d427bb1f93adfba257ffba2673f102d602e78f",
        "control_program": "0014e6f5f21fa02f0b6f1876e62c5083553235e43aaf",
        "spent_output_id": "5d7a88851f5696ded279cb9bc380e050024c555258ea7851dfdedc2797b0d820",
        "type": "spend"
      }
    ],
    "outputs": [
      {
        "account_alias": "alice",
        "account_id": "0F1MQVI500A02",
        "address": "sm1q39sztlh4jq5nknstn2udvvpm6v5ugussx2djc0",
        "amount": 9980000000,
        "asset_alias": "BTM",
        "asset_definition": {
          "decimals": 8,
          "description": "Bytom Official Issue",
          "name": "BTM",
          "symbol": "BTM"
        },
        "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
        "control_program": "0014896025fef590293b4e0b9ab8d6303bd329c47210",
        "id": "2b44969d28d79544006e792411d6cd1d245f9af20419f6138494b4b5aac2a72e",
        "position": 0,
        "type": "control"
      },
      {
        "account_alias": "alice",
        "account_id": "0F1MQVI500A02",
        "address": "sm1q258yd0gvatje4pn0qc8z9w8cdv45j9tvhfpjh8",
        "amount": 999999999901,
        "asset_alias": "GOLD",
        "asset_definition": {
          "decimals": 8,
          "description": {},
          "name": "",
          "symobol": ""
        },
        "asset_id": "71deb74415f16a1f7bffb04c61d427bb1f93adfba257ffba2673f102d602e78f",
        "control_program": "0014550e46bd0ceae59a866f060e22b8f86b2b49156c",
        "id": "54be1bc876d1deccb9845acec79eabf62d7eacd5935e337850233657914d0f9d",
        "position": 1,
        "type": "control"
      },
      {
        "amount": 99,
        "asset_alias": "GOLD",
        "asset_definition": {
          "decimals": 8,
          "description": {},
          "name": "",
          "symobol": ""
        },
        "asset_id": "71deb74415f16a1f7bffb04c61d427bb1f93adfba257ffba2673f102d602e78f",
        "control_program": "20e864761d8181103b6476435a805cba97361df9a05c40fae644c27f69ce045d3c16001464d928e181900d382fa33def66534c7323c778c4015820684d6683d014abb4e019878b50fbbb547bcbf9c4739498d8eeef565d37f9a82f741a547a6413000000007b7b51547ac1631a000000547a547aae7cac00c0",
        "id": "347553923bb550c236a703e46600d53f25161e3eb74ee3183884d398e5d894b0",
        "position": 2,
        "type": "control"
      }
    ],
    "size": 691,
    "status_fail": false,
    "tx_id": "383f8636842301b2fe292c5b8b2f540c6ed7867ba5751680b2e77827c300e41e"
  }
]
```
## build-transaction
建立交易。

#### 参数

- `String` - *base_transaction*, 交易基本数据, 默认为空.
- `Integer` - *ttl*,时间，单位为秒.
- `Integer` - *time_range*，时间戳.
- `Arrary of Object` - *actions* :
    - `String` - *account_id* | *account_alias*, 别名或帐户ID.
    - `String` - *asset_id* | *asset_alias*, 资产的别名或ID.
    - `Integer` - *amount*, 与此交易一起发送的金额的指定资产.
    - `String`- *type*,交易类型, 有效类型包括: 'spend_account', 'issue', 'spend_account_unspent_output', 'control_address', 'control_program', 'retire'.
    - `String` - *address*,  接收者地址（类型为 control_address）地址类型为P2PKH或P2SH.
    - `String` - *control_program*, (type is control_program) control program of receiver.

#### 返回
- `Object of build-transaction` -  *transaction*, 构建好的交易..
#### 例子
```java
Client client = TestUtils.generateClient();
Transaction.Template controlAddress = new Transaction.Builder()
    .addAction(
    new Transaction.Action.SpendFromAccount()
    .setAccountId(senderAccount.id)
    .setAssetId(senderAsset.id)
    .setAmount(300000000)
	)
    .addAction(
    new Transaction.Action.ControlWithAddress()
    .setAddress(receiverAddress.address)
    .setAssetId(senderAsset.id)
    .setAmount(200000000)
	).build(client);
```
```js
//Result示例
{
  "allow_additional_actions": false,
  "local": true,
  "raw_transaction": "07010000020161015fb6a63a3361170afca03c9d5ce1f09fe510187d69545e09f95548b939cd7fffa3ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff80fc93afdf01000116001426bd1b851cf6eb8a701c20c184352ad8720eeee90100015d015bb6a63a3361170afca03c9d5ce1f09fe510187d69545e09f95548b939cd7fffa33152a15da72be51b330e1c0f8e1c0db669269809da4f16443ff266e07cc43680c03e0101160014489a678741ccc844f9e5c502f7fac0a665bedb25010003013effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff80a2cfa5df0101160014948fb4f500e66d20fbacb903fe108ee81f9b6d9500013a3152a15da72be51b330e1c0f8e1c0db669269809da4f16443ff266e07cc43680dd3d01160014cd5a822b34e3084413506076040d508bb12232c70001393152a15da72be51b330e1c0f8e1c0db669269809da4f16443ff266e07cc436806301160014a3f9111f3b0ee96cbd119a3ea5c60058f506fb1900",
  "signing_instructions": [
    {
      "position": 0,
      "witness_components": [
        {
          "keys": [
            {
              "derivation_path": [
                "010100000000000000",
                "0500000000000000"
              ],
              "xpub": "ee9dd8affdef7e0cacd0fbbf310217c7f588156c28e414db74c27afaedd8f876cf54547a672b431ff06ee8a146207df9595638a041b55ada1a764a8b5b30bda0"
            }
          ],
          "quorum": 1,
          "signatures": null,
          "type": "raw_tx_signature"
        },
        {
          "type": "data",
          "value": "62a73b6b7ffe52b6ad782b0e0efdc8309bf2f057d88f9a17d125e41bb11dbb88"
        }
      ]
    },
    {
      "position": 1,
      "witness_components": [
        {
          "keys": [
            {
              "derivation_path": [
                "010100000000000000",
                "0600000000000000"
              ],
              "xpub": "ee9dd8affdef7e0cacd0fbbf310217c7f588156c28e414db74c27afaedd8f876cf54547a672b431ff06ee8a146207df9595638a041b55ada1a764a8b5b30bda0"
            }
          ],
          "quorum": 1,
          "signatures": null,
          "type": "raw_tx_signature"
        },
        {
          "type": "data",
          "value": "ba5a63e7416caeb945eefc2ce874f40bc4aaf6005a1fc792557e41046f7e502f"
        }
      ]
    }
  ]
}
```

## sign-transaction

签署交易。

#### 参数

`Object`:

- `String` - *password*, 密码签名.
- `Object` - *transaction*, 构建好的交易.

#### 返回

`Object`:

- `Boolean` - *sign_complete*, 如果签名成功返回true,false签名不成功.
- `Object of sign-transaction` - *transaction*, 交易签名.

#### 例子

```java
Transaction.Template singer = new Transaction.SignerBuilder().sign(client,controlAddress, "123456");
```

```js
// Result
{
  "sign_complete": true,
  "transaction": {
    "allow_additional_actions": false,
    "local": true,
    "raw_transaction": "07010000020161015fb6a63a3361170afca03c9d5ce1f09fe510187d69545e09f95548b939cd7fffa3ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff80fc93afdf01000116001426bd1b851cf6eb8a701c20c184352ad8720eeee96302400d432e6f0e22da3168d76552273e60d23d432d61b4dac53e6769d39a1097f1cd1bd8e54c7d39eda334803e5c904bc2de2f27ff29748166e0334dcfded20e980b2062a73b6b7ffe52b6ad782b0e0efdc8309bf2f057d88f9a17d125e41bb11dbb88015d015bb6a63a3361170afca03c9d5ce1f09fe510187d69545e09f95548b939cd7fffa33152a15da72be51b330e1c0f8e1c0db669269809da4f16443ff266e07cc43680c03e0101160014489a678741ccc844f9e5c502f7fac0a665bedb256302401eadd84ad07c3643f71a35cc5669a2c1def96ae98e790d287217e6a3543fe602dd90afffe853c729bd5237a28f33538df631572847d9870829fb1fd1100ff20820ba5a63e7416caeb945eefc2ce874f40bc4aaf6005a1fc792557e41046f7e502f03013effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff80a2cfa5df0101160014948fb4f500e66d20fbacb903fe108ee81f9b6d9500013a3152a15da72be51b330e1c0f8e1c0db669269809da4f16443ff266e07cc43680dd3d01160014cd5a822b34e3084413506076040d508bb12232c70001393152a15da72be51b330e1c0f8e1c0db669269809da4f16443ff266e07cc436806301160014a3f9111f3b0ee96cbd119a3ea5c60058f506fb1900",
    "signing_instructions": [
      {
        "position": 0,
        "witness_components": [
          {
            "keys": [
              {
                "derivation_path": [
                  "010100000000000000",
                  "0500000000000000"
                ],
                "xpub": "ee9dd8affdef7e0cacd0fbbf310217c7f588156c28e414db74c27afaedd8f876cf54547a672b431ff06ee8a146207df9595638a041b55ada1a764a8b5b30bda0"
              }
            ],
            "quorum": 1,
            "signatures": [
              "0d432e6f0e22da3168d76552273e60d23d432d61b4dac53e6769d39a1097f1cd1bd8e54c7d39eda334803e5c904bc2de2f27ff29748166e0334dcfded20e980b"
            ],
            "type": "raw_tx_signature"
          },
          {
            "type": "data",
            "value": "62a73b6b7ffe52b6ad782b0e0efdc8309bf2f057d88f9a17d125e41bb11dbb88"
          }
        ]
      },
      {
        "position": 1,
        "witness_components": [
          {
            "keys": [
              {
                "derivation_path": [
                  "010100000000000000",
                  "0600000000000000"
                ],
                "xpub": "ee9dd8affdef7e0cacd0fbbf310217c7f588156c28e414db74c27afaedd8f876cf54547a672b431ff06ee8a146207df9595638a041b55ada1a764a8b5b30bda0"
              }
            ],
            "quorum": 1,
            "signatures": [
              "1eadd84ad07c3643f71a35cc5669a2c1def96ae98e790d287217e6a3543fe602dd90afffe853c729bd5237a28f33538df631572847d9870829fb1fd1100ff208"
            ],
            "type": "raw_tx_signature"
          },
          {
            "type": "data",
            "value": "ba5a63e7416caeb945eefc2ce874f40bc4aaf6005a1fc792557e41046f7e502f"
          }
        ]
      }
    ]
  }
}
```

## submit-transaction

提交交易。

#### 参数

- `Object` - *raw_transaction*, 已经签名好的交易.

#### 返回

- `String` - *tx_id*, 交易id 交易hash.

#### 例子
```java
Transaction.SubmitResponse txs = Transaction.submit(client, singer);
```
```js
// Result
{
  "tx_id": "2c0624a7d251c29d4d1ad14297c69919214e78d995affd57e73fbf84ece316cb"
}
```

## estimate-transaction-gas 

估计交易消耗的neu(1BTM = 10^8NEU)。

##### 参数

- `Object` - *transaction_template*, 构建交易响应.

##### 返回

- `Integer` - *total_neu*,发送交易时总共消耗的neo(1BTM = 10^8NEU),total_neu 是 storage_neu + vm_neu 四舍五入得到的.
- `Integer` - *storage_neu*, 存储交易时消耗的neu.
- `Integer` - *vm_neu*, 虚拟机执行消耗的neu.

##### 例子
```java
TransactionGas.estimateGas(Client client, Template template);
```
```bash
// Result
{
  "storage_neu": 3840000,
  "total_neu": 5259000,
  "vm_neu": 1419000
}
```

## get-unconfirmed-transaction

根据交易ID查询在缓冲池里面查询未确认的交易.

#### 参数

- `String` - *tx_id*, 交易id,交易hash.

#### 返回

- `String` - *id*, 交易id,交易hash.
- `Integer` - *version*, 交易版本.
- `Integer` - *size*, 交易大小.
- `Integer` - *time_range*, 交易的时间范围.
- `Boolean` - *status_fail*, 请求的状态是否失败.
- `String` - *mux_id*, 前一笔交易的mux id(钱包启用可以获得，这个地方是空的).
- `Array of Object` - *inputs*, 交易的输入对象(输入结构请参考get-transaction API描述).
- `Array of Object` - *outputs*, 交易输出对象(输出结构请参考get-transction API描述).

#### 例子
```java
Client client = TestUtils.generateClient();
utxResponse = UnconfirmedTransaction.list(client);
unconfirmedTransaction = UnconfirmedTransaction.get(client, utxResponse.txIds.get(0));
Assert.assertNotNull(unconfirmedTransaction);
```
```bash
// Result
{
  "id": "382090f24fbfc2f737fa7372b9d161a43f00d1c597a7130a56589d1f469d04b5",
  "inputs": [
    {
      "address": "bm1qqrm7ruecx7yrg9smtwmnmgj3umg9vcukgy5sdj",
      "amount": 41250000000,
      "asset_definition": {},
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "001400f7e1f338378834161b5bb73da251e6d0566396",
      "spent_output_id": "161b44e547a6cc68d732eb64fa38031da98211a99319e088cfe632223f9ac6d8",
      "type": "spend"
    }
  ],
  "mux_id": "0000000000000000000000000000000000000000000000000000000000000000",
  "outputs": [
    {
      "address": "bm1qehxd5cdnepckh5jc72ggn30havd78lsgcqmt7k",
      "amount": 21230000000,
      "asset_definition": {},
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "0014cdccda61b3c8716bd258f29089c5f7eb1be3fe08",
      "id": "a8f21ad24689c290634db85278f56d152efe6fe08bc194e5dee5127ed6d3ebee",
      "position": 0,
      "type": "control"
    },
    {
      "address": "bm1q2me9gwccnm3ehpnrcr99gcnj730js2zfucms3r",
      "amount": 20000000000,
      "asset_definition": {},
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "001456f2543b189ee39b8663c0ca546272f45f282849",
      "id": "78219e422ea3257aeb32f6d952b5ce5560dab1d6440c9f3aebcdaad2a852d2a8",
      "position": 1,
      "type": "control"
    }
  ],
  "size": 664,
  "status_fail": false,
  "time_range": 0,
  "version": 1
}
```

## list-unconfirmed-transactions

返回缓冲池交易的总数和交易ID列表.

#### 参数

none

#### 返回

- `Integer` - *total*, 交易版本.
- `Array of Object` - *tx_ids*, 列出所有交易id.

#### 例子
```java
Client client = TestUtils.generateClient();
utxResponse = UnconfirmedTransaction.list(client);
Assert.assertNotNull(utxResponse);
```
```bash
// Result
{
  "total": 2,
  "tx_ids": [
    "382090f24fbfc2f737fa7372b9d161a43f00d1c597a7130a56589d1f469d04b5",
    "fc2da5dfa094c2170144f149fa07a312983157aec0ec95063a1319eedcb2d23b"
  ]
}
```

## decode-raw-transaction

反序列化交易十六进制字符串为json对象.

#### 参数

- `String` - *raw_transaction*, 交易的序列化字符串.

#### 返回

- `Integer` - *version*,交易版本.
- `String` - *size*, 交易大小.
- `String` - *time_range*, 交易时间范围.
- `String` - *fee*, 发送交易的反馈.
- `Array of Object` - *inputs*, 交易的输入对象(输入结构请参考get-transaction API描述).
- `Array of Object` - *outputs*, 交易输出对象(输出结构请参考get-transction API描述).

#### 例子
```java
Client client = TestUtils.generateClient();
String rawTxId = "070100010161015f30e052cd50e385951936c08fb5642bd12b727da958960249ddad8c9a77e5371fffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff8099c4d59901000116001412a47b53b3bbdaf9f3510e1d8c19d69f81ca91426302405a8b5adebd2ab63ba1ac55a7bbadc1fe246806c37732df0442b827fa4e06058137711d9d012becdc9de507a8ad0de0dd50780c0503c0dcff2dc03d7592e31a08206e1efce70e2b29efa348aec7c148edc2beb72edc0d4422a03cfb0f40e6e4cfc602013effffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff80d3bdc6980101160014a9c0ea4abe4d09546197bac3c86f4dd39fde1afb00013cffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff8084af5f011600144cc6edb1f4077c740e0201bb3688e6efba4a098c00";
rawTransaction = RawTransaction.decode(client, rawTxId);
Assert.assertNotNull(rawTransaction);
```
```bash
// Result
{
  "fee": 20000000,
  "inputs": [
    {
      "address": "tm1q26kpwrrevhh2c8xrfy5vnaryu0ugc97c4yxp66",
      "amount": 41250000000,
      "asset_definition": {},
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "001456ac170c7965eeac1cc34928c9f464e3f88c17d8",
      "spent_output_id": "01bb3309666618a1507cb5be845b17dee5eb8028ee7e71b17d74b4dc97085bc8",
      "type": "spend"
    }
  ],
  "outputs": [
    {
      "address": "tm1qc0fjpcwuflnc06038s2xfcl2t2hfdfv06pfd70",
      "amount": 41030000000,
      "asset_definition": {},
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "0014c3d320e1dc4fe787e9f13c1464e3ea5aae96a58f",
      "id": "567b34857614d16292220beaca16ce34b939c75023a49cc43fa432fff51ca0dd",
      "position": 0,
      "type": "control"
    },
    {
      "address": "tm1qhwfumd8v5a9sdqepa6uy43wnx6rzsxm9uhmk4q",
      "amount": 200000000,
      "asset_definition": {},
      "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
      "control_program": "0014bb93cdb4eca74b068321eeb84ac5d33686281b65",
      "id": "a8069d412e48c2b2994d2816758078cff46b215421706b4bad41f72a32928d92",
      "position": 1,
      "type": "control"
    }
  ],
  "size": 332,
  "time_range": 0,
  "version": 1
}
```

