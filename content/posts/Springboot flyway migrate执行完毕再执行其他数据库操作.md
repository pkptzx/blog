---
title: "Springboot flyway migrate执行完毕再执行其他数据库操作"
date: 2019-10-17T18:01:25+08:00
draft: false
weight: 70
keywords: ["Springboot"]
description: "Springboot flyway migrate执行完毕再执行其他数据库操作 "
tags: ["springboot","flyway"]
categories: ["springboot"]
author: "码魂"
url: "2019/10/17"
---
项目中使用了flyway，遇到flyway还未合并完数据库，业务代码就执行了，导致报错。要实现这个目标，有两种方法：

1. 使用DependsOn对相关Bean添加依赖，让数据库相关DAO Bean依赖flyway的Bean。这样DAO Bean初始化和使用就会在flyway Bean初始化之后了。
```java
@DependsOn({"flyway", "flywayInitializer"})
@Component
public class UserDao {
}
```
2. 继承FlywayMigrationStrategy。这种方式可以在migrate执行前后注入特定的操作。从执行日志也可以看到，真的起效果了，达到了我们的目标要求。
```java
@Component
@Slf4j
public class CallbackFlywayMigrationStrategy implements FlywayMigrationStrategy {


    @Override
    public void migrate(Flyway flyway) {
        log.info("before flyway migration...");
        flyway.migrate();
        log.info("after flyway migration...");
    }

}
```


