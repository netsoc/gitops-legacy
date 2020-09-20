# SOPS

Be sure to update the public key in [.sops.yaml](../.sops.yaml).

## PGP key generation

Make sure _not_ to use a passphrase.

```bash
gpg --generate-key
gpg --export-secret-keys --armor <key fingerprint> | \
    k -n flux create secret generic flux-pgp --from-file=flux.asc=/dev/stdin --dry-run=client -o yaml | \
    sops -e --encrypted-regex '^data$' --input-type yaml --output-type yaml /dev/stdin > \
    k8s/flux/pgp.yaml
```

## Create a secret and encrypt it

```bash
kubectl -n my-namespace create secret generic my-secret --from-literal=password=hunter2 --dry-run=client -o yaml | \
    sops -e --encrypted-regex '^data$' --input-type yaml --output-type yaml /dev/stdin > \
    my-secret.yaml
```
