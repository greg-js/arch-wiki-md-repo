**Status de tradução:** Esse artigo é uma tradução de [IPv6](/index.php/IPv6 "IPv6"). Data da última tradução: 2018-12-31\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=IPv6&diff=0&oldid=529196) na versão em inglês.

Artigos relacionados

*   [IPv6 tunnel broker setup](/index.php/IPv6_tunnel_broker_setup "IPv6 tunnel broker setup")

No Arch Linux, IPv6 está habilitado por padrão.

## Contents

*   [1 Descoberta de vizinhança](#Descoberta_de_vizinhança)
*   [2 Autoconfiguração sem estado (SLAAC)](#Autoconfiguração_sem_estado_(SLAAC))
    *   [2.1 Para clientes](#Para_clientes)
    *   [2.2 Para gateways](#Para_gateways)
*   [3 Extensões de privacidade](#Extensões_de_privacidade)
    *   [3.1 dhcpcd](#dhcpcd)
    *   [3.2 NetworkManager](#NetworkManager)
    *   [3.3 systemd-networkd](#systemd-networkd)
    *   [3.4 connman](#connman)
*   [4 Endereço estático](#Endereço_estático)
*   [5 IPv6 e PPPoE](#IPv6_e_PPPoE)
*   [6 Delegação de prefixo (DHCPv6-PD)](#Delegação_de_prefixo_(DHCPv6-PD))
    *   [6.1 Com dibbler](#Com_dibbler)
    *   [6.2 Com dhcpcd](#Com_dhcpcd)
    *   [6.3 Com WIDE-DHCPv6](#Com_WIDE-DHCPv6)
    *   [6.4 Outros clientes](#Outros_clientes)
*   [7 Desabilitar IPv6](#Desabilitar_IPv6)
    *   [7.1 Desabilitar funcionalidade](#Desabilitar_funcionalidade)
    *   [7.2 Outros programas](#Outros_programas)
        *   [7.2.1 dhcpcd](#dhcpcd_2)
        *   [7.2.2 NetworkManager](#NetworkManager_2)
        *   [7.2.3 ntpd](#ntpd)
    *   [7.3 systemd-networkd](#systemd-networkd_2)
*   [8 Veja também](#Veja_também)

## Descoberta de vizinhança

Pingar o endereço multicast `ff02::1` resulta em todos os hosts no escopo link-local responderem. Uma interface tem que ser especificada:

```
$ ping ff02::1%eth0

```

Após isso, você pode obter uma lista de todos os vizinhos na rede local com:

```
$ ip -6 neigh

```

Com um ping para o endereço multicast `ff02::2` apenas roteadores vão responderem.

Se você adicionar uma opção `-I *seu-ipv6-global*`, hosts link-local vão responder com seus endereços de escopo link-global. A interface pode ser omitida neste caso:

```
$ ping -I 2001:4f8:fff6::21 ff02::1

```

## Autoconfiguração sem estado (SLAAC)

A maneira mais fácil de adquirir um endereço IPv6, desde que sua rede esteja configurada, é através de *Stateless address autoconfiguration* (abreviado para SLAAC, que poderia ser traduzido para português como "Autoconfiguração de endereço sem estado"). O endereço é inferido automaticamente do prefixo que o seu roteador anuncia e não requer nenhuma configuração adicional nem software especializado, como um cliente DHCP.

### Para clientes

Se você está usando o [netctl](/index.php/Netctl "Netctl"), você só precisa adicionar a seguinte linha para sua configuração Ethernet ou sem fio.

```
IP6=stateless

```

Se você está usando o [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)"), então endereços IP são habilitados automaticamente se houver anúncios para eles na rede.

Observe que a autoconfiguração sem estado funciona com a condição de que pacotes icmp IPv6 sejam permitidos em toda a rede. Portanto, para o lado do cliente, os pacotes `ipv6-icmp` devem ser aceitos. Se você estiver usando um [Firewall stateful simples](/index.php/Simple_stateful_firewall "Simple stateful firewall") ou o [iptables](/index.php/Iptables "Iptables"), você só precisa adicionar:

```
-A INPUT -p ipv6-icmp -j ACCEPT

```

Se você estiver usando um outro front-end de firewall (ufw, shorewall, etc), consulte sua documentação sobre como habilitar os pacotes `ipv6-icmp`.

### Para gateways

Para distribuir corretamente os IPv6s aos clientes da rede, precisaremos usar um daemon de anúncio. A ferramenta padrão para este trabalho é [radvd](https://www.archlinux.org/packages/?name=radvd) e está disponível em [repositórios oficiais](/index.php/Reposit%C3%B3rios_oficiais "Repositórios oficiais"). Configuração do radvd é bastante simples. Edite `/etc/radvd.conf` para incluir:

```
# substitua LAN com sua interface de LAN
interface LAN {
  AdvSendAdvert on;
  MinRtrAdvInterval 3;
  MaxRtrAdvInterval 10;
  prefix ::/64 {
    AdvOnLink on;
    AdvAutonomous on;
    AdvRouterAddr on;
  };
};

```

A configuração acima dirá aos clientes para se autoconfigurarem usando endereços do bloco /64 anunciado. Observe que a configuração acima anuncia "todos os prefixos disponíveis" atribuídos à interface de LAN. Se você quiser limitar os prefixos anunciados em vez de `::/64` use o prefixo desejado, por exemplo, `2001:DB8::/64`. O bloco `prefix` pode ser repetido várias vezes para mais prefixos.

O gateway também deve permitir o tráfego de pacotes `ipv6-icmp` em todas as cadeias básicas. Para um [Firewall stateful simples](/index.php/Simple_stateful_firewall "Simple stateful firewall") ou o [iptables](/index.php/Iptables "Iptables"), adicione:

```
-A INPUT -p ipv6-icmp -j ACCEPT
-A OUTPUT -p ipv6-icmp -j ACCEPT
-A FORWARD -p ipv6-icmp -j ACCEPT

```

Ajuste de acordo com outros front-ends de firewall e não se esqueça de habilitar `radvd.service`.

## Extensões de privacidade

When a client acquires an address through SLAAC its IPv6 address is derived from the advertised prefix and the MAC address of the network interface of the client. This may raise security concerns as the MAC address of the computer can be easily derived by the IPv6 address. In order to tackle this problem the *IPv6 Privacy Extensions* standard ([RFC 4941](https://tools.ietf.org/html/rfc4941)) has been developed. With privacy extensions the kernel generates a *temporary* address that is mangled from the original autoconfigured address. Private addresses are preferred when connecting to a remote server so the original address is hidden. To enable Privacy Extensions reproduce the following steps:

Add these lines to `/etc/sysctl.d/40-ipv6.conf`:

```
# Enable IPv6 Privacy Extensions
net.ipv6.conf.all.use_tempaddr = 2
net.ipv6.conf.default.use_tempaddr = 2
net.ipv6.conf.*nic0*.use_tempaddr = 2
...
net.ipv6.conf.*nicN*.use_tempaddr = 2

```

Where `nic0` to `nicN` are your **N**etwork **I**nterface **C**ards. You can find their names using the instructions in [Network configuration#Listing network interfaces](/index.php/Network_configuration#Listing_network_interfaces "Network configuration"). The `all.use_tempaddr` or `default.use_tempaddr` parameters are not applied to nic's that already exist when the [sysctl](/index.php/Sysctl "Sysctl") settings are executed.

After a reboot, at the latest, Privacy Extensions should be enabled.

### dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") includes in its default configuration file since version 6.4.0 the option `slaac private`, which enables "Stable Private IPv6 Addresses instead of hardware based ones", implementing [RFC 7217](https://tools.ietf.org/html/rfc7217) ([commit](http://roy.marples.name/projects/dhcpcd/info/8aa9dab00dc72c453aeccbde885ecce27a3d81ff)). Therefore, it is not necessary to change anything, except if it is desired to change of IPv6 address more often than each time the system is connected to a new network. Set it to `slaac hwaddr` for a stable address.

### NetworkManager

NetworkManager does not honour the settings placed in `/etc/sysctl.d/40-ipv6.conf`. This can be verified by running `$ ip -6 addr show *interface*` after rebooting: no `scope global **temporary**` address appears besides the regular one.

To enable IPv6 Privacy Extensions by default, add these lines to `/etc/NetworkManager/NetworkManager.conf`

 `/etc/NetworkManager/NetworkManager.conf` 
```
...
**[connection]**
**ipv6.ip6-privacy=2**
```

In order to enable IPv6 Privacy Extensions for individual NetworkManager-managed connections, edit the desired connection keyfile in `/etc/NetworkManager/system-connections/` and append to its `[ipv6]` section the key-value pair `ip6-privacy=2`:

 `/etc/NetworkManager/system-connections/*example_connection*` 
```
...
[ipv6]
method=auto
**ip6-privacy=2**
```

**Note:** Although it may seem the `scope global temporary` IPv6 address created by enabling Privacy Extensions never gets renewed (it never shifts to `deprecated` status at the term of its `valid_lft` lifetime), it is to be verified over a longer period of time that this address **does** indeed change.

### systemd-networkd

Systemd-networkd also does not honor the settings `net.ipv6.conf.xxx.use_tempaddr` placed in `/etc/sysctl.d/40-ipv6.conf` unless the option `IPv6PrivacyExtensions` is set with the value `kernel` in the .network file(s).

Other options for the IPv6 Privacy Extensions like:

```
net.ipv6.conf.xxx.temp_prefered_lft
net.ipv6.conf.xxx.temp_valid_lft

```

are honored, however.

**Note:** `temp_prefered_lft` is the variable name, preferred has to be misspelled.

See [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") and [systemd.network(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.network.5) for details.

### connman

Add to `/var/lib/connman/settings` under the global section:

```
[global]
IPv6.privacy=preferred

```

## Endereço estático

Sometimes, using a static address can improve security. For example, if your local router uses Neighbor Discovery or radvd ([RFC 2461](http://www.apps.ietf.org/rfc/rfc2461.html)), your interface will automatically be assigned an address based on its MAC address (using IPv6's Stateless Autoconfiguration). This may be less than ideal for security since it allows a system to be tracked even if the network portion of the IP address changes.

To assign a static IP address using [netctl](/index.php/Netctl "Netctl"), look at the example profile in `/etc/netctl/examples/ethernet-static`. The following lines are important:

```
...
# For IPv6 static address configuration
IP6=static
Address6=('1234:5678:9abc:def::1/64' '1234:3456::123/96')
Routes6=('abcd::1234')
Gateway6='1234:0:123::abcd'

```

**Note:** If you are connected IPv6-only, then you need to determine your IPv6 DNS server. For example:
```
DNS=('6666:6666::1' '6666:6666::2')

```
If your provider did not give you IPv6 DNS and you are not running your own, you can choose from the [resolv.conf](/index.php/Resolv.conf "Resolv.conf") article.

## IPv6 e PPPoE

The standard tool for PPPoE, `pppd`, provides support for IPv6 on PPPoE as long as your ISP and your modem support it. Just add the following to `/etc/ppp/pppoe.conf`

```
+ipv6

```

If you are using [netctl](/index.php/Netctl "Netctl") for PPPoE then just add the following to your netctl configuration instead

```
PPPoEIP6=yes

```

## Delegação de prefixo (DHCPv6-PD)

**Note:** This section is targeted towards custom gateway configuration, not client machines. For standard market routers please consult the documentation of your router on how to enable prefix delegation.

Prefix delegation is a common IPv6 deployment technique used by many ISPs. It is a method of assigning a network prefix to a user site (ie. local network). A router can be configured to assign different network prefixes to various subnetworks. The ISP handles out a network prefix using DHCPv6 (usually a `/56` or `/64`) and a dhcp client assigns the prefixes to the local network. For a simple two interface gateway it practically assigns an IPv6 prefix to the interface connected to to the local network from an address acquired through the interface connected to WAN (or a pseudo-interface such as ppp).

### Com dibbler

[Dibbler](http://klub.com.pl/dhcpv6/) is a portable DHCPv6 client a server which can be used for Prefix delegation. It is available in the [AUR](/index.php/AUR "AUR") as [dibbler](https://aur.archlinux.org/packages/dibbler/).

If you are using `dibbler` edit `/etc/dibbler/client.conf`

```
log-mode short
log-level 7
# use the interface connected to your WAN
iface "WAN" {
  ia
  pd
}

```

**Tip:** Read dibbler-client(8) for more information.

### Com dhcpcd

[dhcpcd](/index.php/Dhcpcd "Dhcpcd") apart from IPv4 dhcp support also provides a fairly complete implementation of the DHCPv6 client standard which includes DHCPv6-PD. If you are using `dhcpcd` edit `/etc/dhcpcd.conf`. You might already be using dhcpcd for IPv4 so just update your existing configuration.

```
duid
noipv6rs
waitip 6
# Uncomment this line if you are running dhcpcd for IPv6 only.
#ipv6only

# use the interface connected to WAN
interface WAN
ipv6rs
iaid 1
# use the interface connected to your LAN
ia_pd 1 LAN
#ia_pd 1/::/64 LAN/0/64

```

This configuration will ask for a prefix from WAN interface (`WAN`) and delegate it to the internal interface (`LAN`). In the event that a `/64` range is issued, you will need to use the 2nd `ia_pd instruction` that is commented out instead. It will also disable router solicitations on all interfaces except for the WAN interface (`WAN`).

**Tip:** Also read [dhcpcd(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.8)and [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5).

### Com WIDE-DHCPv6

[WIDE-DHCPv6](http://wide-dhcpv6.sourceforge.net/) is an open-source implementation of Dynamic Host Configuration Protocol for IPv6 (DHCPv6) originally developed by the KAME project. It is available in the [AUR](/index.php/AUR "AUR") as [wide-dhcpv6](https://aur.archlinux.org/packages/wide-dhcpv6/).

If you are using `wide-dhcpv6` edit `/etc/wide-dhcpv6/dhcp6c.conf`

```
# use the interface connected to your WAN
interface WAN {
  send ia-pd 0;
};

id-assoc pd 0 {
  # use the interface connected to your LAN
  prefix-interface LAN {
    sla-id 1;
    sla-len 8;
  };
};

```

**Note:** `sla-len` should be set so that `(WAN-prefix) + (sla-len) = 64`. In this case it is set up for a `/56` prefix 56+8=64\. For a `/64` prefix `sla-len` should be `0`.

To enable/start wide-dhcpv6 client use the following command. Change `WAN` with the interface that is connected to your WAN.

```
# systemctl enable/start dhcp6c@WAN.service

```

**Tip:** Read dhcp6c(8) and dhcp6c.conf(5) for more information.

### Outros clientes

[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") claims to be capable of DHCPv6-PD but is lacking documentation on how to do it.

[dhclient](/index.php/Dhclient "Dhclient") can also request a prefix, but assigning that prefix, or parts of that prefix to interfaces must be done using a dhclient exit script. For example: [https://github.com/jaymzh/v6-gw-scripts/blob/master/dhclient-ipv6](https://github.com/jaymzh/v6-gw-scripts/blob/master/dhclient-ipv6).

## Desabilitar IPv6

**Note:** The Arch kernel has IPv6 support built in directly, therefore a module cannot be blacklisted.

### Desabilitar funcionalidade

**Warning:** Disabling the IPv6 stack can break certain programs which expect it to be enabled. [FS#46297](https://bugs.archlinux.org/task/46297)

Adding `ipv6.disable=1` to the kernel line disables the whole IPv6 stack, which is likely what you want if you are experiencing issues. See [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") for more information.

Alternatively, adding `ipv6.disable_ipv6=1` instead will keep the IPv6 stack functional but will not assign IPv6 addresses to any of your network devices.

One can also avoid assigning IPv6 addresses to specific network interfaces by adding the following sysctl config to `/etc/sysctl.d/40-ipv6.conf`:

```
# Disable IPv6
net.ipv6.conf.all.disable_ipv6 = 1
net.ipv6.conf.*nic0*.disable_ipv6 = 1
...
net.ipv6.conf.*nicN*.disable_ipv6 = 1

```

Note that you must list all of the targeted interfaces explicitly, as disabling `all.disable_ipv6` does not apply to interfaces that are already "up" when sysctl settings are applied.

Note 2, if disabling IPv6 by sysctl, you should comment out the IPv6 hosts in your `/etc/hosts`:

```
#<ip-address> <hostname.domain.org> <hostname>
127.0.0.1 localhost.localdomain localhost
#::1 localhost.localdomain localhost

```

otherwise there could be some connection errors because hosts are resolved to their IPv6 address which is not reachable.

### Outros programas

Disabling IPv6 functionality in the kernel does not prevent other programs from trying to use IPv6\. In most cases, this is completely harmless, but if you find yourself having issues with that program, you should consult the program's manual pages for a way to disable that functionality.

#### dhcpcd

*dhcpcd* will continue to harmlessly attempt to perform IPv6 router solicitation. To disable this, as stated in the [dhcpcd.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dhcpcd.conf.5)[man page](/index.php/Man_page "Man page"), add the following to `/etc/dhcpcd.conf`:

```
noipv6rs
noipv6

```

#### NetworkManager

To disable IPv6 in NetworkManager, right click the network status icon, and select *Edit Connections > Wired >* Network name *> Edit > IPv6 Settings > Method > Ignore/Disabled*

Then click "Save".

#### ntpd

Following advice in [systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd"), change how systemd starts `ntpd.service`:

```
# systemctl edit ntpd.service

```

This will create a drop-in snippet that will be run instead of the default `ntpd.service`. The `-4` flag prevents IPv6 from being used by the ntp daemon. Put the following into the drop-in snippet:

```
[Service]
ExecStart=
ExecStart=/usr/bin/ntpd -4 -g -u ntp:ntp

```

which first clears the previous `ExecStart`, and then replaces it with one that includes the `-4` flag.

### systemd-networkd

networkd supports disabling IPv6 on a per-interface basis. When a network unit's `[Network]` section has either `LinkLocalAddressing=ipv4` or `LinkLocalAddressing=no`, networkd will not try to configure IPv6 on the matching interfaces.

Note however that even when using the above option, networkd will still be expecting to receive router advertisements if IPv6 is not disabled globally. If IPv6 traffic is not being received by the interface (e.g. due to sysctl or ip6tables settings), it will remain in the configuring state and potentially cause timeouts for services waiting for the network to be fully configured. To avoid this, the `IPv6AcceptRA=no` option should also be set in the `[Network]` section.

## Veja também

*   [IPv6](https://www.kernel.org/doc/Documentation/networking/ipv6.txt) - kernel.org documentation
*   [IPv6 temporary addresses](http://www.ipsidixit.net/2012/08/09/ipv6-temporary-addresses-and-privacy-extensions/) - a summary about temporary addresses and privacy extensions
*   [IPv6 prefixes](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/ch03s02.html) - a summary of prefix types
*   [net.ipv6 options](http://tldp.org/HOWTO/Linux+IPv6-HOWTO/ch11s02.html) - documentation of kernel parameters