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

## Running To concurrent k8s env
```shell
kind create cluster --wait 60s --name cluster-1 && \
kind create cluster --wait 60s --name cluster-2
```
see the list of running clusters
```shell
kind get clusters
```
to see the docker container running
```shell
docker ps
```
interact with the cluster using kubectl
```shell
kubectl get nodes
kubectl --context kind-cluster-1 get nodes
kubectl --context kind-cluster-2 get nodes
```
have look at the change in  ~/.kube/config
```shell
cat ~/.kube/config
```
to delete the clusters
```shell
kind delete cluster --name cluster-1 && \
kind delete cluster --name cluster-2
```
## Setting up a multi-node cluster
```shell
kind create cluster --wait 60s --name multi-cluster --config=cluster-config.yaml
```
viewing nodes
```shell
kubectl get nodes
docker ps
docker stats
```
installing ingress
```shell
kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/static/provider/kind/deploy.yaml
```
let's run an application

```shell
helm create demo
```
edit "demo/values.yaml" file and enable the ingress then replace "chart-example.local" with "localhost" and then install the chart

```shell
helm install demo ./demo/
```
You can view the app via [http://localhost/](http://localhost/) 

To tearing down the cluster use the following domain
```shell
kind delete cluster --name multi-cluster
```
