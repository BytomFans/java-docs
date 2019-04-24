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
```java
Client client = TestUtils.generateClient();
String filter = "asset_id='57fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c' AND amount_lower_limit = 50 AND amount_upper_limit = 100";
String alias = "test";
new Transaction.Feed.Builder()
    .setAlias(alias)
    .setFilter(filter)
    .create(client);
```
```bash
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
```java
Client client = TestUtils.generateClient();
String alias = "test2";
Transaction.Feed transactionFeed = Transaction.Feed.getByAlias(client, alias);

Assert.assertNotNull(transactionFeed);
```
```bash
// Result
{"alias":"test2","filter":"asset_id\u003d\u002757fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c\u0027 AND amount_lower_limit \u003d 50 AND amount_upper_limit \u003d 100","param":{"assetid":"57fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c","lowerlimit":50,"upperlimit":100}}
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
```java
Client client = TestUtils.generateClient();
List<Transaction.Feed> txFeedList = Transaction.Feed.list(client);
Assert.assertNotNull(txFeedList);
```
```bash
// Result
{"alias":"test1","filter":"asset_id\u003d\u002784778a666fe453cf73b2e8c783dbc9e04bc4fd7cbb4f50caeaee99cf9967ebed\u0027 AND amount_lower_limit \u003d 60 AND amount_upper_limit \u003d 80","param":{"assetid":"84778a666fe453cf73b2e8c783dbc9e04bc4fd7cbb4f50caeaee99cf9967ebed","lowerlimit":60,"upperlimit":80}}
{"alias":"test2","filter":"asset_id\u003d\u002757fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c\u0027 AND amount_lower_limit \u003d 50 AND amount_upper_limit \u003d 100","param":{"assetid":"57fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c","lowerlimit":50,"upperlimit":100}}
```

## delete-transaction-feed

根据交易名字删除交易反馈.

#### 参数

- `String` - *alias*, 交易反馈名字.

#### 返回

如果交易反馈删除成功，则返回successfully.

#### 例子
```java
Client client = TestUtils.generateClient();
String filter = "asset_id='57fab05b689a2b8b6738cffb5cf6cffcd0bf6156a04b7d9ba0173e384fe38c8c' AND amount_lower_limit = 50 AND amount_upper_limit = 100";
String alias = "test2";

Transaction.Feed.update(client, alias, filter);
```
```bash
// Result
update-transaction-feed successfully
```

## update-transaction-feed

更新交易反馈.

#### 参数

- `String` - *alias*, 交易反馈名字.
- `String` - *filter*, 交易反馈过滤器.

#### 返回

如果交易反馈更新成功，则返回successfully.

#### 例子

当交易反馈存在的时候删除它，并使用别名和过滤器创建它:
```java
Client client = TestUtils.generateClient();
String alias = "test2";
Transaction.Feed.deleteByAlias(client, alias);
```
```bash
// Result
delete-transaction-feed successfully
```