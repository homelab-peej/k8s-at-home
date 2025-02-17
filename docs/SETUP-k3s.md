# Install [K3S](https://docs.k3s.io/quick-start)

- Set proxy variables for the system in `/etc/environment`
- Run `curl -sfL https://get.k3s.io | sh -s - --flannel-backend=none --disable-network-policy --disable=traefik --disable=metrics-server` for your control plane
- Get your `K3S_TOKEN` from `/var/lib/rancher/k3s/server/node-token`
- Run `curl -sfL https://get.k3s.io | K3S_URL=https://myserver:6443 K3S_TOKEN=mynodetoken sh -` for any additional nodes
- Copy contents of `/etc/rancher/k3s/k3s.yaml` on the control plane to `~/.kube/config` on your local machine so you can access your cluster remotely with `kubectl`. Be sure to update the `server` address to the IP of the control plane
