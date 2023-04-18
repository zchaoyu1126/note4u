---
title: 云原生学习笔记
categories: Cloud Native
abbrlink: 606938d0
date: 2023-01-07 21:31:08
tags:
sticky: 9
cover: http://img.note4u.top/base/cloud_native_cover.jpg
---

本系列写于第一次接触云计算与云原生，在此之前也没有参与过一个软件工程的全生命周期，对软件的部署、交付、运维等这一块了解不多。此外，之前在校开发的一些应用都属于单体架构，对基于分布式、微服务等应用的了解不够深入。
希望能在日后工作的实践中，逐渐加深理解，并对本文进行完善与补充。

## Accomplished
[001 云计算与云原生基本概念](http://note4u.top/post/6328194b.html)
[002 虚拟机与容器、Docker与K8S常见混淆点梳理](http://note4u.top/post/757d0b1c.html)
[004 Docker 命令](http://note4u.top/post/f0295783.html)
[005使用 Dockerfile 构建镜像](http://note4u.top/post/78184262.html)

## In hand
- [003 Docker 安装与入门]
- [006 使用 minikube 搭建 k8s 环境]
- [007 kubectl 命令]
- [008 K8S 组件与概念]
  - kubectl、Master、Node、API Server、Scheduler、etcd、Proxy、CoreDNS、Dashboard
  - pod、ReplicationController、ReplicaSet、Deployment、Service、Ingress、ConfigMap、Secrets

## To do list
Flink:  
- 掌握Flink的核心概念，包括WaterMark/State/Window/ExecutionGraph等，熟悉主要流程，包括 资源配置/作业拓扑/作业启动/checkpoint生成/Failover流程 等。
- 在Flink官网上购买一个试用的集群(费用较高，仅首月有优惠），熟悉基本的sql+datastream作业编写，配置调优，作业运维流程，会写作业，会排查简单的作业问题（延时，Fo)。
  
K8S:
- ~~了解k8s的设计理念，理解包括申明式API、控制机制、cni/csi/cri等~~。
- 学习云原生架构概念，包括Serverless、OAM等。
- 通读《k8s in action》+ k8s 官方文档，深入学习 k8s 调度+资源管理 内容。
- 基于 docker 熟悉容器虚拟化技术，深入学习 镜像 + unionFS 相关知识。

Go:
- 实现一个简易的重调度，并基于 docker 熟悉构建，打包，发布，部署流程（minikube）方法通过 minikube 环境，和 client-go 客户端的学习，自己搭建一套怎么通过「client-go」来获取 k8s resource（比如 pod, node..）的信息，并且根据自己的简单决策算法（比如 podName = "shouldEvict"），对 pod 进行操作（比如 eviction） 
  - 标准基本标准： 「能够使用 client-go，获得 pod, node 信息，根据这些信息，设置一些简单的判断条件，最后调用 k8s v1/core eviction 的原生 api，对 pod 进行驱逐」
  - 高阶标准： 「能自己写 informer ，或者 reflector（list & watch），获取 自定义的 CR 信息，根据这些信息，设置一些简单的判断条件进行驱逐」

SRE业务场景：
- 学习 FFA 中关于 inspector 的介绍。