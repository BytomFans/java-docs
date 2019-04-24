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

```java
Client client = TestUtils.generateClient();
List<Account> accountList = Account.list(client);
String alias = "GOLD";
List<String> xpubs = accountList.get(0).xpubs;
Asset.Builder builder = new Asset.Builder()
    .setAlias(alias)
    .setQuorum(1)
    .setRootXpubs(xpubs);
System.out.println(builder);
```

```bash
// Result
Builder{alias='GOLD', definition=null, rootXpubs=[872e6fbe0ad47b0ff6435bcc4c18fd0c00631afe6c4433938fd7059f32d9c26bb888d0f112cbc07880a1d9ef50111154fa34570233bda070503f6fbe94daf974], quorum=1, access_token='null'}
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
```java
Client client = TestUtils.generateClient();
Asset.QueryBuilder queryBuilder = new Asset.QueryBuilder();
String id = queryBuilder.list(client).get(1).id;
queryBuilder.setId(id);
Asset asset = queryBuilder.get(client);
```

```bash
// Result
{"id":"57ba2e10543e35f682d4e47729da3c6da0372a94b4c6d04fe59bd389e2e68edc","alias":"HELLOWORLD","key_index":1,"xpubs":["f6a16704f745a168642712060e6c5a69866147e21ec2447ae628f87d756bb68cc9b91405ad0a95f004090e864fde472f62ba97053ea109837bc89d63a64040d5"],"quorum":1,"definition":{"decimals":8.0,"description":{},"name":"GOLD","symbol":"GOLD"},"vm_version":1,"type":"asset","raw_definition_byte":"7b0a202022646563696d616c73223a20382c0a2020226465736372697074696f6e223a207b7d2c0a2020226e616d65223a2022474f4c44222c0a20202273796d626f6c223a2022474f4c44220a7d"}
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

```java
Client client = TestUtils.generateClient();
Asset.QueryBuilder queryBuilder = new Asset.QueryBuilder();
List<Asset> assetList = queryBuilder.list(client);
```

```bash
// Result
[Asset{id='ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff', alias='BTM', issuanceProgram='null', keys=null, keyIndex=0, xpubs=null, quorum=0, definition={decimals=8.0, description=Bytom Official Issue, name=BTM, symbol=BTM}, vmVersion=1, type='internal', rawDefinitionByte='7b0a202022646563696d616c73223a20382c0a2020226465736372697074696f6e223a20224279746f6d204f6666696369616c204973737565222c0a2020226e616d65223a202242544d222c0a20202273796d626f6c223a202242544d220a7d'}, Asset{id='57ba2e10543e35f682d4e47729da3c6da0372a94b4c6d04fe59bd389e2e68edc', alias='HELLOWORLD', issuanceProgram='null', keys=null, keyIndex=1, xpubs=[f6a16704f745a168642712060e6c5a69866147e21ec2447ae628f87d756bb68cc9b91405ad0a95f004090e864fde472f62ba97053ea109837bc89d63a64040d5], quorum=1, definition={decimals=8.0, description={}, name=GOLD, symbol=GOLD}, vmVersion=1, type='asset', rawDefinitionByte='7b0a202022646563696d616c73223a20382c0a2020226465736372697074696f6e223a207b7d2c0a2020226e616d65223a2022474f4c44222c0a20202273796d626f6c223a2022474f4c44220a7d'}, Asset{id='c2b370f20c418db3222254270f1c3f4d3a2d65c3fc8090c8a9005b5cf8289cda', alias='GOLD', issuanceProgram='null', keys=null, keyIndex=2, xpubs=[872e6fbe0ad47b0ff6435bcc4c18fd0c00631afe6c4433938fd7059f32d9c26bb888d0f112cbc07880a1d9ef50111154fa34570233bda070503f6fbe94daf974], quorum=1, definition=null, vmVersion=1, type='asset', rawDefinitionByte='7b7d'}]
```

## update-asset-alias

按assetID更新资产别名。

#### 参数

- `String` - *id*, 资产id
- `String` - *alias*, 资产的新别名

#### 返回

如果资产别名更新成功，则为none。

##### 例子

```java
Client client = TestUtils.generateClient();
Asset.QueryBuilder queryBuilder = new Asset.QueryBuilder();
String id = queryBuilder.list(client).get(1).id;
String alias = "HELLOWORLD";
//修改列表中下标为1的资产别名
Asset.AliasUpdateBuilder aliasUpdateBuilder =
    new Asset.AliasUpdateBuilder()
    .setAlias(alias)
    .setAssetId(id);
aliasUpdateBuilder.update(client);
```

```bash
// Result
[Asset{id='57ba2e10543e35f682d4e47729da3c6da0372a94b4c6d04fe59bd389e2e68edc', alias='HELLOWORLD', issuanceProgram='null', keys=null, keyIndex=1, xpubs=[f6a16704f745a168642712060e6c5a69866147e21ec2447ae628f87d756bb68cc9b91405ad0a95f004090e864fde472f62ba97053ea109837bc89d63a64040d5], quorum=1, definition={decimals=8.0, description={}, name=GOLD, symbol=GOLD}, vmVersion=1, type='asset', rawDefinitionByte='7b0a202022646563696d616c73223a20382c0a2020226465736372697074696f6e223a207b7d2c0a2020226e616d65223a2022474f4c44222c0a20202273796d626f6c223a2022474f4c44220a7d'}]
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

```java
Client client = TestUtils.generateClient();
List<Balance> balanceList = new Balance.QueryBuilder().list(client);
Assert.assertNotNull(balanceList);
```

```bash
// Result
[{"account_alias": "default","account_id": "0BDQ9AP100A02","amount": 35508000000000,"asset_alias": "BTM","asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"},{"account_alias": "alice","account_id": "0BDQARM800A04","amount": 60000000000,"asset_alias": "BTM", "asset_id": "ffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffffff"}]
```

## list-unspent-outputs

返回钱包中所有帐户的所有未花费事务输出。

#### 参数

- `String` - *alias*, 未花费的输出alias

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

按资产别名查找所有可用的未使用输出：
```java
Balance balance = new Balance.QueryBuilder().listByAssetAlias(client, "BTM");
Assert.assertNotNull(balance);
```

```bash
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
按账户别名查找所有可用的未使用输出：
```java
List<Balance> balanceList = new Balance.QueryBuilder().listByAccountAlias(client, "test");
Assert.assertNotNull(balanceList);
```
```bash
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