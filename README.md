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

Create a GitHub API token. Grant it read/write access on pull requests and read access on webhooks.

Create a secret with the token:

```shell
# Copy your token to the clipboard, then write it to a file:
pbpaste > token
```

Configure a webhook to point to `https://<your public IP address>/push`.

* Use Content type `applicaton/json`
* Create a new, secure secret and write it to a file called `secret` (`pbpaste > secret`)
* Disable SSL verification - this is a demo, so we're not using a real certificate
* Only enable Pull request events

```shell
kubectl create secret generic github-access --from-file token --from-file secret -n argo-events
```
