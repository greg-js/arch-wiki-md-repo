Este documento irá guiá-lo no processo de instalação [Arch Linux](/index.php/Arch_Linux "Arch Linux") usando o [Arch Install Scripts](https://projects.archlinux.org/arch-install-scripts.git/). Antes de instalar, é recomendável ler rapidamente o [FAQ_(Português)](/index.php/FAQ_(Portugu%C3%AAs) "FAQ (Português)"). Consulte [Beginners'_Guide_(Português)](/index.php/Beginners%27_Guide_(Portugu%C3%AAs) "Beginners' Guide (Português)") para um guia de instalação mais detalhado.

[Arch wiki](/index.php/Main_page "Main page") é um excelente recurso e deve ser consultado para as primeiras questões. O canal [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), e o [[1]](http://forum.archlinux-br.org/index.php) também estão disponíveis se a resposta não puder ser encontrada em outro lugar. Além disso, não esqueça de verificar as páginas `man` para qualquer comando não familiarizado, o que normalmente pode ser invocado com `man *command*`.

## Contents

*   [1 Download](#Download)
*   [2 Instalação](#Instala.C3.A7.C3.A3o)
    *   [2.1 Layout do teclado](#Layout_do_teclado)
    *   [2.2 Partição de discos](#Parti.C3.A7.C3.A3o_de_discos)
    *   [2.3 Formatar as partições](#Formatar_as_parti.C3.A7.C3.B5es)
    *   [2.4 Montar as partições](#Montar_as_parti.C3.A7.C3.B5es)
    *   [2.5 Conectar-se à internet](#Conectar-se_.C3.A0_internet)
        *   [2.5.1 Rede sem fio](#Rede_sem_fio)
    *   [2.6 Instalar o sistema base](#Instalar_o_sistema_base)
    *   [2.7 Configurar o sistema](#Configurar_o_sistema)
    *   [2.8 Instalar e configurar um gerenciador de boot](#Instalar_e_configurar_um_gerenciador_de_boot)
    *   [2.9 Desmontar e reiniciar](#Desmontar_e_reiniciar)
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

## Download

Baixe a nova mídia ISO Arch Linux em [Arch Linux download page](https://www.archlinux.org/download/).

*   Uma única imagem é fornecida, que pode ser iniciada de forma "live" em sistemas i686 e x86_64 para instalar Arch Linux através da rede. A mídia que contém o repositório [core] não são mais fornecidas.
*   Instale imagens que sejam assinadas e é altamente recomendável verificar a sua assinatura antes do uso: isso pode ser feito baixando o arquivo *.sig* da página de download (ou um dos espelhos listados lá) para o mesmo diretório do arquivo *.iso* e usando `pacman-key -v *iso-file*.sig`.
*   A imagem pode ser queimada para um CD, montada como um arquivo ISO, ou diretamente [gravados em um pen drive](/index.php/USB_Installation_Media "USB Installation Media"). Destina-se só para novas instalações, um sistema Arch Linux existente pode ser sempre atualizado com `pacman -Syu`.

## Instalação

### Layout do teclado

Para a maioria dos países, os tipos de mapeamentos de teclado já estão disponíveis, e um comando como `loadkeys uk` pode fazer o que quer. Mais arquivos de mapeamento de teclado podem ser encontrados em `/usr/share/kbd/keymaps/` (você pode omitir o caminho e arquivo de extensão keymap ao usar loadkeys).

### Partição de discos

Consulte [partitioning](/index.php/Partitioning "Partitioning") para detalhes.

Se deseja criar quaisquer blocos de dispositivos como [LVM](/index.php/LVM "LVM"), [LUKS](/index.php/Dm-crypt_with_LUKS "Dm-crypt with LUKS"), ou [RAID](/index.php/RAID "RAID"), faça agora.

### Formatar as partições

Consulte [File Systems](/index.php/File_systems#Step_2:_create_the_new_file_system "File systems") para detalhes.

Se você usa (U)EFI provavelmente você vai precisar de uma outra partição para hospedar o sistema de partição UEFI. Leia [Crie uma partição de sistema UEFI no Linux](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface").

### Montar as partições

Agora temos de montar a partição root em `/mnt`.Também deve criar diretórios para e montar outras partições (`/mnt/boot`, `/mnt/home`, ...) e monte sua partição [swap](/index.php/Swap "Swap") se quiser que seja detectada pelo `genfstab`.

### Conectar-se à internet

Um serviço DHCP já está ativado para todos os dispositivos disponíveis. Se você precisa configurar um IP estático ou usar ferramentas de gerenciamento, como o [Netctl](/index.php/Netctl "Netctl"), você deveria parar este serviço primeiro: `systemctl stop dhcpcd.service`. Para maiores informações, leia [configuring network](/index.php/Configuring_network "Configuring network").

#### Rede sem fio

Execute `wifi-menu` para configurar sua rede sem fio. Para detalhes, consulte [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") e [Netctl](/index.php/Netctl "Netctl").

### Instalar o sistema base

Antes de instalar, talvez você queira editar `/etc/pacman.d/mirrorlist` de tal modo que seu [espelho](/index.php/Mirrors "Mirrors") preferido seja o primeiro. Esta cópia da lista de espelhos será instalado em seu novo sistema pelo `pacstrap`, então vale a pena fazer direito.

Usando o script [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) instalamos o sistema básico

```
# pacstrap /mnt base

```

Outros pacotes podem ser instalados adicionando seus nomes no comando acima (separados por espaço), incluindo o gerenciador de boot, se quiser.

### Configurar o sistema

*   Gerar um [fstab](/index.php/Fstab "Fstab") com o seguinte comando (se preferir use UUIDs ou labels, adicione a opção `-U` ou `-L`, respectivamente):

	 `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   [chroot](/index.php/Chroot "Chroot") em nosso sistema recém-instalado:

	 `# arch-chroot /mnt` 

*   Escreva seu hostname em `/etc/hostname`.

*   Symlink `/etc/localtime` para `/usr/share/zoneinfo/Zone/SubZone`. Substitua `Zone` e `Subzone` em seu liking. Por exemplo:

	 `# ln -s /usr/share/zoneinfo/America/Sao_Paulo /etc/localtime` 

*   Descomente o local selecionado em `/etc/locale.gen` e gere-o com `locale-gen`.
*   Defina a preferência [locale](/index.php/Locale#Setting_system-wide_locale "Locale") em `/etc/locale.conf`.
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

*   Instale o GRUB antes de executar o chroot (sessão [Configurando o Sistema](#Configurando_o_Sistema)).

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

Consulte [pacman](/index.php/Pacman "Pacman") e [FAQ#Package Management](/index.php/FAQ#Package_Management "FAQ") para respostas sobre a instalação, atualização e gerenciamento de pacotes.

### Gerenciamento de serviços

Arch Linux usa [Systemd_(Português)](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") como init, que é um sistema e gerenciador de serviços para Linux. Para manter sua instalação do Arch Linux, é recomendável aprender o básico sobre o assunto. Interação com systemd é feito via comando `systemctl`. Leia [Uso_básico_systemctl](/index.php/Systemd_(Portugu%C3%AAs)#Uso_b.C3.A1sico_systemctl "Systemd (Português)") para maiores informações.

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
| [xf86-video-nv](https://www.archlinux.org/packages/?name=xf86-video-nv) | – | (driver legacy) |
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