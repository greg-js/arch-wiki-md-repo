**Status de tradução:** Esse artigo é uma tradução de [openresolv](/index.php/Openresolv "Openresolv"). Data da última tradução: 2018-10-30\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Openresolv&diff=0&oldid=547380) na versão em inglês.

Artigos relacionados

*   [systemd-resolvconf](/index.php/Systemd-resolvconf "Systemd-resolvconf")

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

*   [Unbound](/index.php/Unbound "Unbound")
*   [dnsmasq (Português)#openresolv](/index.php/Dnsmasq_(Portugu%C3%AAs)#openresolv "Dnsmasq (Português)")
*   [BIND](/index.php/BIND "BIND")
*   [pdnsd](/index.php/Pdnsd "Pdnsd")

Veja a [documentação oficial](https://roy.marples.name/projects/openresolv/config) para instruções.

## Dicas e truques

### Definindo vários valores por opções

A página man não menciona isso, mas para definir vários valores, para opções que oferecem suporte a isso (p.ex., `name_servers`, `/etc/resolv_conf_options` etc.) no `/etc/resolvconf.conf`, você precisa escrevê-los separados por espaço entre aspas. Por exemplo:

 `/etc/resolvconf.conf` 
```
resolv_conf_options="edns0 single-request"
name_servers="192.168.35.1 fd7b:d0bd:7a6e::1"
```