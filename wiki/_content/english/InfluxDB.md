Related articles

*   [Telegraf](/index.php/Telegraf "Telegraf")
*   [Grafana](/index.php/Grafana "Grafana")

InfluxDB is a time series database built from the ground up to handle high write and query loads. It is the second piece of the [TICK stack](https://www.influxdata.com/time-series-platform/). InfluxDB is meant to be used as a backing store for any use case involving large amounts of timestamped data, including DevOps monitoring, application metrics, IoT sensor data, and real-time analytics. For more detailed information, see the [official documentation](https://docs.influxdata.com/influxdb/).

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [influxdb](https://www.archlinux.org/packages/?name=influxdb) and [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `influxdb` service.

**Warning:** The default configuration listens on `*:8086` so make sure to change the configuration or enable the relevant firewall rules.

## Configuration

All configuration is done in `/etc/influxdb/influxdb.conf`.

## Usage

The InfluxDB can be used as part of the **TICK stack**. In this setup, data is written into the database using [Telegraf](/index.php/Telegraf "Telegraf"). **Kapacitor** and **Chronograf** then use the database to send alerts and display data respectively.

InfluxDB can also be used with other input plugins, e.g. [collectd](/index.php/Collectd "Collectd"). Another tool for data visualization is [Grafana](/index.php/Grafana "Grafana").

Writing and querying the database can also be done using their HTTP API for [writing](https://docs.influxdata.com/influxdb/latest/guides/writing_data/) and [querying](https://docs.influxdata.com/influxdb/latest/guides/querying_data/).

## See also

*   [InfluxData](https://www.influxdata.com/)
*   [Github](https://github.com/influxdata/influxdb/)