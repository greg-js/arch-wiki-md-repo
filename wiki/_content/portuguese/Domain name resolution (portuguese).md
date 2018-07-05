Artigos relacionados

*   [Serviços DNS alternativos](/index.php/Alternative_DNS_services "Alternative DNS services")
*   [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede")

Em geral, um [nome de domínio](https://en.wikipedia.org/wiki/pt:Dom%C3%ADnio "wikipedia:pt:Domínio") representa um endereço IP e está associado a ele no [Sistema de Nomes de Domínio](https://en.wikipedia.org/wiki/pt:Sistema_de_Nomes_de_Dom%C3%ADnio "wikipedia:pt:Sistema de Nomes de Domínio"), ou *Domain Name System* (DNS). Esse artigo explica como para configurar resolução de nome de domínio e resolver nomes de domínio.

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
*   [5 Privacidade](#Privacidade)
*   [6 Utilitários de lookup](#Utilit.C3.A1rios_de_lookup)
*   [7 Veja também](#Veja_tamb.C3.A9m)

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

O resolvedor do glibc lê `/etc/resolv.conf` para toda resolução para determinar os servidores de nome e opções para usar.

[resolv.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolv.conf.5) lista servidores de nomes juntos com algumas opções de configuração.

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

[systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8) é um serviço [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") que fornece resolução de nome de rede para aplicativos locais por uma interface [D-Bus](/index.php/D-Bus "D-Bus"), o serviço NSS `resolve` ([nss-resolve(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nss-resolve.8)) e um *listener* DNS local em `127.0.0.53`.

*systemd-resolved* tem quatro modos diferentes para lidar com o *resolv.conf* do [resolvedor do glibc](#Resolvedor_do_glibc) (descrito em [systemd-resolved(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-resolved.8#.2FETC.2FRESOLV.CONF)). Vamos nos concentrar aqui nos dois modos mais relevantes.

1.  O modo no qual *systemd-resolved* é um cliente do `/etc/resolv.conf`. Esse modo preserva o `/etc/resolv.conf` e é **compatível** com os procedimentos descritos nesta página.
2.  Os modos de operação **recomendados** do *systemd-resolved*: o arquivo stub como indicado abaixo ambos no `127.0.0.53` local como apenas nos servidores DNS e uma lista de domínios de pesquisa.

 `/run/systemd/resolve/stub-resolv.conf` 
```
nameserver 127.0.0.53
search lan

```

Os usuários do serviço são aconselhados a redirecionar o arquivo `/etc/resolv.conf` para o arquivo local do resolvedor DNS do stub `/run/systemd/resolve/stub-resolv.conf` gerenciado por *systemd-resolved*. Isso propaga a configuração gerenciada do systemd para todos os clientes. Isso pode ser feito excluindo ou renomeando o `/etc/resolv.conf` existente e substituindo-o por um link simbólico para o stub do systemd:

```
# ln -s /run/systemd/resolve/stub-resolv.conf /etc/resolv.conf

```

Neste modo, os servidores DNS são fornecidos no arquivo [resolved.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/resolved.conf.5):

 `/etc/systemd/resolved.conf` 
```
[Resolve]
**DNS=91.239.100.100 89.233.43.71**
...
```

Para verificar o DNS realmente usado pelo *systemd-resolved*, o comando a ser usado é:

```
$ systemd-resolve --status

```

**Dica:**

*   Para entender o contexto em torno das opções de DNS e switches, é possível ativar informações detalhadas de depuração para *systemd-resolved*, conforme descrito em [Systemd (Português)#Diagnosticar um serviço](/index.php/Systemd_(Portugu%C3%AAs)#Diagnosticar_um_servi.C3.A7o "Systemd (Português)").
*   O modo de operação do *systemd-resolved* é detectado automaticamente, dependendo se o `/etc/resolv.conf` é um link simbólico para o arquivo local do resolvedor de DNS stub ou contém nomes de servidor.

## Desempenho

O [#Resolvedor do glibc](#Resolvedor_do_glibc) não armazena em cache as consultas. Se você quiser que o cache local use [#Systemd-resolved](#Systemd-resolved) ou configure um [servidor DNS](/index.php/Servidor_DNS "Servidor DNS") de cache local e use `127.0.0.1`.

**Dica:** Os [#Utilitários de lookup](#Utilit.C3.A1rios_de_lookup) *dig* e *drill* relatam o tempo de consulta.

Provedores de serviços de Internet geralmente fornecem servidores DNS em funcionamento. Um roteador também pode adicionar um servidor DNS extra, caso tenha seu próprio servidor de cache. A alternância entre servidores DNS é transparente para usuários do Windows, porque se um servidor DNS estiver lento ou não funcionar, ele mudará imediatamente para um servidor melhor. No entanto, o Linux geralmente leva mais tempo para o tempo limite, o que poderia causar atrasos.

## Privacidade

A maioria dos servidores DNS mantém um registro de endereços IP e sites visitados em uma base mais ou menos temporária. Os dados coletados podem ser usados para realizar vários estudos estatísticos. Informações de identificação pessoal têm valor e também podem ser alugadas ou vendidas a terceiros. O artigo [Serviços DNS alternativos](/index.php/Alternative_DNS_services "Alternative DNS services") fornece uma lista de serviços populares, verifique sua política de privacidade para obter informações sobre como os dados do usuário são manipulados.

## Utilitários de lookup

Para consultar servidores DNS específicos e registros DNS/[DNSSEC](/index.php/DNSSEC "DNSSEC"), você pode usar utilitários de pesquisa de DNS dedicados. Essas ferramentas implementam o próprio DNS e não usam [NSS](#Name_Service_Switch).

*   [bind-tools](https://www.archlinux.org/packages/?name=bind-tools) fornece [dig(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/dig.1), [host(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/host.1), [nslookup(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nslookup.1) e várias ferramentas `dnssec-`.
*   [ldns](https://www.archlinux.org/packages/?name=ldns) fornece [drill(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/drill.1), que é similar ao *dig*

Por exemplo, para consultar um servidor de nomes específico com drill por registros TXT de um domínio:

```
$ drill @*servidor-de-nome* TXT *domínio*

```

Se você não especificar um servidor DNS *dig* e *drill*, use os servidores de nome definidos em `/etc/resolv.conf`.

## Veja também

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/x-087-2-resolv.html)
*   [Debian Handbook](https://www.debian.org/doc/manuals/debian-handbook/sect.hostname-name-service.en.html#sect.name-resolution)