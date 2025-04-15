# Infrastructure

Apps and services that are essential to a functioning cluster to support the applications that I want to run. Essential to me doesn't necessarily mean essential to you. Some applications below are included with K3S, but may not be as configurable. Installing them separately allows for a more portable install across different cluster environments. Many choices below have alternatives as well.

### [Actions Runner Controller](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller#runner-scale-set)
Actions Runner Controller (ARC) is a Kubernetes operator that orchestrates and scales self-hosted runners for GitHub Actions. With ARC, you can create runner scale sets that automatically scale based on the number of workflows running in your repository, organization, or enterprise. Because controlled runners can be ephemeral and based on containers, new runner instances can scale up or down rapidly and cleanly.

### [Authelia](https://github.com/authelia/authelia)
Authelia is an open-source authentication and authorization server providing two-factor authentication and single sign-on (SSO) for your applications via a web portal. It acts as a companion for reverse proxies by allowing, denying, or redirecting requests.

### [Cert-Manager](https://github.com/cert-manager/cert-manager)
Cert-manager is a X.509 certificate manager for Kubernetes. It adds multiple certificate and issuer resources to your cluster can help you automate obtaininig, renewing, and using your certificates. By using the [DNS challenge](https://cert-manager.io/docs/configuration/acme/dns01/#setting-nameservers-for-dns01-self-check) option we can obtain certificates even for an internal-only domain name. Cert-manager knows that you still control the domain since it can write TXT records back to Cloudflare with your API token. If you have an internal DNS server and use [split-horizon](https://en.wikipedia.org/wiki/Split-horizon_DNS) be sure to add the extraAgs shown above to force cert-manager to use public DNS to authenticate since your internal DNS will not propogate those records.

### [Cilium](https://github.com/cilium/cilium)
Cilium is an open source, cloud native solution for providing, securing, and observing network connectivity between workloads, fueled by the revolutionary Kernel technology eBPF

### [Cloudflare-DDNS](https://github.com/favonia/cloudflare-ddns)
A feature-rich and robust Cloudflare DDNS updater with a small footprint. The program will detect your machine’s public IP addresses and update DNS records using the [Cloudflare API](https://dash.cloudflare.com/profile/api-tokens).

### [CloudNative Postgres Operator](https://github.com/cloudnative-pg/cloudnative-pg)
CloudNativePG is a comprehensive open source platform designed to seamlessly manage PostgreSQL databases within Kubernetes environments, covering the entire operational lifecycle from initial deployment to ongoing maintenance. The main component is the CloudNativePG operator. Deploy a Postgres `Cluster` to [define your deployment](https://cloudnative-pg.io/documentation/1.25/cloudnative-pg.v1/#Cluster).
```
apiVersion: postgresql.cnpg.io/v1
kind: Cluster
metadata:
  name: cluster-example
  namespace: default
spec:
  instances: 3
  storage:
    size: 1Gi
```

### [CSI Driver NFS](https://github.com/kubernetes-csi/csi-driver-nfs)
This driver allows Kubernetes to access NFS servers on both Linux and Windows nodes, plugin name: `nfs.csi.k8s.io`.

### [CSI Driver SMB](https://github.com/kubernetes-csi/csi-driver-smb)
This driver allows Kubernetes to access SMB servers on both Linux and Windows nodes, plugin name: `smb.csi.k8s.io`.

### [Flux Extensions](https://github.com/fluxcd/flux2/)
- [Monitoring Alerts](https://fluxcd.io/flux/monitoring/alerts/) - This guide will help you setup alerts that use the notification controller. Many Flux `kind`s can be monitored and send alerts based on state changes or errors. Cross-namespace references are difficult (by design) so I've done a single secret in `flux-system` as well as the provider which references it. The alert can point to objects in other namespaces so this removes the need for replicating resources across namespaces.
- [Webhook Receivers](https://fluxcd.io/flux/guides/webhook-receivers/) - With cert-manager installed and the ability to create certificates for custom domains, we can turn Flux into a push-based pipeline that will trigger a sync any time there's a commit.

### [GPU Operator](https://github.com/NVIDIA/gpu-operator)
Kubernetes provides access to special hardware resources such as NVIDIA GPUs, NICs, Infiniband adapters and other devices through the device plugin framework. However, configuring and managing nodes with these hardware resources requires configuration of multiple software components such as drivers, container runtimes or other libraries which are difficult and prone to errors. The NVIDIA GPU Operator uses the operator framework within Kubernetes to automate the management of all NVIDIA software components needed to provision GPU. These components include the NVIDIA drivers (to enable CUDA), Kubernetes device plugin for GPUs, the NVIDIA Container Runtime, automatic node labelling, DCGM based monitoring and others.

### [Longhorn](https://github.com/longhorn/longhorn)
Longhorn is a lightweight, reliable and easy-to-use distributed block storage system for Kubernetes. We can use local disks to store data and backup data to TrueNAS and other locations.

### [MetalLB](https://github.com/metallb/metallb)
Bare-metal Kubernetes installs do not have a native load-balancer implementation. This tool lets you dedicate IP addresses to be available to your cluster for [Services of type LoadBalancer](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/) to claim for use. I'll set one address aside specifically for a reverse-proxy to use with a DNS name, and I'll have another small pool available for other random stuff. See [basic L2 configuration](https://metallb.io/configuration/) to get started.

### [Node Feature Discovery](https://github.com/kubernetes-sigs/node-feature-discovery)
Node Feature Discovery is an addon to detect node capabilities for Kubernetes. It detects hardware features available on each node in a Kubernetes cluster, and advertises those features using node labels and optionally node extended resources, annotations and node taints. Node Feature Discovery is compatible with any recent version of Kubernetes (v1.24+).

### [Reloader](https://github.com/stakater/reloader)
Reloader will watch many resources for `ConfigMap` or `Secret` changes and automatically rollout an update for those changes. Simply add the annotation `reloader.stakater.com/auto: "true"` to your Deployment `.metadata`. See the [documentation](https://github.com/stakater/reloader#how-to-use-reloader) for more examples.

### [System Upgrade Controller](https://github.com/rancher/system-upgrade-controller)
This project aims to provide a general-purpose, Kubernetes-native upgrade controller (for nodes). It introduces a new CRD, the `Plan`, for defining any and all of your upgrade policies/requirements. A `Plan` is an outstanding intent to mutate nodes in your cluster. This is the recommended way to automate K3S updates according to the [documentation](https://docs.k3s.io/upgrades/automated).

### [Traefik](https://github.com/traefik/traefik)
Traefik is an ingress controller that will let you access services with DNS names and a standard port across all services. To setup your service with Traefik, define a service type of `ClusterIP` with the `.spec.ports.port` your application is exposing. Then define a Kubernetes Ingress that points to your service. You can update your hosts file on a local system if you'd like to resolve a name to an IP address. If you have a DNS server, you can configure A records such as `homelab.local` and `*.homelab.local` that point to the IP address Traefik is running on. If you have a public domain name, you can do the same on your public DNS provider and then port-forward your router to Traefik to access services remotely.
