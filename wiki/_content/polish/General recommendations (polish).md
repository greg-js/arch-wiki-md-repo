Related articles

*   [FAQ (Polski)](/index.php?title=FAQ_(Polski)&action=edit&redlink=1 "FAQ (Polski) (page does not exist)")
*   [Installation guide (Polski)](/index.php/Installation_guide_(Polski) "Installation guide (Polski)")
*   [Beginners' guide (Polski)](/index.php/Beginners%27_guide_(Polski) "Beginners' guide (Polski)")
*   [List of applications (Polski)](/index.php?title=List_of_applications_(Polski)&action=edit&redlink=1 "List of applications (Polski) (page does not exist)")

Ten dokument to zbiór popularnych artykułów i przydatnych informacji o dodawaniu funkcjonalności do zainstalowanego systemu Arch. Zakłada się, że czytelnicy przeczytali i wykonali instrukcje zawarte w [Beginners' guide (Polski)](/index.php/Beginners%27_guide_(Polski) "Beginners' guide (Polski)") lub [Installation guide (Polski)](/index.php/Installation_guide_(Polski) "Installation guide (Polski)") i zainstalowali podstawowy system. Zaznajomienie się z informacjami zawartymi w [#Administracja systemem](#Administracja_systemem) i [#Zarządzanie pakietami](#Zarz.C4.85dzanie_pakietami) jest *wymagane* do zrozumienia innych sekcji tej strony i pozostałych stron na wiki.

## Contents

*   [1 Administracja systemem](#Administracja_systemem)
    *   [1.1 Użytkownicy i grupy](#U.C5.BCytkownicy_i_grupy)
    *   [1.2 Eskalacja uprawnień](#Eskalacja_uprawnie.C5.84)
    *   [1.3 Zarządzanie usługami](#Zarz.C4.85dzanie_us.C5.82ugami)
    *   [1.4 Utrzymywanie systemu](#Utrzymywanie_systemu)
*   [2 Zarządzanie pakietami](#Zarz.C4.85dzanie_pakietami)
    *   [2.1 pacman](#pacman)
    *   [2.2 Repositories](#Repositories)
    *   [2.3 Mirrors](#Mirrors)
    *   [2.4 Arch Build System](#Arch_Build_System)
    *   [2.5 Arch User Repository](#Arch_User_Repository)
*   [3 Booting](#Booting)
    *   [3.1 Hardware auto-recognition](#Hardware_auto-recognition)
    *   [3.2 Microcode](#Microcode)
    *   [3.3 Retaining boot messages](#Retaining_boot_messages)
    *   [3.4 Num Lock activation](#Num_Lock_activation)
*   [4 Graphical user interface](#Graphical_user_interface)
    *   [4.1 Display server](#Display_server)
    *   [4.2 Display drivers](#Display_drivers)
    *   [4.3 Desktop environments](#Desktop_environments)
    *   [4.4 Window managers](#Window_managers)
    *   [4.5 Display manager](#Display_manager)
*   [5 Power management](#Power_management)
    *   [5.1 ACPI events](#ACPI_events)
    *   [5.2 CPU frequency scaling](#CPU_frequency_scaling)
    *   [5.3 Laptops](#Laptops)
    *   [5.4 Suspend and Hibernate](#Suspend_and_Hibernate)
*   [6 Multimedia](#Multimedia)
    *   [6.1 Sound](#Sound)
    *   [6.2 Browser plugins](#Browser_plugins)
    *   [6.3 Codecs](#Codecs)
*   [7 Networking](#Networking)
    *   [7.1 Clock synchronization](#Clock_synchronization)
    *   [7.2 DNS security](#DNS_security)
    *   [7.3 Setting up a firewall](#Setting_up_a_firewall)
    *   [7.4 Resource sharing](#Resource_sharing)
*   [8 Input devices](#Input_devices)
    *   [8.1 Keyboard layouts](#Keyboard_layouts)
    *   [8.2 Mouse buttons](#Mouse_buttons)
    *   [8.3 Laptop touchpads](#Laptop_touchpads)
    *   [8.4 TrackPoints](#TrackPoints)
*   [9 Optimization](#Optimization)
    *   [9.1 Benchmarking](#Benchmarking)
    *   [9.2 Maximizing performance](#Maximizing_performance)
    *   [9.3 Solid state drives](#Solid_state_drives)
*   [10 System service](#System_service)
    *   [10.1 File index and search](#File_index_and_search)
    *   [10.2 Local mail delivery](#Local_mail_delivery)
    *   [10.3 Printing](#Printing)
*   [11 Appearance](#Appearance)
    *   [11.1 Fonts](#Fonts)
    *   [11.2 GTK and Qt themes](#GTK_and_Qt_themes)
*   [12 Console improvements](#Console_improvements)
    *   [12.1 Aliases](#Aliases)
    *   [12.2 Alternative shells](#Alternative_shells)
    *   [12.3 Bash additions](#Bash_additions)
    *   [12.4 Colored output](#Colored_output)
    *   [12.5 Compressed files](#Compressed_files)
    *   [12.6 Console prompt](#Console_prompt)
    *   [12.7 Emacs shell](#Emacs_shell)
    *   [12.8 Mouse support](#Mouse_support)
    *   [12.9 Scrollback buffer](#Scrollback_buffer)
    *   [12.10 Session management](#Session_management)

## Administracja systemem

Ta sekcja mówi o zadaniach administracyjnycj i zarządzaniem systemem. Jeśli chcesz wiedzieć więcej, odwiedź [Core utilities (Polski)](/index.php?title=Core_utilities_(Polski)&action=edit&redlink=1 "Core utilities (Polski) (page does not exist)") i [Category:System administration (Polski)](/index.php/Category:System_administration_(Polski) "Category:System administration (Polski)")

### Użytkownicy i grupy

Na nowej instalacji posiadasz tylko konto super-użytkownika, lepiej znanego jako "root". Logowanie się jako root przez dłuższy okres czasu, może nawet odsłanianie go przez [SSH (Polski)](/index.php?title=SSH_(Polski)&action=edit&redlink=1 "SSH (Polski) (page does not exist)"), [jest niebezpieczne](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). Zamiast tego, powiniwneś stworzyć i używać do większości zadań nieuprzywilejowanego konta użytkownika, a konta root tylko do administracji systemem. Zobacz [Users and groups (Polski)#Zarządzanie użytkownikami](/index.php?title=Users_and_groups_(Polski)&action=edit&redlink=1 "Users and groups (Polski) (page does not exist)") żeby uzyskać więcej informacji.

Grupy i użytkownicy są mechanizmem *kontroli dostępu*; administratorzy mogą dostosować członkostwo i własności grup żeby przyznać lub odmówić użytkownikom i usługom dostęp do zasobów systemu. Przeczytaj [Users and groups (Polski)](/index.php?title=Users_and_groups_(Polski)&action=edit&redlink=1 "Users and groups (Polski) (page does not exist)") żeby uzyskać detale dotyczące potencjalnych zagrożeń dla bezpieczeństwa.

### Eskalacja uprawnień

Komenda [su (Polski)](/index.php?title=Su_(Polski)&action=edit&redlink=1 "Su (Polski) (page does not exist)") (substitute user) umożliwia przyjęcie tożsamości innego użytkownika systemu (najczęściej root'a) z poziomu zalogowaneo użytkownika, natomiast komenda [sudo (Polski)](/index.php?title=Sudo_(Polski)&action=edit&redlink=1 "Sudo (Polski) (page does not exist)") (substitute user do) tymczasowo podnosi uprawninia dla pojedynczej komendy.

### Zarządzanie usługami

Arch Linux używa [systemd (Polski)](/index.php?title=Systemd_(Polski)&action=edit&redlink=1 "Systemd (Polski) (page does not exist)") jako procesu [init (Polski)](/index.php?title=Init_(Polski)&action=edit&redlink=1 "Init (Polski) (page does not exist)"). Jest on menadżerem systemu i usług dla linuxa. Jeśli chcesz utrzymać swój system w dobrej kondycji, dobrym pomysłem jest żeby poznać jego podstawy. Interakcje z *systemd* są wykonywane za pośrednictwem komendy *systemctl*. Przeczytaj [systemd (Polski)#Podstawowe użycie systemctl](/index.php?title=Systemd_(Polski)&action=edit&redlink=1 "Systemd (Polski) (page does not exist)") żeby uzyskać więcej informacji.

### Utrzymywanie systemu

Arch jest systemem o częstych aktualizacjach i zmianach w pakietach, więc użytkownicy muszą poświęcić trochę czasu na [system maintenance (Polski)](/index.php?title=System_maintenance_(Polski)&action=edit&redlink=1 "System maintenance (Polski) (page does not exist)"). Przeczytaj [Security (Polski)](/index.php?title=Security_(Polski)&action=edit&redlink=1 "Security (Polski) (page does not exist)") żeby dowiedzieć się jak zabezpieczyć swój system przed atakami.

## Zarządzanie pakietami

Ta sekcja zawiera pomocne informacje dotyczące zarządzania pakietami. Zeby przeczytać o tym więcej odwiedź [FAQ (Polski)#Package management](/index.php?title=FAQ_(Polski)&action=edit&redlink=1 "FAQ (Polski) (page does not exist)") i [Category:Package management (Polski)](/index.php/Category:Package_management_(Polski) "Category:Package management (Polski)")

**Note:** It is imperative to keep up to date with changes in Arch Linux that require manual intervention **before** upgrading your system. Subscribe to the [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) or check the front page [Arch news](https://www.archlinux.org/) every time before you update. Alternatively, you may find it useful to subscribe to [this RSS feed](https://www.archlinux.org/feeds/news/) or follow [@archlinux](https://twitter.com/archlinux) on Twitter.

### pacman

[pacman](/index.php/Pacman "Pacman") is the Arch Linux *pac*kage *man*ager: all users are required to become familiar with it before reading any other articles.

See [pacman tips](/index.php/Pacman_tips "Pacman tips") for suggestions on how to improve your interaction with *pacman* and package management in general.

### Repositories

See [Official repositories](/index.php/Official_repositories "Official repositories") for details about the purpose of each officially maintained repository.

If you installed Arch Linux x86_64 and plan on using 32-bit applications, you will want to enable the [multilib](/index.php/Multilib "Multilib") repository.

[Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") lists several other unsupported repositories.

### Mirrors

Visit [Mirrors](/index.php/Mirrors "Mirrors") for steps on taking full advantage of using the fastest and most up to date *pacman* mirrors. As explained in the article, a particularly good advice is to routinely check the [Mirror Status](https://www.archlinux.org/mirrors/status/) page and/or [Mirror-Status](http://www.archlinux.de/?page=MirrorStatus) for a list of mirrors that have been recently synced.

### Arch Build System

*Ports* is a system initially used by BSD distributions consisting of build scripts that reside in a directory tree on the local system. Simply put, each port contains a script within a directory intuitively named after the installable third-party application.

The [ABS](/index.php/ABS "ABS") tree offers the same functionality by providing build scripts called [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"), which are populated with information for a given piece of software; integrity hashes, project URL, version, license and build instructions. These PKGBUILDs are later parsed by [makepkg](/index.php/Makepkg "Makepkg"), the actual program that generates packages cleanly manageable by *pacman*.

Every package in the repositories along with those present in the AUR are subject to recompilation with *makepkg*.

### Arch User Repository

While the ABS tree allows the ability of building software available in the official repositories, the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) is the equivalent for user submitted packages. It is an unsupported repository of build scripts accessible through the [web interface](https://aur.archlinux.org/) or by an [AUR helper](/index.php/AUR_helper "AUR helper").

## Booting

This section contains information pertaining to the boot process. An overview of the Arch boot process can be found at [Arch boot process](/index.php/Arch_boot_process "Arch boot process"). For more, please see [Category:Boot process](/index.php/Category:Boot_process "Category:Boot process").

### Hardware auto-recognition

Hardware should be auto-detected by [udev](/index.php/Udev "Udev") during the boot process by default. A potential improvement in boot time can be achieved by disabling module auto-loading and specifying required modules manually, as described in [Kernel modules#Loading](/index.php/Kernel_modules#Loading "Kernel modules"). Additionally, [Xorg](/index.php/Xorg "Xorg") should be able to auto-detect required drivers using udev, but users have the option to configure the X server manually too.

### Microcode

Processors may have [faulty behaviour](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), which the kernel can correct by updating the *microcode* on startup. Intel processors require a separate package to this effect. See [Microcode](/index.php/Microcode "Microcode") for details.

### Retaining boot messages

Once it concludes, the screen is cleared and the login prompt appears, leaving users unable to gather feedback from the boot process. [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") to overcome this limitation.

### Num Lock activation

Num Lock is a toggle key found in most keyboards. For activating Num Lock's number key-assignment during startup, see [Activating Numlock on Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup").

## Graphical user interface

This section provides orientation for users wishing to run graphical applications on their system. See [Category:X server](/index.php/Category:X_server "Category:X server") for additional resources.

### Display server

[Xorg](/index.php/Xorg "Xorg") is the public, open-source implementation of the [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (commonly X11, or X). It is required for running applications with graphical user interfaces (GUIs), and the majority of users will want to install it.

[Wayland](/index.php/Wayland "Wayland") is a new, alternative display server protocol and the Weston reference implementation is available. There is very little support for it from applications at this early stage of development.

### Display drivers

The default *vesa* display driver will work with most video cards, but performance can be significantly improved and additional features harnessed by installing the appropriate driver for [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel"), or [NVIDIA](/index.php/NVIDIA "NVIDIA") products.

### Desktop environments

Although Xorg provides the basic framework for building a graphical environment, additional components may be considered necessary for a complete user experience. [Desktop environments](/index.php/Desktop_environment "Desktop environment") such as [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), and [Xfce](/index.php/Xfce "Xfce") bundle together a wide range of *X clients*, such as a window manager, panel, file manager, terminal emulator, text editor, icons, and other utilities. Users with less experience may wish to install a desktop environment for a more familiar environment. See [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") for additional resources.

### Window managers

A full-fledged desktop environment provides a complete and consistent graphical user interface, but tends to consume a considerable amount of system resources. Users seeking to maximize performance or otherwise simplify their environment may opt to install a [window manager](/index.php/Window_manager "Window manager") alone and hand-pick desired extras. Most desktop environments allow use of an alternative window manager as well. [Dynamic](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [stacking](/index.php/Category:Stacking_WMs "Category:Stacking WMs"), and [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") window managers differ in their handling of window placement.

### Display manager

Most desktop environment include a [display manager](/index.php/Display_manager "Display manager") for automatically starting the graphical environment and managing user logins. Users without a desktop environment can install one separately. Alternatively you may [start X at login](/index.php/Start_X_at_login "Start X at login") as a simple alternative to a display manager.

## Power management

This section may be of use to laptop owners or users otherwise seeking power management controls. For more, please see [Category:Power management](/index.php/Category:Power_management "Category:Power management").

See [Power management](/index.php/Power_management "Power management") for more general overview.

### ACPI events

Users can configure how the system reacts to ACPI events such as pressing the power button or closing a laptop's lid. For the new (recommended) method using [systemd](/index.php/Systemd "Systemd"), see [Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management"). For the old method, see [acpid](/index.php/Acpid "Acpid").

### CPU frequency scaling

Modern processors can decrease their frequency and voltage to reduce heat and power consumption. Less heat leads to more quiet system and prolongs the life of hardware. See [CPU frequency scaling](/index.php/CPU_frequency_scaling "CPU frequency scaling") for details.

### Laptops

For articles related to portable computing along with model-specific installation guides, please see [Category:Laptops](/index.php/Category:Laptops "Category:Laptops"). For a general overview of laptop-related articles and recommendations, see [Laptop](/index.php/Laptop "Laptop").

### Suspend and Hibernate

See main article: [Suspend and hibernate](/index.php/Suspend_and_hibernate "Suspend and hibernate").

## Multimedia

[Category:Multimedia](/index.php/Category:Multimedia "Category:Multimedia") includes additional resources.

### Sound

[Sound](/index.php/Sound "Sound") is provided by kernel sound drivers:

*   [ALSA](/index.php/ALSA "ALSA") is included with the kernel and is recommended because usually it works out of the box (it just needs to be [unmuted](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture")).

*   [OSS](/index.php/OSS "OSS") is a viable alternative in case ALSA does not work.

Users may additionally wish to install and configure a [sound server](/index.php/Sound#Sound_servers "Sound") such as [PulseAudio](/index.php/PulseAudio "PulseAudio"). For advanced audio requirements, see [professional audio](/index.php/Professional_audio "Professional audio").

### Browser plugins

For access to certain web content, [browser plugins](/index.php/Browser_plugins "Browser plugins") such as Adobe Acrobat Reader, Adobe Flash Player, and Java can be installed.

### Codecs

[Codecs](/index.php/Codecs "Codecs") are utilized by multimedia applications to encode or decode audio or video streams. In order to play encoded streams, users must ensure an appropriate codec is installed.

## Networking

This section is confined to small networking procedures. Head over to [Network configuration](/index.php/Network_configuration "Network configuration") for a full guide. For more, please see [Category:Networking](/index.php/Category:Networking "Category:Networking").

### Clock synchronization

The [Network Time Protocol](https://en.wikipedia.org/wiki/Network_Time_Protocol "wikipedia:Network Time Protocol") (NTP) is a protocol for synchronizing the clocks of computer systems over packet-switched, variable-latency data networks. See [Time#Time synchronization](/index.php/Time#Time_synchronization "Time") for implementations of such protocol.

### DNS security

For better security while browsing web, paying online, connecting to [SSH](/index.php/SSH "SSH") services and similar tasks consider using [DNSSEC](/index.php/DNSSEC "DNSSEC")-enabled client software which can validate signed [DNS](https://en.wikipedia.org/wiki/Domain_Name_System "wikipedia:Domain Name System") records, and [DNSCrypt](/index.php/DNSCrypt "DNSCrypt") to encrypt DNS traffic.

### Setting up a firewall

A [firewall](/index.php/Firewall "Firewall") can provide an extra layer of protection on top of the Linux networking stack. While the stock Arch kernel is capable of using [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")'s [iptables](/index.php/Iptables "Iptables"), it is not enabled by default. It is highly recommended to set up some form of firewall, see [Firewalls](/index.php/Firewalls "Firewalls") for the available guides.

### Resource sharing

To share files among the machines in a network, follow the [NFS](/index.php/NFS "NFS") or the [SSHFS](/index.php/SSHFS "SSHFS") article.

Use [Samba](/index.php/Samba "Samba") to join a Windows network. To configure the machine to use Active Directory for authentication, read [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration").

See also [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Input devices

This section contains popular input device configuration tips. For more, please see [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Keyboard layouts

Non-English or otherwise non-standard keyboards may not function as expected by default. The necessary steps to configure the keymap are different for virtual console and [Xorg](/index.php/Xorg "Xorg"), they are described in [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") respectively.

### Mouse buttons

Owners of advanced or unusual mice may find that not all mouse buttons are recognized by default, or may wish to assign different actions for extra buttons. Instructions can be found in [All Mouse Buttons Working](/index.php/All_Mouse_Buttons_Working "All Mouse Buttons Working").

### Laptop touchpads

Many laptops use [Synaptics](http://www.synaptics.com/) or [ALPS](http://www.alps.com/) "touchpad" pointing devices. These, and several other touchpad models, use the Synaptics input driver; see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") for installation and configuration details.

### TrackPoints

See the [TrackPoint](/index.php/TrackPoint "TrackPoint") article to configure your TrackPoint device.

## Optimization

This section aims to summarize tweaks, tools and available options useful to improve system and application performance.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") is the act of measuring performance and comparing the results to another system's results or a widely accepted standard through a unified procedure.

### Maximizing performance

The [Improving performance](/index.php/Improving_performance "Improving performance") article gathers information and is a basic rundown about gaining performance in Arch Linux.

### Solid state drives

The [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") article covers many aspects of solid state drives, including configuring them to maximize their lifetimes.

## System service

This section relates to [daemons](/index.php/Daemons "Daemons"). For more, please see [Category:Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services").

### File index and search

Most distributions have a `locate` command available to be able to quickly search for files. To get this functionality in Arch Linux, [mlocate](https://www.archlinux.org/packages/?name=mlocate) is the recommended install. After the install you should run `updatedb` to index the filesystems.

### Local mail delivery

A default base setup bestows no means for mail syncing. To configure *Postfix* for simple local mailbox delivery, see [Postfix](/index.php/Postfix "Postfix"). Other options are [SSMTP](/index.php/SSMTP "SSMTP"), [msmtp](/index.php/Msmtp "Msmtp") and [fdm](/index.php/Fdm "Fdm").

### Printing

[CUPS](/index.php/CUPS "CUPS") is a standards-based, open source printing system developed by Apple. See [Category:Printers](/index.php/Category:Printers "Category:Printers") for printer-specific articles.

## Appearance

This section contains frequently-sought "eye candy" tweaks for an aesthetically pleasing Arch experience. For more, please see [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Fonts

You may wish to install a set of TrueType fonts, as only unscalable bitmap fonts are included in a basic Arch system. The [ttf-dejavu](https://www.archlinux.org/packages/?name=ttf-dejavu) package provides a set of high quality, general-purpose fonts with good [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") coverage.

A plethora of information on the subject can be found in the [Fonts](/index.php/Fonts "Fonts") and [Font configuration](/index.php/Font_configuration "Font configuration") articles.

If spending a significant amount of time working from the virtual console (i.e. outside an X server), users may wish to change the console font to improve readability; see [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts").

### GTK and Qt themes

A big part of the applications with a graphical interface for Linux systems are based on the [GTK+](/index.php/GTK%2B "GTK+") or the [Qt](/index.php/Qt "Qt") toolkits. See those articles and [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for ideas to improve the appearance of your installed programs and adapt it to your liking.

## Console improvements

This section applies to small modifications that better console programs' practicality. For more, please see [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### Aliases

Aliasing a command, or a group thereof, is a way of saving time when using the console. This is specially helpful for repetitive tasks that do not need significant alteration to their parameters between executions. Common time-saving aliases can be found in [Bash#Aliases](/index.php/Bash#Aliases "Bash"), which are easily portable to [zsh](/index.php/Zsh "Zsh") as well.

### Alternative shells

[Bash](/index.php/Bash "Bash") is the shell that is installed by default in an Arch system. The live installation media, however, uses [zsh](/index.php/Zsh "Zsh") with the [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) addon package. See [Command-line shell#List of shells](/index.php/Command-line_shell#List_of_shells "Command-line shell") for more alternatives.

### Bash additions

A list of miscellaneous Bash settings, including completion enhancements, history search and [Readline](/index.php/Readline "Readline") macros is available in [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Colored output

Even though a number of applications have built-in color capabilities, using a general-purpose colorizing wrapper, such as `cope`, is another route. Install the [cope-git](https://aur.archlinux.org/packages/cope-git/) package. The [acoc](https://aur.archlinux.org/packages/acoc/) package provides a similar application.

Colorizing the output of specific core utilities such as `grep` and `ls` is covered in the [Core utilities](/index.php/Core_utilities "Core utilities") article.

Man pages (or manual pages) are one of the most useful resources available to GNU/Linux users. To aid readability, the pager can be configured to render colored text as explained in [man page#Colored man pages](/index.php/Man_page#Colored_man_pages "Man page").

### Compressed files

Compressed files, or archives, are frequently encountered on a GNU/Linux system. [Tar](/index.php/Tar "Tar") is one of the most commonly used archiving tools, and users should be familiar with its syntax (Arch Linux packages, for example, are simply xzipped tarballs). See [Bash#Functions](/index.php/Bash#Functions "Bash") for other helpful commands.

### Console prompt

The console prompt (PS1) can be customized to a great extent. See [Color Bash Prompt](/index.php/Color_Bash_Prompt "Color Bash Prompt") or [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") if using Bash or Zsh, respectively.

### Emacs shell

Emacs is known for featuring options beyond the duties of regular text editing, one of these being a full shell replacement. Consult [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") for a fix regarding garbled characters that may result from enabling colored output.

### Mouse support

Using a mouse with the console for copy-paste operations can be preferred over [GNU Screen](/index.php/GNU_Screen "GNU Screen")'s traditional copy mode. Refer to [Console mouse support](/index.php/Console_mouse_support "Console mouse support") for comprehensive directions.

### Scrollback buffer

To be able to save and view text which has scrolled off the screen, refer to [Scrollback buffer](/index.php/Scrollback_buffer "Scrollback buffer").

### Session management

Using terminal multiplexers like [tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen"), programs may be run under sessions composed of tabs and panes that can be detached at will, so when the user either kills the terminal emulator, terminates [X](/index.php/X "X"), or logs off, the programs associated with the session will continue to run in the background as long as the terminal multiplexer server is active. Interacting with the programs requires reattaching to the session.