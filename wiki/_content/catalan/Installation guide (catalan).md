Aquest document et guiarà en el procés d'instal·lació de [Arch Linux](/index.php/Arch_Linux "Arch Linux") des del sistema d'arranc de la imatge oficial. Abans de començar la instal·lació et recomanem que passis per la pàgina de preguntes freqüents [FAQ](/index.php/FAQ "FAQ").

La comunitat-mantenidora [Arch wiki](/index.php/Main_page "Main page") és un recurs excelent i hauria de ser consultat primerament. El canal [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC") ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)) juntament amb els [forums](https://bbs.archlinux.org/) estàn a disposició, si no pots trobar la resposta al teu problema enlloc més. Pensa també a consultar els manuals `man`. Pots consultar un manual sobre una comanda/paquet amb `man *commanda*`.

## Contents

*   [1 Descàrrega](#Desc.C3.A0rrega)
*   [2 Instal·lació](#Instal.C2.B7laci.C3.B3)
    *   [2.1 Distribució del teclat](#Distribuci.C3.B3_del_teclat)
    *   [2.2 Partició de disc](#Partici.C3.B3_de_disc)
    *   [2.3 Format the partitions](#Format_the_partitions)
    *   [2.4 Mount the partitions](#Mount_the_partitions)
    *   [2.5 Connect to the internet](#Connect_to_the_internet)
        *   [2.5.1 Wireless](#Wireless)
    *   [2.6 Install the base system](#Install_the_base_system)
    *   [2.7 Configure the system](#Configure_the_system)
    *   [2.8 Install and configure a boot loader](#Install_and_configure_a_boot_loader)
    *   [2.9 Unmount and reboot](#Unmount_and_reboot)
*   [3 Post-installation](#Post-installation)
    *   [3.1 User management](#User_management)
    *   [3.2 Package management](#Package_management)
    *   [3.3 Service management](#Service_management)
    *   [3.4 Sound](#Sound)
    *   [3.5 Display server](#Display_server)
    *   [3.6 Fonts](#Fonts)
*   [4 Appendix](#Appendix)

## Descàrrega

Descarrega la darrera ISO de Arch Linux des de [Arch Linux download page](https://www.archlinux.org/download/).

*   La imatge descarregada és un sistema arrencable des d'arquitectures i686 i x86_64 per a instal·lar Arch Linux per la xarxa. Ja no hi ha imatges ISO disponibles que contenguin el repositori [core], per tant es necessària una connexió a internet per a la instal·lació.
*   Les imatges de instal·lació tenen signatura digital. Es recomanable verificar la imatge abans del seu ús. Això es pot fer descarregant l'arxiu *.sig* de la pàgina de descarrega (o des de un dels mirrors) i després comprovar la signatura PGP amb `pacman-key -v *iso-file*.sig` o les sumes md5 amb `md5sum *iso-file*.iso`.
*   La imatge pot esser gravada a un CD, com a arxiu ISO, o també se pot [escriure a un llapis USB](/index.php/USB_Installation_Media "USB Installation Media"). Aquest procediment es només per a noves instal·lacions, Arch Linux es un *rolling release* i el sistema sempre se pot actualitzar amb `pacman -Syu`.

## Instal·lació

Una vegada s'hagi arrencat la imatge de instal·lació, es requeriran els següents pasos per a inicialitzar el procés de instal·lació.

### Distribució del teclat

Hi ha disponibles mapes de teclats apropiats per a molts països, i una comanda com a `loadkeys es` pot ser suficient per a obtenir la seva distribució de teclat. Se poden trobar més mapes de teclat al directori `/usr/share/kbd/keymaps/` (amb la comanda *loadkeys* no és necessari indicar la ruta o la extensió de l'arxiu).

### Partició de disc

Vegi [partitioning](/index.php/Partitioning "Partitioning") per a més informació; algunes particions especials poden ser necessàries, vegi [EFI System Partition](/index.php/UEFI#EFI_System_Partition "UEFI") i [GRUB BIOS boot partition](/index.php/GRUB#GUID_Partition_Table_.28GPT.29_specific_instructions "GRUB"). Si desitja crear qualsevol dispositiu de blocs apilats (*stacked block devices*) per a [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") o [RAID](/index.php/RAID "RAID"), faci-ho ara.

### Format the partitions

See [File Systems](/index.php/File_systems#Step_2:_create_the_new_file_system "File systems") and optionally [Swap](/index.php/Swap "Swap") for details.

If you are using (U)EFI you will most probably need another partition to host the UEFI System partition. Read [Create an UEFI System Partition in Linux](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface").

### Mount the partitions

You must now mount the root partition on `/mnt`. After that, you should create directories for and mount any other partitions (`/mnt/boot`, `/mnt/home`, ...) and activate your *swap* partition if you want them to be detected by *genfstab*.

### Connect to the internet

A DHCP service is already enabled for all available devices. If you need to setup a static IP or use management tools such as [Netctl](/index.php/Netctl "Netctl"), you should stop this service first: `systemctl stop dhcpcd.service`. For more information read [configuring network](/index.php/Configuring_network "Configuring network").

#### Wireless

Run `wifi-menu` to set up your wireless network. For details, see [Wireless Setup](/index.php/Wireless_Setup "Wireless Setup") and [Netctl](/index.php/Netctl "Netctl").

### Install the base system

Before installing, you may want to edit `/etc/pacman.d/mirrorlist` such that your preferred [mirror](/index.php/Mirrors "Mirrors") is first. This copy of the mirrorlist will be installed on your new system by `pacstrap` as well, so it's worth getting it right.

Using the [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) script we install the base system.

```
# pacstrap /mnt base

```

Other packages can be installed by appending their names to the above command (space seperated), including the boot loader if you want.

### Configure the system

*   Generate an [fstab](/index.php/Fstab "Fstab") with the following command (if you prefer to use UUIDs or labels, add the `-U` or `-L` option, respectively):

	 `# genfstab -p /mnt >> /mnt/etc/fstab` 

*   [chroot](/index.php/Chroot "Chroot") into our newly installed system:

	 `# arch-chroot /mnt` 

*   Write your hostname to `/etc/hostname`.

*   Symlink `/etc/localtime` to `/usr/share/zoneinfo/Zone/SubZone`. Replace `Zone` and `Subzone` to your liking. For example:

	 `# ln -s /usr/share/zoneinfo/Europe/Athens /etc/localtime` 

*   Uncomment the selected locale in `/etc/locale.gen` and generate it with `locale-gen`.
*   Set [locale](/index.php/Locale#Setting_the_system_locale "Locale") preferences in `/etc/locale.conf`.
*   Add [console keymap](/index.php/KEYMAP "KEYMAP") and [font](/index.php/Fonts#Console_fonts "Fonts") preferences in `/etc/vconsole.conf`
*   Configure `/etc/mkinitcpio.conf` as needed (see [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")) and create an initial RAM disk with:

	 `# mkinitcpio -p linux` 

*   Set a root password with `passwd`.
*   Configure the network again for newly installed environment. See [Network configuration](/index.php/Network_configuration "Network configuration") and [Wireless Setup](/index.php/Wireless_Setup "Wireless Setup").

### Install and configure a boot loader

See [Boot loaders](/index.php/Boot_loader "Boot loader") for the available choices.

### Unmount and reboot

If you are still in the chroot environment type `exit` or press `Ctrl+D` in order to exit. Earlier we mounted the partitions under `/mnt`. In this step we will unmount them:

```
# umount -R /mnt

```

Now reboot and then login into the new system with the root account.

## Post-installation

### User management

Add any user accounts you require besides root, as described in [User management](/index.php/Users_and_groups#User_management "Users and groups"). It is not good practice to use the root account for regular use, or expose it via [SSH](/index.php/SSH "SSH") on a server. The root account should only be used for administrative tasks.

### Package management

See [pacman](/index.php/Pacman "Pacman") and [FAQ#Package management](/index.php/FAQ#Package_management "FAQ") for answers regarding installing, updating, and managing packages.

### Service management

Arch Linux uses [systemd](/index.php/Systemd "Systemd") as init, which is a system and service manager for Linux. For maintaining your Arch Linux installation, it is a good idea to learn the basics about it. Interaction with systemd is done through the `systemctl` command. Read [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd") for more information.

### Sound

[ALSA](/index.php/ALSA "ALSA") usually works out-of-the-box. It just needs to be unmuted. Install [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (which contains `alsamixer`) and follow [these](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture") instructions.

ALSA is included with the kernel and it is recommended. If it does not work, [OSS](/index.php/OSS "OSS") is a viable alternative. If you have advanced audio requirements, take a look at [Sound system](/index.php/Sound_system "Sound system") for an overview of various articles.

### Display server

The X Window System (commonly X11, or X) is a networking and display protocol which provides windowing on bitmap displays. It is the de-facto standard for implementating graphical user interfaces. See the [Xorg](/index.php/Xorg "Xorg") article for details.

[Wayland](/index.php/Wayland "Wayland") is a new display server protocol and the Weston reference implementation is available. There is very little support for it from applications at this early stage of development.

### Fonts

You may wish to install a set of TrueType fonts, as only unscalable bitmap fonts are included by default. DejaVu is a set of high quality, general-purpose fonts with good [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") coverage:

```
# pacman -S ttf-dejavu

```

Refer to [Font configuration](/index.php/Font_configuration "Font configuration") for how to configure font rendering and [Fonts](/index.php/Fonts "Fonts") for font suggestions and installation instructions.

## Appendix

For a list of applications that may be of interest, see [List of applications](/index.php/List_of_applications "List of applications").

See [General recommendations](/index.php/General_recommendations "General recommendations") for post-installation tutorials like setting up a touchpad or font rendering.