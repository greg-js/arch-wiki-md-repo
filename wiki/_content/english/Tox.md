From the project [home page](https://tox.chat/): "Tox is a distributed, secure messenger with audio and video chat capabilities."

## Installation

In order to use Tox, you should [install](/index.php/Install "Install") a [Tox client](https://wiki.tox.chat/clients). See [List of applications/Internet#Tox clients](/index.php/List_of_applications/Internet#Tox_clients "List of applications/Internet").

## Proxy

To connect via [Tor](/index.php/Tor "Tor"), first start it with:

```
sudo -u tor /usr/bin/tor

```

Then configure your Tox client. For example:

```
toxic -t -p 127.0.0.1 9050

```

## Run a node

To be able to connect to others, Tox needs to connect to a [DHT node](https://wiki.tox.chat/users/nodes) first. All DHT nodes are connected to each other, and since everyone is connected to at least one DHT node, you can connect to others one way or the other.

The package [toxcore](https://www.archlinux.org/packages/?name=toxcore) creates user *tox-bootstrapd* and includes a systemd unit file in `/usr/lib/systemd/system/tox-bootstrapd.service` and a configuration file in `/etc/tox-bootstrapd.conf`.

Edit the configuration file and add appropriate nodes from [Tox wiki](https://wiki.tox.chat/users/nodes) or [Node status page](https://nodes.tox.chat/).

[Enable](/index.php/Enable "Enable") and start `tox-bootstrapd.service` and check if it is running fine and port has been bound:

 `# ss --listening --numeric --processes | grep *node_port*`  `udp        0      0 *:*node_port*                 *:*                                 576/DHT_bootstrap`