Related articles

*   [FAQ](/index.php/FAQ "FAQ")
*   [Installation guide](/index.php/Installation_guide "Installation guide")
*   [List of applications](/index.php/List_of_applications "List of applications")

This document is an annotated index of popular articles and important information for improving and adding functionalities to the installed Arch system. Readers are assumed to have read and followed the [Installation guide](/index.php/Installation_guide "Installation guide") to obtain a basic Arch Linux installation. Having read and understood the concepts explained in [#System administration](#System_administration) and [#Package management](#Package_management) is *required* for following the other sections of this page and the other articles in the wiki.

## Contents

*   [1 System administration](#System_administration)
    *   [1.1 Users and groups](#Users_and_groups)
    *   [1.2 Privilege escalation](#Privilege_escalation)
    *   [1.3 Service management](#Service_management)
    *   [1.4 System maintenance](#System_maintenance)
*   [2 Package management](#Package_management)
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
    *   [9.2 Improving performance](#Improving_performance)
    *   [9.3 Solid state drives](#Solid_state_drives)
*   [10 System service](#System_service)
    *   [10.1 File index and search](#File_index_and_search)
    *   [10.2 Local mail delivery](#Local_mail_delivery)
    *   [10.3 Printing](#Printing)
*   [11 Appearance](#Appearance)
    *   [11.1 Fonts](#Fonts)
    *   [11.2 GTK+ and Qt themes](#GTK.2B_and_Qt_themes)
*   [12 Console improvements](#Console_improvements)
    *   [12.1 Tab-completion enhancements](#Tab-completion_enhancements)
    *   [12.2 Aliases](#Aliases)
    *   [12.3 Alternative shells](#Alternative_shells)
    *   [12.4 Bash additions](#Bash_additions)
    *   [12.5 Colored output](#Colored_output)
    *   [12.6 Compressed files](#Compressed_files)
    *   [12.7 Console prompt](#Console_prompt)
    *   [12.8 Emacs shell](#Emacs_shell)
    *   [12.9 Mouse support](#Mouse_support)
    *   [12.10 Scrollback buffer](#Scrollback_buffer)
    *   [12.11 Session management](#Session_management)

## System administration

This section deals with administrative tasks and system management. For more, please see [Core utilities](/index.php/Core_utilities "Core utilities") and [Category:System administration](/index.php/Category:System_administration "Category:System administration").

### Users and groups

A new installation leaves you with only the [superuser](https://en.wikipedia.org/wiki/Superuser "wikipedia:Superuser") account, better known as "root". Logging in as root for prolonged periods of time, possibly even exposing it via [SSH](/index.php/SSH "SSH") on a server, [is insecure](https://apple.stackexchange.com/questions/192365/is-it-ok-to-use-the-root-user-as-a-normal-user/192422#192422). Instead, you should create and use unprivileged user account(s) for most tasks, only using the root account for system administration. See [Users and groups#User management](/index.php/Users_and_groups#User_management "Users and groups") for details.

Users and groups are a mechanism for *access control*; administrators may fine-tune group membership and ownership to grant or deny users and services access to system resources. Read the [Users and groups](/index.php/Users_and_groups "Users and groups") article for details and potential security risks.

### Privilege escalation

Both the [su](/index.php/Su "Su") and [sudo](/index.php/Sudo "Sudo") commands allow you to run commands as another user. By default *su* drops you to a login shell as the root user, and *sudo* by default temporarily grants you root privileges for a single command. See their respective articles for differences.

### Service management

Arch Linux uses [systemd](/index.php/Systemd "Systemd") as the [init](/index.php/Init "Init") process, which is a system and service manager for Linux. For maintaining your Arch Linux installation, it is a good idea to learn the basics about it. Interaction with *systemd* is done through the *systemctl* command. Read [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd") for more information.

### System maintenance

Arch is a rolling release system and has rapid package turnover, so users have to take some time to do [system maintenance](/index.php/System_maintenance "System maintenance"). Read [Security](/index.php/Security "Security") for recommendations and best practices on hardening the system.

## Package management

This section contains helpful information related to package management. For more, please see [FAQ#Package management](/index.php/FAQ#Package_management "FAQ") and [Category:Package management](/index.php/Category:Package_management "Category:Package management").

**Note:** It is imperative to keep up to date with changes in Arch Linux that require manual intervention **before** upgrading your system. Subscribe to the [arch-announce mailing list](https://mailman.archlinux.org/mailman/listinfo/arch-announce/) or check the front page [Arch news](https://www.archlinux.org/) every time before you update. Alternatively, you may find it useful to subscribe to [this RSS feed](https://www.archlinux.org/feeds/news/).

### pacman

[pacman](/index.php/Pacman "Pacman") is the Arch Linux *pac*kage *man*ager: all users are required to become familiar with it before reading any other articles.

See [pacman/Tips and tricks](/index.php/Pacman/Tips_and_tricks "Pacman/Tips and tricks") for suggestions on how to improve your interaction with *pacman* and package management in general.

### Repositories

See the [Official repositories](/index.php/Official_repositories "Official repositories") article for details about the purpose of each officially maintained repository.

If you plan on using 32-bit applications, you will want to enable the [multilib](/index.php/Multilib "Multilib") repository.

The [Unofficial user repositories](/index.php/Unofficial_user_repositories "Unofficial user repositories") article lists several other unsupported repositories.

You may consider installing the [pkgstats](/index.php/Pkgstats "Pkgstats") service.

### Mirrors

Visit the [Mirrors](/index.php/Mirrors "Mirrors") article for steps on taking full advantage of using the fastest and most up to date mirrors of the official repositories. As explained in the article, a particularly good advice is to routinely check the [Mirror Status](https://www.archlinux.org/mirrors/status/) page for a list of mirrors that have been recently synced.

### Arch Build System

*Ports* is a system initially used by BSD distributions consisting of build scripts that reside in a directory tree on the local system. Simply put, each port contains a script within a directory intuitively named after the installable third-party application.

The [Arch Build System](/index.php/Arch_Build_System "Arch Build System") offers the same functionality by providing build scripts called [PKGBUILDs](/index.php/PKGBUILD "PKGBUILD"), which are populated with information for a given piece of software; integrity hashes, project URL, version, license and build instructions. These PKGBUILDs are later parsed by [makepkg](/index.php/Makepkg "Makepkg"), the actual program that generates packages is cleanly manageable by *pacman*.

Every package in the repositories along with those present in the AUR are subject to recompilation with *makepkg*.

### Arch User Repository

While the Arch Build System allows the ability of building software available in the official repositories, the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") (AUR) is the equivalent for user submitted packages. It is an unsupported repository of build scripts accessible through the [web interface](https://aur.archlinux.org/) or through the [Aurweb RPC interface](/index.php/Aurweb_RPC_interface "Aurweb RPC interface").

## Booting

This section contains information pertaining to the boot process. An overview of the Arch boot process can be found at [Arch boot process](/index.php/Arch_boot_process "Arch boot process"). For more, please see [Category:Boot process](/index.php/Category:Boot_process "Category:Boot process").

### Hardware auto-recognition

Hardware should be auto-detected by [udev](/index.php/Udev "Udev") during the boot process by default. A potential improvement in boot time can be achieved by disabling module auto-loading and specifying required modules manually, as described in [Kernel modules](/index.php/Kernel_modules "Kernel modules"). Additionally, [Xorg](/index.php/Xorg "Xorg") should be able to auto-detect required drivers using `udev`, but users have the option to configure the X server manually too.

### Microcode

Processors may have [faulty behaviour](http://www.anandtech.com/show/8376/intel-disables-tsx-instructions-erratum-found-in-haswell-haswelleep-broadwelly), which the kernel can correct by updating the *microcode* on startup. See [Microcode](/index.php/Microcode "Microcode") for details.

### Retaining boot messages

Once it concludes, the screen is cleared and the login prompt appears, leaving users unable to gather feedback from the boot process. [Disable clearing of boot messages](/index.php/Disable_clearing_of_boot_messages "Disable clearing of boot messages") to overcome this limitation.

### Num Lock activation

Num Lock is a toggle key found in most keyboards. For activating Num Lock's number key-assignment during startup, see [Activating Numlock on Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup").

## Graphical user interface

This section provides orientation for users wishing to run graphical applications on their system. See [Category:Graphical user interfaces](/index.php/Category:Graphical_user_interfaces "Category:Graphical user interfaces") for additional resources.

### Display server

[Xorg](/index.php/Xorg "Xorg") is the public, open-source implementation of the [X Window System](https://en.wikipedia.org/wiki/X_Window_System "wikipedia:X Window System") (commonly X11, or X). It is required for running applications with graphical user interfaces (GUIs), and the majority of users will want to install it.

[Wayland](/index.php/Wayland "Wayland") is a newer, alternative display server protocol and the Weston reference implementation is available.

### Display drivers

The default *vesa* display driver will work with most video cards, but performance can be significantly improved and additional features harnessed by installing the appropriate driver for [ATI](/index.php/ATI "ATI"), [Intel](/index.php/Intel "Intel"), or [NVIDIA](/index.php/NVIDIA "NVIDIA") products.

### Desktop environments

Although Xorg provides the basic framework for building a graphical environment, additional components may be considered necessary for a complete user experience. [Desktop environments](/index.php/Desktop_environment "Desktop environment") such as [GNOME](/index.php/GNOME "GNOME"), [KDE](/index.php/KDE "KDE"), [LXDE](/index.php/LXDE "LXDE"), and [Xfce](/index.php/Xfce "Xfce") bundle together a wide range of *X clients*, such as a window manager, panel, file manager, terminal emulator, text editor, icons, and other utilities. Users with less experience may wish to install a desktop environment for a more familiar environment. See [Category:Desktop environments](/index.php/Category:Desktop_environments "Category:Desktop environments") for additional resources.

### Window managers

A full-fledged desktop environment provides a complete and consistent graphical user interface, but tends to consume a considerable amount of system resources. Users seeking to maximize performance or otherwise simplify their environment may opt to install a [window manager](/index.php/Window_manager "Window manager") alone and hand-pick desired extras. Most desktop environments allow use of an alternative window manager as well. [Dynamic](/index.php/Category:Dynamic_WMs "Category:Dynamic WMs"), [stacking](/index.php/Category:Stacking_WMs "Category:Stacking WMs"), and [tiling](/index.php/Category:Tiling_WMs "Category:Tiling WMs") window managers differ in their handling of window placement.

### Display manager

Most desktop environments include a [display manager](/index.php/Display_manager "Display manager") for automatically starting the graphical environment and managing user logins. Users without a desktop environment can install one separately. Alternatively you may [start X at login](/index.php/Start_X_at_login "Start X at login") as a simple alternative to a display manager.

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

Users may additionally wish to install and configure a [sound server](/index.php/Sound_system#Sound_servers "Sound system") such as [PulseAudio](/index.php/PulseAudio "PulseAudio"). For advanced audio requirements, see [professional audio](/index.php/Professional_audio "Professional audio").

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

A firewall can provide an extra layer of protection on top of the Linux networking stack. While the stock Arch kernel is capable of using [Netfilter](https://en.wikipedia.org/wiki/Netfilter "wikipedia:Netfilter")'s [iptables](/index.php/Iptables "Iptables") and [nftables](/index.php/Nftables "Nftables"), neither are enabled by default. It is highly recommended to set up some form of firewall. See [Category:Firewalls](/index.php/Category:Firewalls "Category:Firewalls") for available guides.

### Resource sharing

To share files among the machines in a network, follow the [NFS](/index.php/NFS "NFS") or the [SSHFS](/index.php/SSHFS "SSHFS") article.

Use [Samba](/index.php/Samba "Samba") to join a Windows network. To configure the machine to use Active Directory for authentication, read [Active Directory Integration](/index.php/Active_Directory_Integration "Active Directory Integration").

See also [Category:Network sharing](/index.php/Category:Network_sharing "Category:Network sharing").

## Input devices

This section contains popular input device configuration tips. For more, please see [Category:Input devices](/index.php/Category:Input_devices "Category:Input devices").

### Keyboard layouts

Non-English or otherwise non-standard keyboards may not function as expected by default. The necessary steps to configure the keymap are different for virtual console and [Xorg](/index.php/Xorg "Xorg"), they are described in [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") and [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") respectively.

### Mouse buttons

Owners of advanced or unusual mice may find that not all mouse buttons are recognized by default, or may wish to assign different actions for extra buttons. Instructions can be found in [Mouse buttons](/index.php/Mouse_buttons "Mouse buttons").

### Laptop touchpads

Many laptops use [Synaptics](https://www.synaptics.com/) or [ALPS](http://www.alps.com/) "touchpad" pointing devices. For these, and several other touchpad models, you can use either the Synaptics input driver or libinput; see [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics") and [libinput](/index.php/Libinput "Libinput") for installation and configuration details.

### TrackPoints

See the [TrackPoint](/index.php/TrackPoint "TrackPoint") article to configure your TrackPoint device.

## Optimization

This section aims to summarize tweaks, tools and available options useful to improve system and application performance.

### Benchmarking

[Benchmarking](/index.php/Benchmarking "Benchmarking") is the act of measuring performance and comparing the results to another system's results or a widely accepted standard through a unified procedure.

### Improving performance

The [Improving performance](/index.php/Improving_performance "Improving performance") article gathers information and is a basic rundown about gaining performance in Arch Linux.

### Solid state drives

The [Solid State Drives](/index.php/Solid_State_Drives "Solid State Drives") article covers many aspects of solid state drives, including configuring them to maximize their lifetimes.

## System service

This section relates to [daemons](/index.php/Daemons "Daemons"). For more, please see [Category:Daemons and system services](/index.php/Category:Daemons_and_system_services "Category:Daemons and system services").

### File index and search

Most distributions have a *locate* command available to be able to quickly search for files. To get this functionality in Arch Linux, [mlocate](https://www.archlinux.org/packages/?name=mlocate) is the recommended install. After the install you should run *updatedb* to index the filesystems.

[Desktop search engines](/index.php/List_of_applications/Utilities#Finders "List of applications/Utilities") provide a similar service, while better integrated into [desktop environments](/index.php/Desktop_environment "Desktop environment").

### Local mail delivery

A default setup does not provide a way to sync mail. To configure *Postfix* for simple local mailbox delivery, see [Postfix](/index.php/Postfix "Postfix"). Other options are [SSMTP](/index.php/SSMTP "SSMTP"), [msmtp](/index.php/Msmtp "Msmtp") and [fdm](/index.php/Fdm "Fdm").

### Printing

[CUPS](/index.php/CUPS "CUPS") is a standards-based, open source printing system developed by Apple. See [Category:Printers](/index.php/Category:Printers "Category:Printers") for printer-specific articles.

## Appearance

This section contains frequently-sought "eye candy" tweaks for an aesthetically pleasing Arch experience. For more, please see [Category:Eye candy](/index.php/Category:Eye_candy "Category:Eye candy").

### Fonts

You may wish to install a set of TrueType fonts, as only unscalable bitmap fonts are included in a basic Arch system. There are several general-purpose [font families](/index.php/Fonts#Families "Fonts") providing large [Unicode](https://en.wikipedia.org/wiki/Unicode "wikipedia:Unicode") coverage and even [metric compatibility](/index.php/Metric-compatible_fonts "Metric-compatible fonts") with fonts from other operating systems.

A plethora of information on the subject can be found in the [Fonts](/index.php/Fonts "Fonts") and [Font configuration](/index.php/Font_configuration "Font configuration") articles.

If spending a significant amount of time working from the virtual console (i.e. outside an X server), users may wish to change the console font to improve readability; see [Fonts#Console fonts](/index.php/Fonts#Console_fonts "Fonts").

### GTK+ and Qt themes

A big part of the applications with a graphical interface for Linux systems are based on the [GTK+](/index.php/GTK%2B "GTK+") or the [Qt](/index.php/Qt "Qt") toolkits. See those articles and [Uniform look for Qt and GTK applications](/index.php/Uniform_look_for_Qt_and_GTK_applications "Uniform look for Qt and GTK applications") for ideas to improve the appearance of your installed programs and adapt it to your liking.

## Console improvements

This section applies to small modifications that improve console programs' practicality. For more, please see [Category:Command shells](/index.php/Category:Command_shells "Category:Command shells").

### Tab-completion enhancements

It is recommended to properly set up extended [tab completion](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion") right away, as instructed in the article of your chosen shell.

### Aliases

Aliasing a command, or a group thereof, is a way of saving time when using the console. This is specially helpful for repetitive tasks that do not need significant alteration to their parameters between executions. Common time-saving aliases can be found in [Bash#Aliases](/index.php/Bash#Aliases "Bash"), which are easily portable to [zsh](/index.php/Zsh "Zsh") as well.

### Alternative shells

[Bash](/index.php/Bash "Bash") is the shell that is installed by default in an Arch system. The live installation media, however, uses [zsh](/index.php/Zsh "Zsh") with the [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config) addon package. See [Command-line shell#List of shells](/index.php/Command-line_shell#List_of_shells "Command-line shell") for more alternatives.

### Bash additions

A list of miscellaneous Bash settings, history search and [Readline](/index.php/Readline "Readline") macros is available in [Bash#Tips and tricks](/index.php/Bash#Tips_and_tricks "Bash").

### Colored output

This section is covered in [Color output in console](/index.php/Color_output_in_console "Color output in console").

### Compressed files

Compressed files, or archives, are frequently encountered on a GNU/Linux system. [Tar](/index.php/Tar "Tar") is one of the most commonly used archiving tools, and users should be familiar with its syntax (Arch Linux packages, for example, are simply xzipped tarballs). See [Archiving and compression](/index.php/Archiving_and_compression "Archiving and compression").

### Console prompt

The console prompt (PS1) can be customized to a great extent. See [Bash/Prompt customization](/index.php/Bash/Prompt_customization "Bash/Prompt customization") or [Zsh#Prompts](/index.php/Zsh#Prompts "Zsh") if using Bash or Zsh, respectively.

### Emacs shell

Emacs is known for featuring options beyond the duties of regular text editing, one of these being a full shell replacement. Consult [Emacs#Colored output issues](/index.php/Emacs#Colored_output_issues "Emacs") for a fix regarding garbled characters that may result from enabling colored output.

### Mouse support

Using a mouse with the console for copy-paste operations can be preferred over [GNU Screen](/index.php/GNU_Screen "GNU Screen")'s traditional copy mode. Refer to [Console mouse support](/index.php/Console_mouse_support "Console mouse support") for comprehensive directions. Note that you can already do this in [terminal emulators](/index.php/Terminal_emulators "Terminal emulators") with the [clipboard](/index.php/Clipboard "Clipboard").

### Scrollback buffer

To be able to save and view text which has scrolled off the screen, refer to [General troubleshooting#Scrollback](/index.php/General_troubleshooting#Scrollback "General troubleshooting").

### Session management

Using terminal multiplexers like [tmux](/index.php/Tmux "Tmux") or [GNU Screen](/index.php/GNU_Screen "GNU Screen"), programs may be run under sessions composed of tabs and panes that can be detached at will, so when the user either kills the terminal emulator, terminates [X](/index.php/X "X"), or logs off, the programs associated with the session will continue to run in the background as long as the terminal multiplexer server is active. Interacting with the programs requires reattaching to the session.