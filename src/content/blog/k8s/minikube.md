---
title: Minikube and Kubernetes
author: Son Nguyen
pubDatetime: 2023-02-7T05:17:19Z
postSlug: minikube-and-introduction-to-k8s
featured: true
draft: true
tags:
  - kubernetes
  - k8s
  - cloud
  - minikube
description: This is the example description of the example post.
---

1. Minikube: A local Kubernetes, focusing on making it easy to learn and develop for Kubernetes.
2. Pod: A Kubernetes Pod is a group of one or more Containers, tied together for the purposes of administration and networking. The Pod in this tutorial has only one Container.
3. Deployment: A Kubernetes Deployment checks on the health of your Pod and restarts the Pod's Container if it terminates. Deployments are the recommended way to manage the creation and scaling of Pods.
4. Create the deployment

```script
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
```

![create deployment](/public/assets/content/k8s/create_deployment.png) 2. View the Deployment

```
kubectl get deployments
```

3.
