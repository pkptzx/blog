---
title: "LBS基站查询"
date: 2018-11-21T22:52:47+08:00
draft: false
weight: 70
keywords: ["LBS"]
description: "LBS基站查询"
tags: ["LBS"]
categories: ["位置服务"]
author: "码魂"
---

今天调试机器发现返回的LBS是"LBS":"7300B084A16"

没有见过这种的,后来问了人才知道这是基站的。

2g是8位.
4g是11位.

不管是2/4g,头4位为LAC/TAC,剩下的是CI

可以通过这个地址直接查询：

http://www.gpsspg.com/bs.htm

免费接口地址：

http://api.cellocation.com:81/cell/?mcc=460&mnc=1&lac=4301&ci=20986&output=xml

文档地址：


http://www.cellocation.com/api/