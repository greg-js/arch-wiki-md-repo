**[List of applications](/index.php/List_of_applications "List of applications")**

* * *

[Internet](/index.php/List_of_applications/Internet "List of applications/Internet") – [Multimedia](/index.php/List_of_applications/Multimedia "List of applications/Multimedia") – **Utilities** – [Documents](/index.php/List_of_applications/Documents "List of applications/Documents") – [Security](/index.php/List_of_applications/Security "List of applications/Security") – [Science](/index.php/List_of_applications/Science "List of applications/Science") – [Other](/index.php/List_of_applications/Other "List of applications/Other")

## Contents

*   [1 Utilities](#Utilities)
    *   [1.1 Partitioning tools](#Partitioning_tools)
    *   [1.2 Mount tools](#Mount_tools)
        *   [1.2.1 Udisks](#Udisks)
    *   [1.3 Basic shell commands](#Basic_shell_commands)
    *   [1.4 getty](#getty)
    *   [1.5 Integrated development environments](#Integrated_development_environments)
    *   [1.6 Build automation](#Build_automation)
    *   [1.7 Terminal emulators](#Terminal_emulators)
        *   [1.7.1 VTE-based](#VTE-based)
        *   [1.7.2 KMS-based](#KMS-based)
        *   [1.7.3 framebuffer-based](#framebuffer-based)
    *   [1.8 Files](#Files)
        *   [1.8.1 File managers](#File_managers)
            *   [1.8.1.1 Console](#Console)
            *   [1.8.1.2 Graphical](#Graphical)
        *   [1.8.2 Trash management](#Trash_management)
        *   [1.8.3 File synchronization](#File_synchronization)
        *   [1.8.4 Archiving and compression tools](#Archiving_and_compression_tools)
            *   [1.8.4.1 Console](#Console_2)
            *   [1.8.4.2 Graphical](#Graphical_2)
        *   [1.8.5 Comparison, diff, merge](#Comparison.2C_diff.2C_merge)
        *   [1.8.6 Batch renamers](#Batch_renamers)
        *   [1.8.7 Search and replace](#Search_and_replace)
    *   [1.9 Disk cleaning](#Disk_cleaning)
    *   [1.10 Disk usage display](#Disk_usage_display)
    *   [1.11 Clock synchronization](#Clock_synchronization)
    *   [1.12 System maintenance](#System_maintenance)
    *   [1.13 System monitoring](#System_monitoring)
    *   [1.14 System information viewers](#System_information_viewers)
        *   [1.14.1 Console](#Console_3)
        *   [1.14.2 Graphical](#Graphical_3)
        *   [1.14.3 Others](#Others)
    *   [1.15 Keyboard layout switchers](#Keyboard_layout_switchers)
    *   [1.16 Power management](#Power_management)
    *   [1.17 Clipboard managers](#Clipboard_managers)
    *   [1.18 Wallpaper setters](#Wallpaper_setters)
    *   [1.19 Package management](#Package_management)
    *   [1.20 Input method editor](#Input_method_editor)
    *   [1.21 Finders](#Finders)

## Utilities

### Partitioning tools

See [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").

### Mount tools

*   **9mount** — Mount 9p filesystems.

	[http://sqweek.net/code/9mount/](http://sqweek.net/code/9mount/) || [9mount](https://aur.archlinux.org/packages/9mount/)

*   **cryptmount** — Mount an encrypted file system as a regular user.

	[https://sourceforge.net/projects/cryptmount/](https://sourceforge.net/projects/cryptmount/) || [cryptmount](https://aur.archlinux.org/packages/cryptmount/)

*   **ldm** — A lightweight daemon that mounts drives automagically using *udev*

	[https://github.com/LemonBoy/ldm](https://github.com/LemonBoy/ldm) || [ldm](https://aur.archlinux.org/packages/ldm/)

*   **pmount** — Mount *source* as a regular user to an automatically created destination `/media/*source_name*`.

	[https://pmount.alioth.debian.org/](https://pmount.alioth.debian.org/) || [pmount](https://aur.archlinux.org/packages/pmount/)

*   **pmount-safe-removal** — Mount removable devices as regular user with safe removal

	[https://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device](https://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device) || [pmount-safe-removal](https://aur.archlinux.org/packages/pmount-safe-removal/)

*   **udevil** — Mounts removable devices as a regular user, show device info, and monitor device changes. Only depends on *udev* and glib.

	[https://ignorantguru.github.io/udevil](https://ignorantguru.github.io/udevil) || [udevil](https://www.archlinux.org/packages/?name=udevil)

*   **ws** — Mount Windows network shares ([CIFS](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") and [VFS](https://en.wikipedia.org/wiki/Virtual_file_system "wikipedia:Virtual file system")).

	[https://sourceforge.net/projects/winshares/](https://sourceforge.net/projects/winshares/) || [ws](https://aur.archlinux.org/packages/ws/)

*   **zulucrypt** — A GUI frontend for cryptsetup to create, manage and mount encrypted volumes; supports encfs as well

	[https://mhogomchungu.github.io/zuluCrypt/](https://mhogomchungu.github.io/zuluCrypt/) || [zulucrypt](https://aur.archlinux.org/packages/zulucrypt/)

#### Udisks

*   **bashmount** — A bash script to mount and manage removable media as a regular user with udisks.

	[https://github.com/jamielinux/bashmount](https://github.com/jamielinux/bashmount) || [bashmount](https://aur.archlinux.org/packages/bashmount/)

*   **udiskie** — Automatic disk mounting service using *udisks*

	[https://pypi.python.org/pypi/udiskie](https://pypi.python.org/pypi/udiskie) || [udiskie](https://www.archlinux.org/packages/?name=udiskie)

*   **udisks_functions** — Bash functions and aliases for *udisks2*

	[https://bbs.archlinux.org/viewtopic.php?id=109307](https://bbs.archlinux.org/viewtopic.php?id=109307) || [udisks_functions](https://aur.archlinux.org/packages/udisks_functions/)

*   **udisksvm** — GUI *udisks* wrapper for removable media

	[https://bbs.archlinux.org/viewtopic.php?id=112397](https://bbs.archlinux.org/viewtopic.php?id=112397) || [udisksvm](https://aur.archlinux.org/packages/udisksvm/)

### Basic shell commands

*   **[Core utilities](/index.php/Core_utilities "Core utilities")** — The basic file, shell and text manipulation utilities of the GNU operating system

	[https://www.gnu.org/software/coreutils/coreutils.html](https://www.gnu.org/software/coreutils/coreutils.html) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

### getty

See [getty#Installation](/index.php/Getty#Installation "Getty").

### Integrated development environments

See also [Wikipedia:Comparison of integrated development environments](https://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments "wikipedia:Comparison of integrated development environments").

*   **[Anjuta](https://en.wikipedia.org/wiki/Anjuta "wikipedia:Anjuta")** — Versatile IDE with project management, an application wizard, an interactive debugger, a source editor, version control support and many more tools.

	[http://www.anjuta.org/](http://www.anjuta.org/) || [anjuta](https://www.archlinux.org/packages/?name=anjuta)

*   **[Aptana Studio](https://en.wikipedia.org/wiki/Aptana#Aptana_Studio "wikipedia:Aptana")** — IDE based on Eclipse, but geared towards web development, with support for HTML, CSS, Javascript, Ruby on Rails, PHP, Adobe AIR and others.

	[http://www.aptana.com/](http://www.aptana.com/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)

*   **[Bluefish](https://en.wikipedia.org/wiki/Bluefish_(text_editor) "wikipedia:Bluefish (text editor)")** — GTK+ editor/IDE with an MDI interface, syntax highlighting and support for Python plugins.

	[http://bluefish.openoffice.nl/](http://bluefish.openoffice.nl/) || [bluefish](https://www.archlinux.org/packages/?name=bluefish)

*   **[Bluej](https://en.wikipedia.org/wiki/Bluej "wikipedia:Bluej")** — Fully featured Java IDE used mainly for educational and beginner purposes.

	[https://bluej.org/](https://bluej.org/) || [bluej](https://aur.archlinux.org/packages/bluej/)

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "wikipedia:Brackets (text editor)")** — A free open-source editor written in HTML, CSS, and Javascript with a primary focus on Web Development. It was created by Adobe Systems, licensed under the MIT License, and is currently maintained on GitHub.

	[http://brackets.io/](http://brackets.io/) || [brackets](https://aur.archlinux.org/packages/brackets/)

*   **[Builder](https://en.wikipedia.org/wiki/GNOME_Builder "wikipedia:GNOME Builder")** — General purpose IDE for GNOME.

	[https://wiki.gnome.org/Apps/Builder](https://wiki.gnome.org/Apps/Builder) || [gnome-builder](https://www.archlinux.org/packages/?name=gnome-builder)

*   **[Code::Blocks](https://en.wikipedia.org/wiki/Code::Blocks "wikipedia:Code::Blocks")** — Open source and cross-platform C/C++ IDE.

	[http://www.codeblocks.org/](http://www.codeblocks.org/) || [codeblocks](https://www.archlinux.org/packages/?name=codeblocks)

*   **[Cloud9](https://en.wikipedia.org/wiki/Cloud9_IDE "wikipedia:Cloud9 IDE")** — State-of-the-art IDE that runs in your browser and lives in the cloud, allowing you to run, debug and deploy applications from anywhere, anytime.

	[https://c9.io/](https://c9.io/) || [c9.core](https://aur.archlinux.org/packages/c9.core/)

*   **[Eclipse](/index.php/Eclipse "Eclipse")** — Open source community project, which aims to provide a universal development platform.

	[https://eclipse.org/](https://eclipse.org/) || [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java), [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp), [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php)

*   **[Editra](https://en.wikipedia.org/wiki/Editra "wikipedia:Editra")** — Multi-platform text editor with an implementation that focuses on creating an easy to use interface and features that aid in code development.

	[http://www.editra.org](http://www.editra.org) || [editra-svn](https://aur.archlinux.org/packages/editra-svn/)

*   **[Eric](https://en.wikipedia.org/wiki/Eric_Python_IDE "wikipedia:Eric Python IDE")** — Full-featured Python and Ruby IDE in PyQt5.

	[https://eric-ide.python-projects.org/](https://eric-ide.python-projects.org/) || [eric](https://www.archlinux.org/packages/?name=eric)

*   **[Gambas](/index.php/Gambas "Gambas")** — Free development environment based on a Basic interpreter with object extensions.

	[http://gambas.sourceforge.net/en/main.html](http://gambas.sourceforge.net/en/main.html) || [gambas3-ide](https://www.archlinux.org/packages/?name=gambas3-ide)

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — Text editor using the GTK+ toolkit with basic features of an integrated development environment.

	[https://geany.org](https://geany.org) || [geany](https://www.archlinux.org/packages/?name=geany)

*   **[IntelliJ IDEA](https://en.wikipedia.org/wiki/IntelliJ_IDEA "wikipedia:IntelliJ IDEA")** — IDE for Java, Groovy and other programming languages with advanced refactoring features.

	[http://www.jetbrains.com/idea/](http://www.jetbrains.com/idea/) || [intellij-idea-community-edition](https://www.archlinux.org/packages/?name=intellij-idea-community-edition)

*   **[KDevelop](https://en.wikipedia.org/wiki/KDevelop "wikipedia:KDevelop")** — Feature-full, plugin extensible IDE for C/C++ and other programming languages.

	[http://kdevelop.org/](http://kdevelop.org/) || [kdevelop](https://www.archlinux.org/packages/?name=kdevelop)

*   **[Komodo Edit](https://en.wikipedia.org/wiki/Komodo_Edit "wikipedia:Komodo Edit")** — A free, multi-language editor.

	[http://www.activestate.com/komodo-edit](http://www.activestate.com/komodo-edit) || [komodo-edit](https://aur.archlinux.org/packages/komodo-edit/)

*   **[Lazarus](https://en.wikipedia.org/wiki/Lazarus_(IDE) "wikipedia:Lazarus (IDE)")** — Cross-platform IDE for Object Pascal.

	[http://lazarus.freepascal.org/](http://lazarus.freepascal.org/) || [lazarus](https://www.archlinux.org/packages/?name=lazarus)

*   **LiteIDE** — A simple, open source, cross-platform Go IDE.

	[https://github.com/visualfc/liteide](https://github.com/visualfc/liteide) || [liteide](https://www.archlinux.org/packages/?name=liteide)

*   **MonkeyStudio** — Monkey Studio (MkS) is a cross platform IDE written in C++/Qt 4\. Syntax highlighting for more than 22 programming languages.

	[http://monkeystudio.org/](http://monkeystudio.org/) || [monkeystudio](https://aur.archlinux.org/packages/monkeystudio/)

*   **[MonoDevelop](https://en.wikipedia.org/wiki/MonoDevelop "wikipedia:MonoDevelop")** — Cross-platform IDE targeted for the Mono and .NET frameworks.

	[http://monodevelop.com/](http://monodevelop.com/) || [monodevelop](https://www.archlinux.org/packages/?name=monodevelop)

*   **[MPLAB](https://en.wikipedia.org/wiki/MPLAB "wikipedia:MPLAB")** — IDE for Microchip PIC and dsPIC development

	[http://www.microchip.com/mplabx](http://www.microchip.com/mplabx) || [microchip-mplabx-bin](https://aur.archlinux.org/packages/microchip-mplabx-bin/)

*   **[Netbeans](/index.php/Netbeans "Netbeans")** — Integrated development environment (IDE) for developing with Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, and other languages.

	[http://netbeans.org/](http://netbeans.org/) || [netbeans](https://www.archlinux.org/packages/?name=netbeans)

*   **[Ninja-IDE](https://en.wikipedia.org/wiki/Ninja-IDE "wikipedia:Ninja-IDE")** — from the recursive acronym: "Ninja-IDE Is Not Just Another IDE", is a cross-platform integrated development environment (IDE); runs on Linux/X11, Mac OS X and Windows OSs. Used, for example, for Python development

	[http://ninja-ide.org/](http://ninja-ide.org/) || [ninja-ide](https://www.archlinux.org/packages/?name=ninja-ide)

*   **[PHPStorm](/index.php/PHPStorm "PHPStorm")** — JetBrains PhpStorm is a commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform, providing an editor for PHP, HTML and JavaScript with on-the-fly code analysis, error prevention and automated refactorings for PHP and JavaScript code.

	[https://www.jetbrains.com/phpstorm/](https://www.jetbrains.com/phpstorm/) || [phpstorm](https://aur.archlinux.org/packages/phpstorm/) [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/)

*   **[PyCharm](https://en.wikipedia.org/wiki/PyCharm "wikipedia:PyCharm")** — IDE used for programming in Python with support for code analysis, debugging, unit testing, version control and web development with Django.

	[http://www.jetbrains.com/pycharm/](http://www.jetbrains.com/pycharm/) || [pycharm-community](https://aur.archlinux.org/packages/pycharm-community/)

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — Lightweight, cross-platform C++ integrated development environment with a focus on Qt.

	[https://www.qt.io/ide/](https://www.qt.io/ide/) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **[Scratch](https://en.wikipedia.org/wiki/Scratch_(programming_language) "wikipedia:Scratch (programming language)")** — A multimedia authoring tool for educational and entertainment purposes, such as creating interactive projects and simple sprite-based games. It is used primarly by unskilled users (such as children) as an entry to [event-driven programming](https://en.wikipedia.org/wiki/Event-driven_programming "wikipedia:Event-driven programming"). *Scratch* is free software under GPL v2 and [Scratch Source Code License](http://wiki.scratch.mit.edu/wiki/Scratch_Source_Code_License).

	[http://scratch.mit.edu](http://scratch.mit.edu) || [scratch](https://www.archlinux.org/packages/?name=scratch) [scratch2](https://aur.archlinux.org/packages/scratch2/)

*   **[Spyder](https://en.wikipedia.org/wiki/Spyder_(software) "wikipedia:Spyder (software)")** — Scientific PYthon Development EnviRonment providing MATLAB-like features.

	[https://github.com/spyder-ide/spyder](https://github.com/spyder-ide/spyder) || [spyder](https://www.archlinux.org/packages/?name=spyder)

*   **Thonny** — Python IDE for beginners.

	[http://thonny.cs.ut.ee/](http://thonny.cs.ut.ee/) || [thonny](https://aur.archlinux.org/packages/thonny/)

### Build automation

See also [Wikipedia:List of build automation software](https://en.wikipedia.org/wiki/List_of_build_automation_software "wikipedia:List of build automation software").

*   **Apache Ant** — Java library and command-line tool whose mission is to drive processes described in build files as targets and extension points dependent upon each other.

	[http://ant.apache.org/](http://ant.apache.org/) || [apache-ant](https://www.archlinux.org/packages/?name=apache-ant)

*   **Apache Maven** — Software project management and comprehension tool.

	[http://maven.apache.org/](http://maven.apache.org/) || [maven](https://www.archlinux.org/packages/?name=maven)

*   **Gradle** — Powerful build system for the JVM.

	[https://gradle.org/](https://gradle.org/) || [gradle](https://www.archlinux.org/packages/?name=gradle)

*   **Phing** — PHP program designed to automate tasks of all kinds.

	[https://www.phing.info/](https://www.phing.info/) || [phing](https://aur.archlinux.org/packages/phing/)

### Terminal emulators

Terminal emulators show a GUI Window that contains a terminal. Most emulate Xterm, which in turn emulates VT102, which emulates typewriter. For further background information, see [Wikipedia:Terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator").

For a comprehensive list, see [Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators").

*   **[aterm](https://en.wikipedia.org/wiki/aterm "wikipedia:aterm")** — Xterm replacement with transparency support. It has been deprecated in favour of urxvt since 2008.

	[http://aterm.sourceforge.net/](http://aterm.sourceforge.net/) || [aterm](https://aur.archlinux.org/packages/aterm/)

*   **Cool Retro Term** — A good looking terminal emulator which mimics the old cathode display.

	[https://github.com/Swordfish90/cool-retro-term](https://github.com/Swordfish90/cool-retro-term) || [cool-retro-term](https://www.archlinux.org/packages/?name=cool-retro-term)

*   **Eterm** — Terminal emulator intended as a replacement for xterm and designed for the [Enlightenment](/index.php/Enlightenment "Enlightenment") desktop.

	[http://eterm.org](http://eterm.org) || [eterm](https://aur.archlinux.org/packages/eterm/)

*   **Gate One** — Web-based terminal emulator and SSH client.

	[https://github.com/liftoff/GateOne](https://github.com/liftoff/GateOne) || [gateone-git](https://aur.archlinux.org/packages/gateone-git/)

*   **[Konsole](https://en.wikipedia.org/wiki/Konsole "wikipedia:Konsole")** — Terminal emulator included in the [KDE](/index.php/KDE "KDE") desktop.

	[http://kde.org/applications/system/konsole/](http://kde.org/applications/system/konsole/) || [konsole](https://www.archlinux.org/packages/?name=konsole)

*   **mlterm** — A multi-lingual terminal emulator supporting various character sets and encodings in the world.

	[http://sourceforge.net/projects/mlterm/](http://sourceforge.net/projects/mlterm/) || [mlterm](https://aur.archlinux.org/packages/mlterm/)

*   **[Mrxvt](https://en.wikipedia.org/wiki/mrxvt "wikipedia:mrxvt")** — Tabbed X terminal emulator based on rxvt.

	[http://materm.sourceforge.net/wiki/pmwiki.php](http://materm.sourceforge.net/wiki/pmwiki.php) || [mrxvt](https://aur.archlinux.org/packages/mrxvt/)

*   **QTerminal** — A lightweight Qt-based terminal emulator.

	[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal](https://www.archlinux.org/packages/?name=qterminal)

*   **[rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt")** — Popular replacement for the xterm.

	[http://rxvt.sourceforge.net/](http://rxvt.sourceforge.net/) || [rxvt](https://aur.archlinux.org/packages/rxvt/)

*   **shellinabox** — A web-based SSH Terminal

	[https://github.com/shellinabox/shellinabox](https://github.com/shellinabox/shellinabox) || [shellinabox-git](https://aur.archlinux.org/packages/shellinabox-git/)

*   **[st](/index.php/St "St")** — Simple terminal implementation for X.

	[http://st.suckless.org](http://st.suckless.org) || [st](https://www.archlinux.org/packages/?name=st)

*   **Terminal** — A terminal emulator, that supports multiple windows, scroll buffer and all the expected features. A part of GNUstep.

	[http://gap.nongnu.org/terminal/index.html](http://gap.nongnu.org/terminal/index.html) || [gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/)

*   **Terminology** — Terminal emulator by the Enlightenment project team with innovative features: file thumbnails and media play like a media player.

	[http://enlightenment.org/p.php?p=about/terminology](http://enlightenment.org/p.php?p=about/terminology) || [terminology](https://www.archlinux.org/packages/?name=terminology)

*   **[Tilda](/index.php/Tilda "Tilda")** — Terminal inspired by many classic terminals from first person shooter games such as Quake, Doom and Half-Life.

	[https://github.com/lanoxx/tilda/](https://github.com/lanoxx/tilda/) || [tilda](https://www.archlinux.org/packages/?name=tilda)

*   **[urxvt](/index.php/Urxvt "Urxvt")** — Highly extendable (with Perl) unicode enabled rxvt-clone terminal emulator featuring tabbing, url launching, a Quake style drop-down mode and pseudo-transparency.

	[http://software.schmorp.de/pkg/rxvt-unicode.html](http://software.schmorp.de/pkg/rxvt-unicode.html) || [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode)

*   **[xterm](/index.php/Xterm "Xterm")** — Simple terminal emulator for the X Window System. It provides DEC VT102 and Tektronix 4014 compatible terminals for programs that can't use the window system directly.

	[http://invisible-island.net/xterm/](http://invisible-island.net/xterm/) || [xterm](https://www.archlinux.org/packages/?name=xterm)

*   **[Yakuake](https://en.wikipedia.org/wiki/Yakuake "wikipedia:Yakuake")** — Drop-down terminal (Quake style) emulator based on Konsole.

	[http://yakuake.kde.org/](http://yakuake.kde.org/) || [yakuake](https://www.archlinux.org/packages/?name=yakuake)

#### VTE-based

[VTE](http://developer.gnome.org/vte/unstable/) (Virtual Terminal Emulator) is a widget developed during early GNOME days for use in the GNOME Terminal. It has since given birth to many terminals with similar capabilities.

*   **evilvte** — Very lightweight and highly customizable terminal emulator with support for tabs, auto-hiding and different encodings.

	[http://calno.com/evilvte/](http://calno.com/evilvte/) || [evilvte](https://aur.archlinux.org/packages/evilvte/)

*   **Germinal** — Minimalist terminal emulator which provides a borderless maximized terminal, attached to a tmux session by default, hence providing tabs and panels.

	[http://www.imagination-land.org/tags/germinal.html](http://www.imagination-land.org/tags/germinal.html) || [germinal](https://aur.archlinux.org/packages/germinal/)

*   **[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")** — A terminal emulator included in the [GNOME](/index.php/GNOME "GNOME") desktop with support for Unicode and pseudo-transparency.

	[https://wiki.gnome.org/Apps/Terminal](https://wiki.gnome.org/Apps/Terminal) || [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)

*   **[Guake](/index.php/Guake "Guake")** — Drop-down terminal for the GNOME desktop.

	[http://guake-project.org/](http://guake-project.org/) || [guake](https://www.archlinux.org/packages/?name=guake)

*   **[LilyTerm](/index.php/LilyTerm "LilyTerm")** — Very light and easy to use X Terminal Emulator

	[http://lilyterm.luna.com.tw/](http://lilyterm.luna.com.tw/) || [lilyterm](https://www.archlinux.org/packages/?name=lilyterm)

*   **LXTerminal** — Desktop independent terminal emulator for [LXDE](/index.php/LXDE "LXDE").

	[http://wiki.lxde.org/en/LXTerminal](http://wiki.lxde.org/en/LXTerminal) || [lxterminal](https://www.archlinux.org/packages/?name=lxterminal)

*   **MATE terminal** — A fork of [Wikipedia:GNOME terminal](https://en.wikipedia.org/wiki/GNOME_terminal "wikipedia:GNOME terminal") for the [MATE](/index.php/MATE "MATE") desktop.

	[http://www.mate-desktop.org/](http://www.mate-desktop.org/) || [mate-terminal](https://www.archlinux.org/packages/?name=mate-terminal)

*   **Pantheon Terminal** — A super lightweight, beautiful, and simple terminal emulator. It's designed to be setup with sane defaults and little to no configuration.

	[https://launchpad.net/pantheon-terminal](https://launchpad.net/pantheon-terminal) || [pantheon-terminal](https://www.archlinux.org/packages/?name=pantheon-terminal)

*   **ROXTerm** — Tabbed terminal emulator with a small footprint.

	[http://roxterm.sourceforge.net/](http://roxterm.sourceforge.net/) || [roxterm](https://www.archlinux.org/packages/?name=roxterm)

*   **sakura** — Terminal emulator based on GTK+ and VTE.

	[http://www.pleyades.net/david/projects/sakura](http://www.pleyades.net/david/projects/sakura) || [sakura](https://www.archlinux.org/packages/?name=sakura)

*   **[Terminal](https://en.wikipedia.org/wiki/Terminal_(Xfce) "wikipedia:Terminal (Xfce)")** — Terminal emulator included in the [Xfce](/index.php/Xfce "Xfce") desktop with support for a colorized prompt and a tabbed interface.

	[http://docs.xfce.org/apps/terminal/start](http://docs.xfce.org/apps/terminal/start) || [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)

*   **[terminator](/index.php/Terminator "Terminator")** — Terminal emulator supporting multiple resizable terminal panels.

	[http://gnometerminator.blogspot.it/](http://gnometerminator.blogspot.it/) || [terminator](https://www.archlinux.org/packages/?name=terminator)

*   **Terminix** — A tiling terminal emulator for Linux using GTK+ 3

	[https://github.com/gnunn1/terminix](https://github.com/gnunn1/terminix) || [terminix](https://aur.archlinux.org/packages/terminix/), [terminix-git](https://aur.archlinux.org/packages/terminix-git/)

*   **Termit** — Simple terminal emulator based on the vte library that includes tabs, bookmarks, and the ability to switch encodings.

	[https://github.com/nonstop/termit/wiki](https://github.com/nonstop/termit/wiki) || [termit](https://aur.archlinux.org/packages/termit/)

*   **[Termite](/index.php/Termite "Termite")** — A keyboard-centric VTE-based terminal, aimed at use within a window manager with tiling and/or tabbing support.

	[https://github.com/thestinger/termite](https://github.com/thestinger/termite) || [termite](https://www.archlinux.org/packages/?name=termite)

*   **Terra** — is a GTK+3.0 based terminal emulator with useful user interface, it also supports multiple terminals with splitting screen horizontally or vertically -- (similar to guake).

	[https://github.com/ozcan/terra-terminal](https://github.com/ozcan/terra-terminal) || [terra](https://aur.archlinux.org/packages/terra/)

*   **tinyterm** — Very lightweight terminal emulator based on VTE.

	[https://github.com/lahwaacz/tinyterm](https://github.com/lahwaacz/tinyterm) || [tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/)

#### KMS-based

The following terminal emulators are based on the [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") that could be invoked without X.

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — A KMS/DRM-based system console(getty) with an integrated terminal emulator for Linux operating systems.

	[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

#### framebuffer-based

In GNU/Linux world, the [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") could be refered to a virtual device in the Linux kernel (**fbdev**) or the virtual framebuffer system for X (**xvfb**). This section mainly lists the terminal emulators that based on the in-kernel virtual device, i.e. **fbdev**.

*   **[fbterm](/index.php/Fbterm "Fbterm")** — A fast framebuffer-based terminal emulator with many amazing features. Development stopped.

	[https://code.google.com/archive/p/fbterm/](https://code.google.com/archive/p/fbterm/) || [fbterm](https://www.archlinux.org/packages/?name=fbterm)

*   **yaft** — A simple terminal emulator for living without X, with UCS2 glyphs, wallpaper and 256color support.

	[https://github.com/uobikiemukot/yaft](https://github.com/uobikiemukot/yaft) || [yaft](https://aur.archlinux.org/packages/yaft/)

### Files

#### File managers

See also [Wikipedia:Comparison of file managers](https://en.wikipedia.org/wiki/Comparison_of_file_managers "wikipedia:Comparison of file managers").

##### Console

*   **Clex** — File manager with full-screen user interface

	[http://www.clex.sk/](http://www.clex.sk/) || [clex](https://aur.archlinux.org/packages/clex/)

*   **[Dired](https://en.wikipedia.org/wiki/Dired "wikipedia:Dired")** — Directory editor integrated with [Emacs](/index.php/Emacs "Emacs").

	[http://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html](http://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **dired** — Ancient DIRectory EDitor since 1980.

	[http://fossies.org/linux/misc/old/](http://fossies.org/linux/misc/old/) || [dired](https://aur.archlinux.org/packages/dired/)

*   **Last File Manager** — Powerful file manager written in Python 3 with a curses interface.

	[https://inigo.katxi.org/devel/lfm/](https://inigo.katxi.org/devel/lfm/) || [lfm](https://aur.archlinux.org/packages/lfm/)

*   **[Midnight Commander](/index.php/Midnight_Commander "Midnight Commander")** — Console-based, dual-paneled file manager.

	[http://www.midnight-commander.org](http://www.midnight-commander.org) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **nffm** — "Nothing Fancy File Manager", a mouseless ncurses file manager written in C.

	[https://github.com/mariostg/nffm](https://github.com/mariostg/nffm) || [nffm-git](https://aur.archlinux.org/packages/nffm-git/)

*   **Pilot** — File manager that comes with the [Alpine](/index.php/Alpine "Alpine") email client.

	[http://patches.freeiz.com/alpine/](http://patches.freeiz.com/alpine/) || [alpine](https://aur.archlinux.org/packages/alpine/)

*   **[Ranger](/index.php/Ranger "Ranger")** — Console-based file manager with vi bindings, customizability, and lots of features.

	[http://nongnu.org/ranger](http://nongnu.org/ranger) || [ranger](https://www.archlinux.org/packages/?name=ranger)

*   **[Vifm](/index.php/Vifm "Vifm")** — Ncurses-based two-panel file manager with vi-like keybindings.

	[http://vifm.info](http://vifm.info) || [vifm](https://www.archlinux.org/packages/?name=vifm)

##### Graphical

*   **Andromeda** — Qt-based cross-platform file manager.

	[https://github.com/ABBAPOH/Andromeda/](https://github.com/ABBAPOH/Andromeda/) || [andromeda](https://aur.archlinux.org/packages/andromeda/)

*   **Caja** — The file manager for the MATE desktop.

	[https://github.com/mate-desktop/caja](https://github.com/mate-desktop/caja) || [caja](https://www.archlinux.org/packages/?name=caja)

*   **Deepin File Manager** — File manager developed for [Deepin](/index.php/Deepin "Deepin").

	[https://github.com/linuxdeepin/dde-file-manager](https://github.com/linuxdeepin/dde-file-manager) || [deepin-file-manager](https://www.archlinux.org/packages/?name=deepin-file-manager)

*   **Dino** — Easy to use and powerful file manager built in Qt.

	[http://dfm.sourceforge.net/](http://dfm.sourceforge.net/) || [dino-dfm](https://aur.archlinux.org/packages/dino-dfm/)

*   **[Dolphin](/index.php/Dolphin "Dolphin")** — File manager included in the KDE desktop.

	[http://dolphin.kde.org/](http://dolphin.kde.org/) || [dolphin](https://www.archlinux.org/packages/?name=dolphin)

*   **Double Commander** — File manager with two panels side by side. It is inspired by Total Commander and features some new ideas.

	[http://doublecmd.sourceforge.net//](http://doublecmd.sourceforge.net//) || [doublecmd-gtk2](https://www.archlinux.org/packages/?name=doublecmd-gtk2) [doublecmd-qt](https://www.archlinux.org/packages/?name=doublecmd-qt)

*   **[emelFM2](https://en.wikipedia.org/wiki/emelFM2 "wikipedia:emelFM2")** — File manager that implements the popular two-panel design.

	[http://emelfm2.net/](http://emelfm2.net/) || [emelfm2](https://www.archlinux.org/packages/?name=emelfm2)

*   **Gentoo** — A lightweight file manager for GTK.

	[http://www.obsession.se/gentoo/](http://www.obsession.se/gentoo/) || [gentoo](https://aur.archlinux.org/packages/gentoo/)

*   **[GNOME Commander](https://en.wikipedia.org/wiki/GNOME_Commander "wikipedia:GNOME Commander")** — A dual-paned file manager for the GNOME Desktop.

	[http://gcmd.github.io/](http://gcmd.github.io/) || [gnome-commander](https://www.archlinux.org/packages/?name=gnome-commander)

*   **[GNOME Files](/index.php/GNOME_Files "GNOME Files")** — Extensible, heavyweight file manager used by default in GNOME with support for custom scripts.

	[https://wiki.gnome.org/Apps/Nautilus](https://wiki.gnome.org/Apps/Nautilus) || [nautilus](https://www.archlinux.org/packages/?name=nautilus)

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — File manager and web browser for the KDE desktop.

	[http://www.konqueror.org/](http://www.konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **[Krusader](https://en.wikipedia.org/wiki/Krusader "wikipedia:Krusader")** — Advanced twin panel (Midnight Commander style) file manager for the KDE desktop.

	[http://www.krusader.org/](http://www.krusader.org/) || [krusader](https://www.archlinux.org/packages/?name=krusader)

*   **muCommander** — A lightweight, cross-platform file manager with a dual-pane interface written in Java.

	[http://www.mucommander.com/](http://www.mucommander.com/) || [mucommander](https://aur.archlinux.org/packages/mucommander/)

*   **[Nemo](/index.php/Nemo "Nemo")** — Nemo is the file manager of the Cinnamon desktop. A fork of Nautilus.

	[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [nemo](https://www.archlinux.org/packages/?name=nemo)

*   **[PathFinder](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit")** — File browser that comes with the FOX toolkit.

	[http://fox-toolkit.org/](http://fox-toolkit.org/) || [fox](https://www.archlinux.org/packages/?name=fox)

*   **[PCManFM](/index.php/PCManFM "PCManFM")** — Lightweight file manager which features tabbed and dual pane browsing; also it can optionally manage the desktop icons and background.

	[http://wiki.lxde.org/en/PCManFM](http://wiki.lxde.org/en/PCManFM) || [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)

*   **qtFM** — Small, lightweight filemanager for Linux desktops based on pure Qt.

	[http://www.qtfm.org/](http://www.qtfm.org/) || [qtfm](https://www.archlinux.org/packages/?name=qtfm)

*   **ROX** — Small and fast file manager which can optionally manage the desktop background and panels.

	[http://rox.sourceforge.net](http://rox.sourceforge.net) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[SpaceFM](/index.php/SpaceFM "SpaceFM")** — GTK+ multi-panel tabbed file manager.

	[http://ignorantguru.github.com/spacefm/](http://ignorantguru.github.com/spacefm/) || [spacefm](https://www.archlinux.org/packages/?name=spacefm)

*   **Sunflower** — Small and highly customizable twin-panel file manager for Linux with support for plugins.

	[http://sunflower-fm.org/](http://sunflower-fm.org/) || [sunflower](https://aur.archlinux.org/packages/sunflower/)

*   **[Thunar](/index.php/Thunar "Thunar")** — File manager that can be run as a daemon with excellent start up and directory load times.

	[http://docs.xfce.org/xfce/thunar/start](http://docs.xfce.org/xfce/thunar/start) || [thunar](https://www.archlinux.org/packages/?name=thunar)

*   **Tux Commander** — Windowed file manager with two panels side by side similar to popular Total Commander or Midnight Commander file managers.

	[http://tuxcmd.sourceforge.net/description.php](http://tuxcmd.sourceforge.net/description.php) || [tuxcmd](https://www.archlinux.org/packages/?name=tuxcmd)

*   **Worker** — Fast, lightweight and feature-rich file manager for the X Window System.

	[http://www.boomerangsworld.de/worker/](http://www.boomerangsworld.de/worker/) || [worker](https://aur.archlinux.org/packages/worker/)

*   **[Xfe](https://en.wikipedia.org/wiki/Xfe "wikipedia:Xfe")** — Microsoft Explorer-like file manager for X (X File Explorer).

	[http://roland65.free.fr/xfe/](http://roland65.free.fr/xfe/) || [xfe](https://www.archlinux.org/packages/?name=xfe)

#### Trash management

*   **trash-cli** — A command-line interface implementing FreeDesktop.org's Trash specification.

	[https://github.com/andreafrancia/trash-cli](https://github.com/andreafrancia/trash-cli) || [trash-cli](https://www.archlinux.org/packages/?name=trash-cli)

#### File synchronization

See [Synchronization and backup programs#Data synchronization](/index.php/Synchronization_and_backup_programs#Data_synchronization "Synchronization and backup programs").

#### Archiving and compression tools

See also [Wikipedia:Comparison of file archivers](https://en.wikipedia.org/wiki/Comparison_of_file_archivers "wikipedia:Comparison of file archivers").

##### Console

*   **atool** — Script for managing file archives of various types.

	[http://www.nongnu.org/atool/](http://www.nongnu.org/atool/) || [atool](https://www.archlinux.org/packages/?name=atool)

*   **arj** — An archiver that formerly used on DOS/Windows in mid-1990s. This is an open source clone.

	[http://arj.sourceforge.net/](http://arj.sourceforge.net/) || [arj](https://www.archlinux.org/packages/?name=arj)

*   **[cpio](https://en.wikipedia.org/wiki/cpio "wikipedia:cpio")** — GNU tool supporting cpio and tar file archive formats.

	[http://www.gnu.org/software/cpio](http://www.gnu.org/software/cpio) || [cpio](https://www.archlinux.org/packages/?name=cpio)

*   **[dar](https://en.wikipedia.org/wiki/Dar_(disk_archiver) "wikipedia:Dar (disk archiver)")** — An archiving and compression utility avoiding the drawbacks of tar

	[DAR - Disk ARchive](http://dar.linux.free.fr/) || [dar](https://aur.archlinux.org/packages/dar/)

*   **lha** — Archiver to create LH-7 format archives. 32-bit only (require multilib on x86_64).

	[http://www.infor.kanazawa-it.ac.jp/~ishii/lhaunix](http://www.infor.kanazawa-it.ac.jp/~ishii/lhaunix) || [lha](https://aur.archlinux.org/packages/lha/)

*   **lrzip** — Multi-threaded compressor using the rzip/lzma, lzo, and zpaq algorithms.

	[http://lrzip.kolivas.org/](http://lrzip.kolivas.org/) || [lrzip](https://www.archlinux.org/packages/?name=lrzip)

*   **lz4** — A file compressor using lz4 - An extremely fast compression algorithm.

	[https://github.com/lz4/lz4](https://github.com/lz4/lz4) || [lz4](https://www.archlinux.org/packages/?name=lz4)

*   **lzop** — Fast file compressor using lzo lib.

	[http://www.lzop.org/](http://www.lzop.org/) || [lzop](https://www.archlinux.org/packages/?name=lzop)

*   **[p7zip](/index.php/P7zip "P7zip")** — Port of 7-Zip for POSIX systems, including Linux. The commandline tool is called **7z**.

	[http://p7zip.sourceforge.net/](http://p7zip.sourceforge.net/) || [p7zip](https://www.archlinux.org/packages/?name=p7zip)

*   **pixz** — A multi-threaded and indexed compressor that avoiding the drawbacks of xz.

	[https://github.com/vasi/pixz](https://github.com/vasi/pixz) || [pixz](https://www.archlinux.org/packages/?name=pixz)

*   **[tar](/index.php/Tar "Tar")** — GNU utility for manipulating the ubiquitous tar archives (tarballs).

	[http://www.gnu.org/software/tar](http://www.gnu.org/software/tar) || [tar](https://www.archlinux.org/packages/?name=tar)

*   **[zpaq](https://en.wikipedia.org/wiki/ZPAQ "wikipedia:ZPAQ")** — A high compression ratio archiver written in C++. Powered by Context-Model, LZ77 and BWT algorithm.

	[http://mattmahoney.net/dc/zpaq.html](http://mattmahoney.net/dc/zpaq.html) || [zpaq](https://aur.archlinux.org/packages/zpaq/)

*   **zopfli** — High compress ratio file compressor from Google, using a deflate-compatible algorithm called zopfli.

	[https://github.com/google/zopfli](https://github.com/google/zopfli) || [zopfli-git](https://aur.archlinux.org/packages/zopfli-git/)

*   **[zoo](https://en.wikipedia.org/wiki/Zoo_(file_format) "wikipedia:Zoo (file format)")** — Rarely used archiver that was mostly used in VMS world before PKZIP became popular.

	[http://www.ibiblio.org/pub/Linux/utils/compress/zoo-2.10-3.src.rpm](http://www.ibiblio.org/pub/Linux/utils/compress/zoo-2.10-3.src.rpm) || [zoo](https://aur.archlinux.org/packages/zoo/)

##### Graphical

*   **[Ark](https://en.wikipedia.org/wiki/Ark_(software) "wikipedia:Ark (software)")** — Archiving tool included in the KDE desktop.

	[http://kde.org/applications/utilities/ark/](http://kde.org/applications/utilities/ark/) || [ark](https://www.archlinux.org/packages/?name=ark)

*   **Engrampa** — Archive manager for [MATE](/index.php/MATE "MATE")

	[https://github.com/mate-desktop/engrampa](https://github.com/mate-desktop/engrampa) || [engrampa](https://www.archlinux.org/packages/?name=engrampa)

*   **[File Roller](https://en.wikipedia.org/wiki/File_Roller "wikipedia:File Roller")** — Archive manager included in the GNOME desktop.

	[http://fileroller.sourceforge.net/](http://fileroller.sourceforge.net/) || [file-roller](https://www.archlinux.org/packages/?name=file-roller)

*   **FreeArc** — General-purpose archiver written in haskell, comes with a GTK2 gui. Currently only available on 32-bit platform. (Requires multilib on x86_64)

	[http://encode.ru/threads/43-FreeArc/](http://encode.ru/threads/43-FreeArc/) || [freearc](https://aur.archlinux.org/packages/freearc/)

*   **[PeaZip](https://en.wikipedia.org/wiki/PeaZip "wikipedia:PeaZip")** — Open source file and archive manager.

	[http://www.peazip.org/peazip-linux.html](http://www.peazip.org/peazip-linux.html) || [peazip-gtk2](https://aur.archlinux.org/packages/peazip-gtk2/) [peazip-qt](https://aur.archlinux.org/packages/peazip-qt/)

*   **Squeeze** — Featherweight front-end for commandline archiving tools.

	[http://squeeze.xfce.org/](http://squeeze.xfce.org/) || [squeeze-git](https://aur.archlinux.org/packages/squeeze-git/)

*   **[Xarchiver](https://en.wikipedia.org/wiki/Xarchiver "wikipedia:Xarchiver")** — Lightweight desktop independent archive manager built with GTK+.

	[https://github.com/ib/xarchiver](https://github.com/ib/xarchiver) || [xarchiver](https://www.archlinux.org/packages/?name=xarchiver)

#### Comparison, diff, merge

See also [Wikipedia:Comparison of file comparison tools](https://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools "wikipedia:Comparison of file comparison tools").

For managing *pacnew*/*pacsave* files, specialised tools exist. See [Pacnew and Pacsave files#Managing .pacnew files](/index.php/Pacnew_and_Pacsave_files#Managing_.pacnew_files "Pacnew and Pacsave files").

*   **colordiff** — A Perl script wrapper for 'diff' that produces the same output but with pretty 'syntax' highlighting.

	[http://www.colordiff.org/](http://www.colordiff.org/) || [colordiff](https://www.archlinux.org/packages/?name=colordiff)

*   **Diffuse** — Small and simple text merge tool written in Python.

	[http://diffuse.sourceforge.net/](http://diffuse.sourceforge.net/) || [diffuse](https://www.archlinux.org/packages/?name=diffuse)

*   **KDiff3** — File and directory diff and merge tool for the KDE desktop.

	[http://kdiff3.sourceforge.net/](http://kdiff3.sourceforge.net/) || [kdiff3](https://www.archlinux.org/packages/?name=kdiff3)

*   **[Kompare](https://en.wikipedia.org/wiki/Kompare "wikipedia:Kompare")** — GUI front-end program for viewing and merging differences between source files. It supports a variety of diff formats and provides many options to customize the information level displayed.

	[http://www.caffeinated.me.uk/kompare/](http://www.caffeinated.me.uk/kompare/) || [kompare](https://www.archlinux.org/packages/?name=kompare)

*   **[Meld](https://en.wikipedia.org/wiki/Meld_(software) "wikipedia:Meld (software)")** — Visual diff and merge tool that can compare files, directories, and version controlled projects.

	[http://meldmerge.org/](http://meldmerge.org/) || [meld](https://www.archlinux.org/packages/?name=meld)

*   **xxdiff** — A graphical browser for file and directory differences.

	[http://furius.ca/xxdiff/](http://furius.ca/xxdiff/) || [xxdiff](https://aur.archlinux.org/packages/xxdiff/)

[Vim](/index.php/Vim "Vim") and [Emacs](/index.php/Emacs "Emacs") provide merge functionality with [vimdiff](/index.php/Vim#Merging_files "Vim") and `ediff`.

#### Batch renamers

*   **[GPRename](https://en.wikipedia.org/wiki/GPRename "wikipedia:GPRename")** — GTK+ batch renamer for files and directories.

	[http://gprename.sourceforge.net](http://gprename.sourceforge.net) || [gprename](https://www.archlinux.org/packages/?name=gprename)

*   **[KRename](https://en.wikipedia.org/wiki/KRename "wikipedia:KRename")** — Very powerful batch file renamer for the KDE desktop.

	[http://www.krename.net](http://www.krename.net) || [krename](https://www.archlinux.org/packages/?name=krename)

*   **metamorphose2** — wxPython based batch renamer with support for regular expressions, renaming multimedia files according to their metadata, etc.

	[http://file-folder-ren.sourceforge.net](http://file-folder-ren.sourceforge.net) || [metamorphose2](https://aur.archlinux.org/packages/metamorphose2/)

*   **pyRenamer** — Application for the mass renaming of files.

	[https://github.com/SteveRyherd/pyRenamer](https://github.com/SteveRyherd/pyRenamer) || [pyrenamer](https://aur.archlinux.org/packages/pyrenamer/)

*   **rename.pl** — Batch renamer based on perl regex.

	[http://search.cpan.org/~pederst/rename/bin/rename.PL](http://search.cpan.org/~pederst/rename/bin/rename.PL) || [perl-rename](https://www.archlinux.org/packages/?name=perl-rename)

#### Search and replace

*   **KfileReplace** — GUI for batch processing search and replace operations.

	[https://www.kde.org/applications/utilities/kfilereplace/](https://www.kde.org/applications/utilities/kfilereplace/) || [kdewebdev-kfilereplace](https://www.archlinux.org/packages/?name=kdewebdev-kfilereplace)

### Disk cleaning

*   **rmlint** — Tool to quickly find (and optionally remove) duplicate files and other lint

	[https://rmlint.readthedocs.org/en/latest/](https://rmlint.readthedocs.org/en/latest/) || [rmlint](https://www.archlinux.org/packages/?name=rmlint)

*   **[BleachBit](https://en.wikipedia.org/wiki/BleachBit "wikipedia:BleachBit")** — It frees disk space and guards your privacy; frees cache, deletes cookies, clears Internet history, shreds temporary files, deletes logs, and discards junk you didn't know was there.

	[http://bleachbit.sourceforge.net/](http://bleachbit.sourceforge.net/) || [bleachbit](https://www.archlinux.org/packages/?name=bleachbit) [bleachbit-git](https://aur.archlinux.org/packages/bleachbit-git/)

*   **gconf-cleaner** — cleans up the unknown/invalid gconf keys that still sitting down on your gconf database

	[https://code.google.com/archive/p/gconf-cleaner/](https://code.google.com/archive/p/gconf-cleaner/) || [gconf-cleaner](https://aur.archlinux.org/packages/gconf-cleaner/)

### Disk usage display

*   **[Disk Usage Analyzer](https://en.wikipedia.org/wiki/Disk_Usage_Analyzer "wikipedia:Disk Usage Analyzer") (Baobab)** — Disk usage analyzer for the [GNOME](/index.php/GNOME "GNOME") desktop.

	[http://www.marzocca.net/linux/baobab](http://www.marzocca.net/linux/baobab) || [baobab](https://www.archlinux.org/packages/?name=baobab)

*   **[Filelight](https://en.wikipedia.org/wiki/Filelight "wikipedia:Filelight")** — Disk usage analyzer that creates an interactive map of concentric, segmented rings that help visualise disk usage on your computer.

	[http://methylblue.com/filelight/](http://methylblue.com/filelight/) || [filelight](https://www.archlinux.org/packages/?name=filelight)

*   **GdMap** — Disk usage analyzer that draws a map of rectangles sized according to file or dir sizes.

	[http://gdmap.sourceforge.net/](http://gdmap.sourceforge.net/) || [gdmap](https://www.archlinux.org/packages/?name=gdmap)

*   **gt5** — Diff-capable "du-browser".

	[http://gt5.sourceforge.net](http://gt5.sourceforge.net) || [gt5](https://aur.archlinux.org/packages/gt5/)

*   **ncdu** — Simple ncurses disk usage analyzer.

	[http://dev.yorhel.nl/ncdu](http://dev.yorhel.nl/ncdu) || [ncdu](https://www.archlinux.org/packages/?name=ncdu)

*   **duc** — A library and suite of tools for inspecting disk usage.

	[http://duc.zevv.nl/](http://duc.zevv.nl/) || [duc](https://aur.archlinux.org/packages/duc/)

### Clock synchronization

*   **[NTPd](/index.php/NTPd "NTPd")** — Network Time Protocol reference implementation.

	[http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project](http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project) || [ntp](https://www.archlinux.org/packages/?name=ntp)

*   **[Chrony](/index.php/Chrony "Chrony")** — Lightweight NTP client and server.

	[http://chrony.tuxfamily.org/](http://chrony.tuxfamily.org/) || [chrony](https://www.archlinux.org/packages/?name=chrony)

*   **[OpenNTPD](/index.php/OpenNTPD "OpenNTPD")** — Free, easy to use implementation of the Network Time Protocol.

	[http://www.openntpd.org/](http://www.openntpd.org/) || [openntpd](https://www.archlinux.org/packages/?name=openntpd)

*   **[systemd-timesyncd](/index.php/Systemd-timesyncd "Systemd-timesyncd")** — A daemon that has been added for synchronizing the system clock across the network.

	[https://www.freedesktop.org/wiki/Software/systemd/](https://www.freedesktop.org/wiki/Software/systemd/) || [systemd](https://www.archlinux.org/packages/?name=systemd)

### System maintenance

*   **cylon** — Updates, Maintenance, anti-malware, backup and system checks in a menu driven Bash script.

	[https://github.com/gavinlyonsrepo/cylon](https://github.com/gavinlyonsrepo/cylon) || [cylon](https://aur.archlinux.org/packages/cylon/)

### System monitoring

See also [Category:Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification").

*   **candybar** — WebKit-based status line for tiling window managers.

	[https://github.com/Lokaltog/candybar](https://github.com/Lokaltog/candybar) || [candybar-git](https://aur.archlinux.org/packages/candybar-git/)

*   **[Conky](/index.php/Conky "Conky")** — Lightweight, scriptable system monitor.

	[https://github.com/brndnmtthws/conky](https://github.com/brndnmtthws/conky) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **Collectd** — A simple, extensible system monitoring daemon based on [rrdtool](http://oss.oetiker.ch/rrdtool/). It has a small footprint and can be set up either stand-alone or as a server/client application.

	[https://collectd.org/](https://collectd.org/) || [collectd](https://www.archlinux.org/packages/?name=collectd)

*   **collectl** — Collectl is a light-weight performance monitoring tool capable of reporting interactively as well as logging to disk. It reports statistics on cpu, disk, infiniband, lustre, memory, network, nfs, process, quadrics, slabs and more in easy to read format.

	[http://collectl.sourceforge.net/](http://collectl.sourceforge.net/) || [collectl](https://aur.archlinux.org/packages/collectl/)

*   **dstat** — Versatile resource statistics tool.

	[http://dag.wieers.com/home-made/dstat/](http://dag.wieers.com/home-made/dstat/) || [dstat](https://www.archlinux.org/packages/?name=dstat)

*   **[GKrellM](https://en.wikipedia.org/wiki/GKrellM "wikipedia:GKrellM")** — Simple, flexible system monitor package for [GTK+](/index.php/GTK%2B "GTK+") with many plug-ins.

	[http://billw2.github.io/gkrellm/gkrellm.html](http://billw2.github.io/gkrellm/gkrellm.html) || [gkrellm](https://www.archlinux.org/packages/?name=gkrellm)

*   **glances** — CLI curses-based monitoring tool in Python.

	[http://nicolargo.github.io/glances](http://nicolargo.github.io/glances) || [glances](https://www.archlinux.org/packages/?name=glances)

*   **gnome-system-monitor** — A system monitor for [GNOME](/index.php/GNOME "GNOME").

	[https://help.gnome.org/users/gnome-system-monitor/](https://help.gnome.org/users/gnome-system-monitor/) || [gnome-system-monitor](https://www.archlinux.org/packages/?name=gnome-system-monitor) [gnome-system-monitor-gtk2](https://aur.archlinux.org/packages/gnome-system-monitor-gtk2/)

*   **[htop](https://en.wikipedia.org/wiki/Htop "wikipedia:Htop")** — Simple, ncurses interactive process viewer.

	[http://htop.sourceforge.net/](http://htop.sourceforge.net/) || [htop](https://www.archlinux.org/packages/?name=htop)

*   **[KSysGuard](https://en.wikipedia.org/wiki/KDE_System_Guard "wikipedia:KDE System Guard")** — Also known as KSysguard, is the [KDE](/index.php/KDE "KDE") task manager and performance monitor.

	[http://userbase.kde.org/KSysGuard](http://userbase.kde.org/KSysGuard) || [ksysguard](https://www.archlinux.org/packages/?name=ksysguard) or as part of [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **linux process explorer** — Graphical process explorer for Linux.

	[http://sourceforge.net/projects/procexp/](http://sourceforge.net/projects/procexp/) || [procexp](https://aur.archlinux.org/packages/procexp/)

*   **LXTask** — Lightweight task manager for [LXDE](/index.php/LXDE "LXDE").

	[http://wiki.lxde.org/en/LXTask](http://wiki.lxde.org/en/LXTask) || [lxtask](https://www.archlinux.org/packages/?name=lxtask)

*   **mate-system-monitor** — A GTK2 system monitor for [MATE](/index.php/MATE "MATE").

	[https://github.com/mate-desktop/mate-system-monitor](https://github.com/mate-desktop/mate-system-monitor) || [mate-system-monitor](https://www.archlinux.org/packages/?name=mate-system-monitor)

*   **netdata** — A web-based real-time performance monitor

	[https://github.com/firehol/netdata/wiki](https://github.com/firehol/netdata/wiki) || [netdata](https://www.archlinux.org/packages/?name=netdata)

*   **Task Manager** — GTK2 process mangement application for [Xfce](/index.php/Xfce "Xfce").

	[http://goodies.xfce.org/projects/applications/xfce4-taskmanager](http://goodies.xfce.org/projects/applications/xfce4-taskmanager) || [xfce4-taskmanager](https://www.archlinux.org/packages/?name=xfce4-taskmanager)

*   **[Paramano](/index.php/Paramano "Paramano")** — A light battery monitor and a CPU frequency scaler. Forked from [trayfreq](http://trayfreq.sourceforge.net/)

	[https://github.com/phillid/paramano](https://github.com/phillid/paramano) || [paramano](https://aur.archlinux.org/packages/paramano/)

*   **Sysstat** — A collection of resource monitoring tools: iostat, isag, mpstat, pidstat, sadf, sar.

	[http://pagesperso-orange.fr/sebastien.godard/](http://pagesperso-orange.fr/sebastien.godard/) || [sysstat](https://www.archlinux.org/packages/?name=sysstat)

*   **xosview** — A system monitor that resembles gr_osview from SGI IRIX

	[http://www.pogo.org.uk/~mark/xosview/](http://www.pogo.org.uk/~mark/xosview/) || [xosview](https://aur.archlinux.org/packages/xosview/)

### System information viewers

#### Console

*   **alsi** — A system information tool for Arch Linux. It can be configured for every other system without even touching the source code of the script.

	[http://trizenx.blogspot.ro/2012/08/alsi.html](http://trizenx.blogspot.ro/2012/08/alsi.html) || [alsi](https://aur.archlinux.org/packages/alsi/)

*   **archey2** — Simple python script that displays the arch logo and some basic information. Python 2.x version.

	[https://github.com/djmelik/archey](https://github.com/djmelik/archey) || [archey2](https://aur.archlinux.org/packages/archey2/)

*   **archey3** — Python script to display system infomation alongside the Arch Linux logo.

	[http://www.generictestdomain.net/archey3/](http://www.generictestdomain.net/archey3/) || [archey3](https://www.archlinux.org/packages/?name=archey3)

*   **dmidecode** — It reports information about your system's hardware as described in your system BIOS according to the SMBIOS/DMI standard.

	[http://www.nongnu.org/dmidecode/](http://www.nongnu.org/dmidecode/) || [dmidecode](https://www.archlinux.org/packages/?name=dmidecode)

*   **hwdetect** — Simple script to list modules that are exported by /sys, a part of [archboot](/index.php/Archboot "Archboot").

	[https://projects.archlinux.org/](https://projects.archlinux.org/) || [hwdetect](https://www.archlinux.org/packages/?name=hwdetect)

*   **hwinfo** — Powerful hardware detection tool come from openSUSE.

	[https://github.com/openSUSE/hwinfo](https://github.com/openSUSE/hwinfo) || [hwinfo](https://www.archlinux.org/packages/?name=hwinfo)

*   **inxi** — A script to get system information.

	[https://github.com/smxi/inxi](https://github.com/smxi/inxi) || [inxi](https://www.archlinux.org/packages/?name=inxi)

*   **neofetch** — A fast, highly customizable system info script that supports displaying images with w3m.

	[https://github.com/dylanaraps/neofetch](https://github.com/dylanaraps/neofetch) || [neofetch](https://aur.archlinux.org/packages/neofetch/), [neofetch-git](https://aur.archlinux.org/packages/neofetch-git/)

*   **screenfetch** — Similar to archey but has an option to take a screenshot. Written in bash.

	[https://github.com/KittyKatt/screenFetch](https://github.com/KittyKatt/screenFetch) || [screenfetch](https://www.archlinux.org/packages/?name=screenfetch)

#### Graphical

*   **CPU-G** — An application that shows useful information about your hardware, it looks like CPU-Z in Windows.

	[http://cpug.sourceforge.net/](http://cpug.sourceforge.net/) || [cpu-g](https://aur.archlinux.org/packages/cpu-g/)

*   **hardinfo** — A small application that displays information about your hardware and operating system, it looks like the Device Manager in Windows.

	[http://hardinfo.berlios.de/HomePage](http://hardinfo.berlios.de/HomePage) || [hardinfo](https://www.archlinux.org/packages/?name=hardinfo)

*   **i-Nex** — An application that gathers information for hardware components available on your system and displays it using an user interface similar to the popular Windows tool CPU-Z.

	[http://i-nex.linux.pl/](http://i-nex.linux.pl/) || [i-nex-git](https://aur.archlinux.org/packages/i-nex-git/)

*   **lshw** — A small tool to provide detailed information on the hardware configuration of the machine with CLI and GTK interfaces.

	[http://ezix.org/project/wiki/HardwareLiSter](http://ezix.org/project/wiki/HardwareLiSter) || [lshw](https://www.archlinux.org/packages/?name=lshw)

*   **KDE Info Center** — Shows hardware and software information.

	[https://www.kde.org/applications/system/kinfocenter/](https://www.kde.org/applications/system/kinfocenter/) || [kinfocenter](https://www.archlinux.org/packages/?name=kinfocenter)

#### Others

*   **tp-hdd-led** — Monitor HDD use with the Think-Led

	[http://timherbst.de/en/tp-hdd-led/](http://timherbst.de/en/tp-hdd-led/) || [tp-hdd-led](https://aur.archlinux.org/packages/tp-hdd-led/)

### Keyboard layout switchers

*   **fbxkb** — A NETWM compliant keyboard indicator and switcher. It shows a flag of current keyboard in a systray area and allows you to switch to another one.

	[http://fbxkb.sourceforge.net/](http://fbxkb.sourceforge.net/) || [fbxkb](https://aur.archlinux.org/packages/fbxkb/)

*   **xxkb** — A lightweight keyboard layout indicator and switcher.

	[http://sourceforge.net/projects/xxkb/](http://sourceforge.net/projects/xxkb/) || [xxkb](https://www.archlinux.org/packages/?name=xxkb)

*   **qxkb** — A keyboard switcher written in Qt.

	[https://github.com/disels/qxkb](https://github.com/disels/qxkb) || [qxkb](https://aur.archlinux.org/packages/qxkb/)

*   **[X Neural Switcher](https://en.wikipedia.org/wiki/X_Neural_Switcher "wikipedia:X Neural Switcher")** — A text analyser, it detects the language of the input and corrects the keyboard layout if needed.

	[http://www.xneur.ru/](http://www.xneur.ru/) || [xneur](https://aur.archlinux.org/packages/xneur/), [gxneur](https://aur.archlinux.org/packages/gxneur/) (GUI)

### Power management

See [Power management](/index.php/Power_management "Power management").

### Clipboard managers

See: [List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard").

### Wallpaper setters

*   **bgs** — An extremely fast and small background setter for X based on imlib2.

	[https://github.com/Gottox/bgs/](https://github.com/Gottox/bgs/) || [bgs-git](https://aur.archlinux.org/packages/bgs-git/)

*   **esetroot** — Eterm's root background setter, packaged separately

	[http://www.eterm.org/](http://www.eterm.org/) || [esetroot](https://aur.archlinux.org/packages/esetroot/)

*   **[Feh](/index.php/Feh "Feh")** — A lightweight and powerful image viewer that can also be used to manage the desktop wallpaper.

	[http://linuxbrit.co.uk/software/feh/](http://linuxbrit.co.uk/software/feh/) || [feh](https://www.archlinux.org/packages/?name=feh)‎

*   **habak** — A background changing app

	[http://fvwm-crystal.org/](http://fvwm-crystal.org/) || [habak](https://www.archlinux.org/packages/?name=habak)

*   **hsetroot** — A tool to create compose wallpapers.

	[https://packages.debian.org/sid/hsetroot](https://packages.debian.org/sid/hsetroot) || [hsetroot](https://aur.archlinux.org/packages/hsetroot/)

*   **[Nitrogen](/index.php/Nitrogen "Nitrogen")** — A fast and lightweight desktop background browser and setter for X windows.

	[http://projects.l3ib.org/nitrogen/](http://projects.l3ib.org/nitrogen/) || [nitrogen](https://www.archlinux.org/packages/?name=nitrogen)

*   **pybgsetter** — Multi-backend (hsetroot, Esetroot, habak, feh) to set desktop wallpaper

	http://bbs.archlinux.org/viewtopic.php?id=88997 || [pybgsetter](https://aur.archlinux.org/packages/pybgsetter/)

*   **wallpaperd** — A small application that takes care of setting the background image

	[https://projects.pekdon.net/projects/wallpaperd](https://projects.pekdon.net/projects/wallpaperd) || [wallpaperd](https://aur.archlinux.org/packages/wallpaperd/)

*   **xli** — An image display program for X

	[https://packages.debian.org/sid/xli](https://packages.debian.org/sid/xli) || [xli](https://aur.archlinux.org/packages/xli/)

**Tip:** In order to avoid installing one more package, you may find convenient to use the `display` utility from [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) or `gm display` from [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick). E.g.: `display -backdrop -background '#3f3f3f' -flatten -window root *image*`.

### Package management

See [pacman tips#Utilities](/index.php/Pacman_tips#Utilities "Pacman tips").

### Input method editor

See also [Wikipedia:Input method](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method").

*   **[Fcitx](/index.php/Fcitx "Fcitx")** — Flexible Context-aware Input Tool with eXtension.

	[http://fcitx-im.org](http://fcitx-im.org) || [fcitx](https://www.archlinux.org/packages/?name=fcitx)

*   **Hime** — A GTK2+/GTK3+ based universal input method platform.

	[http://hime-ime.github.io/](http://hime-ime.github.io/) || [hime-git](https://aur.archlinux.org/packages/hime-git/)

*   **[IBus](/index.php/IBus "IBus")** — Next Generation Input Bus for Linux.

	[http://ibus.googlecode.com](http://ibus.googlecode.com) || [ibus](https://www.archlinux.org/packages/?name=ibus)

*   **[Rime IME](/index.php/Rime_IME "Rime IME")** — Rime input method engine.

	[http://rime.im/](http://rime.im/) || [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime) or [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime)

*   **[UIM](/index.php/UIM "UIM")** — Multilingual input method library.

	[https://github.com/uim/uim](https://github.com/uim/uim) || [uim](https://www.archlinux.org/packages/?name=uim)

### Finders

See also [Wikipedia:List of search engines#Desktop search engines](https://en.wikipedia.org/wiki/List_of_search_engines#Desktop_search_engines "wikipedia:List of search engines").

*   **fuzzy-find** — Fuzzy completion for finding files.

	[https://github.com/silentbicycle/ff](https://github.com/silentbicycle/ff) || [ff-git](https://aur.archlinux.org/packages/ff-git/)

*   **fzf** — General-purpose command-line fuzzy finder.

	[https://github.com/junegunn/fzf](https://github.com/junegunn/fzf) || [fzf](https://www.archlinux.org/packages/?name=fzf) [fzf-git](https://aur.archlinux.org/packages/fzf-git/)

*   **Baloo** — KDE's file indexing and search solution

	[https://community.kde.org/Baloo](https://community.kde.org/Baloo) || [baloo](https://www.archlinux.org/packages/?name=baloo)

*   **Catfish** — Versatile file searching tool

	[https://launchpad.net/catfish-search](https://launchpad.net/catfish-search) || [catfish](https://www.archlinux.org/packages/?name=catfish)

*   **Docfetcher** — A java open source desktop search application

	[http://docfetcher.sourceforge.net](http://docfetcher.sourceforge.net) || [docfetcher](https://aur.archlinux.org/packages/docfetcher/)

*   **Gnome Search Tool** — Default Gnome utility to search for files

	[http://gnome.org](http://gnome.org) || [gnome-search-tool](https://www.archlinux.org/packages/?name=gnome-search-tool)

*   **Gnome Search Tool No Nautilus** — *gnome-search-tool* to search for files without [GNOME Files](/index.php/GNOME_Files "GNOME Files") or *gnome-desktop*

	|| [gnome-search-tool-no-nautilus](https://aur.archlinux.org/packages/gnome-search-tool-no-nautilus/)

*   **Recoll** — Full text search tool based on Xapian backend

	[http://www.lesbonscomptes.com/recoll/](http://www.lesbonscomptes.com/recoll/) || [recoll](https://www.archlinux.org/packages/?name=recoll)

*   **Searchmonkey** — A powerful GUI search utility for matching regex patterns

	[http://searchmonkey.sourceforge.net/](http://searchmonkey.sourceforge.net/) || [searchmonkey](https://aur.archlinux.org/packages/searchmonkey/)

*   **[Tracker](https://en.wikipedia.org/wiki/Tracker_(search_software) "wikipedia:Tracker (search software)")** — All-in-one indexer, search tool and metadata database.

	[https://wiki.gnome.org/Projects/Tracker](https://wiki.gnome.org/Projects/Tracker) || [tracker](https://www.archlinux.org/packages/?name=tracker)