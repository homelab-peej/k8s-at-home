# Infrastructure

Apps and services that are essential to a functioning cluster to support the applications that I want to run. Essential to me doesn't necessarily mean essential to you. Some applications below are included with K3S, but may not be as configurable. Installing them separately allows for a more portable install across different cluster environments. Many choices below have alternatives as well.

### [Flux Extensions](https://fluxcd.io/flux/guides/)
- [Monitoring Alerts](https://fluxcd.io/flux/monitoring/alerts/) - This guide will help you setup alerts that use the notification controller. Many Flux `kind`s can be monitored and send alerts based on state changes or errors. Cross-namespace references are difficult (by design) so I've done a single secret in `flux-system` as well as the provider which references it. The alert can point to objects in other namespaces so this removes the need for replicating resources across namespaces.

### [Reloader](https://github.com/stakater/reloader)
Reloader will watch many resources for `ConfigMap` or `Secret` changes and automatically rollout an update for those changes. Simply add the annotation `reloader.stakater.com/auto: "true"` to your Deployment `.metadata`. See the [documentation](https://github.com/stakater/reloader#how-to-use-reloader) for more examples.
