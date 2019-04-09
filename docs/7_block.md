---
id: block
title: Block API
sidebar_label: Bytom.Block.API
---

## get-block-count

返回当前区块链的高度.

#### 参数

none

#### 返回

- `Integer` - *block_count*, 当前的区块高度.

#### 例子
```php
BytomClient::getBlockCount();
```
```js
// Result
{
    "block_count": 519
}
```

## get-block-hash

返回当前区块的hash.

#### 参数

none

#### 返回

- `String` - *block_hash*, 最近的区块hash.

#### 例子
```php
BytomClient::getBlockHash();
```
```js
// Result
{
  "block_hash": "997bf5cecb4df097991a7a121a7fd3cb5a404fa856e3d6032c791ac07bc7c74c"
}
```

## get-block

区块高度或块哈希返回详细信息块。

#### 参数

`Object`: block_height | block_hash

可选:

- `String` - *block_hash*, 区块hash.
- `Integer` - *block_height*, 区块高度.

#### 返回

`Object`:

- `String` - *hash*, 区块hash.

- `Integer` - *size*, 区块大小.

- `Integer` - *version*, 区块版本.

- `Integer` - *height*, 区块高度.

- `String` - *previous_block_hash*, 前一个区块hash.

- `Integer` - *timestamp*, 区块时间戳.

- `Integer` - *nonce*, 随机数值.

- `Integer` - *bits*, 区块难度.

- `String` - *difficulty*, 难度值(String type).

- `String` - *transaction_merkle_root*, 交易的默克尔根.

- `String` - *transaction_status_hash*, 交易状态的默克尔根.

- `Array of Object`- * transactions*, 交易对象:

  - `String` - *id*, transaction id, 交易hash.

  - `Integer` - *version*, 交易版本.

  - `Integer` - *size*, 交易大小.

  - `Integer` - *time_range*, 响应请求时的unix时间戳.

  - `Boolean` - *status_fail*, 请求状态是否是失败的.

  - `String` - *mux_id*, 前一笔交易的mux id(utxo的源ID).

  - `Array of Object`- *inputs*, 交易对象的输入.

    - `String` - *type*, 输入操作的类型，可用选项包括: 'spend', 'issue', 'coinbase'.
    - `String` - *asset_id*, 资产id.
    - `String` - *asset_alias*, 资产名字.
    - `Object` - *asset_definition*, 资产定义(json 对象).
    - `Integer` - *amount*, 资产数量.
    - `Object` - *issuance_program*, issuance program, 当交易类型为'issue'.
    - `Object` - *control_program*, control program of account, 当交易类型为'spend'.
    - `String` - *address*, 账户地址, 当类型是'spend'时存在.
    - `String` - *spent_output_id*, the front of outputID to be spent in this input, 当交易类型为'spend'.
    - `String` - *account_id*, 账户id.
    - `String` - *account_alias*, 账户名字.
    - `Object` - *arbitrary*, 任意信息都可以由矿工设置，当交易类型为'coinbase'时.

  - `Array of Object` - *outputs* , 交易输出对象.

    - `String` - *type*, 输出action的类型，可选项包括:"retire","control".
    - `String` - *id*, 与utxo相关的交易输出id.
    - `Integer` - *position*, 输出的位置.
    - `String` - *asset_id*, 资产id.
    - `String` - *asset_alias*, 资产名字.
    - `Object` - *asset_definition*, 资产定义(json 对象).
    - `Integer` - *amount*, 资产数量.
    - `String` - *account_id*, 账户id.
    - `String` - *account_alias*, 账户名字.
    - `Object` - *control_program*, 账户的控制程序.
    - `String` - *address*, 账户地址.

#### 例子

