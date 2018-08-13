Related articles

*   [Zabbix](/index.php/Zabbix "Zabbix")
*   [Munin](/index.php/Munin "Munin")

[Grafana](https://grafana.com/) is an open-source, general purpose dashboard and graph composer, which runs as a web application. It supports graphite, [InfluxDB](/index.php/InfluxDB "InfluxDB") or opentsdb as backends.

## Contents

*   [1 Installation](#Installation)
*   [2 Example usage](#Example_usage)
    *   [2.1 Influxdb installation](#Influxdb_installation)
    *   [2.2 Aggregate data](#Aggregate_data)
    *   [2.3 Creating Grafana dashboard](#Creating_Grafana_dashboard)
*   [3 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [grafana](https://www.archlinux.org/packages/?name=grafana) package.

After that you can [Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `grafana` service and access the application on localhost, e.g.: [http://127.0.0.1:3000](http://127.0.0.1:3000) . The default username is `admin` and password `admin` to access the web frontend.

**Warning:** The default configuration listens on `*:3000` so make sure to change the configuration or enable the relevant firewall rules.

## Example usage

### Influxdb installation

One often used backend is [InfluxDB](/index.php/InfluxDB "InfluxDB"). [Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `influxdb` service. The web interface is available at [http://localhost:8083/](http://localhost:8083/)

### Aggregate data

In case of scaleable server monitoring in combination with Grafana and InfluxDB, one could choose software like [collectd](/index.php/Collectd "Collectd") or [statsd](/index.php?title=Statsd&action=edit&redlink=1 "Statsd (page does not exist)"). More generally any measurement data can be aggregated with InfluxDB and displayed with Grafana. There are modules and libraries for several programming languages to interact with InfluxDB and one could even store data with a simple http post command using the program [curl](/index.php?title=Curl&action=edit&redlink=1 "Curl (page does not exist)").

Herefore, create a database named `example`:

```
curl -G [http://localhost:8086/query](http://localhost:8086/query) --data-urlencode "q=CREATE DATABASE example"

```

Post data into the example database:

```
curl -i -XPOST '[http://localhost:8086/write?db=example'](http://localhost:8086/write?db=example') --data-binary 'cpu_load_short,host=server01,region=us-west value=0.64 1434055562000000000'

```

### Creating Grafana dashboard

*   Before creating a dashboard, we have to add a data source. So first click on `Data sources` in the left menu and then on `Add new`.
*   Name can be something like `influxdb` and the type should be set to `InfluxDB 0.9`. In this example, the url for the Http settings is `[http://localhost:8086](http://localhost:8086)`. Note that the port is not the same as the one of the web interface! Database name corresponds to the one earlier choosen, e.g. `example`. If not changed, username and password are `root`.
*   Click on `Test connection` to see everything is working and then on `Save`.
*   Next, back at the front page, click `Home` in the left-upper corner and then on `New`.
*   Now this might be a bit counter-intuitive, but to add a new dashboard you have to hover and click over the little green box on the left side and then, for example, choose: `Add panel` and `Graph`.
*   Click on the title of the new graph and select `Edit`.
*   In the graph settings in `Metrics` choose `influxdb` as data source in the lower-right corner.
*   Create a query by selecting your aggregated data. Click on `select measurement` which is located beside `FROM`. In the dropdown menu should appear a list of "tables" in your database, e.g. the table named `localhost`. If no suggestions comes up, your connection to InfluxDB might be broken or no data has been aggregated yet.
*   Beside the bold text `SELECT` click on `value` and choose for example the measurement data `uptime`.
*   To save changes, click `Back to dashboard`, then the floppy disc icon.

## See also

*   [Official homepage](https://grafana.org/)