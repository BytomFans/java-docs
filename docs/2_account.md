---
id: account
title: Account API
sidebar_label: Bytom.Account.API
---



## creat-account

创建账户以管理地址。单签账户只包含一个root_xpubs且quorum默认为1 ；但是多签账户包含许多root_xpubs且quorum不为1。

#### 参数

- `Array of Sring` -  *root_xpubs*, 公钥数组

- `String` - *alias*, 账户名称

- `Integer` - *quorum*, 默认值为1，范围是[1,len(root_xpubs)]，交易必须要由所有控制资产单位的账户密钥签名

Optional:

- `String` - *access_token*， 在本地创建账户时可不填，如果是远程创建账户则是必不可少的

#### 返回

-  `String` - *id*, 账户id

-  `String` - *alias*, 账户名称

-  `Integer` - *key_index*, 账户key的索引

-  `Integer` - *quorom*, 交易必须要由所有控制资产单位的账户密钥签名

-  `Array of Object` -  *xpubs*, 公钥数组

#### 例子
```java
Client client = TestUtils.generateClient();
String alias = "AccountTest.testAccountCreate.002";
Integer quorum = 1;
List<String> root_xpubs = new ArrayList<>();
root_xpubs.add("c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5");
Account.Builder builder = new Account.Builder().setAlias(alias).setQuorum(quorum).setRootXpub(root_xpubs);
Account account = Account.create(client, builder);
System.out.println(account);
```

```bash
// Result
INFO  [2019-04-23 16:39:23]  create-account
INFO  [2019-04-23 16:39:23]  Account{id='0RKNGHTRG0A08', alias='accounttest.testaccountcreate.002', key_index=3, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}
Account{id='0RKNGHTRG0A08', alias='accounttest.testaccountcreate.002', key_index=3, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}
```

## list-accounts

返回所有可用账户的列表。

#### 参数
none
#### 返回
- `Array of Object`, 账户数组
  - `String` - *id*, 账户id
  - `String` - *alias*, 公钥名称
  - `Integer` - *key_index*, 账户密钥的索引
  - `Integer` - quorom,  交易必须要由所有控制资产单位的账户密钥签名
  - `Array of Object` - xpubs, 公钥数组
#### 例子

```java
Client client = TestUtils.generateClient();
List<Account> accountList = Account.list(client);
```

```bash
// Result
INFO  [2019-04-23 16:47:25]  list-accounts:
INFO  [2019-04-23 16:47:25]  size of accountList:3
INFO  [2019-04-23 16:47:25]  [Account{id='0QRSNOQE00A02', alias='alice', key_index=1, quorum=1, xpubs=[872e6fbe0ad47b0ff6435bcc4c18fd0c00631afe6c4433938fd7059f32d9c26bb888d0f112cbc07880a1d9ef50111154fa34570233bda070503f6fbe94daf974]}, Account{id='0RKCD5TR00A04', alias='accounttest.testaccountcreate.002', key_index=1, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}, Account{id='0RKCF7B800A06', alias='accounttest.testaccountcreate.002', key_index=2, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}, Account{id='0RKNGHTRG0A08', alias='accounttest.testaccountcreate.002', key_index=3, quorum=1, xpubs=[c4b25825e92cd8623de4fd6a35952ad0efb2ed215fdb1b40754f0ed12eff7827d147d1e8b003601ba2f78a4a84dcc77e93ed282633f2679048c5d5ac5ea10cb5]}]
```

## delete-account

删除现有账户，请确保相关地址中没有余额。

#### 参数
- `String` - *account-info*,　账户别名或者id
#### 返回
如果账户已成功删除，则为none
#### 例子
```java
Client client = TestUtils.generateClient();
String id = "0QRSNOQE00A02";
Account.delete(client, id);
```
```bash
//none
```
## create-account-receiver
创建地址和控制程序，地址和控制程序是一对一的关系。在构建交易API中，接收器是动作类型为control_address时的地址，接收器是动作类型为control_program时的控制程序，它们是相同的结果。
#### 参数
`Object`: *account_alias | account_id*, 账户别名或账户id
可选：

- `String` - *account_alias*, 账户别名
- `String` - *account_id*, 账户id
#### 返回
- `String` - *address*, 账户地址
- `String` - *control_program*, 账户的控制程序
#### 例子
```java
Client client = TestUtils.generateClient();
String alias = "test1";
String id = "0RKNGHTRG0A08";
Account.ReceiverBuilder receiverBuilder = new Account.ReceiverBuilder().setAccountAlias(alias).setAccountId(id);

Receiver receiver = receiverBuilder.create(client);
System.out.println(receiver);
```
```bash
// Result
{"address":"bm1q87xrkeha33sgyn0gtj2pdxfcn22u78263yqfx7","control_program":"00143f8c3b66fd8c60824de85c941699389a95cf1d5a"}
```

## list-addresses

按账户返回所有可用地址的列表。

#### 参数

- `String` - *account_alias*, 账户别名
- `String` - *account_id*, 账户id

#### 返回

  - `String` - *account_alias*, 账户别名.
  - `String` - *account_id*, 账户id.
  - `String` - *address*, 账户地址.
  - `Boolean` - *change*, 账户地址是否改变.

####  例子

```java
Client client = TestUtils.generateClient();
String alias = "test1";
String id = "0RKNGHTRG0A08";
Account.AddressBuilder addressBuilder = new Account.AddressBuilder().setAccountId(id).setAccountAlias(alias);

List<Account.Address> addressList = addressBuilder.list(client);
```
```bash
// Result
[
  {
    "account_alias": "alice",
    "account_id": "086KQD75G0A02",
    "address": "bm1qcn9lf7nxhswratvmg6d78nq7r7yupm36qgsv55",
    "change": false
  },
  {
    "account_alias": "alice",
    "account_id": "086KQD75G0A02",
    "address": "bm1qew4h5uvt5ssrtg2alms0j77r94c30m78ucrcxy",
    "change": false
  },
  {
    "account_alias": "alice",
    "account_id": "086KQD75G0A02",
    "address": "bm1qgnp4lte7wge0rsekevjlrdh39vkzz0c2alheue",
    "change": false
  }
]
```

## validate-address

验证地址是否有效，并判断地址是否为自己。

#### 参数

- `String` - *address*，账户地址

####　返回

- `Boolean` - *vaild*，账户地址是否有效

- `Boolean` - *is_local*，账户地址是否是本地地址

#### 例子

```java
Client client = TestUtils.generateClient();
String alias = "test1";
String id = "0RKNGHTRG0A08";

Account.AddressBuilder addressBuilder = new Account.AddressBuilder().setAccountId(id).setAccountAlias(alias);
List<Account.Address> addressList = addressBuilder.list(client);

Account.Address address = addressBuilder.validate(client, addressList.get(0).address);
```

```bash
// Result
{"is_local":true}
```