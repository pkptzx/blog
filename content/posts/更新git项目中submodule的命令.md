---
title: "更新git项目中submodule的命令"
date: 2020-12-21T16:31:50+08:00
draft: false
weight: 70
keywords: ["git","submodule"]
description: "更新git项目中submodule的命令"
tags: ["git"]
categories: ["git"]
author: "码魂"
url: "2020/12/21/git-submodule-update"
---
之前一直没有注意submodule如何更新的问题,一直以为我clone后submodule就是新的,后来才发现即便我重新clone,submodule也是按照当时提交时候的版本.找了几个小时才找到简单的命令进行更新submodule.
```
git submodule update --recursive --remote --merge --force
```
