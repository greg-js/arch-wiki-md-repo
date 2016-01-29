# List of applications

****List of applications****

* * *

[Internet](/index.php/List_of_applications/Internet "List of applications/Internet") – [Multimedia](/index.php/List_of_applications/Multimedia "List of applications/Multimedia") – [Utilities](/index.php/List_of_applications/Utilities "List of applications/Utilities") – [Documents](/index.php/List_of_applications/Documents "List of applications/Documents") – [Security](/index.php/List_of_applications/Security "List of applications/Security") – [Science](/index.php/List_of_applications/Science "List of applications/Science") – [Other](/index.php/List_of_applications/Other "List of applications/Other")

Related articles

*   [Core utilities](/index.php/Core_utilities "Core utilities")
*   [List of games](/index.php/List_of_games "List of games")

This article is a general list of applications sorted by category, as a reference for those looking for packages. Many sections are split between console and graphical applications.

**Tip:**

*   This page exists primarily to make it easier to search for alternatives to an application that you do not know under which section has been added. Use the links in the template at the top to view the main sections as separate pages.
*   Please consider [installing](/index.php/Installing "Installing") the [pkgstats](/index.php/Pkgstats "Pkgstats") package, which provides a timer that sends a list of the packages installed on your system, along with the architecture and the mirrors you use, to the Arch Linux developers in order to help them prioritize their efforts and make the distribution even better. The information is sent anonymously and cannot be used to identify you. You can view the collected data at the [Statistics page](https://www.archlinux.de/?page=Statistics). More information is available in [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=105431).
*   Daemon packages usually include the relevant systemd unit file to [start](/index.php/Start "Start"); some packages even include different ones. After installation `pacman -Qql _package_ | grep -Fe .service -e .socket` can be used to check and find the relevant one.

**Note:** Applications listed in "Console" sections can have graphical front-ends. Official ones are currently omitted.

## Contents

*   [1 Internet](#Internet)
    *   [1.1 Network managers](#Network_managers)
    *   [1.2 Web browsers](#Web_browsers)
        *   [1.2.1 Console](#Console)
        *   [1.2.2 Graphical](#Graphical)
            *   [1.2.2.1 Gecko-based](#Gecko-based)
                *   [1.2.2.1.1 Firefox forks](#Firefox_forks)
            *   [1.2.2.2 Blink-based](#Blink-based)
            *   [1.2.2.3 Webkit-based](#Webkit-based)
            *   [1.2.2.4 Other](#Other)
    *   [1.3 File sharing](#File_sharing)
        *   [1.3.1 FTP](#FTP)
            *   [1.3.1.1 FTP clients](#FTP_clients)
            *   [1.3.1.2 FTP servers](#FTP_servers)
        *   [1.3.2 BitTorrent clients](#BitTorrent_clients)
            *   [1.3.2.1 Console](#Console_2)
                *   [1.3.2.1.1 Command line / backend](#Command_line_.2F_backend)
                *   [1.3.2.1.2 Console Interface](#Console_Interface)
            *   [1.3.2.2 Graphical Interface](#Graphical_Interface)
                *   [1.3.2.2.1 libtorrent-rasterbar backend](#libtorrent-rasterbar_backend)
                *   [1.3.2.2.2 libktorrent backend](#libktorrent_backend)
                *   [1.3.2.2.3 others](#others)
        *   [1.3.3 Other P2P networks](#Other_P2P_networks)
        *   [1.3.4 Video downloaders](#Video_downloaders)
    *   [1.4 Communication](#Communication)
        *   [1.4.1 Email clients](#Email_clients)
            *   [1.4.1.1 Console](#Console_3)
            *   [1.4.1.2 Graphical](#Graphical_2)
        *   [1.4.2 Instant messaging](#Instant_messaging)
            *   [1.4.2.1 IRC clients](#IRC_clients)
                *   [1.4.2.1.1 Console](#Console_4)
                *   [1.4.2.1.2 Graphical](#Graphical_3)
            *   [1.4.2.2 XMPP (Jabber)](#XMPP_.28Jabber.29)
                *   [1.4.2.2.1 Console clients](#Console_clients)
                *   [1.4.2.2.2 Graphical clients](#Graphical_clients)
                *   [1.4.2.2.3 Servers](#Servers)
            *   [1.4.2.3 Multi-protocol clients](#Multi-protocol_clients)
                *   [1.4.2.3.1 Console](#Console_5)
                *   [1.4.2.3.2 Graphical](#Graphical_4)
            *   [1.4.2.4 Lan messengers](#Lan_messengers)
        *   [1.4.3 VoIP / Softphone](#VoIP_.2F_Softphone)
            *   [1.4.3.1 Clients](#Clients)
                *   [1.4.3.1.1 SIP](#SIP)
                *   [1.4.3.1.2 IAX2](#IAX2)
                *   [1.4.3.1.3 Skype](#Skype)
                *   [1.4.3.1.4 Other](#Other_2)
                *   [1.4.3.1.5 Multi-protocol](#Multi-protocol)
            *   [1.4.3.2 Utilities](#Utilities)
        *   [1.4.4 Speech recognition](#Speech_recognition)
    *   [1.5 News, RSS, and blogs](#News.2C_RSS.2C_and_blogs)
        *   [1.5.1 News aggregators](#News_aggregators)
            *   [1.5.1.1 Console](#Console_6)
            *   [1.5.1.2 Graphical](#Graphical_5)
        *   [1.5.2 Podcast clients](#Podcast_clients)
        *   [1.5.3 Usenet newsreaders & newsgrabbers](#Usenet_newsreaders_.26_newsgrabbers)
        *   [1.5.4 Blog software](#Blog_software)
        *   [1.5.5 Microblogging clients](#Microblogging_clients)
    *   [1.6 Pastebin clients](#Pastebin_clients)
    *   [1.7 Bitcoin](#Bitcoin)
    *   [1.8 Surveying](#Surveying)
*   [2 Multimedia](#Multimedia)
    *   [2.1 Codecs](#Codecs)
    *   [2.2 Image](#Image)
        *   [2.2.1 Image viewers](#Image_viewers)
            *   [2.2.1.1 Console](#Console_7)
            *   [2.2.1.2 Graphical](#Graphical_6)
        *   [2.2.2 Graphics and image manipulation](#Graphics_and_image_manipulation)
            *   [2.2.2.1 Raster editors](#Raster_editors)
            *   [2.2.2.2 Vector graphics - illustration](#Vector_graphics_-_illustration)
            *   [2.2.2.3 Vector graphics - CAD](#Vector_graphics_-_CAD)
            *   [2.2.2.4 3D modeling/rendering](#3D_modeling.2Frendering)
        *   [2.2.3 Screen capture](#Screen_capture)
    *   [2.3 Audio](#Audio)
        *   [2.3.1 Audio systems](#Audio_systems)
        *   [2.3.2 Audio players](#Audio_players)
            *   [2.3.2.1 Music player daemons and clients](#Music_player_daemons_and_clients)
            *   [2.3.2.2 Command-line players](#Command-line_players)
            *   [2.3.2.3 GUI players](#GUI_players)
        *   [2.3.3 Volume managers](#Volume_managers)
        *   [2.3.4 CD ripping](#CD_ripping)
        *   [2.3.5 Visualization](#Visualization)
        *   [2.3.6 Audio tag editors](#Audio_tag_editors)
        *   [2.3.7 Sound editing](#Sound_editing)
    *   [2.4 Mobile phone managers](#Mobile_phone_managers)
    *   [2.5 Video](#Video)
        *   [2.5.1 Video players](#Video_players)
            *   [2.5.1.1 Console](#Console_8)
            *   [2.5.1.2 Graphical](#Graphical_7)
        *   [2.5.2 Subtitles](#Subtitles)
        *   [2.5.3 DVD ripping](#DVD_ripping)
        *   [2.5.4 Video editors](#Video_editors)
            *   [2.5.4.1 Console](#Console_9)
            *   [2.5.4.2 Graphical](#Graphical_8)
        *   [2.5.5 Screencast](#Screencast)
    *   [2.6 Optical media burning](#Optical_media_burning)
    *   [2.7 Podcasts](#Podcasts)
    *   [2.8 Collection managers](#Collection_managers)
    *   [2.9 Lyrics fetchers](#Lyrics_fetchers)
*   [3 Utilities](#Utilities_2)
    *   [3.1 Partitioning tools](#Partitioning_tools)
    *   [3.2 Mount tools](#Mount_tools)
        *   [3.2.1 Udisks](#Udisks)
    *   [3.3 Basic shell commands](#Basic_shell_commands)
    *   [3.4 Integrated development environments](#Integrated_development_environments)
    *   [3.5 Build automation](#Build_automation)
    *   [3.6 Terminal emulators](#Terminal_emulators)
        *   [3.6.1 VTE-based](#VTE-based)
        *   [3.6.2 KMS-based](#KMS-based)
        *   [3.6.3 framebuffer-based](#framebuffer-based)
    *   [3.7 Files](#Files)
        *   [3.7.1 File managers](#File_managers)
            *   [3.7.1.1 Console](#Console_10)
            *   [3.7.1.2 Graphical](#Graphical_9)
        *   [3.7.2 Desktop search engines](#Desktop_search_engines)
        *   [3.7.3 Archiving and compression tools](#Archiving_and_compression_tools)
            *   [3.7.3.1 Console](#Console_11)
            *   [3.7.3.2 Graphical](#Graphical_10)
        *   [3.7.4 Comparison, diff, merge](#Comparison.2C_diff.2C_merge)
        *   [3.7.5 Batch renamers](#Batch_renamers)
    *   [3.8 Disk cleaning](#Disk_cleaning)
    *   [3.9 Disk usage display](#Disk_usage_display)
    *   [3.10 Clock synchronization](#Clock_synchronization)
    *   [3.11 System monitoring](#System_monitoring)
    *   [3.12 System information viewers](#System_information_viewers)
        *   [3.12.1 Console](#Console_12)
        *   [3.12.2 Graphical](#Graphical_11)
        *   [3.12.3 Others](#Others_2)
    *   [3.13 Keyboard layout switchers](#Keyboard_layout_switchers)
    *   [3.14 Power management](#Power_management)
    *   [3.15 Clipboard managers](#Clipboard_managers)
    *   [3.16 Wallpaper setters](#Wallpaper_setters)
    *   [3.17 Package management](#Package_management)
    *   [3.18 Input method editor](#Input_method_editor)
    *   [3.19 Trash management](#Trash_management)
    *   [3.20 File synchronization](#File_synchronization)
    *   [3.21 Finders](#Finders)
*   [4 Documents and texts](#Documents_and_texts)
    *   [4.1 Office suites](#Office_suites)
    *   [4.2 Word processors](#Word_processors)
    *   [4.3 Document markup languages](#Document_markup_languages)
    *   [4.4 Spreadsheets](#Spreadsheets)
    *   [4.5 Scientific documents](#Scientific_documents)
    *   [4.6 Translation and localization](#Translation_and_localization)
    *   [4.7 Text editors](#Text_editors)
        *   [4.7.1 Console](#Console_13)
            *   [4.7.1.1 Vi text editors](#Vi_text_editors)
        *   [4.7.2 Graphical](#Graphical_12)
            *   [4.7.2.1 Collaborative text editors](#Collaborative_text_editors)
    *   [4.8 Readers and Viewers](#Readers_and_Viewers)
        *   [4.8.1 E-book applications](#E-book_applications)
            *   [4.8.1.1 Book organizers](#Book_organizers)
        *   [4.8.2 PDF and DjVu](#PDF_and_DjVu)
            *   [4.8.2.1 Console](#Console_14)
            *   [4.8.2.2 Graphical](#Graphical_13)
        *   [4.8.3 Terminal pagers](#Terminal_pagers)
        *   [4.8.4 CHM](#CHM)
        *   [4.8.5 Comic book (comix/manga)](#Comic_book_.28comix.2Fmanga.29)
    *   [4.9 Scanning software](#Scanning_software)
    *   [4.10 OCR software](#OCR_software)
        *   [4.10.1 Engines](#Engines)
        *   [4.10.2 Layout analyzers and user interfaces](#Layout_analyzers_and_user_interfaces)
    *   [4.11 Note taking organizers](#Note_taking_organizers)
        *   [4.11.1 Console](#Console_15)
        *   [4.11.2 Graphical](#Graphical_14)
    *   [4.12 Mind-mapping tools](#Mind-mapping_tools)
    *   [4.13 Character Selector](#Character_Selector)
    *   [4.14 Stylus notes taking](#Stylus_notes_taking)
    *   [4.15 Bibliographic reference managers](#Bibliographic_reference_managers)
*   [5 Security](#Security)
    *   [5.1 Firewalls](#Firewalls)
    *   [5.2 Network security](#Network_security)
    *   [5.3 Threat and vulnerability detection](#Threat_and_vulnerability_detection)
    *   [5.4 File security](#File_security)
    *   [5.5 Anti malware](#Anti_malware)
    *   [5.6 Backup programs](#Backup_programs)
    *   [5.7 Screen lockers](#Screen_lockers)
    *   [5.8 Hash checkers](#Hash_checkers)
    *   [5.9 Encryption, signing, steganography](#Encryption.2C_signing.2C_steganography)
    *   [5.10 Password managers](#Password_managers)
*   [6 Science](#Science)
    *   [6.1 Scientific documents](#Scientific_documents_2)
    *   [6.2 Mathematics](#Mathematics)
        *   [6.2.1 Calculator](#Calculator)
        *   [6.2.2 Computer algebra system](#Computer_algebra_system)
        *   [6.2.3 Scientific or technical computing](#Scientific_or_technical_computing)
        *   [6.2.4 Statistics](#Statistics)
        *   [6.2.5 Data evaluation](#Data_evaluation)
    *   [6.3 Chemistry and biology](#Chemistry_and_biology)
        *   [6.3.1 Computational biology and bioinformatics](#Computational_biology_and_bioinformatics)
        *   [6.3.2 Molecules](#Molecules)
            *   [6.3.2.1 Viewers](#Viewers)
            *   [6.3.2.2 Drawing](#Drawing)
            *   [6.3.2.3 Modeling](#Modeling)
        *   [6.3.3 Periodic table](#Periodic_table)
        *   [6.3.4 Biochemistry](#Biochemistry)
        *   [6.3.5 Image manipulation](#Image_manipulation)
    *   [6.4 Astronomy](#Astronomy)
    *   [6.5 Physics](#Physics)
        *   [6.5.1 Electronics](#Electronics)
            *   [6.5.1.1 Digital logic](#Digital_logic)
            *   [6.5.1.2 HDL](#HDL)
            *   [6.5.1.3 MCU IDE](#MCU_IDE)
            *   [6.5.1.4 Schematic capture editor](#Schematic_capture_editor)
        *   [6.5.2 Physics simulation](#Physics_simulation)
        *   [6.5.3 Unit conversion](#Unit_conversion)
*   [7 Others](#Others_3)
    *   [7.1 Work environment](#Work_environment)
        *   [7.1.1 Bootsplash](#Bootsplash)
        *   [7.1.2 Command shells](#Command_shells)
        *   [7.1.3 Terminal multiplexers](#Terminal_multiplexers)
        *   [7.1.4 Desktop environments](#Desktop_environments)
        *   [7.1.5 Window managers](#Window_managers)
            *   [7.1.5.1 Console](#Console_16)
            *   [7.1.5.2 Graphical](#Graphical_15)
        *   [7.1.6 Window tilers](#Window_tilers)
        *   [7.1.7 Virtual desktop pagers](#Virtual_desktop_pagers)
        *   [7.1.8 Support applications](#Support_applications)
            *   [7.1.8.1 Login managers](#Login_managers)
            *   [7.1.8.2 Composite managers](#Composite_managers)
            *   [7.1.8.3 Taskbars / panels / docks](#Taskbars_.2F_panels_.2F_docks)
            *   [7.1.8.4 Application launchers](#Application_launchers)
            *   [7.1.8.5 Logout dialogue](#Logout_dialogue)
        *   [7.1.9 Accessibility](#Accessibility)
            *   [7.1.9.1 Screen reading](#Screen_reading)
            *   [7.1.9.2 Speech recognition](#Speech_recognition_2)
    *   [7.2 Finance](#Finance)
    *   [7.3 Flashcards](#Flashcards)
    *   [7.4 Time management](#Time_management)
        *   [7.4.1 Console](#Console_17)
        *   [7.4.2 Graphical](#Graphical_16)
    *   [7.5 Emulators](#Emulators)
        *   [7.5.1 Consoles](#Consoles)
        *   [7.5.2 Other](#Other_3)
    *   [7.6 Amateur radio](#Amateur_radio)
*   [8 See also](#See_also)

## Internet

**Note:** For possibly more up to date selection of applications, try checking the [AUR 'network' category](https://aur.archlinux.org/packages.php?O=0&K=&do_Search=Go&detail=1&C=13&SeB=nd&SB=n&SO=a&PP=50)

### Network managers

*   **[Connman](/index.php/Connman "Connman")** — Daemon for managing internet connections within embedded devices running the Linux operating system. Comes with a command-line client, plus Enlightenment, GTK and Dmenu clients are available.

NaN

*   **[netctl](/index.php/Netctl "Netctl")** — Simple and robust tool to manage network connections via profiles. Intended for use with [systemd](/index.php/Systemd "Systemd").

NaN

*   **[NetworkManager](/index.php/NetworkManager "NetworkManager")** — Manager that provides wired, wireless, mobile broadband and OpenVPN detection with configuration and automatic connection.

NaN

*   **[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")** — Native [systemd](/index.php/Systemd "Systemd") daemon that manages network configuration. It includes support for basic network configuration through [udev](/index.php/Udev "Udev"). The service is available with _systemd_ > 210.

NaN

*   **[Wicd](/index.php/Wicd "Wicd")** — Wireless and wired connection manager with few dependencies. Comes with an ncurses interface, and a GTK interface [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) is available.

NaN

### Web browsers

See also [Wikipedia:Comparison of web browsers](https://en.wikipedia.org/wiki/Comparison_of_web_browsers "wikipedia:Comparison of web browsers").

#### Console

*   **[ELinks](https://en.wikipedia.org/wiki/ELinks "wikipedia:ELinks")** — Advanced and well-established feature-rich text mode web browser (Links fork, barely supported since 2009).

NaN

*   **[Links](https://en.wikipedia.org/wiki/Links_(web_browser) "wikipedia:Links (web browser)")** — Text WWW browser. Includes a console version [links] similar to Lynx, and a graphical X-window/framebuffer version [links -g] (must be compiled in, Arch has both) with CSS, image rendering, pull-down menus.

NaN

*   **[Lynx](https://en.wikipedia.org/wiki/Lynx_(web_browser) "wikipedia:Lynx (web browser)")** — Text browser for the World Wide Web.

NaN

*   **retawq** — Interactive, multi-threaded network client (web browser) for text terminals.

NaN

*   **[w3m](https://en.wikipedia.org/wiki/W3m "wikipedia:W3m")** — Pager/text-based web browser. It has vim-like keybindings, and is able to display images. It has javascript support too.

NaN

#### Graphical

##### Gecko-based

See also [Wikipedia:Gecko (software)](https://en.wikipedia.org/wiki/Gecko_(software) "wikipedia:Gecko (software)").

*   **[Conkeror](https://en.wikipedia.org/wiki/Conkeror "wikipedia:Conkeror")** — Keyboard-based browser modeled after [Emacs](/index.php/Emacs "Emacs") using [XULRunner](https://en.wikipedia.org/wiki/XULRunner "wikipedia:XULRunner"). Customizable via JavaScript.

NaN

*   **[Firefox](/index.php/Firefox "Firefox")** — Extensible browser from Mozilla based on Gecko with fast rendering.

NaN

*   **Seamonkey** — Continuation of the Mozilla Internet Suite.

NaN

###### Firefox forks

**Warning:** The following browsers are third-party builds of Firefox. Please direct any support requests to their respective creators.

*   **[GNU IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat")** — Web browser distributed by the GNU Project, stripped of non-free components and with additional privacy extensions. Release cycle may be delayed compared to Mozilla Firefox.

NaN

*   **[Iceweasel](https://en.wikipedia.org/wiki/Mozilla_Corporation_software_rebranded_by_the_Debian_project#Iceweasel "wikipedia:Mozilla Corporation software rebranded by the Debian project")** — Fork of Firefox developed by Debian Linux. The main difference is that it does not include any trademarked Mozilla artwork. See [glandium](http://web.glandium.org/blog/?p=97) for more information on Iceweasel's existence.

NaN

*   **[Pale Moon](https://en.wikipedia.org/wiki/Pale_Moon_(web_browser) "wikipedia:Pale Moon (web browser)")** — Fork based on Firefox, using a Firefox 3+ interface through selective use of add-ons. Firefox add-ons may not be compatible. [[1]](https://addons.palemoon.org/firefox/incompatible/) Compiled for SSE2, with disabled optional code and no support for newer Firefox features such as cache2, e10s, and OTMC.

NaN

##### Blink-based

See also [Wikipedia:Blink (layout engine)](https://en.wikipedia.org/wiki/Blink_(layout_engine) "wikipedia:Blink (layout engine)").

*   **[Chromium](/index.php/Chromium "Chromium")** — Web browser developed by Google, the open source project behind Google Chrome.

NaN

*   **[Opera](/index.php/Opera "Opera")** — Highly customizable browser with focuses on an adherence to web rendering standards.

NaN

##### Webkit-based

See also [Wikipedia:Webkit](https://en.wikipedia.org/wiki/Webkit "wikipedia:Webkit").

*   **[Arora](https://en.wikipedia.org/wiki/Arora_(browser) "wikipedia:Arora (browser)")** — Cross-platform web browser built using QtWebKit. Development stopped in January 2012.

NaN

*   **[dwb](/index.php/Dwb "Dwb")** — Lightweight, highly customizable web browser based on the WebKit engine with _vi_-like shortcuts and tiling layouts. As of October 2014 _dwb_ is [unmaintained](https://bitbucket.org/portix/dwb/pull-request/22/several-cleanups-to-increase-portability/diff#comment-3217936).

NaN

*   **[GNOME Web](/index.php/GNOME_Web "GNOME Web")** — Browser which uses the WebKitGTK+ rendering engine, part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

NaN

*   **[Jumanji](/index.php/Jumanji "Jumanji")** — Highly customizable and functional web browser.

NaN

*   **[Luakit](/index.php/Luakit "Luakit")** — Highly configurable, micro-browser framework based on the WebKit engine and the GTK+ toolkit. It is very fast, extensible by Lua and licensed under the GNU GPLv3 license.

NaN

*   **Maxthon** — A browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier.

NaN

*   **[Midori](https://en.wikipedia.org/wiki/Midori_(web_browser) "wikipedia:Midori (web browser)")** — Lightweight web browser based on GTK+ and WebKit.

NaN

*   **Otter-browser** — Browser aiming to recreate classic Opera (12.x) UI using Qt5.

NaN

*   **[QupZilla](https://en.wikipedia.org/wiki/QupZilla "wikipedia:QupZilla")** — New and very fast open source browser based on WebKit core, written in Qt framework.

NaN

*   **[qutebrowser](/index.php/Qutebrowser "Qutebrowser")** — A keyboard-driven, [vim](/index.php/Vim "Vim")-like browser based on PyQt5 and QtWebKit.

NaN

*   **[Rekonq](https://en.wikipedia.org/wiki/Rekonq "wikipedia:Rekonq")** — WebKit-based web browser for KDE.

NaN

*   **Sb** — Very lightweight WebKit-based browser that uses keybindings to perform most things the URL bar would usually do.

NaN

*   **SlimBoat** — Fast, free secure and powerful web browser based on QtWebkit.

NaN

*   **Surf** — Lightweight WebKit-based browser, which follows the [suckless ideology](http://suckless.org/philosophy) (basically, the browser itself is a single C source file).

NaN

*   **[Uzbl](https://en.wikipedia.org/wiki/Uzbl "wikipedia:Uzbl")** — Group of web interface tools which adhere to the Unix philosophy.

NaN

*   **vimb** — Fast and lightweight vim like web browser based on the webkit web browser engine and the GTK toolkit.

NaN

*   **[Vimprobable](/index.php/Vimprobable "Vimprobable")** — Browser that behaves like the Vimperator plugin available for Mozilla Firefox. It is based on the WebKit engine and uses the GTK+ bindings.

NaN

*   **[Xombrero](https://en.wikipedia.org/wiki/Xombrero "wikipedia:Xombrero") (formerly known as _xxxterm_)** — Webkit minimalist web browser with sophisticated security features designed-in, BSD style.

NaN

*   **Brave** — At Brave, our goal is to block everything on the web that can cramp your style and compromise your privacy. Annoying ads are yesterday's news, and cookies stay in your jar where they belong. An open source browser created by the co-founder of Mozilla. Find more at [https://www.brave.com/](https://www.brave.com/)

NaN

##### Other

*   **[Abaco](https://en.wikipedia.org/wiki/Abaco_(web_browser) "wikipedia:Abaco (web browser)")** — Multi-page graphical web browser for the Plan 9 OS.

NaN

*   **[Dillo](https://en.wikipedia.org/wiki/Dillo "wikipedia:Dillo")** — Small, fast graphical web browser built on [FLTK](https://en.wikipedia.org/wiki/Fltk "wikipedia:Fltk").

NaN

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Web browser based on Qt and KHTML, part of [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/).

NaN

*   **[NetSurf](https://en.wikipedia.org/wiki/NetSurf "wikipedia:NetSurf")** — Featherweight browser written in C, notable for its slowly developing JavaScript support and fast rendering through its own custom rendering engine.

NaN

### File sharing

#### FTP

##### FTP clients

See also [Wikipedia:Comparison of FTP client software](https://en.wikipedia.org/wiki/Comparison_of_FTP_client_software "wikipedia:Comparison of FTP client software").

*   **[CurlFtpFS](/index.php/CurlFtpFS "CurlFtpFS")** — Filesystem for accessing FTP hosts; based on FUSE and libcurl.

NaN

*   **FatRat** — Download manager with support for HTTP, FTP, SFTP, BitTorrent, RapidShare and more.

NaN

*   **[FileZilla](https://en.wikipedia.org/wiki/FileZilla "wikipedia:FileZilla")** — Fast and reliable FTP, FTPS and SFTP client.

NaN

*   **[fuseftp](/index.php/FtpFs#Fuseftp "FtpFs")** — FTP filesystem written in Perl, using [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace").

NaN

*   **[gFTP](https://en.wikipedia.org/wiki/gFTP "wikipedia:gFTP")** — Multithreaded FTP client for Linux.

NaN

*   **[LFTP](https://en.wikipedia.org/wiki/Lftp "wikipedia:Lftp")** — Sophisticated command-line FTP client.

NaN

*   **LftpFS** — Read-only filesystem based on lftp (also supports HTTP, FISH, SFTP, HTTPS, FTPS and proxies).

NaN

*   **ncftp** — A set of free application programs implementing FTP.

NaN

*   **[tnftp](https://en.wikipedia.org/wiki/tnftp "wikipedia:tnftp")** — FTP client with several advanced features for [NetBSD](https://en.wikipedia.org/wiki/NetBSD "wikipedia:NetBSD").

NaN

Some file managers like Dolphin, [GNOME Files](/index.php/GNOME_Files "GNOME Files") and [Thunar](/index.php/Thunar "Thunar") also provide FTP functionality.

##### FTP servers

*   **bftpd** — Small, easy-to-configure FTP server

NaN

*   **[proFTPd](/index.php/Proftpd "Proftpd")** — A secure and configurable FTP server

NaN

*   **[Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")** — Free (BSD-licensed), secure, production-quality and standard-compliant FTP server.

NaN

*   **[vsftpd](/index.php/Vsftpd "Vsftpd")** — Lightweight, stable and secure FTP server for UNIX-like systems.

NaN

#### BitTorrent clients

See also [Wikipedia:Comparison of BitTorrent clients](https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients "wikipedia:Comparison of BitTorrent clients").

##### Console

###### Command line / backend

Can be used as-is via command line, but all have a choice of front-end options as well.

*   **[aria2](/index.php/Aria2 "Aria2")** — Lightweight download utility that supports simultaneous adaptive downloading via HTTP(S), FTP, BitTorrent (DHT, PEX, MSE/PE) protocols and Metalink. It can run as a daemon controlled via a built-in JSON-RPC or XML-RPC interface.

NaN

*   **Ctorrent** — CTorrent is a BitTorrent client implemented in C++ to be lightweight and quick.

NaN

*   **[MLDonkey](https://en.wikipedia.org/wiki/MLDonkey "wikipedia:MLDonkey")** — Multi-protocol P2P client that supports BitTorrent, HTTP, FTP, eDonkey and Direct Connect.

NaN

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with a daemon version, GTK+, Qt GUI, web and CLI front-ends.

NaN

###### Console Interface

*   **[rTorrent](/index.php/RTorrent "RTorrent")** — Simple and lightweight ncurses BitTorrent client. Requires [libtorrent](https://www.archlinux.org/packages/?name=libtorrent) backend.

NaN

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with a daemon version, ncurses CLI. Requires [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) backend.

NaN

##### Graphical Interface

###### libtorrent-rasterbar backend

*   **[Deluge](/index.php/Deluge "Deluge")** — User-friendly BitTorrent client written in PyGTK that can run as a daemon.

NaN

*   **FatRat** — Qt4 based download manager with support for HTTP, FTP, SFTP, BitTorrent, rapidshare and more. Written in C++.

NaN

*   **[qBittorrent](https://en.wikipedia.org/wiki/qBittorrent "wikipedia:qBittorrent")** — Open source (GPLv2) BitTorrent client that strongly resembles µtorrent.

NaN

*   **[Tribler](https://en.wikipedia.org/wiki/Tribler "wikipedia:Tribler")** — 4th generation file sharing system bittorrent client.

NaN

###### libktorrent backend

*   **[KGet](https://en.wikipedia.org/wiki/KGet "wikipedia:KGet")** — Download manager for KDE that supports HTTP(S), FTP and BitTorrent. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

NaN

*   **[Ktorrent](/index.php/Ktorrent "Ktorrent")** — Feature-rich BitTorrent client for KDE.

NaN

###### others

*   **Tixati** — P2P client that uses the BitTorrent protocol.

NaN

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with daemon version, GTK+, Qt GUI, web and CLI front-ends.

NaN

*   **[Vuze](https://en.wikipedia.org/wiki/Vuze "wikipedia:Vuze")** — Feature-rich BitTorrent client written in Java (formerly Azureus).

NaN

*   **Vuze Plus Extreme Mod** — A modded version of the Vuze BitTorrent client with multiple spoofing capabilities.

NaN

#### Other P2P networks

See also [Wikipedia:Comparison of eDonkey software](https://en.wikipedia.org/wiki/Comparison_of_eDonkey_software "wikipedia:Comparison of eDonkey software").

*   **[aMule](/index.php/AMule "AMule")** — Well-known eDonkey/Kad client with a daemon version and GTK+, web, and CLI front-ends.

NaN

*   **KaMule** — KDE graphical front-end for aMule.

NaN

*   **MlDonkey** — A multi-network P2P client.

NaN

*   **Sendanywhere** — GTK2 client for the cross platform P2P file sharing service, Sendanywhere. Allow users to send files of any type and size to other Android, iOS, and Desktop devices.

NaN

*   **[Sharelin](https://en.wikipedia.org/wiki/Sharelin "wikipedia:Sharelin")** — Gnutella2 only client with a web UI.

NaN

#### Video downloaders

*   **youtube-dl** — Download videos from YouTube and many other platforms.

NaN

*   **You-Get** — Dumb downloader that scrapes the web.

NaN

### Communication

#### Email clients

See also [Wikipedia:Comparison of e-mail clients](https://en.wikipedia.org/wiki/Comparison_of_e-mail_clients "wikipedia:Comparison of e-mail clients").

##### Console

*   **alot** — An experimental terminal MUA based on [notmuch mail](http://notmuchmail.org/). It is written in python using the [urwid](http://urwid.org/) toolkit.

NaN

*   **[Alpine](/index.php/Alpine "Alpine")** — Fast, easy-to-use and Apache-licensed email client based on [Pine](https://en.wikipedia.org/wiki/Pine_(email_client) "wikipedia:Pine (email client)").

NaN

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

NaN

*   **[S-nail](/index.php/S-nail "S-nail")** — a mail processing system with a command syntax reminiscent of _ed_ with lines replaced by messages. Provides the functionality of [mailx](https://en.wikipedia.org/wiki/mailx "wikipedia:mailx").

NaN

*   **mu/mu4e** — Email indexer (mu) and client for emacs (mu4e). Xapian based for fast searches.

NaN

*   **[Mutt](/index.php/Mutt "Mutt")** — Small but very powerful text-based mail client.

NaN

*   **[nmh](/index.php/Nmh "Nmh")** — A modular mail handling system.

NaN

*   **[notmuch](/index.php/Notmuch "Notmuch")** — A fast mail indexer built on top of _xapian_.

NaN

*   **[Sup](/index.php/Sup "Sup")** — CLI mail client with very fast searching, tagging, threading and GMail like operation.

NaN

*   **Wanderlust** — Email client and news reader for Emacs.

NaN

##### Graphical

*   **[Balsa](/index.php/Balsa "Balsa")** — Simple and light email client that is part of the Gnome project.

NaN

*   **[Claws Mail](https://en.wikipedia.org/wiki/Claws_Mail "wikipedia:Claws Mail")** — Lightweight GTK-based email client and news reader.

NaN

*   **[Evolution](/index.php/Evolution "Evolution")** — Mature and feature-rich e-mail client used in GNOME by default. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

NaN

*   **FossaMail** — FossaMail is a Mozilla Thunderbird-based mail, news and chat client by the Pale Moon developers.

NaN

*   **Geary** — Simple desktop mail client built in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

NaN

*   **[Kmail](https://en.wikipedia.org/wiki/Kmail "wikipedia:Kmail")** — Mature and feature-rich email client. Part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

NaN

*   **Manitou Mail** — Database-driven email system.

NaN

*   **N1** — A new mail client, built on the modern web and designed to be extended.

NaN

*   **Roundcubemail** — Browser-based multilingual IMAP client with a native application-like user interface.

NaN

*   **[Sylpheed](https://en.wikipedia.org/wiki/Sylpheed "wikipedia:Sylpheed")** — Lightweight and user-friendly GTK+ email client.

NaN

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Feature-rich email client from Mozilla written in GTK+.

NaN

*   **Trojitá** — Qt IMAP email client. Only supports one IMAP account.

NaN

#### Instant messaging

See also [Wikipedia:Comparison of instant messaging protocols](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_protocols "wikipedia:Comparison of instant messaging protocols").

This section lists all software with [instant messaging](https://en.wikipedia.org/wiki/Instant_messaging "wikipedia:Instant messaging") support. Particularly, that are client and server applications.

##### IRC clients

See also [Wikipedia:Comparison of Internet Relay Chat clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients "wikipedia:Comparison of Internet Relay Chat clients").

**Note:** Most web browsers and many IM clients also support IRC.

###### Console

*   **[BitchX](https://en.wikipedia.org/wiki/BitchX "wikipedia:BitchX")** — Console-based IRC client developed from the popular [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

NaN

*   **ERC** — Powerful, modular, and extensible IRC client for [Emacs](/index.php/Emacs "Emacs").

NaN

*   **[ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)")** — Featherweight IRC client, literally `tail -f` the conversation and `echo` back your replies to a file.

NaN

*   **Ircfs** — File system interface to IRC written in [Limbo](http://limbo.cat-v.org).

NaN

*   **[Irssi](/index.php/Irssi "Irssi")** — Highly-configurable ncurses-based IRC client.

NaN

*   **ScrollZ** — Advanced IRC client based on [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

NaN

*   **sic** — Extremely simple IRC client, similar to [ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)").

NaN

*   **[WeeChat](https://en.wikipedia.org/wiki/WeeChat "wikipedia:WeeChat")** — Modular, lightweight ncurses-based IRC client.

NaN

###### Graphical

*   **HexChat** — Fork of XChat for Linux and Windows.

NaN

*   **[Konversation](https://en.wikipedia.org/wiki/Konversation "wikipedia:Konversation")** — Qt-based IRC client for the KDE desktop.

NaN

*   **[KVIrc](https://en.wikipedia.org/wiki/KVIrc "wikipedia:KVIrc")** — Qt-based IRC client featuring extensive themes support.

NaN

*   **Loqui** — GTK+ IRC client with only one dependency: [GNet](https://wiki.gnome.org/Projects/GNetLibrary).

NaN

*   **LostIRC** — Simple GTK+ IRC client with tab-autocompletion, multiple server support, logging and others.

NaN

*   **pcw** — Frontend for [ii](http://tools.suckless.org/ii) that opens a new terminal for each channel.

NaN

*   **Polari** — Simple IRC client by the GNOME project.

NaN

*   **[Quassel](https://en.wikipedia.org/wiki/Quassel_IRC "wikipedia:Quassel IRC")** — Modern, cross-platform, distributed IRC client.

NaN

*   **[Smuxi](https://en.wikipedia.org/wiki/Smuxi "wikipedia:Smuxi")** — Cross-platform IRC client for the GNOME desktop inspired by [Irssi](/index.php/Irssi "Irssi").

NaN

*   **[XChat](https://en.wikipedia.org/wiki/XChat "wikipedia:XChat")** — GTK-based IRC client that works on both Linux and Windows.

NaN

##### XMPP (Jabber)

See also [Wikipedia:XMPP](https://en.wikipedia.org/wiki/XMPP "wikipedia:XMPP") and [Wikipedia:Comparison of instant messaging clients#XMPP-related features](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients#XMPP-related_features "wikipedia:Comparison of instant messaging clients").

###### Console clients

*   **Freetalk** — Console-based Jabber client.

NaN

*   **jabber.el** — Minimal Jabber client for [Emacs](/index.php/Emacs "Emacs").

NaN

*   **[MCabber](https://en.wikipedia.org/wiki/MCabber "wikipedia:MCabber")** — Small Jabber console client, includes features: SSL, PGP, MUC, OTR, and UTF8.

NaN

*   **Profanity** — A console based Jabber client inspired by Irssi.

NaN

*   **Poezio** — XMPP client with IRC feeling

NaN

###### Graphical clients

*   **[Gajim](https://en.wikipedia.org/wiki/Gajim "wikipedia:Gajim")** — Jabber client written in PyGTK.

NaN

*   **Jabbim** — Jabber client written in PyQt.

NaN

*   **[Psi](https://en.wikipedia.org/wiki/Psi_(instant_messaging_client) "wikipedia:Psi (instant messaging client)")** — Qt-based Jabber client which supports video conferencing (since version 0.13).

NaN

*   **Psi+** — Enhanced version of the Psi Jabber client with many new [features](http://psi-plus.com/wiki/en:features#differences_between_psi_beta_version_and_the_official_psi_015-dev_version).

NaN

*   **[Tkabber](https://en.wikipedia.org/wiki/Tkabber "wikipedia:Tkabber")** — Easy to hack feature-rich XMPP client by the author of the ejabberd XMPP server.

NaN

###### Servers

See also [Wikipedia:Comparison of XMPP server software](https://en.wikipedia.org/wiki/Comparison_of_XMPP_server_software "wikipedia:Comparison of XMPP server software").

*   **[Prosody](/index.php/Prosody "Prosody")** — An XMPP server written in the [Lua](http://www.lua.org/) programming language. Prosody is designed to be lightweight and highly extensible. It is licensed under a permissive [MIT license](http://prosody.im/source/mit).

NaN

*   **Ejabberd** — Jabber server written in Erlang

NaN

*   **[Jabberd2](/index.php/Jabberd2 "Jabberd2")** — An XMPP server written in the C language and licensed under the GNU General Public License. It was inspired by jabberd14.

NaN

*   **Openfire** — An XMPP IM multiplatform server written in Java

NaN

##### Multi-protocol clients

See also [Wikipedia:Comparison of instant messaging clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients").

**Note:** All messengers, that support several networks by means of direct connections to them, belong to this section.

Many clients listed here (including Pidgin and all its forks) support multiple IM networks via [libpurple](https://en.wikipedia.org/wiki/libpurple "wikipedia:libpurple"). The number of networks supported by these clients is very large but they (like any multiprotocol clients) usually have very limited or no support for network-specific features.

###### Console

*   **BarnOwl** — Ncurses-based chat client with support for the Zephyr, AIM, Jabber, IRC, and Twitter protocols.

NaN

*   **[Bitlbee](/index.php/Bitlbee "Bitlbee")** — IRC client that provides a gateway to popular chat networks (XMPP, MSN, Yahoo, AIM, ICQ and Twitter).

NaN

*   **[CenterIM](https://en.wikipedia.org/wiki/Centericq "wikipedia:Centericq")** — Fork of CenterICQ, a text mode menu- and window-driven IM interface.

NaN

*   **[Finch](/index.php/Pidgin "Pidgin")** — Ncurses-based chat client that uses libpurple and supports all its protocols.

NaN

*   **[naim](https://en.wikipedia.org/wiki/naim_(software) "wikipedia:naim (software)")** — Ncurses chat client with support for AOL, ICQ, IRC and the Lily CMC.

NaN

*   **pork** — Programmable, ncurses-based AIM and IRC client that mostly looks and feels like ircII.

NaN

*   **[Tox](/index.php/Tox "Tox")** — Tox is a distributed, secure messenger with audio and video chat capabilities.

NaN

###### Graphical

*   **Carrier** — Pidgin fork providing minor GUI enhancements (formerly FunPidgin).

NaN

*   **[Emesene](https://en.wikipedia.org/wiki/Emesene "wikipedia:Emesene")** — PyGTK instant messenger for the Windows Live Messenger network, also compatible with Jabber, Facebook and Google Talk.

NaN

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) "wikipedia:Empathy (software)")** — GNOME instant messaging client using the [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) "wikipedia:Telepathy (software)") framework.

NaN

*   **Galaxium Messenger** — Messenger application designed for the GNOME desktop.

NaN

*   **[Instantbird](https://en.wikipedia.org/wiki/Instantbird "wikipedia:Instantbird")** — Multi-protocol chat client using Mozilla's XUL and libpurple.

NaN

*   **[Kopete](https://en.wikipedia.org/wiki/Kopete "wikipedia:Kopete")** — User-friendly IM supporting AIM, ICQ, Windows Live Messenger, Yahoo, Jabber, Gadu-Gadu, Novell GroupWise Messenger, and other IM networks. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

NaN

*   **[KDE Telepathy](/index.php/KDE#KDE_Telepathy "KDE")** — KDE instant messaging client using the [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) "wikipedia:Telepathy (software)") framework. Meant as a replacement for Kopete.

NaN

*   **Licq** — Instant messaging client for UNIX supporting multiple protocols (currently ICQ, MSN and Jabber).

NaN

*   **Mikutter** — An open-source Twitter client using [GTK+](/index.php/GTK%2B "GTK+") and Ruby.

NaN

*   **[Pidgin](/index.php/Pidgin "Pidgin")** — Multi-protocol instant messaging client.

NaN

*   **qutIM** — Simple and user-friendly IM supporting ICQ, Jabber, Mail.Ru, IRC and VKontakte messaging.

NaN

##### Lan messengers

See also: [Comparison of LAN messengers](https://en.wikipedia.org/wiki/Comparison_of_LAN_messengers "wikipedia:Comparison of LAN messengers").

*   **iptux** — Lan communication software, compatible with IP Messenger.

NaN

#### VoIP / Softphone

See also [Wikipedia:Comparison of VoIP software](https://en.wikipedia.org/wiki/Comparison_of_VoIP_software "wikipedia:Comparison of VoIP software") and [Wikipedia:List of SIP software](https://en.wikipedia.org/wiki/List_of_SIP_software "wikipedia:List of SIP software").

##### Clients

**Note:** Some [IM clients](#Instant_messaging) also offer voice and video communication

###### SIP

*   **[Blink](https://en.wikipedia.org/wiki/Blink_(software) "wikipedia:Blink (software)")** — State of the art, easy to use SIP client.

NaN

*   **[Ekiga](https://en.wikipedia.org/wiki/Ekiga "wikipedia:Ekiga")** — VoIP and video conferencing application with full SIP and H.323 support (formerly known as GNOME Meeting).

NaN

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) "wikipedia:Empathy (software)")** — GNOME instant messenger client using the Telepathy framework with SIP support (using the Sofia-SIP library).

NaN

*   **[Jitsi](https://en.wikipedia.org/wiki/Jitsi "wikipedia:Jitsi")** — Audio/video SIP VoIP phone and instant messenger written in Java (formerly SIP-Communicator).

NaN

*   **[KPhone](https://en.wikipedia.org/wiki/KPhone "wikipedia:KPhone")** — Qt SIP User Agent with voice, video and text messaging support.

NaN

*   **[Linphone](https://en.wikipedia.org/wiki/Linphone "wikipedia:Linphone")** — VoIP phone application that allows you to to communicate freely with people over the internet, with voice, video, and text instant messaging.

NaN

*   **Minisip** — SIP User Agent with focus on security (supports TLS, end-to-end security, SRTP, MIKEY (DH, PSK, PKE)).

NaN

*   **[QuteCom](https://en.wikipedia.org/wiki/QuteCom "wikipedia:QuteCom")** — Softphone which allows you to make free PC to PC video and voice calls, and to integrate all your IM contacts in one place (formerly Wengo Phone).

NaN

*   **[Twinkle](https://en.wikipedia.org/wiki/Twinkle_(software) "wikipedia:Twinkle (software)")** — Qt softphone for VoIP and IM communication using SIP.

NaN

*   **[X-Lite](https://en.wikipedia.org/wiki/X-Lite "wikipedia:X-Lite")** — Proprietary freeware VoIP soft phone that uses SIP.

NaN

*   **[Zfone](https://en.wikipedia.org/wiki/Zfone "wikipedia:Zfone")** — Softphone application for secure voice communication over the Internet (VoIP), using the ZRTP protocol.

NaN

###### IAX2

*   **Kiax** — Qt-based IAX/2 Softphone.

NaN

###### Skype

*   **[Skype](/index.php/Skype "Skype")** — Popular but proprietary application for high-quality voice communication.

NaN

###### Other

*   **Hangups** — A third-party instant messaging client for Google Hangouts

NaN

*   **[Mumble](https://en.wikipedia.org/wiki/Mumble_(software) "wikipedia:Mumble (software)")** — Voice chat application similar to TeamSpeak.

NaN

*   **[TeamSpeak](/index.php/TeamSpeak "TeamSpeak")** — Proprietary VoIP application with gamers as its target audience.

NaN

###### Multi-protocol

*   **[SFLPhone](https://en.wikipedia.org/wiki/SFLphone "wikipedia:SFLphone")** — Open-source SIP/IAX2 compatible softphone with PulseAudio support.

NaN

##### Utilities

*   **Gladstone** — Educational ITU-T G.729 compliant codec with a GStreamer plugin.

NaN

*   **SIPp** — Open source test tool and traffic generator for the SIP protocol.

NaN

*   **Sipsak** — Small command-line tool for developers and administrators of SIP applications.

NaN

#### Speech recognition

See [Speech recognition#List of speech recognition applications](/index.php/Speech_recognition#List_of_speech_recognition_applications "Speech recognition").

### News, RSS, and blogs

#### News aggregators

See also [Wikipedia:Comparison of feed aggregators](https://en.wikipedia.org/wiki/Comparison_of_feed_aggregators "wikipedia:Comparison of feed aggregators").

##### Console

*   **[Canto](https://en.wikipedia.org/wiki/Canto_(news_aggregator) "wikipedia:Canto (news aggregator)")** — Ncurses RSS aggregator.

NaN

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

NaN

*   **Newsbeuter** — Ncurses RSS aggregator with layout and keybinding similar to the [Mutt](/index.php/Mutt "Mutt") email client.

NaN

*   **Rawdog** — "RSS Aggregator Without Delusions Of Grandeur" that parses RSS/CDF/Atom feeds into a static HTML page of articles in chronological order.

NaN

*   **Snownews** — Text mode RSS news reader.

NaN

##### Graphical

*   **[Akregator](https://en.wikipedia.org/wiki/Kontact#News_Feed_Aggregator "wikipedia:Kontact")** — News aggregator for KDE, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

NaN

*   **Blam** — Simple newsreader for GNOME written in C Sharp.

NaN

*   **[Liferea](https://en.wikipedia.org/wiki/Liferea "wikipedia:Liferea")** — GTK+ news aggregator for online news feeds and weblogs.

NaN

*   **RSS Guard** — Very tiny RSS and ATOM news reader developed using Qt framework.

NaN

*   **[RSSOwl](https://en.wikipedia.org/wiki/RSSOwl "wikipedia:RSSOwl")** — Powerful aggregator for RSS and Atom feeds, written in Java using Eclipse Rich Client Platform and SWT as a widget toolkit.

NaN

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Email client from Mozilla which also functions as a pretty nice news aggregator.

NaN

*   **Tickr (formerly News)** — GTK-based RSS Reader that displays feeds as a smooth scrolling line on your Desktop, as known from TV stations.

NaN

*   **Urssus** — Cross platform GUI news aggregator.

NaN

*   **QuiteRSS** — RSS/Atom feed reader written on Qt/С++.

NaN

#### Podcast clients

*   **gPodder** — A podcast client and feed aggregator (GTK+ and CLI interface).

NaN

*   **Greg** — A command-line podcast aggregator.

NaN

*   **Marrie** — A simple podcast client that runs on the Command Line Interface.

NaN

*   **PodCastXDL** — A simple podcast Downloader for the terminal.

NaN

*   **Vocal** — Simple Podcast Client for the Modern Desktop (GTK+).

NaN

#### Usenet newsreaders & newsgrabbers

Some [email clients](#Email_clients) also support NNTP. This section mainly lists NNTP-only client.

See also: [Wikipedia:List of Usenet newsreaders](https://en.wikipedia.org/wiki/List_of_Usenet_newsreaders "wikipedia:List of Usenet newsreaders"), [Wikipedia:Comparison of Usenet newsreaders](https://en.wikipedia.org/wiki/Comparison_of_Usenet_newsreaders "wikipedia:Comparison of Usenet newsreaders").

*   **lottanzb** — A _SABnzbd+_ (Usenet binary downloader) GUI front-end written in PyGTK

NaN

*   **nn** — Alternative more user-friendly(curses-based) Usenet newsreader for UNIX.

NaN

*   **[NZBGet](/index.php/NZBGet "NZBGet")** — CLI Utility to grab Usenet binary file using .nzb files.

NaN

*   **[pan](https://en.wikipedia.org/wiki/Pan_(newsreader) "wikipedia:Pan (newsreader)")** — A GTK2 Usenet newsreader that's good at both text and binaries.

NaN

*   **[slrn](https://en.wikipedia.org/wiki/slrn "wikipedia:slrn")** — An open source text-based news client.

NaN

*   **[tin](https://en.wikipedia.org/wiki/Tin_(newsreader) "wikipedia:Tin (newsreader)")** — A cross-platform threaded NNTP and spool based UseNet newsreader.

NaN

*   **trn** — A text-based Threaded Usenet newsreader.

NaN

*   **[XPN](https://en.wikipedia.org/wiki/XPN_(newsreader) "wikipedia:XPN (newsreader)")** — A graphical newsreader use PyGTK.

NaN

*   **xrn** — Usenet newsreader for X Window System.

NaN

#### Blog software

See also [Wikipedia:Blog software](https://en.wikipedia.org/wiki/Blog_software "wikipedia:Blog software") and [Wikipedia:List of content management systems](https://en.wikipedia.org/wiki/List_of_content_management_systems "wikipedia:List of content management systems").

*   **[Drupal](/index.php/Drupal "Drupal")** — An open source content management platform powering millions of websites and applications. It is built, used, and supported by an active and diverse community of people around the world.

NaN

*   **[Ghost](/index.php/Ghost "Ghost")** — Blogging platform written in JavaScript and distributed under the MIT License, designed to simplify the process of online publishing for individual bloggers as well as online publications.

NaN

*   **Hexo** — A fast, simple & powerful blog framework, powered by Node.js.

NaN

*   **[Jekyll](/index.php/Jekyll "Jekyll")** — A static blog engine, written in Ruby, which supports Markdown, textile and other formats.

NaN

*   **Nanoblogger** — A small weblog engine written in Bash for the command line. It uses common UNIX tools such as cat, grep, and sed to create static HTML content. It is not mantained anymore.

NaN

*   **Nikola** — A static site generator written in Python, with incremental rebuilds and multiple markup formats.

NaN

*   **Pelican** — A static site generator, powered by Python.

NaN

*   **[Wordpress](/index.php/Wordpress "Wordpress")** — An easy to setup and administer FLOSS content management system featuring a strong and vibrant community with thousands of plugins and themes.

NaN

#### Microblogging clients

See also [Wikipedia:List of Twitter services and applications](https://en.wikipedia.org/wiki/List_of_Twitter_services_and_applications "wikipedia:List of Twitter services and applications").

*   **Birdie** — A beautiful Twitter client for GNU/Linux, currently [under active development](http://www.birdieapp.eu/2014/10/26/birdie-2-status.html).

NaN

*   **Choqok** — Microblogging client for KDE that supports Twitter.com, Pump.io, GNU social and opendesktop.org services.

NaN

*   **Corebird** — Native Gtk+ Twitter client for the Linux desktop.

NaN

*   **[Gwibber](https://en.wikipedia.org/wiki/Gwibber "wikipedia:Gwibber")** — GTK-based microblogging client with support for Facebook, Identi.ca, Twitter, Flickr, Foursquare, Sina and Sohu.

NaN

*   **[Hotot](https://en.wikipedia.org/wiki/Hotot_(program) "wikipedia:Hotot (program)")** — Lightweight and open source microblogging client with support for Twitter and Identi.ca and integration with various image sharing services and URL shorteners [(discontinued)](http://hotot.org/).

NaN

*   **Pino** — Simple and fast client for Twitter and Identi.ca written in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

NaN

*   **Polly** — Linux Twitter client designed for multiple columns of multiple accounts.

NaN

*   **Pumpa** — Pump.io client written in C++ and Qt.

NaN

*   **Qwit** — Cross-platform client for Twitter using the Qt toolkit.

NaN

*   **ttytter** — Easily scriptable twitter client written in Perl.

NaN

*   **Turpial** — Multi-interface Twitter client written in Python.

NaN

*   **turses** — Twitter client for the console based off [tyrs](https://aur.archlinux.org/packages/tyrs/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tyrs)]</sup> with major improvements.

NaN

### Pastebin clients

See also [Wikipedia:Pastebin](https://en.wikipedia.org/wiki/Pastebin "wikipedia:Pastebin").

Pastebin services are often used to quote text or images while collaborating and troubleshooting. Pastebin clients provide a convenient way to post from the command line.

**Tip:** You can access the [ptpb.pw](https://ptpb.pw), [sprunge.us](http://sprunge.us/) and [ix.io](http://ix.io/) pastebins using curl. For example pipe the output of a command to ptpb: `_command_ | curl -F c=@- https://ptpb.pw ` or upload a file (including images): `curl -F c=@- https://ptpb.pw < _file_` 

**Note:** [pastebin.com](http://pastebin.com/) is blocked for some people and has a history of annoying issues (javascript, adverts, poor formatting, etc).

*   **codepad-git** — A [codepad.org](http://www.codepad.org) pastebin client written in python.

NaN

*   **Elmer** — Pastebin client similar to wgetpaste and curlpaste, except written in Perl and usable with wget or curl. Servers: [codepad.org](http://codepad.org/), [rafb.me](http://rafb.me/), [sprunge.us](http://sprunge.us/).

NaN

*   **Fb-client** — Client for the [paste.xinu.at](http://paste.xinu.at/) pastebin.

NaN

*   **Gist** — Command-line interface for the [gist.github.com](https://gist.github.com/) pastebin service.

NaN

*   **Haste** — Universal pastebin tool, written in Haskell. Servers: [hpaste.org](http://hpaste.org/), [paste2.org](http://paste2.org/), [pastebin.com](http://pastebin.com/) and others.

NaN

*   **Hg-paste** — Pastebin extension for Mercurial which can send diffs to various pastebin websites for easy sharing. Servers: [dpaste.com](http://dpaste.com/) and [dpaste.org](http://dpaste.org/).

NaN

*   **imgur** — A CLI client which can upload image to [imgur.com](http://imgur.com) image sharing service.

NaN

*   **Ix** — Client for the ix.io pastebin.

NaN

*   **Npaste-client** — Client for the [npaste.de](http://npaste.de/) pastebin.

NaN

*   **Pastebinit** — Really small Python script that acts as a Pastebin client. Servers: [pastie.org](http://pastie.org/), [paste.kde.org](http://paste.kde.org/), [paste.debian.net](http://paste.debian.net/), [paste.ubuntu.com](http://paste.ubuntu.com/) and others (for a full list see `pastebinit -l`).

NaN

*   **paste-binouse** — C++ standalone pastebin web server

NaN

*   **pb** — A very fast, lightweight pastebin and general file uploader written in python with a ton of features.

NaN

*   **ruby-haste** — Client for [hastebin.com](http://hastebin.com/).

NaN

*   **Uppity** — The pastebin client with an attitude.

NaN

*   **Vim-gist** — Vim script for [gist.github.com](https://gist.github.com/).

NaN

*   **Vim-paster** — Vim plugin to paste to any pastebin service using curl.

NaN

*   **Wgetpaste** — Bash script that automates pasting to a number of pastebin services. Servers: [pastebin.ca](http://pastebin.ca/), [codepad.org](http://codepad.org/), [dpaste.com](http://dpaste.com/) and [pastebin.osuosl.org](http://pastebin.osuosl.org/).

NaN

### Bitcoin

See the main article: [Bitcoin](/index.php/Bitcoin "Bitcoin").

*   **Armory** — Bitcoin client with features such as support for multiple wallets, importing keys and backups.

NaN

*   **[Bitcoin](/index.php/Bitcoin "Bitcoin")** — Official tool to manage Bitcoins, a P2P currency.

NaN

*   **Electrum** — An easy to use Bitcoin client.

NaN

*   **MultiBit** — A lightweight Bitcoin desktop client powered by the BitCoinJ library.

NaN

### Surveying

*   **[LimeSurvey](https://en.wikipedia.org/wiki/LimeSurvey "wikipedia:LimeSurvey")** — An open source on-line survey application. As a web server-based software it enables users to develop and publish on-line surveys, and collect responses, with no programming.

NaN

## Multimedia

### Codecs

See the main article: [Codecs](/index.php/Codecs "Codecs").

### Image

#### Image viewers

See also [Wikipedia:Comparison of image viewers](https://en.wikipedia.org/wiki/Comparison_of_image_viewers "wikipedia:Comparison of image viewers").

##### Console

*   **fbi** — Image viewer for the linux framebuffer console.

NaN

*   **fbv** — Very simple graphic file viewer for the framebuffer console.

NaN

*   **fim** — Highly customizable and scriptable framebuffer image viewer based on fbi.

NaN

*   **jfbview** — Framebuffer PDF and image viewer based on Imlib2\. Features include Vim-like controls, rotation and zoom, zoom-to-fit, and fast multi-threaded rendering.

NaN

##### Graphical

*   **[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")** — Image viewing and cataloging program, which is a part of the GNOME desktop environment.

NaN

*   **Eye of MATE** — Simple graphics viewer for the MATE desktop.

NaN

*   **[feh](/index.php/Feh "Feh")** — Fast, lightweight image viewer that uses imlib2.

NaN

*   **meh** — meh is a small, simple, super fast image viewer using raw XLib.

NaN

*   **GalaPix** — OpenGL-based image viewer for simultaneously viewing and zooming large collections of image files,

NaN

*   **[Geeqie](https://en.wikipedia.org/wiki/Geeqie "wikipedia:Geeqie")** — Image browser and viewer (fork of GQview) that adds additional functionality such as support for RAW files.

NaN

*   **Gimmage** — Gtkmm image viewer.

NaN

*   **GPicView** — Simple and fast image viewer for X, which is part of the [LXDE](/index.php/LXDE "LXDE") desktop.

NaN

*   **[GQview](https://en.wikipedia.org/wiki/GQview "wikipedia:GQview")** — Image browser that features single click access to view images and move around the directory tree

NaN

*   **[gThumb](https://en.wikipedia.org/wiki/GThumb "wikipedia:GThumb")** — Image viewer for the GNOME desktop.

NaN

*   **[Gwenview](https://en.wikipedia.org/wiki/Gwenview "wikipedia:Gwenview")** — Fast and easy to use image viewer for the KDE desktop.

NaN

*   **imv** — Lightweight image viewer with support for Wayland and animated GIFs.

NaN

*   **Mirage** — PyGTK image viewer featuring support for crop and resize, custom actions and a thumbnail panel.

NaN

*   **nomacs** — Free (GPLv3) Qt image viewer for many operating systems. It is feature-rich but starts fast and can be configured to show additional widgets or only the image.

NaN

*   **Phototonic** — Fast and functional image viewer and organizer (Qt).

NaN

*   **PhotoQt** — Fast and highly configurable image viewer with a simple and nice interface.

NaN

*   **[Picasa](https://en.wikipedia.org/wiki/Picasa "wikipedia:Picasa")** — Image organizer and viewer from Google that has editing capabilities and integration with the photo-sharing website.

NaN

*   **Quick Image Viewer** — Very small and fast image viewer based on GTK+ and imlib2.

NaN

*   **Ristretto** — Fast and lightweight image viewer for the Xfce desktop environment.

NaN

*   **Shotwell** — A digital photo organizer designed for the GNOME desktop environment

NaN

*   **[Simple Viewer GL](/index.php?title=Simple_Viewer_GL&action=edit&redlink=1 "Simple Viewer GL (page does not exist)")** — Simple image viewer using OpenGL, it has few dependencies.

NaN

*   **[sxiv](/index.php/Sxiv "Sxiv")** — Simple image viewer based on imlib2 that works well with tiling window managers.

NaN

*   **[Viewnior](https://en.wikipedia.org/wiki/Viewnior "wikipedia:Viewnior")** — Minimalistic GTK+ image viewer featuring support for flipping, rotating, animations and configurable mouse actions.

NaN

*   **Xloadimage** — Classic X image viewer.

NaN

*   **[XnView MP](https://en.wikipedia.org/wiki/XnView "wikipedia:XnView")** — Efficient image viewer, browser and converter.

NaN

*   **[xv](https://en.wikipedia.org/wiki/Xv_(software) "wikipedia:Xv (software)")** — Shareware program written by John Bradley to display and modify digital images under the X Window System.

NaN

#### Graphics and image manipulation

##### Raster editors

See also [Wikipedia:Comparison of raster graphics editors](https://en.wikipedia.org/wiki/Comparison_of_raster_graphics_editors "wikipedia:Comparison of raster graphics editors").

*   **AfterShot Pro** — Professional workflow and RAW conversion. Successor of Bibble Pro.

NaN

*   **AzPainter** — A Painting software.

NaN

*   **[darktable](https://en.wikipedia.org/wiki/darktable "wikipedia:darktable")** — Photography workflow and RAW development application.

NaN

*   **dcraw** — Converts many camera RAW formats.

NaN

*   **[digiKam](https://en.wikipedia.org/wiki/digiKam "wikipedia:digiKam")** — KDE-based image organizer with built-in editing features via a plugin architecture. digiKam asserts it is more full featured than similar applications with a larger set of image manipulation features including RAW image import and manipulation.

NaN

*   **[GIMP](https://en.wikipedia.org/wiki/GIMP "wikipedia:GIMP")** — Image editing suite in the vein of proprietary editors such as [Adobe Photoshop](https://en.wikipedia.org/wiki/Adobe_Photoshop "wikipedia:Adobe Photoshop"). GIMP ([GNU](/index.php/GNU "GNU") Image Manipulation Program) has been started in the mid 1990s and has acquired a large number of [plugins](/index.php/CMYK_support_in_The_GIMP "CMYK support in The GIMP") and additional tools.

NaN

*   **[Gpaint](https://en.wikipedia.org/wiki/GNU_Paint "wikipedia:GNU Paint")** — [Paintbrush](https://en.wikipedia.org/wiki/PC_Paintbrush "wikipedia:PC Paintbrush") clone for GNOME.

NaN

*   **[GraphicsMagick](https://en.wikipedia.org/wiki/GraphicsMagick "wikipedia:GraphicsMagick")** — Fork of ImageMagick designed to have API and command-line stability. It also supports multi-CPU for enhanced performance and thus is used by some large commercial sites (Flickr, etsy) for its performance.

NaN

*   **[ImageMagick](https://en.wikipedia.org/wiki/ImageMagick "wikipedia:ImageMagick")** — Command-line image manipulation program. It is known for its accurate format conversions with support for over 100 formats. Its API enables it to be scripted and it is usually used as a backend processor.

NaN

*   **[KolourPaint](https://en.wikipedia.org/wiki/KolourPaint "wikipedia:KolourPaint")** — Free raster graphics editor for KDE, similar to Microsoft's Paint application before Windows 7, but with some additional features such as support for transparency. Part of [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) and [kdegraphics](https://www.archlinux.org/groups/x86_64/kdegraphics/) groups.

NaN

*   **[Krita](https://en.wikipedia.org/wiki/Krita "wikipedia:Krita")** — Digital painting and illustration software included based on the KDE platform and Calligra libraries. Part of [calligra](https://www.archlinux.org/groups/x86_64/calligra/) group.

NaN

*   **Luminance HDR** — Open source graphical user interface application that aims to provide a workflow for HDR imaging.

NaN

*   **mtPaint** — Graphics editing program geared towards creating indexed palette images and pixel art.

NaN

*   **[MyPaint](https://en.wikipedia.org/wiki/MyPaint "wikipedia:MyPaint")** — Free software graphics application for digital painters.

NaN

*   **[Pinta](https://en.wikipedia.org/wiki/Pinta_(software) "wikipedia:Pinta (software)")** — Drawing and editing program modeled after [Paint.NET](https://en.wikipedia.org/wiki/Paint.net "wikipedia:Paint.net"). Its goal is to provide a simplified alternative to GIMP for casual users.

NaN

*   **[Shotwell](https://en.wikipedia.org/wiki/Shotwell_(software) "wikipedia:Shotwell (software)")** — Image organizer with a small set of image manipulation features (rotate, crop, color adjust, and red eye removal). It can import photos directly from digital cameras and export them to social media sites (Facebook, Flickr, Picasa Web Albums, etc.).

NaN

*   **[XPaint](https://en.wikipedia.org/wiki/XPaint "wikipedia:XPaint")** — Color image editing tool which features most standard paint program options.

NaN

##### Vector graphics - illustration

See also [Wikipedia:Comparison of vector graphics editors](https://en.wikipedia.org/wiki/Comparison_of_vector_graphics_editors "wikipedia:Comparison of vector graphics editors").

*   **[Asymptote](https://en.wikipedia.org/wiki/Asymptote_(vector_graphics_language) "wikipedia:Asymptote (vector graphics language)")** — A descriptive vector graphics language (like PGF/TikZ and Metapost) with a C-like syntax and LaTeX support.

NaN

*   **[Dia](https://en.wikipedia.org/wiki/Dia_(software) "wikipedia:Dia (software)")** — GTK+-based diagram creation program.

NaN

*   **[Graphviz](https://en.wikipedia.org/wiki/Graphviz "wikipedia:Graphviz")** — Set of tools for drawing graphs in the descriptive DOT language.

NaN

*   **[Inkscape](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")** — Vector graphics editor, with capabilities similar to [Illustrator](https://en.wikipedia.org/wiki/Adobe_Illustrator "wikipedia:Adobe Illustrator"), [CorelDraw](https://en.wikipedia.org/wiki/CorelDRAW "wikipedia:CorelDRAW"), or [Xara X](https://en.wikipedia.org/wiki/Xara_X "wikipedia:Xara X"), using the SVG (Scalable Vector Graphics) file format. Inkscape supports many advanced SVG features (markers, clones, alpha blending, etc.) and great care is taken in designing a streamlined interface. It is very easy to edit nodes, perform complex path operations, trace bitmaps and much more. It's developers also aim to maintain a thriving user and developer community by using open, community-oriented development.

NaN

*   **[Karbon](https://en.wikipedia.org/wiki/Karbon_(software) "wikipedia:Karbon (software)")** — Vector graphics editor, part of the Calligra Suite. Part of [calligra](https://www.archlinux.org/groups/x86_64/calligra/) group.

NaN

*   **[Pencil Project](https://en.wikipedia.org/wiki/Pencil2D "wikipedia:Pencil2D")** — An open-source GUI prototyping and mockup tool.

NaN

*   **[sK1](https://en.wikipedia.org/wiki/SK1_(program) "wikipedia:SK1 (program)")** — Replacement for Adobe Illustrator or CorelDraw, oriented for "prepress ready" PostScript & PDF output.

NaN

*   **[Xara LX](https://en.wikipedia.org/wiki/Xara_Xtreme_LX "wikipedia:Xara Xtreme LX")** — Advanced vector graphics program, the open source version of the commercial Xara X.

NaN

*   **[yEd](https://en.wikipedia.org/wiki/yEd "wikipedia:yEd")** — General-purpose diagramming program for flowcharts, network diagrams, UML diagrams, BPMN diagrams, mind maps, organization charts, and Entity Relationship diagrams.

NaN

##### Vector graphics - CAD

See also [Wikipedia:List of computer-aided design editors](https://en.wikipedia.org/wiki/List_of_computer-aided_design_editors "wikipedia:List of computer-aided design editors").

*   **[BRL-CAD](https://en.wikipedia.org/wiki/BRL-CAD "wikipedia:BRL-CAD")** — Constructive solid geometry (CSG) solid modeling computer-aided design (CAD) system that includes an interactive geometry editor, ray tracing support for graphics rendering and geometric analysis, computer network distributed framebuffer support, scripting, image-processing and signal-processing tools.

NaN

*   **[DraftSight](https://en.wikipedia.org/wiki/DraftSight "wikipedia:DraftSight")** — Dassault Systemes' freeware 2D CAD application. DraftSight allows users to access DWG/DXF files, regardless of which CAD software was originally used to create them.

NaN

*   **[FreeCAD](https://en.wikipedia.org/wiki/FreeCAD "wikipedia:FreeCAD")** — CAD/CAE program, based on OpenCascade, Qt and Python with features such as macro recording, workbenches and the ability to run as server.

NaN

*   **LeoCAD** — CAD program for creating virtual LEGO models. It has an easy to use interface and currently includes over 6000 different pieces created by the LDraw community.

NaN

*   **[LibreCAD](https://en.wikipedia.org/wiki/LibreCAD "wikipedia:LibreCAD")** — Powerful 2D CAD application based on Qt. It has been forked from QCad Community Edition.

NaN

*   **[OpenSCAD](https://en.wikipedia.org/wiki/OpenSCAD "wikipedia:OpenSCAD")** — Open source 2D/3D CAD using programmers approach.

NaN

*   **[QCAD](https://en.wikipedia.org/wiki/QCad "wikipedia:QCad")** — Powerful 2D CAD application that began in 1999\. QCaD includes DFX standard file format and supports HPGL format.

NaN

*   **[VariCAD](https://en.wikipedia.org/wiki/VariCAD "wikipedia:VariCAD")** — 3D/2D CAD and mechanical engineering application which provides support for parameters and geometric constraints, tools for shells, pipelines, sheet metal unbending and crash tests, assembly support, mechanical part and symbol libraries, calculations, bills of materials, and more.

NaN

##### 3D modeling/rendering

See also [Wikipedia:Comparison of 3D computer graphics software](https://en.wikipedia.org/wiki/Comparison_of_3D_computer_graphics_software "wikipedia:Comparison of 3D computer graphics software").

*   **[Art of Illusion](https://en.wikipedia.org/wiki/Art_of_Illusion "wikipedia:Art of Illusion")** — 3D modeling and rendering studio written in Java.

NaN

*   **[Blender](https://en.wikipedia.org/wiki/Blender_(software) "wikipedia:Blender (software)")** — fully integrated 3D graphics creation suite capable of 3D modeling, texturing, and animation, among other things.

NaN

*   **[MakeHuman™](https://en.wikipedia.org/wiki/MakeHuman "wikipedia:MakeHuman")** — Parametrical modeling program for creating human bodies.

NaN

*   **[POV-Ray](https://en.wikipedia.org/wiki/POV-Ray "wikipedia:POV-Ray")** — Script-based raytracer for creating 3D graphics.

NaN

*   **[Wings 3D](https://en.wikipedia.org/wiki/Wings3d "wikipedia:Wings3d")** — Advanced subdivision modeler that is both powerful and easy to use.

NaN

#### Screen capture

See also: [Taking a screenshot](/index.php/Taking_a_screenshot "Taking a screenshot").

### Audio

#### Audio systems

See the main article: [Sound system](/index.php/Sound_system "Sound system").

See also [Wikipedia:Sound server](https://en.wikipedia.org/wiki/Sound_server "wikipedia:Sound server").

*   **wineasio** — Provides an ASIO to JACK driver for _wine_. ASIO is the most common Windows low-latency driver, so is commonly used in audio workstation programs.

NaN

#### Audio players

See also [Wikipedia:Comparison of audio player software](https://en.wikipedia.org/wiki/Comparison_of_audio_player_software "wikipedia:Comparison of audio player software").

##### Music player daemons and clients

See also: [List of MPD clients](/index.php/Music_Player_Daemon#Clients "Music Player Daemon")

*   **[Music Player Daemon](/index.php/Music_Player_Daemon "Music Player Daemon")** — Lightweight and scalable choice for music management.

NaN

*   **[XMMS2](https://en.wikipedia.org/wiki/XMMS2 "wikipedia:XMMS2")** — Complete rewrite of the popular music player.

NaN

##### Command-line players

*   **[cmus](/index.php/Cmus "Cmus")** — Very feature-rich ncurses-based music player.

NaN

*   **Cplay** — Curses front-end for various audio players (ogg123, mpg123, mpg321, splay, madplay, and mikmod, xmp, and sox).

NaN

*   **Herrie** — Minimalistic console-based music player with native AudioScrobbler support.

NaN

*   **[MOC](/index.php/Moc "Moc")** — Ncurses console audio player with support for the MP3, OGG, and WAV formats.

NaN

*   **MPFC** — Gstreamer-based audio player with curses interface.

NaN

*   **[mpg123](https://en.wikipedia.org/wiki/Mpg123 "wikipedia:Mpg123")** — Fast free MP3 console audio player for Linux, FreeBSD, Solaris, HP-UX and nearly all other UNIX systems (also decodes MP1 and MP2 files).

NaN

*   **mps-youtube** — Terminal based YouTube jukebox with playlist management. Plays audio/video through mplayer/mpv.

NaN

*   **pancake** — Cli pandora client built with urwid.

NaN

*   **[pianobar](/index.php/Pianobar "Pianobar")** — Console-based frontend for Pandora.

NaN

*   **shell-fm** — Console-based player for the streams provided by [last.fm](http://www.last.fm/).

NaN

*   **[VLC](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Highly portable multimedia player with ncurses interface module, and multimedia framework capable of reading most audio and video formats as well as DVDs, Audio CDs, VCDs, and various streaming protocols.

NaN

*   **whistle** — a curses-based commandline audio player.

NaN

##### GUI players

*   **[Amarok](/index.php/Amarok "Amarok")** — Mature Qt-based player known for its plethora of features.

NaN

*   **[aTunes](https://en.wikipedia.org/wiki/aTunes "wikipedia:aTunes")** — Audio player written in Java.

NaN

*   **[Audacious](/index.php/Audacious "Audacious")** — [Winamp](https://en.wikipedia.org/wiki/Winamp "wikipedia:Winamp") clone like Beep and old XMMS versions.

NaN

*   **[Banshee](https://en.wikipedia.org/wiki/Banshee_(media_player) "wikipedia:Banshee (media player)")** — [iTunes](https://en.wikipedia.org/wiki/iTunes "wikipedia:iTunes") clone, built with GTK+ and [Mono](/index.php/Mono "Mono"), feature-rich and more actively developed.

NaN

*   **[Clementine](https://en.wikipedia.org/wiki/Clementine_(software) "wikipedia:Clementine (software)")** — Amarok 1.4 clone, ported to Qt 4.

NaN

*   **Cuberok** — Music player and collection manager with a lightweight interface.

NaN

*   **DeaDBeeF** — Light and fast music player with many features, no GNOME or KDE dependencies, supports console-only, as well as a GTK+ GUI, comes with many plugins, and has a metadata editor.

NaN

*   **[Exaile](/index.php/Exaile "Exaile")** — GTK+ clone of Amarok.

NaN

*   **gmusicbrowser** — Open-source jukebox for large collections of MP3/OGG/FLAC files.

NaN

*   **GNOME Music** — Music is the new GNOME music playing application. It aims to combine an elegant and immersive browsing experience with simple and straightforward controls.

NaN

*   **Goggles Music Manager** — Music collection manager and player that automatically categorizes your music, supports gapless playback, features easy tag editing, and internet radio support. Uses the [Fox toolkit](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit").

NaN

*   **Guayadeque** — Full featured media player that can easily manage large collections and uses the GStreamer media framework.

NaN

*   **[JuK](https://en.wikipedia.org/wiki/JuK "wikipedia:JuK")** — JuK is an audio jukebox application, supporting collections of MP3, Ogg Vorbis, and FLAC audio files.

NaN

*   **Listen** — Listen is a Music player and management for GNOME written in python.

NaN

*   **LXMusic** — A minimalist xmms2-based music player.

NaN

*   **Miam-player** — Cross-platform open source music player.

NaN

*   **[Nightingale](https://en.wikipedia.org/wiki/Nightingale_(software) "wikipedia:Nightingale (software)")** — Open source clone of iTunes-based on [Songbird](https://en.wikipedia.org/wiki/Songbird_(software) "wikipedia:Songbird (software)"), that uses Mozilla technologies and the GStreamer framework.

NaN

*   **Noise** — Simple, fast, and good looking music player.

NaN

*   **Nuvola Player** — Integrated Google Music, 8tracks and Hype Machine player.

NaN

*   **Potamus** — Lightweight, intuitive GTK+ audio player with an emphasis on high audio quality.

NaN

*   **Pragha** — GTK+ music manager. (fork of the Consonance Music Manager)

NaN

*   **Qmmp** — Qt-based multimedia player with a user interface that is similar to Winamp or XMMS.

NaN

*   **[Quod Libet](https://en.wikipedia.org/wiki/Quod_Libet_(software) "wikipedia:Quod Libet (software)")** — Audio player written with PyGTK and GStreamer with support for regular expressions in playlists.

NaN

*   **[Rhythmbox](https://en.wikipedia.org/wiki/Rhythmbox "wikipedia:Rhythmbox")** — GTK+ clone of iTunes, used by default in GNOME.

NaN

*   **[Spotify](/index.php/Spotify "Spotify")** — Proprietary music streaming service. It supports local playback and streaming from Spotify's vast library (requires a free account).

NaN

*   **[SpotCommander](/index.php/SpotCommander "SpotCommander")** — A remote control for Spotify, optimized for mobile devices. It works on any device with a modern browser, and it's free and open source.

NaN

*   **Tomahawk** — Music player application written in C++/Qt. It decouples the name of the song from the source it was shared from - and fulfills the request using all of your available sources.

NaN

*   **[VLC](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Highly portable multimedia player and multimedia framework capable of reading most audio and video formats as well as DVDs, Audio CDs, VCDs, and various streaming protocols.

NaN

*   **[XMMS](https://en.wikipedia.org/wiki/XMMS "wikipedia:XMMS")** — Skinnable GTK+ standalone media player similar to Winamp.

NaN

#### Volume managers

*   **GVolWheel** — An audio mixer which lets you control the volume through a tray icon.

NaN

*   **GVTray** — A master volume mixer for the system tray.

NaN

*   **pa-applet** — PulseAudio system tray applet with volume bar.

NaN

*   **PNMixer** — A fork of Obmixer. It has many new features such as ALSA channel selection, connect/disconnect detection, shortcuts, etc.

NaN

*   **[Volnoti](/index.php/Volnoti "Volnoti")** — A lightweight volume notification daemon for GNU/Linux and other POSIX operating systems.

NaN

*   **Volti** — A GTK application for controlling audio volume from system tray with an internal mixer and support for multimedia keys that uses only ALSA.

NaN

*   **VolumeIcon** — Another volume control for your system tray with channel selection, themes and an external mixer.

NaN

*   **VolWheel** — A little application which lets you control the sound volume easily through a tray icon you can scroll on.

NaN

#### CD ripping

See [Optical disc drive#CD](/index.php/Optical_disc_drive#CD "Optical disc drive").

#### Visualization

*   **[ProjectM](https://en.wikipedia.org/wiki/MilkDrop "wikipedia:MilkDrop")** — Music visualizer which uses 3D accelerated iterative image-based rendering.

NaN

*   **[VSXu](https://en.wikipedia.org/wiki/VSXu "wikipedia:VSXu")** — Free to use program that lets you create and perform real-time audio visual presets.

NaN

#### Audio tag editors

*   **Audio Tag Tool** — Tool to edit tags in MP3 and Ogg Vorbis files.

NaN

*   **Cowbell** — Elegant music organizer that supports many audio formats including MP3, Ogg/FLAC, and MusePack.

NaN

*   **[EasyTag](https://en.wikipedia.org/wiki/EasyTag "wikipedia:EasyTag")** — Utility for viewing, editing and writing ID3 tags of music files, supports many audio formats.

NaN

*   **[Ex Falso](https://en.wikipedia.org/wiki/Ex_Falso_(software) "wikipedia:Ex Falso (software)")** — Cross-platform free and open source audio tag editor and library organizer.

NaN

*   **ID3 Mass Tagger** — Command-line utility to edit ID3 1.x and 2.x tags.

NaN

*   **Kid3** — MP3, Ogg/Vorbis, FLAC, MPC, MP4/AAC, MP2, Speex, TrueAudio, WavPack, WMA, WAV and AIFF files tag editor.

NaN

*   **MP3Info** — MP3 technical info viewer and ID3 1.x tag editor.

NaN

*   **[MusicBrainz Picard](https://en.wikipedia.org/wiki/MusicBrainz_Picard "wikipedia:MusicBrainz Picard")** — Cross-platform audio tag editor written in Python (the official MusicBrainz tagger).

NaN

*   **[Puddletag](https://en.wikipedia.org/wiki/Puddletag "wikipedia:Puddletag")** — Replacement for the famous MP3tag for Windows.

NaN

*   **taffy** — Simple command-line tag editor for many audio formats.

NaN

*   **Tag Editor** — A tag editor with Qt 5 GUI and command-line interface supporting MP4/AAC (iTunes), ID3v1, ID3v2, Ogg/Vorbis and Matroska.

NaN

*   **Qoobar** — Universal QT-based audio tagger (specialized for classical music)

NaN

#### Sound editing

*   **[Ardour](https://en.wikipedia.org/wiki/Ardour_(software) "wikipedia:Ardour (software)")** — Multichannel hard disk recorder and digital audio workstation.

NaN

*   **[Audacity](https://en.wikipedia.org/wiki/Audacity_(audio_editor) "wikipedia:Audacity (audio editor)")** — Program that lets you manipulate digital audio waveforms.

NaN

*   **GNOME Sound Recorder** — The Sound Recorder application enables you to record and play .flac, .ogg (OGG audio, or .oga), and .wav sound files.

NaN

*   **[Jokosher](https://en.wikipedia.org/wiki/Jokosher "wikipedia:Jokosher")** — Non-linear multi-track digital audio editor that is being developed in Python, using the GTK+ interface and GStreamer as an audio back-end.

NaN

*   **KWave** — Sound editor for KDE.

NaN

*   **[LMMS](/index.php/LMMS "LMMS")** — The Linux MultiMedia Studio. Free cross-platform software which allows you to produce music with your computer.

NaN

*   **[Qtractor](https://en.wikipedia.org/wiki/Qtractor "wikipedia:Qtractor")** — Qt-based hard disk recorder and digital audio workstation application that aims to provide digital audio workstation software simple enough for the average home user, and yet powerful enough for the professional user.

NaN

*   **[Rosegarden](https://en.wikipedia.org/wiki/Rosegarden "wikipedia:Rosegarden")** — Digital audio workstation program developed with ALSA and Qt that acts as an audio and MIDI sequencer, scorewriter and musical composition and editing tool.

NaN

*   **XCFA** — Tool to extract the contens of audio CDs and convert them to various formats.

NaN

### Mobile phone managers

*   **gnokii** — Tools and user space driver for use with mobile phones.

NaN

*   **GNOME Phone Manager** — Control your mobile phone from your GNOME desktop.

NaN

*   **KDE Connect** — A project that aims to communicate all your devices.

NaN

*   **Moto4Lin** — File manager and seem editor for Motorola P2K phones (like C380/C650).

NaN

### Video

#### Video players

See also [Wikipedia:Comparison of video player software](https://en.wikipedia.org/wiki/Comparison_of_video_player_software "wikipedia:Comparison of video player software").

##### Console

*   **[MPlayer](/index.php/MPlayer "MPlayer")** — Video player that supports a complete and versatile array of video and audio formats.

NaN

*   **[mpv](/index.php/Mpv "Mpv")** — Movie player based on MPlayer and mplayer2.

NaN

*   **[xine-ui](https://en.wikipedia.org/wiki/xine "wikipedia:xine")** — Free multimedia player.

NaN

*   **[VLC ncurses](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Command-line version of the famous video player that can play smoothly high definition videos in the TTY.

NaN

##### Graphical

See also: [MPlayer#Frontends/GUIs](/index.php/MPlayer#Frontends.2FGUIs "MPlayer"), [mpv#Front ends](/index.php/Mpv#Front_ends "Mpv").

*   **[Dragon Player](https://en.wikipedia.org/wiki/Kdemultimedia#Dragon_Player "wikipedia:Kdemultimedia")** — Simple video player for KDE. Part of the [kdemultimedia](https://www.archlinux.org/groups/x86_64/kdemultimedia/) group.

NaN

*   **[Kaffeine](https://en.wikipedia.org/wiki/Kaffeine "wikipedia:Kaffeine")** — Very versatile KDE media player that, by default, utilizes Xine as its backend and has excellent support of digital TV (DVB).

NaN

*   **Parole** — Modern media player based on the GStreamer framework.

NaN

*   **Rage** — Video and audio player written with Enlightenment Foundation Libraries with some extra bells and whistles.

NaN

*   **Snappy** — Powerful media player with a minimalistic interface.

NaN

*   **[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")** — Media player (audio and video) for the GNOME desktop that uses GStreamer. Part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

NaN

*   **[VLC media player](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Middleweight video player with support for a wide variety of audio and video formats.

NaN

*   **Whaaw! Media Player** — Lightweight GStreamer-based audio and video player that can serve as a good alternative to Totem for those who do not like all of those GNOME dependencies.

NaN

*   **Xnoise** — GTK+ and GStreamer-based media player for both audio and video with "a slick GUI, great speed and lots of features." (development ceased)

NaN

*   **QMPlay2** — QMPlay2 is a QT based video player. It can play and stream all formats supported by ffmpeg and libmodplug. It has on integrated module system, which includes a Youtube browser.

NaN

#### Subtitles

*   **Gaupol** — Full-featured subtitle editor.

NaN

*   **Penguin Subtitle Player** — Penguin Subtitle Player is an open-source, cross-platform standalone subtitle player, as an alternative to Greenfish Subtitle Player, SrtViewer (Mac), SRTPlayer, JustSubsPlayer and Free Subtitle Player.

NaN

*   **subdl** — Automatic subtitle downloader.

NaN

*   **SubtitlesPrinter** — Print subtitles above a X-screen, independently of the video player.

NaN

#### DVD ripping

See [Optical disc drive#DVD_2](/index.php/Optical_disc_drive#DVD_2 "Optical disc drive").

#### Video editors

See also [Wikipedia:Comparison of video editing software](https://en.wikipedia.org/wiki/Comparison_of_video_editing_software "wikipedia:Comparison of video editing software").

##### Console

*   **[Avidemux](https://en.wikipedia.org/wiki/Avidemux "wikipedia:Avidemux")** — Free video editor designed for simple cutting, filtering and encoding tasks.

NaN

*   **[FFmpeg](/index.php/FFmpeg "FFmpeg")** — Complete, cross-platform solution to record, convert and stream audio and video.

NaN

*   **HandBrake-CLI** — Simple yet powerful video transcoder ideal for batch mkv/x264 ripping.

NaN

##### Graphical

*   **[Avidemux](https://en.wikipedia.org/wiki/Avidemux "wikipedia:Avidemux")** — Free video editor designed for simple cutting, filtering and encoding tasks.

NaN

*   **[Cinelerra (Community Version)](https://en.wikipedia.org/wiki/Cinelerra "wikipedia:Cinelerra")** — Professional video editing and compositing environment.

NaN

*   **HandBrake** — Simple yet powerful video transcoder ideal for batch mkv/x264 ripping. GTK+ version.

NaN

*   **[Kdenlive](https://en.wikipedia.org/wiki/Kdenlive "wikipedia:Kdenlive")** — Non-linear video editor designed for basic to semi-professional work.

NaN

*   **[Lightworks](https://en.wikipedia.org/wiki/Lightworks "wikipedia:Lightworks")** — A proprietary professional non-linear editing system for editing and mastering digital video in various formats.

NaN

*   **[LiVES](https://en.wikipedia.org/wiki/LiVES "wikipedia:LiVES")** — Video editor and VJ (live performance) platform.

NaN

*   **[Open Shot](https://en.wikipedia.org/wiki/OpenShot_Video_Editor "wikipedia:OpenShot Video Editor")** — Non-linear video editor based on MLT framework.

NaN

*   **[PiTiVi](https://en.wikipedia.org/wiki/Pitivi "wikipedia:Pitivi")** — Video editor designed to be intuitive and integrate well in the GNOME desktop.

NaN

*   **[Shotcut](https://en.wikipedia.org/wiki/Shotcut "wikipedia:Shotcut")** — Shotcut is a free, open source, cross-platform video editor.

NaN

*   **Transmageddon** — Simple python application for transcoding video into formats supported by GStreamer.

NaN

#### Screencast

See also [Wikipedia:Comparison of screencasting software](https://en.wikipedia.org/wiki/Comparison_of_screencasting_software "wikipedia:Comparison of screencasting software").

Screencast utilities allow you to create a video of your desktop or individual windows.

*   **byzanz** — Simple screencast tool that produces GIF animations.

NaN

*   **glc** — Screencast tool that can capture the sound and video from OpenGL applications, such as games, where regular X11 screencast tools produce choppy results.

NaN

*   **Istanbul** — Simple desktop session recorder that produces ogg videos.

NaN

*   **Kazam** — Screencasting program with design in mind.

NaN

*   **OBS** — Free and open source software for video recording and live streaming.

NaN

*   **[RecordMyDesktop](https://en.wikipedia.org/wiki/RecordMyDesktop "wikipedia:RecordMyDesktop")** — An easy to use utility that records your desktop into the ogg format with a CLI, Qt or GTK+ interface.

NaN

*   **simplescreenrecorder** — A feature-rich screen recorder written in C++/Qt4 that supports X11 and OpenGL.

NaN

*   **vokoscreen** — Simple screencast tool, GUI ffmpeg.

NaN

*   **[XVidCap](https://en.wikipedia.org/wiki/XVidCap "wikipedia:XVidCap")** — Application used for recording a screencast or digital recording of an X Window System screen output with an audio narration.

NaN

*   **FFcast** — FFmpeg-based screencast tool written in Bash.

NaN

### Optical media burning

See [Optical disc drive#Burning CD/DVD/BD with a GUI](/index.php/Optical_disc_drive#Burning_CD.2FDVD.2FBD_with_a_GUI "Optical disc drive").

### Podcasts

see [Podcast clients](/index.php/List_of_applications/Internet#Podcast_clients "List of applications/Internet")

### Collection managers

*   **[Beets](/index.php/Beets "Beets")** — Music library organizer, tagger and more.

NaN

*   **Demlo** — Batch music tagger, encoder, renamer and more.

NaN

*   **[GCstar](https://en.wikipedia.org/wiki/GCstar "wikipedia:GCstar")** — GNOME application for organizing various collections (board games, comic books, movies, stamps, etc.).

NaN

*   **[Kodi](/index.php/Kodi "Kodi")** — Application for organizing various collections and automatically retrieving info about them (video, music, photos).

NaN

*   **[Tellico](https://en.wikipedia.org/wiki/Tellico "wikipedia:Tellico")** — KDE application for organizing various collections (books, video, music, coins, etc.).

NaN

### Lyrics fetchers

*   **clyrics** — An extensible lyrics fetcher, with daemon support for cmus and mocp.

NaN

## Utilities

### Partitioning tools

See [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").

### Mount tools

*   **9mount** — Mount 9p filesystems.

NaN

*   **cryptmount** — Mount an encrypted file system as a regular user.

NaN

*   **ldm** — A lightweight daemon that mounts drives automagically using _udev_

NaN

*   **pmount** — Mount _source_ as a regular user to an automatically created destination `/media/_source_name_`.

NaN

*   **pmount-safe-removal** — Mount removable devices as regular user with safe removal

NaN

*   **udevil** — Mounts removable devices as a regular user, show device info, and monitor device changes. Only depends on _udev_ and glib.

NaN

*   **ws** — Mount Windows network shares ([CIFS](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") and [VFS](https://en.wikipedia.org/wiki/Virtual_file_system "wikipedia:Virtual file system")).

NaN

#### Udisks

*   **bashmount** — A bash script to mount and manage removable media as a regular user with udisks.

NaN

*   **udiskie** — Automatic disk mounting service using _udisks_

NaN

*   **udisks_functions** — Bash functions and aliases for _udisks2_

NaN

*   **udisksvm** — GUI _udisks_ wrapper for removable media

NaN

### Basic shell commands

*   **[Core utilities](/index.php/Core_utilities "Core utilities")** — The basic file, shell and text manipulation utilities of the GNU operating system

NaN

### Integrated development environments

See also [Wikipedia:Comparison of integrated development environments](https://en.wikipedia.org/wiki/Comparison_of_integrated_development_environments "wikipedia:Comparison of integrated development environments").

*   **[Anjuta](https://en.wikipedia.org/wiki/Anjuta "wikipedia:Anjuta")** — Versatile IDE with project management, an application wizard, an interactive debugger, a source editor, version control support and many more tools.

NaN

*   **[Aptana Studio](https://en.wikipedia.org/wiki/Aptana#Aptana_Studio "wikipedia:Aptana")** — IDE based on Eclipse, but geared towards web development, with support for HTML, CSS, Javascript, Ruby on Rails, PHP, Adobe AIR and others.

NaN

*   **[Bluefish](https://en.wikipedia.org/wiki/Bluefish_(text_editor) "wikipedia:Bluefish (text editor)")** — GTK+ editor/IDE with an MDI interface, syntax highlighting and support for Python plugins.

NaN

*   **[Bluej](https://en.wikipedia.org/wiki/Bluej "wikipedia:Bluej")** — Fully featured Java IDE used mainly for educational and beginner purposes.

NaN

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "wikipedia:Brackets (text editor)")** — A free open-source editor written in HTML, CSS, and Javascript with a primary focus on Web Development. It was created by Adobe Systems, licensed under the MIT License, and is currently maintained on GitHub.

NaN

*   **[Builder](https://en.wikipedia.org/wiki/GNOME_Builder "wikipedia:GNOME Builder")** — General purpose IDE for GNOME.

NaN

*   **[Code::Blocks](https://en.wikipedia.org/wiki/Code::Blocks "wikipedia:Code::Blocks")** — Open source and cross-platform C/C++ IDE.

NaN

*   **[Cloud9](https://en.wikipedia.org/wiki/Cloud9_IDE "wikipedia:Cloud9 IDE")** — State-of-the-art IDE that runs in your browser and lives in the cloud, allowing you to run, debug and deploy applications from anywhere, anytime.

NaN

*   **[Eclipse](/index.php/Eclipse "Eclipse")** — Open source community project, which aims to provide a universal development platform.

NaN

*   **[Editra](https://en.wikipedia.org/wiki/Editra "wikipedia:Editra")** — Multi-platform text editor with an implementation that focuses on creating an easy to use interface and features that aid in code development.

NaN

*   **[Eric](https://en.wikipedia.org/wiki/Eric_Python_IDE "wikipedia:Eric Python IDE")** — Full-featured Python 3.x and Ruby IDE in PyQt4.

NaN

*   **[Gambas](/index.php/Gambas "Gambas")** — Free development environment based on a Basic interpreter with object extensions.

NaN

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — Text editor using the GTK+ toolkit with basic features of an integrated development environment.

NaN

*   **IEP** — Cross-platform Python IDE focused on interactivity and introspection, which makes it very suitable for scientific computing.

NaN

*   **[IntelliJ IDEA](https://en.wikipedia.org/wiki/IntelliJ_IDEA "wikipedia:IntelliJ IDEA")** — IDE for Java, Groovy and other programming languages with advanced refactoring features.

NaN

*   **[KDevelop](https://en.wikipedia.org/wiki/KDevelop "wikipedia:KDevelop")** — Feature-full, plugin extensible IDE for C/C++ and other programming languages.

NaN

*   **[Komodo Edit](https://en.wikipedia.org/wiki/Komodo_Edit "wikipedia:Komodo Edit")** — A free, multi-language editor.

NaN

*   **[Lazarus](https://en.wikipedia.org/wiki/Lazarus_(IDE) "wikipedia:Lazarus (IDE)")** — Cross-platform IDE for Object Pascal.

NaN

*   **LiteIDE** — A simple, open source, cross-platform Go IDE.

NaN

*   **MonkeyStudio** — Monkey Studio (MkS) is a cross platform IDE written in C++/Qt 4\. Syntax highlighting for more than 22 programming languages.

NaN

*   **[MonoDevelop](https://en.wikipedia.org/wiki/MonoDevelop "wikipedia:MonoDevelop")** — Cross-platform IDE targeted for the Mono and .NET frameworks.

NaN

*   **[MPLAB](https://en.wikipedia.org/wiki/MPLAB "wikipedia:MPLAB")** — IDE for Microchip PIC and dsPIC development

NaN

*   **[NetBeans](/index.php/Netbeans "Netbeans")** — Integrated development environment (IDE) for developing with Java, JavaScript, PHP, Python, Ruby, Groovy, C, C++, Scala, Clojure, and other languages.

NaN

*   **[Ninja-IDE](https://en.wikipedia.org/wiki/Ninja-IDE "wikipedia:Ninja-IDE")** — from the recursive acronym: "Ninja-IDE Is Not Just Another IDE", is a cross-platform integrated development environment (IDE); runs on Linux/X11, Mac OS X and Windows OSs. Used, for example, for Python development

NaN

*   **[PHPStorm](/index.php/PHPStorm "PHPStorm")** — JetBrains PhpStorm is a commercial, cross-platform IDE for PHP built on JetBrains' IntelliJ IDEA platform, providing an editor for PHP, HTML and JavaScript with on-the-fly code analysis, error prevention and automated refactorings for PHP and JavaScript code.

NaN

*   **[PyCharm](https://en.wikipedia.org/wiki/PyCharm "wikipedia:PyCharm")** — IDE used for programming in Python with support for code analysis, debugging, unit testing, version control and web development with Django.

NaN

*   **[QDevelop](https://en.wikipedia.org/wiki/QDevelop "wikipedia:QDevelop")** — Free and cross-platform IDE for Qt.

NaN

*   **[Qt Creator](https://en.wikipedia.org/wiki/Qt_Creator "wikipedia:Qt Creator")** — Lightweight, cross-platform C++ integrated development environment with a focus on Qt.

NaN

*   **[Scratch](https://en.wikipedia.org/wiki/Scratch_(programming_language) "wikipedia:Scratch (programming language)")** — A multimedia authoring tool for educational and entertainment purposes, such as creating interactive projects and simple sprite-based games. It is used primarly by unskilled users (such as children) as an entry to [event-driven programming](https://en.wikipedia.org/wiki/Event-driven_programming "wikipedia:Event-driven programming"). _Scratch_ is free software under GPL v2 and [Scratch Source Code License](http://wiki.scratch.mit.edu/wiki/Scratch_Source_Code_License).

NaN

*   **[Spyder](https://en.wikipedia.org/wiki/Spyder_(software) "wikipedia:Spyder (software)")** — Scientific PYthon Development EnviRonment providing MATLAB-like features.

NaN

### Build automation

See also [Wikipedia:List of build automation software](https://en.wikipedia.org/wiki/List_of_build_automation_software "wikipedia:List of build automation software").

*   **Apache Ant** — Java library and command-line tool whose mission is to drive processes described in build files as targets and extension points dependent upon each other.

NaN

*   **Apache Maven** — Software project management and comprehension tool.

NaN

*   **Gradle** — Powerful build system for the JVM.

NaN

### Terminal emulators

See also [Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators").

Power users use terminal emulators quite often, so unsurprisingly lots of X11 terminal emulators exist. Most of them emulate Xterm that emulates VT102, which emulates typewriter, so you will have to read the [Wikipedia article](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") and [other sources](https://google.com/search?q=linux+terminal+emulators) to get a hold on these things.

*   **[aterm](https://en.wikipedia.org/wiki/aterm "wikipedia:aterm")** — Xterm replacement with transparency support. It has been deprecated in favour of urxvt since 2008.

NaN

*   **Eterm** — Terminal emulator intended as a replacement for xterm and designed for the [Enlightenment](/index.php/Enlightenment "Enlightenment") desktop.

NaN

*   **Final Term** — A new breed of terminal emulator. Project is dead.

NaN

*   **Gate One** — Web-based terminal emulator and SSH client.

NaN

*   **[Konsole](https://en.wikipedia.org/wiki/Konsole "wikipedia:Konsole")** — Terminal emulator included in the [KDE](/index.php/KDE "KDE") desktop.

NaN

*   **mlterm** — A multi-lingual terminal emulator supporting various character sets and encodings in the world.

NaN

*   **[Mrxvt](https://en.wikipedia.org/wiki/mrxvt "wikipedia:mrxvt")** — Tabbed X terminal emulator based on rxvt.

NaN

*   **QTerminal** — A lightweight Qt-based terminal emulator.

NaN

*   **[rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt")** — Popular replacement for the xterm.

NaN

*   **[st](/index.php/St "St")** — Simple terminal implementation for X.

NaN

*   **Terminal** — A terminal emulator, that supports multiple windows, scroll buffer and all the expected features. A part of GNUstep.

NaN

*   **[terminator](/index.php/Terminator "Terminator")** — Terminal emulator supporting multiple resizable terminal panels.

NaN

*   **Terminology** — Terminal emulator by the Enlightenment project team with innovative features: file thumbnails and media play like a media player.

NaN

*   **[Tilda](/index.php/Tilda "Tilda")** — Terminal inspired by many classic terminals from first person shooter games such as Quake, Doom and Half-Life.

NaN

*   **[urxvt](/index.php/Urxvt "Urxvt")** — Highly extendable (with Perl) unicode enabled rxvt-clone terminal emulator featuring tabbing, url launching, a Quake style drop-down mode and pseudo-transparency.

NaN

*   **[xterm](/index.php/Xterm "Xterm")** — Simple terminal emulator for the X Window System. It provides DEC VT102 and Tektronix 4014 compatible terminals for programs that can't use the window system directly.

NaN

*   **[Yakuake](https://en.wikipedia.org/wiki/Yakuake "wikipedia:Yakuake")** — Drop-down terminal (Quake style) emulator based on Konsole.

NaN

#### VTE-based

[VTE](http://developer.gnome.org/vte/unstable/) (Virtual Terminal Emulator) is a widget developed during early GNOME days for use in the GNOME Terminal. It has since given birth to many terminals with similar capabilities.

*   **evilvte** — Very lightweight and highly customizable terminal emulator with support for tabs, auto-hiding and different encodings.

NaN

*   **Germinal** — Minimalist terminal emulator which provides a borderless maximized terminal, attached to a tmux session by default, hence providing tabs and panels.

NaN

*   **[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")** — A terminal emulator included in the [GNOME](/index.php/GNOME "GNOME") desktop with support for Unicode and pseudo-transparency.

NaN

*   **[Guake](/index.php/Guake "Guake")** — Drop-down terminal for the GNOME desktop.

NaN

*   **Terra** — is a GTK+3.0 based terminal emulator with useful user interface, it also supports multiple terminals with splitting screen horizontally or vertically -- (similar to guake).

NaN

*   **[LilyTerm](/index.php/LilyTerm "LilyTerm")** — Very light and easy to use X Terminal Emulator

NaN

*   **LXTerminal** — Desktop independent terminal emulator for [LXDE](/index.php/LXDE "LXDE").

NaN

*   **MATE terminal** — A fork of [Wikipedia:GNOME terminal](https://en.wikipedia.org/wiki/GNOME_terminal "wikipedia:GNOME terminal") for the [MATE](/index.php/MATE "MATE") desktop.

NaN

*   **Pantheon Terminal** — A super lightweight, beautiful, and simple terminal emulator. It's designed to be setup with sane defaults and little to no configuration.

NaN

*   **ROXTerm** — Tabbed terminal emulator with a small footprint.

NaN

*   **sakura** — Terminal emulator based on GTK+ and VTE.

NaN

*   **Stjerm** — GTK+-based drop-down terminal emulator that provides a minimalistic interface combined with a small file size, lightweight memory usage and easy integration with composite window managers such as Compiz.

NaN

*   **[Terminal](https://en.wikipedia.org/wiki/Terminal_(Xfce) "wikipedia:Terminal (Xfce)")** — Terminal emulator included in the [Xfce](/index.php/Xfce "Xfce") desktop with support for a colorized prompt and a tabbed interface.

NaN

*   **Terminix** — A tiling terminal emulator for Linux using GTK+ 3

NaN

*   **Termit** — Simple terminal emulator based on the vte library that includes tabs, bookmarks, and the ability to switch encodings.

NaN

*   **[Termite](/index.php/Termite "Termite")** — A keyboard-centric VTE-based terminal, aimed at use within a window manager with tiling and/or tabbing support.

NaN

*   **tinyterm** — Very lightweight terminal emulator based on VTE.

NaN

#### KMS-based

The following terminal emulators are based on the [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") that could be invoked without X.

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — A KMS/DRM-based system console(getty) with an integrated terminal emulator for Linux operating systems.

NaN

#### framebuffer-based

In GNU/Linux world, the [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") could be refered to a virtual device in the Linux kernel (**fbdev**) or the virtual framebuffer system for X (**xvfb**). This section mainly lists the terminal emulators that based on the in-kernel virtual device, i.e. **fbdev**.

*   **[fbterm](/index.php/Fbterm "Fbterm")** — A fast framebuffer-based terminal emulator with many amazing features. Development stopped.

NaN

*   **yaft** — A simple terminal emulator for living without X, with UCS2 glyphs, wallpaper and 256color support.

NaN

### Files

#### File managers

See also [Wikipedia:Comparison of file managers](https://en.wikipedia.org/wiki/Comparison_of_file_managers "wikipedia:Comparison of file managers").

##### Console

*   **Clex** — File manager with full-screen user interface

NaN

*   **[Dired](https://en.wikipedia.org/wiki/Dired "wikipedia:Dired")** — Directory editor integrated with [Emacs](/index.php/Emacs "Emacs").

NaN

*   **dired** — Ancient DIRectory EDitor since 1980.

NaN

*   **[Midnight Commander](/index.php/Midnight_Commander "Midnight Commander")** — Console-based, dual-paneled file manager.

NaN

*   **nffm** — "Nothing Fancy File Manager", a mouseless ncurses file manager written in C.

NaN

*   **Pilot** — File manager that comes with the [Alpine](/index.php/Alpine "Alpine") email client.

NaN

*   **[Ranger](/index.php/Ranger "Ranger")** — Console-based file manager with vi bindings, customizability, and lots of features.

NaN

*   **[Vifm](/index.php/Vifm "Vifm")** — Ncurses-based two-panel file manager with vi-like keybindings.

NaN

##### Graphical

*   **Andromeda** — Qt-based cross-platform file manager.

NaN

*   **Caja** — The file manager for the MATE desktop.

NaN

*   **Dino** — Easy to use and powerful file manager built in Qt.

NaN

*   **[Dolphin](/index.php/Dolphin "Dolphin")** — File manager included in the KDE4 desktop.

NaN

*   **Double Commander** — File manager with two panels side by side. It is inspired by Total Commander and features some new ideas.

NaN

*   **[emelFM2](https://en.wikipedia.org/wiki/emelFM2 "wikipedia:emelFM2")** — File manager that implements the popular two-panel design.

NaN

*   **Gentoo** — A lightweight file manager for GTK.

NaN

*   **[GNOME Commander](https://en.wikipedia.org/wiki/GNOME_Commander "wikipedia:GNOME Commander")** — A dual-paned file manager for the GNOME Desktop.

NaN

*   **[GNOME Files](/index.php/GNOME_Files "GNOME Files")** — Extensible, heavyweight file manager used by default in GNOME with support for custom scripts.

NaN

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — File manager and web browser for the KDE desktop.

NaN

*   **[Krusader](https://en.wikipedia.org/wiki/Krusader "wikipedia:Krusader")** — Advanced twin panel (Midnight Commander style) file manager for the KDE desktop.

NaN

*   **muCommander** — A lightweight, cross-platform file manager with a dual-pane interface written in Java.

NaN

*   **[Nemo](/index.php/Nemo "Nemo")** — Nemo is the file manager of the Cinnamon desktop. A good alternative to Nautilus.

NaN

*   **[PathFinder](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit")** — File browser that comes with the FOX toolkit.

NaN

*   **[PCManFM](/index.php/PCManFM "PCManFM")** — Lightweight file manager which features tabbed and dual pane browsing; also it can optionally manage the desktop icons and background.

NaN

*   **QtFileMan** — File manager similar to PCManFM from LXDE.

NaN

*   **qtFM** — Small, lightweight filemanager for Linux desktops based on pure Qt.

NaN

*   **ROX** — Small and fast file manager which can optionally manage the desktop background and panels.

NaN

*   **[SpaceFM](/index.php/SpaceFM "SpaceFM")** — GTK+ multi-panel tabbed file manager.

NaN

*   **Sunflower** — Small and highly customizable twin-panel file manager for Linux with support for plugins.

NaN

*   **[Thunar](/index.php/Thunar "Thunar")** — File manager that can be run as a daemon with excellent start up and directory load times.

NaN

*   **Tux Commander** — Windowed file manager with two panels side by side similar to popular Total Commander or Midnight Commander file managers.

NaN

*   **Worker** — Fast, lightweight and feature-rich file manager for the X Window System.

NaN

*   **[Xfe](https://en.wikipedia.org/wiki/Xfe "wikipedia:Xfe")** — Microsoft Explorer-like file manager for X (X File Explorer).

NaN

#### Desktop search engines

See also [Wikipedia:List of search engines#Desktop search engines](https://en.wikipedia.org/wiki/List_of_search_engines#Desktop_search_engines "wikipedia:List of search engines").

*   **Baloo** — KDE's file indexing and search solution

NaN

*   **Catfish** — Versatile file searching tool

NaN

*   **Docfetcher** — A java open source desktop search application

NaN

*   **Gnome Search Tool** — Default Gnome utility to search for files

NaN

*   **Gnome Search Tool No Nautilus** — _gnome-search-tool_ to search for files without [GNOME Files](/index.php/GNOME_Files "GNOME Files") or _gnome-desktop_

NaN

*   **Pinot** — Personal search and metasearch tool

NaN

*   **Recoll** — Full text search tool based on Xapian backend

NaN

*   **Searchmonkey** — A powerful GUI search utility for matching regex patterns

NaN

*   **[Strigi](https://en.wikipedia.org/wiki/Strigi "wikipedia:Strigi")** — Fast crawling desktop search engine with a Qt GUI.

NaN

*   **[Tracker](https://en.wikipedia.org/wiki/Tracker_(search_software) "wikipedia:Tracker (search software)")** — All-in-one indexer, search tool and metadata database.

NaN

#### Archiving and compression tools

See also [Wikipedia:Comparison of file archivers](https://en.wikipedia.org/wiki/Comparison_of_file_archivers "wikipedia:Comparison of file archivers").

##### Console

*   **atool** — Script for managing file archives of various types.

NaN

*   **arj** — An archiver that formerly used on DOS/Windows in mid-1990s. This is an open source clone.

NaN

*   **[cpio](https://en.wikipedia.org/wiki/cpio "wikipedia:cpio")** — GNU tool supporting cpio and tar file archive formats.

NaN

*   **[dar](https://en.wikipedia.org/wiki/Dar_(disk_archiver) "wikipedia:Dar (disk archiver)")** — An archiving and compression utility avoiding the drawbacks of tar

NaN

*   **lha** — Archiver to create LH-7 format archives. 32-bit only (require multilib on x86_64).

NaN

*   **lrzip** — Multi-threaded compressor using the rzip/lzma, lzo, and zpaq algorithms.

NaN

*   **lz4** — A file compressor using lz4 - An extremely fast compression algorithm.

NaN

*   **lzop** — Fast file compressor using lzo lib.

NaN

*   **[p7zip](/index.php/P7zip "P7zip")** — Port of 7-Zip for POSIX systems, including Linux. The commandline tool is called **7z**.

NaN

*   **pixz** — A multi-threaded and indexed compressor that avoiding the drawbacks of xz.

NaN

*   **[tar](/index.php/Tar "Tar")** — GNU utility for manipulating the ubiquitous tar archives (tarballs).

NaN

*   **[zpaq](https://en.wikipedia.org/wiki/ZPAQ "wikipedia:ZPAQ")** — A high compression ratio archiver written in C++. Powered by Context-Model, LZ77 and BWT algorithm.

NaN

*   **zopfli** — High compress ratio file compressor from Google, using a deflate-compatible algorithm called zopfli.

NaN

*   **zoo** — Rarely used archiver that was mostly used in VMS world before PKZIP became popular.

NaN

##### Graphical

*   **[Ark](https://en.wikipedia.org/wiki/Ark_(software) "wikipedia:Ark (software)")** — Archiving tool included in the KDE desktop.

NaN

*   **Engrampa** — Archive manager for [MATE](/index.php/MATE "MATE")

NaN

*   **[File Roller](https://en.wikipedia.org/wiki/File_Roller "wikipedia:File Roller")** — Archive manager included in the GNOME desktop.

NaN

*   **FreeArc** — General-purpose archiver written in haskell, comes with a GTK2 gui. Currently only available on 32-bit platform. (Requires multilib on x86_64)

NaN

*   **[PeaZip](https://en.wikipedia.org/wiki/PeaZip "wikipedia:PeaZip")** — Open source file and archive manager.

NaN

*   **Squeeze** — Featherweight front-end for commandline archiving tools.

NaN

*   **Xarchive** — Generic GTK2 front-end that uses external wrappers around commandline archiving tools.

NaN

*   **[Xarchiver](https://en.wikipedia.org/wiki/Xarchiver "wikipedia:Xarchiver")** — Lightweight desktop independent archive manager built with GTK+.

NaN

#### Comparison, diff, merge

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Pacnew and Pacsave files#Managing .pacnew files](/index.php/Pacnew_and_Pacsave_files#Managing_.pacnew_files "Pacnew and Pacsave files").**

**Notes:** There's only a list of tools, and it must be in **List of applications** (Discuss in [Talk:List of applications#](https://wiki.archlinux.org/index.php/Talk:List_of_applications))

See also [Wikipedia:Comparison of file comparison tools](https://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools "wikipedia:Comparison of file comparison tools").

*   **colordiff** — A Perl script wrapper for 'diff' that produces the same output but with pretty 'syntax' highlighting.

NaN

*   **Diffuse** — Small and simple text merge tool written in Python.

NaN

*   **KDiff3** — File and directory diff and merge tool for the KDE desktop.

NaN

*   **[Kompare](https://en.wikipedia.org/wiki/Kompare "wikipedia:Kompare")** — GUI front-end program for viewing and merging differences between source files. It supports a variety of diff formats and provides many options to customize the information level displayed.

NaN

*   **[Meld](https://en.wikipedia.org/wiki/Meld_(software) "wikipedia:Meld (software)")** — Visual diff and merge tool that can compare files, directories, and version controlled projects.

NaN

*   **xxdiff** — A graphical browser for file and directory differences.

NaN

[Vim](/index.php/Vim "Vim") and [Emacs](/index.php/Emacs "Emacs") provide merge functionality with [vimdiff](/index.php/Vim#Merging_files_.28vimdiff.29 "Vim") and `ediff`.

#### Batch renamers

*   **[GPRename](https://en.wikipedia.org/wiki/GPRename "wikipedia:GPRename")** — GTK+ batch renamer for files and directories.

NaN

*   **[KRename](https://en.wikipedia.org/wiki/KRename "wikipedia:KRename")** — Very powerful batch file renamer for the KDE desktop.

NaN

*   **metamorphose2** — wxPython based batch renamer with support for regular expressions, renaming multimedia files according to their metadata, etc.

NaN

*   **pyRenamer** — Application for the mass renaming of files.

NaN

*   **rename.pl** — Batch renamer based on perl regex.

NaN

### Disk cleaning

*   **[BleachBit](https://en.wikipedia.org/wiki/BleachBit "wikipedia:BleachBit")** — It frees disk space and guards your privacy; frees cache, deletes cookies, clears Internet history, shreds temporary files, deletes logs, and discards junk you didn't know was there.

NaN

*   **gconf-cleaner** — cleans up the unknown/invalid gconf keys that still sitting down on your gconf database

NaN

### Disk usage display

*   **[Disk Usage Analyzer](https://en.wikipedia.org/wiki/Disk_Usage_Analyzer "wikipedia:Disk Usage Analyzer") (Baobab)** — Disk usage analyzer for the [GNOME](/index.php/GNOME "GNOME") desktop.

NaN

*   **[Filelight](https://en.wikipedia.org/wiki/Filelight "wikipedia:Filelight")** — Disk usage analyzer that creates an interactive map of concentric, segmented rings that help visualise disk usage on your computer.

NaN

*   **GdMap** — Disk usage analyzer that draws a map of rectangles sized according to file or dir sizes.

NaN

*   **gt5** — Diff-capable "du-browser".

NaN

*   **ncdu** — Simple ncurses disk usage analyzer.

NaN

### Clock synchronization

*   **[NTPd](/index.php/NTPd "NTPd")** — Network Time Protocol reference implementation.

NaN

*   **[Chrony](/index.php/Chrony "Chrony")** — Lightweight NTP client and server.

NaN

*   **[OpenNTPD](/index.php/OpenNTPD "OpenNTPD")** — Free, easy to use implementation of the Network Time Protocol.

NaN

### System monitoring

*   **adesklet SystemMonitor** — Collection of modular stackable system monitors for [adesklets](https://en.wikipedia.org/wiki/Adesklets "wikipedia:Adesklets").

NaN

*   **candybar** — WebKit-based status line for tiling window managers.

NaN

*   **[Conky](/index.php/Conky "Conky")** — Lightweight, scriptable system monitor.

NaN

*   **Collectd** — A simple, extensible system monitoring daemon based on [rrdtool](http://oss.oetiker.ch/rrdtool/). It has a small footprint and can be set up either stand-alone or as a server/client application.

NaN

*   **dstat** — Versatile resource statistics tool.

NaN

*   **[GKrellM](https://en.wikipedia.org/wiki/GKrellM "wikipedia:GKrellM")** — Simple, flexible system monitor package for [GTK+](/index.php/GTK%2B "GTK+") with many plug-ins.

NaN

*   **gnome-system-monitor** — A system monitor for [GNOME](/index.php/GNOME "GNOME").

NaN

*   **[htop](https://en.wikipedia.org/wiki/Htop "wikipedia:Htop")** — Simple, ncurses interactive process viewer.

NaN

*   **[KSysGuard](https://en.wikipedia.org/wiki/KDE_System_Guard "wikipedia:KDE System Guard")** — Also known as KSysguard, is the [KDE](/index.php/KDE "KDE") task manager and performance monitor.

NaN

*   **linux process explorer** — Graphical process explorer for Linux.

NaN

*   **LXTask** — Lightweight task manager for [LXDE](/index.php/LXDE "LXDE").

NaN

*   **mate-system-monitor** — A GTK2 system monitor for [MATE](/index.php/MATE "MATE").

NaN

*   **Task Manager** — GTK2 process mangement application for [Xfce](/index.php/Xfce "Xfce").

NaN

*   **[Paramano](/index.php/Paramano "Paramano")** — A light battery monitor and a CPU frequency scaler. Forked from trayfreq

NaN

*   **Sysstat** — A collection of resource monitoring tools: iostat, isag, mpstat, pidstat, sadf, sar.

NaN

### System information viewers

#### Console

*   **alsi** — A system information tool for Arch Linux. It can be configured for every other system without even touching the source code of the script.

NaN

*   **archey2** — Simple python script that displays the arch logo and some basic information. Python 2.x version.

NaN

*   **archey3-git** — Python script to display system infomation alongside the Arch Linux logo.

NaN

*   **dmidecode** — It reports information about your system's hardware as described in your system BIOS according to the SMBIOS/DMI standard.

NaN

*   **hwdetect** — Simple script to list modules that are exported by /sys, a part of [archboot](/index.php/Archboot "Archboot").

NaN

*   **hwinfo** — Powerful hardware detection tool come from openSUSE.

NaN

*   **inxi** — A script to get system information.

NaN

*   **screenfetch** — Similar to archey but has an option to take a screenshot. Written in bash.

NaN

#### Graphical

*   **CPU-G** — An application that shows useful information about your hardware, it looks like CPU-Z in Windows.

NaN

*   **hardinfo** — A small application that displays information about your hardware and operating system, it looks like the Device Manager in Windows.

NaN

*   **i-Nex** — An application that gathers information for hardware components available on your system and displays it using an user interface similar to the popular Windows tool CPU-Z.

NaN

*   **lshw-gtk** — A small tool to provide detailed information on the hardware configuration of the machine with CLI and GTK interfaces.

NaN

#### Others

*   **tp-hdd-led** — Monitor HDD use with the Think-Led

NaN

### Keyboard layout switchers

*   **fbxkb** — A NETWM compliant keyboard indicator and switcher. It shows a flag of current keyboard in a systray area and allows you to switch to another one.

NaN

*   **xxkb** — A lightweight keyboard layout indicator and switcher.

NaN

*   **qxkb** — A keyboard switcher written in Qt.

NaN

*   **[X Neural Switcher](https://en.wikipedia.org/wiki/X_Neural_Switcher "wikipedia:X Neural Switcher")** — A text analyser, it detects the language of the input and corrects the keyboard layout if needed.

NaN

### Power management

See [Power saving#Packages](/index.php/Power_saving#Packages "Power saving").

### Clipboard managers

See: [List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard").

### Wallpaper setters

*   **bgs** — An extremely fast and small background setter for X based on imlib2.

NaN

*   **esetroot** — Eterm's root background setter, packaged separately

NaN

*   **[Feh](/index.php/Feh "Feh")** — A lightweight and powerful image viewer that can also be used to manage the desktop wallpaper.

NaN

*   **habak** — A background changing app

NaN

*   **hsetroot** — A tool to create compose wallpapers.

NaN

*   **[Nitrogen](/index.php/Nitrogen "Nitrogen")** — A fast and lightweight desktop background browser and setter for X windows.

NaN

*   **pybgsetter** — Multi-backend (hsetroot, Esetroot, habak, feh) to set desktop wallpaper

NaN

*   **wallpaperd** — A small application that takes care of setting the background image

NaN

*   **xli** — An image display program for X

NaN

**Tip:** In order to avoid installing one more package, you may find convenient to use the `display` utility from [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) or `gm display` from [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick). E.g.: `display -backdrop -background '#3f3f3f' -flatten -window root _image_`.

### Package management

See [pacman tips#Utilities](/index.php/Pacman_tips#Utilities "Pacman tips").

### Input method editor

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Internationalization#Input_methods_in_Xorg](/index.php/Internationalization#Input_methods_in_Xorg "Internationalization").**

**Notes:** Then just link there. (Discuss in [Talk:List of applications#](https://wiki.archlinux.org/index.php/Talk:List_of_applications))

See also [Wikipedia:Input method](https://en.wikipedia.org/wiki/Input_method "wikipedia:Input method").

*   **[Fcitx](/index.php/Fcitx "Fcitx")** — Flexible Context-aware Input Tool with eXtension.

NaN

*   **Hime** — A GTK2+/GTK3+ based universal input method platform.

NaN

*   **[IBus](/index.php/IBus "IBus")** — Next Generation Input Bus for Linux.

NaN

*   **[Rime IME](/index.php/Rime_IME "Rime IME")** — Rime input method engine.

NaN

*   **[UIM](/index.php/UIM "UIM")** — Multilingual input method library.

NaN

### Trash management

*   **trash-cli** — A command-line interface implementing FreeDesktop.org's Trash specification.

NaN

### File synchronization

*   **[rsync](/index.php/Rsync "Rsync")** — An incremental transfer and synchronization program.

NaN

*   **[Syncthing](/index.php/Syncthing "Syncthing")** — Open, trustworthy and decentralized cloud synchronization service.

NaN

*   **[Unison](/index.php/Unison "Unison")** — Bidirectional sync. It keeps track of changes like a VCS.

NaN

### Finders

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

[![Tango-view-fullscreen.png](/images/3/38/Tango-view-fullscreen.png)](/index.php/File:Tango-view-fullscreen.png)

**This article or section needs expansion.**

**Reason:** See also [find](/index.php/Find "Find") and [locate](/index.php/Locate "Locate"). (Discuss in [Talk:List of applications#](https://wiki.archlinux.org/index.php/Talk:List_of_applications))

*   **fuzzy-find** — Fuzzy completion for finding files.

NaN

*   **fzf** — General-purpose command-line fuzzy finder.

NaN

*   **rmlint** — Tool to quickly find (and optionally remove) duplicate files and other lint

NaN

## Documents and texts

### Office suites

See also [Wikipedia:Comparison of office suites](https://en.wikipedia.org/wiki/Comparison_of_office_suites "wikipedia:Comparison of office suites").

*   **[Calligra](https://en.wikipedia.org/wiki/Calligra_Suite "wikipedia:Calligra Suite")** — Actively developed fork of KOffice, the [KDE](/index.php/KDE "KDE") office suite. It offers most of the features of OpenOffice while also having versions for smartphones (Calligra Mobile) and tablets (Calligra Active).

NaN

*   **[LibreOffice](/index.php/LibreOffice "LibreOffice")** — More actively developed fork of OpenOffice.

NaN

*   **[OpenOffice](/index.php/OpenOffice "OpenOffice")** — Open-source office software suite for word processing, spreadsheets, presentations, graphics, databases and more, under the Apache Licence.

NaN

*   **[Siag Office](https://en.wikipedia.org/wiki/Siag_Office "wikipedia:Siag Office")** — Extremely lightweight office suite that provides a word processor, spreadsheet, text editor, file manager and previewer.

NaN

*   **[SoftMaker Office](https://en.wikipedia.org/wiki/SoftMaker_Office "wikipedia:SoftMaker Office")** — A complete, reliable, lightning-fast and Microsoft Office-compatible office suite with a word processor, spreadsheet, and presentation graphics software.

NaN

*   **[WPS Office](https://en.wikipedia.org/wiki/Kingsoft_Office "wikipedia:Kingsoft Office")** — Propietary office productivity suite, previously known as Kingsoft Office.

NaN

### Word processors

See also [Wikipedia:Comparison of word processors](https://en.wikipedia.org/wiki/Comparison_of_word_processors "wikipedia:Comparison of word processors").

*   **[Abiword](/index.php/Abiword "Abiword")** — Full-featured word processor.

NaN

*   **[BlueGriffon](https://en.wikipedia.org/wiki/BlueGriffon "wikipedia:BlueGriffon")** — WYSIWYG content editor for the World Wide Web.

NaN

*   **[Calligra Words](https://en.wikipedia.org/wiki/Calligra_Words "wikipedia:Calligra Words")** — Powerful word processor included in the Calligra Suite.

NaN

*   **gLabels** — program for creating labels and business cards.

NaN

*   **[LibreOffice Writer](/index.php/LibreOffice "LibreOffice")** — Full-featured word processor included in the LibreOffice suite.

NaN

*   **[OpenOffice Writer](/index.php/OpenOffice "OpenOffice")** — Full-featured word processor included in the OpenOffice suite.

NaN

*   **Pathetic Writer** — X-based rich text processor included in Siag Office.

NaN

*   **[Scribus](https://en.wikipedia.org/wiki/Scribus "wikipedia:Scribus")** — Desktop publishing program.

NaN

*   **[Ted](https://en.wikipedia.org/wiki/Ted_(word_processor) "wikipedia:Ted (word processor)")** — Easy to use GTK+-based rich text processor (with footnote support).

NaN

### Document markup languages

See also [Wikipedia:Comparison of document markup languages](https://en.wikipedia.org/wiki/Comparison_of_document_markup_languages "wikipedia:Comparison of document markup languages").

*   **[asciidoc](https://en.wikipedia.org/wiki/AsciiDoc "wikipedia:AsciiDoc")** — Human-readable text document format. Used by Arch for generating _pacman_ 's man pages[[2]](https://www.archlinux.org/pacman/pacman.8.html).

NaN

*   **Asciidoctor** — An asciidoc implementation written in Ruby, with many extra features.

NaN

*   **[Markdown](https://en.wikipedia.org/wiki/Markdown "wikipedia:Markdown")** — Text-to-HTML conversion tool that allows you to write using a simple plain text format.

NaN

*   **[Pandoc](https://en.wikipedia.org/wiki/Pandoc "wikipedia:Pandoc")** — Swiss-army knife for converting one markup format into another.

NaN

*   **[Sphinx](https://en.wikipedia.org/wiki/Sphinx_(documentation_generator) "wikipedia:Sphinx (documentation generator)")** — A documentation generation system using [reStructuredText](https://en.wikipedia.org/wiki/ReStructuredText "wikipedia:ReStructuredText") to generate output in multiple formats (primary documentation system for the Python project).

NaN

*   **[txt2tags](https://en.wikipedia.org/wiki/Txt2tags "wikipedia:Txt2tags")** — Dead-simple, KISS-compliant lightweight, human-readable markup language to produce rich format content out of plain text files.

NaN

### Spreadsheets

See also [Wikipedia:Comparison of spreadsheet software](https://en.wikipedia.org/wiki/Comparison_of_spreadsheet_software "wikipedia:Comparison of spreadsheet software").

*   **[Calligra Sheets](https://en.wikipedia.org/wiki/Calligra_Sheets "wikipedia:Calligra Sheets")** — Powerful spreadsheet application included in the Calligra Suite

NaN

*   **[Gnumeric](/index.php/Gnumeric "Gnumeric")** — Spreadsheet program that is part of the GNOME desktop.

NaN

*   **[LibreOffice Calc](/index.php/LibreOffice "LibreOffice")** — Full-featured spreadsheet application included in the LibreOffice suite.

NaN

*   **[OpenOffice Calc](/index.php/OpenOffice "OpenOffice")** — Full-featured spreadsheet application included in the OpenOffice suite.

NaN

*   **Pyspread** — Pyspread is a non-traditional spreadsheet application that is based on and written in the programming language Python.

NaN

*   **Siag** — Spreadsheet application based on the X Window System and the Scheme programming language included in Siag Office.

NaN

### Scientific documents

With [TeX, LaTeX and friends](/index.php/TeX_Live "TeX Live"), creation of any scientific document, article, journal, etc. is made commonplace.

See also [Wikipedia:Comparison of TeX editors](https://en.wikipedia.org/wiki/Comparison_of_TeX_editors "wikipedia:Comparison of TeX editors") and [the LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Editors).

*   **[AUCTeX](https://en.wikipedia.org/wiki/AUCTEX "wikipedia:AUCTEX")** — Together with RefTex, AUCTeX provices an extensible environment for writing and formatting TeX files in Emacs.

NaN

*   **EqualX** — LaTeX equation editor with real time preview.

NaN

*   **gedit-latex** — Add code-completion to gedit and allows for compiling LaTeX documents and managing BibTeX bibliographies.

NaN

*   **[Gummi](https://en.wikipedia.org/wiki/Gummi_(software) "wikipedia:Gummi (software)")** — Lightweight TeX/LaTeX GTK+-based editor. It features a continuous preview mode, integrated BibTeX support, extendable snippet interface and multi-document support.

NaN

*   **JabRef** — Java GUI frontend for managing BibTeX and other bibliographies.

NaN

*   **[Kile](https://en.wikipedia.org/wiki/Kile "wikipedia:Kile")** — User-friendly TeX/LaTeX editor for the KDE desktop with many features.

NaN

*   **Ktikz** — GUI making diagrams with [PGF/TikZ](http://pgf.sourceforge.net/) easier.

NaN

*   **LaTeXila** — LaTeX editor for the GNOME Desktop including support for code completion, compiling and project management.

NaN

*   **[LyX](https://en.wikipedia.org/wiki/LyX "wikipedia:LyX")** — Document processor that encourages an approach to writing based on the structure of your documents (WYSIWYM) and not simply their appearance (WYSIWYG).

NaN

*   **[TeXmacs](https://en.wikipedia.org/wiki/GNU_TeXmacs "wikipedia:GNU TeXmacs")** — WYSIWYW (what you see is what you want) editing platform with special features for scientists.

NaN

*   **[Texmaker](https://en.wikipedia.org/wiki/Texmaker "wikipedia:Texmaker")** — Cross-platform, light and easy-to-use LaTeX IDE. It integrates many tools needed to develop documents with LaTeX, in just one application

NaN

*   **TeXstudio** — Fork of TeXMaker including support for code completion of bibtex items, grammar check and automatic detection of the need for multiple LaTeX runs.

NaN

*   **[Vim-LaTeX-suite](/index.php/Vim "Vim")** — Customizable LaTeX environment for Vim.

NaN

*   **[Vimtex](/index.php/Vim "Vim")** — This vim plugin is a fork of [LaTeX-Box](https://github.com/LaTeX-Box-Team/LaTeX-Box). It provides automatic syntax-based folding, omni-completion (for citations and labels), latexmk-based compilation and synctex functionality for [zathura](https://www.archlinux.org/packages/?name=zathura) and [mupdf](https://www.archlinux.org/packages/?name=mupdf).

NaN

*   **WhizzyTeX** — WhizzyTeX provides a nice live preview editor for Emacs.

NaN

*   **Winefish** — A very lightweight LaTeX editing suite. It supports highlighting and code completion, compile-from-editor, among other things.

NaN

*   **Zotero** — This is a free, easy-to-use tool to help you collect, organize, cite, and share your research sources. There is a stand-alone version and a Firefox add-on available.

NaN

### Translation and localization

*   **[Apertium](https://en.wikipedia.org/wiki/Apertium "wikipedia:Apertium")** — Free and open source rule-based machine translation platform with available language data. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, TMX, MediaWiki and others.

NaN

*   **[Gtranslator](https://en.wikipedia.org/wiki/Gtranslator "wikipedia:Gtranslator")** — Enhanced gettext po file editor for the GNOME. It handles all forms of gettext po files and includes very useful features.

NaN

*   **[Lokalize](https://en.wikipedia.org/wiki/Lokalize "wikipedia:Lokalize")** — Standard [KDE](/index.php/KDE "KDE") tool for software translation. It includes basic editing of PO files, support for glossary, translation memory, project managing, etc. It belongs to [kdesdk](https://www.archlinux.org/groups/x86_64/kdesdk/)

NaN

*   **[Moses](https://en.wikipedia.org/wiki/Moses_(machine_translation) "wikipedia:Moses (machine translation)")** — Statistical machine translation tool (language data not included).

NaN

*   **[OmegaT](https://en.wikipedia.org/wiki/OmegaT "wikipedia:OmegaT")** — General translator's tool which contains a lot of translation memory features and can give suggestions from Google Translate. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, XLIFF/Okapi, MediaWiki, plain text, TMX and others.

NaN

*   **[Poedit](https://en.wikipedia.org/wiki/Poedit "wikipedia:Poedit")** — Simple gettext/po-based translation tool.

NaN

*   **Pology** — Set of Python tools for dealing with gettext/po-files.

NaN

*   **[Virtaal](https://en.wikipedia.org/wiki/Virtaal "wikipedia:Virtaal")** — Editor for translation of both software and other text, based on [Translate Toolkit](https://en.wikipedia.org/wiki/Translate_Toolkit "wikipedia:Translate Toolkit"). It supports the following formats: [gettext](https://en.wikipedia.org/wiki/gettext "wikipedia:gettext"), [XLIFF](https://en.wikipedia.org/wiki/XLIFF "wikipedia:XLIFF") , TMX, TBX, [Wordfast](https://en.wikipedia.org/wiki/Wordfast "wikipedia:Wordfast"), Qt Linguist , Qt Phrase Book, [OmegaT glossary](https://en.wikipedia.org/wiki/OmegaT "wikipedia:OmegaT") and others. It can also show suggestions from [Apertium](https://en.wikipedia.org/wiki/Apertium "wikipedia:Apertium"), [Google Translate](https://en.wikipedia.org/wiki/Google_Translate "wikipedia:Google Translate"), [Bing Translator](https://en.wikipedia.org/wiki/Bing_Translator "wikipedia:Bing Translator"), [Moses](https://en.wikipedia.org/wiki/Moses_(machine_translation) "wikipedia:Moses (machine translation)") and others.

NaN

### Text editors

See also [Wikipedia:Comparison of text editors](https://en.wikipedia.org/wiki/Comparison_of_text_editors "wikipedia:Comparison of text editors").

Some of the lighter-weight [Integrated development environments](/index.php/List_of_applications/Utilities#Integrated_development_environments "List of applications/Utilities") can also serve as text editors.

#### Console

*   **e3** — Tiny editor without dependencies, written in assembly.

NaN

*   **ee** — A classic curse-based text editor. Born in HP-UX, used in FreeBSD.

NaN

*   **dex** — Small and easy to use text editor with support for ctags and parsing compiler errors.

NaN

*   **[Emacs-nox](/index.php/Emacs "Emacs")** — The extensible, customizable, self-documenting real-time display editor, without X11 support.

NaN

*   **[JED](https://en.wikipedia.org/wiki/JED_(text_editor) "wikipedia:JED (text editor)")** — Text editor that makes extensive use of the [S-Lang library](https://en.wikipedia.org/wiki/S-Lang_(programming_library) "wikipedia:S-Lang (programming library)"). Includes a console version (jed) and an X-window version (xjed).

NaN

*   **[Joe](/index.php/Joe "Joe") (Joe's Own Editor)** — Terminal-based text editor designed to be easy to use.

NaN

*   **[mcedit](https://en.wikipedia.org/wiki/Midnight_Commander "wikipedia:Midnight Commander")** — Useful text editor that comes with Midnight Commander file manager.

NaN

*   **[MicroEmacs](https://en.wikipedia.org/wiki/MicroEMACS "wikipedia:MicroEMACS")** — Ncurses-based text editor. Includes a console version (me -n) and an X-window version (me).

NaN

*   **[mg](https://en.wikipedia.org/wiki/mg_(editor) "wikipedia:mg (editor)")** — Small, fast, and portable Emacs-like editor.

NaN

*   **mp** — Minimum Profit is a text editor for programmers. It helps you definitively abandon vi, emacs and other six-legged freaks.

NaN

*   **[Nano](/index.php/Nano "Nano")** — Console text editor based on pico with on-screen key bindings help.

NaN

*   **Ne** — Minimalist text editor with Windows-like key-bindings.

NaN

*   **Slap** — Sublime-like terminal-based text editor.

NaN

*   **[vile](https://en.wikipedia.org/wiki/Vile_(editor) "wikipedia:Vile (editor)")** — A lightweight Emacs clone with _vi_-like key bindings.

NaN

*   **[Zile](https://en.wikipedia.org/wiki/Zile_(editor) "wikipedia:Zile (editor)")** — A lightweight Emacs clone.

NaN

##### Vi text editors

*   **[Neovim](/index.php/Neovim "Neovim")** — Vim's rebirth for the 21st century

NaN

*   **[Vi](/index.php/Vi "Vi")** — The original ex/vi text editor.

NaN

*   **[Vim](/index.php/Vim "Vim") (Vi IMproved)** — Advanced text editor that seeks to provide the power of the de-facto Unix editor 'vi', with a more complete feature set.

NaN

#### Graphical

*   **[Acme](https://en.wikipedia.org/wiki/Acme_(text_editor) "wikipedia:Acme (text editor)")** — Minimalist and flexible programming environment developed by Rob Pike for the Plan 9 operating system.

NaN

*   **[Atom](/index.php/Atom "Atom")** — A promising text editor developed by GitHub. With support for plug-ins written in Node.js and embedded [Git](/index.php/Git "Git") Control.

NaN

*   **Beaver** — A GTK+ editor designed to be modular, lightweight and stylish.

NaN

*   **Brackets** — An open source code editor for the web, written in JavaScript, HTML and CSS.

NaN

*   **[Cream](https://en.wikipedia.org/wiki/Cream_(software) "wikipedia:Cream (software)")** — A user-friendly editor atop of gVim.

NaN

*   **Edile** — PyGTK code and scripting editor implemented in one file.

NaN

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — A text editor using the GTK2 toolkit with basic features of an integrated development environment. It has support for TeX-based documents.

NaN

*   **[Gedit](https://en.wikipedia.org/wiki/Gedit "wikipedia:Gedit")** — GTK+ editor for the GNOME desktop with syntax highlighting, automatic indentation, matching brackets, etc., and a number of add-ons to increase functionality.

NaN

*   **[GNU Emacs](/index.php/GNU_Emacs "GNU Emacs")** — The extensible, customizable, self-documenting real-time display editor.

NaN

*   **[gVim](/index.php/GVim "GVim")** — Graphical interface for Vim.

NaN

*   **Jedit** — Text editor for programmers, written in Java.

NaN

*   **[JuffEd](https://en.wikipedia.org/wiki/JuffEd "wikipedia:JuffEd")** — Simple tabbed text editor with syntax highlighting, written in Qt.

NaN

*   **[Kate](https://en.wikipedia.org/wiki/Kate_(text_editor) "wikipedia:Kate (text editor)")** — Full-featured programmer's editor for the KDE desktop with MDI and a filesystem browser.

NaN

*   **[KWrite](https://en.wikipedia.org/wiki/KWrite "wikipedia:KWrite")** — Lightweight text editor for the KDE desktop that uses the same editor widget as Kate.

NaN

*   **[Leafpad](https://en.wikipedia.org/wiki/Leafpad "wikipedia:Leafpad")** — Notepad clone for GTK+ that emphasizes simplicity.

NaN

*   **L3afpad** — Simple text editor forked from Leafpad, supports GTK+ 3.

NaN

*   **Medit** — Programming and around-programming text editor.

NaN

*   **[Mousepad](https://en.wikipedia.org/wiki/Xfce#Leafpad "wikipedia:Xfce")** — Fast text editor for the Xfce Desktop Environment.

NaN

*   **[Nedit](https://en.wikipedia.org/wiki/NEdit "wikipedia:NEdit")** — Text editor for the [lesstif](https://www.archlinux.org/packages/?name=lesstif) environment.

NaN

*   **[Pluma](/index.php/MATE "MATE")** — A powerful text editor for MATE.

NaN

*   **[PyRoom](https://en.wikipedia.org/wiki/PyRoom "wikipedia:PyRoom")** — Great distractionless PyGTK text editor, a clone of the infamous WriteRoom.

NaN

*   **QEdit** — A multi-purpose text editor based on NEdit using Qt.

NaN

*   **QSciTE** — Qt clone of the SciTE text and code editor.

NaN

*   **QXmlEdit** — Simple Qt XML editor and XSD viewer.

NaN

*   **[Sam](https://en.wikipedia.org/wiki/Sam_(text_editor) "wikipedia:Sam (text editor)")** — Minimalist text editor with a graphical user interface, a very powerful command language and remote editing capabilities, developed by Rob Pike.

NaN

*   **[SciTE](https://en.wikipedia.org/wiki/SciTE "wikipedia:SciTE")** — Generally useful editor with facilities for building and running programs.

NaN

*   **Scribes** — An ultra minimalist text editor that combines simplicity with power.

NaN

*   **[Sublime Text 2](https://en.wikipedia.org/wiki/Sublime_Text "wikipedia:Sublime Text")** — Closed-source C++ and Python-based editor with many advanced features and plugins while staying lightweight and pretty.

NaN

*   **Tea** — Qt-based feature rich text editor.

NaN

*   **[Textadept](/index.php/Textadept "Textadept")** — Lua-extensible feature rich text editor based on Scintilla and written in C.

NaN

*   **XEdit** — Simple text editor for the X Window System.

NaN

##### Collaborative text editors

*   **Gobby** — Collaborative editor supporting multiple documents in one session and a multi-user chat.

NaN

### Readers and Viewers

#### E-book applications

**Note:** Some [PDF and DjVu viewers](#PDF_and_DjVu) also support other e-book formats.

*   **[Calibre](https://en.wikipedia.org/wiki/Calibre_(software) "wikipedia:Calibre (software)")** — E-book library management application that can also convert between different formats and sync with a variety of e-book readers. Supported formats include CBZ, CBR, CBC, CHM, DJVU, EPUB, FictionBook, HTML, HTMLZ, LIT, LRF, Mobipocket, ODT, PDF, PRC, PDB, PML, RB, RTF, SNB, TCR, TXT and TXTZ.

NaN

*   **Cool Reader** — E-book viewer with many supported formats such as EPUB (non-DRM), FictionBook, TXT, RTF, HTML, CHM and TCR.

NaN

*   **epub** — A console EPUB reader using Python and Curses.

NaN

*   **[FBReader](https://en.wikipedia.org/wiki/FBReader "wikipedia:FBReader")** — E-book viewer with many supported formats such as EPUB, FictionBook, HTML, plucker, PalmDoc, zTxt, TCR, CHM, RTF, OEB, Mobipocket (non-DRM) and TXT.

NaN

*   **pPub** — Simple EPUB reader using Python, GTK3 and WebKit.

NaN

*   **[Sigil](https://en.wikipedia.org/wiki/Sigil_(application) "wikipedia:Sigil (application)")** — WYSIWYG ebook editor.

NaN

##### Book organizers

for more collection apps, see also [Multimedia#Collection managers](/index.php/Multimedia#Collection_managers "Multimedia")

*   **Alexandria** — GNOME application to help manage your book collection.

NaN

*   **[Koha](https://en.wikipedia.org/wiki/Koha_(software) "wikipedia:Koha (software)")** — Open source Integrated Library System (ILS), used world-wide by public, school and special libraries.

NaN

#### PDF and DjVu

**Note:** [PDF forms](https://en.wikipedia.org/wiki/Portable_Document_Format#Interactive_elements "wikipedia:Portable Document Format") support:

*   [acroread](https://aur.archlinux.org/packages/acroread/)<sup><small>AUR</small></sup> is able to save both AcroForms and XFA forms into PDF files.
*   Poppler-based readers such as [evince](https://www.archlinux.org/packages/?name=evince) and [kdegraphics-okular](https://www.archlinux.org/packages/?name=kdegraphics-okular) support AcroForms, but not full XFA forms. [[3]](https://bugs.freedesktop.org/show_bug.cgi?id=18935) [[4]](https://bugs.launchpad.net/ubuntu/+source/poppler/+bug/321720)
*   For CJK(Chinese, Japanese, Korean) support in poppler-based readers such as [evince](https://www.archlinux.org/packages/?name=evince) and [kdegraphics-okular](https://www.archlinux.org/packages/?name=kdegraphics-okular), install [poppler-data](https://www.archlinux.org/packages/?name=poppler-data). poppler-data is an optional dependency of poppler which is an indirect dependency of evince and okular.

See also [Wikipedia:List of PDF software](https://en.wikipedia.org/wiki/List_of_PDF_software "wikipedia:List of PDF software") and [Wikipedia:DjVu](https://en.wikipedia.org/wiki/DjVu "wikipedia:DjVu").

##### Console

*   **fbpdf** — Small framebuffer PDF and DjVu viewer based off of MuPDF, with [Vim](/index.php/Vim "Vim") keybindings and written in C

NaN

*   **jfbview** — Framebuffer PDF and image viewer. Features include Vim-like controls, zoom-to-fit, a TOC (outline) view, fast multi-threaded rendering and asynchronous pre-caching. Originally a fork of _fbpdf_ called _jfbpdf_, now completely rewritten.

NaN

##### Graphical

**Note:** Some [web browsers](/index.php/List_of_applications/Internet#Web_browsers "List of applications/Internet") have support for displaying PDF files, either built-in or via plugin.

*   **acroread** — A PDF file viewer offered by Adobe (closed source).

NaN

*   **apvlv** — Lightweight PDF/DjVu/UMD/TXT viewer with [Vim](/index.php/Vim "Vim") keybindings.

NaN

*   **Atril** — Simple multi-page document viewer for MATE.

NaN

*   **ePDFView** — Free lightweight PDF document viewer using the Poppler and GTK+ libraries. Development stopped.

NaN

*   **[Evince](https://en.wikipedia.org/wiki/Evince "wikipedia:Evince")** — Document viewer for multiple document formats. Supports PDF, PostScript, DjVu, TIFF and DVI.

NaN

*   **[Foxit Reader](https://en.wikipedia.org/wiki/Foxit_Reader "wikipedia:Foxit Reader")** — Small, fast (compared to Acrobat) PDF viewer. (closed source)

NaN

*   **gv** — Graphical user interface for the Ghostscript interpreter that allows to view and navigate through PostScript and PDF documents.

NaN

*   **[llpp](/index.php/Llpp "Llpp")** — Very fast PDF reader based off of MuPDF, that supports continuous page scrolling, bookmarking, and text search through the whole document.

NaN

*   **[MuPDF](https://en.wikipedia.org/wiki/MuPDF "wikipedia:MuPDF")** — Very fast PDF and XPS viewer and toolkit written in portable C. Features CJK font support.

NaN

*   **[Okular](https://en.wikipedia.org/wiki/Okular "wikipedia:Okular")** — Universal PDF viewer for KDE.

NaN

*   **PdfMod** — You can reorder, rotate, and remove pages, export images from a document, edit the title, subject, author, and keywords, and combine documents via drag and drop.

NaN

*   **PDF Studio** — All-in-one PDF editor similar to Adobe Acrobat (proprietary).

NaN

*   **qpdfview** — Tabbed document viewer. It uses Poppler for PDF support, libspectre for PS support, DjVuLibre for DjVu support, CUPS for printing support and the Qt toolkit for its interface.

NaN

*   **[Xournal](https://en.wikipedia.org/wiki/Xournal "wikipedia:Xournal")** — Pdf viewer/note taking application.

NaN

*   **[Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf")** — Viewer that can decode LZW and read encrypted PDFs.

NaN

*   **[zathura](https://en.wikipedia.org/wiki/Zathura_(document_viewer) "wikipedia:Zathura (document viewer)")** — Highly customizable and functional PDF/DjVu/PostScript/ComicBook viewer (plugin based).

NaN

#### Terminal pagers

See also [Wikipedia:Terminal pager](https://en.wikipedia.org/wiki/Terminal_pager "wikipedia:Terminal pager").

*   [more](https://en.wikipedia.org/wiki/More_(command) "wikipedia:More (command)") — A simple and feature-light pager. It is a part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package.
*   **[less](/index.php/Core_utilities#less "Core utilities")** — A program similar to more, but with support for both forward and backward scrolling, as well as partial loading of files.

NaN

*   **less-mouse** — less with mouse scrolling support. It is present in the AUR as [less-mouse](https://aur.archlinux.org/packages/less-mouse/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/less-mouse)]</sup>.
*   **[most](https://en.wikipedia.org/wiki/Most_(Unix) "wikipedia:Most (Unix)")** — A pager with support for multiple windows, left and right scrolling, and built-in colour support

NaN

*   **mcview** — A pager with mouse and colour support. It is bundled with midnight commander.

NaN

*   **vimpager** — A script that turns vim into a pager. As a result, you get various vim features such as colour schemes, mouse support, split screens, etc.

NaN

#### CHM

See also [Wikipedia:Microsoft Compiled HTML Help](https://en.wikipedia.org/wiki/Microsoft_Compiled_HTML_Help "wikipedia:Microsoft Compiled HTML Help").

*   **ChmSee** — CHM viewer based on xulrunner.

NaN

*   **Kchmviewer** — Qt-based CHM viewer that uses chmlib and borrows some ideas from xchm. It does not depend on [KDE](/index.php/KDE "KDE"), but it can be compiled to integrate with it.

NaN

*   **[xCHM](https://en.wikipedia.org/wiki/xCHM "wikipedia:xCHM")** — Lightweight CHM viewer, based on chmlib.

NaN

#### Comic book (comix/manga)

*   **[MComix](https://en.wikipedia.org/wiki/MComix "wikipedia:MComix")** — GTK2 image viewer specifically designed to handle comic book archives (fork of Comix). Also includes library manager.

NaN

*   **QComicBook** — Lightweight comic book viewer written in C++ and Qt4.

NaN

*   **YACReader** — Comic book viewer written in C++ and Qt5\. Comes with YACReaderLibrary for managing comics.

NaN

### Scanning software

See [SANE#Install a frontend](/index.php/SANE#Install_a_frontend "SANE").

### OCR software

See also [Wikipedia:Comparison of optical character recognition software](https://en.wikipedia.org/wiki/Comparison_of_optical_character_recognition_software "wikipedia:Comparison of optical character recognition software").

#### Engines

*   **CuneiForm** — Command line OCR system originally developed and open sourced by Cognitive technologies. Supported languages: eng, ger, fra, rus, swe, spa, ita, ruseng, ukr, srp, hrv, pol, dan, por, dut, cze, rum, hun, bul, slo, lav, lit, est, tur.

NaN

*   **GOCR/JOCR** — OCR engine which also supports barcode recognition.

NaN

*   **Ocrad** — OCR program based on a feature extraction method.

NaN

*   **Tesseract** — Accurate open source OCR engine. Package splitted, you need install some datafiles for each language ([tesseract-data-eng](https://www.archlinux.org/packages/?name=tesseract-data-eng) for example).

NaN

#### Layout analyzers and user interfaces

*   **gImageReader** — Graphical GTK frontend to Tesseract.

NaN

*   **gscan2pdf** — Scans, runs an OCR engine, minor post-processing, creates a document.

NaN

*   **OCRFeeder** — Python GUI for Gnome which performs document analysis and rendition, and can use either CuneiForm, GOCR, Ocrad or Tesseract as OCR engines. It can import from PDF or image files, and export to HTML or OpenDocument.

NaN

*   **OCRopy** — OCR _platform_, modules exist for document layout analysis, OCR engines (it can use Tesseract or its own engine), natural language modeling, etc.

NaN

*   **[YAGF](/index.php/YAGF "YAGF")** — Graphical interface for the CuneiForm text recognition program on the Linux platform.

NaN

### Note taking organizers

See also [Wikipedia:Comparison of notetaking software](https://en.wikipedia.org/wiki/Comparison_of_notetaking_software "wikipedia:Comparison of notetaking software").

#### Console

*   **hnb (hierarchical notebook)** — Program to organize many kinds of data (addresses, to-do lists, ideas, book reviews, etc.) in one place using the XML format.

NaN

*   **pynote** — Manage notes on the commandline

NaN

#### Graphical

*   **[BasKet](https://en.wikipedia.org/wiki/BasKet_Note_Pads "wikipedia:BasKet Note Pads")** — Application for organizing, sharing, and taking notes. It can manage various types of information such as to-do lists, links, pictures, and other types, similar to a scrapbook.

NaN

*   **Cherrytree** — Hierarchical note taking application, featuring rich text and syntax highlighting, storing data in a single xml or sqlite file.

NaN

*   **[Gnote](https://en.wikipedia.org/wiki/Gnote "wikipedia:Gnote")** — Experimental port of Tomboy to C++.

NaN

*   **KeepNote** — Cross-platform GTK+ note-taking application with rich text formatting.

NaN

*   **KNotes** — A program that lets you write the computer equivalent of sticky notes.

NaN

*   **NoteCase** — Portable hierarchical note manager, coded in C++ using bindings to the GTK+ toolkit.

NaN

*   **[org-mode](https://en.wikipedia.org/wiki/org-mode "wikipedia:org-mode")** — [Emacs](/index.php/Emacs "Emacs") mode for notes, project planning and authoring.

NaN

*   **[Tomboy](https://en.wikipedia.org/wiki/Tomboy_(software) "wikipedia:Tomboy (software)")** — Desktop note-taking application for Linux and Unix with a wiki-like linking system to connect notes together.

NaN

*   **wiznote** — Opensource cross-platform cloud based note-taking client.

NaN

*   **[zim](/index.php/Zim "Zim")** — WYSIWYG text editor that aims at bringing the concept of a wiki to the desktop.

NaN

*   **znotes** — A lightweight crossplatform application for notes managment with simple interface, use qt4 libraries.

NaN

### Mind-mapping tools

*   **FreeMind** — Premier free mind-mapping software written in Java.

NaN

*   **Freeplane** — Free and open source software application that supports thinking, sharing information and getting things done at work, in school and at home. The software can be used for mind mapping and analyzing the information contained in mind maps.

NaN

*   **Semantik** — A mind-mapping application for KDE.

NaN

*   **TreeSheets** — The ultimate replacement for spreadsheets, mind mappers, outliners, PIMs, text editors and small databases.

NaN

*   **View Your Mind** — Tool to generate and manipulate maps which show your thoughts. Such maps can help you to improve your creativity and effectivity. You can use them for time management, to organize tasks, to get an overview over complex contexts, to sort your ideas etc.

NaN

*   **Visual Understanding Environment** — Open Source project focused on creating flexible tools for managing and integrating digital resources in support of teaching, learning and research.

NaN

*   **XMind** — Brainstorming and mind mapping application. It provides a rich set of different visualization styles, and allows sharing of created mind maps via their website.

NaN

### Character Selector

*   **GNOME Characters** — Character map application for GNOME

NaN

*   **gucharmap** — A GTK+ 3 Character Selector, distributed with GNOME desktop.

NaN

*   **kdeutils-kcharselect** — A tool to select special characters from all installed fonts and copy them into the clipboard. Distributed with KDE.

NaN

### Stylus notes taking

*   **Write** — a word processor for hand writing.

NaN

*   **Gournal** — note-taking application written for usage on Tablet-PC, written in perl.

NaN

*   **Xournal** — an application for notetaking, sketching, keeping a journal using a stylus.

NaN

### Bibliographic reference managers

See also [Wikipedia:Comparison of reference management software](https://en.wikipedia.org/wiki/Comparison_of_reference_management_software "wikipedia:Comparison of reference management software").

*   **Bibus** — A bibliographic database that can directly insert references in OpenOffice.org/LibreOffice and generate the bibliographic index.

NaN

*   **DocEar** — Docear is an academic literature suite for searching, organizing and creating academic literature, built upon the mind mapping software Freeplane and the reference manager JabRef.

NaN

*   **JabRef** — GUI frontend for BibTeX, written in Java.

NaN

*   **Zotero** — Zotero Standalone. Is a free, easy-to-use tool to help you collect, organize, cite, and share your research sources.

NaN

## Security

For detailed guides, see the main ArchWiki page, [Security](/index.php/Security "Security").

#### Firewalls

See the main article: [Firewalls](/index.php/Firewalls "Firewalls").

See also [Wikipedia:Comparison of firewalls](https://en.wikipedia.org/wiki/Comparison_of_firewalls "wikipedia:Comparison of firewalls").

#### Network security

*   **[Arpwatch](https://en.wikipedia.org/wiki/Arpwatch "wikipedia:Arpwatch")** — Tool that monitors ethernet activity and keeps a database of Ethernet/IP address pairings.

NaN

*   **Bro** — Powerful network analysis framework that is much different from the typical IDS you may know.

NaN

*   **EtherApe** — Graphical network monitor for Unix modeled after etherman. Featuring link layer, IP and TCP modes, it displays network activity graphically. Hosts and links change in size with traffic. Color coded protocols display.

NaN

*   **[Honeyd](/index.php/Honeyd "Honeyd")** — Tool that allows the user to set up and run multiple virtual hosts on a computer network.

NaN

*   **IPTraf** — Console-based network monitoring utility.

NaN

*   **Kismet** — 802.11 layer2 wireless network detector, sniffer, and intrusion detection system.

NaN

*   **Nemesis** — Command-line network packet crafting and injection utility.

NaN

*   **[Nmap](/index.php/Nmap "Nmap")** — Security scanner used to discover hosts and services on a computer network, thus creating a "map" of the network.

NaN

*   **[Ntop](/index.php/Ntop "Ntop")** — Network probe that shows network usage in a way similar to what top does for processes.

NaN

*   **[Snort](/index.php/Snort "Snort")** — Network intrusion prevention and detection system.

NaN

*   **[Sshguard](/index.php/Sshguard "Sshguard")** — Daemon that protects SSH and other services against brute-force attacts, similar to Fail2ban.

NaN

*   **[Suricata](/index.php/Suricata "Suricata")** — High performance Network IDS, IPS and Network Security Monitoring engine.

NaN

*   **[Tcpdump](https://en.wikipedia.org/wiki/tcpdump "wikipedia:tcpdump")** — Common console-based packet analyzer that allows the user to intercept and display TCP/IP and other packets being transmitted or received over a network.

NaN

*   **[vnStat](/index.php/VnStat "VnStat")** — Console-based network traffic monitor that keeps a log of network traffic for the selected interfaces.

NaN

*   **[Wireshark](/index.php/Wireshark "Wireshark")** — Network protocol analyzer that lets you capture and interactively browse the traffic running on a computer network.

NaN

#### Threat and vulnerability detection

*   **AFICK** — Security tool that allows to monitor the changes on your files systems, and so can detect intrusions.

NaN

*   **Lynis** — Security and system auditing tool to harden Unix/Linux systems.

NaN

*   **[Metasploit Framework](/index.php/Metasploit_Framework "Metasploit Framework")** — An advanced open-source platform for developing, testing, and using exploit code.

NaN

*   **[Nessus](/index.php/Nessus "Nessus")** — Comprehensive vulnerability scanning program.

NaN

*   **[OpenVAS](/index.php/OpenVAS "OpenVAS")** — Framework of several services and tools offering a comprehensive and powerful vulnerability scanning and vulnerability management solution. FOSS Nessus fork.

NaN

*   **Osiris** — Tool for monitoring system integrity and changes across a network.

NaN

*   **OSSEC** — Open Source Host-based Intrusion Detection System that performs log analysis, file integrity checking, policy monitoring, rootkit detection, real-time alerting and active response.

NaN

*   **Samhain** — Host-based intrusion detection system (HIDS) provides file integrity checking and log file monitoring/analysis, as well as rootkit detection, port monitoring, detection of rogue SUID executables, and hidden processes.

NaN

*   **Tiger** — Security tool that can be use both as a security audit and intrusion detection system.

NaN

*   **[Tripwire](https://en.wikipedia.org/wiki/Open_Source_Tripwire "wikipedia:Open Source Tripwire")** — Intrusion detection system.

NaN

#### File security

*   **[AIDE](/index.php/AIDE "AIDE")** — File and directory integrity checker.

NaN

*   **Logcheck** — Simple utility which is designed to allow a system administrator to view the logfiles which are produced upon hosts under their control.

NaN

*   **[Logwatch](/index.php/Logwatch "Logwatch")** — Customizable log analysis system.

NaN

*   **OpenDLP** — OpenDLP is a free and open source, agent- and agentless-based, centrally-managed, massively distributable data loss prevention tool.

NaN

*   **Swatch** — Utility that can monitor just about any type of log.

NaN

#### Anti malware

*   **chkrootkit** — Locally checks for signs of a rootkit.

NaN

*   **[ClamAV](/index.php/ClamAV "ClamAV")** — Open source antivirus engine for detecting trojans, viruses, malware & other malicious threats.

NaN

*   **Linux Malware Detect** — Malware scanner designed around the threats faced in shared hosted environments.

NaN

*   **Rootkit Hunter** — Checks machines for the presence of rootkits and other unwanted tools.

NaN

#### Backup programs

See the main article: [Backup programs](/index.php/Backup_programs "Backup programs").

See also [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software").

#### Screen lockers

**Warning:** Only _sflock_, _physlock_, _Cinnamon Screensaver_, _MATE Screensaver_ and _GNOME Screensaver_ are able to block tty access.

*   **Cinnamon Screensaver** — Screen locker for the Cinnamon desktop.

NaN

*   **GNOME Screensaver** — Screen locker for the GNOME Flashback desktop.

NaN

*   **i3lock** — A simple screen locker. Provides user feedback, uses PAM authentication, supports DPMS. The background can be set to an image or solid color.

NaN

*   **i3lock-blur** — Fork of _i3lock_ which can use your desktop with the blur effect applied as a background.

NaN

*   **i3lock-wrapper** — A simple wrapper around _i3lock_ which sets up a blurred screenshot of the desktop as a background image.

NaN

*   **Light-locker** — A simple locker (forked from _gnome-screensaver_) that aims to have simple, sane, secure defaults and be well integrated with the desktop while not carrying any desktop-specific dependencies. It relies on [LightDM](/index.php/LightDM "LightDM") for locking and unlocking your session via ConsoleKit/UPower or _logind/systemd_

NaN

*   **MATE Screensaver** — Screensaver and locker for MATE Desktop Environment.

NaN

*   **physlock** — Screen and console locker.

NaN

*   **sflock** — Simple screen locker utility for X, based on slock. Provides a very basic user feedback.

NaN

*   **slock** — Very simple and lightweight X screen locker. Offers only a black background when locked, there are no animations or text fields.

NaN

*   **sxlock** — Fork of sflock with a few enhancements. Provides basic user feedback, uses PAM authentication, supports DPMS and RandR. Supports `sxlock.service` to lock the screen on suspend/hibernation. See the [README](https://github.com/lahwaacz/sxlock/blob/master/README.md) for more information.

NaN

*   **vlock** — TTY locker. A mirror of the [original vlock](https://lists.archlinux.org/pipermail/aur-general/2013-July/024662.html) is available at [github](https://github.com/WorMzy/vlock).

NaN

*   **xlockmore** — Simple X11 screen lock with PAM support.

NaN

*   **[XScreenSaver](/index.php/XScreenSaver "XScreenSaver")** — Screen saver and locker for the X Window System.

NaN

*   **XSecureLock** — X11 screen lock utility designed with the primary goal of security.

NaN

#### Hash checkers

*   **cfv** — Tiny utility to both test and create checksum files, support `.sfv`, `.csv`, `.crc`, `.md5`, `md5sum`, `sha1sum`, `.torrent`, `par`, and `.par2` files.

NaN

*   **GtkHash** — A GTK+ utility for computing message digests or checksums

NaN

*   **hashdeep** — A cross-platform tools to computer hashes, or message digests, for any number of files

NaN

*   **Parano** — A GNOME frontend for creating/editing/checking MD5 and SFV files

NaN

*   **Quick Hash GUI** — A GUI to enable the rapid selection and subsequent hashing of files (individually or recursively throughout a folder structure) text and (on Linux) disks.

NaN

*   **RHash** — Utility for verifying hash sums (SFV, CRC, etc). Supports lots of algorithms.

NaN

*   **MassHash** — A set of file hashing tools (both CLI and GTK+ GUI) written in Python. Supported algorithms include MD5, SHA-1, SHA-224, SHA-256, SHA-384, SHA-512.

NaN

#### Encryption, signing, steganography

*   **ccrypt** — A command-line utility for encrypting and decrypting files and streams.

NaN

*   **[Enigmail](https://en.wikipedia.org/wiki/Enigmail "wikipedia:Enigmail")** — _a security extension to Mozilla Thunderbird and Seamonkey. It enables you to write and receive email messages signed and/or encrypted with the OpenPGP standard._

NaN

*   **[GnuPG](/index.php/GnuPG "GnuPG")** — The GNU project's complete and free implementation of the OpenPGP standard as defined by RFC4880\. Free and Open Source replacement of PGP, mostly used for digital signing of packages.

NaN

*   **gzsteg** — A utiltiy that can hide data in gzip compressed files

NaN

*   **[KGpg](https://en.wikipedia.org/wiki/KGPG "wikipedia:KGPG")** — _a simple interface for GnuPG_ for KDE.

NaN

*   **[Seahorse](https://en.wikipedia.org/wiki/Seahorse_(software) "wikipedia:Seahorse (software)")** — _GNOME application for managing encryption keys and passwords in the GnomeKeyring._

NaN

*   **silenteye** — A steganography application written in C++, use Qt4 library.

NaN

*   **snow** — Steganography program for concealing messages in text files

NaN

*   **steghide** — A steganography utility that is able to hide data in various kinds of image and audio files.

NaN

*   **stegparty** — A steganography utility hides text by typoing text existing text files.

NaN

#### Password managers

*   **Console Password Manager** — Curses based password manager using PGP-encryption.

NaN

*   **Figaro's Password Manager 2** — GTK2 port of [Figaro's Password Manager](http://fpm.sourceforge.net/) with some new enhancements.

NaN

*   **GPass** — Password manegement software for GNOME2 desktop.

NaN

*   **GPassword Manager** — Simple, lightweight and cross-platform utility for managing and accessing passwords.

NaN

*   **Gtkpass** — Gtkpass is a GTK and Libkpass-based password manager for KeePass 1.x databases.

NaN

*   **Ked Password Manager** — A password manager that helps to manage large numbers of passwords.

NaN

*   **[KeePass Password Safe](/index.php/KeePass "KeePass")** — Free open source Mono-based password manager, which helps you to manage your passwords in a secure way.

NaN

*   **KeePassC** — KeePassC is a curses-based password manager compatible to KeePass v.1.x and KeePassX.

NaN

*   **KeePassX** — Free and open source Qt-based password manager. Compatible with KeePass v.1.x and KeePass v.2.x.

NaN

*   **MyPasswords** — What you need for managing your passwords, including the passwords of your online accounts, bank accounts and ... with the corresponding URLs.

NaN

*   **MyPasswordSafe** — Easy-to-use QT based password manager, compatible with Password Safe files (and therefore pwsafe).

NaN

*   **Pasaffe** — Easy to use password manager for Gnome with a Password Safe 3.0 compatible database.

NaN

*   **[pass](/index.php/Pass "Pass")** — Simple console based password manager

NaN

*   **Password Gorilla** — A cross-platform password manager.

NaN

*   **Password Safe** — Simple and secure password manager.

NaN

*   **pwsafe** — Unix commandline program that manages encrypted password databases.

NaN

*   **QPass** — Easy to use password manager with built-in password generator.

NaN

*   **Revelation** — Password manager for the GNOME desktop.

NaN

*   **Seahorse** — GNOME application for managing encryption keys and passwords in the GnomeKeyring.

NaN

*   **Universal Password Manager** — Allows you to store usernames, passwords, URLs and generic notes in an encrypted database protected by one master password.

NaN

## Science

**Note:** For possibly more up to date selection of scientific applications, try checking the [AUR 'science' category](https://aur.archlinux.org/packages.php?O=0&do_Search=Go&detail=1&C=15&SeB=nd&SB=v&SO=d&PP=50)

### Scientific documents

See the main article: [List of applications/Documents#Scientific documents](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents").

### Mathematics

#### Calculator

See also [Wikipedia:Comparison of software calculators](https://en.wikipedia.org/wiki/Comparison_of_software_calculators "wikipedia:Comparison of software calculators").

*   **[bc](https://en.wikipedia.org/wiki/bc_programming_language "wikipedia:bc programming language")** — Arbitrary precision calculator language.

NaN

*   **calc** — Arbitrary precision console calculator.

NaN

*   **Extcalc** — Qt-based scientfic graphical calculator.

NaN

*   **galculator** — GTK+ based scientific calculator.

NaN

*   **[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")** — Scientific calculator included in the GNOME desktop.

NaN

*   **[GCalctool](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")** — Scientific calculator included in the GNOME desktop (old GTK2 version).

NaN

*   **KAlgebra** — Calculator and 3D plotter included in KDE EDU.

NaN

*   **[KCalc](https://en.wikipedia.org/wiki/KCalc "wikipedia:KCalc")** — Scientific calculator included in the KDE desktop.

NaN

*   **Qalculate** — Calculator and equation solver with fault-tolerant parsing, constant recognition and units.

NaN

*   **SpeedCrunch** — Fast, high precision and powerful cross-platform calculator.

NaN

*   **[xcalc](https://en.wikipedia.org/wiki/xcalc "wikipedia:xcalc")** — Scientific calculator for X with algebraic and reverse polish notation modes.

NaN

#### Computer algebra system

See also [Wikipedia:Comparison of computer algebra systems](https://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems "wikipedia:Comparison of computer algebra systems").

*   **[AXIOM](https://en.wikipedia.org/wiki/Axiom_(computer_algebra_system) "wikipedia:Axiom (computer algebra system)")** — FriCAS: derivative of the powerful AXIOM-CAS

NaN

*   **[Fermat](https://en.wikipedia.org/wiki/Fermat_(computer_algebra_system) "wikipedia:Fermat (computer algebra system)")** — Computer algebra system that does arithmetic of arbitrarily long integers and fractions, multivariate polynomials, symbolic calculations, matrices over polynomial rings, graphics, and other numerical calculations.

NaN

*   **[GAP](https://en.wikipedia.org/wiki/GAP_(computer_algebra_system) "wikipedia:GAP (computer algebra system)")** — Computer algebra system for computational discrete algebra with particular emphasis on computational group theory.

NaN

*   **[Maple](/index.php/Maple "Maple")** — Famous commercial CAS. Often used in education.

NaN

*   **Mathics** — A free CAS for symbolic mathematical computations which uses [Python](/index.php/Python "Python") as its main language. It aims at achieving a Mathematica-compatible syntax and functions. It relies mostly on Sympy for most mathematical tasks and, optionally, Sage for more advanced functionality.

NaN

*   **[Mathomatic](https://en.wikipedia.org/wiki/Mathomatic "wikipedia:Mathomatic")** — General purpose Computer Algebra System written in C.

NaN

*   **[Maxima](https://en.wikipedia.org/wiki/Maxima_(software) "wikipedia:Maxima (software)")** — [Maple](https://en.wikipedia.org/wiki/Maple_(software) "wikipedia:Maple (software)")/[Mathematica](https://en.wikipedia.org/wiki/Wolfram_Mathematica "wikipedia:Wolfram Mathematica")-like program with a wxWidgets based frontend.

NaN

*   **[PARI/GP](https://en.wikipedia.org/wiki/PARI/GP "wikipedia:PARI/GP")** — Computer algebra system designed for fast computations in number theory.

NaN

*   **[Xcas](https://en.wikipedia.org/wiki/Xcas "wikipedia:Xcas")** — User interface to Giac, a free, basic computer algebra system.

NaN

#### Scientific or technical computing

See also [Wikipedia:Comparison of numerical analysis software](https://en.wikipedia.org/wiki/Comparison_of_numerical_analysis_software "wikipedia:Comparison of numerical analysis software").

*   **EngLab** — Cross-compile mathematical platform with a C like syntax.

NaN

*   **[Euler](https://en.wikipedia.org/wiki/Euler_(software) "wikipedia:Euler (software)")** — Numerical application designed for higher level math such as calculus, optimization, and statistics that uses Maxima for symbolic operations.

NaN

*   **[FreeMat](https://en.wikipedia.org/wiki/FreeMat "wikipedia:FreeMat")** — Matlab-like program that supports many of its functions and features a codeless interface to external C, C++, and Fortran code, further parallel distributed algorithm development (via MPI), and 3D visualization capabilities.

NaN

*   **[GNU Radio](/index.php/GNU_Radio "GNU Radio")** — Software development toolkit that provides signal processing blocks to implement software radios.

NaN

*   **[Octave](/index.php/Octave "Octave")** — [Matlab](/index.php/Matlab "Matlab")-like language and interface for numerical computations.

NaN

*   **[PyLab](https://en.wikipedia.org/wiki/matplotlib "wikipedia:matplotlib")** — Collection of Python modules (pyplot, numpy, etc.) used for scientific calculations.

NaN

*   **[Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")** — Mathematics software system, that combines many existing open-source packages into a common Python interface. Alternative to Magma, Maple, Mathematica and Matlab.

NaN

*   **[Scilab](https://en.wikipedia.org/wiki/Scilab "wikipedia:Scilab")** — Matlab alternative used for numerical computations. Its syntax is not equivalent to that of Matlab, but it can be easily converted.

NaN

#### Statistics

See also [Wikipedia:Comparison of statistical packages](https://en.wikipedia.org/wiki/Comparison_of_statistical_packages "wikipedia:Comparison of statistical packages").

*   **[JAGS](https://en.wikipedia.org/wiki/Just_another_Gibbs_sampler "wikipedia:Just another Gibbs sampler") (Just another Gibbs sampler)** — Cross-platform program for analysis of Bayesian hierarchical models using Markov Chain Monte Carlo (MCMC) simulation.

NaN

*   **[Python Data Analysis Library (pandas)](https://en.wikipedia.org/wiki/Pandas_(software) "wikipedia:Pandas (software)")** — Providing high-performance, easy-to-use data structures and data analysis tools with Python programming language.

NaN

*   **[PSPP](https://en.wikipedia.org/wiki/PSPP "wikipedia:PSPP")** — Free SPSS implementation.

NaN

*   **[R](/index.php/R "R")** — Software environment for statistical computing and graphics.

NaN

*   **[RKWard](https://en.wikipedia.org/wiki/RKWard "wikipedia:RKWard")** — Frontend for the statistical language R.

NaN

*   **[RStudio](https://en.wikipedia.org/wiki/RStudio "wikipedia:RStudio")** — A powerful and productive IDE for R written in Qt.

NaN

#### Data evaluation

See also [Wikipedia:List of information graphics software](https://en.wikipedia.org/wiki/List_of_information_graphics_software "wikipedia:List of information graphics software").

*   **Extrema** — Visualization and data analysis tool.

NaN

*   **[Fityk](https://en.wikipedia.org/wiki/Fityk "wikipedia:Fityk")** — Curve fitting and data analysis application, predominantly used to fit analytical, bell-shaped functions to experimental data.

NaN

*   **[Gnuplot](https://en.wikipedia.org/wiki/gnuplot "wikipedia:gnuplot")** — Command-line program that can generate 2D and 3D plots of functions, data, and data fits.

NaN

*   **[Grace](https://en.wikipedia.org/wiki/Grace_(plotting_tool) "wikipedia:Grace (plotting tool)")** — WYSIWYG 2D graph plotting tool.

NaN

*   **[LabPlot](https://en.wikipedia.org/wiki/LabPlot "wikipedia:LabPlot")** — Free software data analysis and visualization application, similar to SciDAVis.

NaN

*   **[QtiPlot](https://en.wikipedia.org/wiki/QtiPlot "wikipedia:QtiPlot")** — Platform-independent application used for interactive scientific graphing and data analysis, similar to the proprietary [Origin](https://en.wikipedia.org/wiki/Origin_(software) "wikipedia:Origin (software)") or [SigmaPlot](https://en.wikipedia.org/wiki/SigmaPlot "wikipedia:SigmaPlot").

NaN

*   **[ROOT](https://en.wikipedia.org/wiki/ROOT "wikipedia:ROOT")** — Data analysis program and library (originally for particle physics) developed by CERN.

NaN

*   **[SciDAVis](https://en.wikipedia.org/wiki/SciDAVis "wikipedia:SciDAVis")** — Fork of QtiPlot with the goal of being better documented and more user friendly.

NaN

See also [List of applications#Spreadsheets](/index.php/List_of_applications#Spreadsheets "List of applications")

### Chemistry and biology

#### Computational biology and bioinformatics

See also [Wikipedia:List of open source bioinformatics software](https://en.wikipedia.org/wiki/List_of_open_source_bioinformatics_software "wikipedia:List of open source bioinformatics software").

*   **[BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL") (Biochemical Algorithms Library)** — Application framework in C++ that provides an extensive set of data structures as well as classes for molecular mechanics, advanced solvation methods, comparison and analysis of protein structures, file import/export, and visualization.

NaN

*   **[BioJava](https://en.wikipedia.org/wiki/BioJava "wikipedia:BioJava")** — Set of Java tools for computational biology, as well as bioinformatics.

NaN

*   **[Biopython](https://en.wikipedia.org/wiki/Biopython "wikipedia:Biopython")** — Python package with tools for computational biology, as well as bioinformatics.

NaN

*   **[EMBOSS](https://en.wikipedia.org/wiki/EMBOSS "wikipedia:EMBOSS") (European Molecular Biology Open Software Suite)** — Open source software analysis package specially developed for the needs of the molecular biology and bioinformatics user community.

NaN

*   **[MEGA](https://en.wikipedia.org/wiki/MEGA,_Molecular_Evolutionary_Genetics_Analysis "wikipedia:MEGA, Molecular Evolutionary Genetics Analysis") (Molecular Evolutionary Genetics Analysis)** — Integrated tool for conducting automatic and manual sequence alignment, inferring phylogenetic trees, mining web-based databases, estimating rates of molecular evolution, inferring ancestral sequences, and testing evolutionary hypotheses.

NaN

*   **[MUMmer](https://en.wikipedia.org/wiki/MUMmer "wikipedia:MUMmer")** — Bioinformatics software system for sequence alignment based on suffix trees.

NaN

*   **[UGENE](https://en.wikipedia.org/wiki/UGENE "wikipedia:UGENE")** — Application that integrates dozens of well-known biological tools and algorithms, providing both graphical user and command-line interfaces.

NaN

#### Molecules

##### Viewers

See also [Wikipedia:List of molecular graphics systems](https://en.wikipedia.org/wiki/List_of_molecular_graphics_systems "wikipedia:List of molecular graphics systems").

*   **[Avogadro](https://en.wikipedia.org/wiki/Avogadro_(software) "wikipedia:Avogadro (software)")** — Editor, viewer and simulator for 3D molecule structures (also supports downloading files from the [Protein Data Bank](https://en.wikipedia.org/wiki/Protein_Data_Bank "wikipedia:Protein Data Bank")).

NaN

*   **BALLView** — Standalone molecular modeling and visualization application, part of the [BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL") framework.

NaN

*   **[Ghemical](https://en.wikipedia.org/wiki/Ghemical "wikipedia:Ghemical")** — Computational chemistry software package used to edit, view and simulate molecular structures.

NaN

*   **[PyMOL](https://en.wikipedia.org/wiki/PyMOL "wikipedia:PyMOL")** — Open-source molecular visualization system that can produce high quality 3D images of small molecules and biological macromolecules, such as proteins.

NaN

*   **[RasMol](https://en.wikipedia.org/wiki/RasMol "wikipedia:RasMol")** — Computer program written for molecular graphics visualization intended and used primarily for the depiction and exploration of biological macromolecule structures.

NaN

##### Drawing

*   **[BKChem](https://en.wikipedia.org/wiki/BKchem "wikipedia:BKchem")** — Practical and goodlooking skeletal formula molecule drawing program.

NaN

*   **[Chemtool](https://en.wikipedia.org/wiki/Chemtool "wikipedia:Chemtool")** — GTK+-based program for drawing chemical structural formulas.

NaN

*   **EasyChem** — Simple skeletal formula molecule drawing program with a focus on producing press-quality figures.

NaN

*   **[Gabedit](https://en.wikipedia.org/wiki/Gabedit "wikipedia:Gabedit")** — Graphical user interface to computational chemistry packages like [GAMESS](https://en.wikipedia.org/wiki/GAMESS_(US) "wikipedia:GAMESS (US)"), [Gaussian](https://en.wikipedia.org/wiki/Gaussian_(software) "wikipedia:Gaussian (software)"), [MOLCAS](https://en.wikipedia.org/wiki/MOLCAS "wikipedia:MOLCAS"), [MOLPRO](https://en.wikipedia.org/wiki/MOLPRO "wikipedia:MOLPRO"), [MPQC](https://en.wikipedia.org/wiki/MPQC "wikipedia:MPQC"), [OpenMopac](https://en.wikipedia.org/wiki/MOPAC "wikipedia:MOPAC"), [Firefly](https://en.wikipedia.org/wiki/PC_GAMESS "wikipedia:PC GAMESS") (previously PC GAMESS) and [Q-Chem](https://en.wikipedia.org/wiki/Q-Chem "wikipedia:Q-Chem").

NaN

*   **[XDrawChem](https://en.wikipedia.org/wiki/XDrawChem "wikipedia:XDrawChem")** — Extensive skeletal formula molecule drawing program (includes spectroscopy prediction).

NaN

##### Modeling

*   **[GROMACS](/index.php/GROMACS "GROMACS") (GROningen MAchine for Chemical Simulations)** — Versatile package to perform molecular dynamics, i.e. simulate the Newtonian equations of motion for systems with hundreds to millions of particles.

NaN

*   **[Quantum ESPRESSO](https://en.wikipedia.org/wiki/Quantum_ESPRESSO "wikipedia:Quantum ESPRESSO")** — Integrated suite of applications for electronic-structure calculations and materials modeling at nanoscale. It is based on density-functional theory, plane waves, and pseudopotentials (both norm-conserving and ultrasoft).

NaN

#### Periodic table

*   **gElemental** — Periodic table of the elements with additional information.

NaN

*   **[Kalzium](https://en.wikipedia.org/wiki/Kalzium "wikipedia:Kalzium")** — Periodic table of the elements with molecule editor and equation solver from the [KDE](/index.php/KDE "KDE") desktop.

NaN

*   **eperiodique** — A simple Periodic Table Of Elements viewer using the EFL.

NaN

#### Biochemistry

*   **[Bioclipse](https://en.wikipedia.org/wiki/Bioclipse "wikipedia:Bioclipse")** — Java-based visual platform for biochemistry that uses the Eclipse Rich Client Platform (RCP).

NaN

#### Image manipulation

*   **[ImageJ](https://en.wikipedia.org/wiki/ImageJ "wikipedia:ImageJ")** — Java-based image processing and analysing program that provides extensibility via plugins and macros. It is widely used in microscopy (e.g. for cell counting).

NaN

*   **[Fiji](https://en.wikipedia.org/wiki/FIJI_(software) "wikipedia:FIJI (software)")** — ImageJ distribution (and soon ImageJ2) with a lot of plugins organized into a coherent menu structure.

NaN

### Astronomy

*   **[Celestia](https://en.wikipedia.org/wiki/Celestia "wikipedia:Celestia")** — 3D astronomy simulation program that allows users to travel through an extensive universe, modeled after reality, at any speed, in any direction and at any time in history.

NaN

*   **GIMP Astronomy Plugins** — Set of GIMP plugins for astronomical image processing.

NaN

*   **GoQat** — Camera acquisition software, especially for QSI cameras, that provides other features such as autoguiding, focusing help and others.

NaN

*   **[KStars](https://en.wikipedia.org/wiki/KStars "wikipedia:KStars")** — Planetarium application that provides an accurate graphical simulation of the night sky, from any location on Earth, at any date and time. It is included in KDE Edu.

NaN

*   **Open PHD Guiding** — Telescope autoguiding software based on the famous PHD Guiding.

NaN

*   **Qastrocam-g2** — Webcam acquisition software for planetary imaging.

NaN

*   **[Skychart / Cartes du Ciel](https://en.wikipedia.org/wiki/Cartes_du_Ciel "wikipedia:Cartes du Ciel")** — Planetarium that maps out and labels most of the constellations, planets, and objects you can see with a telescope. It can also download Digitized Sky Survey Charts and superimpose images over these charts.

NaN

*   **StarPlot** — 3-dimensional star chart viewer.

NaN

*   **[Stellarium](https://en.wikipedia.org/wiki/Stellarium_(computer_program) "wikipedia:Stellarium (computer program)")** — Beautiful 3D planetarium that uses OpenGL to render a realistic sky in real time.

NaN

*   **[XEphem](https://en.wikipedia.org/wiki/XEphem "wikipedia:XEphem")** — Motif-based ephemeris and planetarium program.

NaN

### Physics

#### Electronics

See also [Wikipedia:Comparison of EDA software](https://en.wikipedia.org/wiki/Comparison_of_EDA_software "wikipedia:Comparison of EDA software").

##### Digital logic

Digital logic software are mainly simple educational tools that intended for only designing and simulating logic circuits.

*   **atanua** — Real time logic simulator.

NaN

*   **eqntott** — Utility to convert a set of boolean logic equations to a PLA-esque truth table.

NaN

*   **espresso** — Heuristic logic minimizer, reduces the amount of gates required for digital circuits.

NaN

*   **giraffe** — A simple logic circuit simulator written in Java.

NaN

*   **glogic** — An educational graphical logic circuit simulator.

NaN

*   **KLogic** — Digital logic design and simulation software for KDE which also simulate karnaugh diagrams.

NaN

*   **Logisim** — Educational digital logic design and simulation software, written in Java, officially its development has stopped.

NaN

*   **Logisim Evolution** — Project which continue the development of the original Logisim with new features, written in Java.

NaN

*   **SmartSim** — Simple and beautiful digital logic circuit design and simulation software, mainly target teachers and students, very lightweight and cross platform, GPL licensed, written in Vala.

NaN

##### HDL

*   **[Altera Design Software](/index.php/Altera_Design_Software "Altera Design Software")** — A set of design tools for Altera's FPGA chips that includes Quartus II and ModelSim-Altera.

NaN

*   **[Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK")** — FPGA programmable logic design suit.

NaN

##### MCU IDE

*   **[Arduino](/index.php/Arduino "Arduino")** — Arduino prototyping platform SDK.

NaN

*   **[KTechLab](https://en.wikipedia.org/wiki/KTechLab "wikipedia:KTechLab")** — IDE for electronic and PIC microcontroller circuit design and simulation featuring an extensive circuit designer with autorouting and simulation of all common electronic components and logic elements.

NaN

##### Schematic capture editor

*   **[gEDA](/index.php/GEDA "GEDA")** — Full suite and toolkit of Electronic Design Automation tools that are used for electrical circuit design, schematic capture, simulation, prototyping, and production.

NaN

*   **[KiCAD](https://en.wikipedia.org/wiki/KiCAD "wikipedia:KiCAD")** — Software suite for electronic design automation (EDA) that facilitates the design of schematics for electronic circuits and their conversion to PCB (printed circuit board).

NaN

*   **[Oregano](https://en.wikipedia.org/wiki/Oregano_(software) "wikipedia:Oregano (software)")** — Graphical software application for schematic capture and simulation of electrical circuits. The actual simulation is done by the [ngspice](https://en.wikipedia.org/wiki/Ngspice "wikipedia:Ngspice") or [Gnucap](https://en.wikipedia.org/wiki/GNU_Circuit_Analysis_Package "wikipedia:GNU Circuit Analysis Package") engines.

NaN

*   **QElectroTech** — Application used to draw advanced electrical circuits.

NaN

*   **[Qucs](https://en.wikipedia.org/wiki/Quite_Universal_Circuit_Simulator "wikipedia:Quite Universal Circuit Simulator")** — Electronics circuit simulator application that gives you the ability to set up a circuit with a graphical user interface and simulate its large-signal, small-signal and noise behaviour.

NaN

#### Physics simulation

*   **[Code_Aster](https://en.wikipedia.org/wiki/Code_Aster "wikipedia:Code Aster")** — Software package for Civil and Structural Engineering finite element analysis and numeric simulation in structural mechanics.

NaN

*   **[EPANET](https://en.wikipedia.org/wiki/EPANET "wikipedia:EPANET")** — EPANET performs extended period simulation of the water movement and quality behavior within pressurized pipe networks.

NaN

*   **[Step](https://en.wikipedia.org/wiki/Step_(software) "wikipedia:Step (software)")** — Two-dimensional physics simulation engine that is included in the KDE desktop as part of KDE Edu.

NaN

*   **[SWMM](https://en.wikipedia.org/wiki/SWMM "wikipedia:SWMM")** — Storm Water Management Model is a dynamic rainfall-runoff-subsurface runoff simulation model used for simulation of the surface/subsurface hydrology quantity and quality.

NaN

#### Unit conversion

*   **ConvertAll** — Unit conversion application that allows one to combine units in any way (e.g. inches per decade), even if it does not make sense.

NaN

*   **Gonvert** — Conversion utility that allows conversion between many units like CGS, Ancient, Imperial with many categories like length, mass, numbers, etc.

NaN

*   **[Units](https://en.wikipedia.org/wiki/GNU_Units "wikipedia:GNU Units")** — Command-line unit converter and calculator that can handle multiplicative scale changes, nonlinear conversions such as Fahrenheit to Celsius or wire gauge and others.

NaN

## Others

### Work environment

The default installation of Arch provides Bash as shell interpreter and does not contain any Desktop Environment, therefore forces users to choose one themselves. Most Arch boxes run some X11 Window Manager and/or Desktop Environment, but of course there are still people who prefer doing everyday tasks in bare console.

#### Bootsplash

See also [Wikipedia:Bootsplash](https://en.wikipedia.org/wiki/Bootsplash "wikipedia:Bootsplash").

*   **[Fbsplash](/index.php/Fbsplash "Fbsplash")** — Gentoo implementation as bootsplash program

NaN

*   **[Plymouth](/index.php/Plymouth "Plymouth")** — The new graphical boot process for Fedora, replacing the aging Red Hat Graphical Boot

NaN

*   **[Splashy](/index.php/Splashy "Splashy")** — A graphical boot process designed to replace the aging Bootsplash program

NaN

#### Command shells

See the main article: [Command-line shell](/index.php/Command-line_shell "Command-line shell").

See also [Wikipedia:Comparison of command shells](https://en.wikipedia.org/wiki/Comparison_of_command_shells "wikipedia:Comparison of command shells").

#### Terminal multiplexers

*   **abduco** — Tool for session attach and detach support which allows a process to run independently from its controlling terminal.

NaN

*   **dtach** — Program that emulates the detach feature of [screen](/index.php/Screen "Screen").

NaN

*   **[GNU Screen](/index.php/GNU_Screen "GNU Screen")** — Full-screen window manager that multiplexes a physical terminal.

NaN

*   **[tmux](/index.php/Tmux "Tmux")** — BSD licensed terminal multiplexer.

NaN

*   **[byobu](https://en.wikipedia.org/wiki/Byobu_(software) "wikipedia:Byobu (software)")** — An GPLv3 licensed addon for tmux or screen. It requires a terminal multiplexer installed.

NaN

#### Desktop environments

See the main article: [Desktop environment#List of desktop environments](/index.php/Desktop_environment#List_of_desktop_environments "Desktop environment").

See also [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

#### Window managers

##### Console

See also [#Terminal multiplexers](#Terminal_multiplexers), which offer some of the functions of window managers for the console.

*   **dvtm** — [dwm](/index.php/Dwm "Dwm")-style window manager in the console.

NaN

*   **twin** — Text-mode window manager.

NaN

##### Graphical

See the main article: [Window manager#List of window managers](/index.php/Window_manager#List_of_window_managers "Window manager").

See also [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers").

#### Window tilers

*   **[PyTyle3](/index.php/PyTyle "PyTyle")** — An automatic tiler that is compatible with Openbox Multihead with faster action and lower memory footprint.

NaN

*   **PyWO** — Allows you to easily organize windows on the desktop using keyboard shortcuts.

NaN

*   **QuickTile** — Lightweight standalone alternative to Compiz Grid plugin.

NaN

*   **stiler** — A simple python script to convert any wm to tiling wm.

NaN

*   **[Tile-windows](/index.php/Tile-windows "Tile-windows")** — Tool for tiling windows horizontally or vertically.

NaN

*   **whaw** — Window manager independent window layout tool.

NaN

*   **wumwum** — The Window Manager manager. It can turn emwh compliant window managers into a tiling window manager while retaining all initial functionalities.

NaN

#### Virtual desktop pagers

See also [Wikipedia:Pager (GUI)](https://en.wikipedia.org/wiki/Pager_(GUI) "wikipedia:Pager (GUI)").

*   **bbpager** — Dockable pager for [blackbox](/index.php?title=Blackbox&action=edit&redlink=1 "Blackbox (page does not exist)") and other window managers.

NaN

*   **fbpager** — Virtual desktop pager for fluxbox.

NaN

*   **IPager** — A configurable pager with transparency, originally developed for Fluxbox.

NaN

*   **Neap** — An non-intrusive and light pager that runs in the notification area of your panel.

NaN

*   **Netwmpager** — A NetWM/EWMH compatible pager.

NaN

*   **obpager** — Pager for [Openbox](/index.php/Openbox "Openbox") writen in C++.

NaN

*   **Pager** — A highly configurable pager compatible with Openbox Multihead.

NaN

#### Support applications

##### Login managers

See the main article: [Display manager#List of display managers](/index.php/Display_manager#List_of_display_managers "Display manager").

##### Composite managers

See the main article: [Xorg#List of composite managers](/index.php/Xorg#List_of_composite_managers "Xorg").

##### Taskbars / panels / docks

*   **[Avant Window Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")** — Lightweight dock which sits at the bottom of the screen.

NaN

*   **[Bmpanel](/index.php/Bmpanel "Bmpanel")** — Lightweight, NETWM compliant panel.

NaN

*   **[Cairo-Dock](/index.php/Cairo-Dock "Cairo-Dock")** — Highly customizable dock and launcher application.

NaN

*   **Daisy** — KDE Plasma widget which acts as a dock.

NaN

*   **Docker** — Docking application which acts as a system tray.

NaN

*   **[Docky](https://en.wikipedia.org/wiki/Docky "wikipedia:Docky")** — Full fledged dock application that makes opening common applications and managing windows easier and quicker.

NaN

*   **[fbpanel](/index.php/Fbpanel "Fbpanel")** — Lightweight, NETWM compliant desktop panel.

NaN

*   **[GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")** — Panel included in the [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") desktop.

NaN

*   **KoolDock** — KDE3 docker with great effects that tries to resemble the OS X dock.

NaN

*   **LXPanel** — Lightweight X11 desktop panel and part of the LXDE desktop.

NaN

*   **MATE Panel** — Panel included in the [MATE](/index.php/MATE "MATE") desktop.

NaN

*   **PerlPanel** — The ideal accompaniment to a light-weight Window Manager such as OpenBox, or a desktop-drawing program like iDesk.

NaN

*   **plank** — Elegant, simple, clean dock from [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

NaN

*   **[PyPanel](/index.php/PyPanel "PyPanel")** — Lightweight panel/taskbar written in Python and C.

NaN

*   **qtpanel** — Project to create useful and beautiful panel in Qt.

NaN

*   **[Stalonetray](/index.php/Stalonetray "Stalonetray")** — Stand-alone system tray.

NaN

*   **[Tint2](/index.php/Tint2 "Tint2")** — Simple panel/taskbar developed specifically for Openbox.

NaN

*   **Trayer** — Lightweight GTK+-based systray.

NaN

*   **wbar** — Quick launch bar developed with speed in mind.

NaN

*   **Xfce Panel** — Panel included in the [Xfce](/index.php/Xfce "Xfce") desktop.

NaN

##### Application launchers

See also [Wikipedia:Comparison of desktop application launchers](https://en.wikipedia.org/wiki/Comparison_of_desktop_application_launchers "wikipedia:Comparison of desktop application launchers").

*   **ADeskBar** — Easy, simple and unobtrusive application launcher for Openbox.

NaN

*   **Albert** — An application launcher inspired by Alfred.

NaN

*   **Ayr** — Manages menus of application launchers, either executables or desktop files. Also opens files and URLs with launchers, desktop files, or applications associated by name or mimetype. Uses dmenu to manage its menus.

NaN

*   **Bashrun2** — Provides a different, barebones approach to a run dialog, using a specialized Bash session within a small xterm window.

NaN

*   **[dmenu](/index.php/Dmenu "Dmenu")** — Fast and lightweight dynamic menu for X which is also useful as an application launcher.

NaN

*   **dmenu-extended** — An extension to _dmenu_ for quickly opening files and folders.

NaN

*   **dmenu-launch** — Simple _dmenu_-based application launcher. Launches binaries and XDG shortcuts.

NaN

*   **dswitcher** — _dmenu_-based window switcher that works regardless of workspace or minimization.

NaN

*   **Fehlstart** — Small GTK+-based application launcher.

NaN

*   **[Gmrun](/index.php/Gmrun "Gmrun")** — Lightweight GTK+-based application launcher, with the ability to run programs inside a terminal and other handy features.

NaN

*   **[GNOME Do](https://en.wikipedia.org/wiki/GNOME_Do "wikipedia:GNOME Do")** — Application launcher inspired by [Quicksilver](https://en.wikipedia.org/wiki/Quicksilver_(software) "wikipedia:Quicksilver (software)") with many plugins, originally developed for the GNOME desktop.

NaN

*   **j4-dmenu-desktop** — Very fast dmenu application launcher.

NaN

*   **Kupfer** — Convenient command and access tool for the GNOME desktop that can launch applications, open documents and access different types of objects and act on them.

NaN

*   **[Launchy](https://en.wikipedia.org/wiki/Launchy "wikipedia:Launchy")** — Very popular cross-platform application launcher with a plugin-based system used to provide extra functionality.

NaN

*   **Lighthouse** — A simple scriptable popup dialog to run on X.

NaN

*   **rofi** — A popup window switcher roughly based on superswitcher, requiring only xlib and pango.

NaN

*   **slingshot** — An application launcher has a clear look, part of [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

NaN

*   **Synapse** — Synapse is a semantic launcher written in Vala that you can use to start applications as well as find and access relevant documents and files by making use of the Zeitgeist engine.

NaN

*   **Whippet** — A launcher and xdg-open replacement for control freaks. Opens files and URLs with applications associated by name and/or mimetype. Applications and associations may be customized using an SQLite database. Uses dmenu to manage its menus.

NaN

*   **xboomx** — Light _dmenu_ wrapper that reorders commands based on popularity, written in Python.

NaN

*   **xfce4-appfinder** — An eazy-to-use application launcher from Xfce.

NaN

*   **Yeganesh** — Light _dmenu_ wrapper that reorders commands based on popularity, written in Haskell.

NaN

##### Logout dialogue

A few simple shutdown managers are available:

*   **exitx** — A logout dialog for Openbox that uses [Sudo](/index.php/Sudo "Sudo").

NaN

*   **exitx-polkit** — A GTK logout dialog for Openbox with PolicyKit support.

NaN

*   **exitx-systemd** — A GTK logout dialog for Openbox with systemd support.

NaN

*   **oblogout** — A graphical logout script for [Openbox](/index.php/Openbox "Openbox") that may be used with other WMs.

NaN

*   **obshutdown** — A great GTK/Cairo based shutdown manager for Openbox and other window managers.

NaN

#### Accessibility

##### Screen reading

*   **Orca** — Screen reader for individuals who are blind or visually impaired

NaN

*   **[Simple Orca Plugin System](/index.php/Simple_Orca_Plugin_System "Simple Orca Plugin System")** — Plug-in extension for the Orca screen reader

NaN

##### Speech recognition

See the main article [Speech recognition](/index.php/Speech_recognition "Speech recognition") for applications.

### Finance

See also [Wikipedia:Comparison of accounting software](https://en.wikipedia.org/wiki/Comparison_of_accounting_software "wikipedia:Comparison of accounting software").

*   **esniper** — Simple, lightweight tool for [sniping](https://en.wikipedia.org/wiki/Auction_sniping "wikipedia:Auction sniping") eBay auctions.

NaN

*   **[GnuCash](https://en.wikipedia.org/wiki/GnuCash "wikipedia:GnuCash")** — Financial application that implements a double-entry book-keeping system with features for small business accounting.

NaN

*   **[Grisbi](https://en.wikipedia.org/wiki/Grisbi "wikipedia:Grisbi")** — Personal finance system which manages third party, expenditure and receipt categories, as well as budgetary lines, financial years, and other information that makes it suitable for associations.

NaN

*   **[HomeBank](https://en.wikipedia.org/wiki/HomeBank "wikipedia:HomeBank")** — Easy to use finance manager that can analyse your personal finance in detail using powerful filtering tools and graphs.

NaN

*   **[KMyMoney](https://en.wikipedia.org/wiki/KMyMoney "wikipedia:KMyMoney")** — Personal finance manager that operates in a similar way to [Microsoft Money](https://en.wikipedia.org/wiki/Microsoft_Money "wikipedia:Microsoft Money"). It supports different account types, categorisation of expenses and incomes, reconciliation of bank accounts and import/export to the “QIF” file format.

NaN

*   **Ledger** — Ledger is a powerful, double-entry accounting system that is accessed from the UNIX command-line.

NaN

*   **Moneychanger** — An intuitive QT/C++ system tray client for _Open-Transactions_

NaN

*   **Manager Accounting** — Manager is free accounting software for small business.

NaN

*   **Money Manager EX** — An easy-to-use personal finance suite

NaN

*   **Skrooge** — Personal finances manager for the KDE desktop.

NaN

*   **openerp** — Open source erp system purely in python.

NaN

*   **Open-Transactions** — A financial cryptography library used for issuing currencies, stock, paying dividends, creating asset accounts, sending/receiving digital cash, trading on markets and escrow.

NaN

### Flashcards

*   **[Anki](/index.php/Anki "Anki")** — Anki is a program which makes remembering things easy.

NaN

*   **iGNUit** — Memorization aid based on the Leitner flashcard system.

NaN

*   **[Mnemosyne](/index.php/Mnemosyne "Mnemosyne")** — Free flash-card tool which optimizes your learning process.

NaN

### Time management

#### Console

*   **Calcurse** — Text-based ncurses calendar and scheduling system.

NaN

*   **Doneyet** — Ncurses-based hierarchical To-do list manager written in C++.

NaN

*   **Pal** — Very lightweight calendar with both interactive and non-interactive interfaces.

NaN

*   **[Remind](/index.php/Remind "Remind")** — Highly sophisticated text-based calendaring and notification system.

NaN

*   **[Taskwarrior](https://en.wikipedia.org/wiki/Taskwarrior "wikipedia:Taskwarrior")** — Command-line To-do list application with support for lua customization and more.

NaN

*   **Todo.txt** — Small command-line To-do manager.

NaN

*   **TuDu** — Ncurses-based hierarchical To-do list manager with vim-like keybindings.

NaN

*   **When** — Simple personal calendar program.

NaN

*   **Wyrd** — Text-based front-end to Remind, a calendar and alarm program used on UNIX and Linux computers.

NaN

*   **mail2rem** — Small script for importing *.ics calendars from Maildir to Remind calendar.

NaN

*   **DevTodo** — Is a small command line application for maintaining lists of tasks.

NaN

#### Graphical

*   **Calendar** — Calendar application for GNOME.

NaN

*   **Day Planner** — Program designed to help you easily plan and manage your time. It can manage appointments, birthdays and more.

NaN

*   **etm (Event and Task Manager)** — Simple application with a "Getting Things Done!" approach to handling events, tasks, activities, reminders and projects.

NaN

*   **Glista** — Simple GTK+ To-do list manager with notes support.

NaN

*   **GTG (Getting Things GNOME!)** — Personal tasks and To-do list items organizer for the GNOME desktop.

NaN

*   **Hamster** — Time tracking application that helps you to keep track on how much time you have spent during the day on activities you choose to track.

NaN

*   **[KOrganizer](https://en.wikipedia.org/wiki/Kontact#Organizer "wikipedia:Kontact")** — Calendar and scheduling program, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

NaN

*   **[Lightning](https://en.wikipedia.org/wiki/Lightning_(software) "wikipedia:Lightning (software)")** — Extension to Mozilla Thunderbird that provides calendar and task support.

NaN

*   **Orage** — GTK+ calendar and task manager often seen integrated with Xfce.

NaN

*   **Osmo** — GTK+ personal organizer, which includes calendar, tasks manager and address book modules.

NaN

*   **Outspline** — Extensible outliner with advanced time management features, supporting events with complex recurrence schemes.

NaN

*   **QTodoTxt** — A cross-platform UI client for `todo.txt` files (see [project's page](http://todotxt.com/))

NaN

*   **Rachota** — Portable time tracker for personal projects.

NaN

*   **Task Coach** — Simple open source To-do manager to manage personal tasks and To-do lists.

NaN

*   **[Tasque](https://en.wikipedia.org/wiki/Tasque_(software) "wikipedia:Tasque (software)")** — Easy quick task management app written in C Sharp.

NaN

*   **Tider** — Lightweight time tracking application (GTK+)

NaN

*   **TkRemind** — Sophisticated calendar and alarm program.

NaN

*   **wxRemind** — Python text and graphical frontend to Remind.

NaN

### Emulators

An emulator is a program which serves to replicate the functions of another platform or system so as to allow applications and games to be run in environments they were not programmed for.

**Note:** For possibly more up to date selection of emulators, try checking the [AUR 'emulators' category](https://aur.archlinux.org/packages.php?O=0&K=&do_Search=Go&detail=1&L=0&C=5&SeB=nd&SB=n&SO=a&PP=25)

**Warning:** Owning a high-level emulator is not illegal, but distribution of any type of copyrighted ROMs and unauthorized emulation (without written permission of the copyright holder allowing the user to do so) are **illegal**. Consequently, Arch Linux does not distribute this copyrighted content, including game ROMs and ripped console BIOSs. You are fully responsible for whatever usage of the emulators obtained from the [official repositories](/index.php/Official_repositories "Official repositories") or the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") you make, as well as any legal repercussion that result. Arch Linux bears no responsibility at all.

#### Consoles

See also [Wikipedia:List of video game console emulators](https://en.wikipedia.org/wiki/List_of_video_game_console_emulators "wikipedia:List of video game console emulators").

*   **Citra** — Nintendo 3DS emulator.

NaN

*   **DeSmuME** — Nintendo DS emulator.

NaN

*   **[Dolphin](/index.php/Dolphin_emulator "Dolphin emulator")** — Very capable GameCube and Wii emulator.

NaN

*   **epsxe** — Emulator for the PlayStation video game console for x86-based PC hardware.

NaN

*   **fakenes** — NES (Nintendo Famicom) emulator.

NaN

*   **FCEUX** — NTSC and PAL 8 bit Nintendo/Famicom emulator that is an evolution of the original FCE Ultra emulator. It is accurate, compatible and actively maintained.

NaN

*   **Gens2** — Emulator for Sega Genesis, Sega CD and 32X that is written in assembly language and no longer actively developed.

NaN

NaN

*   **Gens-GS** — Gens2, rewritten in C++, combining features from various Gens forks.

NaN

*   **gngeo** — Command-line NeoGeo emulator.

NaN

*   **higan** — Multisystem emulator focusing on accuracy, supporting SNES, NES, GB, GBC, GBA.

NaN

*   **mednafen** — Command line driven multi system emulator.

NaN

*   **Mupen64Plus** — Highly compatible Nintendo 64 emulator with plugin system.

NaN

*   **pSX** — A not plugin-based PlayStation emulator with fairly high compatibility.

NaN

*   **PCSXR** — PlayStation emulator; Debian fork of the abandoned original PCSX

NaN

*   **PCSX2** — PlayStation 2 emulator. It is still being maintained and developed. It requires BIOS files.

NaN

*   **snes-9x** — Portable, freeware Super Nintendo Entertainment System (SNES) emulator.

NaN

*   **[Visual Boy Advance](/index.php/Visual_Boy_Advance "Visual Boy Advance")** — Game Boy emulator with Game Boy Advance, Game Boy Color, and Super Game Boy support.

NaN

*   **ZSNES** — Highly compatible Super Nintendo emulator.

NaN

#### Other

*   **DOSBox** — Open-source DOS emulator which primarily focuses on running DOS Games.

NaN

*   **DOSEmu** — Open-source DOS emulator.

NaN

*   **MAME** — Multiple Arcade Machine Emulator.

NaN

*   **ResidualVM** — Cross-platform 3D game interpreter which allows you to play LucasArts' Lua-based 3D adventures.

NaN

*   **[RetroArch](/index.php/RetroArch "RetroArch")** — Frontend to libretro (emulation library, using modified versions of existing emulators as plugins).

NaN

*   **ScummVM** — Virtual machine for old school adventures.

NaN

*   **X Neko Project II** — PC-9801 emulator.

NaN

### Amateur radio

See the main article: [Amateur radio#Software list](/index.php/Amateur_radio#Software_list "Amateur radio").

See also [Wikipedia:List of software-defined radios](https://en.wikipedia.org/wiki/List_of_software-defined_radios "wikipedia:List of software-defined radios").

## See also

*   [List of terminal applications with their screenshots and reviews](http://kmandla.wordpress.com/software/)
*   [Arch Linux Forums / LnF Awards 2011](https://bbs.archlinux.org/viewtopic.php?id=111878) - The best Light & Fast apps of 2011
*   [Arch Linux Forums / LnF Awards 2012](https://bbs.archlinux.org/viewtopic.php?id=138281) - The best Light & Fast apps of 2012
*   [Survey: Vote for the most popular apps of 2013-2014](https://bbs.archlinux.org/viewtopic.php?id=174764)
*   [http://sourceforge.net/](http://sourceforge.net/) open source software
*   [http://www.oschina.net/](http://www.oschina.net/) open source china
*   [http://linuxappfinder.com/](http://linuxappfinder.com/)
*   [http://www.linuxlinks.com/](http://www.linuxlinks.com/)
*   [Wikipedia:List of open source software packages](https://en.wikipedia.org/wiki/List_of_open_source_software_packages "wikipedia:List of open source software packages")
*   [http://linuxappfinder.com/alternatives](http://linuxappfinder.com/alternatives) - Windows and OS X Software Alternatives
*   [http://alternativeto.net/](http://alternativeto.net/) - find alternatives to popular programs
*   [http://www.linuxalt.com/](http://www.linuxalt.com/) - Linux equivalents of Windows software
*   [http://lin-app.com/](http://lin-app.com/) - on-line information service of various commercial applications and games for Linux
*   [http://www.osalt.com/](http://www.osalt.com/)

Retrieved from "[https://wiki.archlinux.org/index.php?title=List_of_applications&oldid=396023](https://wiki.archlinux.org/index.php?title=List_of_applications&oldid=396023)"