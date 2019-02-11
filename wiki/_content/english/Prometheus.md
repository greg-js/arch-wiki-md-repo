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
*   [3 Using the UI](#Using_the_UI)
*   [4 See also](#See_also)

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

## Using the UI

Prometheus comes with a very limited web UI to verify configuration, query and graph metrics. You can reach it at [http://localhost:9090](http://localhost:9090) by default. You can find an in-depth explanation of Prometheus' query language in the [Prometheus docs](https://prometheus.io/docs/prometheus/latest/querying/basics/).

## See also

*   [Official homepage](https://prometheus.io/)