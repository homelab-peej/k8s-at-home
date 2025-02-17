# Infrastructure

Apps and services that are essential to a functioning cluster to support the applications that I want to run. Essential to me doesn't necessarily mean essential to you. Some applications below are included with K3S, but may not be as configurable. Installing them separately allows for a more portable install across different cluster environments. Many choices below have alternatives as well.

### [Flux Extensions](https://fluxcd.io/flux/guides/)
- [Monitoring Alerts](https://fluxcd.io/flux/monitoring/alerts/) - This guide will help you setup alerts that use the notification controller. Many Flux `kind`s can be monitored and send alerts based on state changes or errors. Cross-namespace references are difficult (by design) so I've done a single secret in `flux-system` as well as the provider which references it. The alert can point to objects in other namespaces so this removes the need for replicating resources across namespaces.

### [MetalLB](https://metallb.universe.tf/)
Bare-metal Kubernetes installs do not have a native load-balancer implementation. This tool lets you dedicate IP addresses to be available to your cluster for [Services of type LoadBalancer](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/) to claim for use. I'll set one address aside specifically for a reverse-proxy to use with a DNS name, and I'll have another small pool available for other random stuff. See [basic L2 configuration](https://metallb.io/configuration/) to get started.

### [Reloader](https://github.com/stakater/reloader)
Reloader will watch many resources for `ConfigMap` or `Secret` changes and automatically rollout an update for those changes. Simply add the annotation `reloader.stakater.com/auto: "true"` to your Deployment `.metadata`. See the [documentation](https://github.com/stakater/reloader#how-to-use-reloader) for more examples.
