---
title: "Rust 安装与环境设置"
date: 2022-01-08T08:23:22+08:00
draft: false
weight: 70
keywords: ["Rust"]
description: "Rust 安装与环境设置"
tags: ["Rust"]
categories: ["Rust"]
author: "码魂"
url: "2022/01/08/rust-setup"
---

# rust 安装与环境设置
## 配置环境变量
新建cargo, rustup文件夹, 后期包的累积可能会占用巨量的存储空间, 土豪请随意.
CARGO_HOME : Cargo 在本地缓存注册表索引和箱子的 git 版本。如: E:\RUST\CARGO
RUSTUP_HOME: 工具链, 如: E:\RUST\RUSTUP

rustup target list
rustup target add x86_64-pc-windows-gnu

windows中编译成linux可执行文件:
先添加或安装工具链:x86_64-unknown-linux-musl
~/.cargo/config添加:
[target.x86_64-unknown-linux-musl]
linker = "rust-lld"
编译:
cargo build --target x86_64-unknown-linux-musl --release

## 国内源
~/.cargo/config添加:
```ini
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
replace-with = 'ustc'
[source.ustc]
registry = "git://mirrors.ustc.edu.cn/crates.io-index"

[target.x86_64-pc-windows-gnu]
linker = "D:\\mingw-w64\\x86_64-8.1.0-posix-seh-rt_v6-rev0\\mingw64\\bin\\gcc.exe"
ar = "D:\\mingw-w64\\x86_64-8.1.0-posix-seh-rt_v6-rev0\\mingw64\\bin\\ar.exe"
```
-   或者在项目工程结构中，与 Cargo.toml 同级目录的 .cargo 文件夹下创建 config 文件，config 文件配置方法和内容与第一种相同。

cargo build --target x86_64-pc-windows-gnu

cargo run --release --target x86_64-pc-windows-gnu

查看当前默认工具链
rustup default
修改为gnu
rustup default stable-gnu
修改为msvc
rustup default stable-msvc

rustup toolchain install stable-x86_64-pc-windows-gnu
rustup default stable-x86_64-pc-windows-gnu

## 升级
```shell
rustup self update
```
```shell
rustup update
```

## cargo 常用命令
创建一个新项目,默认是二进制程序,可以不写--bin,如果是创建库项目则--lib
默认还会初始化git存储库,如果不要则--vcs none
`cargo new hello_world --bin`
编译release版本
`cargo build --release`
编译运行
`cargo run`

## 国内源参考:
```ini
[source.crates-io]
registry = "https://github.com/rust-lang/crates.io-index"
# 指定镜像
replace-with = '镜像源名' # 如：tuna、sjtu、ustc，或者 rustcc

# 注：以下源配置一个即可，无需全部

# 中国科学技术大学
[source.ustc]
registry = "https://mirrors.ustc.edu.cn/crates.io-index"
# >>> 或者 <<<
registry = "git://mirrors.ustc.edu.cn/crates.io-index"

# 上海交通大学
[source.sjtu]
registry = "https://mirrors.sjtug.sjtu.edu.cn/git/crates.io-index/"

# 清华大学
[source.tuna]
registry = "https://mirrors.tuna.tsinghua.edu.cn/git/crates.io-index.git"

# rustcc社区
[source.rustcc]
registry = "https://code.aliyun.com/rustcc/crates.io-index.git"

```

## strip减小文件体积

## rust相关参考
cargo: https://cargo.budshome.com/guide/dependencies.html
Rust实践指南: https://rust-guide.budshome.com/
rust-in-databend: https://github.com/wubx/rust-in-databend
