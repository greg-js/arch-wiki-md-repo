Este documento irá guiá-lo no processo de instalação [Arch Linux](/index.php/Arch_Linux "Arch Linux") usando o [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Antes de instalar, é recomendável ler rapidamente o [FAQ (Português)](/index.php/FAQ_(Portugu%C3%AAs) "FAQ (Português)"). Para convenções usadas neste documento, veja [Help:Reading](/index.php/Help:Reading "Help:Reading").

Para instruções mais detalhadas, veja os respectivos artigos [ArchWiki](/index.php/ArchWiki:About "ArchWiki:About") ou as [páginas de manual](/index.php/Man_page "Man page") dos vários programas, ambos relacionados neste guia. Veja [archlinux(7)](https://projects.archlinux.org/svntogit/packages.git/tree/filesystem/trunk/archlinux.7.txt) para uma visão geral da configuração. Para uma ajuda interativa, o [canal IRC](/index.php/IRC_channel "IRC channel") e os [fóruns](https://bbs.archlinux.org/) também estão disponíveis.

## Contents

*   [1 Pré-instalação](#Pr.C3.A9-instala.C3.A7.C3.A3o)
    *   [1.1 Defina o layout do teclado](#Defina_o_layout_do_teclado)
    *   [1.2 Verificar o modo de inicialização](#Verificar_o_modo_de_inicializa.C3.A7.C3.A3o)
    *   [1.3 Conectar à Internet](#Conectar_.C3.A0_Internet)
    *   [1.4 Atualizar o relógio do sistema](#Atualizar_o_rel.C3.B3gio_do_sistema)
    *   [1.5 Partição dos discos](#Parti.C3.A7.C3.A3o_dos_discos)
    *   [1.6 Formatar as partições](#Formatar_as_parti.C3.A7.C3.B5es)
    *   [1.7 Montar os sistemas de arquivos](#Montar_os_sistemas_de_arquivos)
*   [2 Instalação](#Instala.C3.A7.C3.A3o)
    *   [2.1 Selecionar os mirrors](#Selecionar_os_mirrors)
    *   [2.2 Instalar os pacotes base](#Instalar_os_pacotes_base)
    *   [2.3 Configurar o sistema](#Configurar_o_sistema)
    *   [2.4 Instalar e configurar um gerenciador de boot](#Instalar_e_configurar_um_gerenciador_de_boot)
    *   [2.5 Desmontar e reiniciar](#Desmontar_e_reiniciar)
*   [3 Pós-instalação](#P.C3.B3s-instala.C3.A7.C3.A3o)
*   [4 Configure o pacman](#Configure_o_pacman)
*   [5 Atualizando o sistema](#Atualizando_o_sistema)
    *   [5.1 Gerenciamento de usuários](#Gerenciamento_de_usu.C3.A1rios)
    *   [5.2 Gerenciamento de pacotes](#Gerenciamento_de_pacotes)
    *   [5.3 Gerenciamento de serviços](#Gerenciamento_de_servi.C3.A7os)
    *   [5.4 Som](#Som)
    *   [5.5 Driver de Video](#Driver_de_Video)
    *   [5.6 Servidor de exibição](#Servidor_de_exibi.C3.A7.C3.A3o)
    *   [5.7 Fontes](#Fontes)
*   [6 Apêndice](#Ap.C3.AAndice)

## Pré-instalação

Arch Linux deve funcionar em qualquer máquina compatível com [x86_64](https://en.wikipedia.org/wiki/X86-64 "w:X86-64") com um mínimo de 512 MB de RAM. Uma instalação básica com todos os pacotes do grupo [base](https://www.archlinux.org/groups/x86_64/base/) deve levar menos de 800 MB de espaço em disco. Como o processo de instalação precisa obter pacotes de repositório remoto, uma conexão internet deve é necessária.

Baixe e inicialize a mídia de instalação como explicado em [Category:Getting and installing Arch (Português)](/index.php/Category:Getting_and_installing_Arch_(Portugu%C3%AAs) "Category:Getting and installing Arch (Português)"). Você será autenticado no primeiro [console virtual](https://en.wikipedia.org/wiki/Virtual_console "w:Virtual console") como o usuário root e apresentado como um prompt shell [Zsh](/index.php/Zsh "Zsh"); comandos comuns como [systemctl(1)](http://man7.org/linux/man-pages/man1/systemctl.1.html) podem ser [completados com tab](https://en.wikipedia.org/wiki/Command-line_completion "w:Command-line completion").

Para trocar para um console diferente — por exemplo, para ver esse guia com [ELinks](/index.php/ELinks "ELinks") junto com a instalação — use o [atalho](/index.php/Keyboard_shortcuts "Keyboard shortcuts") `Alt+*arrow*`. Para [editar](/index.php/Textedit "Textedit") arquivos de configuração, [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "w:vi") e [vim](/index.php/Vim#Usage "Vim") estão disponíveis.

### Defina o layout do teclado

O [mapa de teclas de console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") padrão é [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "w:File:KB United States-NoAltGr.svg"). Para listar todos os layouts disponíveis, execute `ls /usr/share/kbd/keymaps/**/*.map.gz`.

Para modificar o layout, acrescente um nome de arquivo ao [loadkeys(1)](http://man7.org/linux/man-pages/man1/loadkeys.1.html), omitindo caminho e extensão de arquivo. Por exemplo, execute `loadkeys br-abnt2` para definir um layout de teclado [brasileiro](https://en.wikipedia.org/wiki/File:KB_Portuguese_Brazil.svg "w:File:KB Portuguese Brazil.svg").

[Fontes de console](/index.php/Console_fonts "Console fonts") estão localizadas em `/usr/share/kbd/consolefonts/` e, de forma semelhante, podem ser definidas com [setfont(8)](http://man7.org/linux/man-pages/man8/setfont.8.html).

### Verificar o modo de inicialização

Se o modo UEFI estiver disponível em uma placa-mãe [UEFI](/index.php/UEFI "UEFI"), [Archiso](/index.php/Archiso "Archiso") vai [inicializar](/index.php/Boot "Boot") o Arch Linux adequadamente via [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). Para verificar isso, liste o diretório [efivars](/index.php/UEFI#UEFI_Variables "UEFI"):

```
# ls /sys/firmware/efi/efivars

```

Se o diretório não existir, o sistema pode ser inicializado no modo [BIOS](https://en.wikipedia.org/wiki/BIOS "w:BIOS") ou CSM. Veja o manual da sua placa-mãe para detalhes.

### Conectar à Internet

A imagem de instalação [habilita](/index.php/Enable "Enable") o *daemon* [dhcpcd](/index.php/Dhcpcd "Dhcpcd") na inicialização para dispositivos [cabeados](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) e vai tentar iniciar uma conexão. Verifique sea conectividade da internet está disponível, por exemplo com [ping](/index.php/Ping "Ping"):

```
# ping archlinux.org

```

Se nenhum estiver disponível, [pare](/index.php/Stop "Stop") o serviço *dhcpcd* com `systemctl stop dhcpcd@<TAB>` e veja [Configuração de rede](/index.php/Network_configuration#Device_driver "Network configuration").

Para conexões **sem fio** (*wireless*), iw(8), wpa_supplicant(8) e [netctl](/index.php/Netctl#Wireless_.28WPA-PSK.29 "Netctl") estão disponíveis. Veja [Configuração de rede sem fio](/index.php/Wireless_network_configuration "Wireless network configuration").

### Atualizar o relógio do sistema

Use [timedatectl(1)](http://man7.org/linux/man-pages/man1/timedatectl.1.html) para garantir que o relógio do sistema está certo:

```
# timedatectl set-ntp true

```

Para verificar o status do serviço, use `timedatectl status`.

### Partição dos discos

Quando reconhecido pelo sistema *live*, discos são atribuídos a um *dispositivo de bbloco* tal como `/dev/sda`. Para identificar esses dispositivos, use [lsblk](/index.php/Lsblk "Lsblk") ou *fdisk* — resultados no final de `rom`, `loop` ou `airoot` podem ser ignorados:

```
# fdisk -l

```

As seguintes *partições* (mostradas com um sufixo numérico) são exigidos para um dispositivo escolhido:

*   Uma partição para o diretório raiz `/`.
*   Se [UEFI](/index.php/UEFI "UEFI") estiver habilitado, um [Partição de Sistema EFI](/index.php/EFI_System_Partition "EFI System Partition").

[Espaço swap](/index.php/Swap_space "Swap space") pode ser definido em uma partição separada ou um [arquivo swap](/index.php/Swap_file "Swap file").

Para modificar as *tabelas de partição*, use [fdisk](/index.php/Fdisk "Fdisk") ou [parted](/index.php/Parted "Parted"). Veja [Particionamento](/index.php/Partitioning "Partitioning") para mais informações.

Se você quiser criar qualquer dispositivo de bloco *stacked* para [LVM](/index.php/LVM "LVM"), [criptografia de disco](/index.php/Disk_encryption "Disk encryption") ou [RAID](/index.php/RAID "RAID"), faça-o agora.

### Formatar as partições

Assim que as partições tenham sido criadas, cada uma deve ser formatada com um [sistema de arquivos](/index.php/File_system "File system") adequado. Por exemplo, para formatar a partição raiz em `/dev/*sda1*` com `*ext4*`, execute:

```
# mkfs.*ext4* /dev/*sda1*

```

Veja [File systems#Create a file system](/index.php/File_systems#Create_a_file_system "File systems") para detalhes.

### Montar os sistemas de arquivos

[Monte](/index.php/File_systems#Mount_a_filesystem "File systems") o sistema de arquivos da partição raiz em `/mnt`, por exemplo:

```
# mount /dev/*sda1* /mnt

```

Crie pontos de montagem para quaisquer partições restantes e monte-as conforme adequado, por exemplo:

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

Para [instalar](/index.php/Install "Install") pacotes e outros grupos, tal como [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), anexe os nomes ao *pacstrap* (separados por espaço) ou a comandos [pacman](/index.php/Pacman_(Portugu%C3%AAs) "Pacman (Português)") após a etapa do [#Chroot](#Chroot).

### Configurar o sistema

*   Gerar um [fstab](/index.php/Fstab "Fstab") com o seguinte comando (se preferir use UUIDs ou labels, adicione a opção `-U` ou `-L`, respectivamente):

	 `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   [chroot](/index.php/Chroot "Chroot") em nosso sistema recém-instalado:

	 `# arch-chroot /mnt` 

*   Escreva seu hostname em `/etc/hostname`.

*   Symlink `/etc/localtime` para `/usr/share/zoneinfo/Zone/SubZone`. Substitua `Zone` e `Subzone` em seu liking. Por exemplo:

	 `# ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime` 

*   Descomente o local selecionado em `/etc/locale.gen` e gere-o com `locale-gen`.
*   Defina a preferência [locale](/index.php/Locale#Setting_the_system_locale "Locale") em `/etc/locale.conf`.
*   Adicione a preferência [console keymap](/index.php/KEYMAP "KEYMAP") e [font](/index.php/Fonts#Console_fonts "Fonts") em `/etc/vconsole.conf`
*   Configure `/etc/mkinitcpio.conf` conforme necessário (veja [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")) e crie um disco RAM inicial com:

	 `# mkinitcpio -p linux` 

*   Defina uma seha root com `passwd`.
*   Configure a rede novamente para o ambiente recém-instalado. Consulte [Network configuration](/index.php/Network_configuration "Network configuration") e [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration").

### Instalar e configurar um gerenciador de boot

Você pode escolher entre [GRUB](/index.php/GRUB "GRUB") ou [Syslinux](/index.php/Syslinux "Syslinux").

*GRUB*

*   Para BIOS:

```
# arch-chroot /mnt pacman -S grub-bios

```

*   Para EFI(e em raros casos você precisará instalar `grub-efi-i386` ao invés de x86_64):

```
# arch-chroot /mnt pacman -S /mnt grub-efi-x86_64

```

*   Instale o GRUB antes de executar o chroot (sessão [Configurando o Sistema](#Configurar_o_sistema)).

*Syslinux*

```
# arch-chroot /mnt pacman -S syslinux

```

### Desmontar e reiniciar

Se você ainda está no ambiente chroot digite `exit` ou pressione `Ctrl+D` para sair. Anteriormente montamos as partições em `/mnt`. Nesta etapa vamos desmontá-las:

```
# umount /mnt/{boot,home,}

```

Agora reinicie e então faça a autenticação no seu novo sistema com a conta root.

## Pós-instalação

## Configure o pacman

Edite `/etc/pacman.conf` e configure as opções, assim como os repositórios que deseja.

Veja [Pacman](/index.php/Pacman "Pacman") e [Official repositories](/index.php/Official_repositories "Official repositories") para mais detalhes.

## Atualizando o sistema

A partir deste ponto, é aconselhavel que você atualize o sistema.

Veja [atualizando os pacotes](/index.php/Pacman#Upgrading_packages "Pacman") para maiores instruções.

### Gerenciamento de usuários

Adicione as contas de usuário que você precisa além do conta root, como descrito em [User management](/index.php/Users_and_groups#User_management "Users and groups"). Não é recomendável usar a conta root para uso normal, ou expô-la via [SSH](/index.php/SSH "SSH") em um servidor. A conta root só deve ser usada para tarefas administrativas.

### Gerenciamento de pacotes

Consulte [pacman](/index.php/Pacman "Pacman") e [FAQ#Package management](/index.php/FAQ#Package_management "FAQ") para respostas sobre a instalação, atualização e gerenciamento de pacotes.

### Gerenciamento de serviços

Arch Linux usa [systemd (Português)](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") como init, que é um sistema e gerenciador de serviços para Linux. Para manter sua instalação do Arch Linux, é recomendável aprender o básico sobre o assunto. Interação com systemd é feito via comando `systemctl`. Leia [Uso_básico_systemctl](/index.php/Systemd_(Portugu%C3%AAs)#Uso_b.C3.A1sico_systemctl "Systemd (Português)") para maiores informações.

### Som

Instale o [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (que contém `alsamixer`) e siga as instruções [these](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture").

ALSA está incluído no kernel e é recomendado. Se não funcionar, [OSS](/index.php/OSS "OSS") é uma alternativa viável. Se houver requisitos avançadas de áudio, dê uma olhada no [Sound system](/index.php/Sound_system "Sound system") para uma visão geral de vários artigos.

### Driver de Video

O kernel do Linux inclui drivers de vídeo de código aberto e suporte para hardware framebuffers. No entanto, é necessário o suporte em nível usuário para OpenGL e aceleração 2D no X11.

Se você não sabe qual o chipset de vídeo que está disponível no seu computador, execute:

```
$ lspci | grep VGA

```

Para obter uma lista completa de drivers de vídeo de código aberto, procure o banco de dados do pacote:

```
$ pacman -Ss xf86-video | less

```

O driver `vesa` é um controlador de definição de modo genérico, que irá trabalhar com quase todas as GPU, mas não fornecerá nenhuma aceleração 2D ou 3D. Se um driver preferível não puder ser localizado ou falhar ao carregar, Xorg voltará para o vesa. Para instalá-lo:

```
# pacman -S xf86-video-vesa

```

Para aceleração de vídeo funcionar, e muitas vezes para mostrar todos os modos de definição da GPU, um driver de vídeo adequado é necessário:

| Marca | Tipo | Driver | Pacote [Multilib](/index.php/Multilib "Multilib")
(para aplicativos 32-bit em Arch x86_64) | Documentação |
| **AMD/ATI** | Código aberto | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-ati-dri](https://www.archlinux.org/packages/?name=lib32-ati-dri) | [ATI](/index.php/ATI "ATI") |
| Proprietário | [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| **Intel** | Código aberto | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| **Nvidia** | Código aberto | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri) | [Nouveau](/index.php/Nouveau "Nouveau") |
| [xf86-video-nv](https://aur.archlinux.org/packages/xf86-video-nv/) | – | (driver legacy) |
| Proprietário | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) |

### Servidor de exibição

O Sistema X Window (geralmente X11, ou X) é uma rede e protocolo de exibição que fornece janelas em bitmap. É o padrão de fato para implementação de interfaces gráficas de usuário. Consulte o artigo [Xorg](/index.php/Xorg "Xorg") para obter mais detalhes.

[Wayland](/index.php/Wayland "Wayland") é um novo protocolo de servidor de exibição e a implementação de referência Weston está disponível. Há muito pouco suporte de aplicações nesta fase inicial de desenvolvimento.

### Fontes

Você pode querer instalar um conjunto de fontes TrueType, como somente não escalar fontes bitmap que são incluídas por padrão. DejaVu é um conjunto de alta qualidade, as fontes de uso geral com boa cobertura [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode"):

```
# pacman -S ttf-dejavu

```

Consulte [Font configuration](/index.php/Font_configuration "Font configuration") para saber como configurar a renderização de fontes e [Fonts](/index.php/Fonts "Fonts") para sugestões de fonte e instruções de instalação.

## Apêndice

Para uma lista de aplicativos que podem ser do seu interesse, veja a [List of applications](/index.php/List_of_applications "List of applications").

Consulte [General recommendations](/index.php/General_recommendations "General recommendations") para tutoriais de pós-instalação, como confirar touchpad ou fonte de renderização.