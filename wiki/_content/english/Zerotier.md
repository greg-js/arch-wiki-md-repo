Zerotier is an open source, cross-platform and easy to use virtual LAN / Hamachi alternative, also available on Android, ios, Mac, Windows. A GUI is only available on Mac and Windows according to the developers.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installing](#Installing)
*   [2 Configuration](#Configuration)
*   [3 Manual configuration](#Manual_configuration)
*   [4 Slow shutdown](#Slow_shutdown)

## Installing

ZeroTier can be [installed](/index.php/Install "Install") with the [zerotier-one](https://www.archlinux.org/packages/?name=zerotier-one).

## Configuration

You will need to create an account over at [My Zerotier](https://my.zerotier.com/) and create a network and select your desired options, such as support for IPv4 or IPv6 or both. Keep note of the network ID of the newly-created network as you will be needing it later on.

Leave the page for the network that you will use open, as you will need to authorize each computer or device that you connect, and also verify that they get an IP.

To begin [start](/index.php/Start "Start") `zerotier-one.service`, if one would like it to start at boot [enable](/index.php/Enable "Enable") `zerotier-one.service`. To find out your computer id, which will be a 10-digit hexadecimal number similar to 89e92ceee5, run:

 `# zerotier-cli info` 
```
200 info 89e92ceee5 1.2.4 ONLINE

```

where 89e92ceee5 is address and 1.2.4 is the version, followed by its status.

Next you will need to join a network:

```
# zerotier-cli join *network_id*

```

The network ID is a 16-digit hexadecimal number like 8056c2e21c000001 which you can get on the Networks page.

Back on the network page at my.zerotier, scroll down to the Members section where you should see all addresses that have joined. To authorize each computer or device, check the left-most checkbox and verify that it is given an IP address (this may take 10 or 20 seconds). You may need to run [dhcpcd](/index.php/Dhcpcd "Dhcpcd") to acquire the new IP address locally.

To verify that all devices can see each other you can [ping](/index.php/Ping "Ping") each address using its associated IP, like so:

 `$ ping 192.168.192.91` 
```
PING 192.168.192.91 (192.168.192.91) 56(84) bytes of data.
64 bytes from 192.168.192.91: icmp_req=1 ttl=53 time=52.9 ms
...

```

One can also see connected peers by running:

 `# zerotier-cli listpeers` 
```
200 listpeers <ztaddr> <path> <latency> <version> <role>
200 listpeers 12ac4a1e71 87.98.218.130/30883;12;12;1.00 589 1.2.5 LEAF
200 listpeers 8841408a2e 159.203.2.154/9993;13262;13220;1.00 127 1.1.5 PLANET
200 listpeers 9d219039f3 159.203.97.171/9993;13241;3218;1.00 63 1.1.5 PLANET
...

```

and see a list of networks the computer is connected to by running:

```
# zerotier-cli listnetworks

```

## Manual configuration

Manual configuration can be achieved by creating the file `local.conf` in the program's home directory `/var/lib/zerotier-one`. This allows you to set various configuration options, such as restricting the service to specific interfaces, or enforcing use of a different port. This file **must** be valid JSON as it can be re-written by zerotier-one. Below is an example `local.conf` which stops zerotier-one using docker and bridged interfaces:

```
{
    "settings": {
        "interfacePrefixBlacklist": [ "docker", "br-" ]
    }
}

```

More information on the available configuration items is available on the [program's GitHub repo](https://github.com/zerotier/ZeroTierOne/tree/master/service#local-configuration-file)

## Slow shutdown

By default, zerotier-one will take 90 seconds for stopping the systemd service on system shutdown.

To override this:

```
# /etc/systemd/system/zerotier-one.service.d/override.conf
[Unit]
# Wait for network connectivity (service not activated by default) before starting
After=NetworkManager-wait-online.service

# Shutdown zerotier before tearing down the network stack
# https://github.com/zerotier/ZeroTierOne/pull/1093/commits/c9f07e855e2abac9c1a29cd412d888500a6a0bbb
After=network.target

[Service]
# Override default 90 second timeout in pathological conditions
TimeoutStopSec=5

```