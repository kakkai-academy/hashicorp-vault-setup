# Install
```
helm repo add hashicorp https://helm.releases.hashicorp.com

helm repo update

kubectl create ns secret-management

helm install consul hashicorp/consul -n secret-management --version 0.34.1 -f consul_values_dev.yaml

helm install vault hashicorp/vault -n secret-management --version 0.16.1 -f vault_values_dev.yaml
```

# Vault Operator Init Step
```
vault operator init
```

# Vault Unseal Step
- unseal by ssh to each pod and then fill unseal key 3 times by unique key per node
```
vault operator unseal
```

# Operations
```
ssh -L 8200:localhost:8200 <your-user>@34.126.74.170 -v

kubectl port-forward svc/vault-ui 8200:8200 -n secret-management

enter url to http://127.0.0.1:8200/ui
```

# Kubernetes Auth

https://learn.hashicorp.com/tutorials/vault/agent-kubernetes


# Uninstall HashiCorp Vault 
```
helm uninstall vault -n secret-management
helm uninstall consul -n secret-management
```