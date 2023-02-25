---
title: Kubernetes Clusters
author: Son Nguyen
pubDatetime: 2023-02-15T21:59:38-06:00
postSlug: kubernetes-clusters
featured: true
draft: false
tags:
  - kubernetes
  - k8s
  - cloud
  - clusters
description: Basic of a Kubernetes cluster and Minikube and basic commands to interact with Kubernetes cluster and Minikube
---

# What is a Kubernetes Clusters

> Kubernetes coordinates a highly available cluster of computers that are connected to work as a single unit.
> Kubernestes automates the distribution and scheduling of application containers across a cluster in a more efficient way.

A Kubernetes cluster consists of two types of resources:

- The **Control Plane** coordinates the cluster
- **Nodes** are the workers that run applications

## Cluster Diagram

![cluster-diagram](https://d33wubrfki0l68.cloudfront.net/283cc20bb49089cb2ca54d51b4ac27720c1a7902/34424/docs/tutorials/kubernetes-basics/public/images/module_01_cluster.svg "cluster-diagram")

- The **_Control Plane_** is responsible for managing the cluster.
- A **_node_** is a **_Virtural Machine (VM)_** or **_a physical computer_** that serves as **_a worker machine_** in a Kubernetes cluster. Each **_node_** has **_a Kubelet_**, which is an agent for managing the node and communicating with the Kubernetes control plane.
- The **_nodes_** communicate with the control plane using the [**_Kubernetes API_**](https://kubernetes.io/docs/concepts/overview/kubernetes-api/)
- **_A Kubernetes cluster_** can be deployed on either physical or virtual machines.

## Minikube

- **_Minikube_** is a lightweight Kubernetes implementation that creates a VM on local machine and deploys a simple cluster containing only **_none node_**. **_Minikube_** can be used to get started with **Kubernetes development**.
- The **_Minikube CLI_** provides basic bootstrapping operations for working with your cluster, including **start**, **stop**, **status**, and **delete**.

## Get your hands dirty

### Prerequisties

- [minikube](https://minikube.sigs.k8s.io/docs/start/)
- [kubectl](https://kubernetes.io/docs/tasks/tools/)

### Commands

1. Check **minikube** version

```
minikube version
```

![minikube_version](/assets/content/k8s/minikube_version.png "minikube version")

2. Start **minikube**

```
minikube start
```

![minikube_start](/assets/content/k8s/minikube_start.png "minikube start")

3. Check **kubectl** version

```
kubectl version
```

![kubectl_version](/assets/content/k8s/kubectl_version.png "kubectl version")

4. Check **cluster** info

```
kubectl cluster info
```

![kubectl_cluster-info](/assets/content/k8s/kubectl_cluster-info.png "kubectl cluster-info")

5. Get cluster's **nodes**

```
kubectl cluster nodes
```

![kubectl_get_nodes](/assets/content/k8s/kubectl_get_nodes.png "kubectl get nodes")
