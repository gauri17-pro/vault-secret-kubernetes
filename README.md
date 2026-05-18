# Using Hashicorp vault for managing our secrets in Kubernetes

## Prerequisites

1. Install kubectl: https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/
2. Install helm: https://helm.sh/docs/intro/install/

## Install hashicorp vault on the cluster

```
helm repo add hashicorp https://helm.releases.hashicorp.com/
helm repo update
helm install vault hashicorp/vault --set "server.dev.enabled=true"
```



