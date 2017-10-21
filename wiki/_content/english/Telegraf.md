Related articles

*   [InfluxDB](/index.php/InfluxDB "InfluxDB")
*   [Grafana](/index.php/Grafana "Grafana")

[Telegraf](https://github.com/influxdata/telegraf/) is an agent written in Go for collecting, processing, aggregating, and writing metrics. It is an open source application developed by InfluxData and closely integrated into the TICK Stack. It is highly customizable with plugins for different metrics and backends.

## Installation

[Install](/index.php/Install "Install") the [telegraf](https://aur.archlinux.org/packages/telegraf/) or the [telegraf-bin](https://aur.archlinux.org/packages/telegraf-bin/) package. If you want to write your own plugins, it may be better to get it directly from [GitHub](https://github.com/influxdata/telegraf/) and compile it in your [$GOPATH](/index.php/Go#.24GOPATH "Go").

[Start/enable](/index.php/Start/enable "Start/enable") the `telegraf` service.

## Configuration

All configuration is done in `/etc/telegraf/telegraf.conf`. By default it expects you to have [InfluxDB](/index.php/InfluxDB "InfluxDB") installed. To test the default output, run `telegraf --test`.

The configuration is well documented, but you can also have a look at [their documentation](https://docs.influxdata.com/telegraf/latest/).

## See also

*   [InfluxData](https://www.influxdata.com/)
*   [Documentation](https://docs.influxdata.com/telegraf/latest/)
*   [GitHub](https://github.com/influxdata/telegraf/)