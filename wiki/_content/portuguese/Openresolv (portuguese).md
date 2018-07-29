[Openresolv](https://roy.marples.name/projects/openresolv) é uma implementação de [resolvconf](https://en.wikipedia.org/wiki/resolvconf "wikipedia:resolvconf"), isto é, framework de gerenciamento de [resolv.conf](/index.php/Resolv.conf_(Portugu%C3%AAs) "Resolv.conf (Português)").

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
*   [2 Uso](#Uso)
*   [3 Usuários](#Usu.C3.A1rios)
*   [4 Assinantes](#Assinantes)
*   [5 Dicas e truques](#Dicas_e_truques)
    *   [5.1 Definindo vários valores por opções](#Definindo_v.C3.A1rios_valores_por_op.C3.A7.C3.B5es)

## Instalação

[Instale](/index.php/Instale "Instale") o pacote [openresolv](https://www.archlinux.org/packages/?name=openresolv).

## Uso

Openresolv fornece [resolvconf(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.8) e é configurado no `/etc/resolvconf.conf`. Veja [resolvconf.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolvconf.conf.5) para opções válidas.

A execução de `resolvconf -u` vai gerar `/etc/resolv.conf`.

## Usuários

Clientes [DHCP](/index.php/DHCP "DHCP") autônomos:

*   [dhcpcd](/index.php/Dhcpcd "Dhcpcd") tem um *hook* que usa *resolvconf* se ele estiver instalado.

[Gerenciadores de rede](/index.php/Gerenciadores_de_rede "Gerenciadores de rede"):

*   [netctl](/index.php/Netctl "Netctl") (usado por padrão)
*   [NetworkManager#Use openresolv](/index.php/NetworkManager#Use_openresolv "NetworkManager")

Clientes [VPN](/index.php/VPN "VPN"):

*   [OpenVPN#DNS](/index.php/OpenVPN#DNS "OpenVPN")
*   [strongSwan](/index.php/StrongSwan "StrongSwan")
*   [WireGuard](/index.php/WireGuard "WireGuard")

## Assinantes

Openresolv pode ser configurado para passar servidores de nome e domínios de pesquisa para resolvedores de DNS. Há suporte aos seguintes resolvedores:

*   [unbound](/index.php/Unbound "Unbound")
*   [dnsmasq#openresolv](/index.php/Dnsmasq#openresolv "Dnsmasq")
*   [BIND](/index.php/BIND "BIND")
*   [pdnsd](/index.php/Pdnsd "Pdnsd")

Veja a [documentação oficial](https://roy.marples.name/projects/openresolv/config) para instruções.

## Dicas e truques

### Definindo vários valores por opções

A página man não menciona isso, mas para definir vários valores, para opções que oferecem suporte a isso (p.ex., `name-servers`, `/etc/resolv_conf_options` etc.) no `/etc/resolvconf.conf`, você precisa escrevê-los separados por espaço entre aspas. Por exemplo:

 `/etc/resolvconf.conf` 
```
resolv_conf_options="edns0 single-request"
name_servers="dns1.example.com dns2.example.com dns3.example.com"
```