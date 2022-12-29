# ntp_exporter Helm Chart
This repository contains a HELM chart to quickly get up and running with the [SAP ntp_exporter](https://github.com/sapcc/ntp_exporter) within Kubernetes.

For further documentation, please see the [README](https://github.com/sapcc/ntp_exporter/blob/master/README.md) of the original repository.

Example scrape config:
~~~yaml
- job_name: 'ntp-exporter'
  kubernetes_sd_configs:
      - role: endpoints
  relabel_configs:
      - source_labels: [__meta_kubernetes_endpoints_label_app_kubernetes_io_name]
      separator: ;
      regex: ntp-exporter
      replacement: $1
      action: keep
      - source_labels: [__meta_kubernetes_endpoint_port_name]
      separator: ;
      regex: metrics
      replacement: $1
      action: keep
      - source_labels: [__meta_kubernetes_namespace]
      separator: ;
      regex: (.*)
      target_label: namespace
      replacement: $1
      action: replace
~~~