通过block_hash或block_height获取指定的块信息，如果两者都存在，则块结果通过哈希查询。
```php
BytomClient::getBlock($block_hash, $block_height);
```
```js
// Result
{
  "bits": 2305843009222082600,
  "difficulty": "5549086336",
  "hash": "886a8e85b275e7d65b569ba510875c0e63dece1a94569914d7624c0dac8002f9",
  "height": 43,
  "nonce": 3,
  "previous_block_hash": "2c72ccbd53b92a4f9423c5b610b4e106bbe8fbf3ecf2e16a1266b17ee323ff9d",
  "size": 386,
  "timestamp": 1521614189,
  "transaction_merkle_root": "77d40262cfeca3a16d4587132974552ef00951e43ce567a26801ebc3dbdb4d96",
  "transaction_status_hash": "53c0ab896cb7a3778cc1d35a271264d991792b7c44f5c334116bb0786dbc5635",
  "transactions": [
    {
      "id": "4576b1b1ec251da3263dbdd5486bcbf9a1cd1f712172dbe7a7a5fe46ab194629",
      "inputs": [
        {
          "amount": 0,
          "arbitrary": "09",
          "asset_definition": "7b7d",
          "asset_id": "0000000000000000000000000000000000000000000000000000000000000000",
          "type": "coinbase"
        }
      ],
      "mux_id": "2383cefe8a34ea5810cc0706f2cf8cf08a106f90fc3eb3441f723cecdbc61331",
      "outputs": [
        {
          "address": "sm1q4pkg8msjumtep7ecsdzuct3tsuzk5pmnm3p8nr",
          "amount": 624000000000,
          "asset_definition": "7b7d",
          "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff",
          "control_program": "0014f3403bcd8b443d03882a280b50f6f98986e1a255",
          "id": "da87b40854a9b93be72ecdc24fe7bb03986ea3530e344b0f918f0788c3d83717",
          "position": 0,
          "type": "control"
        }
      ],
      "size": 77,
      "status_fail": false,
      "time_range": 0,
      "version": 1
    }
  ],
  "version": 1
}
```

## get-block-header

按块高度或块哈希返回详细信息块标头。

#### 参数

`Object`: block_height | block_hash

可选:

- `String` - *block_hash*, 区块hash.
- `Integer` - *block_height*, 区块高度.

#### 返回

- `Object` - *block_header*, 区块头.
- `Integer` - *reward*, 区块奖励.

#### 例子
```php
BytomClient::getBlockHeader($block_hash, $block_height);
```
```js
// Result
{
  "block_header": "01019601e87da37e7d73f31d54304c719c9058ec7bc7de7819deda89a7c8834a99bc05b8fbdbe6d60540eba9e5d5cb79fd87b3c0fad32f6772c1e4483f2a070e093a6176d85226d986a8c9c377e5192668bc0a367e4a4764f11e7c725ecced1d7b6a492974fab1b6d5bc00ad918480808080801e",
  "reward": 41250000000
}
```

## get-difficulty

通过块高度或块散列返回块高度，当请求为空时返回当前块高度。

#### 参数

- `String` - *block_hash*, 区块hash.
- `Integer` - *block_height*, 区块高度.

#### 返回

- `Integer` - *bits*, 区块的位.
- `String` - *difficulty*, 区块难度.
- `String` - *hash*, 区块hash.
- `Integer` - *height*, 区块高度.

##### 例子

为当前块或指定的块散列/高度获取困难。
```php
BytomClient::getDifficulty($block_hash, $block_height);
```
```js
// Result
{
  "bits": 2161727821137910500,
  "difficulty": "15154807",
  "hash": "d1fce60caea5466eae2b812e4586b55120c52aca27b6c92bd7c51e9cda82dcdf",
  "height": 506
}
```

## get-hash-rate

通过块高度或块散列返回块散列率，当请求为空时，它返回当前块散列率。

#### 参数

- `String` - *block_hash*, 区块hash.
- `Integer` - *block_height*, 区块高度.

#### 返回

- `Integer` - *hash_rate*, 区块的出块难度.
- `String` - *hash*, 区块 hash.
- `Integer` - *height*, 区块 height.

#### 例子

获取当前块或指定块散列/高度的哈希率。
```php
BytomClient::getHashRate($block_hash, $block_height);
```
```js
// Result
{
  "hash": "d1fce60caea5466eae2b812e4586b55120c52aca27b6c92bd7c51e9cda82dcdf",
  "hash_rate": 7577403,
  "height": 506
}
```

