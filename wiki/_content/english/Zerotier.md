Zerotier is an open source, cross-platform and easy to use virtual LAN / Hamachi alternative, also available on Android, ios, Mac, Windows. A GUI is only available on Mac and Windows according to the developers.

## Installing

ZeroTier can be [installed](/index.php/Install "Install") with the [zerotier-one](https://www.archlinux.org/packages/?name=zerotier-one).

## Configuration

You will need to create an account over at [My Zerotier](https://my.zerotier.com/) and create a network and select your desired options, It can have either IPv4 or IPv6 or both. Keep note of the network id that you will like to use, you will be needing it later on. Leave the network page open that you will use since you will need to authorize each computer or device, also verify that it has an ip

To begin [start](/index.php/Start "Start") `zerotier-one.service`, if one would like it to start at boot [enable](/index.php/Enable "Enable") `zerotier-one.service`. to find out what your computer id,it will be a 10 alphanumeric similar to 89e92ceee5, is run:

 `# zerotier-cli info` 
```
200 info 89e92ceee5 1.2.4 ONLINE

```

where 89e92ceee5 is address and 1.2.4 is the version, followed by its status

Next you will need to run to join a network:

```
# zerotier-cli join *network_id*

```

The network will be 16 alphanumeric similiar to 8056c2e21c000001 which can be found at the top of the network page under settings.

Back on the network page at my.zerotier, you should see all address that have joined under members. Be sure sure to check the authorize for the desired addresses, and verify that it has IP address. You may need to run [dhcpcd](/index.php/Dhcpcd "Dhcpcd") to acquire the new IP address locally.

To verify that all devices can see each other you can [ping](/index.php/Ping "Ping") each address with its associated IP, like so

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