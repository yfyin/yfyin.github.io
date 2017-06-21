---
title: openshift features
date: 2017-06-20 16:01:36
categories: [Technology]
tags: [openshift,PaaS]
---

Kernel concept: 
Based on kubernetes, naturally inherit the powerful features provided by k8s, such as applicatioin depoyment, scaling, LB etc.

features:

# Management 
- Node 
- User
- Project
- Pod
- Networking
- Volume
- Quota

# Security
- Multi-tenancy
- IPSec and Firewall
- Service accounts
- Users and groups
- Authorization Policies, to control API access
- Image Policy, to control which images are allowed to run on your cluster
- Scoped Tokens, to empower another entity with limited authority
- Security context constraints, to control permissions for pods
- Secure docker buildConfig, via secret file, see [secure build](https://docs.openshift.org/latest/security/build_process.html#security-build)
- Container Content Scanning with External Scanning Tools

# Automation
- Building, using Source-to-Image toolkit for creating image directly from source code
- Deployment, based on Kubernetes
- Infrastructure independent deployment, whether it’s on-premise, in a public cloud, or hosted
- Cluster Monitoring and Auto-Scaling, based on Heapster and Kubernetes horizontal pod autoscalers
- CI/CD, based on jenkins
- Integrated Container Registry, also support third part ones

# Persist Storage
- MySQL
- Postgresql
- MongoDB
- MariaDB

# OPS
- Integrated Web Console 
- Exposed openshift Rest API
- Exposed Kubernetes Rest API  
- Images Monitoring and statistic
- Application Health check, based on Kubenetes, see [here](https://kubernetes.io/docs/user-guide/walkthrough/k8s201/#application-health-checking)
- Backup and restore at cluster level
- Garbage Collection
  - Container garbage collection: Removes terminated containers. Typically run every minute.
  - Image garbage collection: Removes images not referenced by any running pods. Typically run every five minutes. 
Managing Security Context Constraints






