Este documento irá guiá-lo no processo de instalação [Arch Linux](/index.php/Arch_Linux_(Portugu%C3%AAs) "Arch Linux (Português)") usando o [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Antes de instalar, é recomendável ler rapidamente o [FAQ](/index.php/FAQ_(Portugu%C3%AAs) "FAQ (Português)"). Para convenções usadas neste documento, veja [Help:Reading (Português)](/index.php/Help:Reading_(Portugu%C3%AAs) "Help:Reading (Português)"). Em especial, exemplos de código podem conter objetos reservados (formatados em `*italics*`) que devem ser substituídos manualmente.

Para instruções mais detalhadas, veja os respectivos artigos [ArchWiki](/index.php/ArchWiki:About_(Portugu%C3%AAs) "ArchWiki:About (Português)") ou as [páginas de manual](/index.php/Man_page_(Portugu%C3%AAs) "Man page (Português)") dos vários programas, ambos relacionados neste guia. Para uma ajuda interativa, o [canal IRC](/index.php/Canal_IRC "Canal IRC") e os [fóruns](https://bbs.archlinux.org/) também estão disponíveis.

Arch Linux deve funcionar em qualquer máquina compatível com [x86_64](https://en.wikipedia.org/wiki/pt:AMD64 "w:pt:AMD64") com um mínimo de 512 MB de RAM. Uma instalação básica com todos os pacotes do grupo [base](https://www.archlinux.org/groups/x86_64/base/) deve levar menos de 800 MB de espaço em disco. Como o processo de instalação precisa obter pacotes de repositório remoto, esse guia presume que uma conexão com a Internet esteja disponível.

## Contents

*   [1 Pré-instalação](#Pr.C3.A9-instala.C3.A7.C3.A3o)
    *   [1.1 Definir o layout do teclado](#Definir_o_layout_do_teclado)
    *   [1.2 Verificar o modo de inicialização](#Verificar_o_modo_de_inicializa.C3.A7.C3.A3o)
    *   [1.3 Conectar à Internet](#Conectar_.C3.A0_Internet)
    *   [1.4 Atualizar o relógio do sistema](#Atualizar_o_rel.C3.B3gio_do_sistema)
    *   [1.5 Partição dos discos](#Parti.C3.A7.C3.A3o_dos_discos)
    *   [1.6 Formatar as partições](#Formatar_as_parti.C3.A7.C3.B5es)
    *   [1.7 Montar os sistemas de arquivos](#Montar_os_sistemas_de_arquivos)
*   [2 Instalação](#Instala.C3.A7.C3.A3o)
    *   [2.1 Selecionar os mirrors](#Selecionar_os_mirrors)
    *   [2.2 Instalar os pacotes base](#Instalar_os_pacotes_base)
*   [3 Configurar o sistema](#Configurar_o_sistema)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Fuso horário](#Fuso_hor.C3.A1rio)
    *   [3.4 Locale](#Locale)
    *   [3.5 Hostname](#Hostname)
    *   [3.6 Configuração de rede](#Configura.C3.A7.C3.A3o_de_rede)
    *   [3.7 Initramfs](#Initramfs)
    *   [3.8 Senha do root](#Senha_do_root)
    *   [3.9 Gerenciador de boot](#Gerenciador_de_boot)
*   [4 Reiniciar](#Reiniciar)
*   [5 Pós-instalação](#P.C3.B3s-instala.C3.A7.C3.A3o)

## Pré-instalação

Baixe e inicialize a mídia de instalação como explicado em [Category:Getting and installing Arch (Português)](/index.php/Category:Getting_and_installing_Arch_(Portugu%C3%AAs) "Category:Getting and installing Arch (Português)"). Você será autenticado no primeiro [console virtual](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console") como o usuário root e apresentado como um prompt shell [Zsh](/index.php/Zsh "Zsh"); comandos comuns como [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1) podem ser [completados com tab](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion").

Para trocar para um console diferente — por exemplo, para ver esse guia com [ELinks](/index.php/ELinks "ELinks") junto com a instalação — use o [atalho](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*seta*`. Para [editar](/index.php/Edi%C3%A7%C3%A3o_de_texto "Edição de texto") arquivos de configuração, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") e [vim](/index.php/Vim#Usage "Vim") estão disponíveis.

### Definir o layout do teclado

O [mapa de teclas de console](/index.php/Mapa_de_teclas_de_console "Mapa de teclas de console") padrão é [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). Layouts disponíveis podem ser listados com:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

Para modificar o layout, acrescente um nome de arquivo ao [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), omitindo caminho e extensão de arquivo. Por exemplo, para definir um layout de teclado [ABNT (brasileiro)](https://en.wikipedia.org/wiki/File:KB_Portuguese_Brazil.svg "w:File:KB Portuguese Brazil.svg"):

```
# loadkeys br-abnt2

```

[Fontes de console](/index.php/Console_fonts "Console fonts") estão localizadas em `/usr/share/kbd/consolefonts/` e, de forma semelhante, podem ser definidas com [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Verificar o modo de inicialização

Se o modo UEFI estiver disponível em uma placa-mãe [UEFI](/index.php/UEFI "UEFI"), [Archiso](/index.php/Archiso "Archiso") vai [inicializar](/index.php/Boot "Boot") o Arch Linux adequadamente via [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Para verificar isso, liste o diretório [efivars](/index.php/UEFI#UEFI_variables "UEFI"):

```
# ls /sys/firmware/efi/efivars

```

Se o diretório não existir, o sistema pode ser inicializado no modo [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS") ou CSM. Veja o manual da sua placa-mãe para detalhes.

### Conectar à Internet

A imagem de instalação habilita o *daemon* [dhcpcd](/index.php/Dhcpcd "Dhcpcd") na inicialização para dispositivos de rede [cabeada](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules). A conexão pode ser [verificada](/index.php/Configura%C3%A7%C3%A3o_de_rede#Verificando_a_conex.C3.A3o "Configuração de rede") com:

```
# ping archlinux.org

```

Se nenhuma conexão estiver disponível, [pare](/index.php/Pare "Pare") o serviço *dhcpcd* com `systemctl stop dhcpcd@` e pressione `Tab`. Proceda com [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede#Driver_de_dispositivo "Configuração de rede") para dispositivos cabeados ou [Configuração de rede sem fio](/index.php/Wireless_network_configuration "Wireless network configuration") para dispositivos sem fio *(wireless)*.

### Atualizar o relógio do sistema

Use [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) para garantir que o relógio do sistema está certo:

```
# timedatectl set-ntp true

```

Para verificar o status do serviço, use `timedatectl status`.

### Partição dos discos

Quando reconhecido pelo sistema *live*, discos são atribuídos a um [dispositivo de bloco](https://en.wikipedia.org/wiki/Device_file#Naming_conventions "w:Device file") tal como `/dev/sda` ou `/dev/nvme0n1`.. Para identificar esses dispositivos, use [lsblk](/index.php/Lsblk "Lsblk") ou *fdisk*.

```
# fdisk -l

```

Resultados terminando em `rom`, `loop` ou `airoot` podem ser ignorados.

As seguintes *partições* são **exigidos** para um dispositivo escolhido:

*   Uma partição para o diretório raiz `/`.
*   Se [UEFI](/index.php/UEFI "UEFI") estiver habilitado, um [Partição de Sistema EFI](/index.php/EFI_System_Partition "EFI System Partition").

**Nota:** Espaço [swap](/index.php/Swap "Swap") pode ser definido em uma partição separada ou um [arquivo swap](/index.php/Arquivo_swap "Arquivo swap").

Para modificar *tabelas de partição*, use [fdisk](/index.php/Fdisk "Fdisk") ou [parted](/index.php/Parted "Parted").

```
# fdisk /dev/*sda*

```

Veja [Particionamento](/index.php/Partitioning "Partitioning") para mais informações.

**Nota:** Se você quiser criar qualquer dispositivo de bloco *stacked* para [LVM](/index.php/LVM "LVM"), [criptografia de disco](/index.php/Disk_encryption "Disk encryption") ou [RAID](/index.php/RAID "RAID"), faça-o agora.

### Formatar as partições

Assim que as partições tenham sido criadas, cada uma deve ser formatada com um [sistema de arquivos](/index.php/File_system "File system") adequado. Por exemplo, para formatar a partição raiz em `/dev/*sda1*` com `*ext4*`, execute:

```
# mkfs.*ext4* /dev/*sda1*

```

Se você criou uma partição para swap (por exemplo, `/dev/*sda3*`), inicialize-a com *mkswap*:

```
# mkswap /dev/*sda3*
# swapon /dev/*sda3*

```

Veja [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") para detalhes.

### Montar os sistemas de arquivos

[Monte](/index.php/Mount "Mount") o sistema de arquivos da partição raiz em `/mnt`, por exemplo:

```
# mount /dev/*sda1* /mnt

```

Crie pontos de montagem para quaisquer partições restantes e monte-as conforme adequado:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) vai detectar os sistemas de arquivos montados e espaços swap.

## Instalação

### Selecionar os mirrors

Pacotes a serem instalados devem ser baixados de [servidores *mirrors*](/index.php/Mirrors "Mirrors"), que são definidos na `/etc/pacman.d/mirrorlist`. No sistema *live*, todos os mirrors estão habilitados e ordenados por seu status e velocidade de sincronização à época em que a imagem de instalação foi criada.

Quanto mais alto um mirror está posicionado na lista, mais prioritário ele será ao baixar um pacote. Você pode querer editar o arquivo e mover mirrors geograficamente mais pertos para o topo da lista, apesar de que outros critérios devem ser levados em consideração.

Esse arquivo será posteriormente copiado para o novo sistema por *pacstrap*, então é melhor fazer direito.

### Instalar os pacotes base

Use o script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) para instalar o grupo de pacotes [base](https://www.archlinux.org/groups/x86_64/base/):

```
# pacstrap /mnt base

```

Esse grupo não inclui todas as ferramentas da instalação *live*, tal como [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) ou firmware de rede sem fio específico; veja [packages.both](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.both) para comparação.

Para [instalar](/index.php/Instalar "Instalar") pacotes e outros grupos, tal como [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), anexe os nomes ao *pacstrap* (separados por espaço) ou a comandos [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") após a etapa do [#Chroot](#Chroot).

## Configurar o sistema

### Fstab

Gerar um arquivo [fstab](/index.php/Fstab "Fstab") (use `-U` ou `-L` para definir por [UUID](/index.php/UUID "UUID") ou rótulos, respectivamente):

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

Verifique o arquivo resultante em `/mnt/etc/fstab` em seguida e edite-o caso haja erros.

### Chroot

[Mude a raiz](/index.php/Change_root_(Portugu%C3%AAs) "Change root (Português)") para novo sistema:

```
# arch-chroot /mnt

```

### Fuso horário

Defina o [fuso horário](/index.php/Time_zone "Time zone"):

```
# ln -sf /usr/share/zoneinfo/*Região*/*Cidade* /etc/localtime

```

Por exemplo, para definir para o fuso horário de Brasília (*BRT* ou *BRST*), execute:

```
# ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime

```

Execute [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) para gerar `/etc/adjtime`:

```
# hwclock --systohc

```

Esse comando presume que o relógio de hardware está definido para [UTC](https://en.wikipedia.org/wiki/UTC "w:UTC"). Veja [Time#Time standard](/index.php/Time#Time_standard "Time") para mais detalhes.

### Locale

Descomente `pt_BR.UTF-8 UTF-8` e qualquer outra [localização](/index.php/Localiza%C3%A7%C3%A3o "Localização") em `/etc/locale.gen`, e gere-as com:

```
# locale-gen

```

Defina a [variável](/index.php/Vari%C3%A1vel "Variável") `LANG` em [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5) adequadamente, por exemplo:

 `/etc/locale.conf`  `LANG=*pt_BR.UTF-8*` 

Se você [definir o layout do teclado](#Definir_o_layout_do_teclado), torne as alterações persistentes em [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*br-abnt2*` 

### Hostname

Crie o arquivo [hostname](/index.php/Hostname "Hostname"):

 `/etc/hostname` 
```
*meuhostname*

```

Adicione entradas correspondentes ao [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5):

 `/etc/hosts` 
```
127.0.0.1	localhost.localdomain	localhost
::1		localhost.localdomain	localhost
**127.0.1.1	*meuhostname*.localdomain	*meuhostname***

```

Se o sistema tem um endereço IP permanente, ele deve ser usado em vez de `127.0.1.1`.

### Configuração de rede

O recém-instalado ambiente possui nenhuma conectividade de rede ativada por padrão. Veja [Configuração de rede](/index.php/Configura%C3%A7%C3%A3o_de_rede "Configuração de rede") para configurar uma.

Para [Configuração sem fio](/index.php/Wireless_configuration "Wireless configuration"), [instale](/index.php/Instale "Instale") os pacotes [iw](https://www.archlinux.org/packages/?name=iw) e [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant), assim como [pacotes de firmware](/index.php/Wireless#Installing_driver.2Ffirmware "Wireless") que se fizerem necessários. Opcionalmente, instale [dialog](https://www.archlinux.org/packages/?name=dialog) para uso de *wifi-menu*.

### Initramfs

Criar um novo *initramfs* geralmente não é necessário, porque [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") foi executado na instalação do pacote [linux](https://www.archlinux.org/packages/?name=linux) com *pacstrap*.

Para configurações especiais, modifique o arquivo [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) e recrie a imagem initramfs:

```
# mkinitcpio -p linux

```

### Senha do root

Defina a [senha](/index.php/Senha "Senha") do *root* (também conhecido como "superusuário"):

```
# passwd

```

### Gerenciador de boot

Você pode escolher entre [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") ou [Syslinux](/index.php/Syslinux "Syslinux").

Um gerenciador de boot compatível com o Linux deve ser instalado para inicializar o Arch Linux. Veja [Category:Boot loaders (Português)](/index.php/Category:Boot_loaders_(Portugu%C3%AAs) "Category:Boot loaders (Português)") para escolhas disponíveis e configurações.

Se você tiver um CPU Intel, instale o pacote [intel-ucode](https://www.archlinux.org/packages/?name=intel-ucode) também, e [habilite atualizações de *microcode*](/index.php/Microcode#Enabling_Intel_microcode_updates "Microcode").

## Reiniciar

Saia de ambiente *chroot* digitando `exit` ou pressionando `Ctrl+D`.

Opcionalmente, desmonte todas as partições com `umount -R /mnt`: isso permite noticiar quaisquer partições "ocupadas" e localizar a causa com o [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Finalmente, reinicie a máquina digitando `reboot`: quaisquer partições que ainda estejam montadas serão desmontadas automaticamente por *systemd*. Lembre-se de remover a mídia de instalação e, então, se autenticando no novo sistema com a conta de root.

## Pós-instalação

Veja [Recomendações gerais](/index.php/Recomenda%C3%A7%C3%B5es_gerais "Recomendações gerais") por instruções de gerenciamento de sistema e tutoriais pós-instalação (como instalar uma interface gráfica de usuário, som ou um touchpad).

Para uma lista de aplicativos que podem ser de seu interesse, veja [Lista de aplicativos](/index.php/List_of_applications "List of applications").