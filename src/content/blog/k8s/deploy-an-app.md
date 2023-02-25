---
title: Deploy an application on Kubernetes
author: Son Nguyen
pubDatetime: 2023-02-23T11:34:14-06:00
postSlug: deploy-application-to-clusters
featured: true
draft: false
tags:
  - kubernetes
  - k8s
  - cloud
  - clusters
  - deployments
description: Application Deployments and how to deploy an application on Kubernetes with kubectl
---

# Kubernetes Deployments

- To deploy containerized applications on a running Kubernetes cluster, create a `Kubernetes Deployment` configuration.
- The Deployment manages how application instances are created and updated.
- The Kubernetes control plane schedules the instances to run on individual Nodes in the cluster.
- The Deployment Controller continuously monitors the instances and replaces any that fail due to machine failure or maintenance, providing a **_self-healing mechanism_**.
- Kubernetes Deployments offer a fundamentally different approach to application management compared to traditional installation scripts, as they enable recovery from machine failure.

# Deploying app on Kubernetes

![cluster-diagram](https://d33wubrfki0l68.cloudfront.net/8700a7f5f0008913aa6c25a1b26c08461e4947c7/cfc2c/docs/tutorials/kubernetes-basics/public/images/module_02_first_app.svg "cluster-diagram")

## Get your hands dirty

### Prerequisties

- [kubectl](https://kubernetes.io/docs/tasks/tools/)
- [minikube](https://minikube.sigs.k8s.io/docs/start/): **_You need to run `minikube start` before executing commands_**

### Commands

1. Create a new deployment using Google's `kubernetes-bootcamp` image

```
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
```

![create_deployment](/assets/content/k8s/create_deployment.png "create a deployment")

2. Create a new deployment using Google's `kubernetes-bootcamp` image

```
kubectl create deployment kubernetes-bootcamp --image=gcr.io/google-samples/kubernetes-bootcamp:v1
```

![create_deployment](/assets/content/k8s/create_deployment.png "create a deployment")

3. Terminal 1: Create a proxy

> In Kubernetes, Pods are running on a private network that is visible to other Pods and services within the same cluster, but not externally. When using `kubectl, users can interact with their application through an API endpoint, and a proxy can be created to forward communications into the cluster-wide private network.

```
echo -e "\n\n\n\e[92mStarting Proxy. After starting it will not output a response. Please click the first Terminal Tab\n";
kubectl proxy
```

![create_proxy](/assets/content/k8s/create_proxy.png "create proxy")
**_The proxy can be terminated by pressing control-C and does not display any output while running._**

4. Terminal 2: `curl` the proxy

```
curl http://localhost:8001/version
```

![curl](/assets/content/k8s/curl_1.png "curl")
**_The proxy can be terminated by pressing control-C and does not display any output while running._**

5. Get the and export pod name:
   > The API server will automatically create an endpoint for each pod, based on the pod name, that is also accessible through the proxy.

```
export POD_NAME=$(kubectl get pods -o go-template --template '{{range .items}}{{.metadata.name}}{{"\n"}}{{end}}')
echo Name of the Pod: $POD_NAME
```

![export pod name](/assets/content/k8s/export_pod_name.png "export pod name")

6. Access the Pod

```
curl http://localhost:8001/api/v1/namespaces/default/pods/$POD_NAME/
```

![access pod](/assets/content/k8s/access_pod.png "access pod")

**_In order for the new deployment to be accessible without using the Proxy, a Service is required which will be explained in the next post._**
