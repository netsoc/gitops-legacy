# Flux CD bootstrap

Set up SOPS as in [sops.md](sops.md) first.

```bash
kubectl apply -f k8s/flux/_namespace.yaml
# Import PGP key as secret
sops -d k8s/flux/pgp.yaml | kubectl apply -f -
yq r k8s/flux/flux.yaml spec.values | helm install flux -f - -n flux fluxcd/flux

# After it's running, grab the SSH pubkey and add to the repo
fluxctl identity

# Install Helm operator
yq r k8s/flux/helm-operator.yaml spec.values | helm install helm-operator -f - -n flux fluxcd/helm-operator
```
