---
title: Report 2
abbrlink: f0c4d643
date: 2023-05-08 10:14:49
tags:
categories: Cloud Native
cover: 'http://img.note4u.top/base/cnnotes_cover.jpg'
hide: true
---


## 学习内容

- 快速阅读了《云计算(第三版)》中的重点内容；第一周中提到的几个点做出了自己的解释，并整理成一篇笔记
  - 云计算与云原生的关系
  - 通过阅读《迁移到云原生应用架构》等了解云原生的概念，包括产生原因、目的，云原生的特征，演进过程等。
  - 云计算与分布式计算、分布式文件系统(GFS)等的关系
  - 公有云、私有云、混合云
  - 网格化服务、边车(sidecar)
  - 声明式api与命令式api
    
- 通过查询资料，针对docker、k8s这块的一些常见概念进行梳理总结，并整理为一篇笔记
  - OpenStack、VMware、docker、k8s之间的联系
  - CRI-O、runc、CRI、dockershim、containerd、OCI
  - 容器网络接口(CNI)、容器运行时接口(CRI)和容器存储接口(CSI)

- 阅读了《k8s in action》前三章与其他一些资料，实际操作动手部署了k8s集群。具体地，由于硬件条件的限制，所以选择使用了kind(k8s in docker)来搭建k8s学习环境

- 借助教程[七天用 Go 写个 docker](https://topgoer.cn/docs/seven-docker)等资料学习，学习了docker容器技术基础即cgroup、namespace，unionfs；关于unionfs，主要了解了AUFS和overlay、overlay2。

## 小结

- 目前，对上述1和2已整理了两篇笔记，但还没有发布，之后会将链接附在之后的周报中。
- 关于3和4，在学习过程中有一些零散的记录，等有一定积累之后，再进行梳理与总结。