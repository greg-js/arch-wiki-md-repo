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

Para inicializar o Arch Linux, um [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot") capaz de Linux, tal como [GRUB](/index.php/GRUB "GRUB") ou [Syslinux](/index.php/Syslinux "Syslinux"), deve ser instalado no [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") ou no [GUID Partition Table](/index.php/GUID_Partition_Table "GUID Partition Table"). O gerenciador de boot é responsável por carregar o kernel e [initial ramdisk](/index.php/Initial_ramdisk "Initial ramdisk") antes de inicializar o processo de inicialização. O procedimento é bem diferente para for sistemas [BIOS](https://en.wikipedia.org/wiki/pt:BIOS "wikipedia:pt:BIOS") e [UEFI](/index.php/UEFI "UEFI"), a descrição detalhada é dada nessa ou páginas vinculadas.

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
    *   [9.1 Mensagem do dia](#Mensagem_do_dia)
*   [10 Shell](#Shell)
*   [11 xinit](#xinit)
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

1.  Sistema ligado - processo de POST ou [Power-on self-test](https://en.wikipedia.org/wiki/pt:Power_On_Self_Test "wikipedia:pt:Power On Self Test") (tradução livre: *autoteste de inicialização*)
2.  Após o POST, a BIOS inicializa o hardware de sistema necessário para inicializar (disco, controladores de teclado etc.)
3.  A BIOS inicia os primeiros 440 bytes ([Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record")) do primeiro disco na ordem de disco da BIOS
4.  O código de inicialização da MBR, então, toma controle da BIOS e inicia o código de seu próximo estágio (se houver) (em sua maioria, código do [gerenciador de boot](/index.php/Gerenciador_de_boot "Gerenciador de boot"))
5.  O gerenciador de boot lançado

### No UEFI

1.  Sistema ligado. O *Power On Self Test (POST)* é executado.
2.  O firmware UEFI é carregado. O firmware inicializa o hardware necessário para inicializar.
3.  O firmware lê as entradas de inicialização no gerenciador de boot para determinar qual aplicativo UEFI deve ser iniciado e de onde (por exemplo, de qual disco e partição).
4.  O firmware inicia o aplicativo UEFI.
    *   Isso poderia ser o próprio kernel do Arch (já que [EFISTUB](/index.php/EFISTUB "EFISTUB") está habilitado por padrão).
    *   Isso poderia ser algum aplicativo como um shell ou um gerenciador de boot gráfico.
    *   Ou a entrada de inicialização poderia simplesmente ser um disco. Neste caso, o firmware procura por uma [Partição de Sistema EFI](/index.php/EFI_System_Partition "EFI System Partition") naquele disco e tenta executar o aplicativo reserva EFI `\EFI\BOOT\BOOTX64.EFI` (`BOOTIA32.EFI` em [sistemas EFI de 32 bits](/index.php/Unified_Extensible_Firmware_Interface#UEFI_firmware_bitness "Unified Extensible Firmware Interface")). É assim que pendrive UEFI inicializável funciona.

Se [Secure Boot](/index.php/Secure_Boot "Secure Boot") estiver habilitado, o processo de inicialização vai verificar a autenticidade do binário EFI pela assinatura.

**Nota:** em alguns sistemas UEFI (mal desenhados), a única forma de inicializar é usando uma entrada de boot de disco com o caminho reserva de aplicativo UEFI.

### Multiboot no UEFI

Since each OS or vendor can maintain its own files within the EFI System Partition without affecting the other, multi-booting using UEFI is just a matter of launching a different UEFI application corresponding to the particular OS's bootloader. This removes the need for relying on chainloading mechanisms of one [boot loader](/index.php/Boot_loader "Boot loader") to load another OS.

See also [Dual boot with Windows](/index.php/Dual_boot_with_Windows "Dual boot with Windows").

## Gerenciadores de boot

The [boot loader](/index.php/Boot_loader "Boot loader") is the first piece of software started by the [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") or [UEFI](/index.php/UEFI "UEFI"). It is responsible for loading the kernel with the wanted [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"), and [initial RAM disk](/index.php/Mkinitcpio "Mkinitcpio") based on config files.

## Kernel

The [kernel](/index.php/Kernel "Kernel") is the core of an operating system. It functions on a low level (*kernelspace*) interacting between the hardware of the machine and the programs which use the hardware to run. To make efficient use of the CPU, the kernel uses a scheduler to arbitrate which tasks take priority at any given moment, creating the illusion of many tasks being executed simultaneously.

## initramfs

After the kernel is loaded, it unpacks the [initramfs](/index.php/Initramfs "Initramfs") (initial RAM filesystem), which becomes the initial root filesystem. The kernel then executes `/init` as the first process. The *early userspace* starts.

The purpose of the initramfs is to bootstrap the system to the point where it can access the root filesystem (see [FHS](/index.php/FHS "FHS") for details). This means that any modules that are required for devices like IDE, SCSI, SATA, USB/FW (if booting from an external drive) must be loadable from the initramfs if not built into the kernel; once the proper modules are loaded (either explicitly via a program or script, or implicitly via [udev](/index.php/Udev "Udev")), the boot process continues. For this reason, the initramfs only needs to contain the modules necessary to access the root filesystem; it does not need to contain every module one would ever want to use. The majority of modules will be loaded later on by udev, during the init process.

## Processo init

At the final stage of early userspace, the real root is mounted, and then replaces the initial root filesystem. `/sbin/init` is executed, replacing the `/init` process. Arch uses [systemd](/index.php/Systemd "Systemd") as the default [init](/index.php/Init "Init").

## Getty

[init](/index.php/Init "Init") calls [getty](/index.php/Getty "Getty") once for each [virtual terminal](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") (typically six of them), which initializes each tty and asks for a username and password. Once the username and password are provided, getty checks them against `/etc/passwd` and `/etc/shadow`, then calls [login](#Login). Alternatively, getty may start a display manager if one is present on the system.

## Gerenciador de exibição

A [display manager](/index.php/Display_manager "Display manager") can be configured to replace the getty login prompt on a tty.

## Login

The *login* program begins a session for the user by setting environment variables and starting the user's shell, based on `/etc/passwd`.

### Mensagem do dia

The *login* program displays the contents of [/etc/motd](https://en.wikipedia.org/wiki/motd_(Unix) (*m*essage *o*f *t*he *d*ay) after a successful login, just before it executes the login shell.

It is a good place to display your Terms of Service to remind users of your local policies or anything you wish to tell them.

## Shell

Once the user's [shell](/index.php/Shell "Shell") is started, it will typically run a runtime configuration file, such as [bashrc](/index.php/Bashrc "Bashrc"), before presenting a prompt to the user. If the account is configured to [Start X at login](/index.php/Start_X_at_login "Start X at login"), the runtime configuration file will call [startx](/index.php/Startx "Startx") or [xinit](/index.php/Xinit "Xinit").

## xinit

[xinit](/index.php/Xinit "Xinit") runs the user's [xinitrc](/index.php/Xinitrc "Xinitrc") runtime configuration file, which normally starts a [window manager](/index.php/Window_manager "Window manager"). When the user is finished and exits the window manager, xinit, startx, the shell, and login will terminate in that order, returning to getty.

## Veja também

*   [Early Userspace in Arch Linux](https://web.archive.org/web/20150430223035/http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")
*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [NeoSmart: The BIOS/MBR Boot Process](https://neosmart.net/wiki/mbr-boot-process/)
*   [Kernel Newbie Corner: initrd and initramfs](https://www.linux.com/learn/kernel-newbie-corner-initrd-and-initramfs-whats)