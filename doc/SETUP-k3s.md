# Install [K3S](https://docs.k3s.io/quick-start)

- Set proxy variables for the system in `/etc/environment`
- Run `curl -sfL https://get.k3s.io | sh -s - --flannel-backend=none --disable-network-policy --disable=traefik --disable=metrics-server --disable=local-storage --disable=servicelb` for your control plane
- Get your `K3S_TOKEN` from `/var/lib/rancher/k3s/server/node-token`
- Run `curl -sfL https://get.k3s.io | K3S_URL=https://<myserver>:6443 K3S_TOKEN=<mynodetoken> sh -` for any additional nodes
- Copy contents of `/etc/rancher/k3s/k3s.yaml` on the control plane to `~/.kube/config` on your local machine so you can access your cluster remotely with `kubectl`. Be sure to update the `server` address to the IP of the control plane

**Note: The steps above will setup a single control plane with the default embedded sqlite database. If you want to setup multiple control planes for HA, follow the steps below.**

- Add the `--cluster-init` flag to the 2nd step when starting up your server
    - If your cluster is already running and you want to expand it, edit the service file on your running control plane located at `/etc/systemd/system/k3s.service` and add the `--cluster-init` flag to the `ExecStart` block at the end.
    - Run `sudo systemctl daemon-reload`
    - Run `sudo systemctl k3s restart`
- Add additional servers to your cluster with the command `curl -sfL https://get.k3s.io | K3S_TOKEN=<mynodetoken> sh -s - server --server https://<myserver>:6443 --flannel-backend=none --disable-network-policy --disable=traefik --disable=metrics-server --disable=local-storage --disable=servicelb`
    - IMPORTANT: The options for additional servers must match the options you first install K3S with or you will get an error