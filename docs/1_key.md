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
```php
$alias = 'alice';
$pwd = '123456';
//调用BytomClient类下的createKey方法，传入alias和password两个参数
$client = BytomClient::createKey($alias, $password); 
console_($client);
```
```json
// Result
{
  "alias": "alice",
  "xpub": "a7dae957c2d35b42efe7e6871cf5a75ebd2a0d0e51caffe767db42d3e6d69dbe211d1ca492ecf05908fe6fa625ad61b3253375ea744c9442dd5551613ba50aea",
  "file": "/Path/To/Library/Bytom/keystore/UTC--2018-04-22T06-30-27.609315219Z--0e34293c-8856-4f5f-b934-37456a3820fa"
}
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
```php
$client = BytomClient::listKeys();
console_($client);
```
```json
// Result
[
  {
    "alias": "alice",
    "xpub": "a7dae957c2d35b42efe7e6871cf5a75ebd2a0d0e51caffe767db42d3e6d69dbe211d1ca492ecf05908fe6fa625ad61b3253375ea744c9442dd5551613ba50aea",
    "file": "/Path/To/Library/Bytom/keystore/UTC--2018-04-21T02-35-15.035935116Z--4f2b8bd7-0576-4b82-8941-6cc6da05efe3"
  },
  {
    "alias": "bob",
    "xpub": "d30a810e88532f73816b7b5007d413cbd21e526ae9159023e5262511893adc1526b8eacd691b27c080201d7d79336a4f3d2cb4c167d997821cad445765916254",
    "file": "/Path/To/Library/Bytom/keystore/UTC--2018-04-22T06-30-27.609315219Z--0e34293c-8856-4f5f-b934-37456a3820fa"
  }
]
```

## delete-key
删除现有的密钥，请确保相关账户中没有余额。
#### 参数
- `String` - *xpub*, 公钥
- `String` - *password*,密钥的密码
#### 返回
如果删除成功则返回none
#### 例子
```php
$res = BytomClient::deleteKey($xpub, $password);//实例化一个删除对象
$this->assertEquals(200, $res->getHTTPStatus());//获取请求网络状态，若为200则成功
$client = $this->assertTrue($res->isSucceeded());
console_($client)
```
```json
// Result
// none
```
##  reset-key-password

重置密钥密码。

#### 参数

- `String` - *xpub* , 公钥
- `String` - *old_password*, 密钥文件的旧密码
- `String` - *new_password* , 密钥文件的新密码

#### 返回

- `Boolean` - *changed* ,判断重置密钥密码后的状态，若为success则返回true

#### 例子
```php
$res = BytomClient::resetKeyPassword($xpub, $old_password, $new_password);
$this->assertEquals(200, $res->getHTTPStatus());//获取请求网络状态，若为200则成功
$client = $this->assertTrue($res->isSucceeded());
console_($client)
```
```json
// Result
{
  "changed": true
}
```