# Infrastructure

Apps and services that are essential to a functioning cluster to support the applications that I want to run. Essential to me doesn't necessarily mean essential to you. Some applications below are included with K3S, but may not be as configurable. Installing them separately allows for a more portable install across different cluster environments. Many choices below have alternatives as well.

### [Actions Runner Controller](https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners-with-actions-runner-controller/deploying-runner-scale-sets-with-actions-runner-controller#runner-scale-set)
Actions Runner Controller (ARC) is a Kubernetes operator that orchestrates and scales self-hosted runners for GitHub Actions. With ARC, you can create runner scale sets that automatically scale based on the number of workflows running in your repository, organization, or enterprise. Because controlled runners can be ephemeral and based on containers, new runner instances can scale up or down rapidly and cleanly.

### [Cert-Manager](https://github.com/cert-manager/cert-manager)
Cert-manager is a X.509 certificate manager for Kubernetes. It adds multiple certificate and issuer resources to your cluster can help you automate obtaininig, renewing, and using your certificates. By using the [DNS challenge](https://cert-manager.io/docs/configuration/acme/dns01/#setting-nameservers-for-dns01-self-check) option we can obtain certificates even for an internal-only domain name. Cert-manager knows that you still control the domain since it can write TXT records back to Cloudflare with your API token. If you have an internal DNS server and use [split-horizon](https://en.wikipedia.org/wiki/Split-horizon_DNS) be sure to add the extraAgs shown above to force cert-manager to use public DNS to authenticate since your internal DNS will not propogate those records.

### [Cloudflare-DDNS](https://github.com/favonia/cloudflare-ddns)
A feature-rich and robust Cloudflare DDNS updater with a small footprint. The program will detect your machine’s public IP addresses and update DNS records using the [Cloudflare API](https://dash.cloudflare.com/profile/api-tokens).

### [Flux Extensions](https://fluxcd.io/flux/guides/)
- [Automatic Image Updates](https://fluxcd.io/flux/guides/image-update/) - You can follow this guide to automate image scanning and application updates. Flux will monitor a registry and image that you select and automatically pick the latest image based on the parameters provided. Flux will then write those changes back to your source control and update your application. [Mealie](https://github.com/homelab-peej/k8s-at-home/blob/main/self-hosted/mealie.yaml) has a good example.
- [Monitoring Alerts](https://fluxcd.io/flux/monitoring/alerts/) - This guide will help you setup alerts that use the notification controller. Many Flux `kind`s can be monitored and send alerts based on state changes or errors. Cross-namespace references are difficult (by design) so I've done a single secret in `flux-system` as well as the provider which references it. The alert can point to objects in other namespaces so this removes the need for replicating resources across namespaces.
- [Webhook Receivers](https://fluxcd.io/flux/guides/webhook-receivers/) - With cert-manager installed and the ability to create certificates for custom domains, we can turn Flux into a push-based pipeline that will trigger a sync any time there's a commit.

### [Longhorn](https://longhorn.io/docs/latest/what-is-longhorn/)
Longhorn is a lightweight, reliable and easy-to-use distributed block storage system for Kubernetes. We can use local disks to store data and backup data to TrueNAS and other locations.

### [MetalLB](https://metallb.universe.tf/)
Bare-metal Kubernetes installs do not have a native load-balancer implementation. This tool lets you dedicate IP addresses to be available to your cluster for [Services of type LoadBalancer](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/) to claim for use. I'll set one address aside specifically for a reverse-proxy to use with a DNS name, and I'll have another small pool available for other random stuff. See [basic L2 configuration](https://metallb.io/configuration/) to get started.

### [Reloader](https://github.com/stakater/reloader)
Reloader will watch many resources for `ConfigMap` or `Secret` changes and automatically rollout an update for those changes. Simply add the annotation `reloader.stakater.com/auto: "true"` to your Deployment `.metadata`. See the [documentation](https://github.com/stakater/reloader#how-to-use-reloader) for more examples.

### [System Upgrade Controller](https://github.com/rancher/system-upgrade-controller)
This project aims to provide a general-purpose, Kubernetes-native upgrade controller (for nodes). It introduces a new CRD, the `Plan`, for defining any and all of your upgrade policies/requirements. A `Plan` is an outstanding intent to mutate nodes in your cluster. This is the recommended way to automate K3S updates according to the [documentation](https://docs.k3s.io/upgrades/automated).

### [Traefik](https://doc.traefik.io/traefik/)
Traefik is an ingress controller that will let you access services with DNS names and a standard port across all services. To setup your service with Traefik, define a service type of `ClusterIP` with the `.spec.ports.port` your application is exposing. Then define a Kubernetes Ingress that points to your service. You can update your hosts file on a local system if you'd like to resolve a name to an IP address. If you have a DNS server, you can configure A records such as `homelab.local` and `*.homelab.local` that point to the IP address Traefik is running on. If you have a public domain name, you can do the same on your public DNS provider and then port-forward your router to Traefik to access services remotely.
