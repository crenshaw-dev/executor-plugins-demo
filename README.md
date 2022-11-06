# Argo Workflows Executor Plugin Demo

Demo of an Argo Workflows executor plugin diffing an Argo CD app and writing the diff as a GitHub PR comment

## Setup

```shell
kubectl create namespace argocd
kubectl create namespace argo
kubectl create namespace argo-events
kubectl apply -k .
```
