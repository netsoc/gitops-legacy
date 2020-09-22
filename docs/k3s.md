# k3s on Ubuntu one node setup (temp)

k3s was installed with `curl -sfL https://get.k3s.io | INSTALL_K3S_EXEC="--disable=traefik --disable=local-storage --node-external-ip=80.111.124.111" sh -`

Ports 22, 80, 443 and 6443 were allowed via `sudo ufw allow`.
