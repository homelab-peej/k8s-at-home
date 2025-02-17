# Setup your own Kubernetes cluster on Raspberry Pi

### Important Notes
- The steps below were all done on Raspberry Pi 5 8GB
- This [POE M.2 Hat+](https://www.waveshare.com/poe-m.2-hat-plus.htm) was used to provide a M.2 slot for boot and PoE for a rack install
- Running Kubernetes off of a MicroSD card under normal circumstances will likely impact performance and burn out the card quickly
- Use a USB 3.0 drive or NVMe for best results

## Install Raspbian
- Install [Raspberry Pi Imager](https://www.raspberrypi.com/software/) on your system
- Scroll to `Misc Utility Images` and install the `NVMe/USB Boot` configuration to a MicroSD card
- Install `Raspberry Pi OS Lite (64-bit)` on your USB or M.2 NVMe drive
- Insert the MicroSD card and power the Pi, waiting for the LED to steadily blink and a green screen output via HDMI to indicate success ([documentation](https://www.raspberrypi.com/documentation/computers/raspberry-pi.html#bootloader_update_stable)), power off, and remove the MicroSD card
- Install your USB or M.2 drive and power back on to boot
- Add `cgroup_memory=1 cgroup_enable=memory` to `/boot/firmware/cmdline.txt`
- Run `sudo apt update && sudo apt upgrade`
- Reboot

## Choose your Kubernetes Flavor
- [K3S](SETUP-k3s.md) - easy  
- [kubeadm](SETUP-kubeadm.md) - hard  

## Install [Cilium CNI](https://docs.cilium.io/en/stable/installation/k3s/)

- Get the [Cilium CLI](https://docs.cilium.io/en/stable/installation/k3s/#install-cilium) for your client
- Ensure you have configured your `KUBECONFIG` variable
- Install Cilium with `cilium install --version 1.17.1 --set=ipam.operator.clusterPoolIPv4PodCIDRList="10.42.0.0/16"`
- Monitor the install with `cilium status --wait`
- Check your cluster with `kubectl get node` and `kubectl get po -A`
- OPTIONAL: Enable [Hubble observability](https://docs.cilium.io/en/stable/observability/hubble/setup/#setting-up-hubble-observability) with `cilium hubble enable`

## OPTIONAL: Setup [Flux](https://fluxcd.io/flux/) to explore Continuous Delivery and GitOps
- Download the latest [release binary](https://github.com/fluxcd/flux2/releases)
- Extract and move `flux` to `/usr/local/bin`
- Run `chmod +x /usr/local/bin/flux`
- Run `flux version` and verify output
- Run `flux check --pre` and verify output
- Bootstrap the cluster with the command  
```
flux bootstrap github \
  --token-auth \
  --owner=homelab-peej \
  --repository=k8s-at-home \
  --branch=main \
  --path=flux-bootstrap \
  --interval 1h \
  --timeout=15m \
  --components source-controller,kustomize-controller,helm-controller,notification-controller \
  --components-extra image-reflector-controller,image-automation-controller
```
