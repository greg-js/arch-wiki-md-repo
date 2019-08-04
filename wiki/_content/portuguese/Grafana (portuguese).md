Artigos relacionados

*   [Zabbix](/index.php/Zabbix "Zabbix")
*   [Munin](/index.php/Munin "Munin")

[Grafana](https://grafana.com/) é um painel de composição de uso geral e de código aberto, que é executado como um aplicativo da web. Possui suporte a grafite, [InfluxDB](/index.php/InfluxDB "InfluxDB") ou opentsdb como backends.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Instalação](#Instalação)
*   [2 Exemplo de uso](#Exemplo_de_uso)
    *   [2.1 Instalação com Influxdb](#Instalação_com_Influxdb)
    *   [2.2 Agregar dados](#Agregar_dados)
    *   [2.3 Criando painel do Grafana](#Criando_painel_do_Grafana)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [grafana](https://www.archlinux.org/packages/?name=grafana).

Depois disso, você pode [habilitar](/index.php/Habilita "Habilita") e [iniciar](/index.php/Inicia "Inicia") o serviço `grafana` e acessar o aplicativo no host local, por exemplo: [http://127.0.0.1:3000](http://127.0.0.1:3000). O nome de usuário padrão é `admin` e a senha `admin` para acessar a interface web.

**Atenção:** A configuração padrão atende em `*:3000`, portanto, certifique-se de alterar a configuração ou ativar as regras de firewall relevantes.

## Exemplo de uso

### Instalação com Influxdb

Um back-end usado com frequência é o [InfluxDB](/index.php/InfluxDB "InfluxDB"). [Habilite](/index.php/Habilite "Habilite") e [inicie](/index.php/Inicie "Inicie") o serviço `influxdb`. A interface da web está disponível em [http://localhost:8086/](http://localhost:8086/)

### Agregar dados

In case of scaleable server monitoring in combination with Grafana and InfluxDB, one could choose software like [collectd](/index.php/Collectd "Collectd") or [statsd](/index.php?title=Statsd&action=edit&redlink=1 "Statsd (page does not exist)"). More generally any measurement data can be aggregated with InfluxDB and displayed with Grafana. There are modules and libraries for several programming languages to interact with InfluxDB and one could even store data with a simple http post command using the program [curl](/index.php?title=Curl&action=edit&redlink=1 "Curl (page does not exist)").

Herefore, create a database named `example`:

```
curl -G http://localhost:8086/query --data-urlencode "q=CREATE DATABASE example"

```

Post data into the example database:

```
curl -i -XPOST 'http://localhost:8086/write?db=example' --data-binary 'cpu_load_short,host=server01,region=us-west value=0.64 1434055562000000000'

```

### Criando painel do Grafana

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