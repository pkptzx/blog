---
title: "rust使用shuttle部署项目后端"
date: 2023-02-16T18:16:47+08:00
draft: false
weight: 70
keywords: ["rust,shuttle"]
description: "rust使用shuttle来部署项目后端"
tags: ["shuttle", "rust"]
categories: ["shuttle", "rust"]
author: "码魂"
url: "2023/02/16/rust-shuttle"
---

# shuttle v0.10使用说明

https://www.shuttle.rs/

## 安装或更新 shuttle
如果系统磁盘剩余空间比较少,可以通过--target-dir来指定编译时产生的临时文件目录
```shell
cargo install cargo-shuttle --target-dir F:\temp
```

## 登录shuttle
```shell
cargo shuttle login FwvYic0Pk4k35vlx
```

## 初始化
```shell
cargo shuttle init
```

## 部署
```shell
cargo shuttle deploy
# 如果未提交git,提示异常,根据提示提交或增加参数即可
cargo shuttle deploy --allow-dirty
```

## 本地运行
```shell
cargo shuttle run
```
## 指定项目名
创建`Shuttle.toml` 在里面添加:  
name = "your-project-name

## 报错解决
error:
>error: couldn't read \\?\x:\...\target\debug\build\rustversion-...\out/version.expr: 文件名、目录名或卷标语法不正确。 (os error 123)

answer in discord:
>You may need to do a cargo +1.65 build first, and then cargo +1.65 shuttle run for it to work on windows.

>1.66 may work too. The +<version> syntax is just to run a cargo command with a specific toolchain, if your default toolchain is that version you shouldn't need it.

1. 对项目使用指定rust版本,方式一(实际修改了.rustup/settings.toml)
    - 在工程中执行: rustup override set 1.65
    - 移除指定的版本: rustup override unset
2. 方式二
   - 工程中创建: rust-toolchain.toml
   - 添加内容:
   
   ```toml
    [toolchain]
    channel = "1.65"
    # channel = "nightly"
    ```

```shell
# 使用1.65重新安装cargo-shuttle (或者直接binstall[未测])
cargo +1.65 install cargo-shuttle --force
cargo +1.65 build
cargo +1.65 shuttle run
```
