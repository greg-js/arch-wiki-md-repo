Related articles

*   [Zabbix](/index.php/Zabbix "Zabbix")
*   [Munin](/index.php/Munin "Munin")
*   [Grafana](/index.php/Grafana "Grafana")

[Prometheus](https://prometheus.io/) is an open-source metrics collection and processing tool. It consists primarily of a timeseries database and a query language to access and process the metrics it stores. Separate services perform metric exposure, from which the Prometheus server can pull. It provides a very minimal web UI out of the box. To get a functional dashboard system, third-party tools like [Grafana](/index.php/Grafana "Grafana") can be used.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Adding metric](#Adding_metric)
*   [3 Exporters](#Exporters)
*   [4 Using the UI](#Using_the_UI)
*   [5 Alerting](#Alerting)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [prometheus](https://www.archlinux.org/packages/?name=prometheus) or [prometheus-bin](https://aur.archlinux.org/packages/prometheus-bin/) package. After that you can [Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `prometheus` service and access the application via HTTP on port 9090 by default.

The default configuration monitors the `prometheus` process itself, but not much beyond that. To perform system monitoring, you can install [prometheus-node-exporter](https://www.archlinux.org/packages/?name=prometheus-node-exporter) or [prometheus-node-exporter-bin](https://aur.archlinux.org/packages/prometheus-node-exporter-bin/), which performs metric scraping from the local system. You can start and enable the `prometheus-node-exporter` service. It will open port 9100 by default.

## Configuration

The Prometheus configuration is done through [YAML](https://en.wikipedia.org/wiki/YAML "wikipedia:YAML") files, the main one being located at `/etc/prometheus/prometheus.yml`.

### Adding metric

You can add new places to scrape metrics from by adding them to the `scrape_configs` array. To add the local node exporter as a source, next to the prometheus process itself, the configuration would look like this:

```
 scrape_configs:
   - job_name: 'prometheus'
     static_configs:
       - targets: ['localhost:9090']
   - job_name: 'localhost'
     static_configs:
       - targets: ['localhost:9100']

```

## Exporters

The Arch Linux repository contains a subset of the [available exporters [https://prometheus.io/docs/instrumenting/exporters/](https://prometheus.io/docs/instrumenting/exporters/)]:

*   [prometheus-node-exporter](https://www.archlinux.org/packages/?name=prometheus-node-exporter) - system metrics
*   [prometheus-blackbox-exporter](https://www.archlinux.org/packages/?name=prometheus-blackbox-exporter) - blackbox probing of endpoints over HTTP, HTTPS, DNS, TCP and ICMP
*   [prometheus-memcached-exporter](https://www.archlinux.org/packages/?name=prometheus-memcached-exporter) - memcached metrics

## Using the UI

Prometheus comes with a very limited web UI to verify configuration, query and graph metrics. You can reach it at [http://localhost:9090](http://localhost:9090) by default. You can find an in-depth explanation of Prometheus' query language in the [Prometheus docs](https://prometheus.io/docs/prometheus/latest/querying/basics/).

## Alerting

[alertmanager](https://www.archlinux.org/packages/?name=alertmanager) can send out custom alerts when certain conditions are met configured in `/etc/prometheus/alert.rules.yml` and what alert to send out is configured in `/etc/alertmanager/alertmanager.yml`. Alertmanager supports various ways to notify users such as email, slack, and [more](https://prometheus.io/docs/alerting/configuration/). To configure email alerts add the following snippet:

```
 global:
   resolve_timeout: 5m
   smtp_smarthost: 'smtp.example.com:25'
   smtp_from: 'alertmanager@example.com'
 route:
   group_by: ['instance', 'severity']
   group_wait: 30s
   group_interval: 5m
   repeat_interval: 3h
   receiver: team-1
 receivers:
   - name: 'team-1'
     email_configs:
       - to: 'admin@example.com'

```

For prometheus to send alerts to alertmanager include the following snippet in `/etc/prometheus/prometheus.yml`:

```
 alerting:
   alertmanagers:
   - static_configs:
     - targets:
        - localhost:9093

```

To configure an alert for when a systemd unit fails add the following snippet to `/etc/prometheus/alert.rules.yml`. For more rules read the [alerting rules](https://prometheus.io/docs/alerting/configuration/) documentation.

```
 - name: systemd_unit
   interval: 15s
   rules:
   - alert: systemd_unit_failed
     expr: |
       node_systemd_unit_state{state="failed"} > 0
     for: 3m
     labels:
       severity: critical
     annotations:
       description: 'Instance [Template:$labels.instance](/index.php?title=Template:$labels.instance&action=edit&redlink=1 "Template:$labels.instance (page does not exist)"): Service [Template:$labels.name](/index.php?title=Template:$labels.name&action=edit&redlink=1 "Template:$labels.name (page does not exist)") failed'
       summary: 'Systemd unit failed'

```

## See also

*   [Official homepage](https://prometheus.io/)