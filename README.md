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

```
helm repo add external-secrets https://charts.external-secrets.io
helm repo update
helm install external-secrets external-secrets/external-secrets --namespace external-secrets --create-namespace --set installCRDs=true
```

## Steps to be followed

1. Create a secret for vault-token
```
kubectl create secret generic vault-token \
  --namespace default \
  --from-literal=token=root
```

2. Add secrets to the vault
```
vault secrets enable -path=apps kv-v2
```

```
vault kv put -mount=apps my-app DB_USERNAME=appuser DB_PASSWORD=apppassword
vault kv put -mount=apps docker-creds docker_username=gauris17 docker_password=Password@123
```

```
vault kv get apps/my-app
```
