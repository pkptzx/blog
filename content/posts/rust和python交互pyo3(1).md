---
title: "rust和python交互pyo3(一)"
date: 2021-08-04T20:05:48+08:00
draft: false
weight: 70
keywords: ["python","rust","pyo3"]
description: "rust和python交互pyo3"
tags: ["python","rust"]
categories: ["python","rust"]
author: "码魂"
url: "2022/03/12/rust-pyo3-learn-1"
---

### rust和python交互pyo3(1)

pyo3 需要python3.7以上的版本

pip install maturin
新建文件夹后:初始化
maturin init --bindings pyo3
开发编译安装,就可以测试用python调用了
maturin develop
release版本编译,只会编译,不会更新安装到python环境
maturin build --release

生成的pyproject.toml中requires-python可能最小是3.6,有可能导致编译失败,可以手动改为3.7以上


Ubuntu:
sudo apt install python3-dev
centos8:
yum/dnf install python38-devel


这两个features不能同时存在,否则导致rust编译失败
"extension-module","auto-initialize"
将rust写的py库和,rust调用py拆成两个子工程.


whl强制安装/更新
pip install -U --force-reinstall  xxx.whl
