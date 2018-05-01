Artigos relacionados

*   [Jumbo frames](/index.php/Jumbo_frames "Jumbo frames")
*   [Firewalls](/index.php/Firewalls "Firewalls")
*   [Configuração de rede sem fio](/index.php/Configura%C3%A7%C3%A3o_de_rede_sem_fio "Configuração de rede sem fio")
*   [Network bridge](/index.php/Network_bridge "Network bridge")
*   [List of applications#Network Managers](/index.php/List_of_applications#Network_Managers "List of applications")
*   [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing")
*   [Internet sharing](/index.php/Internet_sharing "Internet sharing")
*   [Router](/index.php/Router "Router")
*   [Network Debugging](/index.php/Network_Debugging "Network Debugging")

Esta página explica como configurar uma conexão cabeada. Se você deseja configurar uma rede wireless/sem fio veja a página [Configuração de rede sem fio](/index.php/Configura%C3%A7%C3%A3o_de_rede_sem_fio "Configuração de rede sem fio").

## Contents

*   [1 Depuração de rede](#Depura.C3.A7.C3.A3o_de_rede)
*   [2 Driver de dispositivo](#Driver_de_dispositivo)
    *   [2.1 Verificando o estado](#Verificando_o_estado)
    *   [2.2 Carregando o módulo](#Carregando_o_m.C3.B3dulo)
*   [3 Interface de rede](#Interface_de_rede)
    *   [3.1 Listando interfaces de rede](#Listando_interfaces_de_rede)
    *   [3.2 Habilitando e desabilitando interfaces de rede](#Habilitando_e_desabilitando_interfaces_de_rede)
*   [4 Obtendo um endereço IP](#Obtendo_um_endere.C3.A7o_IP)
    *   [4.1 Endereço IP dinâmico](#Endere.C3.A7o_IP_din.C3.A2mico)
    *   [4.2 Endereço IP estático](#Endere.C3.A7o_IP_est.C3.A1tico)
        *   [4.2.1 Atribuição manual](#Atribui.C3.A7.C3.A3o_manual)
        *   [4.2.2 Calculando endereços](#Calculando_endere.C3.A7os)
    *   [4.3 Gerenciadores de rede](#Gerenciadores_de_rede)
*   [5 Configurando um hostname](#Configurando_um_hostname)
    *   [5.1 Resolução de hostname de rede local](#Resolu.C3.A7.C3.A3o_de_hostname_de_rede_local)
*   [6 Dicas e truques](#Dicas_e_truques)
    *   [6.1 Alterando o nome do dispositivo](#Alterando_o_nome_do_dispositivo)
    *   [6.2 Revertendo para nomes tradicionais de dispositivos](#Revertendo_para_nomes_tradicionais_de_dispositivos)
    *   [6.3 Definindo o MTU do dispositivo e o tamanho da fila](#Definindo_o_MTU_do_dispositivo_e_o_tamanho_da_fila)
    *   [6.4 ifplugd for laptops](#ifplugd_for_laptops)
    *   [6.5 Bonding e LAG(agregação de LINK)](#Bonding_e_LAG.28agrega.C3.A7.C3.A3o_de_LINK.29)
    *   [6.6 Aliasing de endereço IP](#Aliasing_de_endere.C3.A7o_IP)
        *   [6.6.1 Exemplo](#Exemplo)
    *   [6.7 Modo promíscuo](#Modo_prom.C3.ADscuo)
*   [7 Solução de problemas](#Solu.C3.A7.C3.A3o_de_problemas)
    *   [7.1 Trocando computadores no modem a cabo](#Trocando_computadores_no_modem_a_cabo)
    *   [7.2 O problema de escala de janela TCP](#O_problema_de_escala_de_janela_TCP)
        *   [7.2.1 Como diagnosticar o problema](#Como_diagnosticar_o_problema)
        *   [7.2.2 Formas de corrigi-lo](#Formas_de_corrigi-lo)
            *   [7.2.2.1 Ruim](#Ruim)
            *   [7.2.2.2 Bom](#Bom)
            *   [7.2.2.3 Melhor](#Melhor)
        *   [7.2.3 More about it](#More_about_it)
    *   [7.3 Realtek sem link / Problema com WOL](#Realtek_sem_link_.2F_Problema_com_WOL)
        *   [7.3.1 Habilitando a NIC diretamente no Linux](#Habilitando_a_NIC_diretamente_no_Linux)
        *   [7.3.2 Revertendo/alterando driver do Windows](#Revertendo.2Falterando_driver_do_Windows)
        *   [7.3.3 Habilitando WOL no driver do Windows](#Habilitando_WOL_no_driver_do_Windows)
        *   [7.3.4 Driver Realtek mais novo para Linux](#Driver_Realtek_mais_novo_para_Linux)
        *   [7.3.5 Ativando *LAN Boot ROM* na BIOS/CMOS](#Ativando_LAN_Boot_ROM_na_BIOS.2FCMOS)
    *   [7.4 No interface with Atheros chipsets](#No_interface_with_Atheros_chipsets)
    *   [7.5 Broadcom BCM57780](#Broadcom_BCM57780)
    *   [7.6 Realtek RTL8111/8168B](#Realtek_RTL8111.2F8168B)
    *   [7.7 Placa-mãe Gigabyte com Realtek 8111/8168/8411](#Placa-m.C3.A3e_Gigabyte_com_Realtek_8111.2F8168.2F8411)
*   [8 Veja também](#Veja_tamb.C3.A9m)

## Depuração de rede

Você pode usar [ping(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ping.8) para verificar se você consegue alcançar um host.

1.  Certifique-se que sua [#Interface de rede](#Interface_de_rede) está ativa. Se não estiver listada, verifique seu [#Driver de dispositivo](#Driver_de_dispositivo).
2.  Verifique se você consegue acessar a internet pingando um endereço IP público (p. ex., `8.8.8.8`). Se você não conseguir acessar a internet, mas sua interface de rede estiver ativa, veja [#Obtendo um endereço IP](#Obtendo_um_endere.C3.A7o_IP).
3.  Verifique se você consegue resolver nomes de domínio, pingando um nome de domínio (p. ex., `google.com`). Se você não consegue resolver nomes de domínio, mas você está conectado à Internet, veja [resolv.conf](/index.php/Resolv.conf "Resolv.conf") e verifique a linha `hosts` em [nsswitch.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/nsswitch.conf.5).

**Nota:** Se você receber um erro como `ping: icmp open socket: Operation not permitted` ao executar *ping*, tente reinstalar o pacote [iputils](https://www.archlinux.org/packages/?name=iputils).

## Driver de dispositivo

### Verificando o estado

O [udev](/index.php/Udev "Udev") deve detectar sua [interface de rede](https://en.wikipedia.org/wiki/pt:Placa_de_rede "wikipedia:pt:Placa de rede") (em inglês, *network interface controller* ou NIC) e carregará automaticamente o [módulo de kernel](/index.php/Kernel_module "Kernel module") necessário na inicialização. Verifique pela entrada "Ethernet controller" (ou similar) no resultado do comando `lspci -v`. Este comando dirá qual módulo do kernel é necessário para o funcionamento do dispositivo. Por exemplo:

 `$ lspci -v` 
```
02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1

```

Após, veja se o driver foi carregado usando `dmesg | grep *nome_módulo*`. Exemplo:

 `$ dmesg `  ` grep | atl1` 

Pule para a próxima sessão caso o driver tenha sido carregado com sucesso. Caso contrário, você precisará descobrir qual é o módulo necessário para o seu modelo de interface de rede em específico.

### Carregando o módulo

Pesquise na internet pelo modelo/driver para o seu chipset. Algumas módulos comuns são `8139too` para as placas com um chipset da Realtek, ou `sis900` para placas com um chipset da SiS. Assim que descobrir qual módulo deve usar, tente [carregar o módulo manualmente](/index.php/Kernel_modules#Manual_module_handling "Kernel modules"). Caso você esbarre com algum erro dizendo que o módulo não foi encontrado, é possível que o driver não foi incluído no kernel do Arch Linux. Tente procurar no [AUR](/index.php/AUR_(Portugu%C3%AAs) "AUR (Português)") pelo nome do módulo.

Caso o udev não detecte ou não carregue o módulo de forma apropriada e automaticamente durante o boot, veja [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

## Interface de rede

O [udev](/index.php/Udev "Udev") atribui nomes para suas interfaces de rede. Mais especificamente, o [udev](/index.php/Udev "Udev") usa [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames). Interfaces são agora prefixadas com `en` (cabeada/[Ethernet](https://en.wikipedia.org/wiki/pt:Ethernet "w:pt:Ethernet")), `wl` (sem fio/wireless/WLAN) ou `ww` ([WWAN](https://en.wikipedia.org/wiki/pt:Rede_de_longa_dist%C3%A2ncia_sem_fio "w:pt:Rede de longa distância sem fio")) seguido por um identificador gerado automaticamente.

### Listando interfaces de rede

Ambos nomes de interfaces com e sem fio podem ser descobertos por meio de `ls /sys/class/net` ou `ip link`. Note que `lo` é o [dispositivo *loop* ou de laço](https://en.wikipedia.org/wiki/pt:Loop_device "w:pt:Loop device") e não é usado para fazer conexões de rede.

Nomes de dispositivos sem fio também podem ser obtidos usando `iw dev`. Veja também [Configuração de rede sem fio#Obter o nome da interface](/index.php/Configura%C3%A7%C3%A3o_de_rede_sem_fio#Obter_o_nome_da_interface "Configuração de rede sem fio").

**Dica:** Para alterar os nomes de dispositivos, veja [#Alterando o nome do dispositivo](#Alterando_o_nome_do_dispositivo) e [#Revertendo para nomes tradicionais de dispositivos](#Revertendo_para_nomes_tradicionais_de_dispositivos).

### Habilitando e desabilitando interfaces de rede

Você pode ativar uma interface de rede usando:

```
# ip link set *interface* up

```

Para desativá-la, faça:

```
# ip link set *interface* down

```

Para verificar o resultado para a interface `eth0`:

 `$ ip link show dev eth0` 
```
2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP mode DEFAULT qlen 1000
...

```

**Nota:** Se sua rota padrão é por meio da interface `eth0`, desabilitá-la também vai remover a rota e reativá-la não vai restabelecer automaticamente a rota padrão. Veja [#Atribuição manual](#Atribui.C3.A7.C3.A3o_manual) para restabelecê-la.

## Obtendo um endereço IP

### Endereço IP dinâmico

Veja [#Gerenciadores de rede](#Gerenciadores_de_rede) para uma lista de opções na definição de um endereço IP dinâmico

### Endereço IP estático

Um endereço IP estático pode ser configura com a maioria dos [gerenciadores de rede](#Gerenciadores_de_rede) padrão. Independentemente da ferramenta que você escolher, você provavelmente vai precisar estar preparado com a seguinte informação:

*   Endereço IP estático
*   Máscara de sub-rede ou possivelmente sua [notação CIDR](https://en.wikipedia.org/wiki/pt:CIDR#Nota.C3.A7.C3.A3o_standard "wikipedia:pt:CIDR"); por exemplo, `/24` é a notação CIDR da máscara de rede `255.255.255.0`.
*   [Endereço broadcast](https://en.wikipedia.org/wiki/pt:Endere%C3%A7o_de_broadcast "wikipedia:pt:Endereço de broadcast")
*   Endereço IP do [Gateway](https://en.wikipedia.org/wiki/pt:Gateway "wikipedia:pt:Gateway")
*   Endereços IP dos servidores de nome (DNS). Veja também [resolv.conf](/index.php/Resolv.conf "Resolv.conf").

Se você está usando em uma rede privada, é seguro usar endereços IP em `192.168.*.*` para seus endereços IP, com uma máscara de sub-rede de `255.255.255.0` e um endereço broadcast de `192.168.*.255`. O gateway geralmente é `192.168.*.1` ou `192.168.*.254`.

**Atenção:**

*   Certifique-se de que endereços IP atribuídos manualmetne não conflitem com os atribuídos via DHCP. Veja [esse tópico no fórum](http://www.raspberrypi.org/forums/viewtopic.php?f=28&t=16797).
*   Se você compartilha conexão Internet de uma máquina Windows sem um roteador, certifique-se de usar endereços IP estáticos em ambos computadores para evitar problemas de rede local.

**Dica:** Endereços podem ser calculados com o pacote [ipcalc](https://www.archlinux.org/packages/?name=ipcalc); veja [#Calculando endereços](#Calculando_endere.C3.A7os).

#### Atribuição manual

É possível configurar manualmente um IP estático usando apenas o pacote [iproute2](https://www.archlinux.org/packages/?name=iproute2). Essa é uma boa forma de testar as configurações da conexão, já que a conexão feita usando esse método não persistirá entre as reinicializações. Primeiro, ative a [#Interface de rede](#Interface_de_rede):

```
# ip link set *interface* up

```

Atribua um endereço IP estático no console:

```
# ip addr add *endereço_IP*/*máscara_sub-rede* broadcast *endereço_broadcast* dev *interface*

```

Então, adicione o endereço IP do seu gateway:

```
# ip route add default via *gateway_padrão*

```

Por exemplo:

```
# ip link set eth0 up
# ip addr add 192.168.1.2/24 broadcast 192.168.1.255 dev eth0
# ip route add default via 192.168.1.1

```

**Dica:** Se você receber a mensagem `RTNETLINK answers: Network is unreachable`, tente quebrar a criação da rota nas duas partes a seguir:
```
# ip route add 192.168.1.1 dev eth0
# ip route add default via 192.168.1.1 dev eth0

```

Para desfazer esses passos (ex. antes de trocar para um IP dinâmico), primeiro remova qualquer nedereço IP atribuído:

```
# ip addr flush dev *interface*

```

Então, remova qualquer gateway atribuído:

```
# ip route flush dev *interface*

```

E, finalmente, ative a interface:

```
# ip link set *interface* down

```

Para mais opções, veja [ip(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/ip.8). Esses comandos podem ser atualizados usando scripts e [units de systemd](/index.php/Systemd_(Portugu%C3%AAs)#Escrevendo_arquivos_.service_personalizados "Systemd (Português)").

#### Calculando endereços

Você pode usar `ipcalc`, fornecido pelo pacote [ipcalc](https://www.archlinux.org/packages/?name=ipcalc), para calcular IP de broadcast, rede, máscara de rede e intervalo de hosts para mais configurações avançadas. Um exemplo é usar Ethernet por Firewire para conectar uma máquina Windows a Linux. Para melhorar a segurança e organização, ambas máquinas têm que ter sua rede com a máscara de rede e broadcast configurados corretamente.

A descoberta dos respectivos endereços de máscara de rede e broadcast é feita com `ipcalc`, especificando o IP da interface de rede Linux `10.66.66.1` e o número de hosts (aqui dois):

 `$ ipcalc -nb 10.66.66.1 -s 1` 
```
Endereço:   10.66.66.1

Máscara:    255.255.255.252 = 30
IP de Rede: 10.66.66.0/30
HostMín:    10.66.66.1
HostMáx:    10.66.66.2
Broadcast:  10.66.66.3
Hosts/Rede: 2                     Classe A, Internet Privada
```

### Gerenciadores de rede

Existem muitas soluções para escolher, mas lembre-se de que todas elas são mutuamente exclusivas; você não deve executar dois daemons simultaneamente. A tabela a seguir compara os diferentes gerenciadores de conexão. *Atende automaticamente conexão com fio* significa que existe pelo menos uma opção para o usuário simplesmente iniciar o daemon sem criar um arquivo de configuração.

| Gerenciador de rede | Trata da conexão
com fio
automaticamente | GUI
oficial | [Archiso](/index.php/Archiso "Archiso") [[1]](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.both) | Ferramentas
de console | Units de systemd |
| [ConnMan](/index.php/ConnMan "ConnMan") | Sim | Não | Não | `connmanctl` | `connman.service` |
| [dhcpcd](/index.php/Dhcpcd "Dhcpcd") | Sim | Não | Sim ([base](https://www.archlinux.org/groups/x86_64/base/)) | `dhcpcd` | `dhcpcd.service`, `dhcpcd@*interface*.service` |
| [netctl](/index.php/Netctl "Netctl") | Sim | Não | Sim ([base](https://www.archlinux.org/groups/x86_64/base/)) | `netctl` | `netctl-ifplugd@*interface*.service` |
| [NetworkManager](/index.php/NetworkManager_(Portugu%C3%AAs) "NetworkManager (Português)") | Sim | Sim | Não | `nmcli`,`nmtui` | `NetworkManager.service` |
| [systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd") | Não | Não | Sim ([base](https://www.archlinux.org/groups/x86_64/base/)) | `systemd-networkd.service`, `systemd-resolved.service` |
| [Wicd](/index.php/Wicd "Wicd") | Sim | Sim | Não | `wicd-curses` | `wicd.service` |

Veja também [List of applications#Network managers](/index.php/List_of_applications#Network_managers "List of applications").

## Configurando um hostname

Um [hostname](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname"), ou "nome de máquina", é um nome único criado para identificar uma máquina em uma rede, configurada em `/etc/hostname`—veja [hostname(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.5) e [hostname(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hostname.7) para detalhes. O arquivo pode conter o nome de domínio do sistema, se houver. Para configurar o hostname, [edite](/index.php/Edi%C3%A7%C3%A3o_de_texto "Edição de texto") `/etc/hostname` para incluir uma única linha com `*meuhostname*`:

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

Para configurar um hostname "bonito" e outros metadados de máquina, veja [machine-info(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/machine-info.5#https%3A%2F%2Fwww.freedesktop.org%2Fsoftware%2Fsystemd%2Fman%2Fmachine-info.html).

### Resolução de hostname de rede local

O pré-requisito é ter realizado [#Configurando um hostname](#Configurando_um_hostname), após o qual a resolução de nome funciona no sistema local em si:

 `$ ping *meuhostname*` 
```
PING *meuhostname* (192.168.1.2) 56(84) bytes of data.
64 bytes from *meuhostname* (192.168.1.2): icmp_seq=1 ttl=64 time=0.043 ms
```

Para permitir que outras máquinas enderecem o host pelo nome, é necessário:

*   Configurar o arquivo [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5) ou
*   Habilitar um serviço que resolva o hostname.

**Nota:** [systemd](https://www.archlinux.org/packages/?name=systemd) fornece resolução de hostname via o módulo nss de `meuhostname`, habilitado por padrão em `/etc/nsswitch.conf`. Porém, clientes ainda podem dependere de `/etc/hosts`, veja [[2]](https://lists.debian.org/debian-devel/2013/07/msg00809.html) [[3]](https://bugzilla.mozilla.org/show_bug.cgi?id=87717#c55) por exemplos.

Para configurar o arquivo hosts, adicione a seguinte linha ao `/etc/hosts`:

```
127.0.1.1	*meuhostname*.dominiolocal	*meuhostname*

```

**Nota:** A ordem de hostnames/aliases que seguem o endereço IP no `/etc/hosts` é relevante. A primeira string é considerada o hostname canônico e pode ser adicionada a domínios pais, sendo os componentes de domínio separados por um ponto (p. ex., `.dominiolocal` acima). Todas as strings a seguir na mesma linha são considerados aliases. Veja [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5) para mais informações.

Como um resultado, o sistema resolve ambas entradas:

 `$ getent hosts` 
```
127.0.0.1       localhost
127.0.1.1       *meuhostname*.dominiolocal *meuhostname*

```

Para um sistema com um endereço IP permanente, esse endereço IP permanente deve ser usado em vez de `127.0.1.1`.

**Nota:** Outra opção é configurar um servidor DNS completo, como [BIND](/index.php/BIND "BIND") ou [Unbound](/index.php/Unbound "Unbound"), mas é um exagero e muito complexo para a maioria dos sistemas. Para redes menores e flexibilidade dinâmica com hosts entrando e saindo dos serviços de rede [zero-configuration networking ou zeroconf](https://en.wikipedia.org/wiki/Zero-configuration_networking "wikipedia:Zero-configuration networking") podem ser mais aplicáveis:

*   [Samba](/index.php/Samba "Samba") fornece resolução de nomes via **NetBIOS** da Microsoft. Ele precisa da instalação do [samba](https://www.archlinux.org/packages/?name=samba) e habilitação do serviço `nmbd.service`. Computadores usando Windows, macOS ou Linux com `nmbd` ativo, serão capazes de localizar sua máquina.
*   [Avahi](/index.php/Avahi "Avahi") fornece resolução de nomes via **zeroconf**, também conhecido como Avahi ou Bonjour. É necessário uma configuração um pouco mais complexa que o Samba: veja [Avahi#Hostname resolution](/index.php/Avahi#Hostname_resolution "Avahi") para detalhes details. Computadores usando macOS, ou Linux com um daemon Avahi ativo, serão capazes de localizar sua máquina. Windows não têm um cliente ou daemon Avahi incorporados.

## Dicas e truques

### Alterando o nome do dispositivo

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

O caminho do dispositivo deve corresponder ao nome do dispositivo novo e antigo, uma vez que a regra pode ser executada mais de uma vez na inicialização. Por exemplo, na segunda regra, `"/devices/pci*/*1c.0/*/net/enp*"` seria errado, uma vez que irá parar de corresponder depois que o nome for alterado para `en`. Somente a regra padrão do sistema será chamada na segunda vez, fazendo com que o nome seja alterado de volta para, por exemplo, `enp1s0`.

Para [testar](/index.php/Udev#Testing_rules_before_loading "Udev") suas regras, elas podem ser acionadas diretamente do espaço de usuário, por exemplo, com `udevadm --debug test /sys/*CAMINHO_DISPOSITIVO*`. Lembre-se de primeiro retirar a interface que você está tentando renomear (ex. `ip link set enp1s0 down`).

**Nota:** Ao escolher os nomes estáticos **deve-se evitar o uso de nomes no formato de "eth*X*" e "wlan*X*"**, pois eles podem levar a codiçẽos de corrida entre o kernel e udev durante a inicialização. Em vez disso, é melhor usar nomes de interface que não são usados pelo kernel como padrão, ex.: `net0`, `net1`, `wifi0`, `wifi1`. Para detalhes adicionais, por favor veja a documentação do [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames).

### Revertendo para nomes tradicionais de dispositivos

Se você preferir manter os nomes de interface tradicionais, como eth0, [Predictable Network Interface Names](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames) podem ser desabilitados mascarando a regra de rule:

```
# ln -s /dev/null /etc/udev/rules.d/80-net-setup-link.rules

```

Alternativamente, adicione `net.ifnames=0` aos [parâmetros do kernel](/index.php/Kernel_parameters "Kernel parameters").

### Definindo o MTU do dispositivo e o tamanho da fila

Você pode alterar o [MTU](https://en.wikipedia.org/wiki/pt:MTU "wikipedia:pt:MTU") do dispositivo e o tamanho da fila ao definir manualmente com uma regra de udev. Por exemplo:

 `/etc/udev/rules.d/10-network.rules`  `ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1500", ATTR{tx_queue_len}="2000"` 
**Nota:**

*   `mtu`: Para PPPoE, o MTU não deve ser maior que 1492\. Você também pode definir o MTU via [systemd.netdev(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.netdev.5).
*   `tx_queue_len`: Valores pequenos para dispositivos menores com uma latência maior, como modens e ISDN. Valor alto é recomendado para servidor conectado por meio conexões de Internet de alta velocidade que realiza grandes transferências de dados.

### ifplugd for laptops

**Dica:** [dhcpcd](/index.php/Dhcpcd "Dhcpcd") fornece o mesmo recurso pronto para uso.

O [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) é um daemon que configura automaticamente seu dispositivo Ethernet quando um cabo é conectado e desconfigura automaticamente quando desconectado. É útil para laptops com adaptadores de rede *onboards*, pois configurará a interface quando um cabo realmente for conectado. Outro uso é quando você deseja reiniciar as configurações de rede mas não deseja reiniciar o computador ou deseja fazer isto via linha de comando.

Por padrão, ele é configurado para funcionar para o dispositivo `eth0`. Estas e outras configurações como tempo de espera podem ser alterados no arquivo `/etc/ifplugd/ifplugd.conf`.

**Nota:** O pacote [netctl](/index.php/Netctl "Netctl") inclui `netctl-ifplugd@.service`, do contrário você pode usar `ifplugd@.service` do pacote [ifplugd](https://www.archlinux.org/packages/?name=ifplugd). Por exemplo, [habilite](/index.php/Habilite "Habilite") `ifplugd@eth0.service`.

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

Se você deseja habilitar o modo pomíscuo na interface `eth0`, execute [*enable*](/index.php/Habilite "Habilite") `promiscuous@eth0.service`.

## Solução de problemas

### Trocando computadores no modem a cabo

Alguns ISP por cabo têm o modem a cabo configurado para reconhecer apenas um PC cliente, pelo endereço MAC da sua interface de rede. Uma vez que o modem a cabo aprendeu o endereço MAC do primeiro PC ou equipamento que fala com ele, ele não responderá de outro modo a outro endereço MAC. Assim, se você trocar um PC por outro (ou por um roteador), o novo PC (ou roteador) não funcionará com o modem a cabo, porque o novo PC (ou roteador) possui um endereço MAC diferente do antigo. Para reiniciar o modem a cabo para que reconheça o novo PC, você deve desligar e ligar o modem a cabo. Uma vez que o modem a cabo foi reiniciado e voltou totalmente on-line novamente (as luzes indicadoras foram instaladas), reinicie o PC recém-conectado para que ele faça uma solicitação DHCP ou faça com que ele solicite um novo *lease* (concessão) DHCP.

Caso este método não funcione, você deverá clonar o endereço MAC do computador original. Veja também [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing").

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

Simplesmente desative Escala de Janela. Como a Escala de Janela é um bom recurso TCP, pode ser desconfortável desativá-lo, especialmente se você não conseguir corrigir o roteador quebrado. Há várias maneiras de desativar Escala de Janela, e parece que a maneira mais segura (que funcionará com a maioria dos kernels) é adicionar a seguinte linha a `/etc/sysctl.d/99-disable_window_scaling.conf` (veja também [sysctl](/index.php/Sysctl "Sysctl"):

```
net.ipv4.tcp_window_scaling = 0

```

##### Melhor

Esse problema é causado por roteadores/firewalls quebrados, então vamos mudá-los. Alguns usuários relataram que o roteador quebrado era o próprio roteador DSL.

#### More about it

Essa seção é baseada nos artigos, em inglês, do LWN [Escala de janela e roteadores quebrados](http://lwn.net/Articles/92727/) e do Kernel Trap [Escala de Janela na Internet](http://kerneltrap.org/node/6723).

Há também vários tópicos relevantes no LKML.

### Realtek sem link / Problema com WOL

Os usuários com o Realtek 8168 8169 8101 8111(C) baseados em NIC (placas e *on-board*) podem notar um problema onde a NIC parece estar desativada na inicialização e não tem nenhuma luz no Link. Isso geralmente pode ser encontrado em um sistema de *dual boot*, onde o Windows também está instalado. Parece que o uso dos drivers oficiais do Realtek (datado de qualquer coisa após maio de 2007) no Windows é a causa. Esses drivers mais recentes desativam o recurso Wake-On-LAN desabilitando a NIC no tempo de desligamento do Windows, onde ele permanecerá desabilitado até a próxima vez que o Windows for inicializado. Você poderá notar se esse problema está afetando você se a luz do Link estiver desligada até que o Windows seja iniciado; durante o desligamento do Windows, a luz do link será desligada. A operação normal deve ser que a luz do link esteja sempre ativada enquanto o sistema estiver ligado, mesmo durante o POST. Este problema também afetará outros sistemas operacionais sem drivers mais recentes (por exemplo, Live CDs). Aqui estão algumas correções para este problema.

#### Habilitando a NIC diretamente no Linux

Siga [#Habilitando e desabilitando interfaces de rede](#Habilitando_e_desabilitando_interfaces_de_rede) para habilitar a interface.

#### Revertendo/alterando driver do Windows

Você pode reverter o driver de NIC do Windows para o fornecido pela Microsoft (se disponível), ou reverter/instalar um driver Realtek oficial pré-datado de maio de 2007 (pode estar no CD que acompanhou o hardware).

#### Habilitando WOL no driver do Windows

Provavelmente a melhor e mais correção é mudar essa configuração no driver do Windows. Desta forma, ele deve ser corrigido em todo o sistema e não apenas em Arch (ex.:, Live CDs, outros sistemas operacionais). No Windows, no Gerenciamento de dispositivos, encontre seu adaptador de rede Realtek e clique duas vezes nele. Na guia "Avançado", altere "Wake-on-LAN após o desligamento" para "Ativar".

No Windows XP (exemplo):

```
 Realize duple clique no meu computador e escolha "Propriedades"
 --> Aba "Hardware"
  --> Gerenciamento de dispositivo
    --> Adaptadores de rede
      --> "duplo clique" Realtek ...
        --> Aba "Avançada"
          --> Wake-On-Lan após o desligamento
            --> Habilitar

```

**Nota:** Novos drivers Windows do Realtek (testados com *Realtek 8111/8169 LAN Driver v5.708.1030.2008*, datado de 2009/01/22, disponível da GIGABYTE) podem se referir a esta opção de forma ligeiramente diferente, como *Desligar Wake-On-LAN > Ativar*. Parece que mudar para `Desativar` não tem efeito (você notará que a luz do link ainda está desligada no desligamento do Windows). Uma solução de contorno ruim é inicializar no Windows e apenas reiniciar o sistema (executar um reinício/desligamento desagradável), portanto, não dar ao driver do Windows a chance de desabilitar a LAN. A luz de link permanecerá ativada e o adaptador de LAN permanecerá acessível após o POST - isto é, até reiniciar o Windows e desligá-lo corretamente novamente.

#### Driver Realtek mais novo para Linux

Qualquer driver mais recente para estas placas Realtek pode ser encontrado para o Linux no site da Realtek (não testado, mas acredita que também resolve o problema).

#### Ativando *LAN Boot ROM* na BIOS/CMOS

Parece que a configuração *Periféricos integrados > Onboard LAN Boot ROM > Ativado* na BIOS/CMOS reativa o chip de LAN da Realtek na inicialização do sistema, apesar do driver do Windows desabilitando no desligamento do sistema operacional.

**Nota:** Isso foi testado várias vezes em uma placa-mãe GIGABYTE GA-G31M-ES2L, BIOS versão F8 lançada em 2009/02/05.

### No interface with Atheros chipsets

Os usuários de alguns chips de Ethernet da Atheros estão relatando que não funciona pronto para uso (com mídia de instalação de fevereiro de 2014). A solução de trabalho para isso é instalar [backports-patched](https://aur.archlinux.org/packages/backports-patched/).

### Broadcom BCM57780

Este chipset Broadcom às vezes não se comporta bem, a menos que você especifique a ordem dos módulos a serem carregados. Os módulos são `broadcom` e `tg3`, o primeiro que precisa ser carregado primeiro.

Essas etapas devem ajudar se o seu computador tiver esse chipset:

*   Localize sua NIC na saída do *lspci*:

 `$ lspci | grep Ethernet` 
```
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

*   Se sua rede com fio não estiver funcionando de alguma maneira, desconecte seu cabo e, em seguida, faça o seguinte:

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

*   Conecte seu cabo de rede de volta e verifique se o módulo foi carregado com sucesso com:

```
$ dmesg | greg tg3

```

*   Se esse procedimento resolveu o problema, você pode torná-lo permanente adicionando `broadcom` e `tg3` (nesta ordem) para o vetor `MODULES`:

 `/etc/mkinitcpio.conf`  `MODULES=(.. broadcom tg3 ..)` 

*   [Gere novamente o initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs")
*   Alternativamente, você pode criar um `/etc/modprobe.d/broadcom.conf`:

```
softdep tg3 pre: broadcom

```

**Nota:** Esses métodos podem funcionar para outros chipsets, tal como BCM57760.

### Realtek RTL8111/8168B

 `# lspci | grep Ethernet` 
```
03:00.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL8111/8168B PCI Express Gigabit Ethernet controller (rev 02)

```

O adaptador deve ser reconhecido pelo módulo `r8169`. No entanto, com algumas revisões de chips, a conexão pode cair e voltar o tempo todo. A alternativa [r8168](https://www.archlinux.org/packages/?name=r8168) deve ser usada para uma conexão confiável neste caso. [Lista negra](/index.php/Blacklist "Blacklist") `r8169`, se [r8168](https://www.archlinux.org/packages/?name=r8168) não for carregado automaticamente pelo [udev](/index.php/Udev "Udev"), veja [Kernel modules#Automatic module handling](/index.php/Kernel_modules#Automatic_module_handling "Kernel modules").

Outra falha nos drivers para algumas revisões deste adaptador é um suporte fraco de IPv6\. [IPv6#Disable functionality](/index.php/IPv6#Disable_functionality "IPv6") pode ser útil se você encontrar problemas como pendurar páginas da web e velocidades lentas.

### Placa-mãe Gigabyte com Realtek 8111/8168/8411

Com placas-mãe como o *Gigabyte GA-990FXA-UD3*, inicializar com [IOMMU](/index.php/PCI_passthrough_via_OVMF#Setting_up_IOMMU "PCI passthrough via OVMF") desligado (o que pode ser o padrão) fará com que a interface de rede não seja confiável, muitas vezes não conseguindo se conectar, ou até conectar mas não permitindo a transferência. Isso se aplicará à NIC *on-board* e para qualquer outra NIC pci na máquina porque a configuração IOMMU afeta toda a interface de rede na placa. Habilitar o IOMMU e inicializar com a mídia de instalação lançará as falhas da página AMD I-10/xhci por um segundo, mas depois inicializará normalmente, resultando em uma NIC *onboard* totalmente funcional (mesmo com o módulo r8169).

Ao configurar o processo de inicialização para sua instalação, adicione `iommu=soft` como um [parâmetro de kernel](/index.php/Kernel_parameter "Kernel parameter") para eliminar as mensagens de erro na inicialização e restaurar a funcionalidade USB3.0.

## Veja também

*   [Referência do Debian: Configuração de Rede](https://www.debian.org/doc/manuals/debian-reference/ch05.en.html)
*   [RHEL7: Guia de Rede](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Networking_Guide/)
*   [Linux Home Networking](http://www.linuxhomenetworking.com/wiki/)
*   [Monitorando e ajustando o Linux a Pilha de Conectividade: Recebendo dados](https://blog.packagecloud.io/eng/2016/06/22/monitoring-tuning-linux-networking-stack-receiving-data/)
*   [Monitorando e ajustando o Linux a Pilha de Conectividade: Enviando dados](https://blog.packagecloud.io/eng/2017/02/06/monitoring-tuning-linux-networking-stack-sending-data/)
*   [Rastreamento de uma viagem de pacotes usando tracepoints, perf e eBPF](http://blog.yadutaf.fr/2017/07/28/tracing-a-packet-journey-using-linux-tracepoints-perf-ebpf/)