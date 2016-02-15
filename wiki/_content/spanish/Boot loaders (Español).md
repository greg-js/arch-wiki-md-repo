**Estado de la traducción:** este artículo es una versión traducida de [Boot loaders](/index.php/Boot_loaders "Boot loaders"). Fecha de la última traducción/revisión: **2015-07-01**. Puedes ayudar a actualizar la traducción, si adviertes que la versión inglesa ha cambiado: [ver cambios](https://wiki.archlinux.org/index.php?title=Boot_loaders&diff=0&oldid=379913).

El gestor de arranque es la primera pieza de software iniciada por la [BIOS](https://en.wikipedia.org/wiki/es:BIOS "wikipedia:es:BIOS") o [UEFI](/index.php/UEFI "UEFI"). Es responsable de cargar el kérnel con sus [parámetros](/index.php/Kernel_parameters_(Espa%C3%B1ol) "Kernel parameters (Español)"), y la [imagen RAM inicial](/index.php/Mkinitcpio_(Espa%C3%B1ol) "Mkinitcpio (Español)") antes de iniciar el [proceso de arranque](/index.php/Arch_boot_process_(Espa%C3%B1ol) "Arch boot process (Español)"). Se pueden utilizar [diferentes tipos](/index.php/Category:Boot_loaders_(Espa%C3%B1ol) "Category:Boot loaders (Español)") de gestores de arranque en Arch, como [GRUB (Español)](/index.php/GRUB_(Espa%C3%B1ol) "GRUB (Español)") y [Syslinux (Español)](/index.php/Syslinux_(Espa%C3%B1ol) "Syslinux (Español)"). Algunos gestores de arranque solo admiten arrancar desde BIOS o UEFI y otros soportan ambos.

Esta página contiene una breve introducción sobre los gestores de arranque disponibles en Arch. Para obtener información detallada, consulte las páginas correspondientes de cada gestor de arranque.

**Nota:** Para cargar las actualizaciones de [Microcode](/index.php/Microcode "Microcode") hay que realizar ajustes en la configuración del gestor de arranque. [[1]](https://www.archlinux.org/news/changes-to-intel-microcodeupdates/)

## Contents

*   [1 Gestores de arranque tanto para BIOS como para UEFI](#Gestores_de_arranque_tanto_para_BIOS_como_para_UEFI)
    *   [1.1 GRUB](#GRUB)
    *   [1.2 Syslinux](#Syslinux)
    *   [1.3 BURG](#BURG)
*   [2 Gestores de arranque solo para UEFI](#Gestores_de_arranque_solo_para_UEFI)
    *   [2.1 Linux Kernel EFISTUB](#Linux_Kernel_EFISTUB)
        *   [2.1.1 systemd-boot](#systemd-boot)
        *   [2.1.2 Gummiboot](#Gummiboot)
        *   [2.1.3 rEFInd](#rEFInd)
        *   [2.1.4 Clover](#Clover)
    *   [2.2 ELILO](#ELILO)
*   [3 Gestores de arranque solo para BIOS](#Gestores_de_arranque_solo_para_BIOS)
    *   [3.1 GRUB Legacy](#GRUB_Legacy)
    *   [3.2 LILO](#LILO)
    *   [3.3 NeoGRUB](#NeoGRUB)
*   [4 Véase también](#V.C3.A9ase_tambi.C3.A9n)

## Gestores de arranque tanto para BIOS como para UEFI

### GRUB

[GRUB](/index.php/GRUB "GRUB") es un gestor de arranque rico en características y es compatible con escenarios más complejos. Su archivo de configuración es más similar al lenguaje de script de 'sh' y se puede generar de forma automática.

### Syslinux

[Syslinux](/index.php/Syslinux "Syslinux") se limita (actualmente) a cargar solo los archivos desde la partición donde se instaló. Un ejemplo de configuración se puede encontrar en [Syslinux#Examples](/index.php/Syslinux#Examples "Syslinux").

### BURG

**Nota:** BURG no está apoyado oficialmente por los desarrolladores de Arch.

Véase [BURG](/index.php/BURG "BURG").

## Gestores de arranque solo para UEFI

### Linux Kernel EFISTUB

El kérnel de Linux puede arrancar directamente por medio del cargador minimalista EFI integrado. Véase [EFISTUB](/index.php/EFISTUB "EFISTUB").

#### systemd-boot

systemd incluye un gestor de arranque EFI desde de la versión 220\. Es esencialmente igual que [Gummiboot](/index.php/Gummiboot "Gummiboot"), siendo la órden base `bootctl` en lugar de `gummiboot`.

#### Gummiboot

Gummiboot es un gestor de arranque UEFI que proporciona un menú de texto para arrancar los kérnel EFISTUB. Véase [Gummiboot](/index.php/Gummiboot "Gummiboot").

#### rEFInd

rEFInd es un gestor de arranque UEFI que ofrece un menú gráfico para arrancar los kérnel EFISTUB. Véase [rEFInd](/index.php/REFInd "REFInd").

#### Clover

Clover es un gestor de arranque UEFI, que ofrece una interfaz de resolución nativa para arrancar los kérnel EFISTUB. Véase [Clover](/index.php/Clover "Clover").

### ELILO

**Advertencia:** El desarrollo de ELILO ya no está activo, es decir, no se añadirán nuevas características y correcciones de errores a las versiones ya liberados. Véase [https://sourceforge.net/mailarchive/message.php?msg_id=31524008](https://sourceforge.net/mailarchive/message.php?msg_id=31524008) para más información. ELILO no está oficialmente apoyada por los desarrolladores de Arch.

ELILO es la versión para UEFI de [LILO](/index.php/LILO "LILO") solo para BIOS. Su archivo de configuración `elilo.conf` es similar al archivo de configuración de [LILO](/index.php/LILO "LILO"). Los desarrolladores proporcionan ejecutables compilados disponibles en [http://sourceforge.net/projects/elilo/](http://sourceforge.net/projects/elilo/) y un paquete [elilo-efi](https://aur.archlinux.org/packages/elilo-efi/) en AUR.

## Gestores de arranque solo para BIOS

**Advertencia:** Ninguna de las opciones que se presentan aquí son oficialmente soportados en Arch Linux.

### GRUB Legacy

GRUB Legacy (también conocido como grub-0.97), es el antecedente de [GRUB](/index.php/GRUB "GRUB"), una rama solo para BIOS. Véase [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

### LILO

Véase [LILO](/index.php/LILO "LILO").

### NeoGRUB

NeoGRUB proporciona un medio para arrancar Arch desde el gestor de arranque de Windows sin necesidad de instalar un gestor de arranque adicional. Véase [NeoGRUB](/index.php/NeoGRUB "NeoGRUB").

Arrancar Arch desde NeoGRUB no ha sido probado aún en Windows 8 y/o sistemas UEFI.

## Véase también

*   [Rod Smith - Managing EFI Boot Loaders for Linux](http://www.rodsbooks.com/efi-bootloaders/)
*   [Rod Smith - rEFInd, a fork or rEFIt](http://www.rodsbooks.com/refind/)
*   [Linux Kernel Documentation on EFISTUB](https://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=blob_plain;f=Documentation/x86/efi-stub.txt;hb=HEAD)
*   [Linux Kernel EFISTUB Git Commit](http://git.kernel.org/?p=linux/kernel/git/torvalds/linux.git;a=commitdiff;h=291f36325f9f252bd76ef5f603995f37e453fc60;hp=55839d515495e766605d7aaabd9c2758370a8d27)
*   [Rod Smith's page on EFISTUB](http://www.rodsbooks.com/efi-bootloaders/efistub.html)
*   [rEFInd Documentation for booting EFISTUB Kernels](http://www.rodsbooks.com/refind/linux.html)