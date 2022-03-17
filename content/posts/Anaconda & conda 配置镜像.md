---
title: "Anaconda & conda 配置镜像"
date: 2021-08-04T20:05:48+08:00
draft: false
weight: 70
keywords: ["python","anaconda","conda"]
description: "Anaconda & conda 安装配置镜像"
tags: ["python","conda"]
categories: ["python","anaconda "]
author: "码魂"
url: "2021/08/04/anaconda-conda-install-mirrors"
---
## Anaconda & conda 配置镜像 ##

Anaconda 安装包可以到 https://mirrors.tuna.tsinghua.edu.cn/anaconda/archive/ 下载。

各系统都可以通过修改用户目录下的 .condarc 文件。Windows 用户无法直接创建名为 .condarc 的文件，可先执行 `conda config --set show_channel_urls yes` 生成该文件之后再修改。



    channels:
      - defaults
    show_channel_urls: true
    default_channels:
      - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
      - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
      - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
    custom_channels:
      conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
      msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
      bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
      menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
      pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
      simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud

即可添加 Anaconda Python 免费仓库。

运行 conda clean -i 清除索引缓存，保证用的是镜像站提供的索引。

运行 conda create -n myenv numpy 测试一下吧。

    #创建python3.6环境,名称为python3.6,可按照实际环境名称修改
    conda create -n python3.6 python=3.6
    
    #移除环境
    conda remove -n py3 --all

    #进入指定的环境
    conda activate python3.6

    #退出当前环境
    conda deactivate

pip镜像设置

    pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple



requirements.txt 文件生成与安装

pip批量导出包含环境中所有组件的requirements.txt文件

     pip freeze > requirements.txt

pip批量安装requirements.txt文件中包含的组件依赖

    pip install -r requirements.txt

conda批量导出包含环境中所有组件的requirements.txt文件

    conda list -e > requirements.txt

conda批量安装requirements.txt文件中包含的组件依赖

    conda install --yes --file requirements.txt
