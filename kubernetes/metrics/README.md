# Observability and Metrics

This stack runs off of a separate Kustomization so it can be suspended, modified, or deleted independently of other more critical infrastructure apps and the rest of the self-hosted stack.

### [Grafana](https://github.com/grafana/grafana)
Grafana lets you query, visualize, alert on, and explore your metrics, logs, and traces wherever they're stored. This install is a part of the [kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack) which is helpful for monitoring a K8S cluster. It comes with many helpful default dashboards. The default credentials for this install is `admin`/`prom-operator`.

### [Metrics Server](https://github.com/kubernetes-sigs/metrics-server)
Metrics Server is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. Publishes resource usage to enable `HorizontalPodAutoscaler` and `VerticalPodAutoscaler`.

### [MySpeed](https://github.com/gnmyt/myspeed/)
Test analysis software that records your internet speed for up to 30 days.

### [Prometheus](https://github.com/prometheus/prometheus)
Prometheus is a great systems monitoring and alerting toolkit. It's the datasource that is used by Grafana to display your cluster statistics and information. This install is a part of the [kube-prometheus-stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack) which is helpful for monitoring a K8S cluster.

### [Unpoller](https://github.com/unpoller/unpoller)
Unpoller will pull data from Unifi sources through a service account. Data can be exported to InfluxDB or Prometheus for viewing in Grafana. There are some preconfigured dashboards available for import referenced in the Unpoller [docs](https://unpoller.com/docs/install/grafana#dashboard-installation-instructions).
