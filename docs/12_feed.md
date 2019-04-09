---
id: feed
title: Feed API
sidebar_label: Bytom.Feed.API
---

## create-transaction-feed

创建交易反馈。

#### 参数

- `String` - *alias*, 交易反馈的名字.
- `String` - *filter*, 交易反馈的过滤器.

#### 返回

如果交易反馈已成功创建，返回none。

#### 例子
```php
BytomClient::createTransactionFeed($alias, $filter);
```
```js
// Result
//none
```

## get-transaction-feed

按名称查询交易反馈详细信息。

#### 参数

`Object`:

- `String` - *alias*, 交易反馈的名字.

##### 返回

`Object`:

- `String` - *id*, 交易反馈的id.

- `String` - *alias*, 交易反馈的名字.

- `String` - *filter*, 交易反馈的过滤器.

- `Object` - *param*, 交易反馈的参数.
  - `String` - *assetid*, 资产id.
  - `Integer` - *lowerlimit*, 资产数额下限.
  - `Integer` - *upperlimit*, 资产数额上限.
  - `String` - *transtype*, 交易类型.

#### 例子

列出别名可用的txfeed：
```php
BytomClient::getTransactionFeed($alias);
```
```js
// Result
{
  "alias": "test1",
  "filter": "asset_id='84778a666fe453cf73b2e8c783dbc9e04bc4fd7cbb4f50caeaee99cf9967ebed' AND amount_lower_limit = 50 AND amount_upper_limit = 100",
  "param": {}
}
```

## list-transaction-feeds

返回所有可用交易反馈的列表。

#### 参数

none

#### 返回

- `Array of Object` , 交易反馈列表.

  - `Object` :

    - `String` - *id*, 交易反馈id.

    - `String` - *alias*, 交易反馈名字.

    - `String` - *filter*, 交易反馈过滤器.

    - ` Object` - *param* , 交易反馈参数.
      - `String` - *assetid*, 资产id.
      - `Integer` - *lowerlimit*, 资产数额下限.
      - `Integer` - *upperlimit*, 资产数额上限.
      - `String` - *transtype*, 交易类型.

#### 例子

列出所有可用的txfeed：
```php
BytomClient::listTransactionFeeds();
```
```js
// Result
[
  {
    "alias": "test1",
    "filter": "asset_id='84778a666fe453cf73b2e8c783dbc9e04bc4fd7cbb4f50caeaee99cf9967ebed' AND amount_lower_limit = 50 AND amount_upper_limit = 100",
    "param": {}
  },
  {
    "alias": "test2",
    "filter": "asset_id='cee6a588cc3fc280749021ef42d5209952a1e6feceada4e69dd8a424ad22b199' AND amount_lower_limit = 30 AND amount_upper_limit = 100",
    "param": {}
  }
]
```

## delete-transaction-feed

根据交易名字删除交易反馈.

#### 参数

- `String` - *alias*, 交易反馈名字.

#### 返回

如果交易反馈删除成功，则无返回.

#### 例子
```php
BytomClient::deleteTransactionFeed($alias);
```
```js
// Result
//none
```

## update-transaction-feed

更新交易反馈.

#### 参数

- `String` - *alias*, 交易反馈名字.
- `String` - *filter*, 交易反馈过滤器.

#### 返回

如果交易反馈更新成功无返回.

#### 例子

当交易反馈存在的时候删除它，并使用别名和过滤器创建它:
```php
BytomClient::updateTransactionFeed($alias, $filter);
```
```js
// Result
//none
```