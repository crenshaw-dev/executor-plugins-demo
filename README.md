# Argo Workflows Executor Plugin Demo

Demo of an Argo Workflows executor plugin diffing an Argo CD app and writing the diff as a GitHub PR comment

## Setup

```shell
kubectl create namespace argocd
kubectl create namespace argo
kubectl create namespace argo-events
kubectl apply -k .
# Give it a few seconds to install, then get the initial admin password:
kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}"  | base64 -d; echo
```

In a different terminal, start port-forwarding. Then open http://localhost:8080 in your browser.
Log in using the username `admin` and the password retrieved above.

```shell
kubectl port-forward svc/argocd-server -n argocd 8080:443
```
