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

```php
$bytom = new BytomClient();
$res = $bytom->listAccounts();   //实例化一个对象
$this->assertEquals(200, $res->getHTTPStatus());//判断请求状态是否为200，是则为成功
$data = $this->assertTrue($res->isSucceeded());
console_($data);
```

```json
// Result
[
  {
    "alias": "alice",
    "id": "086KQD75G0A02",
    "key_index": 1,
    "quorum": 1,
    "xpubs": [
      "180aab8bf247932a7cf68da5cc9a873266279155097612f1e5fdda4add88d5e91e2e7ce5b736f3ac933824cdee9effcf1531b90dfcb388e5cc306d14e9a2c85e"
    ]
  },
  {
    "alias": "bob",
    "id": "086KQO67G0A04",
    "key_index": 2,
    "quorum": 1,
    "xpubs": [
      "180aab8bf247932a7cf68da5cc9a873266279155097612f1e5fdda4add88d5e91e2e7ce5b736f3ac933824cdee9effcf1531b90dfcb388e5cc306d14e9a2c85e"
    ]
  }
]
```

## update-account-alias

按账户id或账户别名更新账户别名。

#### 参数

- `String` - *account_id*, 账户id
- `String` - *account_alias*, 账户别名
- `String` - *new_alias*，账户的新别名 
#### 返回
如果账户别名更新成功，status为success。
#### 例子
```php
\\\\\
```

```json
// Result
{"status":"success"}
```

## delete-account

删除现有账户，请确保相关地址中没有余额。

#### 参数
- `String` - *account-info*,　账户别名或者id
#### 返回
如果账户已成功删除，则为none
#### 例子
```php
$client = BytomClient::deleteAccount($account_info);
```
```json
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
```php
$client = BytomClient::createAccountReceiver($account_alias, $account_id);
```
```json
// Result
{
    "address": "bm1q5u8u4eldhjf3lvnkmyl78jj8a75neuryzlknk0",
    "control_program": "0014a70fcae7edbc931fb276d93fe3ca47efa93cf064"
}
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

```php
BytomClient::listAddresses($account_alias, $account_id);
```
```json
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

```php
BytomClient::validateAddress($address);
```

```json
// Result
{
   "vaild": true,
   "is_local": true,
}
```