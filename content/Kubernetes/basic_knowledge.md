---
title: "Basic_Knowledge"
date: 2018-06-02 19:03
---

[TOC]

# 基础知识



## Kubernetes 特性



###自动的调度 Auto Scaling

> 对资源默认的调度



### 服务的自动发现 Service Discovery



### 灰度发布 App Deployment

> 灰度发布（又名金丝雀发布）是指在黑与白之间，能够平滑过渡的一种发布方式。在其上可以进行A/B testing，即让一部分用户继续用产品特性A，一部分用户开始用产品特性B，如果用户对B没有什么反对意见，那么逐步扩大范围，把所有用户都迁移到B上面来。灰度发布可以保证整体系统的稳定，在初始灰度的时候就可以发现、调整问题，以保证其影响度。





## Kubernetes 架构



### Master node

> 包含3个进程

* API Server

  > 提供资源统一的入口

  

* Controller manager

  > 资源的管理和调度（pod调度）

* Scheduler

  > 调度的队列，node的列表



> 使用etcd进行存储





### Worker node

> 包含3个进程

* Kubelet

  > 负责pod对应的容器创建，启动停止等任务
  >
  > 于Master node协同同坐

* Kube proxy

  > 实现kubernetes service 的通信和负载均衡机制的重要组件
  >
  > 缓存代理，通过iptables的nat表实现

* Docker

  > Docker 引擎，负责本机的容器创建和管理工作



## Kubernetes 功能

### Pod

> Pod 是Kubernetes中可以创建的最小部署单元， Pod是一组容器的集合
>
> 每个Pod里面都会有一个pause，大概20k大小。这个pause管理网络，以及容器的状态



#### Pod template

* (Resource)[https://kubernetes.io/docs/concepts/workloads/pods/pod-overview/]

```
apiVersion: v1
kind: Pod
metadata:
  name: myapp-pod
  labels:
    app: myapp
spec:
  containers:
  - name: myapp-container
    image: busybox
    command: ['sh', '-c', 'echo Hello Kubernetes! && sleep 3600']
```



### Label 

> label是一个key=value的键值对，可以附加到各种资源对象上



### Replication Controller

> 定义了一个期望的场景，声明某种pod的副本数量在任意时刻都符合某个预期值



### Deployment

> Deployment 为Pod和ReplicaSet提供一个声明方法，用来替代Replication Controller 来方便管理



### Horizontal Pod Autoscaler

> 对资源实现削峰填谷



#### Metrics 支持

* autoscaling/v1
  * CPU
* autoscaling/v2
  * Memory / Other



### Service

> 一个pod的逻辑分组，一种可以访问它们的策略成为微服务
>
> 一组pod能够被Service 访问到，通常通过Label Selector 实现



#### Endpoint

> Endpoint: Pod IP + Container Port 


​    

​    

​    

​    



