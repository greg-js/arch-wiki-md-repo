**Dica:** Esta é parte de um artigo multi-páginas do "The Beginners' Guide" ("O Guia para Iniciantes"). **[Clique aqui](/index.php/Beginners%27_Guide_(Portugu%C3%AAs) "Beginners' Guide (Português)")** se preferir ler o artigo completo.

## Contents

*   [1 Instalação](#Instala.C3.A7.C3.A3o)
    *   [1.1 Alterar a linguagem](#Alterar_a_linguagem)
    *   [1.2 Estabelecendo conexão com a internet](#Estabelecendo_conex.C3.A3o_com_a_internet)
        *   [1.2.1 Rede Cabeada](#Rede_Cabeada)
        *   [1.2.2 Wireless](#Wireless)
        *   [1.2.3 Proxy](#Proxy)
            *   [1.2.3.1 Configurando o pacman](#Configurando_o_pacman)
            *   [1.2.3.2 Configurando o wget](#Configurando_o_wget)
    *   [1.3 Preparando os Discos](#Preparando_os_Discos)
        *   [1.3.1 Exemplo](#Exemplo)
    *   [1.4 Montando as Partições](#Montando_as_Parti.C3.A7.C3.B5es)
    *   [1.5 Selecionando um repositório](#Selecionando_um_reposit.C3.B3rio)
    *   [1.6 Instalando o sistema Base](#Instalando_o_sistema_Base)
    *   [1.7 Crie um FSTAB](#Crie_um_FSTAB)
    *   [1.8 Chroot e configuração do sistema base](#Chroot_e_configura.C3.A7.C3.A3o_do_sistema_base)
        *   [1.8.1 Localização(locale)](#Localiza.C3.A7.C3.A3o.28locale.29)
        *   [1.8.2 Fontes de console e Mapa de teclado](#Fontes_de_console_e_Mapa_de_teclado)
        *   [1.8.3 Fuso Horário](#Fuso_Hor.C3.A1rio)
        *   [1.8.4 Relógio do Hardware](#Rel.C3.B3gio_do_Hardware)
        *   [1.8.5 Módulos do Kernel](#M.C3.B3dulos_do_Kernel)
        *   [1.8.6 Hostname](#Hostname)
    *   [1.9 Configure a rede](#Configure_a_rede)
        *   [1.9.1 Rede Cabeada](#Rede_Cabeada_2)
        *   [1.9.2 Rede sem fio (Wireless)](#Rede_sem_fio_.28Wireless.29)
    *   [1.10 Configurar o pacman](#Configurar_o_pacman)
    *   [1.11 Criar um ambiente ramdisk inicial](#Criar_um_ambiente_ramdisk_inicial)
    *   [1.12 Definir a senha de root e adicionar um usuário regular](#Definir_a_senha_de_root_e_adicionar_um_usu.C3.A1rio_regular)
    *   [1.13 Instalar e configurar o gerenciador de boot](#Instalar_e_configurar_o_gerenciador_de_boot)
        *   [1.13.1 Para Placas-mãe BIOS](#Para_Placas-m.C3.A3e_BIOS)
            *   [1.13.1.1 Syslinux](#Syslinux)
            *   [1.13.1.2 GRUB](#GRUB)
        *   [1.13.2 Placas-mãe UEFI](#Placas-m.C3.A3e_UEFI)
            *   [1.13.2.1 EFISTUB](#EFISTUB)
            *   [1.13.2.2 GRUB](#GRUB_2)
    *   [1.14 Atualizar o sistema](#Atualizar_o_sistema)
    *   [1.15 Desmontar as partições e reiniciar](#Desmontar_as_parti.C3.A7.C3.B5es_e_reiniciar)

## Instalação

A partir deste momento, você está automaticamente logado em uma shell como usuário root.

**Nota:** O Framework de instalação do Arch Linux foi descotinuado, portanto, o procedimento de executar o script /arch/setup não funcionará.

### Alterar a linguagem

**Dica:** Este passo é opcional para a maioria dos usuários. Útil apenas se desejas o sistema em sua linguagem nativa, editar arquivos de configuração adicionando caracteres especiais, ou configurar senhas de Wi-Fi com tais caracteres ou receber mensagens do sistema na sua linguagem.

Por padrão, a linguagem do teclado é a `us`. Para utilizadores do Brasil:

```
# loadkeys *br-abnt2*

```

Para utilizadores de outras comunidades lusófonas:

```
# loadkeys pt-latin9

```

A fonte de letra do console também pode ser alterada, pois a maioria das linguagens utiliza o padrão de 26 letras. Nesses casos, alguns caracteres podem aparecer na tela como quadrados brancos ou outros símbolos. Note que o comando abaixo é case-sensitive, portanto, digite *exatamente* da forma como está escrito:

```
# setfont Lat2-Terminus16

```

Por padrão, a linguagem da instalação é o Inglês(US). Para alterar a linguagem durante o processo de instalação, basta remover o `#` na [localização](http://www.greendesktiny.com/support/knowledgebase_detail.php?ref=EUH-483) desejada no arquivo `/etc/locale.gen`, junto com a entrada em inglês. Priorize a escolha da entrada `UTF-8`.

Pressione `Ctrl+X` para sair, e quando perguntado para salvar as alterações, pressione `Y` seguido de `Enter` para sobrescrever o arquivo.

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
pt_BR.UTF-8 UTF-8
```

```
# locale-gen
# export LANG=pt_BR.UTF-8 

```

ou, para configurar em Português de Portugal:

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
pt_PT.UTF-8 UTF-8
```

```
# locale-gen
# export pt_PT.UTF-8 UTF-8

```

Lembre-se, `Alt Esquerdo + Shift Esquerdo` ativa e desativa um mapa de teclado.

### Estabelecendo conexão com a internet

O serviço `dhcpcd` inicia automaticamente em tempo de inicialização, e tentará iniciar uma conexão cabeada se disponível. Tente pingar um site para verificar a disponibilidade.

 `# ping -c 3 www.google.com` 
```
PING www.l.google.com (74.125.132.105) 56(84) bytes of data.
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=1 ttl=50 time=17.0 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=2 ttl=50 time=18.2 ms
64 bytes from wb-in-f105.1e100.net (74.125.132.105): icmp_req=3 ttl=50 time=16.6 ms

--- www.l.google.com ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 16.660/17.320/18.254/0.678 ms
```

Caso você receba o erro `ping: unknown host`, você deverá configurar a rede manualmente, como descrito abaixo.

Caso contrário, vá para o tópico [Preparando os Discos](#Preparando_os_Discos).

#### Rede Cabeada

Siga o seguinte procedimento para configurar sua conexão cabeada com um endereço IP estático.

Caso o seu computador esteja conectado a uma rede Ethernet você possuirá uma interface chamada `enpXsX` (onde *"X"* corresponde a um número). Você precisa conhecer as seguintes informações (que você pode conseguir com seu administrador de redes):

*   Endereço IP estático.
*   Máscara de rede.
*   Endereço do Gateway
*   Endereço do DNS
*   Nome do domínio(a menos que esteja em uma LAN local, onde pode ignorar tal informação).

Para ativar uma interface de rede como a `enp5s0`, por exemplo:

```
# ip link set enp5s0 up

```

Adicione um endereço:

```
# ip addr add <endereco-ip>/<mascara-de-subrede> dev <interface>

```

Exemplo:

```
# ip addr add 192.168.1.2/24 dev enp5s0

```

Para maiores opções, execute `man ip`.

Adicione o seu gateway da seguinte forma, substituindo o endereço IP pelo do seu gateway em questão:

```
# ip route add default via <endereco-ip>

```

Exemplo:

```
# ip route add default via 192.168.1.1

```

Edite o arquivo `resolv.conf`, substituindo no parametro "nameserver" os endereços IP dos DNS's disponíveis, e o valor do seu domínio no parâmetro "search".

 `# nano /etc/resolv.conf` 
```
nameserver 61.23.173.5
nameserver 61.95.849.8
search example.com
```

**Nota:** Apenas três endereços `nameserver` podem ser incluídos neste arquivo.

A partir daqui, você deve ter acesso a rede cabeada. Caso contrário, dê uma verificada na página [Configuring Network (Português)](/index.php/Configuring_Network_(Portugu%C3%AAs) "Configuring Network (Português)").

#### Wireless

Siga este procedimento caso você precise de conectividade (Wi-Fi) durante o processo de instalação.

Os drivers e utilitários para conexão sem fio agora estão disponíveis na mídia de instalação. Um bom conhecimento do seu hardware sem fio será de suma importância para obter sucesso na configuração. Note que seguindo o procedimento deste passo-a-passo habilitará seu hardware *durante a utilização do sistema live* ou *executando em determinado processo da instalação*. Estes passos precisam ser repetidos após um reboot no sistema.

Note também que estes passos são opcionais, pois **se a conexão sem fio é desnecessária ao processo de instalação, estas configurações podem ser executadas em um período posterior.**

**Nota:** Os exemplos a seguir usam a nomenclatura `wlpXsX` (onde *"X"* corresponde a um número) para a interface de rede e `linksys` para a ESSID. Lembre de alterar estes valores de acordo com a sua configuração.

O procedimento básico será:

*   (opcional) Identificar a sua interface wireless:

```
# lspci | grep -i net

```

Ou, se utilizando uma placa externa (usb):

```
# lsusb

```

*   Certifique-se de que o udev carregou o driver apropriado, e que uma interface utilizável foi criada, através do comando `iwconfig`:

**Nota:** Caso você não visualize uma saída de tela similar a esta, sua placa wireless não foi carregada. Neste caso, você deverá carregar o módulo do driver por sua conta. Veja [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") para informações mais detalhadas.
 `# iwconfig` 
```
lo no wireless extensions.
enp5s0 no wireless extensions.
wlp9s0   unassociated  ESSID:""
         Mode:Managed  Channel=0  Access Point: Not-Associated
         Bit Rate:0 kb/s   Tx-Power=20 dBm   Sensitivity=8/0
         Retry limit:7   RTS thr:off   Fragment thr:off
         Power Management:off
         Link Quality:0  Signal level:0  Noise level:0
         Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
         Tx excessive retries:0  Invalid misc:0   Missed beacon:0
```

Neste exemplo, `wlp9s0` é a interface disponível.

*   Para levantar a interface:

```
# ip link set wlp9s0 up

```

Uma pequena porcentagem dos dispositivos sem fio também necessitam de um firmware para o driver correspondente. Caso sua interface precise de um, o "erro comum" que pode acontecer ao levantar a interface é o seguinte:

 `# ip link set wlp9s0 up`  `SIOCSIFFLAGS: No such file or directory` 

Caso tenha dúvidas, utilize o `dmesg` para buscar por informações no log de kernel e encontrar qual o possível firmware a ser utilizado.

Exemplo de saída de um dispositivo da Intel, requisitando o firmware durante o boot:

 `# dmesg | grep firmware`  `firmware: requesting iwlwifi-5000-1.ucode` 

Caso não haja saída, pode ser concluído que nenhuma firmware é necessária para a sua placa.

**Warning:** Pacotes de firmware de dispositivos sem fio são pré-instalados dentro de `/usr/lib/firmware` no ambiente de instalação(liveCD ou liveUSB), **porém, devem ser explicitamente instalados ao seu sistema para serem funcionais após o reiniciar da instalação!**. A instalação de pacotes será abordada mais tarde neste guia. Certifique-se da instalação de ambos, o módulo e a firmware antes de reiniciar! Veja [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") caso esteja incerto dos requisitos de firmware correspondentes ao seu sistema em particular.

Após, utilize o utilitário wifi-menu para conectar a rede:

```
# wifi-menu wlp9s0

```

A partir de agora, você já deve ter uma conexão de internet funcionando. Caso contrário, verifique a página [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

#### Proxy

Para que seja possível instalar e atualizar o Arch Linux através de um servidor proxy autenticado é preciso alterar a maneira como o [pacman](https://wiki.archlinux.org/index.php/Pacman_%28Portugu%C3%AAs%29) baixa os pacotes, de modo que ele utilize o [wget](/index.php/Wget "Wget") para isso.

##### Configurando o pacman

Edite o arquivo `/etc/pacman.conf` e apague o símbolo `#` da linha *"XferCommand = /usr/bin/wget"*:

 `# nano /etc/pacman.conf`  `XferCommand = /usr/bin/wget --passive-ftp -c -O %o %u` 

##### Configurando o wget

Agora será preciso editar o arquivo `/etc/wgetrc` com as informações do seu proxy, apagando o símbolo `#` do início das linhas e alterando com a sua configuração de proxy:

 `# nano /etc/wgetrc` 
```
https_proxy = http://usuario:senha@ipdoproxy:portadoproxy/
http_proxy = http://usuario:senha@ipdoproxy:portadoproxy/
ftp_proxy = http://usuario:senha@ipdoproxy:portadoproxy/

```

Mais informações sobre configuração de proxy podem ser encontradas em: [Proxy settings](/index.php/Proxy_settings "Proxy settings").

### Preparando os Discos

**Warning:** O particionamento pode causar destruição de dados. Recomendamos **fortemente** que efetue um backup de qualquer informação importante antes de proceder com este passo.

Para completos iniciantes, encorajamos ferramentas gráficas de particionamento. O [GParted](http://gparted.sourceforge.net/download.php) é um bom exemplo de uma distribuição Linux live, assim como [Parted Magic](https://en.wikipedia.org/wiki/Parted_Magic "wikipedia:Parted Magic"), etc. Um dispositivo deve ser primeiramente particionado e então as partições serão formatadas com um [sistema de arquivos](/index.php/File_systems "File systems") antes de reiniciar.

Caso já tenha executado este passo, prossiga para [Montando as partições](#Montando_as_Parti.C3.A7.C3.B5es). Caso contrário, siga o exemplo:

#### Exemplo

A mídia de instalação do Arch Linux provê as seguinter ferramentas de particionamento:

*   [gdisk](https://en.wikipedia.org/wiki/gdisk "wikipedia:gdisk") – Suporta apenas tabelas de partição [GPT](/index.php/GPT "GPT").

*   [cfdisk](https://en.wikipedia.org/wiki/cfdisk "wikipedia:cfdisk") – Suporta apenas tabelas de partição [MBR](/index.php/MBR "MBR").

*   [parted](https://en.wikipedia.org/wiki/parted "wikipedia:parted") – Suporta ambas.

Este exemplo utiliza o **cfdisk**, mas ele pode ser facilmente adaptado para o **gdisk**, que permite o particionamento em tabelas do tipo GPT.

**Notas sobre o boot [UEFI](/index.php/UEFI "UEFI"):**

*   Se você possui uma placa-mãe com suporte a UEFI, você precisará criar uma partição [UEFI](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface") extra.
*   É recomendado sempre usar GPT para boot UEFI, pois algumas firmwares UEFI não permitem inicialização EFI-MBR.

**Notas sobre o particionamento [GPT](/index.php/GPT "GPT"):**

*   Se você não está configurando dual boot com o Windows, utilize GPT ao invés de MBR. Leia a lista de vantagens da [GPT](/index.php/GPT "GPT").
*   Se você possui uma placa mãe com BIOS(ou planeja iniciar em modo de compatibilidade BIOS) e deseja configurar o GRUP em um driver particionado via GPT, você precisará criar uma [Partiçaõ de boot BIOS](/index.php/GRUB#GPT_specific_instructions "GRUB") de 2 MiB. O Syslinux não precisa de uma.

**Nota:** Caso esteja instalando o Arch de um driver USB, veja [Installing Arch Linux on a USB key](/index.php/Installing_Arch_Linux_on_a_USB_key "Installing Arch Linux on a USB key").

```
# cfdisk /dev/sda

```

Este exemplo mostrará um sistema que terá 15 GB de partição raíz (`/`), 1GB de partição `swap`, e o espaço remanescente será destinado ao `/home`.

Vale enfatizar que particionamento de disco trata-se de gosto pessoal, e que este exemplo existe para propósitos ilustrativos. Veja [Partitioning](/index.php/Partitioning "Partitioning").

**Raíz:**

*   Escolha Nova (ou pressione `N`) - `Enter` para Primaria - digite "15360" - `Enter` para "No início" - `Enter` para Bootável.

**Swap:**

*   Pressione seta para baixo para mover a seleção para o "espaço livre" no disco rígido.
*   Escolha Nova (ou pressione `N`) - `Enter` para Primaria - digite "1024" – `Enter` para "No início".
*   Escolha o tipo (ou pressione `T`) – pressione qualquer tecla para rolar a lista para baixo - `Enter` para 82.

**Home:**

*   Pressione seta para baixo para mover a seleção para o "espaço livre" no disco rígido.
*   Escolha Nova (ou pressione `N`) – `Enter` para Primaria - `Enter` para usar o restante do espaço em disco.

O resultado do particionamento ficara parecido com este:

```
Name    Flags     Part Type    FS Type          [Label]       Size (MB)
-----------------------------------------------------------------------
sda1    Boot       Primary     Linux                             15360
sda2               Primary     Linux swap / Solaris              1024
sda3               Primary     Linux                             133000*

```

Verifique novamente, e se certifique que você está contente com os tamanhos das partições assim como o layout delas antes de continuar.

Se quiser reiniciar o processo, você pode simplesmente selecionar "Sair" (ou pressionar `Q`) para sair do particionador sem salvar quaisquer alterações feitas no disco. Depois, basta executar o cfdisk novamente.

Se tiver satisfeito, selecione Gravar (ou pressione `Shift+W`) para finalizar a gravação da tabela de partições para o disco. Digite "Sim"(yes) e selecione Sair (ou pressionar `Q`) para sair do cfdisk.

Particionar não é o bastante; As partições precisam de um [File Systems](/index.php/File_Systems "File Systems"). Para formatar as partições com um sistema de arquivos ext4:

**Warning:** Verifique e "re-Verifique" se é realmente a partição `/dev/sda1` que você deseja formatar. Pode mudar de caso para caso.

```
# mkfs.ext4 /dev/sda1
# mkfs.ext4 /dev/sda3

```

E para formatar e ativar a partição de swap:

```
# mkswap /dev/sda2
# swapon /dev/sda2

```

### Montando as Partições

Cada partição é identificada por um sufixo numeral. Por exemplo, `sda1` especifica a primeira partição do primeiro driver, enquanto `sda` designa o disco por completo.

Para ver o layout de particionamento atual:

```
# lsblk /dev/sda

```

Preste atenção na ordem de montagem, pois ela é importante.

Primeiro, monte a partição raíz em `/mnt`. Seguindo o exemplo abaixo (em seu sistema, pode ser diferente) seria algo como:

```
# mount /dev/sda1 /mnt

```

Monte então a partição destinada ao `/home` e outras separadas para o `/boot`, `/var`, etc, caso desejar:

```
# mkdir /mnt/home
# mount /dev/sda3 /mnt/home

```

No caso da partição `/boot` ser separada:

```
# mkdir /mnt/boot
# mount /dev/sda*X* /mnt/boot

```

Se a sua placa-mãe possuir suporte a UEFI, monte a partição da seguinte maneira:

```
# mkdir /mnt/boot/efi
# mount /dev/sda*X* /mnt/boot/efi

```

### Selecionando um repositório

Antes de instalar, você pode desejar configurar seu arquivo `mirrorlist` para apontar pra um repositório de seu interesse. Uma cópia deste arquivo será instalado no seu sistema através do `pacstrap`

 `# nano /etc/pacman.d/mirrorlist` 
```
##
## Arch Linux repository mirrorlist
## Sorted by mirror score from mirror status page
## Generated on 2012-MM-DD
##

Server = http://mirror.example.xyz/archlinux/$repo/os/$arch
...
```

*   `Alt+6` para copiar a linha `Server`.
*   `PageUp` para subir no arquivo.
*   `Ctrl+U` para colar a linha copiada no topo do arquivo.
*   `Ctrl+X` para sair, e quando lhe for perguntado se deseja salvar as alterações, pressione `Y` e `Enter` para sobrescrever o arquivo

Se desejar, você pode configurar para que este seja o *único* repositório disponível, excluindo todo o resto (usando `Ctrl+K`), porém, é uma boa ideia ter mais de um repositório disponível, caso um deles esteja offline.

**Dica:**

*   Use o [Mirrorlist Generator](https://www.archlinux.org/mirrorlist/) para obter uma lista atualizada dos repositórios de seu país. Repositórios HTTP são mais rápidos que FTP, devido a um conceito chamado [keepalive](https://en.wikipedia.org/wiki/Keepalive "wikipedia:Keepalive"). Via FTP, o pacman precisa enviar um sinal a cada momento que um pacote é baixando, resultando em uma pequena pausa. Para outras formas de gerar repositórios, veja [organizando repositórios](/index.php/Mirrors#Sorting_mirrors "Mirrors") e [Reflector](/index.php/Reflector "Reflector").
*   [Arch Linux MirrorStatus](https://archlinux.org/mirrors/status/) reporta diversos aspectos sobre os repositórios como problemas de rede, problemas de coleta de dados, última data de sincronia, etc.

**Nota:**

*   Sempre que mudar sua lista de repositoŕios, lembre-se de forçar o pacman a atualizar todas as listas de pacotes através de um `pacman -Syy`. Esta ação é considerada uma boa prática e pode evitar dores de cabeça. Veja [Mirrors](/index.php/Mirrors "Mirrors") para maiores informações.
*   Se estiver usando uma mídia de instalação antiga, suas listas de repositórios podem estar desatualizadas, podendo causar problemas na atualização relacionadas ao [FS#22510](https://bugs.archlinux.org/task/22510). Por isto, utilize sempre a última mídia disponível como descrito acima.
*   Alguns problemas foram reportados nos [fórums do Arch Linux](https://bbs.archlinux.org/) relacionados a rede, impedindo o pacman a atualizar/sincronizar repositórios(veja [[1]](https://bbs.archlinux.org/viewtopic.php?id=68944) e [[2]](https://bbs.archlinux.org/viewtopic.php?id=65728)). Quando instalando o Arch Linux nativamente, estes problemas são contornados substituindo o "baixador de arquivos" do pacman por uma alternativa(veja [Aumento de performance do Pacman](/index.php/Improve_pacman_performance "Improve pacman performance") para maiores detalhes). Quando instalar o Arch Linux como hóspede no [VirtualBox]], este problema pode ocorrer ao usar uma interface do tipo "Host interface" ao invés de "NAT" nas configurações desta máquina.

### Instalando o sistema Base

O sistema base é instalado usando o script [pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in).

```
# pacstrap /mnt base base-devel

```

**Nota:** Caso o pacman falhe ao verificar os pacotes, verifique a data/hora do seu sistema. Se a data for inválida (exemplo, ano 2010), algumas chaves serão consideradas expiradas(ou inválidas), e verificações de assinatura dos pacotes falharão, junto com a interrupção da instalação. Certifique-se de corrigir o horário do sistema, fazendo isto manualmente ou através do cliente [ntp](https://www.archlinux.org/packages/?name=ntp), e tente rodar o pacstrap novamente. Veja o artigo [tempo](/index.php/Time "Time") para maiores detalhes sobre correção da data do sistema.

*   [base](https://www.archlinux.org/groups/x86_64/base/): Softwares que fazem parte do repositório [core], fazendo parte do ambiente mínimo necessário.

*   [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/): Ferramentas extras fora do [core] como `make` e `automake`. A maioria dos iniciantes irá instalar este grupo, que será necessário para aumentar o sistema no futuro. O *base-devel* é um grupo necessário para a instalação de pacotes vindos do [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

Isto lhe dará um ambiente Arch básico. Outros pacotes podem ser instalados mais tarde através do [pacman](/index.php/Pacman "Pacman").

**Nota:** Se você está instalando o Arch Linux através de um servidor Proxy é importante instalar o pacote [wget](https://www.archlinux.org/packages/?name=wget), além do *base* e o *base-devel*, através do `pacstrap`.

### Crie um FSTAB

Crie um arquivo [fstab](/index.php/Fstab "Fstab") com o comando `genfstab` utilizando as opções `-U`, para UUIDs, e `-L` para labels (se preferir). É interessante verificar esta informação antes de continuar:

**Nota:** Se erros forem encontrados durante a execução do genfstab, **não** rode o comando novamente; apenas edite o arquivo `/etc/fstab`.

```
# genfstab -p /mnt >> /mnt/etc/fstab
# nano /mnt/etc/fstab

```

Apenas a partição raíz (`/`) precisa de `1` no último campo. O restante, deve ter `2` ou `0` (veja [definições do fstab](/index.php/Fstab#Field_definitions "Fstab")).

Adicionalmente, `data=ordered` deve ser removido. Esta opção é usada automaticamente você definindo-a ou não, então, pode ser removida para manter a "clareza" do arquivo fstab.

### Chroot e configuração do sistema base

Depois, faremos um [chroot](/index.php/Chroot "Chroot") ao nosso novo sistema recém instalado:

```
# arch-chroot /mnt

```

Neste estágio da instalação, você configurará arquivos primários na base do seu Arch Linux. Estes podem ser criados caso existam ou não, ou editados caso deseje mudar a configuração padrão.

Entender todos os passos descritos é de suma importancia para garantir a configuração perfeita do sistema.

#### Localização(locale)

Localizações utilizadas pela **glibc** e outros programas e bibliotecas com tal capacidade para renderizar texto, mostrarão de forma correta opções regionais monetárias, de formato de data, de idiossincrasia, e outros padrões específicos de cada localidade.

Dois arquivos precisam ser editados: `locale.gen` e `locale.conf`.

*   O arquivo `locale.gen` é limpo por padrão(todas linhas comentadas) e você precisará remover o `#` das linhas desejadas. Você deverá descomentar mais linhas que apenas o Inglês (US), assim que escolher a codificação `UTF-8`: encoding:

 `# nano /etc/locale.gen` 
```
en_US.UTF-8 UTF-8
pt_BR.UTF-8 UTF-8
```

```
# locale-gen

```

Este comando irá rodar em cada atualização de **glib**, gerando novamente todas as localizações configuradas no `/etc/locale.gen`.

*   O arquivo `locale.conf` não existe por padrão. Configurar a variável `LANG` será o suficiente. Esta variável será utilizada como padrão por outras variáveis

```
# echo LANG=pt_BR.UTF-8 > /etc/locale.conf
# export LANG=pt_BR.UTF-8

```

Para usar outras variáveis do tipo `LC_*`, primeiro rode o comando `locale` para verificar as opções disponíveis. Um exemplo avançado pode ser encontrado [aqui](/index.php/Locale#Setting_system-wide_locale "Locale").

**Warning:** O uso da variável `LC_ALL` é desencorajado por sobrepor **tudo**.

#### Fontes de console e Mapa de teclado

Se você alterou o mapa do teclado no [inicio](#Instala.C3.A7.C3.A3o) do processo de instalação, recarregue tal configuração novamente pois seu ambiente mudou. Exemplo:

```
# loadkeys *br-abnt2*
# setfont Lat2-Terminus16

```

Para utilizadores de outras comunidades lusófonas:

```
# loadkeys *pt-latin9*
# setfont Lat2-Terminus16

```

Para que tais configurações persistam após um reboot, edite o arquivo `vconsole.conf`:

 `# nano /etc/vconsole.conf` 
```
KEYMAP=br-abnt2
FONT=Lat2-Terminus16
FONT_MAP=
```

*   `KEYMAP` – Tenha em mente que esta configuração é válida apenas para as suas TTYs, e não para gerenciadores gráficou ou seu Xorg.

*   `FONT` – Fontes disponíveis estão localizadas em `/usr/share/kbd/consolefonts/`. A fonte padrão é livre de falhas, porém, pode fazer com que caracteres estrangeiros apareçam como quadrados ou outros símbolos. É recomandado a fonte `Lat2-Terminus16` pois de acordo com o `/usr/share/kbd/consolefonts/README.Lat2-Terminus16`, suporta "todos as linguagens l10".

*   `FONT_MAP` – Mapa de console a ser carregado durante o boot. Leia `man setfont`. O padrão(em branco) é seguro

Veja See [fontes de console](/index.php/Fonts#Console_fonts "Fonts") e `man vconsole.conf` para maiores informações.

#### Fuso Horário

Os fusos horário disponíveis podem ser encontrados nos diretórios `/usr/share/zoneinfo/<Zona>/<SubZona>`

Para visualizar uma <Zona> disponível, liste o conteúdo de `/usr/share/zoneinfo/`:

```
# ls /usr/share/zoneinfo/

```

De forma similar, a informação de uma <SubZona> pode ser obtida:

```
# ls /usr/share/zoneinfo/Europe

```

Crie um link simbólico para `/etc/localtime` com origem no seu fuso horário seguindo o padrão `/usr/share/zoneinfo/<Zona>/<SubZona>` .

**Exemplo:**

```
# ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

```

#### Relógio do Hardware

Defina o modo do relógio de hardware de modo uniforme entre seus sistemas operacionais. Caso contrário, eles podem substituir o relógio do hardware e provocar mudanças de tempo.

Você pode gerar o arquivo `/etc/adjtime` automaticamente, usando um dos seguintes comandos:

*   **UTC** (recomendado)

**Nota:** A utilização [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time "wikipedia:Coordinated Universal Time") para o relógio do hardware não significa que o software irá exibir hora em UTC.

	 `# hwclock --systohc --utc` 

*   **localtime** (desencorajante; usado por padrão no Windows)

**Warning:** Usando *localtime* pode levar a vários bugs conhecidos e incorrigíveis. No entanto, não há planos para largar suporte para *localtime*.

	 `# hwclock --systohc --localtime` 

Se você tem (ou pensando em ter) uma configuração dual boot com o Windows:

*   Recomendado: Definir tanto Arch Linux e Windows para usar UTC. Um rápido [registro fixo](/index.php/Time#UTC_in_Windows "Time") é necessário. Além disso, certifique-se de impedir o Windows de sincronizar o tempo on-line, porque o relógio de hardware será o padrão de volta para o *localtime*. Se você quiser tal funcionalidade (NTP sync), você deve usar [ntpd](/index.php/Ntpd "Ntpd") em sua instalação do Arch Linux em seu lugar.

*   Não recomendado: Defina o Arch Linux para o *localtime* e desativar todos os serviços relacionados com o tempo, como `ntpd.service`. Isso vai deixar o Windows cuidar das correções do relógio do hardware e você precisa se lembrar de inicializar o Windows, pelo menos, duas vezes por ano (na Primavera e no Outono) quando [DST](https://en.wikipedia.org/wiki/Daylight_savings_time "wikipedia:Daylight savings time") retrocede. Então, por favor, não pergunte no fórum por que o relógio é de uma hora atrás ou à frente, se você costuma passar dias ou semanas sem entrar no Windows.

#### Módulos do Kernel

**Dica:** Este é apenas um exemplo, você não precisa defini-lo. Todos os módulos necessários são carregados automaticamente pelo udev, assim você raramente vai precisar adicionar algo aqui. Apenas adicionar módulos que você sabe que estão faltando.

Para que os módulos do kernel carregue durante a inicialização, coloque um `*.conf` no arquivo `/etc/modules-load.d/`, com um nome baseado no programa que vai usá-lo.

 `# nano /etc/modules-load.d/virtio-net.conf` 
```
# Load 'virtio-net.ko' at boot.

virtio-net
```

Se houver mais módulos para carregar por `*.conf`, os nomes dos módulos podem ser separadas por novas linhas. Um bom exemplo são as [Guest Additions in VirtualBox](/index.php/VirtualBox#Arch_Linux_guests "VirtualBox").

Linhas vazias e começando com `#` ou `;` são ignorados.

#### Hostname

Adicione seu *hostname* em `/etc/hostname`:

```
# echo **myhostname** > /etc/hostname

```

Configure ao seu gosto (ex. *arch*). Este é o nome do seu computador. E adicione para `/etc/hosts`, assim:

**Warning:** Este formato, incluindo `localhost` e seu hostname atual, é necessário para a compatibilidade do programa. Erros nessas entradas podem causar mau desempenho da rede e/ou determinados programas podem abrir muito lentamente, ou não funcionar como ao todo.
 `# nano /etc/hosts` 
```
127.0.0.1   **myhostname** localhost
::1         **myhostname** localhost

#192.168.1.100 **myhostname**.domain.org **myhostname**   #Uncomment se você usar um IP estático, remover este comentário.
```

**Nota:** `127.0.0.1` e `::1` são os endereços IPv4 e IPv6 de local [loopback](https://en.wikipedia.org/wiki/localhost "wikipedia:localhost") interface de rede.

**Dica:** Por conveniência, você pode também usar `/etc/hosts` apelidos para hosts em sua rede, e/ou na web.
```
192.168.1.90 media
192.168.1.88 data

```
O exemplo acima permitirá o acesso a um servidor de mídia e dados em sua rede pelo nome e sem a necessidade de digitar os seus respectivos endereços IP.

### Configure a rede

Você precisa configurar a rede novamente, mas desta vez para o seu ambiente recém-instalado. O procedimento e as condições prévias são muito semelhantes ao descrito no [início](#Establish_an_internet_connection), exceto que vamos torná-lo persistente e executar automaticamente na inicialização.

**Nota:** Para mais informações detalhadas sobre a configuração de rede, visite [Configuring Network](/index.php/Configuring_Network "Configuring Network") e [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

#### Rede Cabeada

	IP Dinâmico

Se você só usa uma única conexão de rede fixa cabeada, você não precisa de um serviço de gerenciamento de rede e pode simplesmente habilitar o serviço `dhcpcd`:

```
# systemctl enable dhcpcd@.service

```

Alternativamente, você pode usar [netcfg](https://aur.archlinux.org/packages/netcfg/)'s `net-auto-wired`, que normalmente lidá com conexões dinâmicas para novas redes:

```
# pacman -S netcfg ifplugd
# cd /etc/network.d
# ln -s examples/ethernet-dhcp .
# systemctl enable net-auto-wired.service

```

	IP Estático

Instale [netcfg](https://aur.archlinux.org/packages/netcfg/) e [ifplugd](https://www.archlinux.org/packages/?name=ifplugd), que são necessários para o `net-auto-wired`:

```
# pacman -S netcfg ifplugd

```

Copie uma amostra do perfil `/etc/network.d/examples` para `/etc/network.d`:

```
# cd /etc/network.d
# cp examples/ethernet-static .

```

Edite o perfil, conforme necessário:

```
# nano ethernet-static

```

Habilite o serviço `net-auto-wired`:

```
# systemctl enable net-auto-wired.service

```

#### Rede sem fio (Wireless)

Você vai precisar instalar outros programas para configurar e gerenciar perfis de rede sem fio, tais como [netcf](/index.php?title=Netcf&action=edit&redlink=1 "Netcf (page does not exist)").

[NetworkManager](/index.php/NetworkManager "NetworkManager") e [Wicd](/index.php/Wicd "Wicd") que são outras alternativas populares.

*   Instale os pacotes necessários:

```
# pacman -S wireless_tools wpa_supplicant wpa_actiond netcf dialog

```

Se o seu adaptador sem fio requer um firmware (como descrito acima na seção [Establish an internet connection](#Wireless) e também [here](/index.php/Wireless_network_configuration#Drivers_and_firmware "Wireless network configuration")), instale o pacote que contém o seu firmware. por exemplo:

```
# pacman -S zd1211-firmware

```

*   Conecte à rede com `wifi-menu` (opcionalmente verificar o nome da interface com `ip link`, mas geralmente é `wlpXsX`) (onde "*X*" corresponde a um número), que irá gerar um arquivo de perfil em `/etc/netctl/` nomeado após o SSID. Há também modelos disponíveis no `/etc/netctl/examples/` para configuração manual.

```
# wifi-menu

```

*   Habilite o serviço `netctl-auto`, que vai ligar a redes conhecidas e normalmente lidar com roaming e desconectadas:

```
# systemctl enable netctl-auto@<interface>.service

```

*   Certifique-se de que a interface sem fio está correta (geralmente `wlpXsX`) (onde "*X*" corresponde a um número).

### Configurar o pacman

Pacman é o gerenciador de pacotes do Arch Linux. Seu nome vem de **pac**kage **man**ager. É altamente recomendável estudar e aprender a usá-lo. Leia `man pacman`, deem uma olhada no artigo [pacman](/index.php/Pacman "Pacman"), ou veja o artigo [Pacman Rosetta](/index.php/Pacman_Rosetta "Pacman Rosetta") para uma comparação com outros gerenciadores de pacotes populares.

Para seleções de repositório e opções pacman, edite `pacman.conf`:

**Nota:** Ao escolher um repositório, certifique-se de descomentar tanto as linhas de cabeçalho `[*repo_name*]`, bem como as linhas `Include`. Não fazer isso resultará no repositório escolhido seja omitido! Este é um erro muito comum.

```
# nano /etc/pacman.conf

```

A maioria das pessoas vai querer usar `[core]`, `[extra]` e `[community]`.

Se você instalou o Arch Linux x86_64, é recomendado que você habilite o repositório `[multilib]`, bem (para ser capaz de executar aplicações de 64 bits como de 32 bits):

```
[multilib]
Include = /etc/pacman.d/mirrorlist

```

Veja [Official repositories](/index.php/Official_repositories "Official repositories") para mais informações, incluindo detalhes sobre a finalidade de cada repositório.

Para software indisponível através do pacman (que não esteja nos repositórios oficiais), ver [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository").

### Criar um ambiente ramdisk inicial

**Dica:** A maioria dos usuários pode pular esse passo e usar os padrões previstos em `mkinitcpio.conf`. A imagem initramfs (do diretório `/boot`) já foi gerado com base neste arquivo quando o [linux](https://www.archlinux.org/packages/?name=linux) do pacote (the kernel Linux) foi instalado anteriormente com `pacstrap`.

Aqui você precisa para definir o direito [hooks](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") se a raiz é em um drive USB, se você usar o RAID, LVM, ou se `/usr` está em uma partição separada.

Edite `/etc/mkinitcpio.conf` como necessário e voltar a gerar a imagem initramfs com:

```
# mkinitcpio -p linux

```

### Definir a senha de root e adicionar um usuário regular

Definir a senha de root com:

```
# passwd

```

**Warning:** Linux é um sistema operacional multi-usuário. Você não deve executar tarefas diárias usando a conta root. É considerada uma prática muito pobre e pode ser extremamente perigoso. A conta root somente deve ser usada para tarefas administrativas.

Em seguida, adicione uma conta de usuário normal. Para uma forma mais interativa, você pode usar `adduser`. No entanto, a seguir é a forma não-interativo. O usuário *archie* é apenas um exemplo.

```
# useradd -m -g users -s /bin/bash *archie*
# passwd *archie*

```

Se você quiser começar de novo, use `userdel`. A opção `-r` irá remover o diretório home do usuário e seu conteúdo, juntamente com as configurações do usuário (as chamadas "dot" arquivos).

```
# userdel -r *archie*

```

Para mais informações, leia [Users and groups](/index.php/Users_and_groups "Users and groups").

### Instalar e configurar o gerenciador de boot

#### Para Placas-mãe BIOS

Para sistemas BIOS existem três carregadores de boot(bootloaders) - Syslinux, GRUB e [LILO](/index.php/LILO "LILO"). Escolha o bootloader de acordo com sua conveniência. Abaixo será explicado apenas o Syslinux e GRUB.

*   O Syslinux é(atualmente) limitado a carregar apenas arquivos na partição de onde foi instalado. Seu arquivo de configuração é considerado de mais fácil compreensão. Um exemplo pode ser encontrado [aqui](https://bbs.archlinux.org/viewtopic.php?pid=1109328#p1109328).

*   O GRUB é mais rico em recursos e suporta cenários mais complexos. Seu arquivo de configuração é mais parecido ao de uma linguagem de script, o que pode ser mais difícil para iniciantes gerenciarem manualmente. É recomendado a geração automática de um.

##### Syslinux

Instale o pacote [syslinux](https://www.archlinux.org/packages/?name=syslinux) e utilize o script `syslinux-install_update` para *instalar* os arquivos (`-i`), marcar a partição *ativa* atribuindo a flag (`-a`), e instalar o código de boot na *MBR* (`-m`):

**Nota:** Se você particionou o disco como GPT, instale o pacote [gptfdisk](https://www.archlinux.org/packages/?name=gptfdisk), através do comando (`pacman -S gptfdisk`), pois este contem o software `sgdisk`, que será utilizado especificamente para atribuir a bootável específica da GPT.

```
# pacman -S syslinux
# syslinux-install_update -iam

```

Configure o arquivo {{ic|syslinux.cfg} para apontar pra partição raíz correta. Este passo é vital. Se apontado para a partição errada, o Arch Linux não irá inicializar. Altere a entrada `/dev/sda3` para refletir a configuração específica de sua partição raíz. *(se você particionou seu disco como o explicado no [exemplo](#Preparando_os_Discos), sua partição raíz é o sda1)*. Faça o mesmo para a entrada "fallback".

 `# nano /boot/syslinux/syslinux.cfg` 
```
...
LABEL arch
        ...
        APPEND root=/dev/sda3 ro
        ...
```

Para maiores informações, veja [Syslinux](/index.php/Syslinux "Syslinux").

##### GRUB

**Nota:** Para dispositivos particionados no formato GPT, em placas-mãe BIOS, o GRUB necessitará de uma "[Partição BIOS de boot](/index.php/GRUB#GPT_specific_instructions "GRUB")" de 2 MiB.

**Nota:** Por favor não utilize a nomenclatura `/dev/sda*X*` no comando abaixo. Você deve utilizar `/dev/sdb` se o Arch estiver instalado lá e se foi configurado na BIOS para que este seja o primeiro dispositivo na ordem de inicialização.

```
# pacman -S grub
# grub-install --target=i386-pc --recheck /dev/sda
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

Mesmo não havendo problemas na utilização de um `grub.cfg` gerado manualmente, é recomendado que iniciantes gerem tal arquivo automaticamente:

**Dica:** Para a busca automática de outros sistemas operacionais em seu computador, instale o pacote [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`)antes de rodar o próximo comando.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Para maiores informações sobre a configuração do GRUB, veja [GRUB](/index.php/GRUB "GRUB").

#### Placas-mãe UEFI

Para inicialização UEFI, o dispositivo precisa estar particionado no formato GPT, e uma partição de sistema UEFI(512MiB ou maior, FAT32, tipo`EF00`) precisa estar presente a montada em `/boot/efi`. Se você seguiu este guia desde o início, todos estes passos foram executados.

Mesmo existindo outros [UEFI bootloaders](/index.php/UEFI_Bootloaders "UEFI Bootloaders") disponíveis, usar o EFISTUB é o recomendado. Abaixo há instruções para a configuração do EFISTUB com GRUB.

**Nota:** Syslinux ainda não suporte UEFI.

##### EFISTUB

O Kernel Linux pode atuar como seu próprio bootloader usando o EFISTUP. Este é o método de boot recomendado pelos desenvolvedores, e mais simples se comparado com o `grub-efi-x86_64`. Os passos abaixo configuram o rEFInd(um fork do rEFIt) para prover um menu para kernels EFISTUB, assim como executar outros gerenciadores de inicialização UEFI. Você também pode utilizar o [gummiboot](/index.php/UEFI_Bootloaders#Using_gummiboot "UEFI Bootloaders")(não testado) ao invés do rEFInd. Ambos detecam gerenciadores de inicialização Windows UEFI em caso de dual-boot.

1\. Inicie no modo UEFI e carregue o módulo do kernel `efivars` antes de efetuar o chroot:

```
# modprobe efivars      # antes do chroot

```

2\. Monte a partição UEFISYS em `/mnt/boot/efi`, execute o chroot e [copie os arquivos de kernel e initramfs](/index.php/UEFI_Bootloaders#Setting_up_EFISTUB "UEFI Bootloaders") para `/boot/efi`.

3\. Cada vez que o kernel e o initramfs forem atualizados em `/boot`, precisam ser replicados para `/boot/efi/EFI/arch`. Este processo pode ser automatizado [utilizando o systemd](/index.php/UEFI_Bootloaders#Sync_EFISTUB_Kernel_in_UEFISYS_partition_using_Systemd "UEFI Bootloaders") ou [usando o incron](/index.php/UEFI_Bootloaders#Sync_EFISTUB_Kernel_in_UEFISYS_partition_using_Incron "UEFI Bootloaders") (para instalações sem o systemd).

4\. Instale os seguintes pacotes

```
# pacman -S refind-efi-x86_64 efibootmgr

```

5\. Instale o rEFInd na partição UEFISYS (resumido de [UEFI Bootloaders#Using rEFInd](/index.php/UEFI_Bootloaders#Using_rEFInd "UEFI Bootloaders")):

```
# mkdir -p /boot/efi/EFI/arch/refind
# cp /usr/lib/refind/refindx64.efi /boot/efi/EFI/arch/refind/refindx64.efi
# cp /usr/lib/refind/config/refind.conf /boot/efi/EFI/arch/refind/refind.conf
# cp -r /usr/share/refind/icons /boot/efi/EFI/arch/refind/icons

```

6\. Crie um arquivo `refind_linux.conf` com os parametros de kernel que serão utilizados pelo rEFInd:

 `# nano /boot/efi/EFI/arch/refind_linux.conf` 
```
"Boot to X"          "root=/dev/sdaX ro rootfstype=ext4 systemd.unit=graphical.target"
"Boot to console"    "root=/dev/sdaX ro rootfstype=ext4 systemd.unit=multi-user.target"
```

7\. Adicione o rEFInd ao menu de inicialização UEFI usando [efibootmgr](/index.php/UEFI#efibootmgr "UEFI").

**Warning:** Utilizar o `efibootmgr` em Macs da Apple pode "bricar" a firmware e um novo processo de Flash da ROM da placa-mãe pode ser necessário. Para Macs, utilize o [mactel-boot](https://aur.archlinux.org/packages/mactel-boot/), ou "bless" do próprio Mac OS X.

```
# efibootmgr -c -g -d /dev/sdX -p Y -w -L "Arch Linux (rEFInd)" -l '\\EFI\\arch\\refind\\refindx64.efi'

```

**Nota:** No comando acima o X e o Y denotam o dispositivo e a partição UEFISYS. Por exemplo, em `/dev/sdc5`, X é "c" e Y é "5".

8\. (Opcional) Como um fallback, no caso do `efibootmgr` criar uma entrada de inicialização que não funcione, copie o `refindx64.efi` para o `/boot/efi/EFI/boot/bootx64.efi` como mostrado abaixo:

```
# cp -r /boot/efi/EFI/arch/refind/* /boot/efi/EFI/boot/
# mv /boot/efi/EFI/boot/refindx64.efi /boot/efi/EFI/boot/bootx64.efi

```

##### GRUB

**Nota:** Caso você possua um sistema EFI 32-bit, como os Macs de antes de 2008, instale o `grub-efi-i386` e use o `--target=i386-efi`.

```
# pacman -S grub-efi-x86_64 efibootmgr
# grub-install --target=x86_64-efi --efi-directory=/boot/efi --bootloader-id=arch_grub --recheck
# cp /usr/share/locale/en\@quot/LC_MESSAGES/grub.mo /boot/grub/locale/en.mo

```

Rode o próximo comando para criar a entrada do GRUB no menu da UEFI Veja [efibootmgr](/index.php/UEFI#efibootmgr "UEFI") para maiores informações.

```
# efibootmgr -c -g -d /dev/sdX -p Y -w -L "Arch Linux (GRUB)" -l '\\EFI\\arch_grub\\grubx64.efi'

```

Mesmo não havendo problemas na utilização de um `grub.cfg` gerado manualmente, é recomendado que iniciantes gerem tal arquivo automaticamente:

**Dica:** Para a busca automática de outros sistemas operacionais em seu computador, instale o pacote [os-prober](https://www.archlinux.org/packages/?name=os-prober) (`pacman -S os-prober`)antes de rodar o próximo comando.

```
# grub-mkconfig -o /boot/grub/grub.cfg

```

Para maiores informações sobre a configuração do GRUB, veja [GRUB](/index.php/GRUB "GRUB").

### Atualizar o sistema

**Warning:** Atualizações de sistema devem se efetuadas com cuidado. É muito importante ler e compreender o descrito [aqui](https://bbs.archlinux.org/viewtopic.php?id=57205) antes de executar qualquer procedimento.

Frequentemente, os desenvolvedores disponibilizarão informações importantes para configurações e modificações pertinentes a erros conhecidos. Do usuário Arch Linux é esperado que consulte estes lugares antes de efetuar um upgrade:

*   [Arch news](https://archlinux.org/news/). Se você efetuou um upgrade antes de ler aqui, verifique as notícias *antes* de postar uma questão no fórum!

*   [Lista de email - Anuncios](https://archlinux.org/pipermail/arch-announce/).

Sincronize, atualize o banco de dados de pacotes e atualize o sistema com:

```
# pacman -Syu

```

Sinônimo de:

```
# pacman --sync --refresh --sysupgrade

```

Se você for perguntado para atualizar o próprio pacman em algum momento, responda pressionando `Y`, e então execute uma segunda vez um `pacman -Syu` assim que terminar.

**Nota:** Ocasionalmente, arquivos de configuração podem ser alterados necessitando uma acão de confirmação do usuário; leia a saida do pacman e qualquer informação pertinente. Leia [este artigo](/index.php/Pacnew_and_Pacsave_files "Pacnew and Pacsave files") para maiores detalhes.

Lembre-se que o Arch é uma distribuição **rolling release**. Isto significa que o usuário não precisa reinstalar ou executar rebuilds elaboradas do sistema para atualizá-lo para uma nova versão. Executando um `pacman -Syu` periodicamente (lembrando do aviso acima) é o suficiente para mantes o sistema inteiro atualizado "bleeding edge". No final desta atualização, o sistema estará completamente -current.

Veja [Pacman](/index.php/Pacman "Pacman") e [gerenciamento de pacotes](/index.php/FAQ#Package_Management "FAQ") para respostas sobre atualização e gerenciamento de pacotes.

### Desmontar as partições e reiniciar

Saia do ambiente de chroot:

```
# exit

```

Como as partições estão montadas em `/mnt`, utilize o seguinte comando para desmontá-las:

```
# umount /mnt/{boot,home,}

```

Reinicie através do seguinte comando:

```
# reboot

```

**Dica:** Certifique-se de remover a mídia de instalação, para evitar que ela seja executada depois de reiniciar.

**[Beginners' guide](/index.php/Beginners%27_guide "Beginners' guide")**

* * *

[Prefácio](/index.php/Beginners%27_Guide/Preface_(Portugu%C3%AAs) "Beginners' Guide/Preface (Português)") >> [Preparar a Instalação](/index.php/Beginners%27_Guide/Preparation_(Portugu%C3%AAs) "Beginners' Guide/Preparation (Português)") >> **Instalar o sistema base** >> [Extras](/index.php/Beginners%27_Guide/Extra_(Portugu%C3%AAs) "Beginners' Guide/Extra (Português)")