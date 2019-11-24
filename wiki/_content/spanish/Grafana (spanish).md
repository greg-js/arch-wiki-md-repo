**Estado de la traducción**
Este artículo es una traducción de [Grafana](/index.php/Grafana "Grafana"), revisada por última vez el **2019-11-21**. Si advierte que la versión inglesa [ha cambiado](https://wiki.archlinux.org/index.php?title=Grafana&diff=0&oldid=589613) puede ayudar a actualizar la traducción, bien por [usted mismo](/index.php/ArchWiki:Translation_Team/Contributing_(Espa%C3%B1ol) "ArchWiki:Translation Team/Contributing (Español)") o bien avisando al [equipo de traducción](/index.php/ArchWiki:Translation_Team_(Espa%C3%B1ol) "ArchWiki:Translation Team (Español)").

Artículos relacionados

*   [Zabbix](/index.php/Zabbix "Zabbix")
*   [Munin](/index.php/Munin "Munin")

[Grafana](https://grafana.com/) es un panel de instrumentos y un compositor gráfico de uso general y de código abierto, que se ejecuta como una aplicación web. Es compatible con [graphite](https://www.archlinux.org/packages/?name=graphite), [InfluxDB](/index.php/InfluxDB "InfluxDB"), [Prometheus](/index.php/Prometheus "Prometheus") o opentsdb como backends.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalación](#Instalación)
*   [2 Ejemplo de utilización](#Ejemplo_de_utilización)
    *   [2.1 Instalación de Influxdb](#Instalación_de_Influxdb)
    *   [2.2 Agregar datos](#Agregar_datos)
    *   [2.3 Crear el panel de instrumentos de Grafana](#Crear_el_panel_de_instrumentos_de_Grafana)

## Instalación

[Instale](/index.php/Install_(Espa%C3%B1ol) "Install (Español)") el paquete [grafana](https://www.archlinux.org/packages/?name=grafana).

Después de eso, puede [activar](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") e [iniciar](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `grafana.service` y acceder a la aplicación en localhost, por ejemplo: [http://127.0.0.1:3000](http://127.0.0.1:3000) . El nombre de usuario predeterminado es `admin` y la contraseña `admin` para acceder a la interfaz web.

**Advertencia:** la configuración predeterminada escucha en `*:3000`, de modo que asegúrese de cambiar la configuración o activar las reglas del cortafuegos que le afecten.

## Ejemplo de utilización

### Instalación de Influxdb

Un backend de uso frecuente es [InfluxDB](/index.php/InfluxDB "InfluxDB"). [Active](/index.php/Enable_(Espa%C3%B1ol) "Enable (Español)") e [inicie](/index.php/Start_(Espa%C3%B1ol) "Start (Español)") `influxdb.service`. La interfaz web está disponible en [http://localhost:8086/](http://localhost:8086/)

### Agregar datos

En caso de monitoreo de servidor escalable en combinación con Grafana e InfluxDB, se podría elegir software como [collectd](https://www.archlinux.org/packages/?name=collectd) o [statsd](https://aur.archlinux.org/packages/statsd/). Con carácter más general, cualquier dato de medición puede agregarse con InfluxDB y mostrarse con Grafana. Hay módulos y bibliotecas para que varios lenguajes de programación interactúen con InfluxDB e, incluso, se pueden almacenar datos con una simple orden «post http» utilizando el programa [curl](https://www.archlinux.org/packages/?name=curl).

Por lo tanto, cree una base de datos llamada `*example*`:

```
curl -G http://localhost:8086/query --data-urlencode "q=CREATE DATABASE *example*"

```

Envíe información a la base de datos `*example*`:

```
curl -i -XPOST 'http://localhost:8086/write?db=*example'* --data-binary 'cpu_load_short,host=server01,region=us-west value=0.64 1434055562000000000'

```

### Crear el panel de instrumentos de Grafana

*   Antes de crear un panel de instrumentos, debemos agregar una fuente de datos. Así que primero haga clic en `Data sources` en el menú izquierdo y luego en `Add new`.
*   El nombre puede ser algo como `influxdb` y el tipo debe establecerse en `InfluxDB 0.9`. En este ejemplo, la url de la configuración Http es `[http://localhost:8086](http://localhost:8086)`. Tenga en cuenta que el puerto no es el mismo que el de la interfaz web. El nombre de la base de datos corresponde al elegido anteriormente, por ejemplo `example`. Si no se cambia, el nombre de usuario y la contraseña son `root`.
*   Haga clic en `Test connection` para ver que todo funciona y luego en `Save`.
*   A continuación, vuelta en la página principal, haga clic en `Home` en la esquina superior izquierda y luego en `New`.
*   Ahora, esto puede ser un poco contrario a la intuición, pero para agregar un nuevo panel de instrumentos, debe desplazarse y hacer clic sobre el pequeño cuadro verde en el lado izquierdo y luego, por ejemplo, elegir: `Add panel` y `Graph`.
*   Haga clic en el título del nuevo gráfico y seleccione `Edit`.
*   En la configuración del gráfico en `Metrics` elija `influxdb` como fuente de datos en la esquina inferior derecha.
*   Cree una consulta seleccionando sus datos agregados. Haga clic en `select measurement` que se encuentra al lado de `FROM`. En el menú desplegable debe aparecer una lista de «tablas» en su base de datos, por ejemplo, la tabla llamada `localhost`. Si no surge ninguna sugerencia, su conexión a InfluxDB podría interrumpirse o puede ser que aún no se haya agregado ningún dato.
*   Junto al texto en negrita `SELECT` haga clic en `value` y elija, por ejemplo, los datos de medición `uptime`.
*   Para guardar los cambios, haga clic en `Back to dashboard` y luego en el icono del disquete.