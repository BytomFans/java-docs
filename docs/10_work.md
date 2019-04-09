---
id: work
title: Work API
sidebar_label: Bytom.Work.API
---

## get-work

获得工作证明。

#### 参数

none

#### 返回

`Object`:

- `Object` - *block_header*, 原始区块头.
- `Object` - *seed*, 随机种子.


##### 例子
```php
BytomClient::getWork();
```
```js
// Result
{
  "block_header": "0101870103f2c7495164c8f3af43697e81faa21dcb2d60aa5e10ce4f233491e62420742fbeadfcd50540bef2670a5fade2e58ad4955e2375a04ad1e4cb9c104faddab43f4a79e35be253c9c377e5192668bc0a367e4a4764f11e7c725ecced1d7b6a492974fab1b6d5bc00ffffff838080808020",
  "seed": "702bef3f1707577fd0d75b6359a2919fa216487fe306771e27710acbaa9164ce"
}
```


## submit-work

提交工作证明。

#### 参数

- `Object` - *block_header*, 原始区块头.

#### 返回

如果成功返回true

#### 例子
```php
BytomClient::submitWork($block_header);
```
```js
// Result
true / error
```