---
title: Report 1
abbrlink: 69cd87f9
date: 2023-05-08 10:01:00
tags:
categories: Cloud Native
cover: 'http://img.note4u.top/base/cnnotes_cover.jpg'
hide: true
---

2022.12.26-2023.01.01

## 学习内容

> 本周的学习内容主要集中在对一些概念的查漏补缺，具体如下
> 

- 云计算与云原生的关系
- 通过阅读《迁移到云原生应用架构》等了解云原生的概念，包括产生原因、目的，云原生的特征，演进过程等。
- 云计算与分布式计算、分布式文件系统(GFS)等的关系
- 公有云、私有云、混合云
- OpenStack、VMware、docker、k8s之间的联系
- Devops、网格化服务、边车(sidecar)
- CRI-O、runc、CRI、dockershim、containerd、OCI
- 容器网络接口(CNI)、容器运行时接口(CRI)和容器存储接口(CSI)
- Serverless、OAM
- 声明式api与命令式api

## 小结

- 输入了很多新概念，但没有自己的输出，要整理消化，要有自己的理解
- 云原生涉及的技术很多很复杂，想要完全了解不现实，不能过多纠结。面对庞然大物，容易产生畏难情绪，应先大致了解，然后从小方面切入，再逐步拓展

## 下周计划

- 对上一周的内容进行梳理，并整理成文
- 阅读《k8s in action》，并实际操作动手部署k8s集群
- 学习docker的镜像、UnionFS
    - AUFS、overlay、overlay2、DeviceMapper、VSF
    - LXC、docker、虚拟化技术
    - 阅读《第一本docker书》，进一步学习docker的使用方法
    - 借助教程[七天用 Go 写个 docker](https://topgoer.cn/docs/seven-docker)等资料学习`Namespace` 和`Cgroup`