# Kubernetes in Docker (kind)
kind is a tool for running local Kubernetes clusters using Docker container “nodes”.
[https://kind.sigs.k8s.io/](https://kind.sigs.k8s.io/)

## Installation

For installation instruction please see: [https://kind.sigs.k8s.io/docs/user/quick-start/#installation](https://kind.sigs.k8s.io/docs/user/quick-start/#installation)


## Creating our first kind cluster
```shell
kind create cluster --wait 60s --name my-first-cluster
```
to see the docker container running 
```shell
docker ps
```
have look at the change in  ~/.kube/config
```shell
 cat ~/.kube/config
```
interact with the cluster using kubectl

```shell
kubectl get nodes
kubectl get po --all-namespaces
```

## Deleting our first kind cluster
```shell
kind delete cluster --name my-first-cluster
```
see the docker container is gone
```shell
docker ps
```
