**Status de tradução:** Esse artigo é uma tradução de [Arch boot process](/index.php/Arch_boot_process "Arch boot process"). Data da última tradução: 2020-01-18\. Você pode ajudar a sincronizar a tradução, se houver [alterações](https://wiki.archlinux.org/index.php?title=Arch_boot_process&diff=0&oldid=595393) na versão em inglês.

Artigos relacionados

*   [Master Boot Record](/index.php/Particionamento#Master_Boot_Record "Particionamento")
*   [Tabela de Partição GUID](/index.php/Particionamento#Tabela_de_Partição_GUID "Particionamento")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [init](/index.php/Init_(Portugu%C3%AAs) "Init (Português)")
*   [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)")
*   [fstab](/index.php/Fstab "Fstab")
*   [Inicialização automática](/index.php/Inicializa%C3%A7%C3%A3o_autom%C3%A1tica "Inicialização automática")

Para inicializar o Arch Linux, um carregador [gerenciador de boot](#Gerenciador_de_boot) compatível com Linux deve ser configurado. O gerenciador de boot é responsável por carregar o kernel e o [ramdisk inicial](/index.php/Initial_ramdisk "Initial ramdisk") antes de iniciar o processo de inicialização. O procedimento é bastante diferente para sistemas [BIOS](https://en.wikipedia.org/wiki/pt:BIOS "wikipedia:pt:BIOS") e [UEFI](/index.php/UEFI "UEFI"), a descrição detalhada é fornecida nesta página ou em páginas vinculadas.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Tipos de firmware](#Tipos_de_firmware)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Inicialização do sistema](#Inicialização_do_sistema)
    *   [2.1 Na BIOS](#Na_BIOS)
    *   [2.2 No UEFI](#No_UEFI)
    *   [2.3 Multiboot no UEFI](#Multiboot_no_UEFI)
*   [3 Gerenciador de boot](#Gerenciador_de_boot)
*   [4 Comparação de recursos](#Comparação_de_recursos)
*   [5 Kernel](#Kernel)
*   [6 initramfs](#initramfs)
*   [7 Processo init](#Processo_init)
*   [8 getty](#getty)
*   [9 Gerenciador de exibição](#Gerenciador_de_exibição)
*   [10 Login](#Login)
*   [11 Shell](#Shell)
*   [12 GUI, xinit ou wayland](#GUI,_xinit_ou_wayland)
*   [13 Veja também](#Veja_também)

## Tipos de firmware

### BIOS

Uma [BIOS](https://en.wikipedia.org/wiki/pt:BIOS "wikipedia:pt:BIOS") (acrônimo para *Basic Input-Output System*) é o primeiro programa (firmware) que é executado assim que o sistema é ligado. Na maioria dos casos, é armazenado em uma memória flash na própria placa-mãe e é independente do armazenamento do sistema.

### UEFI

[Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface") tem suporte para ler a tabela de partições e os sistemas de arquivos. UEFI não inicia qualquer [código de inicialização do Master Boot Record (MBR)](/index.php/Particionamento#Master_Boot_Record_(código_de_inicialização) "Particionamento") independentemente de existir ou não - em vez disso, a inicialização depende de entradas de inicialização na [NVRAM](https://en.wikipedia.org/wiki/pt:NVRAM "wikipedia:pt:NVRAM").

A especificação UEFI determina o suporte para os sistemas de arquivos [FAT12, FAT16 e FAT32](/index.php/FAT "FAT") (veja [Especificação UEFI versão 2.8, seção 13.3.1.1](https://uefi.org/sites/default/files/resources/UEFI_Spec_2_8_final.pdf#G17.1019485)), mas qualquer fornecedor em conformidade pode, opcionalmente, adicionar suporte para sistemas de arquivos adicionais; por exemplo, o [Mac](/index.php/Mac "Mac") da Apple (e por padrão) oferece suporte a seus próprios drivers de sistema de arquivos HFS+. As implementações da UEFI também suportam ISO-9660 para discos ópticos.

O UEFI inicia aplicativos EFI, por exemplo [gerenciadores de boot](#Gerenciador_de_boot), [Shell UEFI](/index.php/UEFI_shell "UEFI shell"), etc. Esses aplicativos geralmente são armazenados como arquivos na [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI"). Cada fornecedor pode armazenar seus arquivos na partição do sistema EFI sob a pasta `/EFI/*nome_fornecedor*`. Os aplicativos podem ser iniciados adicionando uma entrada de inicialização à NVRAM ou a partir do shell UEFI.

A especificação UEFI tem suporte para inicializar BIOS legado com sua [Compatibility Support Module (CSM)](https://en.wikipedia.org/wiki/pt:Unified_Extensible_Firmware_Interface#Compatibility_Support_Module "wikipedia:pt:Unified Extensible Firmware Interface"). Se o CSM estiver ativado no UEFI, o UEFI gerará entradas de inicialização do CSM para todas as unidades. Se uma entrada de inicialização do CSM for escolhida para ser inicializada, o CSM do UEFI tentará inicializar a partir do MBR da unidade.

## Inicialização do sistema

### Na BIOS

1.  Sistema ligado, o [power-on self-test (POST)](https://en.wikipedia.org/wiki/pt:Power_On_Self_Test "wikipedia:pt:Power On Self Test") (*autoteste de inicialização*) é executado.
2.  Após o POST, a BIOS inicializa o hardware necessário para inicializar (disco, controladores de teclado etc.).
3.  A BIOS inicia os primeiros 440 bytes ([a área de código de bootstrap do Master Boot Record](/index.php/Particionamento#Master_Boot_Record_(código_de_inicialização) "Particionamento")) do primeiro disco na ordem de disco da BIOS.
4.  O primeiro estágio do gerenciador de boot no código de inicialização da MBR, então, inicia o código de seu segundo estágio (se houver) de:
    *   próximos setores de disco após o MBR, ou seja, o chamado intervalo pós-MBR (somente em uma tabela de partição MBR).
    *   um [registro de inicialização de volume (VBR)](https://en.wikipedia.org/wiki/Volume_boot_record "wikipedia:Volume boot record") do disco com partição ou sem partição.
    *   a [partição de inicialização de BIOS](/index.php/Parti%C3%A7%C3%A3o_de_inicializa%C3%A7%C3%A3o_de_BIOS "Partição de inicialização de BIOS") ([GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") em BIOS/GPT somente).
5.  O atual [gerenciador de boot](#Gerenciador_de_boot) é iniciado.
6.  O gerenciador de boot carrega um sistema operacional por encadeamento ou diretamente o kernel do sistema operacional.

### No UEFI

1.  Sistema ligado, o [power-on self-test (POST)](https://en.wikipedia.org/wiki/pt:Power_On_Self_Test "wikipedia:pt:Power On Self Test") (*autoteste de inicialização*) é executado.
2.  Após o POST, o UEFI inicializa o hardware necessário para carregar o sistema (disco, controladores de teclado etc.).
3.  O firmware lê as entradas de inicialização na NVRAM para determinar qual aplicativo EFI deve ser iniciado e de onde (por exemplo, de qual disco e partição).
    *   Uma entrada de inicialização pode ser simplesmente um disco. Nesse caso, o firmware procura uma [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") nesse disco e tenta localizar o aplicativo EFI no caminho reserva de inicialização `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI` em [sistemas com um IA32 (32 bits)](/index.php/Unified_Extensible_Firmware_Interface#UEFI_firmware_bitness "Unified Extensible Firmware Interface")). É assim que as mídias removíveis inicializáveis UEFI funcionam.
4.  O firmware inicia o aplicativo EFI.
    *   Isso poderia ser um [gerenciador de boot](#Gerenciador_de_boot) ou o [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") do Arch usando [EFISTUB](/index.php/EFISTUB_(Portugu%C3%AAs) "EFISTUB (Português)")
    *   Ele poderia ser algum aplicativo EFI como um shell UEFI ou um [gerenciador de boot](#Gerenciador_de_boot), como [systemd-boot](/index.php/Systemd-boot "Systemd-boot") ou [rEFInd](/index.php/REFInd "REFInd").

Se [Secure Boot](/index.php/Secure_Boot "Secure Boot") estiver habilitado, o processo de inicialização vai verificar a autenticidade do binário EFI pela assinatura.

**Nota:** Alguns sistemas UEFI só podem inicializar a partir do caminho reserva de inicialização.

### Multiboot no UEFI

Como cada sistema operacional ou fornecedor pode manter seus próprios arquivos dentro da [partição de sistema EFI](/index.php/Parti%C3%A7%C3%A3o_de_sistema_EFI "Partição de sistema EFI") sem afetar o outro, a inicialização múltipla *(multi-booting)* usando UEFI é apenas uma questão de iniciar um aplicativo EFI diferente correspondente ao gerenciador de boot do sistema operacional específico. Isso elimina a necessidade de contar com mecanismos de [carregamento em cadeia](https://en.wikipedia.org/wiki/Chain_loading "wikipedia:Chain loading") de um [gerenciador de boot](#Gerenciador_de_boot) para carregar outro sistema operacional.

Veja também [Dual boot com Windows](/index.php/Dual_boot_with_Windows_(Portugu%C3%AAs) "Dual boot with Windows (Português)").

## Gerenciador de boot

Um gerenciador de boot é um peça de software iniciada pelo firmware ([BIOS](https://en.wikipedia.org/wiki/pt:BIOS "wikipedia:pt:BIOS") ou [UEFI](/index.php/UEFI "UEFI")). Ele é responsável por carregar o kernel com os [parâmetros do kernel](/index.php/Par%C3%A2metros_do_kernel "Parâmetros do kernel") desejados e o [disco de RAM inicial](/index.php/Mkinitcpio "Mkinitcpio") com base nos arquivos de configuração. No caso do UEFI, o kernel em si pode ser lançado diretamente pelo UEFI usando o stub de inicialização EFI. Um gerenciador de boot separado ainda pode ser usado para editar os parâmetros do kernel antes de inicializar.

**Atenção:** Um gerenciador de boot deve poder acessar as imagens do kernel e do initramfs, caso contrário, o sistema não inicializará. Portanto, em uma configuração típica, ele deve suportar o acesso a `/boot`. Isso significa que ele deve ter suporte a tudo, desde os dispositivos de bloco, dispositivos de bloco empilhados (LVM, RAID, dm-crypt, LUKS etc.) e terminando com o sistema de arquivos no qual residem o(s) kernel(s) e as imagens initramfs.

**Note:** Carregar atualizações de [microcódigo](/index.php/Microcode "Microcode") exige ajustes na configuração de gerenciador de boot. [[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

## Comparação de recursos

**Nota:**

*   Como o GPT é parte da especificação UEFI, todos os gerenciadores de boot UEFI oferecem suporte a discos GPT. O GPT em sistemas BIOS é possível, usando *hybrid booting* com [Hybrid MBR](https://www.rodsbooks.com/gdisk/hybrid.html) ("inicialização híbrida") ou o novo protocolo [somente GPT](http://repo.or.cz/syslinux.git/blob/HEAD:/doc/gpt.txt). Porém, esse protocolo pode causar problemas com certas implementações de BIOS; veja [rodsbooks](http://www.rodsbooks.com/gdisk/bios.html#bios) para mais detalhes.
*   A criptografia mencionada no suporte a sistema de arquivos é uma [criptografia a nível de sistema de arquivos](https://en.wikipedia.org/wiki/Filesystem-level_encryption "wikipedia:Filesystem-level encryption"), não influenciando [criptografia a nível de bloco](/index.php/Dm-crypt_(Portugu%C3%AAs) "Dm-crypt (Português)").

| Nome | Firmware | [Tabela de partição](/index.php/Tabela_de_parti%C3%A7%C3%A3o "Tabela de partição") | Multiboot | [Sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos") | Notas |
| BIOS | [UEFI](/index.php/UEFI "UEFI") | [MBR](/index.php/MBR_(Portugu%C3%AAs) "MBR (Português)") | [GPT](/index.php/GPT_(Portugu%C3%AAs) "GPT (Português)") | [Btrfs](/index.php/Btrfs "Btrfs") | [ext4](/index.php/Ext4_(Portugu%C3%AAs) "Ext4 (Português)") | ReiserFS | [VFAT](/index.php/VFAT "VFAT") | [XFS](/index.php/XFS "XFS") |
| [EFISTUB](/index.php/EFISTUB_(Portugu%C3%AAs) "EFISTUB (Português)") | – | Sim | Sim | Sim | – | – | – | – | Somente ESP | – | O kernel se tornou em um executável EFI para ser carregado diretamente do firmware [UEFI](/index.php/UEFI "UEFI") ou de outro gerenciado de boot. |
| [Clover](/index.php/Clover "Clover") | emula UEFI | Sim | Sim | Sim | Sim | Não | sem criptografia | Não | Sim | Não | Fork do rEFIt modificado para funcionar em [macOS em hardware que não seja da Apple](https://en.wikipedia.org/wiki/pt:Hackintosh "wikipedia:pt:Hackintosh"). |
| [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)") | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | Sim | No BIOS/GPT, configuração requer uma [partição de inicialização de BIOS](/index.php/Parti%C3%A7%C3%A3o_de_inicializa%C3%A7%C3%A3o_de_BIOS "Partição de inicialização de BIOS").
Possui suporte a RAID, LUKS1 e LVM (mas não volumes de provisionamento fino). |
| [rEFInd](/index.php/REFInd "REFInd") | Não | Sim | Sim | Sim | Sim | sem: criptografia, compressão zstd | sem criptografia | sem recurso de *tail-packing* | Sim | Não | Possui suporte a autodetecção de kernels e parâmetros sem configuração explícita. |
| [Syslinux](/index.php/Syslinux "Syslinux") | Sim | [Parcial](/index.php/Syslinux#Limitations_of_UEFI_Syslinux "Syslinux") | Sim | Sim | [Parcial](/index.php/Syslinux#Chainloading "Syslinux") | sem: volumes de vários dispositivos, compressão, criptografia | sem criptografia | Não | Sim | Somente MBR; sem nós-i esparsos | Sem suporte a certos recursos de [sistema de arquivos](/index.php/Sistema_de_arquivos "Sistema de arquivos") [[2]](https://wiki.syslinux.org/wiki/index.php?title=Filesystem)
Não tem drivers de sistema de arquivos[[3]](https://bugzilla.syslinux.org/show_bug.cgi?id=33), podendo acessar apenas o sistema de arquivos para o qual foi instalado. |
| [systemd-boot](/index.php/Systemd-boot "Systemd-boot") | Não | Sim | [Somente instalação manual](https://github.com/systemd/systemd/issues/1125) | Sim | Sim | Não | Não | Não | Somente ESP | Não | Não é possível iniciar binários de outras partições além da [ESP](/index.php/ESP_(Portugu%C3%AAs) "ESP (Português)"). |
| [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy") | Sim | Não | Sim | Não | Sim | Não | Não | Sim | Sim | Somente v4 | [Descontinuado](https://www.gnu.org/software/grub/grub-legacy.html) em favor do [GRUB](/index.php/GRUB_(Portugu%C3%AAs) "GRUB (Português)"). |
| [LILO](/index.php/LILO "LILO") | Sim | Não | Sim | Não | Sim | Não | sem criptografia | Sim | Sim | [Sim](http://xfs.org/index.php/XFS_FAQ#Q:_Does_LILO_work_with_XFS.3F) | [Descontinuado](http://web.archive.org/web/20180323163248/http://lilo.alioth.debian.org/) em razão de limitações (p.ex., com Btrfs, GPT, RAID). |

1.  Um [gerenciador de boot](https://www.rodsbooks.com/efi-bootloaders/principles.html). Ele só pode iniciar outros aplicativos EFI, por exemplo, imagens de kernel do Linux criadas com `CONFIG_EFI_STUB=y` e Windows `bootmgfw.efi`.

Veja também [Wikipedia:Comparison of boot loaders](https://en.wikipedia.org/wiki/Comparison_of_boot_loaders "wikipedia:Comparison of boot loaders").

## Kernel

O [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") é o núcleo de um sistema operacional. Ele funciona em um baixo nível (*kernelspace* ou espaço de kernel) interagindo entre o hardware da máquina e os programas que usam o hardware para funcionar. O kernel interrompe temporariamente os programas para executar outros programas, entretanto, conhecido como [preemptividade ou preempção](https://en.wikipedia.org/wiki/pt:Preemptividade "wikipedia:pt:Preemptividade"). Isso cria a ilusão de muitas tarefas sendo executadas simultaneamente, mesmo em CPUs de núcleo único. O kernel usa o agendador da CPU para decidir qual programa tem prioridade a qualquer momento.

Para fazer uso eficiente da CPU, o kernel usa um agendador para arbitrar quais tarefas têm prioridade em qualquer momento, criando a ilusão de que muitas tarefas são executadas simultaneamente.

## initramfs

Depois que o [gerenciador de boot](#Gerenciador_de_boot) carrega o [kernel](/index.php/Kernel_(Portugu%C3%AAs) "Kernel (Português)") e os possíveis arquivos initramfs e executa o kernel, o kernel extrai os arquivos initramfs (sistema de arquivos RAM inicial) no (então vazio) rootfs (sistema de arquivos raiz inicial, especificamente um ramfs ou tmpfs). O primeiro initramfs extraído é aquele embutido no binário do kernel durante a construção do kernel, então os possíveis arquivos initramfs externos são extraídos. Assim, os arquivos no initramfs externo sobrescrevem arquivos com o mesmo nome no initramfs incorporado. O kernel então executa `/init` (no rootfs) como o primeiro processo. O *early userspace* é iniciado.

O Arch Linux usa um arquivo vazio para o initramfs incorporado (que é o padrão ao construir o Linux). Veja [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") para mais informações específicas do Arch sobre o initramfs externo.

Depois que o kernel é carregado, ele descompacta o [initramfs](/index.php/Initramfs_(Portugu%C3%AAs) "Initramfs (Português)") (sistema de arquivos RAM inicial ou ***init**ial **RAM** **f**ile**s**ystem*), que se torna o sistema de arquivos raiz inicial. O kernel então executa `/init` como o primeiro processo. O *early userspace* é iniciado.

O objetivo do initramfs é inicializar o sistema até o ponto em que ele pode acessar o sistema de arquivos raiz (consulte [FHS](/index.php/FHS_(Portugu%C3%AAs) "FHS (Português)") para obter detalhes). Isso significa que quaisquer módulos necessários para dispositivos como IDE, SCSI, SATA, USB/FW (se inicializando de uma unidade externa) devem poder ser carregados a partir do initramfs, se não estiverem embutidos no kernel; uma vez que os módulos apropriados são carregados (seja explicitamente através de um programa ou script, ou implicitamente via [udev](/index.php/Udev "Udev")), o processo de inicialização continua. Por esse motivo, o initramfs precisa apenas conter os módulos necessários para acessar o sistema de arquivos raiz; não precisa conter todos os módulos que alguém desejaria usar. A maioria dos módulos será carregada mais tarde pelo udev, durante o processo de inicialização.

## Processo init

No estágio final do início do espaço de usuário, a raiz real é montada e, em seguida, substitui o sistema de arquivos raiz inicial. `/sbin/init` é executado, substituindo o processo `/init`. Arch usa [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") como o [init](/index.php/Init "Init") padrão.

## getty

[init](/index.php/Init "Init") chama [getty](/index.php/Getty "Getty") uma vez para cada [terminal virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (geralmente seis deles), que inicializa cada tty e solicita um nome de usuário e senha. Uma vez que o nome de usuário e a senha são fornecidos, o getty os verifica em `/etc/passwd` e `/etc/shadow`, depois chama [login](#Login). Alternativamente, o getty pode iniciar um gerenciador de exibição se houver um presente no sistema.

## Gerenciador de exibição

Um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") pode ser configurado para substituir o prompt de login do getty em um tty.

Para inicializar automaticamente um gerenciador de exibição após a inicialização, é necessário ativar manualmente a unidade de serviço através de [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)"). Para obter mais informações sobre como ativar e iniciar unidades de serviço, consulte [systemd (Português)#Usando units](/index.php/Systemd_(Portugu%C3%AAs)#Usando_units "Systemd (Português)").

## Login

O programa *login* começa uma sessão para o usuário definindo as variáveis de ambiente e iniciando o shell do usuário, com base no `/etc/passwd`.

O programa *login* exibe o conteúdo de [/etc/motd](https://en.wikipedia.org/wiki/pt:motd_(Unix) (*m*essage *o*f *t*he *d*ay ou, em português, mensagem do dia) após um login bem sucedido, logo antes dele executar o shell de login. É um bom lugar para exibir seus *Terms of Service* (Termos de Serviços) para lembrar seus usuários de suas políticas locais ou qualquer outra coisa que você deseje falar para eles.

## Shell

Uma vez iniciado o [shell](/index.php/Shell_(Portugu%C3%AAs) "Shell (Português)") do usuário, ele normalmente executará um arquivo de configuração de tempo de execução, como o [bashrc](/index.php/Bashrc "Bashrc"), antes de apresentar um prompt ao usuário. Se a conta estiver configurada para [iniciar X no login](/index.php/Iniciar_X_no_login "Iniciar X no login"), o arquivo de configuração de tempo de execução chamará [startx](/index.php/Startx_(Portugu%C3%AAs) "Startx (Português)") ou [xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)").

## GUI, xinit ou wayland

[xinit](/index.php/Xinit_(Portugu%C3%AAs) "Xinit (Português)") executa o arquivo de configuração de tempo de execução [xinitrc](/index.php/Xinitrc_(Portugu%C3%AAs) "Xinitrc (Português)") do usuário, que normalmente inicia um [gerenciador de janelas](/index.php/Gerenciador_de_janela "Gerenciador de janela"). Quando o usuário terminar e sair do gerenciador de janelas, *xinit*, *startx*, o shell e o login serão encerrados nessa ordem, retornando ao [getty](#getty).

## Veja também

*   [Early Userspace in Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:pt:initrd](https://en.wikipedia.org/wiki/pt:initrd "wikipedia:pt:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
*   [Kernel Newbie Corner: initrd and initramfs](https://www.linux.com/learn/kernel-newbie-corner-initrd-and-initramfs-whats)
*   [Rod Smith - Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/)