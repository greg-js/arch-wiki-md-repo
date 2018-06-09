Artigos relacionados

*   [Serviços DNS alternativos](/index.php/Alternative_DNS_services "Alternative DNS services")
*   [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede")

Esse artigo explica como para configurar resolução de [nome de domínio](https://en.wikipedia.org/wiki/pt:Dom%C3%ADnio "wikipedia:pt:Domínio") e resolver nomes de domínio.

## Contents

*   [1 Name Service Switch](#Name_Service_Switch)
    *   [1.1 Verifique se você consegue resolver nomes de domínio](#Verifique_se_voc.C3.AA_consegue_resolver_nomes_de_dom.C3.ADnio)
*   [2 Resolvedor do glibc](#Resolvedor_do_glibc)
    *   [2.1 Sobrescrita do resolv.conf](#Sobrescrita_do_resolv.conf)
    *   [2.2 Limitar o tempo de lookup](#Limitar_o_tempo_de_lookup)
    *   [2.3 Lookup de hostname atrasado com IPv6](#Lookup_de_hostname_atrasado_com_IPv6)
    *   [2.4 Nomes de domínio local](#Nomes_de_dom.C3.ADnio_local)
*   [3 Systemd-resolved](#Systemd-resolved)
*   [4 Desempenho](#Desempenho)
*   [5 Utilitários de lookup](#Utilit.C3.A1rios_de_lookup)
*   [6 Veja também](#Veja_tamb.C3.A9m)

## Name Service Switch

	*"NSS (Português)" redireciona para cá. Para as bibliotecas criptográficas da Mozilla, veja [Network Security Services](/index.php/Network_Security_Services "Network Security Services").*

O recurso [Name Service Switch](https://en.wikipedia.org/wiki/pt:Name_Service_Switch "wikipedia:pt:Name Service Switch") (NSS) é parte da biblioteca C do GNU ([glibc](https://www.archlinux.org/packages/?name=glibc)) e apoia a API [getaddrinfo(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getaddrinfo.3), usada para resolver nomes de domínio. O NSS permite que bancos de dados do sistema sejam fornecidos por serviços separados, cuja ordem de pesquisa pode ser configurada pelo administrador no [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5). O banco de dados responsável pela resolução de nomes de domínio é o banco de dados `hosts`, para o qual a glibc oferece os seguintes serviços:

*   `file`: lê o arquivo `/etc/hosts`, veja [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)
*   `dns`: o [resolvedor do glibc](#Resolvedor_do_glibc) que lê `/etc/resolv.conf`, veja [resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5)

[Systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") fornece três serviços NSS para resolução de hostname:

*   [nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8) - um resolvedor de tronco de DNS em cache, descrito em [#Systemd-resolved](#Systemd-resolved)
*   [nss-myhostname(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-myhostname.8) - fornece resolução de hostname sem ter que editar `/etc/hosts`, descrito em [Configuração de rede#Resolução de hostname local](/index.php/Configura%C3%A7%C3%A3o_de_rede#Resolu.C3.A7.C3.A3o_de_hostname_local "Configuração de rede")
*   [nss-mymachines(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-mymachines.8) - fornece resolução de hostname para os nomes de contêineres locais de [systemd-machined(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-machined.8)

### Verifique se você consegue resolver nomes de domínio

Bancos de dados NSS podem ser consultados com [getent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getent.1). Você pode resolver um nome de domínio por meio do NSS usando:

```
$ getent hosts *nome_domínio*

```

**Nota:** Enquanto a maioria dos programas resolve nomes de domínio usando NSS, alguns podem ler `resolv.conf` e/ou `/etc/hosts` diretamente. Veja [Configuração de rede#Resolução de hostname local](/index.php/Configura%C3%A7%C3%A3o_de_rede#Resolu.C3.A7.C3.A3o_de_hostname_local "Configuração de rede").

## Resolvedor do glibc

O resolvedor de [DNS](https://en.wikipedia.org/wiki/pt:Sistema_de_Nomes_de_Dom%C3%ADnio "wikipedia:pt:Sistema de Nomes de Domínio") do glibc lê `/etc/resolv.conf` ([resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5)) para toda resolução para determinar os servidores de nome e opções para usar.

Servidores de nome *(nameservers)* listados primeiros são tentados primeiro, até os três servidores podem ser listados. Linhas iniciando com um cerquilha, `#`, são ignoradas.

**Nota:** O resolvedor do glibc não faz cache de consultas. Veja [#Desempenho](#Desempenho) para mais informações.

### Sobrescrita do resolv.conf

[Gerenciadores de rede](/index.php/Gerenciador_de_rede "Gerenciador de rede") tendem a sobrescrever `resolv.conf`, para particularidades veja a seção correspondente:

*   [dhcpcd#resolv.conf](/index.php/Dhcpcd#resolv.conf "Dhcpcd")
*   [netctl#resolv.conf](/index.php/Netctl#resolv.conf "Netctl")
*   [NetworkManager (Português)#resolv.conf](/index.php/NetworkManager_(Portugu%C3%AAs)#resolv.conf "NetworkManager (Português)")

Para evitar que programas sobrescrevam `resolv.conf`, você também pode protegê-lo contra gravação definindo o [atributo de arquivo](/index.php/File_attribute "File attribute") imutável.

**Dica:** Se você quiser que vários processos escrevam no `resolv.conf`, você pode usar [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)").

### Limitar o tempo de lookup

Se você for confrontado com uma consulta de hostname muito longa (seja no [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") ou enquanto navega), frequentemente ajuda a definir um pequeno tempo limite após o qual um servidor de nomes alternativo é usado. Para fazer isso, coloque o seguinte em `/etc/resolv.conf`:

```
options timeout:1

```

### Lookup de hostname atrasado com IPv6

Se você tiver um atraso de 5 segundos ao resolver os hostname, isso pode ser devido a um mau comportamento do servidor DNS/Firewall e somente dando uma resposta a uma solicitação paralela A e AAAA ([http://udrepper.livejournal.com/20948.html](http://udrepper.livejournal.com/20948.html) fonte]). Você pode corrigir isso configurando a seguinte opção no `/etc/resolv.conf`:

```
options single-request

```

### Nomes de domínio local

Se você quiser usar o hostname de máquinas locais sem os nomes de domínio totalmente qualificados, adicione uma linha ao `resolv.conf` com o domínio local, como:

```
domain exemplo.com.br

```

Dessa forma, você pode se referir a hosts locais como `maquinaprincipal1.exemplo.com.brm` como simplesmente `maquinaprincipal1` ao usar o comando *ssh*, mas o comando *drill* ainda requer os nomes de domínio totalmente qualificados para realizar pesquisas *(lookup)*.

## Systemd-resolved

[systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8) is a [systemd](/index.php/Systemd "Systemd") service that provides network name resolution to local applications via a [D-Bus](/index.php/D-Bus "D-Bus") interface, the `resolve` NSS service ([nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8)), and a local DNS stub listener on `127.0.0.53`.

*systemd-resolved* has four different modes for handling the [glibc resolver](#Glibc_resolver)'s *resolv.conf* (described in [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8#.2FETC.2FRESOLV.CONF)). We will focus here on the two most relevant modes.

1.  The mode in which *systemd-resolved* is a client of the `/etc/resolv.conf`. This mode preserves `/etc/resolv.conf` and is **compatible** with the procedures described in this page.
2.  The *systemd-resolved'*s **recommended** mode of operation: the DNS stub file as indicated below contains both the local stub `127.0.0.53` as the only DNS servers and a list of search domains.

 `/run/systemd/resolve/stub-resolv.conf` 
```
nameserver 127.0.0.53
search lan

```

The service users are advised to redirect the `/etc/resolv.conf` file to the local stub DNS resolver file `/run/systemd/resolve/stub-resolv.conf` managed by *systemd-resolved*. This propagates the systemd managed configuration to all the clients. This can be done by deleting or renaming the existing `/etc/resolv.conf` and replacing it by a symbolic link to the systemd stub:

```
# ln -s /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf

```

In this mode, the DNS servers are provided in the [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5) file:

 `/etc/systemd/resolved.conf` 
```
[Resolve]
**DNS=91.239.100.100 89.233.43.71**
...
```

In order to check the DNS actually used by *systemd-resolved*, the command to use is:

```
$ systemd-resolve --status

```

**Tip:**

*   To understand the context around the DNS choices and switches, one can turn on detailed debug information for *systemd-resolved* as described in [Systemd#Diagnosing a service](/index.php/Systemd#Diagnosing_a_service "Systemd").
*   The mode of operation of *systemd-resolved* is detected automatically, depending on whether `/etc/resolv.conf` is a symlink to the local stub DNS resolver file or contains server names.

## Desempenho

The [#Glibc resolver](#Glibc_resolver) does not cache queries. If you want local caching use [#Systemd-resolved](#Systemd-resolved) or set up a local caching [DNS server](/index.php/DNS_server "DNS server") and use `127.0.0.1`.

**Tip:** The *dig* and *drill* [#Lookup utilities](#Lookup_utilities) report the query time.

Internet service providers usually provide working DNS servers. A router may also add an extra DNS server in case it has its own cache server. Switching between DNS servers is transparent for Windows users, because if a DNS server is slow or does not work it will immediately switch to a better one. However, Linux usually takes longer to timeout, which could cause delays.

## Utilitários de lookup

To query specific DNS servers and DNS/[DNSSEC](/index.php/DNSSEC "DNSSEC") records you can use dedicated DNS lookup utilities. These tools implement DNS themselves and do not use [NSS](#Name_Service_Switch).

*   [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) provides [dig(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dig.1), [host(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/host.1), [nslookup(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nslookup.1) and a bunch of `dnssec-` tools.
*   [ldns](https://www.archlinux.org/packages/?name=ldns) provides [drill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/drill.1), which is similar to *dig*

For example, to query a specific nameserver with drill for the TXT records of a domain:

```
$ drill @*nameserver* TXT *domain*

```

If you do not specify a DNS server *dig* and *drill* use the nameservers defined in `/etc/resolv.conf`.

## Veja também

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/x-087-2-resolv.html)
*   [Debian Handbook](https://www.debian.org/doc/manuals/debian-handbook/sect.hostname-name-service.en.html#sect.name-resolution)