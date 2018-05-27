Artigos relacionados

*   [Gerenciadores de boot](/index.php/Gerenciadores_de_boot "Gerenciadores de boot")
*   [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")
*   [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table")
*   [Unified Extensible Firmware Interface](/index.php/Unified_Extensible_Firmware_Interface "Unified Extensible Firmware Interface")
*   [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")
*   [init](/index.php/Init "Init")
*   [systemd (Português)](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)")
*   [fstab](/index.php/Fstab "Fstab")
*   [Autostarting](/index.php/Autostarting "Autostarting")

Para usar o Arch Linux, são executados vários softwares chamados "inicialização" ou *"booting"*. Ao ligar o hardware, seu firmware é executado. Ele chama o gerenciador de boot que, por sua vez, executa o kernel Linux. O kernel inicia um processo init que executa programas de espaço de usuário *(userspace)* dependendo de como o sistema está configurado. Dois tipos principais existem [UEFI](/index.php/UEFI "UEFI") e [BIOS](https://en.wikipedia.org/wiki/pt:BIOS "wikipedia:pt:BIOS").

## Contents

*   [1 Tipos de firmware](#Tipos_de_firmware)
    *   [1.1 BIOS](#BIOS)
    *   [1.2 UEFI](#UEFI)
*   [2 Inicialização do sistema](#Inicializa.C3.A7.C3.A3o_do_sistema)
    *   [2.1 Na BIOS](#Na_BIOS)
    *   [2.2 No UEFI](#No_UEFI)
    *   [2.3 Multiboot no UEFI](#Multiboot_no_UEFI)
*   [3 Gerenciadores de boot](#Gerenciadores_de_boot)
*   [4 Kernel](#Kernel)
*   [5 initramfs](#initramfs)
*   [6 Processo init](#Processo_init)
*   [7 Getty](#Getty)
*   [8 Gerenciador de exibição](#Gerenciador_de_exibi.C3.A7.C3.A3o)
*   [9 Login](#Login)
*   [10 Shell](#Shell)
*   [11 GUI, xinit ou wayland](#GUI.2C_xinit_ou_wayland)
*   [12 Veja também](#Veja_tamb.C3.A9m)

## Tipos de firmware

### BIOS

Uma [BIOS](https://en.wikipedia.org/wiki/pt:BIOS "wikipedia:pt:BIOS") (acrônimo para *Basic Input-Output System*) é o primeiro programa (firmware) que é executado assim que o sistema é ligado. Na maioria dos casos, é armazenado em uma memória flash na própria placa-mãe e é independente do armazenamento do sistema.

O BIOS carrega os 512 bytes iniciais ([Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")) do primeiro disco válido na ordem de disco do BIOS. Destes 512 bytes, o primeiro 440 contém o primeiro estágio de um [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot"), como [GRUB](/index.php/GRUB "GRUB"), [Syslinux](/index.php/Syslinux "Syslinux") ou [LILO](/index.php/LILO "LILO"). Uma vez que muito pouco pode ser alcançado por um programa deste tamanho, o segundo estágio (que reside nos próximos setores do disco) é carregado a partir daqui e procura um arquivo armazenado na própria partição (o gerenciador de boot real). Isso, então, carrega um sistema operacional carregando em cadeia ou carregando diretamente o kernel do sistema operacional.

### UEFI

O UEFI tem suporte para ler a tabela de partições, bem como entender os sistemas de arquivos. Portanto, ele não é limitado pela limitação de código de 440 bytes (código de inicialização do MBR) como nos sistemas BIOS. Ele não usa o código de inicialização do MBR.

Os firmwares UEFI comumente usados oferecem suporte a MBR e GPT [tabela de partições](/index.php/Partition_table "Partition table"). EFI em Apple-Intel Macs são conhecidos por também ter suporte ao Apple Partition Map, além de MBR e GPT. A maioria dos firmwares da UEFI tem suporte para acessar sistemas de arquivos FAT12 (disquetes), FAT16 e FAT32 em HDDs e ISO9660 (e UDF) em CD/DVDs. O EFI em Intel Macs também pode acessar sistemas de arquivos HFS/HFS+, além dos mencionados.

O UEFI não inicia nenhum código de inicialização no MBR, independentemente de existir ou não. Em vez disso, ele usa uma partição especial na tabela de partição chamada [Partição de Sistema EFI](/index.php/EFI_System_Partition "EFI System Partition") na qual os arquivos que precisam ser lançados pelo firmware são armazenados. Cada fornecedor pode armazenar seus arquivos na pasta `<PARTIÇÃO DE SISTEMA EFI>/EFI/<NOME DO FORNECEDOR>/` e pode usar o firmware ou seu shell ([UEFI](/index.php/Unified_Extensible_Firmware_Interface#Shell_UEFI "Unified Extensible Firmware Interface")) para iniciar o programa de inicialização. Uma partição do sistema EFI geralmente é formatada como [FAT32](/index.php/FAT32 "FAT32") ou (menos comumente) FAT16.

## Inicialização do sistema

### Na BIOS

1.  Sistema ligado - processo de POST ou [Power-on self-test](https://en.wikipedia.org/wiki/pt:Power_On_Self_Test "wikipedia:pt:Power On Self Test") (tradução livre: *autoteste de inicialização*).
2.  Após o POST, a BIOS inicializa o hardware de sistema necessário para inicializar (disco, controladores de teclado etc.).
3.  A BIOS inicia os primeiros 440 bytes ([Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")) do primeiro disco na ordem de disco da BIOS.
4.  O código de inicialização da MBR, então, toma controle da BIOS e inicia o código de seu próximo estágio (se houver) (em sua maioria, código do [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot")).
5.  O [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot"), como o [GRUB](/index.php/GRUB "GRUB") e [Syslinux](/index.php/Syslinux "Syslinux"), é iniciado

### No UEFI

1.  Sistema ligado. O *Power On Self Test (POST)* é executado.
2.  O firmware UEFI é carregado. O firmware inicializa o hardware necessário para inicializar.
3.  O firmware lê as entradas de inicialização no gerenciador de boot para determinar qual aplicativo UEFI deve ser iniciado e de onde (por exemplo, de qual disco e partição). Uma entrada de inicialização pode ser simplesmente um disco. Nesse caso, o firmware procura uma [Partição de Sistema EFI](/index.php/EFI_System_Partition "EFI System Partition") nesse disco e tenta localizar o aplicativo UEFI de reserva `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI` em [sistemas EFI de 32 bits](/index.php/Unified_Extensible_Firmware_Interface#UEFI_firmware_bitness "Unified Extensible Firmware Interface")). É assim que os pendrives USB inicializáveis por UEFI funcionam.
4.  O firmware inicia o aplicativo UEFI.
    *   Isso poderia ser um gerenciador de boot, como o kernel do Arch (já que [EFISTUB](/index.php/EFISTUB "EFISTUB") está habilitado por padrão).
    *   Isso poderia ser algum aplicativo como um shell ou um gerenciador de boot, como [systemd-boot](/index.php/Systemd-boot "Systemd-boot"), [rEFInd](/index.php/REFInd "REFInd")..

Se [Secure Boot](/index.php/Secure_Boot "Secure Boot") estiver habilitado, o processo de inicialização vai verificar a autenticidade do binário EFI pela assinatura.

**Nota:** Alguns sistemas UEFI têm um gerenciador de boot bem básico, que podem usar o caminho reserva de aplicativo UEFI.

### Multiboot no UEFI

Como cada sistema operacional ou fornecedor pode manter seus próprios arquivos dentro da Partição de Sistema EFI sem afetar o outro, a inicialização múltipla *(multi-booting)* usando UEFI é apenas uma questão de iniciar um aplicativo UEFI diferente correspondente ao gerenciador de boot do sistema operacional específico. Isso elimina a necessidade de contar com mecanismos de carregamento em cadeia de um [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") para carregar outro sistema operacional.

Veja também [Dual boot com Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## Gerenciadores de boot

O [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") é o primeiro software iniciado pela [BIOS](https://en.wikipedia.org/wiki/pt:BIOS "wikipedia:pt:BIOS") ou pelo [UEFI](/index.php/UEFI "UEFI"). Ele é responsável por carregar o kernel com os [parâmetros de kernel](/index.php/Kernel_parameters "Kernel parameters") desejados e o [disco de RAM inicial](/index.php/Mkinitcpio "Mkinitcpio") com base nos arquivos de configuração.

## Kernel

O [kernel](/index.php/Kernel "Kernel") é o núcleo de um sistema operacional. Ele funciona em um baixo nível (*kernelspace* ou espaço de kernel) interagindo entre o hardware da máquina e os programas que usam o hardware para funcionar. Para fazer uso eficiente da CPU, o kernel usa um agendador para arbitrar quais tarefas têm prioridade em qualquer momento, criando a ilusão de que muitas tarefas são executadas simultaneamente.

## initramfs

Depois que o kernel é carregado, ele descompacta o [initramfs](/index.php/Initramfs "Initramfs") (sistema de arquivos RAM inicial ou ***init**ial **RAM** **f**ile**s**ystem*), que se torna o sistema de arquivos raiz inicial. O kernel então executa `/init` como o primeiro processo. O *early userspace* é iniciado.

O objetivo do initramfs é inicializar o sistema até o ponto em que ele pode acessar o sistema de arquivos raiz (consulte [FHS](/index.php/FHS_(Portugu%C3%AAs) "FHS (Português)") para obter detalhes). Isso significa que quaisquer módulos necessários para dispositivos como IDE, SCSI, SATA, USB/FW (se inicializando de uma unidade externa) devem poder ser carregados a partir do initramfs, se não estiverem embutidos no kernel; uma vez que os módulos apropriados são carregados (seja explicitamente através de um programa ou script, ou implicitamente via [udev](/index.php/Udev "Udev")), o processo de inicialização continua. Por esse motivo, o initramfs precisa apenas conter os módulos necessários para acessar o sistema de arquivos raiz; não precisa conter todos os módulos que alguém desejaria usar. A maioria dos módulos será carregada mais tarde pelo udev, durante o processo de inicialização.

## Processo init

No estágio final do início do espaço de usuário, a raiz real é montada e, em seguida, substitui o sistema de arquivos raiz inicial. `/sbin/init` é executado, substituindo o processo `/init`. Arch usa [systemd](/index.php/Systemd_(Portugu%C3%AAs) "Systemd (Português)") como o [init](/index.php/Init "Init") padrão.

## Getty

[init](/index.php/Init "Init") chama [getty](/index.php/Getty "Getty") uma vez para cada [terminal virtual](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (geralmente seis deles), que inicializa cada tty e solicita um nome de usuário e senha. Uma vez que o nome de usuário e a senha são fornecidos, o getty os verifica em `/etc/passwd` e `/etc/shadow`, depois chama [login](#Login). Alternativamente, o getty pode iniciar um gerenciador de exibição se houver um presente no sistema.

## Gerenciador de exibição

Um [gerenciador de exibição](/index.php/Gerenciador_de_exibi%C3%A7%C3%A3o "Gerenciador de exibição") pode ser configurado para substituir o prompt de login do getty em um tty.

## Login

The *login* program begins a session for the user by setting environment variables and starting the user's shell, based on `/etc/passwd`.

The *login* program displays the contents of [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (*m*essage *o*f *t*he *d*ay) after a successful login, just before it executes the login shell. It is a good place to display your Terms of Service to remind users of your local policies or anything you wish to tell them.

## Shell

Once the user's [shell](/index.php/Shell "Shell") is started, it will typically run a runtime configuration file, such as [bashrc](/index.php/Bashrc "Bashrc"), before presenting a prompt to the user. If the account is configured to [Start X at login](/index.php/Start_X_at_login "Start X at login"), the runtime configuration file will call [startx](/index.php/Startx "Startx") or [xinit](/index.php/Xinit "Xinit").

## GUI, xinit ou wayland

[xinit](/index.php/Xinit "Xinit") runs the user's [xinitrc](/index.php/Xinitrc "Xinitrc") runtime configuration file, which normally starts a [window manager](/index.php/Window_manager "Window manager"). When the user is finished and exits the window manager, xinit, startx, the shell, and login will terminate in that order, returning to getty.

## Veja também

*   [Early Userspace in Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
*   [Kernel Newbie Corner: initrd and initramfs](https://www.linux.com/learn/kernel-newbie-corner-initrd-and-initramfs-whats)