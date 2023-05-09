---
title: Report 3
abbrlink: 87c3e6d5
date: 2023-05-08 10:15:13
tags:
categories: Cloud Native
cover: 'http://img.note4u.top/base/cnnotes_cover.jpg'
hide: true
---

## 学习内容

### Docker
- 借助官网文档与实例，学习使用 dockerfile 构建 docker 镜像。对 FROM、RUN、ARG 等命令的用法进行了学习与总结。
    - 整理：[使用 Dockerfile 构建镜像](http://note4u.top/post/78184262.html)
- 学习构建镜像的同时，熟悉 docker 相关的一些基本命令。
    - 整理：[Docker 命令](note4u.top/post/f0295783.html)

### K8s
- 《k8s in action》三到六章
    - 第三章：pod的作用、标签与选择器、注解、命名空间等
        - 整理：[《K8S in Action》第三章笔记](http://note4u.top/post/37731fc2.html)
    - 第四章：存活探针、ReplicationController、ReplicaSet、Service、DaemonSet、Job、CronJob 等
    - 第五章：Service、Ingress、就绪探针等
    - 第六章：Volume 等
- 使用 minikube 与 kind 构建 k8s 集群
    - 了解 k8s sigs
    - 了解 k3d、k3s、kind、microk8s、minikube 区别
    - k8s 的组件构成：etcd、apiserver、controller manager、scheduler…. 等
    - 了解 minikube 的架构
- 阅读《k8s in action》的同时，使用 minikube 进行实践，对常见的一些命令进行总结。
    - 通过实际命令熟悉 kubectl 的使用
    - 了解 kubectl 的插件功能
- client-go
    - 结果官方文档与实例了解 RESTClient、DynamicClient、CilentSet、DiscoveryClient 的使用方法
    - 使用 client-go 获取 k8s 集群的一些基本信息

## 小结
- Docker
    - 已基本掌握 docker 与 dockerfile 的使用，但实践不足，命令记不住。
    - Docker 背后的原理有所欠缺，尤其是 UnionFS 这一块。
- K8S
    - 对 K8S 的构成，即 etcd、apiserver、scheduler 等有了基本的认识
    - 了解 RelicaSet、Service 等 K8S 资源对象，能够通过命令行与 yaml 文件进行创建与管理。
    - 能够通过 ReplicationController、ReplicaSet 等对 pod 的数量进行监控，修改配置可以手动横向扩容。
    - 了解标签的作用，可以在命令行中通过标签进行筛选，或通过标签将 pod 调度至特定的工作节点上。
    - 能够通过 Volume 来访问外部磁盘存储
    - pod 之间的通信，服务（Service）的暴露等相关内容，还有一些混乱，亟待学习与梳理。
    - 能够使用 client-go 获取 k8s 集群的一些基本信息，但还没有深入到对 pod 的操作上（比如 eviction）。

## 后续计划
- 5月：
    - 《k8s in action》学习 
        - k8s 的一些资源对象，比如 Deployment 等
        - 重点学习第十一章：了解 Kubernetes 机理（涉及 pod 间通信等）
    - 对以下内容进行了解与学习
        - Reflector(反射器)
        - DeletaFIFO(增量队列)
        - Indexer(索引器)
        - Controller(控制器)
        - SharedInformer(共享资源通知器)
        - processorListener(事件监听处理器)
        - workqueue(事件处理工作队列) 
    - 完成以下实践
        - 在实践的过程中，发现问题，并解决问题，带着目的去学习      
![20230508153658](http://img.note4u.top/article/20230508153658.png)

- 6月：
    - Flink 相关内容的学习