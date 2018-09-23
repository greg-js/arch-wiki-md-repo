**Status de tradução:** Esse artigo é uma tradução de [Domain name resolution](/index.php/Domain_name_resolution "Domain name resolution"). Data da última tradução: 2018-09-22\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Domain_name_resolution&diff=0&oldid=542529) na versão em inglês.

Artigos relacionados

*   [Serviços DNS alternativos](/index.php/Alternative_DNS_services "Alternative DNS services")
*   [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede")

Em geral, um [nome de domínio](https://en.wikipedia.org/wiki/pt:Dom%C3%ADnio "wikipedia:pt:Domínio") representa um endereço IP e está associado a ele no [Sistema de Nomes de Domínio](https://en.wikipedia.org/wiki/pt:Sistema_de_Nomes_de_Dom%C3%ADnio "wikipedia:pt:Sistema de Nomes de Domínio"), ou *Domain Name System* (DNS). Esse artigo explica como para configurar resolução de nome de domínio e resolver nomes de domínio.

## Contents

*   [1 Name Service Switch](#Name_Service_Switch)
    *   [1.1 Verifique se você consegue resolver nomes de domínio](#Verifique_se_voc.C3.AA_consegue_resolver_nomes_de_dom.C3.ADnio)
*   [2 Resolvedor do glibc](#Resolvedor_do_glibc)
    *   [2.1 Sobrescrita do /etc/resolv.conf](#Sobrescrita_do_.2Fetc.2Fresolv.conf)
    *   [2.2 Limitar o tempo de pesquisa](#Limitar_o_tempo_de_pesquisa)
    *   [2.3 Pesquisa de hostname atrasada com IPv6](#Pesquisa_de_hostname_atrasada_com_IPv6)
    *   [2.4 Nomes de domínio local](#Nomes_de_dom.C3.ADnio_local)
*   [3 Resolvedores](#Resolvedores)
*   [4 Privacidade](#Privacidade)
*   [5 Utilitários de pesquisa](#Utilit.C3.A1rios_de_pesquisa)
*   [6 Veja também](#Veja_tamb.C3.A9m)

## Name Service Switch

	*"NSS (Português)" redireciona para cá. Para as bibliotecas criptográficas da Mozilla, veja [Network Security Services](/index.php/Network_Security_Services "Network Security Services").*

O recurso [Name Service Switch](https://en.wikipedia.org/wiki/pt:Name_Service_Switch "wikipedia:pt:Name Service Switch") (NSS) é parte da biblioteca C do GNU ([glibc](https://www.archlinux.org/packages/?name=glibc)) e apoia a API [getaddrinfo(3)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getaddrinfo.3), usada para resolver nomes de domínio. O NSS permite que bancos de dados do sistema sejam fornecidos por serviços separados, cuja ordem de pesquisa pode ser configurada pelo administrador no [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5). O banco de dados responsável pela resolução de nomes de domínio é o banco de dados `hosts`, para o qual a glibc oferece os seguintes serviços:

*   `file`: lê o arquivo `/etc/hosts`, veja [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)
*   `dns`: o [resolvedor do glibc](#Resolvedor_do_glibc) que lê `/etc/resolv.conf`, veja [resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5)

[Systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") fornece três serviços NSS para resolução de hostname:

*   [nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8) - um resolvedor de tronco de DNS em cache, descrito em [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved")
*   [nss-myhostname(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-myhostname.8) - fornece resolução de hostname sem ter que editar `/etc/hosts`, descrito em [Configuração de rede#Resolução de hostname local](/index.php/Configura%C3%A7%C3%A3o_de_rede#Resolu.C3.A7.C3.A3o_de_hostname_local "Configuração de rede")
*   [nss-mymachines(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-mymachines.8) - fornece resolução de hostname para os nomes de contêineres locais de [systemd-machined(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-machined.8)

### Verifique se você consegue resolver nomes de domínio

Bancos de dados NSS podem ser consultados com [getent(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/getent.1). Você pode resolver um nome de domínio por meio do NSS usando:

```
$ getent hosts *nome_domínio*

```

**Nota:** Enquanto a maioria dos programas resolve nomes de domínio usando NSS, alguns podem ler `/etc/resolv.conf` e/ou `/etc/hosts` diretamente. Veja [Configuração de rede#Resolução de hostname local](/index.php/Configura%C3%A7%C3%A3o_de_rede#Resolu.C3.A7.C3.A3o_de_hostname_local "Configuração de rede").

## Resolvedor do glibc

O resolvedor do glibc lê `/etc/resolv.conf` para toda resolução para determinar os servidores de nome e opções para usar.

[resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5) lista servidores de nomes juntos com algumas opções de configuração.

Servidores de nome *(nameservers)* listados primeiros são tentados primeiro, até os três servidores podem ser listados. Linhas iniciando com um cerquilha (`#`) são ignoradas.

**Nota:** O resolvedor do glibc não faz cache de consultas. Para melhorar tempo de consulta, você pode configurar um resolvedor em cache. Veja [#Resolvedores](#Resolvedores) para mais informações.

### Sobrescrita do /etc/resolv.conf

[Gerenciadores de rede](/index.php/Gerenciadores_de_rede "Gerenciadores de rede") tendem a sobrescrever `/etc/resolv.conf`, para particularidades veja a seção correspondente:

*   [dhcpcd#resolv.conf](/index.php/Dhcpcd#resolv.conf "Dhcpcd")
*   [netctl#resolv.conf](/index.php/Netctl#resolv.conf "Netctl")
*   [NetworkManager#resolv.conf](/index.php/NetworkManager#resolv.conf "NetworkManager")

Para evitar que programas sobrescrevam `/etc/resolv.conf`, você também pode protegê-lo contra gravação definindo o [atributo de arquivo](/index.php/File_attribute "File attribute") imutável:

```
# chattr +i /etc/resolv.conf

```

**Dica:** Se você quiser que vários processos escrevam no `/etc/resolv.conf`, você pode usar [resolvconf](/index.php/Resolvconf_(Portugu%C3%AAs) "Resolvconf (Português)").

### Limitar o tempo de pesquisa

Se você for confrontado com uma consulta de hostname muito longa (seja no [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") ou enquanto navega), frequentemente ajuda a definir um pequeno tempo limite após o qual um servidor de nomes alternativo é usado. Para fazer isso, coloque o seguinte em `/etc/resolv.conf`:

```
options timeout:1

```

### Pesquisa de hostname atrasada com IPv6

Se você tiver um atraso de 5 segundos ao resolver os hostname, isso pode ser devido a um mau comportamento do servidor DNS/Firewall e somente dando uma resposta a uma solicitação paralela A e AAAA.[[1]](https://udrepper.livejournal.com/20948.html) Você pode corrigir isso configurando a seguinte opção no `/etc/resolv.conf`:

```
options single-request

```

### Nomes de domínio local

Se você quiser usar o hostname de máquinas locais sem os nomes de domínio totalmente qualificados, adicione uma linha ao `/etc/resolv.conf` com o domínio local, como:

```
domain exemplo.com.br

```

Dessa forma, você pode se referir a hosts locais como `maquinaprincipal1.exemplo.com.brm` como simplesmente `maquinaprincipal1` ao usar o comando *ssh*, mas o comando *drill* ainda requer os nomes de domínio totalmente qualificados para realizar pesquisas.

## Resolvedores

O resolvedor do Glibc fornece apenas as necessidades mais básicas, não armazena em cache as consultas nem fornece nenhum recurso de segurança. Se você deseja mais funcionalidade, use outro resolvedor.

**Dica:**

*   Os [utilitários de pesquisa](#Utilit.C3.A1rios_de_pesquisa) *drill* ou *dig* relatam o tempo de consulta.
*   Um roteador geralmente configura seu próprio resolvedor de cache como o servidor DNS da rede, fornecendo assim o cache DNS para toda a rede.
*   Se demorar muito para mudar para o próximo servidor DNS, você pode tentar [diminuir o tempo limite](#Limitar_o_tempo_de_pesquisa).

Na tabela abaixo, as colunas têm o seguinte sentido:

*   *Cache*: [Faz cache](https://en.wikipedia.org/wiki/Name_server#Caching_name_server "wikipedia:Name server") de consultas DNS para melhorar os tempos de pesquisa de solicitações idênticas subsequentes.
*   *Recursor*: pode [consultar recursivamente](https://en.wikipedia.org/wiki/Name_server#Recursive_query "wikipedia:Name server") o nome de domínio iniciando da [zona raiz do DNS](https://en.wikipedia.org/wiki/DNS_root_zone "wikipedia:DNS root zone").
*   *Compatibilidade com resolvconf*: pode adquirir servidores de nomes e domínios de pesquisa, para usar solicitações de encaminhamento, de softwares que os definem usando [resolvconf](/index.php/Resolvconf_(Portugu%C3%AAs) "Resolvconf (Português)").
*   *Valida DNSSEC*: [valida](https://en.wikipedia.org/wiki/Domain_Name_System_Security_Extensions#The_lookup_procedure "wikipedia:Domain Name System Security Extensions") respostas de consulta de DNS usando [DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)").
*   *DNS por TLS*: tem suporte a comunicação criptografada com servidor(es) DNS upstream usando o protocolo [DNS over TLS](https://en.wikipedia.org/wiki/DNS_over_TLS "wikipedia:DNS over TLS").
*   *DNS por HTTPS*: tem suporte a comunicação criptografada com servidor(es) DNS upstream usando o protocolo [DNS over HTTPS](https://en.wikipedia.org/wiki/DNS_over_HTTPS "wikipedia:DNS over HTTPS").

| Resolvedor | Cache | Recursor | Compatibilidade *resolvconf* | Valida DNSSEC | DNS por TLS | DNS por HTTPS | Notas |
| [glibc](#Resolvedor_do_glibc) | Não | Não | [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)") | Não | Não | Não |
| [BIND](/index.php/BIND "BIND") | Sim | Sim | se inscreve no [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)") | Sim |  ? |  ? |
| [dnscrypt-proxy](/index.php/Dnscrypt-proxy_(Portugu%C3%AAs) "Dnscrypt-proxy (Português)") | Sim | Não | Não | Não | Não | Sim | Implementa um cliente de protocolo [DNSCrypt](https://en.wikipedia.org/wiki/DNSCrypt "wikipedia:DNSCrypt"). |
| [dnsmasq](/index.php/Dnsmasq_(Portugu%C3%AAs) "Dnsmasq (Português)") | Sim | Não | se inscreve no [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)") | Sim | [Não](http://lists.thekelleys.org.uk/pipermail/dnsmasq-discuss/2018q2/012131.html) | Não |
| [Knot Resolver](/index.php/Knot_Resolver "Knot Resolver") | Sim | Sim | Não | Sim | Sim | [Não](https://gitlab.labs.nic.cz/knot/knot-resolver/issues/243) |
| [pdnsd](/index.php/Pdnsd "Pdnsd") | Sim | Sim | se inscreve no [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)") | Não | Não | Não |
| [Stubby](/index.php/Stubby "Stubby") | Não | Não | Não | Sim | Sim | Não |
| [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved") | Sim | Não | [systemd-resolvconf](/index.php/Systemd-resolvconf "Systemd-resolvconf") | Sim | Inseguro | [Não](https://github.com/systemd/systemd/issues/8639) |
| [Unbound](/index.php/Unbound "Unbound") | Sim | Sim | se inscreve no [openresolv](/index.php/Openresolv_(Portugu%C3%AAs) "Openresolv (Português)") | Sim | Sim | [Não](https://nlnetlabs.nl/bugs-script/show_bug.cgi?id=1200) |

1.  Do [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5): *Note que o resolvedor não é capaz de autenticar o servidor, ele é vulnerável a ataques "man-in-the-middle".* [[2]](https://github.com/systemd/systemd/issues/9397) Além disso, o único modo suportado é "opportunistic", o que *torna o DNS-over-TLS vulnerável a ataques de "downgrade"*.

## Privacidade

A maioria dos servidores DNS mantém um registro de endereços IP e sites visitados em uma base mais ou menos temporária. Os dados coletados podem ser usados para realizar vários estudos estatísticos. Informações de identificação pessoal têm valor e também podem ser alugadas ou vendidas a terceiros. O artigo [Serviços DNS alternativos](/index.php/Alternative_DNS_services "Alternative DNS services") fornece uma lista de serviços populares, verifique sua política de privacidade para obter informações sobre como os dados do usuário são manipulados.

## Utilitários de pesquisa

Para consultar servidores DNS específicos e registros DNS/[DNSSEC](/index.php/DNSSEC_(Portugu%C3%AAs) "DNSSEC (Português)"), você pode usar utilitários de pesquisa de DNS dedicados. Essas ferramentas implementam o próprio DNS e não usam [NSS](/index.php/NSS_(Portugu%C3%AAs) "NSS (Português)").

*   [ldns](https://www.archlinux.org/packages/?name=ldns) fornece [drill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/drill.1), que é uma ferramenta projetada para obter informações do DNS.

Por exemplo, para consultar um servidor de nomes específico com drill por registros TXT de um domínio:

```
$ drill @*servidor-de-nome* TXT *domínio*

```

Se você não especificar um servidor DNS, *drill* use os servidores de nome definidos em `/etc/resolv.conf`.

*   [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) fornece [dig(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dig.1), [host(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/host.1), [nslookup(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nslookup.1) e um monte de ferramentas `dnssec-`.

## Veja também

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/x-087-2-resolv.html)
*   [Debian Handbook](https://www.debian.org/doc/manuals/debian-handbook/sect.hostname-name-service.en.html#sect.name-resolution)