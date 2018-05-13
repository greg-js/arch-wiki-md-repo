[DNSCrypt](http://dnscrypt.info/) 2.x is a protocol that authenticates communications between a DNS client and a DNS resolver. It prevents DNS spoofing. It uses cryptographic signatures to verify that responses originate from the chosen DNS resolver and haven’t been tampered with.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Modify resolv.conf](#Modify_resolv.conf)
    *   [2.2 Start systemd service](#Start_systemd_service)

## Installation

[Install](/index.php/Install "Install") the [dnscrypt-proxy](https://www.archlinux.org/packages/?name=dnscrypt-proxy) package.

## Configuration

Edit `/etc/dnscrypt-proxy/dnscrypt-proxy.toml` file with the following contents:

```
listen_addresses = [] 

server_names = ['exampledns1', 'exampledns2']

[static.'exampledns1']
stamp = 'sdns://AgUAAAAAAAAAAAAOZG5zLmdvb2dsZS5jb20NL2V4cGVyaW1lbnRhbC'

[static.'exampledns2']
stamp = 'sdns://AgUAAAAAAAAAAAAOZG5zLmdvb2dsZS5jb20NL2V4cGVyaW1lbnRhbB'

```

**Note:** List of local addresses and ports to listen to. Can be IPv4 and/or IPv6\. When using systemd socket activation, choose an empty set (i.e. [] ).

```
listen_addresses = []

```

You can obtain the stamp using a tool such as [Online DNS Stamp calculator](https://stamps.dnscrypt.info/).

This is a basic configuration. Look [Dnscrypt-proxy 2 wiki](https://github.com/jedisct1/dnscrypt-proxy/wiki) for more details.

**Note:** The servers can include different properties. For example some do DNSSEC validation. If you want to use only the ones matching your requirements add them [[1]](https://github.com/jedisct1/dnscrypt-proxy/wiki/Configuration-Sources)

Look the example below.

```
listen_addresses = []

server_names = ['exampledns1', 'exampledns2']
require_dnssec = true # Server must support DNS security extensions (DNSSEC)

[static.'exampledns1']
stamp = 'sdns://AgUAAAAAAAAAAAAOZG5zLmdvb2dsZS5jb20NL2V4cGVyaW1lbnRhbC'

[static.'exampledns2']
stamp = 'sdns://AgUAAAAAAAAAAAAOZG5zLmdvb2dsZS5jb20NL2V4cGVyaW1lbnRhbB'

```

### Modify resolv.conf

After modify the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") file and replace the current set of resolver addresses with address for *localhost*:

```
nameserver 127.0.0.1

```

Other programs may overwrite this setting; see [resolv.conf#Preserve DNS settings](/index.php/Resolv.conf#Preserve_DNS_settings "Resolv.conf") for details.

### Start systemd service

Finally, [start and enable](/index.php/Enable "Enable") the `dnscrypt-proxy.service`.