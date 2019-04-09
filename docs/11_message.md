---
id: message
title: Message API
sidebar_label: Bytom.Message.API
---

## sign-message

使用地址的密钥（私钥）对信息进行签名。

#### 参数

- `String` - *address*, 账户地址
- `String` - *message*, 地址xpub签名的消息
- `String` - *password*, 账户密码

#### 返回

- `String` - *derived_xpub*, 派生的xpub.
- `String` - *signature*, 消息的签名.

#### 例子
```php
BytomClient::signMessage($address, $message, $password);
```
```js
// Result
{
  "signature": "74da3d6572233736e3a439166719244dab57dd0047f8751b1efa2da26eeab251d915c1211dcad77e8b013267b86d96e91ae67ff0be520ef4ec326e911410b609",
  "derived_xpub": "6ff8c3d1321ce39a3c3550f57ba70b67dcbcef821e9b85f6150edb7f2f3f91009e67f3075e6e76ed5f657ee4b1a5f4749b7a8c74c8e7e6a1b0e5918ebd5df4d0"
}
```

##  verify-message

用地址派生的pubkey验证已签名的消息。

#### 参数


- `String` - *address*, 账户地址.
- `String` - *derived_xpub*, 派生的xpub.
- `String` - *message*, 来自derived_xpub的签名消息.
- `String` - *signature*, 消息签名.

#### 返回

`Object`:

- `Boolean` - *result*, 验证结果.

#### 例子
```php
BytomClient::verifyMessage($address, $derived_xpub, $message, $signature);
```
```js
// Result
{
  "result": true
}
```