<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Running](#Running)
*   [3 Configuration](#Configuration)
*   [4 Usage](#Usage)

## Installation

[Install](/index.php/Install "Install") the [kibana](https://www.archlinux.org/packages/?name=kibana) package.

## Running

[Start/enable](/index.php/Start/enable "Start/enable") `kibana.service`.

## Configuration

By default `kibana` does not specify a port or bind address. The main Kibana configuration file is located at `/etc/kibana/kibana.yml`.

At a minimum uncomment the following lines:

 `/etc/kibana/kibana.yml` 
```
server.port: 5601
server.host: "localhost"
elasticsearch.hosts: ["http://localhost:9200"]

```

Once the changes are saved [Restart](/index.php/Restart "Restart") the `kibana.service`

## Usage

Access the interface on [http://localhost:5601](http://localhost:5601)