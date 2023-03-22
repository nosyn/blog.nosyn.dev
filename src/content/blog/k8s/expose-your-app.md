---
title: Using a Service to Expose Your App
author: Son Nguyen
pubDatetime: 2023-03-19T20:56:07-05:00
postSlug: expose-app
featured: true
draft: false
tags:
  - kubernetes
  - k8s
  - cloud
  - clusters
  - pods
  - nodes
ogImage: ""
description: How to use a Service in Kubernetes to expose an application outside the cluster and the use of labels and LabelSelector objects in relation to Services.
---

# Overview of Kubernetes Services

Kubernetes [Pods](https://kubernetes.io/docs/concepts/workloads/pods/) have a [lifecycle](https://kubernetes.io/docs/concepts/workloads/pods/pod-lifecycle/) and are not permanent, and if a worker node dies, the Pods on that node are also lost. However, a [ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/) can create new Pods to restore the desired state of the cluster. Each Pod in the cluster has a unique IP address, so changes among Pods need to be reconciled automatically to ensure the application continues to function properly.

In Kubernetes, a Service is a way to define a group of Pods and access them using a policy. Services allow for a decoupling of Pods, and are defined using [YAML](https://kubernetes.io/docs/concepts/configuration/overview/#general-configuration-tips) or JSON with a LabelSelector to determine the targeted set of Pods.

In Kubernetes, Pods have unique IP addresses, but these addresses are not accessible outside of the cluster without the use of a Service. Services enable applications to receive traffic and can be exposed in various ways by defining a `type` in the ServiceSpec:

- **_ClusterIP_** (default) - Exposes the Service on an internal IP in the cluster. This type makes the Service only reachable from within the cluster.
- **_NodePort_** - Exposes the Service on the same port of each selected Node in the cluster using NAT. Makes a Service accessible from outside the cluster using <NodeIP>:<NodePort>. Superset of ClusterIP.
- **_LoadBalancer_** - Creates an external load balancer in the current cloud (if supported) and assigns a fixed, external IP to the Service. Superset of NodePort.
- **_ExternalName_** - Maps the Service to the contents of the externalName field (e.g. foo.bar.example.com), by returning a CNAME record with its value. No proxying of any kind is set up. This type requires v1.7 or higher of kube-dns, or CoreDNS version 0.0.8 or higher.

In some cases with Kubernetes Services, a `selector` is not defined in the spec. When a `selector` is not defined, the corresponding Endpoints object is not created, allowing users to manually map a Service to specific endpoints. Another reason why a selector may not be used is when strictly using `type: ExternalName`.

# Services and Labels

Kubernetes Services enable traffic to be directed to a group of Pods, and provide a layer of abstraction that allows for the replication and replacement of Pods without affecting the application. Services also handle the discovery and routing among dependent Pods, such as the frontend and backend components of an application.

In Kubernetes, Services use [labels and selectors](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels) to match a group of Pods. Labels are key/value pairs that are attached to objects and allow for logical operations on objects in Kubernetes. Labels can be used in a variety of ways.

- Designate objects for development, test, and production
- Embed version tags
- Classify an object using tags

![services-and-labels](https://d33wubrfki0l68.cloudfront.net/7a13fe12acc9ea0728460c482c67e0eb31ff5303/2c8a7/docs/tutorials/kubernetes-basics/public/images/module_04_labels.svg "services-and-labels")

**_References_**:

- https://kubernetes.io/docs/tutorials/kubernetes-basics/expose/expose-intro/
