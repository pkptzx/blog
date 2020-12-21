---
title: "maven导出依赖jar"
date: 2020-12-21T19:20:23+08:00
draft: false
weight: 70
keywords: ["maven"]
description: "maven导出依赖jar"
tags: ["maven"]
categories: ["maven"]
author: "码魂"
url: "2020/12/21/maven-copy-dependencies"
---
在某些场景中,我们需要获取出项目依赖的jar给别人的话,可以使用maven自带的命令参数直接导出所有依赖的jar,并且可以指定要导出jar的范围,如下导出到dist目录,导出范围是runtime的依赖.注意如果写compile会将provided也导出来.

```
mvn dependency:copy-dependencies -DoutputDirectory=dist -DincludeScope=runtime
```
