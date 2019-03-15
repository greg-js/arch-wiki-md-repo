Esta página es para dar a entender los términos usados en la comunidad de Arch Linux. Se libre de agregar o modificar cualquier término. Si decides agregar una, por favor agregarla en orden alfabético.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 ABS](#ABS)
*   [2 AUR](#AUR)
*   [3 PKGBUILD](#PKGBUILD)
*   [4 TU](#TU)
*   [5 TUR](#TUR)
*   [6 bbs](#bbs)
*   [7 [community]](#[community])
*   [8 [core]](#[core])
*   [9 custom/user repository](#custom/user_repository)
*   [10 developer/desarrollador](#developer/desarrollador)
*   [11 /etc/network-profiles](#/etc/network-profiles)
*   [12 /etc/rc.local](#/etc/rc.local)
*   [13 [extra]](#[extra])
*   [14 hotplug](#hotplug)
*   [15 hwd](#hwd)
*   [16 hwdetect](#hwdetect)
*   [17 initramfs](#initramfs)
*   [18 initrd](#initrd)
*   [19 makepkg](#makepkg)
*   [20 namcap](#namcap)
*   [21 package](#package)
*   [22 pacman](#pacman)
*   [23 pacman.conf](#pacman.conf)
*   [24 release/[release]](#release/[release])
*   [25 repository/repo](#repository/repo)
*   [26 RTFM](#RTFM)
*   [27 [testing]](#[testing])
*   [28 udev](#udev)
*   [29 wiki](#wiki)

## ABS

El Arch Build System (Sistema de Construcción de Arch) es útil para:

*   Hacer nuevos paquetes de software para los que no existe un paquete.
*   Personalizar/Modificar paquetes existentes para tus necesidades (activar o desactivar opciones)
*   Re-construir todo el sistema usando tus flags del compilador, "a la Gentoo" (Y obtener módulos funcionando con tu kernel personalizado)

ABS no es necesario para usar Arch Linux, pero es muy útil.

Para mas información consulta la página de [Arch Build System](/index.php/Arch_Build_System "Arch Build System")

## AUR

El Arch Linux User-Community Repository (Repositorio de Usuarios de Arch Linux) es un repositorio manejado por la comunidad de usuarios de Arch. AUR era inicialmente concebido para organizar la compartición de los PKGBUILDs a una audiencia mayor, donde los mas populares son ingresados a los repositorios [core] y [extra] mediante el repositorio de AUR [community].

Es denominado como el lugar de nacimiento de los nuevos paquetes de Arch's. Esto es porque en AUR, los usuarios contribuyen con sus propios paquetes. La comunidad AUR vota por o en contra de ellos, y eventualmente una vez que un paquete ha tenido los suficiente votos positivos, un TU lo toma al repositorio [community] que es accesible por medio de pacman y ABS.

Puedes acceder al a AUR a través de [aquí](https://aur.archlinux.org/index.php?setlang=es)

## PKGBUILD

[PKGBUILD (Español)](/index.php/PKGBUILD_(Espa%C3%B1ol) "PKGBUILD (Español)")

## TU

**T**rusted **U**ser (usuario confiable). Este es alguien que ha sido elegido por otros TU para controlar AUR y el repositorio [community].

Los TU tienen la habilidad de marcar los paquetes como seguros en AUR, y si han sido votados como popular, moverlos al repositorio [community].

Para mas información visitar [esta página](/index.php/Trusted_Users "Trusted Users")

## TUR

**T**rusted **U**ser **R**epository (obsoleto) Antes en AUR, Los TU tenían su propio repositorio para (versiones especiales de) aplicaciones que no estaban en los repositorios oficiales. Cualquiera podria hacer su propio repositorio, pero los TUR creaban uno de mayor calidad, porque ellos eran votados por su calidad y grado de conocimientos.

## bbs

**B**ulletin **B**oard **S**ystem, pero en el caso de Arch es solo el foro de soporto localizado en [https://bbs.archlinux.org](https://bbs.archlinux.org).

## [community]

El repositorio [community] es donde los paquetes pre-construidos se encuentran disponibles gracias a los TU. Una gran mayoría de los paquetes de community, provienen del AUR.

Para acceder a este repositorio, descoméntalo en `/etc/pacman.conf`.

## [core]

El repositorio [core] contiene los pocos paquetes necesarios para un sistema Arch. Tiene todo lo necesario para tener un sistema con línea de comandos.

## custom/user repository

Cualquiera puede crear un repo y ponerlo online para que otros usuarios lo usen. Para crear un repositorio, necesitas una serie de paquetes y una base de datos compatible con pacman para los paquetes. El archivo de BD es creado con [gensync](/index.php?title=Repositorio_local_con_ABS_y_gensync&action=edit&redlink=1 "Repositorio local con ABS y gensync (page does not exist)"). Cuando tienes ambos, puedes ponerlo online (HTTP or FTP) y cualquiera podrá usarlo agregándolo como cualquier repositorio.

## developer/desarrollador

Half-gods working to improve Arch for no financial gain. Developers are outranked only by our god, Judd Vinet.

## /etc/network-profiles

In this, you can create various network configurations.

This is very useful for laptop users that switch networks very often, for example between a home and an office network.

Additionally it can be used with [wpa_supplicant](https://www.archlinux.org/packages/?name=wpa_supplicant) that can manage all of your wireless networks. For each configuration you need to make a configuration file. The easiest way to do this, is by copying the template. After you are done with this, you need to enable these in `/etc/rc.conf`

After applying changes, you should restart your network by using, as root,

```
 /etc/rc.d/network restart

```

## /etc/rc.local

This script is run at the end of every boot. It is intended for miscellaneous commands that you might want to execute before the login prompt. It is not recommended to add any services or settings in `/etc/rc.local` that could be started or set from `/etc/rc.conf` instead.

## [extra]

Arch's official package set is fairly streamlined, but we supplement this with a larger, more complete "extra" repository that contains a lot of the stuff that never made it into our core package set. This repository is constantly growing with the help of packages submitted from our strong community. This is where desktop environments, window managers and common programs are found.

## hotplug

## hwd

Hwd; hardware detect for Arch Linux, is for both devfs and udev device systems and also for kernels 2.4.x and 2.6.x. Instead of running an auto configure script what may be expected, Hwd (`/usr/bin/hwd`) does not change existing configures. Detects hardwares and modules, and provides information how to do manually. This allows the user to have a control over his/her system; basic philosophy of Arch Linux.

Hwd is uploaded in Arch Linux's [extra] repository. To install, run pacman.

```
pacman -S hwd

```

here can you see the things you can use Hwd to [[1]](http://amlug.net/new-projects/hwd/hwd-46.jpg)

## hwdetect

## initramfs

## initrd

The special file `/dev/initrd` is a read-only block device. Device `/dev/initrd` is a RAM disk that is initialized (e.g. loaded) by the boot loader before the kernel is started. The kernel then can use the block device `/dev/initrd`'s contents for a two phased system boot-up.

In the first boot-up phase, the kernel starts up and mounts an initial root file-system from the contents of `/dev/initrd` (e.g. RAM disk initialized by the boot loader). In the second phase, additional drivers or other modules are loaded from the initial root device's contents. After loading the additional modules, a new root file system (i.e. the normal root file system) is mounted from a different device.

## makepkg

makepkg will build packages for you. makepkg will read the metadata required from a PKGBUILD file. All it needs is a build-capable Linux platform, [wget](https://www.archlinux.org/packages/?name=wget), and some build scripts. The advantage to a script-based build is that you only really do the work once. Once you have the build script for a package, you just need to run makepkg and it will do the rest: download and validate source files, check dependencies, configure the build time settings, build the package, install the package into a temporary root, make customizations, generate meta-info, and package the whole thing up for pacman to use.

## namcap

namcap is a package analysis utility that looks for problems with ArchLinux packages or their PKGBUILD files. It can apply rules to the file list, the files themselves, or individual PKGBUILD files.

Rules return lists of messages. Each message can be one of three types: error, warning, or information (think of them as notes or comments). Errors (designated by 'E:') are things that namcap is very sure are wrong and need to be fixed. Warnings (designated by 'W:') are things that namcap thinks should be changed but if you know what you are doing then you can leave them. Information (designated 'I:') are only shown when you use the info argument. Information messages give information that might be helpful but is not anything that needs changing.

## package

A package is an archive containing

*   all the (compiled) files of an application
*   metadata about the application, such as application name, version, dependencies, ...
*   installation files and directives for pacman
*   (optionally) extra files to make your life easier, such as a start/stop script

Arch's package manager pacman can install, update and remove programs cleanly those packages. Using packages instead of compiling and installing programs yourself has various benefits:

*   easily updatable: pacman will update existing packages as soon as updates are available
*   dependency checks: pacman handles dependencies for you, you only need to specify the program and pacman installs it together with every other program it needs
*   clean removal: pacman has a list of every file in a package. This way no files are left behind when you decide to remove a package

**Note:** different GNU/Linux distributions use different packages and package manager, meaning that you cannot use pacman to install a Debian package on Arch.

## pacman

The [Pacman](/index.php/Pacman "Pacman") package manager is one of the great highlights of Arch Linux. It combines a simple binary package format with an easy-to-use build system (see ABS). Pacman makes it possible to easily manage and customize packages, whether they be from the official Arch repositories or the user's own creations. The repository system allows users to build and maintain their own custom package repositories, which encourages community growth and contribution (see AUR).

Pacman can keep a system up to date by synchronizing package lists with the master server, making it a breeze for the security-conscious system administrator to maintain. This server/client model also allows you to download/install packages with a simple command, complete with all required dependencies (similar to Debian's apt-get).

NB: Pacman was written and is being maintained by Judd Vinet, the creator of Arch Linux. It is used as a package management tool by other distros as well, such as FrugalWare, Rubix, UfficioZero (in Italian, based on Ubuntu), and, of course, ArchLinux-derivatives such as Archie and AEGIS.

## pacman.conf

This is the configuration file of pacman. It's located in `/etc`. For a full explanation of its powers

```
man pacman.conf

```

## release/[release]

Release repository follows the semi-regular snapshot releases and does not update until the next snapshot/iso has been released. For example, the Release repository will point to all packages on the 0.5 ISO until we release 0.6; then it will point to 0.6 packages until 0.7 is released. This is useful if you only want to update your system when a new release is available.

## repository/repo

The repository has the pre-compiled packages of one or (usually) more PKGBUILDs. Official repositories are

*   core: containing the latest version of packages required for a full CLI system
*   extra: containing the latest version of packages not needed for a working system, but needed for an enjoyable system ;)
*   community: containing packages that came from [AUR](https://aur.archlinux.org) and got enough user votes

Pacman uses these repositories to search for packages and install them. A repository can be local (i.e. on your own computer) or remote (i.e. the packages are downloaded before they're installed).

## RTFM

**R**ead **T**he **F**ucking **M**anual. This simple message is replied to a lot of new Linux/Arch users who ask about the functionality of a program, when it is clearly defined in `man program`

It is often used when a user fails to make any attempt to find a solution to the problem themselves. If someone tells you this, they are not trying to offend you, they are just frustrated with your lack of effort.

The best thing to do if you are told to do this, is to do as above, and read the manual page:

*   Read the program man page, at a command line

```
man program-name

```

*   Search the wiki
*   Search the forum
*   Search Google

## [testing]

This is the repository where major packages/updates to packages are kept prior to release into the main repositories, so they can be bug tested and upgrade issues can be found. It is disabled by default, but can be enabled in `/etc/pacman.conf`

## udev

udev provides a dynamic device directory containing only the files for actually present devices. It creates or removes device node files in the `/dev` directory, or it renames network interfaces.

Usually udev runs as udevd(8) and receives uevents directly from the kernel if a device is added or removed form the system.

If udev receives a device event, it matches its configured rules against the available device attributes provided in sysfs to identify the device. Rules that match, may provide additional device information or specify a device node name and multiple symlink names and instruct udev to run additional programs as part of the device event handling.

## wiki

[This!](/index.php/Main_page "Main page") A place to find documentation about Arch Linux. Anyone can add and modify the documentation.