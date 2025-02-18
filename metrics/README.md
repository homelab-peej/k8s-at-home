# Observability and Metrics

This stack runs off of a separate Kustomization so it can be suspended, modified, or deleted independently of other more critical infrastructure apps and the rest of the self-hosted stack.

### [Grafana](https://grafana.com/docs/grafana/latest/)
Grafana lets you query, visualize, alert on, and explore your metrics, logs, and traces wherever they're stored. This install is a part of the [kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack) which is helpful for monitoring a K8S cluster. It comes with many helpful default dashboards. The default credentials for this install is `admin`/`prom-operator`.

### [Metrics Server](https://github.com/kubernetes-sigs/metrics-server)
Metrics Server is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. Publishes resource usage to enable `HorizontalPodAutoscaler` and `VerticalPodAutoscaler`.

### [Prometheus](https://prometheus.io/docs/introduction/overview/)
Prometheus is a great systems monitoring and alerting toolkit. It's the datasource that is used by Grafana to display your cluster statistics and information. This install is a part of the [kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack) which is helpful for monitoring a K8S cluster.
