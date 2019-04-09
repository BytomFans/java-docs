---
id: decode_program
title: Decode_program API
sidebar_label: Bytom.Decode_program.API
---

## decode-program

解码程序。

##### 参数

- `String` - *raw_transaction*,已经签名好的交易.

##### 返回

`Object`:

- `String` - *instructions*, 程序的说明和数据.

##### 例子
```php
BytomClient::decodeRawTransaction($raw_transaction);
```
```js
// Result
{
  "instructions": "DUP \nHASH160 \nDATA_20 a86c83ee12e6d790fb388345cc2e2b87056a0773\nEQUALVERIFY \nTXSIGHASH \nSWAP \nCHECKSIG \n"
}
```