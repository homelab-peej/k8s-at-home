# Setup Kubernetes the Hard Way with `kubeadm`

- Set proxy variables for the system in `/etc/environment`
- Write all IP addresses and hostnames for cluster resources in `/etc/hosts`
- Verify SELinux is disabled
- Set firewall rules
- Disable swap with `sudo systemctl disable --now dphys-swapfile.service`

Follow the directions [here](https://kubernetes.io/docs/setup/production-environment/container-runtimes/#containerd) and [here](https://github.com/containerd/containerd/blob/main/docs/getting-started.md) to setup containerd. 

🚨 **Important** 🚨 - when installing the CNI plugins, verify ownership of `/opt/cni/bin` is set to `root`

For containerd, you'll need to enable the kernel modules `overlay` and `br_netfilter`. Add those two modules to `/etc/modules-load.d/modules.conf` so they load on reboot. Also add the following lines to `/etc/sysctl.d/kubernetes.conf` and reload with `sysctl --system` after saving.
```
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
net.ipv4.ip_forward = 1
```

Install the Kubernetes components following the directions [here](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/#install-using-native-package-management).

If the system is using GPU accelerators, install the necessary system drivers as well as the container toolkit following the directions [here](https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/latest/install-guide.html#installing-with-apt). Verify that all GPUs are visible by the driver by running `nvidia-smi`.

🚨 **Important** 🚨- some systems may require an additional grub parameter `pci=realloc=off` to see all GPUs.
