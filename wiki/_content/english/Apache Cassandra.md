Related articles

*   [Apache Spark](/index.php/Apache_Spark "Apache Spark")

[Apache Cassandra](https://cassandra.apache.org/) is a NoSQL multi-master database with linear scalability and no single point of failure.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Systemd unit](#Systemd_unit)
        *   [2.1.1 Logging to journald](#Logging_to_journald)
    *   [2.2 cassandra.yaml](#cassandra.yaml)
        *   [2.2.1 Basic config items to change](#Basic_config_items_to_change)
        *   [2.2.2 Recommended settings for linux specifically](#Recommended_settings_for_linux_specifically)
        *   [2.2.3 Troubleshooting](#Troubleshooting)

## Installation

[Install](/index.php/Install "Install") the [cassandra](https://aur.archlinux.org/packages/cassandra/) package.

## Configuration

### Systemd unit

##### Logging to journald

The package logs to `/var/log/cassandra/system.log` by default. To instead log to journald you will need to copy the systemd unit to `/etc/systemd/system/` so the change persists.

```
$ cp /usr/lib/systemd/system/cassandra.service /etc/systemd/system/

```

Edit the unit

```
$ vim /etc/systemd/system/cassandra.service

```

And set the service to run in the foreground by adding `-f` to the `ExecStart` line, and set Type to `simple` as the process will no longer fork

```
[Service]
Type=simple
ExecStart=/usr/bin/cassandra -p /run/cassandra/cassandra.pid -f

```

If Cassandra was running you will need to drain, and restart Cassandra

```
$ nodetool drain; systemctl restart cassandra

```

### cassandra.yaml

There is copious amounts of documentation in the default `cassandra.yaml`. When installed via the [cassandra](https://aur.archlinux.org/packages/cassandra/) package, it is located in `/etc/cassandra/cassandra.yaml`

##### Basic config items to change

Setting the name of the cluster. This needs to be consistent for all nodes that you intend to have in this cluster.

```
cluster_name: 'Test Cluster'

```

Set the directory where cassandra will write too, below is the default that will be used if unset. If possible set this to a disk used only for storing cassandra data

```
data_file_directories:
    - /var/lib/cassandra/data

```

For the first node (the seed node) make sure to include its IP address in the seeds, and atleast 1 other node. for all other nodes, try and set a broad range of nodes in the cluster. If a node cannot connect to one of the seeds listed in this configuration at startup - it will fail to start.

```
seed_provider:
    - class_name: org.apache.cassandra.locator.SimpleSeedProvider
      parameters:
          - seeds: "192.168.1.53, 192.168.1.52"

```

set this based on what type of disk cassandra is using to store data on `ssd` or `spinning`

```
disk_optimization_strategy: ssd|spinning

```

This is the address Cassandra will listen for client connections on

```
listen_address: 192.168.1.51

```

This is the address this node will advertise itself as, ensure both your clients and nodes can reach this node on this address

```
broadcast_address: 192.168.1.51

```

This is the address used for thrift connections, set to `0.0.0.0` it will listen on all interfaces, which is fine as long as its firewalled for security

```
rpc_address: 0.0.0.0

```

##### Recommended settings for linux specifically

hsha stands for "half synchronous, half asynchronous." All thrift clients are handled asynchronously using a small number of threads that does not vary with the amount of thrift clients (and thus scales well to many clients). This is not recommended on windows machines hsha is about 30% slower

```
rpc_server_type: hsha

```

Because we're using hsha, `rpc_max_threads` must be set, or cassandra will refuse to start. `rpc_max_threads` represents the maximum number of client requests this server may execute concurrently.

```
rpc_max_threads: 100

```

##### Troubleshooting

If Cassandra fails to run as a service, try running Cassandra

```
$ cassandra

```

If you receive the following error:

```
Improperly specified VM option 'ThreadPriorityPolicy=42'
Error: Could not create the Java Virtual Machine.
Error: A fatal exception has occurred. Program will exit.

```

Cassandra only runs on Java 8\. You will need to install Java per directions here [Java](/index.php/Java "Java") to install Java 8 and switch your jvm using `archlinux-java`