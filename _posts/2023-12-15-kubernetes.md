---
title: Kubernetes
date: 2023-12-15 22:34:00 +0700
categories: [MLOPs, Kubernetes, Docker]
tags: [mlops]     # TAG names should always be lowercase
---

## How to access local Kubernetes minikube dashboard remotely
https://stackoverflow.com/questions/47173463/how-to-access-local-kubernetes-minikube-dashboard-remotely

```
kubectl proxy --address='0.0.0.0' --disable-filter=true
curl http://your_api_server_ip:8001/api/v1/namespaces/kube-system/services/http:kubernetes-dashboard:/proxy/

```

