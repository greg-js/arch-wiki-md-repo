**Status de tradução:** Esse artigo é uma tradução de [Grafana](/index.php/Grafana "Grafana"). Data da última tradução: 2019-08-09\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Grafana&diff=0&oldid=578994) na versão em inglês.

Artigos relacionados

*   [Zabbix](/index.php/Zabbix "Zabbix")
*   [Munin](/index.php/Munin "Munin")

[Grafana](https://grafana.com/) é um painel de composição de uso geral e de código aberto, que é executado como um aplicativo da web. Possui suporte a [graphite](https://www.archlinux.org/packages/?name=graphite), [InfluxDB](/index.php/InfluxDB "InfluxDB") ou opentsdb como backends.

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

Depois disso, você pode [habilitar](/index.php/Habilita "Habilita") e [iniciar](/index.php/Inicia "Inicia") o `grafana.service` e acessar o aplicativo no host local, por exemplo: [http://127.0.0.1:3000](http://127.0.0.1:3000). O nome de usuário padrão é `admin` e a senha `admin` para acessar a interface web.

**Atenção:** A configuração padrão atende em `*:3000`, portanto, certifique-se de alterar a configuração ou ativar as regras de firewall relevantes.

## Exemplo de uso

### Instalação com Influxdb

Um back-end usado com frequência é o [InfluxDB](/index.php/InfluxDB "InfluxDB"). [Habilite](/index.php/Habilite "Habilite") e [inicie](/index.php/Inicie "Inicie") o `influxdb.service`. A interface da web está disponível em [http://localhost:8086/](http://localhost:8086/)

### Agregar dados

Em caso de monitoramento de servidor escalonável em combinação com Grafana e InfluxDB, pode-se escolher software como [collectd](https://www.archlinux.org/packages/?name=collectd) ou [statsd](https://aur.archlinux.org/packages/statsd/). Mais geralmente, qualquer dado de medição pode ser agregado com o InfluxDB e exibido com o Grafana. Existem módulos e bibliotecas para diversas linguagens de programação para interagir com o InfluxDB e pode-se até armazenar dados com um simples comando http post usando o programa [curl](https://www.archlinux.org/packages/?name=curl).

Então, crie um banco de dados chamado `*exemplo*`:

```
curl -G http://localhost:8086/query --data-urlencode "q=CREATE DATABASE *exemplo*"

```

Envie dados para o banco de dados `*exemplo*`:

```
curl -i -XPOST 'http://localhost:8086/write?db=*exemplo'* --data-binary 'cpu_load_short,host=server01,region=us-west value=0.64 1434055562000000000'

```

### Criando painel do Grafana

*   Antes de criar um painel, precisamos adicionar uma fonte de dados. Então, primeiro clique em `Data sources` no menu à esquerda e depois em `Add new`.
*   O nome pode ser algo como `influxdb` e o tipo deve ser definido como `InfluxDB 0.9`. Neste exemplo, a URL das configurações do HTTP é `[http://localhost:8086](http://localhost:8086)`. Note que a porta não é a mesma da interface web! O nome do banco de dados corresponde ao escolhido anteriormente, por ex. `exemplo`. Se não for alterado, o nome de usuário e a senha serão `root`.
*   Clique em `Test connection` para ver tudo está funcionando e, em seguida, `Save`.
*   Em seguida, de volta à primeira página, clique em `Home` no canto superior esquerdo e depois em `New`.
*   Agora, isso pode ser um pouco contraintuitivo, mas para adicionar um novo painel você deve passar o mouse sobre a pequena caixa verde no lado esquerdo e depois, por exemplo, escolher: `Adicionar painel` e `Graph`.
*   Clique no título do novo gráfico e selecione `Edit`.
*   Nas configurações do gráfico em `Metrics` escolha `influxdb` como fonte de dados no canto inferior direito.
*   Crie uma consulta selecionando seus dados agregados. Clique em `select measurement` que está localizado ao lado de `FROM`. No menu suspenso, deve aparecer uma lista de "tabelas" em seu banco de dados, por exemplo, a tabela denominada `localhost`. Se nenhuma sugestão aparecer, sua conexão com o InfluxDB poderá ser interrompida ou nenhum dado foi agregado ainda.
*   Ao lado do texto em negrito `SELECT` clique em `value` e escolha, por exemplo, os dados de medição `uptime`.
*   Para salvar as alterações, clique em `Back to dashboard`, então no ícone de disquete.