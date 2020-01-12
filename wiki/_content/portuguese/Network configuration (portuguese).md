**Status de tradução:** Esse artigo é uma tradução de [Network configuration](/index.php/Network_configuration "Network configuration"). Data da última tradução: 2019-11-06\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Network_configuration&diff=0&oldid=585917) na versão em inglês.

Artigos relacionados

*   [Depuração de rede](/index.php/Network_Debugging "Network Debugging")
*   [Firewalls](/index.php/Firewalls "Firewalls")
*   [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")
*   [Compartilhamento de internet](/index.php/Internet_sharing "Internet sharing")
*   [Roteador](/index.php/Router "Router")

Esse artigo descreve como configurar conexões de rede na [camada 3 do Modelo OSI](https://en.wikipedia.org/wiki/pt:Camada_de_rede "wikipedia:pt:Camada de rede") e acima. Especificidades para cada meio de transporte são tratadas nas subpáginas [/Ethernet](/index.php/Network_configuration_(Portugu%C3%AAs)/Ethernet "Network configuration (Português)/Ethernet") e [/Sem fio](/index.php/Network_configuration_(Portugu%C3%AAs)/Sem_fio "Network configuration (Português)/Sem fio").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Verificar a conexão](#Verificar_a_conexão)
    *   [1.1 Ping](#Ping)
*   [2 Gerenciamento de rede](#Gerenciamento_de_rede)
    *   [2.1 net-tools](#net-tools)
    *   [2.2 iproute2](#iproute2)
    *   [2.3 Interfaces de rede](#Interfaces_de_rede)
        *   [2.3.1 Listando interfaces de rede](#Listando_interfaces_de_rede)
        *   [2.3.2 Habilitando e desabilitando interfaces de rede](#Habilitando_e_desabilitando_interfaces_de_rede)
    *   [2.4 Endereço IP estático](#Endereço_IP_estático)
    *   [2.5 Endereços IP](#Endereços_IP)
    *   [2.6 Tabela de roteamento](#Tabela_de_roteamento)
    *   [2.7 DHCP](#DHCP)
    *   [2.8 Gerenciadores de rede](#Gerenciadores_de_rede)
*   [3 Configurando um hostname](#Configurando_um_hostname)
    *   [3.1 Resolução de hostname local](#Resolução_de_hostname_local)
    *   [3.2 Resolução de hostname de rede local](#Resolução_de_hostname_de_rede_local)
*   [4 Dicas e truques](#Dicas_e_truques)
    *   [4.1 Alterando o nome da interface](#Alterando_o_nome_da_interface)
    *   [4.2 Revertendo para nomes tradicionais de interfaces](#Revertendo_para_nomes_tradicionais_de_interfaces)
    *   [4.3 Definindo o MTU do dispositivo e o tamanho da fila](#Definindo_o_MTU_do_dispositivo_e_o_tamanho_da_fila)
    *   [4.4 Bonding e LAG(agregação de LINK)](#Bonding_e_LAG(agregação_de_LINK))
    *   [4.5 Aliasing de endereço IP](#Aliasing_de_endereço_IP)
        *   [4.5.1 Exemplo](#Exemplo)
    *   [4.6 Modo promíscuo](#Modo_promíscuo)
    *   [4.7 Investigar soquetes](#Investigar_soquetes)
*   [5 Solução de problemas](#Solução_de_problemas)
    *   [5.1 O problema de escala de janela TCP](#O_problema_de_escala_de_janela_TCP)
        *   [5.1.1 Como diagnosticar o problema](#Como_diagnosticar_o_problema)
        *   [5.1.2 Formas de corrigi-lo](#Formas_de_corrigi-lo)
            *   [5.1.2.1 Ruim](#Ruim)
            *   [5.1.2.2 Bom](#Bom)
            *   [5.1.2.3 Melhor](#Melhor)
        *   [5.1.3 Mais sobre isso](#Mais_sobre_isso)
*   [6 Veja também](#Veja_também)

## Verificar a conexão

Para solucionar problemas de uma conexão de rede, siga as seguintes condições e assegure-se de atendê-las:

1.  Suas interfaces de rede estão listadas e habilitadas. Do contrário, confira o driver de dispositivo – veja [/Ethernet#Driver de dispositivo](/index.php/Network_configuration_(Portugu%C3%AAs)/Ethernet#Driver_de_dispositivo "Network configuration (Português)/Ethernet") ou [/Sem fio#Driver de dispositivo](/index.php/Network_configuration_(Portugu%C3%AAs)/Sem_fio#Driver_de_dispositivo "Network configuration (Português)/Sem fio").
2.  Você está conectado à rede. O cabo está conectado ou você está [conectado com a rede sem fio](/index.php/Network_configuration_(Portugu%C3%AAs)/Sem_fio "Network configuration (Português)/Sem fio").
3.  Sua interface de rede tem um [endereço IP](#Endereços_IP).
4.  Sua [tabela de roteamento](#Tabela_de_roteamento) está configurada corretamente.
5.  Você pode [pingar](#Ping) um endereço IP local (por exemplo, seu gateway padrão).
6.  Você pode [pingar](#Ping) um endereço IP público (por exemplo, `8.8.8.8`), que é um servidor DNS do Google e é um endereço conveniente para se usar em um teste.
7.  [Verifique se você consegue resolver nomes de domínio](/index.php/Verifique_se_voc%C3%AA_consegue_resolver_nomes_de_dom%C3%ADnio "Verifique se você consegue resolver nomes de domínio") (por exemplo, `archlinux.org`).

### Ping

[ping](https://en.wikipedia.org/wiki/pt:Ping "wikipedia:pt:Ping") é usado para testar se você consegue alcançar um host.

 `$ ping www.example.com` 
```
PING www.example.com (93.184.216.34): 56(84) data bytes
64 bytes from 93.184.216.34: icmp_seq=0 ttl=56 time=11.632 ms
64 bytes from 93.184.216.34: icmp_seq=1 ttl=56 time=11.726 ms
64 bytes from 93.184.216.34: icmp_seq=2 ttl=56 time=10.683 ms
...
```

Para cada resposta que você recebe, o utilitário ping imprimirá uma linha como a acima. Para mais informações, consulte o manual [ping(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8). Observe que os computadores podem ser configurados para não responder às solicitações de eco ICMP. [[1]](https://unix.stackexchange.com/questions/412446/how-to-disable-ping-response-icmp-echo-in-linux-all-the-time)

Se você não receber nenhuma resposta, isso pode estar relacionado a seu gateway padrão ou a seu provedor de internet. Você pode executar um [traceroute](/index.php/Traceroute_(Portugu%C3%AAs) "Traceroute (Português)") para diagnosticar ainda mais a rota para o host.

**Nota:** Se você receber um erro como `ping: icmp open socket: Operation not permitted` ao executar *ping*, tente reinstalar o pacote [iputils](https://www.archlinux.org/packages/?name=iputils).

## Gerenciamento de rede

Para configurar uma conexão de rede, siga as etapas abaixo:

1.  Certifique-se que sua [interface de rede](#Interfaces_de_rede) está listada e habilitada.
2.  Conecte à rede. Conecte o cabo de rede ou [conecte à rede sem fio](/index.php/Network_configuration_(Portugu%C3%AAs)/Sem_fio "Network configuration (Português)/Sem fio").
3.  Configure sua conexão de rede:
    *   [endereço IP estático](#Endereço_IP_estático)
    *   endereço IP dinâmico: use [DHCP](#DHCP)

**Nota:** A imagem de instalação habilita [dhcpcd](/index.php/Dhcpcd "Dhcpcd") (`dhcpcd@*interface*.service`) para [dispositivos de rede cabeada](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) na inicialização.

### net-tools

Arch Linux tornou [net-tools](https://www.archlinux.org/packages/?name=net-tools) obsoleto em favor do [iproute2](https://www.archlinux.org/packages/?name=iproute2).[[2]](https://www.archlinux-br.org/noticias/155/)

| Comando obsoleto | Comandos substitutos |
| arp | ip neighbor |
| [ifconfig](https://en.wikipedia.org/wiki/pt:ifconfig "wikipedia:pt:ifconfig") | ip address, ip link |
| netstat | [ss](#Investigar_soquetes) |
| route | ip route |

Para um resumo mais completo, veja [essa publicação de blogue](https://dougvitale.wordpress.com/2011/12/21/deprecated-linux-networking-commands-and-their-replacements/).

### iproute2

[iproute2](https://en.wikipedia.org/wiki/iproute2 "wikipedia:iproute2") é uma dependência do [metapacote](/index.php/Metapacote "Metapacote") [base](https://www.archlinux.org/packages/?name=base) e fornece a interface de linha de comando [ip(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip.8), usado para gerenciar [interfaces de rede](#Interfaces_de_rede), [endereços IP](#Endereços_IP) e a [tabela de roteamento](#Tabela_de_roteamento). Esteja ciente de que a configuração feita usando `ip` será perdida após uma reinicialização. Para uma configuração persistente, você pode usar um [gerenciador de rede](/index.php/Gerenciador_de_rede "Gerenciador de rede") ou automatizar comandos *ip* usando scripts e [units de systemd](/index.php/Systemd_(Portugu%C3%AAs)#Escrevendo_arquivos_unit "Systemd (Português)"). Observe também que os comandos `ip` geralmente podem ser abreviados, para maior clareza eles são descritos neste artigo.

### Interfaces de rede

Por padrão, o [udev](/index.php/Udev "Udev") atribui nomes para suas interfaces de rede usando [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames), que prefixam nomes de interfaces com `en` (cabeada/[Ethernet](https://en.wikipedia.org/wiki/pt:Ethernet "wikipedia:pt:Ethernet")), `wl` (sem fio/wireless/WLAN) ou `ww` ([WWAN](https://en.wikipedia.org/wiki/pt:Rede_de_longa_dist%C3%A2ncia_sem_fio "wikipedia:pt:Rede de longa distância sem fio")).

**Dica:** Para alterar os nomes de dispositivos, veja [#Alterando o nome da interface](#Alterando_o_nome_da_interface) e [#Revertendo para nomes tradicionais de interfaces](#Revertendo_para_nomes_tradicionais_de_interfaces).

#### Listando interfaces de rede

Ambos nomes de interfaces com e sem fio podem ser descobertos por meio de `ls /sys/class/net` ou `ip link`. Note que `lo` é o [dispositivo *loop* ou de laço](https://en.wikipedia.org/wiki/pt:Loop_device "wikipedia:pt:Loop device") e não é usado para fazer conexões de rede.

Nomes de dispositivos sem fio também podem ser obtidos usando `iw dev`. Veja também [/Sem fio#Obter o nome da interface](/index.php/Network_configuration_(Portugu%C3%AAs)/Sem_fio#Obter_o_nome_da_interface "Network configuration (Português)/Sem fio").

Se sua interface de rede não estiver listada, certifique-se que seu [driver de dispositivo](#Driver_de_dispositivo) foi carregado com sucesso.

#### Habilitando e desabilitando interfaces de rede

Interfaces de rede podem ser habilitadas/desabilitadas usando `ip link set *interface* up|down`. Veja [ip-link(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-link.8).

Para verificar o status da interface `eth0`:

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state DOWN mode DEFAULT qlen 1000
...

```

O `UP` em `<BROADCAST,MULTICAST,UP,LOWER_UP>` é o que indica a interface está ativa, e não o `state DOWN` posterior.

**Nota:** Se sua rota padrão é por meio da interface `eth0`, desabilitá-la também vai remover a rota e reativá-la não vai restabelecer automaticamente a rota padrão. Veja [#Tabela de roteamento](#Tabela_de_roteamento) para restabelecê-la.

### Endereço IP estático

Um endereço IP estático pode ser configurado com a maioria dos [gerenciadores de rede](#Gerenciadores_de_rede) padrão e também [dhcpcd](/index.php/Dhcpcd "Dhcpcd").

Para configurar manualmente um endereço IP estático, adicione um endereço IP como descrito em [#Endereços IP](#Endereços_IP), configure sua [tabela de roteamento](#Tabela_de_roteamento) e [configure seus servidores DNS](/index.php/Resolu%C3%A7%C3%A3o_de_nome_de_dom%C3%ADnio "Resolução de nome de domínio").

### Endereços IP

[Endereços IP](https://en.wikipedia.org/wiki/pt:Endere%C3%A7o_IP "wikipedia:pt:Endereço IP") são gerenciados usando [ip-address(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-address.8).

Liste endereços IP:

```
$ ip address show

```

Adicione um endereço IP a uma interface:

```
# ip address add *endereço/tam_prefixo* broadcast + dev *interface*

```

	Note que:

*   o endereço é dado em [notação CIDR](https://en.wikipedia.org/wiki/pt:Classless_Inter-Domain_Routing#Nota.C3.A7.C3.A3o_standard "wikipedia:pt:Classless Inter-Domain Routing") para também fornecer uma [máscara de sub-rede](https://en.wikipedia.org/wiki/pt:Sub-rede "wikipedia:pt:Sub-rede")
*   `+` é um símbolo especial que faz o `ip` derivar o [endereço broadcast](https://en.wikipedia.org/wiki/pt:Endere%C3%A7o_de_broadcast "wikipedia:pt:Endereço de broadcast") do endereço IP e a máscara de sub-rede

**Nota:** Certifique-se que endereços IP atribuídos manualmente não conflitem com os atribuídos por DHCP.

Exclui um endereço IP de uma interface:

```
$ ip address del *endereço/tam_prefixo* dev *interface*

```

Exclui todos os endereços correspondendo a um critério, por exemplo, de uma interface específica:

```
$ ip address flush dev *interface*

```

**Dica:** Endereços IP podem ser calculados com [ipcalc](http://jodies.de/ipcalc) ([ipcalc](https://www.archlinux.org/packages/?name=ipcalc)).

### Tabela de roteamento

A [tabela de roteamento](https://en.wikipedia.org/wiki/Routing_table "wikipedia:Routing table") é usada para determinar se você pode alcançar um endereço IP diretamente ou qual gateway (roteador) você deve usar. Se nenhuma rota corresponde ao endereço IP, o [gateway padrão](https://en.wikipedia.org/wiki/Default_gateway "wikipedia:Default gateway") é usado.

A tabela de roteamento é gerenciada usando [ip-route(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip-route.8).

*PREFIXO* é uma notação CIDR ou `default` para o gateway padrão.

Lista rotas IPv4:

```
$ ip route show

```

Lista rotas IPv6:

```
$ ip -6 route

```

Adiciona uma rota:

```
# ip route add *PREFIXO* via *endereço* dev *interface*

```

Exclui uma rota:

```
# ip route del *PREFIXO* via *endereço* dev *interface*

```

### DHCP

Um servidor [Dynamic Host Configuration Protocol](https://en.wikipedia.org/wiki/pt:Dynamic_Host_Configuration_Protocol "wikipedia:pt:Dynamic Host Configuration Protocol") (DHCP) fornece aos clientes um endereço IP dinâmico, a máscara de sub-rede, o endereço IP do gateway padrão e, opcionalmente, também servidores de nome DNS.

**Nota:** Você não deve executar dois clientes DHCP simultaneamente.

Para usar DHCP, você precisa de um servidor DHCP em sua rede e um cliente DHCP:

| Cliente | Pacote | [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)") | Nota | Units de systemd |
| [dhcpcd](/index.php/Dhcpcd "Dhcpcd") | [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) | Sim | DHCP, DHCPv6, ZeroConf, IP estático | `dhcpcd.service`, `dhcpcd@*interface*.service` |
| [ISC dhclient](https://www.isc.org/downloads/dhcp/) | [dhclient](https://www.archlinux.org/packages/?name=dhclient) | Sim | DHCP, DHCPv6, BOOTP, IP estático | `dhclient@*interface*.service` |

Note que em vez de usar diretamente um cliente DHCP, você também pode usar um [gerenciador de rede](#Gerenciadores_de_rede).

**Dica:** Você pode verificar se um servidor DHCP estiver funcionando com [dhcping](https://www.archlinux.org/packages/?name=dhcping).

### Gerenciadores de rede

Um gerenciador de rede permite que você gerencie configurações de conexão de rede nos chamados peris de rede para facilitar a troca de redes.

**Nota:** Existem muitas soluções para escolher, mas lembre-se de que todas elas são mutuamente exclusivas; você não deve executar dois daemons simultaneamente.

| Gerenciador
de rede | GUI | [Archiso](/index.php/Archiso_(Portugu%C3%AAs) "Archiso (Português)") [[3]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) | Ferramentas CLI | Suporte a [PPP](https://en.wikipedia.org/wiki/pt:Point-to-Point_Protocol "wikipedia:pt:Point-to-Point Protocol") (ex., Modem 3G) | [Cliente DHCP](#DHCP) | Units de systemd |
| [ConnMan](/index.php/ConnMan "ConnMan") | 8 não oficiais | Não | [connmanctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/connmanctl.1) | Sim ((com [ofono](https://aur.archlinux.org/packages/ofono/)) | interno | `connman.service` |
| [netctl](/index.php/Netctl "Netctl") | 2 não oficiais | Sim | [netctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/netctl.1), wifi-menu | Sim | [dhcpcd](/index.php/Dhcpcd "Dhcpcd") ou [dhclient](https://www.archlinux.org/packages/?name=dhclient) | `netctl-ifplugd@*interface*.service`, `netctl-auto@*interface*.service` |
| [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") | Sim | Não | [nmcli(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmcli.1), [nmtui(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nmtui.1) | Sim | interno, [dhcpcd](/index.php/Dhcpcd "Dhcpcd") ou [dhclient](https://www.archlinux.org/packages/?name=dhclient) | `NetworkManager.service` |
| [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") | Não | Sim ([base](https://www.archlinux.org/packages/?name=base)) | [networkctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/networkctl.1) | [Não](https://github.com/systemd/systemd/issues/481) | interno | `systemd-networkd.service`, `systemd-resolved.service` |
| [Wicd](/index.php/Wicd "Wicd") | Sim | Não | [wicd-cli(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-cli.8), [wicd-curses(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/wicd-curses.8) | Não | [dhcpcd](/index.php/Dhcpcd "Dhcpcd") | `wicd.service` |

Há também o [Wifi Radar](/index.php/Wifi_Radar_(Portugu%C3%AAs) "Wifi Radar (Português)"), um aplicativo GUI que gerencia redes Wifi por meio do [wireless_tools](https://www.archlinux.org/packages/?name=wireless_tools), porém ele não gerencia conexões cabeadas.

Veja também [List of applications#Network managers](/index.php/List_of_applications#Network_managers "List of applications").

## Configurando um hostname

Um [hostname](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname"), ou "nome de máquina", é um nome único criado para identificar uma máquina em uma rede, configurada em `/etc/hostname` — veja [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) e [hostname(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.7) para detalhes. O arquivo pode conter o nome de domínio do sistema, se houver. Para configurar o hostname, [edite](/index.php/Edi%C3%A7%C3%A3o_de_texto "Edição de texto") `/etc/hostname` para incluir uma única linha com `*meuhostname*`:

 `/etc/hostname` 
```
*meuhostname*

```

**Dica:** Para um conselho quanto ao hostname, veja [RFC 1178](https://tools.ietf.org/html/rfc1178).

Alternativamente, usando [hostnamectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostnamectl.1):

```
# hostnamectl set-hostname *meuhostname*

```

Para definir temporariamente o hostname (até reiniciar), use [hostname(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.1) do [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
# hostname *meuhostname*

```

Para configurar um hostname "bonito" e outros metadados de máquina, veja [machine-info(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/machine-info.5).

### Resolução de hostname local

O módulo [Name Service Switch](/index.php/Name_Service_Switch_(Portugu%C3%AAs) "Name Service Switch (Português)") (NSS) `myhostname` do [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") fornece resolução de hostname local sem ter que editar `/etc/hosts` ([hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)). Ele está habilitado por padrão.

Alguns clientes, porém, podem depender de `/etc/hosts`, veja [[4]](https://lists.debian.org/debian-devel/2013/07/msg00809.html) [[5]](https://bugzilla.mozilla.org/show_bug.cgi?id=87717#c55) por exemplos.

Para configurar o arquivo hosts, adicione as seguintes linhas ao `/etc/hosts`:

```
127.0.0.1        localhost
::1              localhost
127.0.1.1        *meuhostname*.localdomain        *meuhostname*

```

**Nota:** A ordem de hostnames/aliases que seguem o endereço IP no `/etc/hosts` é relevante. A primeira string é considerada o hostname canônico e pode ser adicionada a domínios pais, sendo os componentes de domínio separados por um ponto (p. ex., `.dominiolocal` acima). Todas as strings a seguir na mesma linha são considerados aliases. Veja [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5) para mais informações.

Como um resultado, o sistema resolve ambas entradas:

 `$ getent hosts` 
```
127.0.0.1       localhost
127.0.0.1       localhost
127.0.1.1       *meuhostname*.localdomain *meuhostname*

```

Para um sistema com um endereço IP permanente, esse endereço IP permanente deve ser usado em vez de `127.0.1.1`.

### Resolução de hostname de rede local

Para tornar sua máquina acessível em sua LAN por seu hostname, você pode:

*   editar o arquivo `/etc/hosts` para todo dispositivio em sua LAN, veja [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5)
*   configurar um [servidor DNS](/index.php/Servidor_DNS "Servidor DNS") para resolver seu hostname e faça com que os dispositivos LAN o usem (ex., por [#DHCP](#DHCP))
*   ou a forma fácil: use um serviço [Zero-configuration networking](https://en.wikipedia.org/wiki/pt:Zeroconf "wikipedia:pt:Zeroconf"):
    *   Resolução de nomes de host através do serviço [NetBIOS](https://en.wikipedia.org/wiki/pt:NetBIOS#Servi.C3.A7o_de_nomes "wikipedia:pt:NetBIOS") da Microsoft. Fornecido pelo [Samba](/index.php/Samba "Samba") no Linux. Ele precisa da instalação do [samba](https://www.archlinux.org/packages/?name=samba) e habilitação do serviço `nmb.service`. Computadores usando Windows, macOS ou Linux com `nmb` ativo, serão capazes de localizar sua máquina.
    *   Resolução de nomes de host via [mDNS](https://en.wikipedia.org/wiki/pt:Multicast_DNS "wikipedia:pt:Multicast DNS"). Fornecido por `nss_mdns` com [Avahi](/index.php/Avahi "Avahi") (consulte [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") para detalhes de configuração) ou [systemd-resolved](/index.php/Systemd-resolved "Systemd-resolved"). Computadores usando macOS, ou Linux com o Avahi ou o systemd-running em execução, poderão localizar sua máquina. O Windows não possui um cliente ou daemon mDNS integrado.

## Dicas e truques

### Alterando o nome da interface

**Nota:** Ao alterar o esquema de nomes de interface, não se esqueça de atualizar todos os arquivos de configuração relacionados a rede e arquivos personalizados de unit de systemd para refletir a alteração.

Você pode alterar o nome de um dispositivo definindo o nome em uma regra de udev. Exemplo:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"
```

Essas regras serão aplicadas automaticamente na inicialização.

Alguns detalhes devem ser ressaltados:

*   Para obter o endereço MAC de cada placa de rede, utilize o comando: `cat /sys/class/net/*nome_dispositivo*/address`
*   Certifique-se de usar valores hexadecimais minúsculos em suas regras de udev. Ele não gosta de letras maiúsculas.

Se a placa de rede possui um MAC dinâmico, você pode usar `DEVPATH`, por exemplo:

 `/etc/udev/rules.d/10-network.rules` 
```
SUBSYSTEM=="net", DEVPATH=="/devices/platform/wemac.*", NAME="int"
SUBSYSTEM=="net", DEVPATH=="/devices/pci*/*1c.0/*/net/*", NAME="en"
```

Para obter o `DEVPATH` de todos os dispositivos atualmente conecados, veja para onde os links simbólicos em `/sys/class/net/` levam. Por exemplo:

 `file /sys/class/net/*` 
```
/sys/class/net/enp0s20f0u4u1: symbolic link to ../../devices/pci0000:00/0000:00:14.0/usb2/2-4/2-4.1/2-4.1:1.0/net/enp0s20f0u4u1
/sys/class/net/enp0s31f6:     symbolic link to ../../devices/pci0000:00/0000:00:1f.6/net/enp0s31f6
/sys/class/net/lo:            symbolic link to ../../devices/virtual/net/lo
/sys/class/net/wlp4s0:        symbolic link to ../../devices/pci0000:00/0000:00:1c.6/0000:04:00.0/net/wlp4s0

```

O caminho do dispositivo deve corresponder ao nome do dispositivo novo e antigo, uma vez que a regra pode ser executada mais de uma vez na inicialização. Por exemplo, na segunda regra, `"/devices/pci*/*1c.0/*/net/enp*"` seria errado, uma vez que irá parar de corresponder depois que o nome for alterado para `en`. Somente a regra padrão do sistema será chamada na segunda vez, fazendo com que o nome seja alterado de volta para, por exemplo, `enp1s0`.

Se você estiver usando um dispositivo de rede USB (por exemplo, tethering de telefone Android) que tenha um endereço MAC dinâmico e deseje usar diferentes portas USB, poderá usar uma regra que corresponda, dependendo do fornecedor e do ID do produto:

 `/etc/udev/rules.d/10-network.rules`  `SUBSYSTEM=="net", ACTION=="add", ATTRS{idVendor}=="12ab", ATTRS{idProduct}=="3cd4", NAME="net2"` 

Para [testar](/index.php/Udev#Testing_rules_before_loading "Udev") suas regras, elas podem ser acionadas diretamente do espaço de usuário, por exemplo, com `udevadm --debug test /sys/class/net/*`. Lembre-se de primeiro retirar a interface que você está tentando renomear (ex. `ip link set enp1s0 down`).

**Nota:** Ao escolher os nomes estáticos **deve-se evitar o uso de nomes no formato de "eth*X*" e "wlan*X*"**, pois eles podem levar a codiçẽos de corrida entre o kernel e udev durante a inicialização. Em vez disso, é melhor usar nomes de interface que não são usados pelo kernel como padrão, ex.: `net0`, `net1`, `wifi0`, `wifi1`. Para detalhes adicionais, por favor veja a documentação do [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames).

### Revertendo para nomes tradicionais de interfaces

Se você preferir manter os nomes de interface tradicionais, como eth0, [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) podem ser desabilitados mascarando a regra de rule:

```
# ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

```

Alternativamente, adicione `net.ifnames=0` aos [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel").

### Definindo o MTU do dispositivo e o tamanho da fila

Você pode alterar o [MTU](https://en.wikipedia.org/wiki/pt:MTU "wikipedia:pt:MTU") do dispositivo e o tamanho da fila ao definir manualmente com uma regra de udev. Por exemplo:

 `/etc/udev/rules.d/10-network.rules`  `ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1500", ATTR{tx_queue_len}="2000"` 
**Nota:**

*   `mtu`: Para PPPoE, o MTU não deve ser maior que 1492\. Você também pode definir o MTU via [systemd.netdev(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.netdev.5).
*   `tx_queue_len`: Valores pequenos para dispositivos menores com uma latência maior, como modens e ISDN. Valor alto é recomendado para servidor conectado por meio conexões de Internet de alta velocidade que realiza grandes transferências de dados.

### Bonding e LAG(agregação de LINK)

Veja [netctl#Bonding](/index.php/Netctl#Bonding "Netctl") ou [Wireless bonding](/index.php/Wireless_bonding "Wireless bonding").

### Aliasing de endereço IP

*IP aliasing* é o processo de adicionar mais de um endereço IP para uma interface de rede. Como isso, um nó em uma rede pode ter múltiplas conexões com uma rede, cada uma servindo um propósito diferente. Usos típicos são hospedagem virtual de servidores Web e FTP ou reorganização de servidores sem ter que atualizar qualquer outras máquinas (isso é especialmente útil para servidores de nome).

#### Exemplo

Para definir manualmente um alias, para algumas interfaces de rede, use [iproute2](https://www.archlinux.org/packages/?name=iproute2) para executar

```
# ip addr add 192.168.2.101/24 dev eth0 label eth0:1

```

Para remover um dado alias, execute

```
# ip addr del 192.168.2.101/24 dev eth0:1

```

Os pacotes de rede destinados para uma sub-rede vão usar o alias primário por padrão. Se o IP de destino está dentro de uma sub-rede de um alias secundário, então o IP fonte está definido respectivamente. Considere o caso em que há mais de uma interface de rede, as rotas padrão podem ser listadas com `ip route`.

### Modo promíscuo

Ativar [modo promíscuo](https://en.wikipedia.org/wiki/pt:Modo_prom%C3%ADscuo "wikipedia:pt:Modo promíscuo") fará com que uma interface de rede (sem fio) encaminhe todo o tráfego que receber para o sistema operacional para processamento posterior. Isso é contrário ao "modo normal" onde uma interface de rede irá descartar quadros que não pretende receber. É usado com mais frequência para solução de problemas avançados de rede e [análise de pacotes (sniffing)](https://en.wikipedia.org/wiki/pt:Analisador_de_pacotes "wikipedia:pt:Analisador de pacotes").

 `/etc/systemd/system/promiscuous@.service` 
```
[Unit]
Description=Set %i interface in promiscuous mode
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/ip link set dev %i promisc on
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target

```

Se você deseja habilitar o modo promíscuo na interface `eth0`, execute [*enable*](/index.php/Habilite "Habilite") `promiscuous@eth0.service`.

### Investigar soquetes

*ss* é um utilitário para investigar portas de rede e é parte do pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2). Ele tem uma funcionalidade similar ao utilitário [obsoleto](https://www.archlinux.org/news/deprecation-of-net-tools/) netstat.

Uso comum inclui:

Exibe todos os TCP Sockets com nomes de serviços:

```
$ ss -at

```

Exibe todos os TCP Sockets com números de portas:

```
$ ss -atn

```

Exibe todos os UDP Sockets:

```
$ ss -au

```

Para mais informações, veja [ss(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ss.8).

## Solução de problemas

### O problema de escala de janela TCP

Os pacotes TCP contêm um valor "janela" em seus cabeçalhos indicando quantos dados o outro host pode enviar em troca. Esse valor é representado com apenas 16 bits, então o tamanho da janela é no máximo 64Kb. Os pacotes TCP são armazenados em cache por um tempo (eles precisam ser reordenados) e, como a memória é (ou costumava ser) limitada, um host poderia ficar sem isso.

Em 1992, à medida que mais e mais memória ficava disponível, [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html) foi escrito para melhorar a situação: escala de janela. O valor "janela", fornecido em todos os pacotes, será modificado por um Fator de Escala definido uma vez, no início da conexão. Esse Fator de Escala de 8 bits permite que a Janela seja até 32 vezes maior do que os 64Kb iniciais.

Parece que alguns roteadores quebrados e firewalls na Internet estão reescrevendo o Fator de Escala para 0, o que causa mal-entendidos entre hosts. O kernel do Linux 2.6.17 introduziu um novo esquema de cálculo gerando maiores fatores de escala, tornando visíveis as consequências dos roteadores quebrados e dos firewalls.

A conexão resultante é no máximo muito lenta ou quebrada.

#### Como diagnosticar o problema

Antes de mais, vamos deixar claro: esse problema é estranho. Em alguns casos, você não poderá usar conexões TCP (HTTP, FTP, ...) e em outros, você poderá se comunicar com alguns hosts (muito poucos).

Quando você tiver esse problema, a saída do `dmesg` está normal, os logs estão limpos e `ip addr` informará o estado como normal... e, na verdade, tudo parece normal.

Se você não pode navegar em nenhum site, mas você pode fazer ping em alguns hosts aleatórios, você tem grande chances de estar enfrentando esse problema: o ping usa o ICMP e não é afetado pelos problemas do TCP.

Você pode tentar usar [Wireshark](/index.php/Wireshark_(Portugu%C3%AAs) "Wireshark (Português)"). Você pode ver comunicações UDP e ICMP bem-sucedidas, mas comunicações TCP mal sucedidas (somente para hosts estrangeiros).

#### Formas de corrigi-lo

##### Ruim

Para corrigi-lo de forma incorreta, você pode alterar o valor `tcp_rmem`, no qual o cálculo do Fator de Escala se baseia. Embora ele funcione para a maioria dos hosts, não é garantido, especialmente para os mais distantes.

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

##### Bom

Simplesmente desative Escala de Janela. Como a Escala de Janela é um bom recurso TCP, pode ser desconfortável desativá-lo, especialmente se você não conseguir corrigir o roteador quebrado. Há várias maneiras de desativar Escala de Janela, e parece que a maneira mais segura (que funcionará com a maioria dos kernels) é adicionar a seguinte linha a `/etc/sysctl.d/99-disable_window_scaling.conf` (veja também [sysctl](/index.php/Sysctl "Sysctl")):

```
net.ipv4.tcp_window_scaling = 0

```

##### Melhor

Esse problema é causado por roteadores/firewalls quebrados, então vamos mudá-los. Alguns usuários relataram que o roteador quebrado era o próprio roteador DSL.

#### Mais sobre isso

Essa seção é baseada nos artigos, em inglês, do LWN [Escala de janela e roteadores quebrados](http://lwn.net/Articles/92727/) e do Kernel Trap [Escala de Janela na Internet](https://web.archive.org/web/20120426135627/http://kerneltrap.org:80/node/6723) (arquivado).

Há também vários tópicos relevantes no LKML.

## Veja também

*   [Linux Network Administrators Guide](https://www.tldp.org/LDP/nag2/index.html)
*   [Referência do Debian: Configuração de Rede](https://www.debian.org/doc/manuals/debian-reference/ch05.en.html)
*   [RHEL7: Guia de Rede](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/)
*   [Linux Home Networking](http://www.linuxhomenetworking.com/wiki/)
*   [Monitorando e ajustando o Linux a Pilha de Conectividade: Recebendo dados](https://blog.packagecloud.io/eng/2016/06/22/monitoring-tuning-linux-networking-stack-receiving-data/)
*   [Monitorando e ajustando o Linux a Pilha de Conectividade: Enviando dados](https://blog.packagecloud.io/eng/2017/02/06/monitoring-tuning-linux-networking-stack-sending-data/)
*   [Rastreamento de uma viagem de pacotes usando tracepoints, perf e eBPF](http://blog.yadutaf.fr/2017/07/28/tracing-a-packet-journey-using-linux-tracepoints-perf-ebpf/)