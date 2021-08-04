---
title: "Jupyter Notebook使用Anaconda虚拟环境"
date: 2021-08-04T20:41:06+08:00
draft: false
weight: 70
keywords: ["python","Jupyter"]
description: "Jupyter Notebook使用Anaconda虚拟环境"
tags: ["python","Jupyter"]
categories: ["python","Jupyter"]
author: "码魂"
url: "2021/08/04/jupyternotebook-use-anaconda-env"
---
## Jupyter Notebook使用Anaconda虚拟环境 ##

第一步：安装ipykernel：
法一：
1.进入虚拟环境

Windows：在Anaconda Prompt, 运行 activate myenv
macOS & Linux, 在Terminal, 运行 source activate myenv
安装ipykernel：conda install ipykernel
法二：
在任何环境下都可以直接运行conda install -n myenv ipykernel为myenv安装ipykernel

第二步：将环境写入notebook的kernel中
首先要保证在当前虚拟环境下，进入虚拟环境的过程如第一步的法一。
运行python -m ipykernel install --user --name=myenv 将环境写入notebook的kernel中

生成配置文件:

``` shell
jupyter notebook --generate-config
```

生成密码

输入ipython后

``` python
from notebook.auth import passwd

passwd()
```

修改配置文件

``` python
c.NotebookApp.ip='*' 
c.NotebookApp.notebook_dir = '/home/ozh/share'#共享目录
c.NotebookApp.password = u'sha1:5df252f58b7f:bf65d53125bb36c085162b3780377f66d73972d1' #填写刚刚生成的密文  
c.NotebookApp.open_browser = False # 禁止notebook启动时自动打开浏览器(在linux服务器一般都是ssh命令行访问，没有图形界面的。所以，启动也没啥用)  
c.NotebookApp.port =8899 #指定访问的端口，默认是8899  

c.NotebookApp.allow_remote_access = True
```

启动

``` shell
jupyter notebook --port=8890 --allow-root
```



如果要输出图形，请安装

``` shell
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

pip/conda install matplotlib

pip install akshare --upgrade

pip install backtrader

pip install tushare

conda install scipy

anaconda search -t conda tensorflow

conda install tensorflow

conda install pytorch

conda install sympy
```



    # backtrader兼容性问题
    pip uninstall matplotlib
    pip install matplotlib==3.2.2

conda activate py3

nohup jupyter notebook --port=8890 --allow-root > /root/jupyternotebook.log 2>&1 &



    conda activate py3
    nohup jupyter notebook --port=8890 --allow-root --NotebookApp.terminals_enabled=False > /root/jupyternotebook.log 2>&1 &
    # 禁用控制台命令行
    --NotebookApp.terminals_enabled=False
    

## xeus-cling 安装

conda create -n xeus-cling python=3.6

conda activate xeus-cling

conda install -c conda-forge xeus-cling

Anaconda3的安装路径下的/envs/xeus-cling/share/jupyter/kernels/下

    jupyter kernelspec install PREFIX/share/jupyter/xcpp11 --sys-prefix
    jupyter kernelspec install PREFIX/share/jupyter/xcpp14 --sys-prefix
    jupyter kernelspec install PREFIX/share/jupyter/xcpp17 --sys-prefix

    jupyter kernelspec install /root/anaconda3/envs/xeus-cling/share/jupyter/kernels/xcpp11 --sys-prefix
    jupyter kernelspec install /root/anaconda3/envs/xeus-cling/share/jupyter/kernels/xcpp14 --sys-prefix
    jupyter kernelspec install /root/anaconda3/envs/xeus-cling/share/jupyter/kernels/xcpp17 --sys-prefix

/root/anaconda3/envs/xeus-cling/share/jupyter/kernels



    firewall-cmd --zone=public --add-port=8891/tcp --permanent
    firewall-cmd --reload



    conda activate xeus-cling
    nohup jupyter notebook --port=8891 --allow-root --NotebookApp.terminals_enabled=True > /root/jupyternotebookc.log 2>&1 &



cmake 安装

yum install -y gcc gcc-c++ make automake

https://cmake.org/download/

sh  cmake-3.21.1-linux-x86_64.sh --prefix=/usr/local --exclude-subdir



    yum install  -y openssl  openssl-devel 
    cd finarthur-master
    mkdir build
    cd build
    cmake ..
    make




## 低延时调优文章

https://zhuanlan.zhihu.com/p/59242346

安装 openonload

    ## 进入相应的文件夹
    cd openonload-201811/
    
    ## 源代码存放
    cd scripts/
    
    ## 搭建环境
    ./onload_build
    ## 执行安装
    ./onload_install
    #加载 onload
    onload_tool reload

    ## 停止 cpuspeed 服务以避免进入省电模式，降低CPU时钟速度
    systemctl stop cpuspeed
    
    ## 停止 irqbalance 服务器以防止 OS 在可用的CPU内核之间重新平衡中断
    systemctl stop irqbalance
    
    ## 停止防火墙辐射器以消除简介消耗
    systemctl stop firewalld
    
    ## 禁用 interrupt moderation
    ethtool -C enp1s0f1 rx-usecs-irq 0 adaptive-rx off
    
    ## 启动低延时配置：tuned-adm
    tuned-adm list
    tuned-adm profile network-latency
    
    ## 防止系统进入 CPU 低功耗模式　cstates
    ## 参考博文: https://williamlfang.github.io/post/2019-12-11-linux-调整-cstate-实现cpu超频/
