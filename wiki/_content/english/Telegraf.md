Telegraf is an agent written in Go for collecting, processing, aggregating, and writing metrics [[1]](https://github.com/influxdata/telegraf/). It is an open source application developed by InfluxData and closely integrated into the [TICK Stack](/index.php?title=TICK_Stack&action=edit&redlink=1 "TICK Stack (page does not exist)"). It is highly customizable with plugins for different metrics and backends.

## Installation

[Install](/index.php/Install "Install") the [telegraf](https://aur.archlinux.org/packages/telegraf/) or the [telegraf-bin](https://aur.archlinux.org/packages/telegraf-bin/) package. If you want to write your own plugins, it may be better to get it directly from [github](https://github.com/influxdata/telegraf/) and compile it in your [$GOPATH](/index.php/Go#.24GOPATH "Go").

[Enable](/index.php/Enable "Enable") and [start](/index.php/Start "Start") the `telegraf` service.

## Configuration

All configuration is done in `/etc/telegraf/telegraf.conf`. By default it expects you to have [InfluxDB](/index.php/InfluxDB "InfluxDB") installed. To test the default output, run `telegraf --test`.

The configuration is well documented, but you can also ahve a look at their [Documentation](https://docs.influxdata.com/telegraf/latest/)

## See also

*   [InfluxData](https://www.influxdata.com/)
*   [Documentation](https://docs.influxdata.com/telegraf/latest/)
*   [Github](https://github.com/influxdata/telegraf/)