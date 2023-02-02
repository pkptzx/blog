---
title: "centos7安装新版本的git客户端"
date: 2023-02-02T15:16:47+08:00
draft: false
weight: 70
keywords: ["linux,git,github,centos"]
description: "linux centos7中访问github和安装新版本的git客户端"
tags: ["linux","git"]
categories: ["linux","git"]
author: "码魂"
url: "2023/02/02/centosgit2"
---

# linux中访问github:参见: https://gitclone.com/  
```shell
方法一（替换URL）
git clone https://gitclone.com/github.com/tendermint/tendermint.git
方法二（设置git参数）
git config --global url."https://gitclone.com/".insteadOf https://
git clone https://github.com/tendermint/tendermint.git
方法三（使用cgit客户端）
cgit clone https://github.com/tendermint/tendermint.git
```

# 安装新版本的git客户端: 使用 https://ius.io/ 源  
```shell
curl -sSL https://setup.ius.io | sh
# 查看哪些包提供git这个命令
yum provides git
# 这里结果显示最新版本为ius提供的包，版本为2.36.4
yum install git236 -y
# 查看版本
git --version
```
