---
title: "Minikube Lab"
description: "Production-Ready K8s Locally"
type: docs
toc: false
weight: 1
---

# Bringing Production Power to Your Laptop

Testing Kubernetes shouldn't always require a cloud provider and a credit card. This lab is designed to bridge the gap between basic local development and production-grade architecture by utilizing multi-node setups.

---

## What’s Inside

This lab mimics real-world cluster behavior. Instead of a standard single-node setup, we deploy a **multi-node cluster**. This allows us to experiment with:
* **Node Affinity & Anti-affinity:** Control which nodes your pods land on.
* **High Availability:** See what happens when one node "fails."
* **Load Balancing:** Distribute traffic across multiple instances.

## Why Minikube?

Minikube is the industry standard for local K8s for several reasons:

* **Safe Break-Fix:** Intentionally crash components to learn how Kubernetes self-heals.
* **API Consistency:** It uses the same Kubernetes APIs found in EKS, GKE, or AKS.
* **GitOps Ready:** The perfect environment to test ArgoCD or Flux pipelines locally.

> 🧪 **Lab Environment:**
> - **Driver:** Docker
> - **K8s Version:** v1.29+
> - **OS:** macOS

---

## Setup Guide

### 1. Install the Tools
If you are on macOS, use Homebrew. For other OSs, visit the official Docker and Minikube download pages.

```bash
brew install minikube
brew install docker
```

### 2. Start Docker

Ensure your Docker engine is active before proceeding:

```bash
open -a docker
```

### 3. Provision the Cluster

We will launch a cluster named shivam-k8s with two nodes. This creates a Control Plane and a Worker node.

```bash
minikube start --nodes=2 -p shivam-k8s
```

### 4. Deploy a Test Workload

K8s Imperative commands to create Deployment and Service:

```bash
kubectl create deploy shivam-deploy --image=vimal13/apache-webserver-php --replicas=2 
kubectl expose deploy shivam-deploy --type=NodePort --port=8080 --target-port=80
```

### 5. Expose and Access

Minikube makes it easy to access your NodePort service without complex networking rules:

```bash
minikube service shivam-deploy url -p shivam-k8s
```

This command will output a URL. Copy and paste it into your browser to see the landing page live!

### 6. Clean Up

When you're finished with your lab, you can stop or delete the cluster to save system resources:
Bash

**To pause the lab**
```bash
minikube stop -p shivam-k8s
```


**To delete everything**
```bash
minikube delete -p shivam-k8s
```