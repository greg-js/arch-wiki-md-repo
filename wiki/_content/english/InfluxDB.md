Related articles

*   [Telegraf](/index.php/Telegraf "Telegraf")
*   [Chronograf](/index.php?title=Chronograf&action=edit&redlink=1 "Chronograf (page does not exist)")
*   [Kapacitor](/index.php?title=Kapacitor&action=edit&redlink=1 "Kapacitor (page does not exist)")
*   [Grafana](/index.php/Grafana "Grafana")

InfluxDB is a time series database built from the ground up to handle high write and query loads. It is the second piece of the [TICK stack](/index.php?title=TICK_stack&action=edit&redlink=1 "TICK stack (page does not exist)"). InfluxDB is meant to be used as a backing store for any use case involving large amounts of timestamped data, including DevOps monitoring, application metrics, IoT sensor data, and real-time analytics.[[1]](https://docs.influxdata.com/influxdb/v1.2/)

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
*   [3 Usage](#Usage)
*   [4 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [influxdb](https://aur.archlinux.org/packages/influxdb/) and [enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `influxdb` service.

## Configuration

All configuration is done in `/etc/influxdb/influxdb.conf`. By default, it listens at [https://localhost:8086](https://localhost:8086) for data.

The configuration is well documented, but you can also have a look at their [Documentation](https://docs.influxdata.com/influxdb/latest/)

## Usage

The InfluxDB can be used as part of the [TICK stack](/index.php?title=TICK_stack&action=edit&redlink=1 "TICK stack (page does not exist)"). In this setup, data is written into the database using [Telegraf](/index.php/Telegraf "Telegraf"). [Kapacitor](/index.php?title=Kapacitor&action=edit&redlink=1 "Kapacitor (page does not exist)") and [Chronograf](/index.php?title=Chronograf&action=edit&redlink=1 "Chronograf (page does not exist)") then use the database to send alerts and display data respectively.

InfluxDB can also be used with other input plugins, e.g. [collectd](/index.php/Collectd "Collectd"). Another tool for data visualization is [Grafana](/index.php/Grafana "Grafana").

Writing and querying the database can also be done using their HTTP API for [writing](https://docs.influxdata.com/influxdb/latest/guides/writing_data/) and [querying](https://docs.influxdata.com/influxdb/latest/guides/querying_data/).

## See also

*   [InfluxData](https://www.influxdata.com/)
*   [Documentation](https://docs.influxdata.com/influxdb/latest/)
*   [Github](https://github.com/influxdata/influxdb/)