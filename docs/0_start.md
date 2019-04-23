---
id: start
title: quick start
sidebar_label: SDK环境配置
---

## 安装

我们有很多种方法安装Bytom java-sdk，本文档提供三种方法帮开发者快速安装。注意：bytom-sdk要求java7.0以上。

#### 添加Maven依赖库

在根目录pom.xml中添加如下配置：

```xml
<dependency>
    <groupId>io.bytom</groupId>
    <artifactId>java-sdk</artifactId>
    <version>1.0.0</version>
</dependency>
```

#### 使用Gradle/Grails安装

```bash
compile 'io.bytom:bytom-sdk:1.0.1'
```

#### 使用GitHub下载

从github上clone，编译并安装到你本地的Maven仓库中：

```bash
git clone https://github.com/Bytom/bytom-java-sdk.git
cd java-sdk
mvn install -Dmaven.test.skip=true
```

## 使用示例

创建一个SDK的实例，默认会连接你本地（[http://127.0.0.1:9888](http://127.0.0.1:9888/)）的core：

```java
public static Client generateClient() throws BytomException {
    String coreURL = Configuration.getValue("bytom.api.url");
    String accessToken = Configuration.getValue("client.access.token");
    if (coreURL == null || coreURL.isEmpty()) {
        coreURL = "http://127.0.0.1:9888/";
    }
    return new Client(coreURL, accessToken);
}
```

创建一个key

```java
import io.bytom.api.Key;
import io.bytom.http.Client;

public class Main {
    public static void main(String[] args) throws Exception {
        //创建一个SDK的实例，连接到本地core
        Client client = Client.generateClient();
        String alias = "testJava1";
        String password = "123456";
        Key.Builder builder = new Key.Builder().setAlias(alias).setPassword(password);
        Key key = Key.create(client, builder);
        System.out.println(key);
    }
}
```

控制台返回如下：
```bash
Key{alias='testjava1', xpub='57011d2ed46aafe47c9c77f6f3b4cef95ba19474f50d918fefe71a675ac15413c8e733ff6581b311d89bbfb5fedc34de4e7f6aedf2f5ac1f1b56cedc5a23ece9', file='C:\Users\mumu\AppData\Roaming\Bytom\keystore\UTC--2019-04-23T07-19-41.724077700Z--532f7a7a-86d7-44c5-b624-c547be0bd050'}
```

## 其他示例

请参考文档：[API中文文档](docs/key)

## 支持与反馈

如果你发现了该SDK的bug，请直接在github上提交issue： [Bytom-java-SDK Issues](<https://github.com/chainworld/java-bytom/issues>)

## license

[Apache License, Version 2.0](http://www.apache.org/licenses/LICENSE-2.0.txt) 

