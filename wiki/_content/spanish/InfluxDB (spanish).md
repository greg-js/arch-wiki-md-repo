**Estado de la traducción:** este artículo es una versión traducida de [InfluxDB](/index.php/InfluxDB "InfluxDB"). Fecha de la última traducción/revisión: **2018-08-11**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=InfluxDB&diff=0&oldid=533358).

Artículos relacionados

*   [Telegraf](/index.php/Telegraf "Telegraf")
*   [Grafana](/index.php/Grafana "Grafana")

InfluxDB es una base de datos de series de tiempo construida desde cero para manejar altas cargas de escritura y consultas. Es la segunda pieza de la [pila TICK](https://www.influxdata.com/time-series-platform/). InfluxDB está destinado a ser utilizado como una almacenamiento de reserva para cualquier tipo de uso que involucre grandes cantidades de datos con marcas de tiempo, incluyendo la supervisión DevOps, métricas de aplicaciones, datos de sensores IoT y análisis en tiempo real. Para obtener información más detallada, consulte la [documentación oficial](https://docs.influxdata.com/influxdb/).

## Contents

*   [1 Instalación](#Instalaci.C3.B3n)
*   [2 Configuración](#Configuraci.C3.B3n)
*   [3 Utilización](#Utilizaci.C3.B3n)
*   [4 Consulte también](#Consulte_tambi.C3.A9n)

## Instalación

[Instale](/index.php/Install "Install") el paquete [influxdb](https://www.archlinux.org/packages/?name=influxdb) y [active](/index.php/Enable "Enable") e [inicie](/index.php/Start "Start") el servicio `influxdb`.

**Advertencia:** La configuración predeterminada escucha en `*:8086` así que asegúrese de cambiar la configuración o habilitar las reglas del cortafuegos relevantes.

## Configuración

Toda la configuración se realiza en `/etc/influxdb/influxdb.conf`.

## Utilización

InfluxDB se puede usar como parte de la **pila TICK**. En esta configuración, los datos se escriben en la base de datos usando [Telegraf](/index.php/Telegraf "Telegraf"). **Kapacitor** y **Chronograf**. Luego usan la base de datos para enviar alertas y mostrar datos respectivamente.

También se puede usar con otros complementos de entrada, como por ejemplo [collectd](/index.php/Collectd "Collectd"). Otra herramienta para la visualización de datos es [Grafana](/index.php/Grafana "Grafana").

La operaciones con la base de datos se pueden hacer mediante su API HTTP, tanto para [escribir](https://docs.influxdata.com/influxdb/latest/guides/writing_data/) como para [consultar](https://docs.influxdata.com/influxdb/latest/guides/querying_data/).

## Consulte también

*   [InfluxData](https://www.influxdata.com/)
*   [Github](https://github.com/influxdata/influxdb/)