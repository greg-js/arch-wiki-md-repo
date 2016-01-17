# List of applications/Utilities

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**[List of applications](/index.php/List_of_applications "List of applications")**

* * *

[Internet](/index.php/List_of_applications/Internet "List of applications/Internet") – [Multimedia](/index.php/List_of_applications/Multimedia "List of applications/Multimedia") – **Utilities** – [Documents](/index.php/List_of_applications/Documents "List of applications/Documents") – [Security](/index.php/List_of_applications/Security "List of applications/Security") – [Science](/index.php/List_of_applications/Science "List of applications/Science") – [Other](/index.php/List_of_applications/Other "List of applications/Other")

## Contents

*   [1 Utilities](#Utilities)
    *   [1.1 Partitioning tools](#Partitioning_tools)
    *   [1.2 Mount tools](#Mount_tools)
        *   [1.2.1 Udisks](#Udisks)
    *   [1.3 Basic shell commands](#Basic_shell_commands)
    *   [1.4 Integrated development environments](#Integrated_development_environments)
    *   [1.5 Terminal emulators](#Terminal_emulators)
        *   [1.5.1 VTE-based](#VTE-based)
        *   [1.5.2 KMS-based](#KMS-based)
        *   [1.5.3 framebuffer-based](#framebuffer-based)
    *   [1.6 Files](#Files)
        *   [1.6.1 File managers](#File_managers)
            *   [1.6.1.1 Console](#Console)
            *   [1.6.1.2 Graphical](#Graphical)
        *   [1.6.2 Desktop search engines](#Desktop_search_engines)
        *   [1.6.3 Archiving and compression tools](#Archiving_and_compression_tools)
            *   [1.6.3.1 Console](#Console_2)
            *   [1.6.3.2 Graphical](#Graphical_2)
        *   [1.6.4 Comparison, diff, merge](#Comparison.2C_diff.2C_merge)
        *   [1.6.5 Batch renamers](#Batch_renamers)
    *   [1.7 Disk cleaning](#Disk_cleaning)
    *   [1.8 Disk usage display](#Disk_usage_display)
    *   [1.9 Clock synchronization](#Clock_synchronization)
    *   [1.10 System monitoring](#System_monitoring)
    *   [1.11 System information viewers](#System_information_viewers)
        *   [1.11.1 Console](#Console_3)
        *   [1.11.2 Graphical](#Graphical_3)
        *   [1.11.3 Others](#Others)
    *   [1.12 Keyboard layout switchers](#Keyboard_layout_switchers)
    *   [1.13 Power management](#Power_management)
    *   [1.14 Clipboard managers](#Clipboard_managers)
    *   [1.15 Wallpaper setters](#Wallpaper_setters)
    *   [1.16 Package management](#Package_management)
    *   [1.17 Input method editor](#Input_method_editor)
    *   [1.18 Trash management](#Trash_management)
    *   [1.19 File synchronization](#File_synchronization)
    *   [1.20 Finders](#Finders)

## Utilities

### Partitioning tools

See [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").

### Mount tools

*   **9mount** — Mount 9p filesystems.

[http://sqweek.net/code/9mount/](http://sqweek.net/code/9mount/) || [9mount](https://aur.archlinux.org/packages/9mount/)<sup><small>AUR</small></sup>

*   **cryptmount** — Mount an encrypted file system as a regular user.

[http://cryptmount.sourceforge.net/](http://cryptmount.sourceforge.net/) || [cryptmount](https://aur.archlinux.org/packages/cryptmount/)<sup><small>AUR</small></sup>

*   **ldm** — A lightweight daemon that mounts drives automagically using _udev_

[https://github.com/LemonBoy/ldm](https://github.com/LemonBoy/ldm) || [ldm](https://aur.archlinux.org/packages/ldm/)<sup><small>AUR</small></sup>

*   **pmount** — Mount _source_ as a regular user to an automatically created destination `/media/_source_name_`.

[http://pmount.alioth.debian.org/](http://pmount.alioth.debian.org/) || [pmount](https://aur.archlinux.org/packages/pmount/)<sup><small>AUR</small></sup>

*   **pmount-safe-removal** — Mount removable devices as regular user with safe removal

[http://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device](http://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device) || [pmount-safe-removal](https://aur.archlinux.org/packages/pmount-safe-removal/)<sup><small>AUR</small></sup>

*   **udevil** — Mounts removable devices as a regular user, show device info, and monitor device changes. Only depends on _udev_ and glib.

[http://ignorantguru.github.io/udevil](http://ignorantguru.github.io/udevil) || [udevil](https://www.archlinux.org/packages/?name=udevil)

*   **ws** — Mount Windows network shares ([CIFS](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") and [VFS](https://en.wikipedia.org/wiki/Virtual_file_system "wikipedia:Virtual file system")).

[http://winshares.sourceforge.net/](http://winshares.sourceforge.net/) || [ws](https://aur.archlinux.org/packages/ws/)<sup><small>AUR</small></sup>

#### Udisks

*   **bashmount** — A bash script to mount and manage removable media as a regular user with udisks.

[https://github.com/jamielinux/bashmount](https://github.com/jamielinux/bashmount) || [bashmount](https://aur.archlinux.org/packages/bashmount/)<sup><small>AUR</small></sup>

*   **udiskie** — Automatic disk mounting service using _udisks_

[https://pypi.python.org/pypi/udiskie](https://pypi.python.org/pypi/udiskie) || [udiskie](https://www.archlinux.org/packages/?name=udiskie)

*   **udisks_functions** — Bash functions and aliases for _udisks2_

[https://bbs.archlinux.org/viewtopic.php?id=109307](https://bbs.archlinux.org/viewtopic.php?id=109307) || [udisks_functions](https://aur.archlinux.org/packages/udisks_functions/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/udisks_functions)]</sup>

*   **udisksvm** — GUI _udisks_ wrapper for removable media

[https://bbs.archlinux.org/viewtopic.php?id=112397](https://bbs.archlinux.org/viewtopic.php?id=112397) || [udisksvm](https://aur.archlinux.org/packages/udisksvm/)<sup><small>AUR</small></sup>

### Basic shell commands

*   **[Core utilities](/index.php/Core_utilities "Core utilities")** — The basic file, shell and text manipulation utilities of the GNU operating system

[http://www.gnu.org/software/coreutils](http://www.gnu.org/software/coreutils) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

### Integrated development environments

See also [Wikipedia:Comparison of integrated development environments](https://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments "wikipedia:Comparison of integrated development environments").

*   **[Anjuta](/index.php/Anjuta "Anjuta")** — Versatile IDE with project management, an application wizard, an interactive debugger, a source editor, version control support and many more tools.

[http://www.anjuta.org/](http://www.anjuta.org/) || [anjuta](https://www.archlinux.org/packages/?name=anjuta)

*   **[Aptana Studio](https://en.wikipedia.org/wiki/Aptana#Aptana_Studio "wikipedia:Aptana")** — IDE based on Eclipse, but geared towards web development, with support for HTML, CSS, Javascript, Ruby on Rails, PHP, Adobe AIR and others.

[http://www.aptana.org/](http://www.aptana.org/) || [aptana-studio](https://aur.archlinux.org/packages/aptana-studio/)<sup><small>AUR</small></sup>

*   **[Bluefish](https://en.wikipedia.org/wiki/Bluefish_(text_editor) "wikipedia:Bluefish (text editor)")** — GTK+ editor/IDE with an MDI interface, syntax highlighting and support for Python plugins.

[http://bluefish.openoffice.nl/](http://bluefish.openoffice.nl/) || [bluefish](https://www.archlinux.org/packages/?name=bluefish)

*   **[BlueGriffon](https://en.wikipedia.org/wiki/BlueGriffon "wikipedia:BlueGriffon")** — A WYSIWYG content editor for the World Wide Web. Powered by Gecko, the rendering engine of [Firefox](/index.php/Firefox "Firefox"), it can edit Web pages in conformance to Web Standards. It runs on Mac OS X, Windows and Linux.

[http://bluegriffon.org/](http://bluegriffon.org/) || [bluegriffon](https://www.archlinux.org/packages/?name=bluegriffon)

*   **[Bluej](https://en.wikipedia.org/wiki/Bluej "wikipedia:Bluej")** — Fully featured Java IDE used mainly for educational and beginner purposes.

[http://bluej.org/](http://bluej.org/) || [bluej](https://aur.archlinux.org/packages/bluej/)<sup><small>AUR</small></sup>

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "wikipedia:Brackets (text editor)")** — A free open-source editor written in HTML, CSS, and Javascript with a primary focus on Web Development. It was created by Adobe Systems, licensed under the MIT License, and is currently maintained on GitHub.

[http://brackets.io/](http://brackets.io/) || [brackets](https://aur.archlinux.org/packages/brackets/)<sup><small>AUR</small></sup>

*   **[Code::Blocks](https://en.wikipedia.org/wiki/Code::Blocks "wikipedia:Code::Blocks")** — Open source and cross-platform C/C++ IDE.

[http://www.codeblocks.org/](http://www.codeblocks.org/) || [codeblocks](https://www.archlinux.org/packages/?name=codeblocks)

*   **[Cloud9](https://en.wikipedia.org/wiki/Cloud9_IDE "wikipedia:Cloud9 IDE")** — State-of-the-art IDE that runs in your browser and lives in the cloud, allowing you to run, debug and deploy applications from anywhere, anytime.

[https://c9.io/](https://c9.io/) || [cloud9](https://aur.archlinux.org/packages/cloud9/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cloud9)]</sup>

*   **[Eclipse](/index.php/Eclipse "Eclipse")** — Open source community project, which aims to provide a universal development platform.

[http://eclipse.org/](http://eclipse.org/) || [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java), [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp), [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php)

*   **[Editra](https://en.wikipedia.org/wiki/Editra "wikipedia:Editra")** — Multi-platform text editor with an implementation that focuses on creating an easy to use interface and features that aid in code development.

[http://www.editra.org](http://www.editra.org) || [editra-svn](https://aur.archlinux.org/packages/editra-svn/)<sup><small>AUR</small></sup>

*   **[Eric](https://en.wikipedia.org/wiki/Eric_Python_IDE "wikipedia:Eric Python IDE")** — Full-featured Python 3.x and Ruby IDE in PyQt4.

[http://eric-ide.python-projects.org/](http://eric-ide.python-projects.org/) || [eric](https://www.archlinux.org/packages/?name=eric) [eric4](https://aur.archlinux.org/packages/eric4/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/eric4)]</sup>

*   **[Gambas](/index.php/Gambas "Gambas")** — Free development environment based on a Basic interpreter with object extensions.

[http://gambas.sourceforge.net/en/main.html](http://gambas.sourceforge.net/en/main.html) || [gambas3-ide](https://www.archlinux.org/packages/?name=gambas3-ide)

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — Text editor using the GTK+ toolkit with basic features of an integrated development environment.

[https://geany.org](https://geany.org) || [geany](https://www.archlinux.org/packages/?name=geany)

*   **IEP** — Cross-platform Python IDE focused on interactivity and introspection, which makes it very suitable for scientific computing.

[http://iep-project.org/](http://iep-project.org/) || [iep](https://aur.archlinux.org/packages/iep/)<sup><small>AUR</small></sup>

*   **[IntelliJ IDEA](https://en.wikipedia.org/wiki/IntelliJ_IDEA "wikipedia:IntelliJ IDEA")** — IDE for Java, Groovy and other programming languages with advanced refactoring features.

[http://www.jetbrains.com/idea/](http://www.jetbrains.com/idea/) || [intellij-idea-community-edition](https://www.archlinux.org/packages/?name=intellij-idea-community-edition)

*   **[KDevelop](https://en.wikipedia.org/wiki/KDevelop "wikipedia:KDevelop")** — Feature-full, plugin extensible IDE for C/C++ and other programming languages.

[http://kdevelop.org/](http://kdevelop.org/) || [kdevelop](https://www.archlinux.org/packages/?name=kdevelop)

*   **[Komodo Edit](https://en.wikipedia.org/wiki/Komodo_Edit "wikipedia:Komodo Edit")** — A free, multi-language editor.

[http://www.activestate.com/komodo-edit](http://www.activestate.com/komodo-edit) || [komodo-edit](https://aur.archlinux.org/packages/komodo-edit/)<sup><small>AUR</small></sup>

*   **[Lazarus](https://en.wikipedia.org/wiki/Lazarus_(IDE) "wikipedia:Lazarus (IDE)")** — Cross-platform IDE for Object Pascal.

[http://lazarus.freepascal.org/](http://lazarus.freepascal.org/) || [lazarus](https://www.archlinux.org/packages/?name=lazarus)

*   **LiteIDE** — A simple, open source, cross-platform Go IDE.

[https://github.com/visualfc/liteide](https://github.com/visualfc/liteide) || [liteide](https://www.archlinux.org/packages/?name=liteide)

*   **MonkeyStudio** — Monkey Studio (MkS) is a cross platform IDE written in C++/Qt 4\. Syntax highlighting for more than 22 programming languages.

[http://monkeystudio.org/](http://monkeystudio.org/) || [monkeystudio](https://aur.archlinux.org/packages/monkeystudio/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/monkeystudio)]</sup>

*   **[MonoDevelop](https://en.wikipedia.org/wiki/MonoDevelop "wikipedia:MonoDevelop")** — Cross-platform IDE targeted for the Mono and .NET frameworks.

[http://monodevelop.com/](http://monodevelop.com/) || [monodevelop](https://www.archlinux.org/packages/?name=monodevelop)

*   **MPLAB** — IDE for Microchip PIC and dsPIC development

[http://www.microchip.com/mplabx](http://www.microchip.com/mplabx) || [microchip-mplabx-bin](https://aur.archlinux.org/packages/microchip-mplabx-bin/)<sup><small>AUR</small></sup>

*   **[NetBeans](/index.php/Netbeans "Netbeans")** — Integrated development environment (IDE) for developing with Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, and other languages.

[http://netbeans.org/](http://netbeans.org/) || [netbeans](https://www.archlinux.org/packages/?name=netbeans)

*   **[Ninja-IDE](https://en.wikipedia.org/wiki/Ninja-IDE "wikipedia:Ninja-IDE")** — from the recursive acronym: "Ninja-IDE Is Not Just Another IDE", is a cross-platform integrated development environment (IDE); runs on Linux/X11, Mac OS X and Windows OSs. Used, for example, for Python development

[http://ninja-ide.org/](http://ninja-ide.org/) || [ninja-ide](https://www.archlinux.org/packages/?name=ninja-ide)

*   **[PHPStorm](/index.php/PHPStorm "PHPStorm")** — JetBrains PhpStorm is a commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform, providing an editor for PHP, HTML and JavaScript with on-the-fly code analysis, error prevention and automated refactorings for PHP and JavaScript code.

[https://www.jetbrains.com/phpstorm/](https://www.jetbrains.com/phpstorm/) || [phpstorm](https://aur.archlinux.org/packages/phpstorm/)<sup><small>AUR</small></sup> [phpstorm-eap](https://aur.archlinux.org/packages/phpstorm-eap/)<sup><small>AUR</small></sup>

*   **[PyCharm](https://en.wikipedia.org/wiki/PyCharm "wikipedia:PyCharm")** — IDE used for programming in Python with support for code analysis, debugging, unit testing, version control and web development with Django.

[http://www.jetbrains.com/pycharm/](http://www.jetbrains.com/pycharm/) || [pycharm-community](https://aur.archlinux.org/packages/pycharm-community/)<sup><small>AUR</small></sup>

*   **[QDevelop](https://en.wikipedia.org/wiki/QDevelop "wikipedia:QDevelop")** — Free and cross-platform IDE for Qt.

[http://biord-software.org/qdevelop/](http://biord-software.org/qdevelop/) || [qdevelop-svn](https://aur.archlinux.org/packages/qdevelop-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qdevelop-svn)]</sup>

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — Lightweight, cross-platform C++ integrated development environment with a focus on Qt.

[http://qt-project.org/downloads#qt-creator](http://qt-project.org/downloads#qt-creator) || [qtcreator](https://www.archlinux.org/packages/?name=qtcreator)

*   **[Scratch](https://en.wikipedia.org/wiki/Scratch "wikipedia:Scratch")** — A multimedia authoring tool for educational and entertainment purposes, such as creating interactive projects and simple sprite-based games. It is used primarly by unskilled users (such as children) as an entry to [event-driven programming](https://en.wikipedia.org/wiki/Event-driven_programming "wikipedia:Event-driven programming"). _Scratch_ is free software under GPL v2 and [Scratch Source Code License](http://wiki.scratch.mit.edu/wiki/Scratch_Source_Code_License).

[http://scratch.mit.edu](http://scratch.mit.edu) || [scratch](https://www.archlinux.org/packages/?name=scratch) [scratch2](https://aur.archlinux.org/packages/scratch2/)<sup><small>AUR</small></sup>

*   **Spyder** — Scientific PYthon Development EnviRonment providing MATLAB-like features.

[http://code.google.com/p/spyderlib/](http://code.google.com/p/spyderlib/) || [spyder](https://www.archlinux.org/packages/?name=spyder)

### Terminal emulators

See also [Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators").

Power users use terminal emulators quite often, so unsurprisingly lots of X11 terminal emulators exist. Most of them emulate Xterm that emulates VT102, which emulates typewriter, so you will have to read the [Wikipedia article](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") and [other sources](https://google.com/search?q=linux+terminal+emulators) to get a hold on these things.

*   **[aterm](https://en.wikipedia.org/wiki/aterm "wikipedia:aterm")** — Xterm replacement with transparency support. It has been deprecated in favour of urxvt since 2008.

[http://aterm.sourceforge.net/](http://aterm.sourceforge.net/) || [aterm](https://aur.archlinux.org/packages/aterm/)<sup><small>AUR</small></sup>

*   **Eterm** — Terminal emulator intended as a replacement for xterm and designed for the [Enlightenment](/index.php/Enlightenment "Enlightenment") desktop.

[http://eterm.org](http://eterm.org) || [eterm](https://aur.archlinux.org/packages/eterm/)<sup><small>AUR</small></sup>

*   **Final Term** — A new breed of terminal emulator. Project is dead.

[http://finalterm.org/](http://finalterm.org/) || [finalterm-git](https://aur.archlinux.org/packages/finalterm-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/finalterm-git)]</sup>

*   **Gate One** — Web-based terminal emulator and SSH client.

[https://github.com/liftoff/GateOne](https://github.com/liftoff/GateOne) || [gateone-git](https://aur.archlinux.org/packages/gateone-git/)<sup><small>AUR</small></sup>

*   **[Konsole](https://en.wikipedia.org/wiki/Konsole "wikipedia:Konsole")** — Terminal emulator included in the [KDE](/index.php/KDE "KDE") desktop.

[http://kde.org/applications/system/konsole/](http://kde.org/applications/system/konsole/) || [konsole](https://www.archlinux.org/packages/?name=konsole)

*   **mlterm** — A multi-lingual terminal emulator supporting various character sets and encodings in the world.

[http://sourceforge.net/projects/mlterm/](http://sourceforge.net/projects/mlterm/) || [mlterm](https://aur.archlinux.org/packages/mlterm/)<sup><small>AUR</small></sup>

*   **[Mrxvt](https://en.wikipedia.org/wiki/mrxvt "wikipedia:mrxvt")** — Tabbed X terminal emulator based on rxvt.

[http://materm.sourceforge.net/wiki/pmwiki.php](http://materm.sourceforge.net/wiki/pmwiki.php) || [mrxvt](https://aur.archlinux.org/packages/mrxvt/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mrxvt)]</sup>

*   **QTerminal** — A lightweight Qt-based terminal emulator.

[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal-git](https://aur.archlinux.org/packages/qterminal-git/)<sup><small>AUR</small></sup>

*   **[rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt")** — Popular replacement for the xterm.

[http://rxvt.sourceforge.net/](http://rxvt.sourceforge.net/) || [rxvt](https://www.archlinux.org/packages/?name=rxvt)

*   **[st](/index.php/St "St")** — Simple terminal implementation for X.

[http://st.suckless.org](http://st.suckless.org) || [st](https://www.archlinux.org/packages/?name=st)

*   **Terminal** — A terminal emulator, that supports multiple windows, scroll buffer and all the expected features. A part of GNUstep.

[http://gap.nongnu.org/terminal/index.html](http://gap.nongnu.org/terminal/index.html) || [gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gnustep-terminal)]</sup>

*   **[terminator](/index.php/Terminator "Terminator")** — Terminal emulator supporting multiple resizable terminal panels.

[http://gnometerminator.blogspot.it/](http://gnometerminator.blogspot.it/) || [terminator](https://www.archlinux.org/packages/?name=terminator)

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

[http://calno.com/evilvte/](http://calno.com/evilvte/) || [evilvte](https://aur.archlinux.org/packages/evilvte/)<sup><small>AUR</small></sup>

*   **Germinal** — Minimalist terminal emulator which provides a borderless maximized terminal, attached to a tmux session by default, hence providing tabs and panels.

[http://www.imagination-land.org/tags/germinal.html](http://www.imagination-land.org/tags/germinal.html) || [germinal](https://aur.archlinux.org/packages/germinal/)<sup><small>AUR</small></sup>

*   **[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")** — A terminal emulator included in the [GNOME](/index.php/GNOME "GNOME") desktop with support for Unicode and pseudo-transparency.

[https://wiki.gnome.org/Apps/Terminal](https://wiki.gnome.org/Apps/Terminal) || [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)

*   **[Guake](/index.php/Guake "Guake")** — Drop-down terminal for the GNOME desktop.

[http://guake-project.org/](http://guake-project.org/) || [guake](https://www.archlinux.org/packages/?name=guake)

*   **Terra** — is a GTK+3.0 based terminal emulator with useful user interface, it also supports multiple terminals with splitting screen horizontally or vertically -- (similar to guake).

[https://github.com/ozcanesen/terra-terminal](https://github.com/ozcanesen/terra-terminal) || [terra](https://aur.archlinux.org/packages/terra/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/terra)]</sup>

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

*   **Stjerm** — GTK+-based drop-down terminal emulator that provides a minimalistic interface combined with a small file size, lightweight memory usage and easy integration with composite window managers such as Compiz.

[https://code.google.com/p/stjerm-terminal-emulator/](https://code.google.com/p/stjerm-terminal-emulator/) || [stjerm-git](https://aur.archlinux.org/packages/stjerm-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/stjerm-git)]</sup>

*   **[Terminal](https://en.wikipedia.org/wiki/Terminal_(Xfce) "wikipedia:Terminal (Xfce)")** — Terminal emulator included in the [Xfce](/index.php/Xfce "Xfce") desktop with support for a colorized prompt and a tabbed interface.

[http://docs.xfce.org/apps/terminal/start](http://docs.xfce.org/apps/terminal/start) || [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)

*   **Termit** — Simple terminal emulator based on the vte library that includes tabs, bookmarks, and the ability to switch encodings.

[https://wiki.github.com/nonstop/termit/](https://wiki.github.com/nonstop/termit/) || [termit](https://aur.archlinux.org/packages/termit/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/termit)]</sup>

*   **[Termite](/index.php/Termite "Termite")** — A keyboard-centric VTE-based terminal, aimed at use within a window manager with tiling and/or tabbing support.

[https://github.com/thestinger/termite](https://github.com/thestinger/termite) || [termite](https://www.archlinux.org/packages/?name=termite)

*   **tinyterm** — Very lightweight terminal emulator based on VTE.

[https://github.com/lahwaacz/tinyterm](https://github.com/lahwaacz/tinyterm) || [tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/)<sup><small>AUR</small></sup>

#### KMS-based

The following terminal emulators are based on the [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") that could be invoked without X.

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — A KMS/DRM-based system console(getty) with an integrated terminal emulator for Linux operating systems.

[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

#### framebuffer-based

In GNU/Linux world, the [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") could be refered to a virtual device in the Linux kernel (**fbdev**) or the virtual framebuffer system for X (**xvfb**). This section mainly lists the terminal emulators that based on the in-kernel virtual device, i.e. **fbdev**.

*   **[fbterm](/index.php/Fbterm "Fbterm")** — A fast framebuffer-based terminal emulator with many amazing features. Development stopped.

[http://code.google.com/p/fbterm/](http://code.google.com/p/fbterm/) || [fbterm](https://www.archlinux.org/packages/?name=fbterm)

*   **yaft** — A simple terminal emulator for living without X, with UCS2 glyphs, wallpaper and 256color support.

[https://github.com/uobikiemukot/yaft](https://github.com/uobikiemukot/yaft) || [yaft](https://aur.archlinux.org/packages/yaft/)<sup><small>AUR</small></sup>

### Files

#### File managers

See also [Wikipedia:Comparison of file managers](https://en.wikipedia.org/wiki/Comparison_of_file_managers "wikipedia:Comparison of file managers").

##### Console

*   **Clex** — File manager with full-screen user interface

[http://www.clex.sk/](http://www.clex.sk/) || [clex](https://aur.archlinux.org/packages/clex/)<sup><small>AUR</small></sup>

*   **[Dired](https://en.wikipedia.org/wiki/Dired "wikipedia:Dired")** — Directory editor integrated with [Emacs](/index.php/Emacs "Emacs").

[http://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html](http://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **dired** — Ancient DIRectory EDitor since 1980.

[http://fossies.org/linux/misc/old/](http://fossies.org/linux/misc/old/) || [dired](https://aur.archlinux.org/packages/dired/)<sup><small>AUR</small></sup>

*   **[Midnight Commander](/index.php/Midnight_Commander "Midnight Commander")** — Console-based, dual-paneled file manager.

[http://www.midnight-commander.org](http://www.midnight-commander.org) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **nffm** — "Nothing Fancy File Manager", a mouseless ncurses file manager written in C.

[https://github.com/mariostg/nffm](https://github.com/mariostg/nffm) || [nffm-git](https://aur.archlinux.org/packages/nffm-git/)<sup><small>AUR</small></sup>

*   **Pilot** — File manager that comes with the [Alpine](/index.php/Alpine "Alpine") email client.

[http://patches.freeiz.com/alpine/](http://patches.freeiz.com/alpine/) || [alpine](https://aur.archlinux.org/packages/alpine/)<sup><small>AUR</small></sup>

*   **[Ranger](/index.php/Ranger "Ranger")** — Console-based file manager with vi bindings, customizability, and lots of features.

[http://nongnu.org/ranger](http://nongnu.org/ranger) || [ranger](https://www.archlinux.org/packages/?name=ranger)

*   **[Vifm](/index.php/Vifm "Vifm")** — Ncurses-based two-panel file manager with vi-like keybindings.

[http://vifm.info](http://vifm.info) || [vifm](https://www.archlinux.org/packages/?name=vifm)

##### Graphical

*   **Andromeda** — Qt-based cross-platform file manager.

[https://github.com/ABBAPOH/Andromeda/](https://github.com/ABBAPOH/Andromeda/) || [andromeda](https://aur.archlinux.org/packages/andromeda/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/andromeda)]</sup>

*   **Caja** — The file manager for the MATE desktop.

[https://github.com/mate-desktop/caja](https://github.com/mate-desktop/caja) || [caja](https://www.archlinux.org/packages/?name=caja)

*   **Dino** — Easy to use and powerful file manager built in Qt.

[http://dfm.sourceforge.net/](http://dfm.sourceforge.net/) || [dino-dfm](https://aur.archlinux.org/packages/dino-dfm/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/dino-dfm)]</sup>

*   **[Dolphin](/index.php/Dolphin "Dolphin")** — File manager included in the KDE4 desktop.

[http://dolphin.kde.org/](http://dolphin.kde.org/) || [kdebase-dolphin](https://www.archlinux.org/packages/?name=kdebase-dolphin)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [dolphin](https://www.archlinux.org/packages/?name=dolphin)]</sup>

*   **Double Commander** — File manager with two panels side by side. It is inspired by Total Commander and features some new ideas.

[http://doublecmd.sourceforge.net//](http://doublecmd.sourceforge.net//) || [doublecmd-gtk2](https://www.archlinux.org/packages/?name=doublecmd-gtk2) [doublecmd-qt](https://www.archlinux.org/packages/?name=doublecmd-qt)

*   **[emelFM2](https://en.wikipedia.org/wiki/emelFM2 "wikipedia:emelFM2")** — File manager that implements the popular two-panel design.

[http://emelfm2.net/](http://emelfm2.net/) || [emelfm2](https://www.archlinux.org/packages/?name=emelfm2)

*   **Gentoo** — A lightweight file manager for GTK.

[http://www.obsession.se/gentoo/](http://www.obsession.se/gentoo/) || [gentoo](https://aur.archlinux.org/packages/gentoo/)<sup><small>AUR</small></sup>

*   **[GNOME Commander](https://en.wikipedia.org/wiki/GNOME_Commander "wikipedia:GNOME Commander")** — A dual-paned file manager for the GNOME Desktop.

[http://gcmd.github.io/](http://gcmd.github.io/) || [gnome-commander](https://www.archlinux.org/packages/?name=gnome-commander)

*   **[GNOME Files](/index.php/GNOME_Files "GNOME Files")** — Extensible, heavyweight file manager used by default in GNOME with support for custom scripts.

[https://wiki.gnome.org/Apps/Nautilus](https://wiki.gnome.org/Apps/Nautilus) || [nautilus](https://www.archlinux.org/packages/?name=nautilus)

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — File manager and web browser for the KDE desktop.

[http://www.konqueror.org/](http://www.konqueror.org/) || [kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)

*   **[Krusader](https://en.wikipedia.org/wiki/Krusader "wikipedia:Krusader")** — Advanced twin panel (Midnight Commander style) file manager for the KDE desktop.

[http://www.krusader.org/](http://www.krusader.org/) || [krusader](https://www.archlinux.org/packages/?name=krusader)

*   **muCommander** — A lightweight, cross-platform file manager with a dual-pane interface written in Java.

[http://www.mucommander.com/](http://www.mucommander.com/) || [mucommander](https://aur.archlinux.org/packages/mucommander/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/mucommander)]</sup>

*   **[Nemo](/index.php/Nemo "Nemo")** — Nemo is the file manager of the Cinnamon desktop. A good alternative to Nautilus.

[http://cinnamon.linuxmint.com/](http://cinnamon.linuxmint.com/) || [nemo](https://www.archlinux.org/packages/?name=nemo)

*   **[PathFinder](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit")** — File browser that comes with the FOX toolkit.

[http://fox-toolkit.org/](http://fox-toolkit.org/) || [fox](https://www.archlinux.org/packages/?name=fox)

*   **[PCManFM](/index.php/PCManFM "PCManFM")** — Lightweight file manager which features tabbed and dual pane browsing; also it can optionally manage the desktop icons and background.

[http://wiki.lxde.org/en/PCManFM](http://wiki.lxde.org/en/PCManFM) || [pcmanfm](https://www.archlinux.org/packages/?name=pcmanfm)

*   **QtFileMan** — File manager similar to PCManFM from LXDE.

[http://gitorious.org/qtfileman](http://gitorious.org/qtfileman) || [qtfileman-git](https://aur.archlinux.org/packages/qtfileman-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qtfileman-git)]</sup>

*   **qtFM** — Small, lightweight filemanager for Linux desktops based on pure Qt.

[http://www.qtfm.org/](http://www.qtfm.org/) || [qtfm](https://www.archlinux.org/packages/?name=qtfm)

*   **ROX** — Small and fast file manager which can optionally manage the desktop background and panels.

[http://rox.sourceforge.net](http://rox.sourceforge.net) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[SpaceFM](/index.php/SpaceFM "SpaceFM")** — GTK+ multi-panel tabbed file manager.

[http://ignorantguru.github.com/spacefm/](http://ignorantguru.github.com/spacefm/) || [spacefm](https://www.archlinux.org/packages/?name=spacefm)

*   **Sunflower** — Small and highly customizable twin-panel file manager for Linux with support for plugins.

[http://sunflower-fm.org/](http://sunflower-fm.org/) || [sunflower](https://aur.archlinux.org/packages/sunflower/)<sup><small>AUR</small></sup>

*   **[Thunar](/index.php/Thunar "Thunar")** — File manager that can be run as a daemon with excellent start up and directory load times.

[http://docs.xfce.org/xfce/thunar/start](http://docs.xfce.org/xfce/thunar/start) || [thunar](https://www.archlinux.org/packages/?name=thunar)

*   **Tux Commander** — Windowed file manager with two panels side by side similar to popular Total Commander or Midnight Commander file managers.

[http://tuxcmd.sourceforge.net/description.php](http://tuxcmd.sourceforge.net/description.php) || [tuxcmd](https://www.archlinux.org/packages/?name=tuxcmd)

*   **Worker** — Fast, lightweight and feature-rich file manager for the X Window System.

[http://www.boomerangsworld.de/worker/](http://www.boomerangsworld.de/worker/) || [worker](https://aur.archlinux.org/packages/worker/)<sup><small>AUR</small></sup>

*   **[Xfe](https://en.wikipedia.org/wiki/Xfe "wikipedia:Xfe")** — Microsoft Explorer-like file manager for X (X File Explorer).

[http://roland65.free.fr/xfe/](http://roland65.free.fr/xfe/) || [xfe](https://www.archlinux.org/packages/?name=xfe)

#### Desktop search engines

See also [Wikipedia:List of search engines#Desktop search engines](https://en.wikipedia.org/wiki/List_of_search_engines#Desktop_search_engines "wikipedia:List of search engines").

*   **Baloo** — KDE's file indexing and search solution

[https://community.kde.org/Baloo](https://community.kde.org/Baloo) || [baloo](https://www.archlinux.org/packages/?name=baloo)

*   **Catfish** — Versatile file searching tool

[https://launchpad.net/catfish-search](https://launchpad.net/catfish-search) || [catfish](https://www.archlinux.org/packages/?name=catfish)

*   **Docfetcher** — A java open source desktop search application

[http://docfetcher.sourceforge.net](http://docfetcher.sourceforge.net) || [docfetcher](https://aur.archlinux.org/packages/docfetcher/)<sup><small>AUR</small></sup>

*   **Gnome Search Tool** — Default Gnome utility to search for files

[http://gnome.org](http://gnome.org) || [gnome-search-tool](https://www.archlinux.org/packages/?name=gnome-search-tool)

*   **Gnome Search Tool No Nautilus** — _gnome-search-tool_ to search for files without [GNOME Files](/index.php/GNOME_Files "GNOME Files") or _gnome-desktop_

|| [gnome-search-tool-no-nautilus](https://aur.archlinux.org/packages/gnome-search-tool-no-nautilus/)<sup><small>AUR</small></sup>

*   **Pinot** — Personal search and metasearch tool

[http://code.google.com/p/pinot-search/](http://code.google.com/p/pinot-search/) || [pinot](https://www.archlinux.org/packages/?name=pinot)

*   **Recoll** — Full text search tool based on Xapian backend

[http://www.lesbonscomptes.com/recoll/](http://www.lesbonscomptes.com/recoll/) || [recoll](https://www.archlinux.org/packages/?name=recoll)

*   **Searchmonkey** — A powerful GUI search utility for matching regex patterns

[http://searchmonkey.sourceforge.net/](http://searchmonkey.sourceforge.net/) || [searchmonkey](https://aur.archlinux.org/packages/searchmonkey/)<sup><small>AUR</small></sup>

*   **[Strigi](https://en.wikipedia.org/wiki/Strigi "wikipedia:Strigi")** — Fast crawling desktop search engine with a Qt GUI.

[http://strigi.sourceforge.net/](http://strigi.sourceforge.net/) || [strigi](https://www.archlinux.org/packages/?name=strigi)

*   **[Tracker](https://en.wikipedia.org/wiki/Tracker_(search_software) "wikipedia:Tracker (search software)")** — All-in-one indexer, search tool and metadata database.

[https://wiki.gnome.org/Projects/Tracker](https://wiki.gnome.org/Projects/Tracker) || [tracker](https://www.archlinux.org/packages/?name=tracker)

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

[DAR - Disk ARchive](http://dar.linux.free.fr/) || [dar](https://aur.archlinux.org/packages/dar/)<sup><small>AUR</small></sup>

*   **lha** — Archiver to create LH-7 format archives. 32-bit only (require multilib on x86_64).

[http://www.infor.kanazawa-it.ac.jp/~ishii/lhaunix](http://www.infor.kanazawa-it.ac.jp/~ishii/lhaunix) || [lha](https://aur.archlinux.org/packages/lha/)<sup><small>AUR</small></sup>

*   **lrzip** — Multi-threaded compressor using the rzip/lzma, lzo, and zpaq algorithms.

[http://lrzip.kolivas.org/](http://lrzip.kolivas.org/) || [lrzip](https://www.archlinux.org/packages/?name=lrzip)

*   **lz4** — A file compressor using lz4 - An extremely fast compression algorithm.

[https://code.google.com/p/lz4/](https://code.google.com/p/lz4/) || [lz4](https://www.archlinux.org/packages/?name=lz4)

*   **lzop** — Fast file compressor using lzo lib.

[http://www.lzop.org/](http://www.lzop.org/) || [lzop](https://www.archlinux.org/packages/?name=lzop)

*   **[p7zip](/index.php/P7zip "P7zip")** — Port of 7-Zip for POSIX systems, including Linux. The commandline tool is called **7z**.

[http://p7zip.sourceforge.net/](http://p7zip.sourceforge.net/) || [p7zip](https://www.archlinux.org/packages/?name=p7zip)

*   **pixz** — A multi-threaded and indexed compressor that avoiding the drawbacks of xz.

[https://github.com/vasi/pixz](https://github.com/vasi/pixz) || [pixz](https://www.archlinux.org/packages/?name=pixz)

*   **[tar](/index.php/Tar "Tar")** — GNU utility for manipulating the ubiquitous tar archives (tarballs).

[http://www.gnu.org/software/tar](http://www.gnu.org/software/tar) || [tar](https://www.archlinux.org/packages/?name=tar)

*   **[zpaq](https://en.wikipedia.org/wiki/ZPAQ "wikipedia:ZPAQ")** — A high compression ratio archiver written in C++. Powered by Context-Model, LZ77 and BWT algorithm.

[http://mattmahoney.net/dc/zpaq.html](http://mattmahoney.net/dc/zpaq.html) || [zpaq](https://aur.archlinux.org/packages/zpaq/)<sup><small>AUR</small></sup>

*   **zopfli** — High compress ratio file compressor from Google, using a deflate-compatible algorithm called zopfli.

[https://code.google.com/p/zopfli](https://code.google.com/p/zopfli) || [zopfli-git](https://aur.archlinux.org/packages/zopfli-git/)<sup><small>AUR</small></sup>

*   **zoo** — Rarely used archiver that was mostly used in VMS world before PKZIP became popular.

[http://ftp.sunet.se/pub/usenet/ftp.uu.net/comp.sources.unix/volume11/zoo/](http://ftp.sunet.se/pub/usenet/ftp.uu.net/comp.sources.unix/volume11/zoo/) || [zoo](https://aur.archlinux.org/packages/zoo/)<sup><small>AUR</small></sup>

##### Graphical

*   **[Ark](https://en.wikipedia.org/wiki/Ark_(software) "wikipedia:Ark (software)")** — Archiving tool included in the KDE desktop.

[http://kde.org/applications/utilities/ark/](http://kde.org/applications/utilities/ark/) || [kdeutils-ark](https://www.archlinux.org/packages/?name=kdeutils-ark)<sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): replaced by [ark](https://www.archlinux.org/packages/?name=ark)]</sup>

*   **Engrampa** — Archive manager for [MATE](/index.php/MATE "MATE")

[https://github.com/mate-desktop/engrampa](https://github.com/mate-desktop/engrampa) || [engrampa](https://www.archlinux.org/packages/?name=engrampa)

*   **[File Roller](https://en.wikipedia.org/wiki/File_Roller "wikipedia:File Roller")** — Archive manager included in the GNOME desktop.

[http://fileroller.sourceforge.net/](http://fileroller.sourceforge.net/) || [file-roller](https://www.archlinux.org/packages/?name=file-roller)

*   **FreeArc** — General-purpose archiver written in haskell, comes with a GTK2 gui. Currently only available on 32-bit platform. (Requires multilib on x86_64)

[http://encode.ru/threads/43-FreeArc/](http://encode.ru/threads/43-FreeArc/) || [freearc](https://aur.archlinux.org/packages/freearc/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/freearc)]</sup>

*   **[PeaZip](https://en.wikipedia.org/wiki/PeaZip "wikipedia:PeaZip")** — Open source file and archive manager.

[http://www.peazip.org/peazip-linux.html](http://www.peazip.org/peazip-linux.html) || [peazip-gtk2](https://aur.archlinux.org/packages/peazip-gtk2/)<sup><small>AUR</small></sup> [peazip-qt](https://aur.archlinux.org/packages/peazip-qt/)<sup><small>AUR</small></sup>

*   **Squeeze** — Featherweight front-end for commandline archiving tools.

[http://squeeze.xfce.org/](http://squeeze.xfce.org/) || [squeeze-git](https://aur.archlinux.org/packages/squeeze-git/)<sup><small>AUR</small></sup>

*   **Xarchive** — Generic GTK2 front-end that uses external wrappers around commandline archiving tools.

[http://xarchive.sourceforge.net/](http://xarchive.sourceforge.net/) || [xarchive](https://aur.archlinux.org/packages/xarchive/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xarchive)]</sup>

*   **[Xarchiver](https://en.wikipedia.org/wiki/Xarchiver "wikipedia:Xarchiver")** — Lightweight desktop independent archive manager built with GTK+.

[http://xarchiver.sourceforge.net/](http://xarchiver.sourceforge.net/) || [xarchiver](https://www.archlinux.org/packages/?name=xarchiver)

#### Comparison, diff, merge

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Pacnew and Pacsave files#Managing .pacnew files](/index.php/Pacnew_and_Pacsave_files#Managing_.pacnew_files "Pacnew and Pacsave files").**

**Notes:** There's only a list of tools, and it must be in [List of applications](/index.php/List_of_applications "List of applications") (Discuss in [Talk:List of applications/Utilities#](https://wiki.archlinux.org/index.php/Talk:List_of_applications/Utilities))

See also [Wikipedia:Comparison of file comparison tools](https://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools "wikipedia:Comparison of file comparison tools").

*   **colordiff** — A Perl script wrapper for 'diff' that produces the same output but with pretty 'syntax' highlighting.

[http://www.colordiff.org/](http://www.colordiff.org/) || [colordiff](https://www.archlinux.org/packages/?name=colordiff)

*   **Diffuse** — Small and simple text merge tool written in Python.

[http://diffuse.sourceforge.net/](http://diffuse.sourceforge.net/) || [diffuse](https://www.archlinux.org/packages/?name=diffuse)

*   **KDiff3** — File and directory diff and merge tool for the KDE desktop.

[http://kdiff3.sourceforge.net/](http://kdiff3.sourceforge.net/) || [kdiff3](https://www.archlinux.org/packages/?name=kdiff3)

*   **[Kompare](https://en.wikipedia.org/wiki/Kompare "wikipedia:Kompare")** — GUI front-end program for viewing and merging differences between source files. It supports a variety of diff formats and provides many options to customize the information level displayed.

[http://www.caffeinated.me.uk/kompare/](http://www.caffeinated.me.uk/kompare/) || [kompare](https://www.archlinux.org/packages/?name=kompare)

*   **[Meld](https://en.wikipedia.org/wiki/Meld_(software) "wikipedia:Meld (software)")** — Visual diff and merge tool that can compare files, directories, and version controlled projects.

[http://meld.sourceforge.net](http://meld.sourceforge.net) || [meld](https://www.archlinux.org/packages/?name=meld)

*   **xxdiff** — A graphical browser for file and directory differences.

[http://furius.ca/xxdiff/](http://furius.ca/xxdiff/) || [xxdiff](https://aur.archlinux.org/packages/xxdiff/)<sup><small>AUR</small></sup>

[Vim](/index.php/Vim "Vim") and [Emacs](/index.php/Emacs "Emacs") provide merge functionality with [vimdiff](/index.php/Vim#Merging_files_.28vimdiff.29 "Vim") and `ediff`.

#### Batch renamers

*   **[GPRename](https://en.wikipedia.org/wiki/GPRename "wikipedia:GPRename")** — GTK+ batch renamer for files and directories.

[http://gprename.sourceforge.net](http://gprename.sourceforge.net) || [gprename](https://www.archlinux.org/packages/?name=gprename)

*   **[KRename](https://en.wikipedia.org/wiki/KRename "wikipedia:KRename")** — Very powerful batch file renamer for the KDE desktop.

[http://www.krename.net](http://www.krename.net) || [krename](https://www.archlinux.org/packages/?name=krename)

*   **metamorphose2** — wxPython based batch renamer with support for regular expressions, renaming multimedia files according to their metadata, etc.

[http://file-folder-ren.sourceforge.net](http://file-folder-ren.sourceforge.net) || [metamorphose2](https://aur.archlinux.org/packages/metamorphose2/)<sup><small>AUR</small></sup>

*   **pyRenamer** — Application for the mass renaming of files.

[http://www.infinicode.org/code/pyrenamer/](http://www.infinicode.org/code/pyrenamer/) || [pyrenamer](https://aur.archlinux.org/packages/pyrenamer/)<sup><small>AUR</small></sup>

*   **rename.pl** — Batch renamer based on perl regex.

[http://search.cpan.org/~pederst/rename/bin/rename.PL](http://search.cpan.org/~pederst/rename/bin/rename.PL) || [perl-rename](https://www.archlinux.org/packages/?name=perl-rename)

### Disk cleaning

*   **[BleachBit](https://en.wikipedia.org/wiki/BleachBit "wikipedia:BleachBit")** — It frees disk space and guards your privacy; frees cache, deletes cookies, clears Internet history, shreds temporary files, deletes logs, and discards junk you didn't know was there.

[http://bleachbit.sourceforge.net/](http://bleachbit.sourceforge.net/) || [bleachbit](https://www.archlinux.org/packages/?name=bleachbit)

*   **gconf-cleaner** — cleans up the unknown/invalid gconf keys that still sitting down on your gconf database

[https://code.google.com/p/gconf-cleaner/](https://code.google.com/p/gconf-cleaner/) || [gconf-cleaner](https://aur.archlinux.org/packages/gconf-cleaner/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gconf-cleaner)]</sup>

### Disk usage display

*   **[Disk Usage Analyzer](https://en.wikipedia.org/wiki/Disk_Usage_Analyzer "wikipedia:Disk Usage Analyzer") (Baobab)** — Disk usage analyzer for the [GNOME](/index.php/GNOME "GNOME") desktop.

[http://www.marzocca.net/linux/baobab](http://www.marzocca.net/linux/baobab) || [baobab](https://www.archlinux.org/packages/?name=baobab) [baobab36](https://aur.archlinux.org/packages/baobab36/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/baobab36)]</sup>

*   **[Filelight](https://en.wikipedia.org/wiki/Filelight "wikipedia:Filelight")** — Disk usage analyzer that creates an interactive map of concentric, segmented rings that help visualise disk usage on your computer.

[http://methylblue.com/filelight/](http://methylblue.com/filelight/) || [filelight](https://www.archlinux.org/packages/?name=filelight)

*   **GdMap** — Disk usage analyzer that draws a map of rectangles sized according to file or dir sizes.

[http://gdmap.sourceforge.net/](http://gdmap.sourceforge.net/) || [gdmap](https://www.archlinux.org/packages/?name=gdmap)

*   **gt5** — Diff-capable "du-browser".

[http://gt5.sourceforge.net](http://gt5.sourceforge.net) || [gt5](https://aur.archlinux.org/packages/gt5/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gt5)]</sup>

*   **ncdu** — Simple ncurses disk usage analyzer.

[http://dev.yorhel.nl/ncdu](http://dev.yorhel.nl/ncdu) || [ncdu](https://www.archlinux.org/packages/?name=ncdu)

### Clock synchronization

*   **[NTPd](/index.php/NTPd "NTPd")** — Network Time Protocol reference implementation.

[http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project](http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project) || [ntp](https://www.archlinux.org/packages/?name=ntp)

*   **[Chrony](/index.php/Chrony "Chrony")** — Lightweight NTP client and server.

[http://chrony.tuxfamily.org/](http://chrony.tuxfamily.org/) || [chrony](https://www.archlinux.org/packages/?name=chrony)

*   **[OpenNTPD](/index.php/OpenNTPD "OpenNTPD")** — Free, easy to use implementation of the Network Time Protocol.

[http://www.openntpd.org/](http://www.openntpd.org/) || [openntpd](https://www.archlinux.org/packages/?name=openntpd)

### System monitoring

*   **adesklet SystemMonitor** — Collection of modular stackable system monitors for [adesklets](https://en.wikipedia.org/wiki/Adesklets "wikipedia:Adesklets").

[http://adesklets.sourceforge.net/desklets.html](http://adesklets.sourceforge.net/desklets.html) || [adesklet-systemmonitor](https://aur.archlinux.org/packages/adesklet-systemmonitor/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/adesklet-systemmonitor)]</sup>

*   **candybar** — WebKit-based status line for tiling window managers.

[https://github.com/Lokaltog/candybar](https://github.com/Lokaltog/candybar) || [candybar-git](https://aur.archlinux.org/packages/candybar-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/candybar-git)]</sup>

*   **[Conky](/index.php/Conky "Conky")** — Lightweight, scriptable system monitor.

[https://github.com/brndnmtthws/conky](https://github.com/brndnmtthws/conky) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **Collectd** — A simple, extensible system monitoring daemon based on [rrdtool](http://oss.oetiker.ch/rrdtool/). It has a small footprint and can be set up either stand-alone or as a server/client application.

[https://collectd.org/](https://collectd.org/) || [collectd](https://www.archlinux.org/packages/?name=collectd)

*   **dstat** — Versatile resource statistics tool.

[http://dag.wieers.com/home-made/dstat/](http://dag.wieers.com/home-made/dstat/) || [dstat](https://www.archlinux.org/packages/?name=dstat)

*   **[GKrellM](https://en.wikipedia.org/wiki/GKrellM "wikipedia:GKrellM")** — Simple, flexible system monitor package for [GTK+](/index.php/GTK%2B "GTK+") with many plug-ins.

[http://members.dslextreme.com/users/billw/gkrellm/gkrellm.html](http://members.dslextreme.com/users/billw/gkrellm/gkrellm.html) || [gkrellm](https://www.archlinux.org/packages/?name=gkrellm)

*   **gnome-system-monitor** — A system monitor for [GNOME](/index.php/GNOME "GNOME").

[https://help.gnome.org/users/gnome-system-monitor/](https://help.gnome.org/users/gnome-system-monitor/) || [gnome-system-monitor](https://www.archlinux.org/packages/?name=gnome-system-monitor) [gnome-system-monitor-gtk2](https://aur.archlinux.org/packages/gnome-system-monitor-gtk2/)<sup><small>AUR</small></sup>

*   **[htop](https://en.wikipedia.org/wiki/Htop "wikipedia:Htop")** — Simple, ncurses interactive process viewer.

[http://htop.sourceforge.net/](http://htop.sourceforge.net/) || [htop](https://www.archlinux.org/packages/?name=htop)

*   **[KSysGuard](https://en.wikipedia.org/wiki/KDE_System_Guard "wikipedia:KDE System Guard")** — Also known as KSysguard, is the [KDE](/index.php/KDE "KDE") task manager and performance monitor.

[http://userbase.kde.org/KSysGuard](http://userbase.kde.org/KSysGuard) || [ksysguard](https://www.archlinux.org/packages/?name=ksysguard) or as part of [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)<sup><small>AUR</small></sup>

*   **linux process explorer** — Graphical process explorer for Linux.

[http://sourceforge.net/projects/procexp/](http://sourceforge.net/projects/procexp/) || [procexp](https://aur.archlinux.org/packages/procexp/)<sup><small>AUR</small></sup>

*   **LXTask** — Lightweight task manager for [LXDE](/index.php/LXDE "LXDE").

[http://wiki.lxde.org/en/LXTask](http://wiki.lxde.org/en/LXTask) || [lxtask](https://www.archlinux.org/packages/?name=lxtask)

*   **mate-system-monitor** — A GTK2 system monitor for [MATE](/index.php/MATE "MATE").

[https://github.com/mate-desktop/mate-system-monitor](https://github.com/mate-desktop/mate-system-monitor) || [mate-system-monitor](https://www.archlinux.org/packages/?name=mate-system-monitor)

*   **Task Manager** — GTK2 process mangement application for [Xfce](/index.php/Xfce "Xfce").

[http://goodies.xfce.org/projects/applications/xfce4-taskmanager](http://goodies.xfce.org/projects/applications/xfce4-taskmanager) || [xfce4-taskmanager](https://www.archlinux.org/packages/?name=xfce4-taskmanager)

*   **[Paramano](/index.php/Paramano "Paramano")** — A light battery monitor and a CPU frequency scaler. Forked from trayfreq

[http://batchbin.ueuo.com/projects/trayfreq-archlinux/](http://batchbin.ueuo.com/projects/trayfreq-archlinux/) || [paramano](https://aur.archlinux.org/packages/paramano/)<sup><small>AUR</small></sup>

*   **Sysstat** — A collection of resource monitoring tools: iostat, isag, mpstat, pidstat, sadf, sar.

[http://pagesperso-orange.fr/sebastien.godard/](http://pagesperso-orange.fr/sebastien.godard/) || [sysstat](https://www.archlinux.org/packages/?name=sysstat)

### System information viewers

#### Console

*   **alsi** — A system information tool for Arch Linux. It can be configured for every other system without even touching the source code of the script.

[http://trizenx.blogspot.ro/2012/08/alsi.html](http://trizenx.blogspot.ro/2012/08/alsi.html) || [alsi](https://aur.archlinux.org/packages/alsi/)<sup><small>AUR</small></sup>

*   **archey** — Simple python script that displays the arch logo and some basic information. Depends on python3.

[https://github.com/djmelik/archey](https://github.com/djmelik/archey) || [archey](https://aur.archlinux.org/packages/archey/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/archey)]</sup>

*   **archey2** — Simple python script that displays the arch logo and some basic information. Python 2.x version.

[https://github.com/djmelik/archey](https://github.com/djmelik/archey) || [archey2](https://aur.archlinux.org/packages/archey2/)<sup><small>AUR</small></sup>

*   **archey3-git** — Python script to display system infomation alongside the Arch Linux logo.

[http://www.generictestdomain.net/archey3/](http://www.generictestdomain.net/archey3/) || [archey3-git](https://aur.archlinux.org/packages/archey3-git/)<sup><small>AUR</small></sup>

*   **dmidecode** — It reports information about your system's hardware as described in your system BIOS according to the SMBIOS/DMI standard.

[http://www.nongnu.org/dmidecode/](http://www.nongnu.org/dmidecode/) || [dmidecode](https://www.archlinux.org/packages/?name=dmidecode)|

*   **hwdetect** — Simple script to list modules that are exported by /sys, a part of [archboot](/index.php/Archboot "Archboot").

[https://projects.archlinux.org/](https://projects.archlinux.org/) || [hwdetect](https://www.archlinux.org/packages/?name=hwdetect)

*   **hwinfo** — Powerful hardware detection tool come from openSUSE.

[https://github.com/openSUSE/hwinfo](https://github.com/openSUSE/hwinfo) || [hwinfo](https://www.archlinux.org/packages/?name=hwinfo)

*   **inxi** — A script to get system information.

[https://code.google.com/p/inxi](https://code.google.com/p/inxi) || [inxi](https://www.archlinux.org/packages/?name=inxi)

*   **screenfetch** — Similar to archey but has an option to take a screenshot. Written in bash.

[https://github.com/KittyKatt/screenFetch](https://github.com/KittyKatt/screenFetch) || [screenfetch](https://www.archlinux.org/packages/?name=screenfetch)

#### Graphical

*   **CPU-G** — An application that shows useful information about your hardware, it looks like CPU-Z in Windows.

[http://cpug.sourceforge.net/](http://cpug.sourceforge.net/) || [cpu-g](https://aur.archlinux.org/packages/cpu-g/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/cpu-g)]</sup>

*   **hardinfo** — A small application that displays information about your hardware and operating system, it looks like the Device Manager in Windows.

[http://hardinfo.berlios.de/HomePage](http://hardinfo.berlios.de/HomePage) || [hardinfo](https://www.archlinux.org/packages/?name=hardinfo)

*   **i-Nex** — An application that gathers information for hardware components available on your system and displays it using an user interface similar to the popular Windows tool CPU-Z.

[http://i-nex.linux.pl/](http://i-nex.linux.pl/) || [i-nex-git](https://aur.archlinux.org/packages/i-nex-git/)<sup><small>AUR</small></sup>

*   **lshw-gtk** — A small tool to provide detailed information on the hardware configuration of the machine with CLI and GTK interfaces.

[http://ezix.org/project/wiki/HardwareLiSter](http://ezix.org/project/wiki/HardwareLiSter) || [lshw-gtk](https://aur.archlinux.org/packages/lshw-gtk/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/lshw-gtk)]</sup>

#### Others

*   **tp-hdd-led** — Monitor HDD use with the Think-Led

[http://en.timherbst.de/tp-hdd-led/](http://en.timherbst.de/tp-hdd-led/) || [tp-hdd-led](https://aur.archlinux.org/packages/tp-hdd-led/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tp-hdd-led)]</sup>

### Keyboard layout switchers

*   **fbxkb** — A NETWM compliant keyboard indicator and switcher. It shows a flag of current keyboard in a systray area and allows you to switch to another one.

[http://fbxkb.sourceforge.net/](http://fbxkb.sourceforge.net/) || [fbxkb](https://aur.archlinux.org/packages/fbxkb/)<sup><small>AUR</small></sup>

*   **xxkb** — A lightweight keyboard layout indicator and switcher.

[http://sourceforge.net/projects/xxkb/](http://sourceforge.net/projects/xxkb/) || [xxkb](https://www.archlinux.org/packages/?name=xxkb)

*   **qxkb** — A keyboard switcher written in Qt.

[http://code.google.com/p/qxkb/](http://code.google.com/p/qxkb/) || [qxkb](https://aur.archlinux.org/packages/qxkb/)<sup><small>AUR</small></sup>

*   **[X Neural Switcher](https://en.wikipedia.org/wiki/X_Neural_Switcher "wikipedia:X Neural Switcher")** — A text analyser, it detects the language of the input and corrects the keyboard layout if needed.

[http://www.xneur.ru/](http://www.xneur.ru/) || [xneur](https://aur.archlinux.org/packages/xneur/)<sup><small>AUR</small></sup>, [gxneur](https://aur.archlinux.org/packages/gxneur/)<sup><small>AUR</small></sup> (GUI)

### Power management

See [Power saving#Packages](/index.php/Power_saving#Packages "Power saving").

### Clipboard managers

See: [List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard").

### Wallpaper setters

*   **bgs** — An extremely fast and small background setter for X based on imlib2.

[http://github.com/Gottox/bgs/](http://github.com/Gottox/bgs/) || [bgs-git](https://aur.archlinux.org/packages/bgs-git/)<sup><small>AUR</small></sup>

*   **esetroot** — Eterm's root background setter, packaged separately

[http://www.eterm.org/](http://www.eterm.org/) || [esetroot](https://aur.archlinux.org/packages/esetroot/)<sup><small>AUR</small></sup>

*   **[Feh](/index.php/Feh "Feh")** — A lightweight and powerful image viewer that can also be used to manage the desktop wallpaper.

[http://linuxbrit.co.uk/software/feh/](http://linuxbrit.co.uk/software/feh/) || [feh](https://www.archlinux.org/packages/?name=feh)‎

*   **habak** — A background changing app

[http://fvwm-crystal.org/](http://fvwm-crystal.org/) || [habak](https://www.archlinux.org/packages/?name=habak)

*   **hsetroot** — A tool to create compose wallpapers.

[https://packages.debian.org/sid/hsetroot](https://packages.debian.org/sid/hsetroot) || [hsetroot](https://aur.archlinux.org/packages/hsetroot/)<sup><small>AUR</small></sup>

*   **[Nitrogen](/index.php/Nitrogen "Nitrogen")** — A fast and lightweight desktop background browser and setter for X windows.

[http://projects.l3ib.org/nitrogen/](http://projects.l3ib.org/nitrogen/) || [nitrogen](https://www.archlinux.org/packages/?name=nitrogen)

*   **pybgsetter** — Multi-backend (hsetroot, Esetroot, habak, feh) to set desktop wallpaper

http://bbs.archlinux.org/viewtopic.php?id=88997 || [pybgsetter](https://aur.archlinux.org/packages/pybgsetter/)<sup><small>AUR</small></sup>

*   **wallpaperd** — A small application that takes care of setting the background image

[https://projects.pekdon.net/projects/wallpaperd](https://projects.pekdon.net/projects/wallpaperd) || [wallpaperd](https://aur.archlinux.org/packages/wallpaperd/)<sup><small>AUR</small></sup>

*   **xli** — An image display program for X

[https://packages.debian.org/sid/xli](https://packages.debian.org/sid/xli) || [xli](https://aur.archlinux.org/packages/xli/)<sup><small>AUR</small></sup>

**Tip:** In order to avoid installing one more package, you may find convenient to use the `display` utility from [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) or `gm display` from [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick). E.g.: `display -backdrop -background '#3f3f3f' -flatten -window root _image_`.

### Package management

See [pacman tips#Utilities](/index.php/Pacman_tips#Utilities "Pacman tips").

### Input method editor

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Internationalization#Input_methods_in_Xorg](/index.php/Internationalization#Input_methods_in_Xorg "Internationalization").**

**Notes:** Then just link there. (Discuss in [Talk:List of applications/Utilities#](https://wiki.archlinux.org/index.php/Talk:List_of_applications/Utilities))

See also [Wikipedia:Input method](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method").

*   **[Fcitx](/index.php/Fcitx "Fcitx")** — Flexible Context-aware Input Tool with eXtension.

[http://fcitx-im.org](http://fcitx-im.org) || [fcitx](https://www.archlinux.org/packages/?name=fcitx)

*   **Hime** — A GTK2+/GTK3+ based universal input method platform.

[http://hime-ime.github.io/](http://hime-ime.github.io/) || [hime-git](https://aur.archlinux.org/packages/hime-git/)<sup><small>AUR</small></sup>

*   **[IBus](/index.php/IBus "IBus")** — Next Generation Input Bus for Linux.

[http://ibus.googlecode.com](http://ibus.googlecode.com) || [ibus](https://www.archlinux.org/packages/?name=ibus)

*   **[Rime IME](/index.php/Rime_IME "Rime IME")** — Rime input method engine.

[http://code.google.com/p/rimeime/](http://code.google.com/p/rimeime/) || [ibus-rime](https://www.archlinux.org/packages/?name=ibus-rime) or [fcitx-rime](https://www.archlinux.org/packages/?name=fcitx-rime)

*   **[UIM](/index.php/UIM "UIM")** — Multilingual input method library.

[http://code.google.com/p/uim/](http://code.google.com/p/uim/) || [uim](https://www.archlinux.org/packages/?name=uim)

### Trash management

*   **trash-cli** — A command-line interface implementing FreeDesktop.org's Trash specification.

[http://github.com/andreafrancia/trash-cli](http://github.com/andreafrancia/trash-cli) || [trash-cli](https://www.archlinux.org/packages/?name=trash-cli)

### File synchronization

*   **[rsync](/index.php/Rsync "Rsync")** — An incremental transfer and synchronization program.

[http://rsync.samba.org](http://rsync.samba.org) || [rsync](https://www.archlinux.org/packages/?name=rsync)

*   **[Syncthing](/index.php/Syncthing "Syncthing")** — Open, trustworthy and decentralized cloud synchronization service.

[https://syncthing.net](https://syncthing.net) || [syncthing](https://www.archlinux.org/packages/?name=syncthing)

*   **[Unison](/index.php/Unison "Unison")** — Bidirectional sync. It keeps track of changes like a VCS.

[http://www.cis.upenn.edu/~bcpierce/unison](http://www.cis.upenn.edu/~bcpierce/unison) || [unison](https://www.archlinux.org/packages/?name=unison)

### Finders

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** See also [find](/index.php/Find "Find") and [locate](/index.php/Locate "Locate"). (Discuss in [Talk:List of applications/Utilities#](https://wiki.archlinux.org/index.php/Talk:List_of_applications/Utilities))

*   **fuzzy-find** — Fuzzy completion for finding files.

[https://github.com/silentbicycle/ff](https://github.com/silentbicycle/ff) || [ff-git](https://aur.archlinux.org/packages/ff-git/)<sup><small>AUR</small></sup>

*   **fzf** — General-purpose command-line fuzzy finder.

[https://github.com/junegunn/fzf](https://github.com/junegunn/fzf) || [fzf](https://aur.archlinux.org/packages/fzf/)<sup><small>AUR</small></sup>

*   **rmlint** — Tool to quickly find (and optionally remove) duplicate files and other lint

[https://rmlint.readthedocs.org/en/latest/](https://rmlint.readthedocs.org/en/latest/) || [rmlint](https://www.archlinux.org/packages/?name=rmlint)

Retrieved from "[https://wiki.archlinux.org/index.php?title=List_of_applications/Utilities&oldid=415664](https://wiki.archlinux.org/index.php?title=List_of_applications/Utilities&oldid=415664)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Applications](/index.php/Category:Applications "Category:Applications")

Hidden categories:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")
*   [Pages or sections flagged with Template:Expansion](/index.php/Category:Pages_or_sections_flagged_with_Template:Expansion "Category:Pages or sections flagged with Template:Expansion")