---
id: key
title: Key API
sidebar_label: Bytom.Key.API
---

## create-key

本质上是创建私钥，返回密钥的信息，其中私钥保存在本地文件中，加密对用户不可见。

#### 参数

- `String` - *alias* ，密钥的名字
- `String` - *password* ，私钥的密码

#### 返回

- `String` - *alias* , 密钥的名字

- `String` - *xpub* , 公钥

- `String` - *file* , 私钥文件在本地的存放路径
#### 例子
```java
Client client = Client.generateClient();
String alias = "testJava1";
String password = "123456";
Key.Builder builder = new Key.Builder().setAlias(alias).setPassword(password);
Key key = Key.create(client, builder);
System.out.println(key);
```
```bash
// Result
Key{alias='testjava1', xpub='57011d2ed46aafe47c9c77f6f3b4cef95ba19474f50d918fefe71a675ac15413c8e733ff6581b311d89bbfb5fedc34de4e7f6aedf2f5ac1f1b56cedc5a23ece9', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-23T07-19-41.724077700Z--532f7a7a-86d7-44c5-b624-c547be0bd050'}
```
## list-keys

返回所有可用的密钥列表。

#### 参数

none

#### 返回

- `Array of Object` , 客户端所拥有的所有私钥信息
  - `object` :
    - `String`  - *alias* , 私钥的名字
    - `String` - *xpub*, 公钥
#### 例子
```java
Client client = Client.generateClient();
List<Key> keyList = Key.list(client);
```
```bash
// Result
1    INFO  [2019-04-23 16:05:00]  list-key:
2    INFO  [2019-04-23 16:05:00]  size of key:3
3    INFO  [2019-04-23 16:05:00]  [Key{alias='alice', xpub='872e6fbe0ad47b0ff6435bcc4c18fd0c00631afe6c4433938fd7059f32d9c26bb888d0f112cbc07880a1d9ef50111154fa34570233bda070503f6fbe94daf974', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-04T01-40-00.441340200Z--653ae5ff-84d2-4949-9784-28ca70809f58'}, Key{alias='bob', xpub='4874e557e062778cba85825064f41e2ca0f61478a1469df0eb5ea35d457de5c317a0520f672cbd98186cf5d26f823d93d926f6383db54bae7fcc92ff975b2215', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-04T07-56-42.134038700Z--13a3e5cb-0fce-46ed-a845-9b6d2380dab9'}, Key{alias='testjava1', xpub='57011d2ed46aafe47c9c77f6f3b4cef95ba19474f50d918fefe71a675ac15413c8e733ff6581b311d89bbfb5fedc34de4e7f6aedf2f5ac1f1b56cedc5a23ece9', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-23T07-19-41.724077700Z--532f7a7a-86d7-44c5-b624-c547be0bd050'}]
```

## delete-key
删除现有的密钥，请确保相关账户中没有余额。
#### 参数
- `String` - *xpub*, 公钥
- `String` - *password*,密钥的密码
#### 返回
如果删除成功则返回none
#### 例子
```java
Client client = Client.generateClient();
List<Key> keyList = Key.list(client);
String xpub = keyList.get(keyList.size()-1).xpub;
//删除最后一个密钥
Key.delete(client, xpub, "123456");
```
```bash
// Result
INFO  [2019-04-23 16:25:52]  delete-key successfully.
```
##  reset-key-password

重置密钥密码。

#### 参数

- `String` - *xpub* , 公钥
- `String` - *old_password*, 密钥文件的旧密码
- `String` - *new_password* , 密钥文件的新密码

#### 返回

如修改成功则返回none

#### 例子
```java
Client client = Client.generateClient();
List<Key> keyList = Key.list(client);
String xpub = keyList.get(keyList.size()-1).xpub;
Key.resetPassword(client, xpub, "123456", "123456789");
```
```bash
// Result
//none
```