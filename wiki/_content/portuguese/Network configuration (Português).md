Esta página explica como configurar uma conexão **cabeada**. Se você deseja configurar uma rede **wireless/sem fio** veja a página [Configuração de Redes Sem Fio](/index.php?title=Wireless_Setup_(Portugu%C3%AAs)&action=edit&redlink=1 "Wireless Setup (Português) (page does not exist)").

## Contents

*   [1 Verificando a conexão](#Verificando_a_conex.C3.A3o)
*   [2 Configurando um hostname](#Configurando_um_hostname)
*   [3 Drivers de dispositivos](#Drivers_de_dispositivos)
    *   [3.1 Verifique o estado do seu driver](#Verifique_o_estado_do_seu_driver)
    *   [3.2 Carregando o driver do dispositivo](#Carregando_o_driver_do_dispositivo)
*   [4 Interfaces de Rede](#Interfaces_de_Rede)
    *   [4.1 Nomes de dispositivos](#Nomes_de_dispositivos)
        *   [4.1.1 Alterando o nome de um dispositivo](#Alterando_o_nome_de_um_dispositivo)
    *   [4.2 Alterando MTU e tamanho da fila](#Alterando_MTU_e_tamanho_da_fila)
    *   [4.3 Descobrir nome dos dispositivos atuais](#Descobrir_nome_dos_dispositivos_atuais)
    *   [4.4 Enabling and disabling network interfaces](#Enabling_and_disabling_network_interfaces)
    *   [4.5 Ativando e desabilitando interfaces de rede](#Ativando_e_desabilitando_interfaces_de_rede)
*   [5 Configurando endereços IP](#Configurando_endere.C3.A7os_IP)
    *   [5.1 Endereço IP dinâmico](#Endere.C3.A7o_IP_din.C3.A2mico)
        *   [5.1.1 Execução manual do serviço(daemon) DHCP](#Execu.C3.A7.C3.A3o_manual_do_servi.C3.A7o.28daemon.29_DHCP)
        *   [5.1.2 DHCP durante o boot](#DHCP_durante_o_boot)
    *   [5.2 Static IP address](#Static_IP_address)
        *   [5.2.1 Atribuição Manual](#Atribui.C3.A7.C3.A3o_Manual)
        *   [5.2.2 Conexão manual no boot utilizando o systemd](#Conex.C3.A3o_manual_no_boot_utilizando_o_systemd)
        *   [5.2.3 Calculando endereços](#Calculando_endere.C3.A7os)
*   [6 Aplicando configurações](#Aplicando_configura.C3.A7.C3.B5es)
*   [7 Configurações adicionais](#Configura.C3.A7.C3.B5es_adicionais)
    *   [7.1 ifplugd para laptops](#ifplugd_para_laptops)
    *   [7.2 Bonding e LAG(agregação de LINK)](#Bonding_e_LAG.28agrega.C3.A7.C3.A3o_de_LINK.29)
    *   [7.3 Alias de endereço de IP](#Alias_de_endere.C3.A7o_de_IP)
        *   [7.3.1 Exemplo](#Exemplo)
    *   [7.4 Alteração de endereço MAC](#Altera.C3.A7.C3.A3o_de_endere.C3.A7o_MAC)
    *   [7.5 Compartilhamento de internet](#Compartilhamento_de_internet)
    *   [7.6 Configuração de roteador](#Configura.C3.A7.C3.A3o_de_roteador)
*   [8 Resolução de problemas](#Resolu.C3.A7.C3.A3o_de_problemas)
    *   [8.1 Computadores alternando quando conectados a um modem](#Computadores_alternando_quando_conectados_a_um_modem)
    *   [8.2 The TCP window scaling problem](#The_TCP_window_scaling_problem)
        *   [8.2.1 How to diagnose the problem](#How_to_diagnose_the_problem)
        *   [8.2.2 How to fix it (The bad way)](#How_to_fix_it_.28The_bad_way.29)
        *   [8.2.3 How to fix it (The good way)](#How_to_fix_it_.28The_good_way.29)
        *   [8.2.4 How to fix it (The best way)](#How_to_fix_it_.28The_best_way.29)
        *   [8.2.5 More about it](#More_about_it)
    *   [8.3 Realtek no link / WOL problem](#Realtek_no_link_.2F_WOL_problem)
        *   [8.3.1 Method 1 - Rollback/change Windows driver](#Method_1_-_Rollback.2Fchange_Windows_driver)
        *   [8.3.2 Method 2 - Enable WOL in Windows driver](#Method_2_-_Enable_WOL_in_Windows_driver)
        *   [8.3.3 Method 3 - Newer Realtek Linux driver](#Method_3_-_Newer_Realtek_Linux_driver)
        *   [8.3.4 Method 4 - Enable _LAN Boot ROM_ in BIOS/CMOS](#Method_4_-_Enable_LAN_Boot_ROM_in_BIOS.2FCMOS)
    *   [8.4 DLink G604T/DLink G502T DNS problem](#DLink_G604T.2FDLink_G502T_DNS_problem)
        *   [8.4.1 How to diagnose the problem](#How_to_diagnose_the_problem_2)
        *   [8.4.2 How to fix it](#How_to_fix_it)
        *   [8.4.3 More about it](#More_about_it_2)
    *   [8.5 Check DHCP problem by releasing IP first](#Check_DHCP_problem_by_releasing_IP_first)
    *   [8.6 No eth0 with Atheros AR8161](#No_eth0_with_Atheros_AR8161)
    *   [8.7 No eth0 with Atheros AR9485](#No_eth0_with_Atheros_AR9485)
    *   [8.8 No carrier / no connection after suspend](#No_carrier_.2F_no_connection_after_suspend)
    *   [8.9 PC Pingable by IP but not by hostname?](#PC_Pingable_by_IP_but_not_by_hostname.3F)
    *   [8.10 Broadcom BCM57780](#Broadcom_BCM57780)

## Verificando a conexão

**Note:** Se você receber algum erro como `ping: icmp open socket: Operation not permitted` quando executar o comando ping, tente reinstalar o pacote `iputils`.

Muitas vezes, o procedimento básico de instalação cria uma configuração de rede cabeada. Para verificar se há configuração, utilize o seguinte comando:

**Note:** A opção `-c 3` chama 3 vezes a ação de envio de pacotes icmp. Veja `man ping` para maiores informações.

 `$ ping -c 3 www.google.com` 

```
PING www.l.google.com (74.125.224.146) 56(84) bytes of data.
64 bytes from 74.125.224.146: icmp_req=1 ttl=50 time=437 ms
64 bytes from 74.125.224.146: icmp_req=2 ttl=50 time=385 ms
64 bytes from 74.125.224.146: icmp_req=3 ttl=50 time=298 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 1999ms
rtt min/avg/max/mdev = 298.107/373.642/437.202/57.415 ms
```

Caso funcione, você precisará apenas personalizar algumas das opções abaixo.

Se o comando acima reclamar de unknown hosts(host desconhecido), significa que seu computador não pôde resolver nomes de domínios. Pode ser relacionado ao seu provedor de internet ou gateway/roteador. Tente pingar um endereço IP para provar que sua máquina possui acesso a internet.

 `$ ping -c 3 8.8.8.8` 

```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_req=1 ttl=53 time=52.9 ms
64 bytes from 8.8.8.8: icmp_req=2 ttl=53 time=72.5 ms
64 bytes from 8.8.8.8: icmp_req=3 ttl=53 time=70.6 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2002ms
rtt min/avg/max/mdev = 52.975/65.375/72.543/8.803 ms
```

**Note:** `8.8.8.8` é um endereço ip estático de fácil memorização. É o endereço do DNS primário do Google, considerado uma fonte confiável para testes e geralmente não bloqueado por sistemas de filtro de conteúdo ou proxies.

Caso você consiga pingar este endereço, pode adicioná-lo ao arquivo `/etc/resolv.conf` com a palavra nameserver na frente como solução de dns.

## Configurando um hostname

Um A [hostname](https://en.wikipedia.org/wiki/Hostname "wikipedia:Hostname") é um endereço único criado para identificar um computador em uma rede. É configurado no arquivo `/etc/hostname`. Este arquivo pode conter o domínio do sistema, se houver. Para configurar um hostname, execute:

```
# hostnamectl set-hostname **meunome**

```

Este comando colocará a informação **meunome** no arquivo `/etc/hostname`.

Veja `man 5 hostname` e `man 1 hostnamectl` para maiores detalhes.

**Note:**

*   `hostnamectl` suporta FQDNs
*   Você não precisa mais editar o arquivo `/etc/hosts`, pois o [systemd](https://www.archlinux.org/packages/?name=systemd) proverá a resolução de nomes, e é instalado por padrão no sistema.

Para alterar o hostname temporariamente(até o próximo restart), utilize o comando `hostname` do pacote [inetutils](https://www.archlinux.org/packages/?name=inetutils):

```
# hostname _meunome_

```

## Drivers de dispositivos

### Verifique o estado do seu driver

O [udev](/index.php/Udev "Udev") deverá detectar sua interface de rede([NIC](http://pt.wikipedia.org/wiki/Placa_de_rede)) e carregará automaticamente o módulo necessário. Busque pela entrada "Ethernet controller"(ou similar) no resultado do comando `lspci -v`. Este comando dirá qual módulo do kernel é necessário para o funcionamento do dispositivo. Por exemplo:

 `$ lspci -v` 

```
 02:00.0 Ethernet controller: Attansic Technology Corp. L1 Gigabit Ethernet Adapter (rev b0)
 	...
 	Kernel driver in use: atl1
 	Kernel modules: atl1
```

Após, veja se o driver foi carregado através de um `dmesg | grep _module_name_`. Exemplo:

```
$ dmesg | grep atl1
   ...
   atl1 0000:02:00.0: eth0 link is up 100 Mbps full duplex

```

Pule para a próxima sessão caso o driver tenha sido carregado com sucesso. Caso contrário, você precisará descobrir qual é o módulo necessário para o seu modelo de interface de rede em específico.

### Carregando o driver do dispositivo

Busque na internet(google) pelo modelo de sua placa e descubra qual o chipset. Algumas placas mais comuns utilizam o chipset da Realtek `8139too`, ou `sis900` da SiS. Assim que descobrir qual módulo deve usar, tente [carregar o módulo manualmente](/index.php/Kernel_modules#Manual_module_handling "Kernel modules"). Caso você esbarre com algum erro dizendo que o módulo não foi encontrado, é possível que o driver não foi incluído no kernel do Arch Linux. Tente procurar no [AUR](/index.php/AUR "AUR") pelo nome do módulo.

Caso o udev não detecte ou não carregue o módulo de forma apropriada e automaticamente durante o boot, veja a página [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules").

## Interfaces de Rede

### Nomes de dispositivos

Para placas-mãe que possuem interfaces de rede embutidas, é importante ter um nome de dispositivo fixo. Grande parte dos problemas são causados por nomes de dispositivos que mudam.

O [Udev](/index.php/Udev "Udev") é o responsavel por qual nome um dispositivo deve receber. O systemd v197 introduziu os [nomes de interface previsíveis](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames), que automaticamente atribuem nomes estáticos a dispositivos de rede. Interfaces são prefixadas como en (ethernet), wl (WLAN), ou ww (WWAN) seguido por um identificados, criando uma entrada similar a `enp0s25`.

Este comportamento pode ser desabilitado com o segunite link simbólico:

```
# ln -s /dev/null /etc/udev/rules.d/80-net-name-slot.rules

```

Usuários atualizando de uma versão mais antiga do systemd terão arquivos de regras criados automaticamente em branco. Caso você queira usar os nomes persistentes, apenas delete tal arquivo.

**Tip:** Você pode rodar um `ip link` ou `ls /sys/class/net` para listar todas as interfaces.

#### Alterando o nome de um dispositivo

Você pode alterar o nome de um dispositivo definindo o nome em uma regra do udev. Exemplo:

 `/etc/udev/rules.d/10-network.rules` 

```
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="aa:bb:cc:dd:ee:ff", NAME="net1"
SUBSYSTEM=="net", ACTION=="add", ATTR{address}=="ff:ee:dd:cc:bb:aa", NAME="net0"
```

Alguns detalhes devem ser ressaltados:

*   Para obter o endereço MAC de cada interface, utilize o comando `cat /sys/class/net/**device-name**/address`
*   Certifique-se de utilizar valores em caixa baixa para valores hexadecimais em regras do udev. Ele não gosta de caixa alta.

**Note:** Quando escolher nomes estáticos **nomes no formato "eth_X_" and "wlan_X_" devem ser evitados**, pois podem causar race conditions entre o kernel e o udev durante o boot. É melhor utilizar nomes que não são os padrões do kernel como: `net0`, `net1`, `wifi0`, `wifi1`. Para maiores detalhes, veja a documentação do [systemd](http://www.freedesktop.org/wiki/Software/systemd/PredictableNetworkInterfaceNames).

### Alterando MTU e tamanho da fila

Você pode alterar o MTU de um dispositivo através de uma regra do udev. Exemplo:

 `/etc/udev/rules.d/10-network.rules`  `ACTION=="add", SUBSYSTEM=="net", KERNEL=="wl*", ATTR{mtu}="1480", ATTR{tx_queue_len}="2000"` 

### Descobrir nome dos dispositivos atuais

Os nomes dos dispositivos em execução podem ser obtidos através do sysfs

 `$ ls /sys/class/net`  `lo eth0 eth1 firewire0` 

### Enabling and disabling network interfaces

### Ativando e desabilitando interfaces de rede

Você pode ativar e desabilitar interfaces de rede através dos comandos:

```
# ip link set eth0 up
# ip link set eth0 down

```

Prova real:

 `$ ip link show dev eth0` 

```
2: eth0: <BROADCAST,MULTICAST,PROMISC,UP,LOWER_UP> mtu 1500 qdisc pfifo_fast master br0 state UP mode DEFAULT qlen 1000
[...]
```

## Configurando endereços IP

Você possui duas opções: Endereços dinâmicos através de [DHCP](http://pt.wikipedia.org/wiki/Dynamic_Host_Configuration_Protocol) ou um endereço "estático".

### Endereço IP dinâmico

#### Execução manual do serviço(daemon) DHCP

Note que `dhcpcd` não é `dhcpd`.

 `# dhcpcd eth0` 

```
 dhcpcd: version 5.1.1 starting
 dhcpcd: eth0: broadcasting for a lease
 ...
 dhcpcd: eth0: leased 192.168.1.70 for 86400 seconds
```

Através do comando, `ip addr show dev eth0` você verificará o endereço obtido.

Em alguns cenários, o comando `dhclient` do pacote [dhclient](https://www.archlinux.org/packages/?name=dhclient) funcionará e o `dhcpcd` falhará.

#### DHCP durante o boot

Se você deseja apenas usar o DHCP em sua coenxão cabeada, você pode usar o serviço `dhcpcd@.service` provido pelo pacote {Pkg|dhcpcd}},

Para iniciar o DHCP na interface `eth0`:

```
# systemctl start dhcpcd@eth0

```

Você pode habilitar o serviço para iniciar no boot do sistema com o comando:

```
# systemctl enable dhcpcd@eth0

```

Caso o serviço dhcpd inicie antes do módulo da interface de rede ser carregado([FS#30235](https://bugs.archlinux.org/task/30235)), adicione sua interface de rede ao arquivo `/etc/modules-load.d/*.conf`. Por exemplo, se o módulo da Realtek `r8169` precisa ser carregado crie o arquivo:

 `/etc/modules-load.d/realtek.conf`  `r8169` 
**Tip:** Para descobrir quais módulos são utilizados por uma placa de rede, utilize o comando `lspci -k`.

Se você utiliza DHCP e **não** deseja ter o DNS configurado automaticamente cada vez que a rede for iniciada, adicione o seguinte conteúdo na última sessão do arquivo `dhcpcd.conf`:

 `/etc/dhcpcd.conf`  `nohook resolv.conf` 

Para previnir que o `dhcpcd` adicione nomes de domínio ao `/etc/resolv.conf`, use a opção `nooption`:

 `/etc/dhcpcd.conf`  `nooption domain_name_servers` 

Assim, você poderá editar o arquivo `/etc/resolv.conf` com suas próprias configurações de DNS.

Você pode usar o pacote [openresolv](https://www.archlinux.org/packages/?name=openresolv) caso diferentes processos desejam controlar o arquivo `/etc/resolv.conf` (por exemplo, [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) e um cliente de VPN). Nenhuma configuração adicional para o [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) é necessária para se adequar ao [openresolv](https://www.archlinux.org/packages/?name=openresolv).

### Static IP address

Há várias razões que levam a utilização de um IP estático de rede. Os benefícios de maior visibilidade são previsibilidade dos ips utilizados, ou por ausência de um servidor DHCP.

**Note:** Caso você compartilhe a Internet através de uma estação Windows, certifique-se de atribuir um ip estático para evitar problemas para ambos computadores.

Você precisa de:

*   Endereço estático
*   [Máscara de rede](http://pt.wikipedia.org/wiki/M%C3%A1scara_de_rede)
*   [Endereço de broadcast](http://pt.wikipedia.org/wiki/Endere%C3%A7o_de_broadcast)
*   Endereço IP do [gateway](http://pt.wikipedia.org/wiki/Gateway)

Se você estiver em uma rede privada, é seguro atribuir endereços ip 192.168.*.* com a máscara de rede 255.255.255.0 e broadcast 192.168.*.255\. O gateway geralmente possui os endereços 192.168.*.1 ou 192.168.*.254.

#### Atribuição Manual

Você pode atribuir um endereço IP no console com o comando:

```
# ip addr add <IP address>/<subnet mask> dev <interface>

```

Exemplo:

```
# ip addr add 192.168.1.2/24 dev eth0

```

**Note:** A máscara de rede deve ser atribuída na notação [CIDR](http://pt.wikipedia.org/wiki/CIDR).

Para maiores opções veja `man ip`.

Para adicionar rota até o gateway da rede:

```
# ip route add default via <default gateway IP address>

```

Exemplo:

```
# ip route add default via 192.168.1.1

```

Caso ocorra o erro No such process", significa que o dispositivo está desabilitado. Execute `ip link set dev eth0 up` como root.

#### Conexão manual no boot utilizando o systemd

Primeiro, crie um arquivo de configuração de serviço do [systemd](/index.php/Systemd "Systemd"), trocando a palavra `<interface>` pela sua interface em questão:

 `/etc/conf.d/network@<interface>` 

```
address=192.168.0.15
netmask=24
broadcast=192.168.0.255
gateway=192.168.0.1

```

Crie um arquivo de unidade do systemd:

 `/etc/systemd/system/network@.service` 

```
[Unit]
Description=Network connectivity (%i)
Wants=network.target
Before=network.target
BindsTo=sys-subsystem-net-devices-%i.device
After=sys-subsystem-net-devices-%i.device

[Service]
Type=oneshot
RemainAfterExit=yes
EnvironmentFile=/etc/conf.d/network@%i
ExecStart=/usr/bin/ip link set dev %i up
ExecStart=/usr/bin/ip addr add ${address}/${netmask} broadcast ${broadcast} dev %i
ExecStart=/usr/bin/ip route add default via ${gateway}

ExecStop=/usr/bin/ip addr flush dev %i
ExecStop=/usr/bin/ip link set dev %i down

[Install]
WantedBy=multi-user.target

```

Habilite a unidade e inicie, passando o nome da interface:

```
# systemctl enable network@eth0.service
# systemctl start network@eth0.service

```

#### Calculando endereços

Você pode utilizar a ferramenta `ipcalc`(pacote [ipcalc](https://www.archlinux.org/packages/?name=ipcalc)) para calcular endereços de broadcast, rede, máscara de rede e escopo para configurações mais avançadas. Por exemplo, eu utilizo ethernet over firewire para conectar uma máquina Windows ao arch. Por razões de segurança e organização, criei uma rede configurando broadcast e máscara de rede de formas que apenas dois computadores caibam em tal endereçamento. Para descobrir a mascara de rede e endereço broadcast, utilizei o ipcalc, provendo o ip do arch com a interface firewire(10.66.66.1) e especificando ao ipcalc que desejava apenas 2 hosts na rede.

 `$ ipcalc -nb 10.66.66.1 -s 1` 

```
Address:   10.66.66.1

Netmask:   255.255.255.252 = 30
Network:   10.66.66.0/30
HostMin:   10.66.66.1
HostMax:   10.66.66.2
Broadcast: 10.66.66.3
Hosts/Net: 2                     Class A, Private Internet
```

## Aplicando configurações

Para testar suas configurações, reinicie o computador ou os serviços relevantes:

```
# systemctl restart dhcpcd@eth0

```

Tente pingar seu gateway, servidor DNS, provedor de internet e outros sites nesta ordem, para detectar problemas ao longo do percurso como mo exemplo abaixo:

```
$ ping -c 3 www.google.com

```

## Configurações adicionais

### ifplugd para laptops

O [ifplugd](https://www.archlinux.org/packages/?name=ifplugd) nos repositórios oficiais é um serviço(daemon) que automaticamente configura uma interface Ethernet quando um cabo é conectado, e automaticamente desconfigura quando desplugado. É util para laptops com adaptadores onboars, pois configurará a interface apenas quando o cabo for realmente conectado. Outro uso é quando você deseja reiniciar as configurações de rede mas não deseja reiniciar o computador ou deseja fazer isto via linha de comando.

Por padrão, ele é configurado para funcionar com a interface de nome `eth0`. Estas e outras configurações como tempo de espera podem ser alterados no arquivo `/etc/ifplugd/ifplugd.conf`.

**Note:** O pacote [netctl](/index.php/Netctl "Netctl") inclui `netctl-ifplugd@.service`, ou você pode usar o serviço `ifplugd@.service` do pacote [ifplugd](https://www.archlinux.org/packages/?name=ifplugd). Isto lhe dá a opção de ativar a rede através do comando `systemctl enable ifplugd@eth0.service`.

### Bonding e LAG(agregação de LINK)

Veja [netctl#Bonding](/index.php/Netctl#Bonding "Netctl").

### Alias de endereço de IP

Alias de IP é o processo de adicionar mais de um endereço IP a uma interface de rede. Com isto, um nó em uma rede pode ter vários IPs, cada um servindo para um propósito distinto. A utilização típica destes é para hospedagem de servidores Web ou FTP, ou reorganização de servidores sem precisar a alteração de outros servidores chave em uma rede (útil especialmente para servidores de DNS).

#### Exemplo

Você precisará do pacote [netctl](https://www.archlinux.org/packages/?name=netctl) instalado.

Configuração:

 `/etc/netctl/minharede` 

```
Connection='ethernet'
Description='Cinco IPs em uma conexão ethernet'
Interface='eth0'
IP='static'
Address=('192.168.1.10' '192.168.178.11' '192.168.1.12' '192.168.1.13' '192.168.1.14' '192.168.1.15')
Gateway='192.168.1.1'
DNS=('192.168.1.1')
```

Então execute:

```
$ netctl start minharede

```

### Alteração de endereço MAC

Veja [MAC address spoofing](/index.php/MAC_address_spoofing "MAC address spoofing").

### Compartilhamento de internet

Veja [Internet sharing](/index.php/Internet_sharing "Internet sharing").

### Configuração de roteador

Veja [Router](/index.php/Router "Router").

## Resolução de problemas

### Computadores alternando quando conectados a um modem

A maioria dos provedores de internet domésticos possuem um modem cabeado configurado para reconhecer apenas um computador cliente pelo MAC address, em sua interface de rede. A partir do momento em que o modem aprendeu o endereço MAC do primeiro equipamento, ele não responderá ao outro MAC localizado na rede. Ainda, se você trocar de um PC para outro, o novo PC não funcionará por possuir um MAC diferente do já aprendido pelo roteador. Para resetar o modem para que reconheça o novo PC, você deve desplugar o cabo de força do modem e plugá-lo novamente. Uma vez que o modem for reiniciado e estiver online(olhe nas luzes alternando), reinicie o novo PC para garantir uma requisição DHCP, ou faça tal requisição na mão.

Caso este método não funcione, você deverá clonar o endereço MAC do computador original. Veja [alterando endereços MAC](/index.php/Configuring_Network#Change_MAC.2Fhardware_address "Configuring Network").

### The TCP window scaling problem

TCP packets contain a "window" value in their headers indicating how much data the other host may send in return. This value is represented with only 16 bits, hence the window size is at most 64Kb. TCP packets are cached for a while (they have to be reordered), and as memory is (or used to be) limited, one host could easily run out of it.

Back in 1992, as more and more memory became available, [RFC 1323](http://www.faqs.org/rfcs/rfc1323.html) was written to improve the situation: Window Scaling. The "window" value, provided in all packets, will be modified by a Scale Factor defined once, at the very beginning of the connection.

That 8-bit Scale Factor allows the Window to be up to 32 times higher than the initial 64Kb.

It appears that some broken routers and firewalls on the Internet are rewriting the Scale Factor to 0 which causes misunderstandings between hosts.

The Linux kernel 2.6.17 introduced a new calculation scheme generating higher Scale Factors, virtually making the aftermaths of the broken routers and firewalls more visible.

The resulting connection is at best very slow or broken.

#### How to diagnose the problem

First of all, let's make it clear: this problem is odd. In some cases, you will not be able to use TCP connections (HTTP, FTP, ...) at all and in others, you will be able to communicate with some hosts (very few).

When you have this problem, the `dmesg`'s output is OK, logs are clean and `ip addr` will report normal status... and actually everything appears normal.

If you cannot browse any website, but you can ping some random hosts, chances are great that you're experiencing this problem: ping uses ICMP and is not affected by TCP problems.

You can try to use Wireshark. You might see successful UDP and ICMP communications but unsuccessful TCP communications (only to foreign hosts).

#### How to fix it (The bad way)

To fix it the bad way, you can change the tcp_rmem value, on which Scale Factor calculation is based. Although it should work for most hosts, it is not guaranteed, especially for very distant ones.

```
# echo "4096 87380 174760" > /proc/sys/net/ipv4/tcp_rmem

```

#### How to fix it (The good way)

Simply disable Window Scaling. Since Window Scaling is a nice TCP feature, it may be uncomfortable to disable it, especially if you cannot fix the broken router. There are several ways to disable Window Scaling, and it seems that the most bulletproof way (which will work with most kernels) is to add the following line to `/etc/sysctl.d/99-disable_window_scaling.conf` (see also [sysctl](/index.php/Sysctl "Sysctl"))

```
net.ipv4.tcp_window_scaling = 0

```

#### How to fix it (The best way)

This problem is caused by broken routers/firewalls, so let's change them. Some users have reported that the broken router was their very own DSL router.

#### More about it

This section is based on the LWN article [TCP window scaling and broken routers](http://lwn.net/Articles/92727/) and a Kernel Trap article: [Window Scaling on the Internet](http://kerneltrap.org/node/6723).

There are also several relevant threads on the LKML.

### Realtek no link / WOL problem

Users with Realtek 8168 8169 8101 8111(C) based NICs (cards / and on-board) may notice a problem where the NIC seems to be disabled on boot and has no Link light. This can usually be found on a dual boot system where Windows is also installed. It seems that using the offical Realtek drivers (dated anything after May 2007) under Windows is the cause. These newer drivers disable the Wake-On-LAN feature by disabling the NIC at Windows shutdown time, where it will remain disabled until the next time Windows boots. You will be able to notice if this problem is affecting you if the Link light remains off until Windows boots up; during Windows shutdown the Link light will switch off. Normal operation should be that the link light is always on as long as the system is on, even during POST. This problem will also affect other operative systems without newer drivers (eg. Live CDs). Here are a few fixes for this problem:

#### Method 1 - Rollback/change Windows driver

You can roll back your Windows NIC driver to the Microsoft provided one (if available), or roll back/install an official Realtek driver pre-dating May 2007 (may be on the CD that came with your hardware).

#### Method 2 - Enable WOL in Windows driver

Probably the best and the fastest fix is to change this setting in the Windows driver. This way it should be fixed system-wide and not only under Arch (eg. live CDs, other operative systems). In Windows, under Device Manager, find your Realtek network adapter and double-click it. Under the Advanced tab, change "Wake-on-LAN after shutdown" to Enable.

```
In Windows XP (example)
Right click my computer
--> Hardware tab
  --> Device Manager
    --> Network Adapters
      --> "double click" Realtek ...
        --> Advanced tab
          --> Wake-On-Lan After Shutdown
            --> Enable

```

**Note:** Newer Realtek Windows drivers (tested with _Realtek 8111/8169 LAN Driver v5.708.1030.2008_, dated 2009/01/22, available from GIGABYTE) may refer to this option slightly differently, like _Shutdown Wake-On-LAN --> Enable_. It seems that switching it to `Disable` has no effect (you will notice the Link light still turns off upon Windows shutdown). One rather dirty workaround is to boot to Windows and just reset the system (perform an ungraceful restart/shutdown) thus not giving the Windows driver a chance to disable LAN. The Link light will remain on and the LAN adapter will remain accessible after POST - that is until you boot back to Windows and shut it down properly again.

#### Method 3 - Newer Realtek Linux driver

Any newer driver for these Realtek cards can be found for Linux on the realtek site. (untested but believed to also solve the problem).

#### Method 4 - Enable _LAN Boot ROM_ in BIOS/CMOS

It appears that setting _Integrated Peripherals --> Onboard LAN Boot ROM --> Enabled_ in BIOS/CMOS reactivates the Realtek LAN chip on system boot-up, despite the Windows driver disabling it on OS shutdown.
<small>This was tested successfully multiple times with GIGABYTE system board GA-G31M-ES2L with BIOS version F8 released on 2009/02/05\. YMMV.</small>

### DLink G604T/DLink G502T DNS problem

Users with a DLink G604T/DLink G502T router, using DHCP and have firmware v2.00+ (typically users with AUS firmware) may have problems with certain programs not resolving the DNS. One of these programs are unfortunatley pacman. The problem is basically the router in certain situations is not sending the DNS properly to DHCP, which causes programs to try and connect to servers with an IP address of 1.0.0.0 and fail with a connection timed out error

#### How to diagnose the problem

The best way to diagnose the problem is to use Firefox/Konqueror/links/seamonkey and to enable wget for pacman. If this is a fresh install of Arch Linux, then you may want to consider installing `links` through the live CD.

Firstly, enable wget for pacman (since it gives us info about pacman when it is downloading packages) Open `/etc/pacman.conf` with your favourite editor and uncomment the following line (remove the # if it is there)

```
XferCommand=/usr/bin/wget --passive-ftp -c -O %o %u

```

While you are editing `/etc/pacman.conf`, check the default mirror that pacman uses to download packages.

Now open up the default mirror in an Internet browser to see if the mirror actually works. If it does work, then do `pacman -Syy` (otherwise pick another working mirror and set it to the pacman default). If you get something similar to the following (notice the 1.0.0.0),

```
ftp://mirror.pacific.net.au/linux/archlinux/extra/os/i686/extra.db.tar.gz
           => '/var/lib/pacman/community.db.tar.gz.part'
Resolving mirror.pacific.net.au... 1.0.0.0

```

then you most likely have this problem. The 1.0.0.0 means it is unable to resolve DNS, so we must add it to `/etc/resolv.conf`.

#### How to fix it

Basically what we need to do is to manually add the DNS servers to our `/etc/resolv.conf` file. The problem is that DHCP automatically deletes and replaces this file on boot, so we need to edit `/etc/conf.d/dhcpcd` and change the flags to stop DHCP from doing this.

When you open `/etc/conf.d/dhcpcd`, you should see something close to the following:

```
DHCPCD_ARGS="-t 30 -h $HOSTNAME"

```

Add the `-R` flag to the arguments, e.g.,

```
DHCPCD_ARGS="-R -t 30 -h $HOSTNAME"

```

**Note:** If you are using [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd) >= 4.0.2, the `-R` flag has been deprecated. Please see the [#For DHCP assigned IP address](#For_DHCP_assigned_IP_address) section for information on how to use a custom `/etc/resolv.conf` file.

Save and close the file; now open `/etc/resolv.conf`. You should see a single nameserver (most likely 10.1.1.1). This is the gateway to your router, which we need to connect to in order to get the DNS servers of your ISP. Paste the IP address into your browser and log in to your router. Go to the DNS section, and you should see an IP address in the Primary DNS Server field; copy it and paste it as a nameserver **ABOVE** the current gateway one.

For example, `/etc/resolv.conf` should look something along the lines of:

```
nameserver 10.1.1.1

```

If my primary DNS server is 211.29.132.12, then change `/etc/resolv.conf` to:

```
nameserver 211.29.132.12
nameserver 10.1.1.1

```

Now restart the network daemon by running `systemctl restart dhcpcd@<interface>` and do `pacman -Syy`. If it syncs correctly with the server, then the problem is solved.

#### More about it

This is the whirlpool forum (Australian ISP community) which talks about and gives the same solution to the problem:

[http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html](http://forums.whirlpool.net.au/forum-replies-archive.cfm/461625.html)

### Check DHCP problem by releasing IP first

Problem may occur when DHCP get wrong IP assignment. For example when two routers are tied together through VPN. The router that is connected to me by VPN may assigning IP address. To fix it. On a console, as root, release IP address:

```
# dhcpcd -k

```

Then request a new one:

```
# dhcpcd

```

Maybe you had to run those two commands many times.

### No eth0 with Atheros AR8161

**Note:** With the 3.10.2-1-ARCH kernel update, the alx ethernet driver module is included in the package.

With the Atheros AR8161 Gigabit Ethernet card, the ethernet connection is not working out-of-the-box (with the installation media of March 2013). The module "alx" needs to be loaded but is not present.

The driver from [compat-wireless](http://linuxwireless.org/en/users/Download/stable/#compat-wireless_stable_releases) (that has become [compat-drives](https://backports.wiki.kernel.org/index.php/Releases) since linux 3.7) need to be installed. The "-u" postfix annotates that Qualcomm have applied a driver under a unified driver.

```
 $ wget [https://www.kernel.org/pub/linux/kernel/projects/backports/2013/03/28/compat-drivers-2013-03-28-5-u.tar.bz2](https://www.kernel.org/pub/linux/kernel/projects/backports/2013/03/28/compat-drivers-2013-03-28-5-u.tar.bz2)
 $ tar xjf compat*
 $ cd compat*
 $ ./scripts/driver-select alx
 $ make
 $ sudo make install
 $ sudo modprobe alx

```

The alx driver has not been added to Linux kernel due to various problems. Compatibility between the different kernel versions has been spotty. For better support follow the [mailing list](http://lists.infradead.org/mailman/listinfo/unified-drivers)and [alx page](http://www.linuxfoundation.org/collaborate/workgroups/networking/alx)for latest working solution for alx.

The driver must be built and installed after every kernel change.

Alternatively you can use the AUR package for [compat drivers](https://aur.archlinux.org/packages/compat-drivers-patched/), which installs many other drivers.

### No eth0 with Atheros AR9485

The ethernet (eth0) for Atheros AR9485 are not working out-of-the-box (with installation media of March 2013). The working solution for this is to install the package [compat-drivers-patched](https://aur.archlinux.org/packages/compat-drivers-patched/) from AUR.

### No carrier / no connection after suspend

After suspend to RAM no connection is found although the network cable is plugged in. This may be caused by PCI power management. What is the output of

```
# ip link show eth0

```

If the line contains "NO-CARRIER" even though there's a cable connected to your eth0 port, it is possible that the device was auto-suspended and the media sense feature doesn't work. To solve this, first you need to find your ethernet controllers PCI address by

```
# lspci

```

This should look similar to this:

```
...
00:19.0 Ethernet controller: Intel Corporation 82577LM Gigabit Network Connection (rev 06)
...

```

So the address is 00:19.0. Now check the PM status of the device by issuing

```
# cat "/sys/bus/pci/devices/0000:00:19.0/power/control"

```

substituting 00:19.0 with the address obtained from lspci. If the output reads "auto", you can try to bring the device out of suspend by

```
# echo on > "/sys/bus/pci/devices/0000:00:19.0/power/control"

```

Don't forget to substitute the address again.

**Note:** This appears to be a bug in kernel 3.8.4.1- (3.8.8.1 is still affected): [Forum discussion.](https://bbs.archlinux.org/viewtopic.php?id=159837&p=2) It also appears a fix is [on the way. (It will be likely fixed in 3.9.)](https://lkml.org/lkml/2013/1/18/147) In the meantime, the above is a suitable workaround.

### PC Pingable by IP but not by hostname?

This issue hunted me for months! Turns out to be a very simple fix IF you are using samba as well. Usually people only start smbd which is enough for network access to work, but does not advocate the pc's name to the router. nmbd is doing that so you should always have:

```
systemctl enable smbd.service
systemctl enable nmbd.service

```

Which makes them run at startup. If you don't want to restart then you can start then right away with:

```
systemctl start smbd.service
systemctl start nmbd.service

```

And that makes the computer available by name on the network.

### Broadcom BCM57780

This Broadcom chipset sometimes does not behave well unless you specify the order of the modules to be loaded. The modules are `broadcom` and `tg3`, the former needing to be loaded first.

These steps should help if your computer has this chipset:

```
$ lspci | grep Ethernet
02:00.0 Ethernet controller: Broadcom Corporation NetLink BCM57780 Gigabit Ethernet PCIe (rev 01)

```

If your wired networking is not functioning in some way or another, try unplugging your cable then doing the following (as root):

```
# modprobe -r tg3
# modprobe broadcom
# modprobe tg3

```

Now plug you network cable in. If this solves your problems you can make this permanent by adding `broadcom` and `tg3` (in this order) to the `MODULES` array in `/etc/mkinitcpio.conf`:

```
MODULES=".. broadcom tg3 .."

```

Then rebuild the initramfs:

```
# mkinitcpio -p linux

```

**Note:** These methods may work for other chipsets, such as BCM57760.