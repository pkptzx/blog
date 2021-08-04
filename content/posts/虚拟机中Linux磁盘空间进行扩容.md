---
title: "虚拟机中Linux磁盘空间进行扩容"
date: 2021-08-04T20:48:07+08:00
draft: false
weight: 70
keywords: ["linux","esxi","VM"]
description: "虚拟机中Linux磁盘空间进行扩容"
tags: ["linux","esxi","VM"]
categories: ["linux","esxi","VM"]
author: "码魂"
url: "2021/08/04/linux-expansion"
---
虚拟机中Linux磁盘空间进行扩容

直接在虚拟机中对Linux进行磁盘容量扩容,如果有快照必须先删除快照再扩容.

然后重启虚拟机

查看磁盘空间信息

fdisk -l

增加分区

fdisk /dev/sda

输入n

输入p

按照分区信息输入下一个编号(3)

使用默认的起始扇区和结束扇区,两次回车,输入t,设置分区类型为8e

输入w保存分区信息

重启

初始化分区加入卷组

    #查看卷组信息
    vgdisplay
    #初始化创建的卷组
    pvcreate /dev/sda3
    #查看卷组信息,记住卷组名称
    vgdisplay
    #将初始化的分区加入到虚拟卷组
    vgextend VolGroup /dev/sda3
    #扩展逻辑卷的大小,使用df -lh查看逻辑卷名称
    lvextend -L +20G /dev/mapper/VolGroup-lv_root
    #查看文件系统格式
    cat /etc/fstab
    #扩容重新加载逻辑卷
    xfs_growfs /dev/mapper/centos-home
    #查看修改后的容量
    df -lh
    
    
    


