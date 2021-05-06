Container + Orchestration

Container - Why containers ??

Libraries , Dependencies having dependency on OS - The  matrix of hell

## Container Orchestration

* **Multiple docker container - Docker Swarm , Kubernetes**
* **Kubernetes support all complex deployments**
* **Scaling feature as per load**

## Kubernetes Architecture

Node - Worker machine where container will be installed(Called Minions)

Cluster - Collection of multiple nodes (in case if node fails or sharing the load)

Master - Master is another node where kubernetes is installed (responsible for actual orchestration)

Components of Kubernetes
--------------------------

Api Server 
etcd Server
Scheduler
Controller(Brain)
Container Runtime
kubelet -(Agent runs of each node)

Master Vs Worker Nodes
-----------------------

Worker Nodes - Container Runtime Installed/Kubelet(communicates with kube api server)

Master - Kuber Api Server/Controller/etcd/Scheduler

```
# Get No of nodes running including master
kubectl get nodes

# Get Version
kubectl get version

# What is the flavour and version of Operating System on which the Kubernetes nodes are running?
kubectl get nodes -o wide
```

Minikube - Single node cluster / microk8s

kubeadm - production grade cluster

Cloud Based Cluster - AKS,GKS 


