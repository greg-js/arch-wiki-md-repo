****List of applications****

* * *

[Internet](/index.php/List_of_applications/Internet "List of applications/Internet") – [Multimedia](/index.php/List_of_applications/Multimedia "List of applications/Multimedia") – [Utilities](/index.php/List_of_applications/Utilities "List of applications/Utilities") – [Documents](/index.php/List_of_applications/Documents "List of applications/Documents") – [Security](/index.php/List_of_applications/Security "List of applications/Security") – [Science](/index.php/List_of_applications/Science "List of applications/Science") – [Other](/index.php/List_of_applications/Other "List of applications/Other")

This article is a general list of applications sorted by category, as a reference for those looking for packages. Many sections are split between console and graphical applications.

**Tip:**

*   This page exists primarily to make it easier to search for alternatives to an application that you do not know under which section has been added. Use the links in the template at the top to view the main sections as separate pages.
*   Please consider [installing](/index.php/Installing "Installing") the [pkgstats](/index.php/Pkgstats "Pkgstats") package, which provides a timer that sends a list of the packages installed on your system, along with the architecture and the mirrors you use, to the Arch Linux developers in order to help them prioritize their efforts and make the distribution even better. The information is sent anonymously and cannot be used to identify you. You can view the collected data at the [Statistics page](https://www.archlinux.de/?page=Statistics). More information is available in [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=105431).
*   Daemon packages usually include the relevant systemd unit file to [start](/index.php/Start "Start"); some packages even include different ones. After installation `pacman -Qql *package* | grep -Fe .service -e .socket` can be used to check and find the relevant one.

**Note:** Applications listed in "Console" sections can have graphical front-ends. Official ones are currently omitted.

## Contents

*   [1 Internet](#Internet)
    *   [1.1 Network managers](#Network_managers)
    *   [1.2 VPN clients](#VPN_clients)
    *   [1.3 Web browsers](#Web_browsers)
        *   [1.3.1 Console](#Console)
        *   [1.3.2 Graphical](#Graphical)
            *   [1.3.2.1 Gecko-based](#Gecko-based)
            *   [1.3.2.2 Blink-based](#Blink-based)
                *   [1.3.2.2.1 Chromium spin-offs](#Chromium_spin-offs)
                *   [1.3.2.2.2 Browsers based on electron](#Browsers_based_on_electron)
                *   [1.3.2.2.3 Browsers based on qt5-webengine](#Browsers_based_on_qt5-webengine)
            *   [1.3.2.3 WebKit-based](#WebKit-based)
                *   [1.3.2.3.1 Browsers based on webkit2gtk](#Browsers_based_on_webkit2gtk)
                *   [1.3.2.3.2 Browsers based on webkitgtk/webkitgtk2](#Browsers_based_on_webkitgtk.2Fwebkitgtk2)
                *   [1.3.2.3.3 Browsers based on qt5-webkit/qtwebkit](#Browsers_based_on_qt5-webkit.2Fqtwebkit)
            *   [1.3.2.4 Other](#Other)
    *   [1.4 File sharing](#File_sharing)
        *   [1.4.1 Download managers](#Download_managers)
        *   [1.4.2 FTP](#FTP)
            *   [1.4.2.1 FTP clients](#FTP_clients)
            *   [1.4.2.2 FTP servers](#FTP_servers)
        *   [1.4.3 Distributed file systems](#Distributed_file_systems)
        *   [1.4.4 BitTorrent clients](#BitTorrent_clients)
            *   [1.4.4.1 Console](#Console_2)
                *   [1.4.4.1.1 Command line / backend](#Command_line_.2F_backend)
                *   [1.4.4.1.2 Console Interface](#Console_Interface)
            *   [1.4.4.2 Graphical Interface](#Graphical_Interface)
                *   [1.4.4.2.1 libtorrent-rasterbar backend](#libtorrent-rasterbar_backend)
                *   [1.4.4.2.2 libktorrent backend](#libktorrent_backend)
                *   [1.4.4.2.3 others](#others)
        *   [1.4.5 Other P2P networks](#Other_P2P_networks)
        *   [1.4.6 Video downloaders](#Video_downloaders)
    *   [1.5 Communication](#Communication)
        *   [1.5.1 Email clients](#Email_clients)
            *   [1.5.1.1 Console](#Console_3)
            *   [1.5.1.2 Graphical](#Graphical_2)
        *   [1.5.2 Instant messaging](#Instant_messaging)
            *   [1.5.2.1 IRC clients](#IRC_clients)
                *   [1.5.2.1.1 Console](#Console_4)
                *   [1.5.2.1.2 Graphical](#Graphical_3)
            *   [1.5.2.2 XMPP (Jabber)](#XMPP_.28Jabber.29)
                *   [1.5.2.2.1 Command line](#Command_line)
                *   [1.5.2.2.2 Console clients](#Console_clients)
                *   [1.5.2.2.3 Graphical clients](#Graphical_clients)
                *   [1.5.2.2.4 Servers](#Servers)
            *   [1.5.2.3 Multi-protocol clients](#Multi-protocol_clients)
                *   [1.5.2.3.1 Console](#Console_5)
                *   [1.5.2.3.2 Graphical](#Graphical_4)
            *   [1.5.2.4 Lan messengers](#Lan_messengers)
        *   [1.5.3 VoIP / Softphone](#VoIP_.2F_Softphone)
            *   [1.5.3.1 Clients](#Clients)
                *   [1.5.3.1.1 SIP](#SIP)
                *   [1.5.3.1.2 IAX2](#IAX2)
                *   [1.5.3.1.3 Skype](#Skype)
                *   [1.5.3.1.4 Other](#Other_2)
                *   [1.5.3.1.5 Multi-protocol](#Multi-protocol)
            *   [1.5.3.2 Utilities](#Utilities)
        *   [1.5.4 Speech recognition](#Speech_recognition)
    *   [1.6 News, RSS, and blogs](#News.2C_RSS.2C_and_blogs)
        *   [1.6.1 News aggregators](#News_aggregators)
            *   [1.6.1.1 Console](#Console_6)
            *   [1.6.1.2 Graphical](#Graphical_5)
        *   [1.6.2 Podcast clients](#Podcast_clients)
        *   [1.6.3 Usenet newsreaders & newsgrabbers](#Usenet_newsreaders_.26_newsgrabbers)
        *   [1.6.4 Blog software](#Blog_software)
        *   [1.6.5 Microblogging clients](#Microblogging_clients)
    *   [1.7 Remote desktop](#Remote_desktop)
        *   [1.7.1 Remote desktop clients](#Remote_desktop_clients)
        *   [1.7.2 Remote desktop servers](#Remote_desktop_servers)
    *   [1.8 Pastebin clients](#Pastebin_clients)
    *   [1.9 Bitcoin](#Bitcoin)
    *   [1.10 Surveying](#Surveying)
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
    *   [2.4 Video](#Video)
        *   [2.4.1 Video players](#Video_players)
            *   [2.4.1.1 Console](#Console_8)
            *   [2.4.1.2 Graphical](#Graphical_7)
        *   [2.4.2 Subtitles](#Subtitles)
        *   [2.4.3 DVD ripping](#DVD_ripping)
        *   [2.4.4 Video editors](#Video_editors)
            *   [2.4.4.1 Console](#Console_9)
            *   [2.4.4.2 Graphical](#Graphical_8)
        *   [2.4.5 Screencast](#Screencast)
    *   [2.5 Mobile phone managers](#Mobile_phone_managers)
    *   [2.6 Digital camera managers](#Digital_camera_managers)
    *   [2.7 Optical media burning](#Optical_media_burning)
    *   [2.8 Podcasts](#Podcasts)
    *   [2.9 Collection managers](#Collection_managers)
    *   [2.10 Lyrics fetchers](#Lyrics_fetchers)
*   [3 Utilities](#Utilities_2)
    *   [3.1 Partitioning tools](#Partitioning_tools)
    *   [3.2 Mount tools](#Mount_tools)
        *   [3.2.1 Udisks](#Udisks)
    *   [3.3 Basic shell commands](#Basic_shell_commands)
    *   [3.4 getty](#getty)
    *   [3.5 Integrated development environments](#Integrated_development_environments)
    *   [3.6 Build automation](#Build_automation)
    *   [3.7 Terminal emulators](#Terminal_emulators)
        *   [3.7.1 VTE-based](#VTE-based)
        *   [3.7.2 KMS-based](#KMS-based)
        *   [3.7.3 framebuffer-based](#framebuffer-based)
    *   [3.8 Files](#Files)
        *   [3.8.1 File managers](#File_managers)
            *   [3.8.1.1 Console](#Console_10)
            *   [3.8.1.2 Graphical](#Graphical_9)
        *   [3.8.2 Desktop search engines](#Desktop_search_engines)
        *   [3.8.3 Archiving and compression tools](#Archiving_and_compression_tools)
            *   [3.8.3.1 Console](#Console_11)
            *   [3.8.3.2 Graphical](#Graphical_10)
        *   [3.8.4 Comparison, diff, merge](#Comparison.2C_diff.2C_merge)
        *   [3.8.5 Batch renamers](#Batch_renamers)
    *   [3.9 Disk cleaning](#Disk_cleaning)
    *   [3.10 Disk usage display](#Disk_usage_display)
    *   [3.11 Clock synchronization](#Clock_synchronization)
    *   [3.12 System maintenance](#System_maintenance)
    *   [3.13 System monitoring](#System_monitoring)
    *   [3.14 System information viewers](#System_information_viewers)
        *   [3.14.1 Console](#Console_12)
        *   [3.14.2 Graphical](#Graphical_11)
        *   [3.14.3 Others](#Others_2)
    *   [3.15 Keyboard layout switchers](#Keyboard_layout_switchers)
    *   [3.16 Power management](#Power_management)
    *   [3.17 Clipboard managers](#Clipboard_managers)
    *   [3.18 Wallpaper setters](#Wallpaper_setters)
    *   [3.19 Package management](#Package_management)
    *   [3.20 Input method editor](#Input_method_editor)
    *   [3.21 Trash management](#Trash_management)
    *   [3.22 File synchronization](#File_synchronization)
    *   [3.23 Finders](#Finders)
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
    *   [6.6 Geography](#Geography)
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
    *   [7.7 Display calibration](#Display_calibration)
        *   [7.7.1 Console](#Console_18)
        *   [7.7.2 Graphical](#Graphical_17)
*   [8 See also](#See_also)

## Internet

### Network managers

*   **[Connman](/index.php/Connman "Connman")** — Daemon for managing internet connections within embedded devices running the Linux operating system. Comes with a command-line client, plus Enlightenment, ncurses, GTK and Dmenu clients are available.

	[https://01.org/connman](https://01.org/connman) || [connman](https://www.archlinux.org/packages/?name=connman)

*   **[netctl](/index.php/Netctl "Netctl")** — Simple and robust tool to manage network connections via profiles. Intended for use with [systemd](/index.php/Systemd "Systemd").

	[https://projects.archlinux.org/netctl.git/](https://projects.archlinux.org/netctl.git/) || [netctl](https://www.archlinux.org/packages/?name=netctl)

*   **[NetworkManager](/index.php/NetworkManager "NetworkManager")** — Manager that provides wired, wireless, mobile broadband and OpenVPN detection with configuration and automatic connection.

	[https://wiki.gnome.org/Projects/NetworkManager](https://wiki.gnome.org/Projects/NetworkManager) || [networkmanager](https://www.archlinux.org/packages/?name=networkmanager)

*   **[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")** — Native [systemd](/index.php/Systemd "Systemd") daemon that manages network configuration. It includes support for basic network configuration through [udev](/index.php/Udev "Udev").

	[http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html) || [systemd](https://www.archlinux.org/packages/?name=systemd)

*   **[Wicd](/index.php/Wicd "Wicd")** — Wireless and wired connection manager with few dependencies. Comes with an ncurses interface, and a GTK interface [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) is available.

	[https://launchpad.net/wicd](https://launchpad.net/wicd) || [wicd](https://www.archlinux.org/packages/?name=wicd)

### VPN clients

*   **[OpenConnect](/index.php/OpenConnect "OpenConnect")** — Supports Cisco and Juniper VPNs.

	[http://www.infradead.org/openconnect/](http://www.infradead.org/openconnect/) || [openconnect](https://www.archlinux.org/packages/?name=openconnect)

*   **[PPTP Client](/index.php/PPTP_Client "PPTP Client")** — To connect to PPTP VPNs, like Microsoft VPNs (MPPE).

	[http://pptpclient.sourceforge.net/](http://pptpclient.sourceforge.net/) || [pptpclient](https://www.archlinux.org/packages/?name=pptpclient)

### Web browsers

See also [Wikipedia:Comparison of web browsers](https://en.wikipedia.org/wiki/Comparison_of_web_browsers "wikipedia:Comparison of web browsers").

#### Console

*   **[ELinks](https://en.wikipedia.org/wiki/ELinks "wikipedia:ELinks")** — Advanced and well-established feature-rich text mode web browser (Links fork, barely supported since 2009).

	[http://elinks.or.cz/](http://elinks.or.cz/) || [elinks](https://www.archlinux.org/packages/?name=elinks)

*   **[Links](https://en.wikipedia.org/wiki/Links_(web_browser) "wikipedia:Links (web browser)")** — Text WWW browser. Includes a console version [links] similar to Lynx, and a graphical X-window/framebuffer version [xlinks -g] (must be compiled in, Arch has both) with CSS, image rendering, pull-down menus.

	[http://links.twibright.com/](http://links.twibright.com/) || [links](https://www.archlinux.org/packages/?name=links)

*   **[Lynx](https://en.wikipedia.org/wiki/Lynx_(web_browser) "wikipedia:Lynx (web browser)")** — Text browser for the World Wide Web.

	[http://lynx.isc.org](http://lynx.isc.org) || [lynx](https://www.archlinux.org/packages/?name=lynx)

*   **retawq** — Interactive, multi-threaded network client (web browser) for text terminals.

	[http://retawq.sourceforge.net/](http://retawq.sourceforge.net/) || [retawq](https://aur.archlinux.org/packages/retawq/)

*   **[w3m](https://en.wikipedia.org/wiki/W3m "wikipedia:W3m")** — Pager/text-based web browser. It has vim-like keybindings, and is able to display images.

	[http://w3m.sourceforge.net/](http://w3m.sourceforge.net/) || [w3m](https://www.archlinux.org/packages/?name=w3m)

#### Graphical

##### Gecko-based

See also [Wikipedia:Gecko (software)](https://en.wikipedia.org/wiki/Gecko_(software) "wikipedia:Gecko (software)").

*   **[Conkeror](https://en.wikipedia.org/wiki/Conkeror "wikipedia:Conkeror")** — Keyboard-based browser modeled after [Emacs](/index.php/Emacs "Emacs") using [XULRunner](https://en.wikipedia.org/wiki/XULRunner "wikipedia:XULRunner"). Customizable via JavaScript.

	[http://conkeror.org/](http://conkeror.org/) || [conkeror](https://aur.archlinux.org/packages/conkeror/)

*   **[Firefox](/index.php/Firefox "Firefox")** — Extensible browser from Mozilla based on Gecko with fast rendering.

	[https://mozilla.com/firefox](https://mozilla.com/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

*   **[GNU IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat")** — A customized build of Firefox ESR distributed by the GNU Project, stripped of non-free components and with additional privacy extensions. Release cycle may be delayed compared to Mozilla Firefox.

	[https://www.gnu.org/software/gnuzilla/](https://www.gnu.org/software/gnuzilla/) || [icecat](https://aur.archlinux.org/packages/icecat/) or [icecat-bin](https://aur.archlinux.org/packages/icecat-bin/)

*   **[SeaMonkey](https://en.wikipedia.org/wiki/SeaMonkey "wikipedia:SeaMonkey")** — Continuation of the Mozilla Internet Suite.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

##### Blink-based

See also [Wikipedia:Blink (layout engine)](https://en.wikipedia.org/wiki/Blink_(layout_engine) "wikipedia:Blink (layout engine)").

*   **[Chromium](/index.php/Chromium "Chromium")** — Web browser developed by Google, the open source project behind Google Chrome.

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

###### Chromium spin-offs

*   **[Google Chrome](/index.php/Google_Chrome "Google Chrome")** — Proprietary web browser developed by Google.

	[https://www.google.com/chrome/](https://www.google.com/chrome/) || [google-chrome](https://aur.archlinux.org/packages/google-chrome/)

*   **Inox** — A privacy-focused patchset for Chromium, which disables Google services, proprietary features, prevents "calling home" and unhides all extensions.

	[https://github.com/gcarq/inox-patchset](https://github.com/gcarq/inox-patchset) || [inox](https://aur.archlinux.org/packages/inox/) or [inox-bin](https://aur.archlinux.org/packages/inox-bin/)

*   **Iridium** — A privacy-focused [patchset](https://git.iridiumbrowser.de/cgit.cgi/iridium-browser/tree/?h=patchview) for Chromium. See [differences from Chromium](https://github.com/iridium-browser/iridium-browser/wiki/Differences-between-Iridium-and-Chromium).

	[https://iridiumbrowser.de/](https://iridiumbrowser.de/) || [iridium](https://aur.archlinux.org/packages/iridium/)

*   **[Opera](/index.php/Opera "Opera")** — Highly customizable proprietary browser with focuses on an adherence to web rendering standards.

	[https://opera.com](https://opera.com) || [opera](https://www.archlinux.org/packages/?name=opera)

*   **[Slimjet](https://en.wikipedia.org/wiki/SlimBrowser "wikipedia:SlimBrowser")** — Fast, smart and powerful proprietary browser based on Chromium.

	[http://www.slimjet.com/](http://www.slimjet.com/) || [slimjet](https://aur.archlinux.org/packages/slimjet/)

*   **[Vivaldi](/index.php/Vivaldi "Vivaldi")** — An advanced proprietary browser made with the power user in mind.

	[https://vivaldi.com/](https://vivaldi.com/) || [vivaldi](https://aur.archlinux.org/packages/vivaldi/)

*   **[Yandex Browser](https://en.wikipedia.org/wiki/Yandex_Browser "wikipedia:Yandex Browser")** — Proprietary browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier.

	[https://browser.yandex.com/](https://browser.yandex.com/) || [yandex-browser-beta](https://aur.archlinux.org/packages/yandex-browser-beta/)

###### Browsers based on electron

*   **[Brave](https://en.wikipedia.org/wiki/Brave_(web_browser) "wikipedia:Brave (web browser)")** — Web browser that blocks ads and trackers by default. Based on the [Electron](http://electron.atom.io/) platform.

	[https://www.brave.com/](https://www.brave.com/) || [brave](https://aur.archlinux.org/packages/brave/)

*   **Min** — A smarter, faster web browser based on the [Electron](http://electron.atom.io/) platform.

	[https://minbrowser.github.io/min/](https://minbrowser.github.io/min/) || [min](https://aur.archlinux.org/packages/min/)

###### Browsers based on qt5-webengine

*   **Liri** — A minimalistic material design web browser written for Papyros.

	[http://liriproject.me/browser](http://liriproject.me/browser) || [liri-browser](https://aur.archlinux.org/packages/liri-browser/)

*   **Qt WebBrowser** — Browser for embedded devices developed using the capabilities of Qt and Qt WebEngine.

	[http://doc.qt.io/QtWebBrowser/](http://doc.qt.io/QtWebBrowser/) || [qtwebbrowser](https://aur.archlinux.org/packages/qtwebbrowser/)

*   **[QupZilla](https://en.wikipedia.org/wiki/QupZilla "wikipedia:QupZilla")** — New and very fast open source browser based on QtWebEngine, written in Qt framework.

	[http://www.qupzilla.com](http://www.qupzilla.com) || [qupzilla](https://www.archlinux.org/packages/?name=qupzilla)

##### WebKit-based

See also [Wikipedia:WebKit](https://en.wikipedia.org/wiki/WebKit "wikipedia:WebKit").

###### Browsers based on webkit2gtk

*   **[GNOME Web](/index.php/GNOME_Web "GNOME Web")** — Browser which uses the WebKitGTK+ rendering engine, part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

	[https://wiki.gnome.org/Apps/Web/](https://wiki.gnome.org/Apps/Web/) || [epiphany](https://www.archlinux.org/packages/?name=epiphany)

*   **[Lariza](/index.php/Lariza "Lariza")** — A simple, experimental web browser using GTK+ 3, GLib and WebKit2GTK+.

	[https://www.uninformativ.de/projects/lariza/](https://www.uninformativ.de/projects/lariza/) || [lariza](https://aur.archlinux.org/packages/lariza/)

*   **Rainbow Lollipop** — The visual history browser. In early state of development.

	[http://rainbow-lollipop.de/](http://rainbow-lollipop.de/) || [rainbow-lollipop-git](https://aur.archlinux.org/packages/rainbow-lollipop-git/)

*   **[Surf](/index.php/Surf "Surf") 2** — A simple web browser based on WebKit2GTK+. Experimental branch.

	[http://surf.suckless.org](http://surf.suckless.org) || [surf-webkit2gtk-git](https://aur.archlinux.org/packages/surf-webkit2gtk-git/)

*   **Webby** — Allows to use web apps as regular desktop apps, integrated with the OS, without tabs and using the default system launcher. In early state of development.

	[https://launchpad.net/webby-browser](https://launchpad.net/webby-browser) || [webby-browser-bzr](https://aur.archlinux.org/packages/webby-browser-bzr/)

###### Browsers based on webkitgtk/webkitgtk2

**Warning:** The following browsers are based on one of four WebKit ports that are today considered insecure and outdated. GTK+ browsers should be switching to webkit2gtk. More info [here](https://blogs.gnome.org/mcatanzaro/2016/02/01/on-webkit-security-updates/).

*   **[dwb](/index.php/Dwb "Dwb")** — Lightweight, highly customizable web browser based on the WebKit engine with *vi*-like shortcuts and tiling layouts. As of October 2014 *dwb* is [unmaintained](https://bitbucket.org/portix/dwb/pull-request/22/several-cleanups-to-increase-portability/diff#comment-3217936).

	[http://portix.bitbucket.org/dwb/](http://portix.bitbucket.org/dwb/) || [dwb](https://www.archlinux.org/packages/?name=dwb)

*   **[Jumanji](/index.php/Jumanji "Jumanji")** — Highly customizable and functional web browser.

	[http://pwmt.org/projects/jumanji](http://pwmt.org/projects/jumanji) || [jumanji-git](https://aur.archlinux.org/packages/jumanji-git/)

*   **[Luakit](/index.php/Luakit "Luakit")** — Highly configurable, micro-browser framework based on the WebKit engine and the GTK+ toolkit. It is very fast, extensible by Lua and licensed under the GNU GPLv3 license.

	[http://mason-larobina.github.com/luakit/](http://mason-larobina.github.com/luakit/) || [luakit](https://www.archlinux.org/packages/?name=luakit)

*   **[Midori](/index.php/Midori "Midori")** — Lightweight web browser based on GTK+ and WebKit.

	[http://midori-browser.org/](http://midori-browser.org/) || GTK+ 3: [midori](https://www.archlinux.org/packages/?name=midori), GTK+ 2: [midori-gtk2](https://www.archlinux.org/packages/?name=midori-gtk2)

*   **[Surf](/index.php/Surf "Surf")** — Lightweight WebKit-based browser, which follows the [suckless ideology](http://suckless.org/philosophy) (basically, the browser itself is a single C source file).

	[http://surf.suckless.org](http://surf.suckless.org) || [surf](https://www.archlinux.org/packages/?name=surf)

*   **[Uzbl](/index.php/UZBL-Browser "UZBL-Browser")** — Group of web interface tools which adhere to the Unix philosophy.

	[http://uzbl.org/](http://uzbl.org/) || [uzbl-browser](https://www.archlinux.org/packages/?name=uzbl-browser)

*   **vimb** — Fast and lightweight vim like web browser based on the webkit web browser engine and the GTK toolkit.

	[https://fanglingsu.github.io/vimb/](https://fanglingsu.github.io/vimb/) || [vimb](https://aur.archlinux.org/packages/vimb/)

*   **[Vimprobable](/index.php/Vimprobable "Vimprobable")** — Browser that behaves like the Vimperator plugin available for Mozilla Firefox. It is based on the WebKit engine and uses the GTK+ bindings.

	[http://sourceforge.net/apps/trac/vimprobable/](http://sourceforge.net/apps/trac/vimprobable/) || [vimprobable-git](https://aur.archlinux.org/packages/vimprobable-git/)

*   **[Xombrero](https://en.wikipedia.org/wiki/Xombrero "wikipedia:Xombrero")** — Webkit minimalist web browser (formerly known as *xxxterm*) with sophisticated security features designed-in, BSD style.

	[https://opensource.conformal.com/wiki/xombrero](https://opensource.conformal.com/wiki/xombrero) || [xombrero-git](https://aur.archlinux.org/packages/xombrero-git/)

###### Browsers based on qt5-webkit/qtwebkit

**Warning:** The following browsers are based on one of four WebKit ports that are today considered insecure and outdated. Qt browsers should be switching to qt5-webengine (Blink). More info [here](https://blogs.gnome.org/mcatanzaro/2016/02/01/on-webkit-security-updates/).

*   **[Arora](https://en.wikipedia.org/wiki/Arora_(web_browser) "wikipedia:Arora (web browser)")** — Cross-platform web browser built using QtWebKit. Development stopped in January 2012.

	[https://github.com/arora/arora](https://github.com/arora/arora) || [arora-git](https://aur.archlinux.org/packages/arora-git/)

*   **[Dooble](https://en.wikipedia.org/wiki/Dooble "wikipedia:Dooble")** — A safe WebKit Web browser.

	[http://dooble.sourceforge.net/](http://dooble.sourceforge.net/) || [dooble](https://aur.archlinux.org/packages/dooble/)

*   **Otter-browser** — Browser aiming to recreate classic Opera (12.x) UI using Qt5.

	[http://otter-browser.org/](http://otter-browser.org/) || [otter-browser](https://aur.archlinux.org/packages/otter-browser/)

*   **[qutebrowser](/index.php/Qutebrowser "Qutebrowser")** — A keyboard-driven, [vim](/index.php/Vim "Vim")-like browser based on PyQt5 and QtWebKit.

	[https://github.com/The-Compiler/qutebrowser](https://github.com/The-Compiler/qutebrowser) || [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser)

*   **[Rekonq](https://en.wikipedia.org/wiki/Rekonq "wikipedia:Rekonq")** — WebKit-based web browser for KDE.

	[http://rekonq.kde.org/](http://rekonq.kde.org/) || [rekonq](https://www.archlinux.org/packages/?name=rekonq)

##### Other

*   **[Dillo](https://en.wikipedia.org/wiki/Dillo "wikipedia:Dillo")** — Small, fast graphical web browser built on [FLTK](https://en.wikipedia.org/wiki/Fltk "wikipedia:Fltk"). Uses its own layout engine.

	[http://dillo.org/](http://dillo.org/) || [dillo](https://www.archlinux.org/packages/?name=dillo)

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Web browser based on Qt toolkit and KHTML layout engine, part of [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/).

	[http://konqueror.org/](http://konqueror.org/) || [kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)

*   **[NetSurf](https://en.wikipedia.org/wiki/NetSurf "wikipedia:NetSurf")** — Featherweight browser written in C, notable for its slowly developing JavaScript support and fast rendering through its own layout engine.

	[http://netsurf-browser.org](http://netsurf-browser.org) || [netsurf](https://www.archlinux.org/packages/?name=netsurf)

*   **[Pale Moon](https://en.wikipedia.org/wiki/Pale_Moon_(web_browser) layout engine, a fork of Gecko. Firefox add-ons may not be compatible. [[1]](https://addons.palemoon.org/firefox/incompatible/) Compiled for SSE2, with disabled optional code and no support for newer Firefox features such as cache2, e10s, and OTMC.

	[http://www.palemoon.org/](http://www.palemoon.org/) || [palemoon](https://aur.archlinux.org/packages/palemoon/)

### File sharing

#### Download managers

*   **[Gwget](https://en.wikipedia.org/wiki/Wget#GWget "wikipedia:Wget")** — Download manager for GNOME.

	[https://projects.gnome.org/gwget/](https://projects.gnome.org/gwget/) || [gwget](https://www.archlinux.org/packages/?name=gwget)

*   **[KGet](https://en.wikipedia.org/wiki/KGet "wikipedia:KGet")** — Download manager for KDE that supports HTTP(S), FTP and BitTorrent. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[http://www.kde.org/applications/internet/kget/](http://www.kde.org/applications/internet/kget/) || [kdenetwork-kget](https://www.archlinux.org/packages/?name=kdenetwork-kget)

*   **uGet** — GTK+ download manager featuring download classification and HTML import.

	[http://ugetdm.com/](http://ugetdm.com/) || [uget](https://www.archlinux.org/packages/?name=uget)

#### FTP

##### FTP clients

See also [Wikipedia:Comparison of FTP client software](https://en.wikipedia.org/wiki/Comparison_of_FTP_client_software "wikipedia:Comparison of FTP client software").

*   **[CurlFtpFS](/index.php/CurlFtpFS "CurlFtpFS")** — Filesystem for accessing FTP hosts; based on FUSE and libcurl.

	[http://curlftpfs.sourceforge.net/](http://curlftpfs.sourceforge.net/) || [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs)

*   **FatRat** — Download manager with support for HTTP, FTP, SFTP, BitTorrent, RapidShare and more.

	[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat-git](https://aur.archlinux.org/packages/fatrat-git/)

*   **[FileZilla](https://en.wikipedia.org/wiki/FileZilla "wikipedia:FileZilla")** — Fast and reliable FTP, FTPS and SFTP client.

	[http://filezilla-project.org/](http://filezilla-project.org/) || [filezilla](https://www.archlinux.org/packages/?name=filezilla)

*   **[gFTP](https://en.wikipedia.org/wiki/gFTP "wikipedia:gFTP")** — Multithreaded FTP client for Linux.

	[http://gftp.seul.org/](http://gftp.seul.org/) || [gftp](https://www.archlinux.org/packages/?name=gftp)

*   **[LFTP](https://en.wikipedia.org/wiki/Lftp "wikipedia:Lftp")** — Sophisticated command-line FTP client.

	[http://lftp.yar.ru/](http://lftp.yar.ru/) || [lftp](https://www.archlinux.org/packages/?name=lftp)

*   **LftpFS** — Read-only filesystem based on lftp (also supports HTTP, FISH, SFTP, HTTPS, FTPS and proxies).

	[http://lftpfs.sourceforge.net/](http://lftpfs.sourceforge.net/) || [lftpfs](https://aur.archlinux.org/packages/lftpfs/)

*   **ncftp** — A set of free application programs implementing FTP.

	[http://www.ncftp.com/](http://www.ncftp.com/) || [ncftp](https://www.archlinux.org/packages/?name=ncftp)

*   **[tnftp](https://en.wikipedia.org/wiki/tnftp "wikipedia:tnftp")** — FTP client with several advanced features for [NetBSD](https://en.wikipedia.org/wiki/NetBSD "wikipedia:NetBSD").

	[http://freecode.com/projects/tnftp](http://freecode.com/projects/tnftp) || [tnftp](https://www.archlinux.org/packages/?name=tnftp)

Some file managers like Dolphin, [GNOME Files](/index.php/GNOME_Files "GNOME Files") and [Thunar](/index.php/Thunar "Thunar") also provide FTP functionality.

##### FTP servers

*   **[bftpd](/index.php/Bftpd "Bftpd")** — Small, easy-to-configure FTP server

	[http://bftpd.sourceforge.net/](http://bftpd.sourceforge.net/) || [bftpd](https://www.archlinux.org/packages/?name=bftpd)

*   **[proFTPd](/index.php/Proftpd "Proftpd")** — A secure and configurable FTP server

	[http://www.proftpd.org/](http://www.proftpd.org/) || [proftpd](https://aur.archlinux.org/packages/proftpd/)

*   **[Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")** — Free (BSD-licensed), secure, production-quality and standard-compliant FTP server.

	[http://www.pureftpd.org/project/pure-ftpd](http://www.pureftpd.org/project/pure-ftpd) || [pure-ftpd](https://aur.archlinux.org/packages/pure-ftpd/)

*   **[vsftpd](/index.php/Vsftpd "Vsftpd")** — Lightweight, stable and secure FTP server for UNIX-like systems.

	[https://security.appspot.com/vsftpd.html](https://security.appspot.com/vsftpd.html) || [vsftpd](https://www.archlinux.org/packages/?name=vsftpd)

#### Distributed file systems

*   **[Ceph](/index.php/Ceph "Ceph")** — Distributed object store and file system designed to provide excellent performance, reliability and scalability.

	[https://ceph.com/](https://ceph.com/) || [ceph](https://www.archlinux.org/packages/?name=ceph)

*   **GlusterFS** — Cluster file system capable of scaling to several peta-bytes.

	[http://www.gluster.org/](http://www.gluster.org/) || [glusterfs](https://www.archlinux.org/packages/?name=glusterfs)

*   **Sheepdog** — Distributed object storage system for volume and container services and manages the disks and nodes intelligently.

	[https://sheepdog.github.io/sheepdog/](https://sheepdog.github.io/sheepdog/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Tahoe-LAFS](https://en.wikipedia.org/wiki/Tahoe-LAFS "wikipedia:Tahoe-LAFS")** — Tahoe Least-Authority Filesystem is a free and open, secure, decentralized, fault-tolerant, peer-to-peer distributed data store and distributed file system.

	[https://tahoe-lafs.org/](https://tahoe-lafs.org/) || [tahoe-lafs](https://aur.archlinux.org/packages/tahoe-lafs/)

#### BitTorrent clients

See also [Wikipedia:Comparison of BitTorrent clients](https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients "wikipedia:Comparison of BitTorrent clients").

##### Console

###### Command line / backend

Can be used as-is via command line, but all have a choice of front-end options as well.

*   **[aria2](/index.php/Aria2 "Aria2")** — Lightweight download utility that supports simultaneous adaptive downloading via HTTP(S), FTP, BitTorrent (DHT, PEX, MSE/PE) protocols and Metalink. It can run as a daemon controlled via a built-in JSON-RPC or XML-RPC interface.

	[http://aria2.sourceforge.net/](http://aria2.sourceforge.net/) || [aria2](https://www.archlinux.org/packages/?name=aria2)

*   **Ctorrent** — CTorrent is a BitTorrent client implemented in C++ to be lightweight and quick.

	[http://www.rahul.net/dholmes/ctorrent/](http://www.rahul.net/dholmes/ctorrent/) || [enhanced-ctorrent](https://aur.archlinux.org/packages/enhanced-ctorrent/)

*   **[MLDonkey](https://en.wikipedia.org/wiki/MLDonkey "wikipedia:MLDonkey")** — Multi-protocol P2P client that supports BitTorrent, HTTP, FTP, eDonkey and Direct Connect.

	[http://mldonkey.sourceforge.net/](http://mldonkey.sourceforge.net/) || [mldonkey](https://www.archlinux.org/packages/?name=mldonkey)

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with a daemon version, GTK+, Qt GUI, web and CLI front-ends.

	[http://transmissionbt.com/](http://transmissionbt.com/) || [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) (includes backend, daemon, command-line interface, and a Web UI interface)

###### Console Interface

*   **[rTorrent](/index.php/RTorrent "RTorrent")** — Simple and lightweight ncurses BitTorrent client. Requires [libtorrent](https://www.archlinux.org/packages/?name=libtorrent) backend.

	[https://rakshasa.github.io/rtorrent/](https://rakshasa.github.io/rtorrent/) || [rtorrent](https://www.archlinux.org/packages/?name=rtorrent)

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with a daemon version, ncurses CLI. Requires [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) backend.

	[http://transmissionbt.com/](http://transmissionbt.com/) || [transmission-remote-cli](https://www.archlinux.org/packages/?name=transmission-remote-cli)

##### Graphical Interface

###### libtorrent-rasterbar backend

*   **[Deluge](/index.php/Deluge "Deluge")** — User-friendly BitTorrent client written in PyGTK that can run as a daemon.

	[http://deluge-torrent.org/](http://deluge-torrent.org/) || [deluge](https://www.archlinux.org/packages/?name=deluge)

*   **FatRat** — Qt4 based download manager with support for HTTP, FTP, SFTP, BitTorrent, rapidshare and more. Written in C++.

	[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat-git](https://aur.archlinux.org/packages/fatrat-git/)

*   **[qBittorrent](https://en.wikipedia.org/wiki/qBittorrent "wikipedia:qBittorrent")** — Open source (GPLv2) BitTorrent client that strongly resembles µtorrent.

	[http://www.qbittorrent.org/](http://www.qbittorrent.org/) || [qbittorrent](https://www.archlinux.org/packages/?name=qbittorrent) [qbittorrent-nox](https://www.archlinux.org/packages/?name=qbittorrent-nox)

*   **[Tribler](https://en.wikipedia.org/wiki/Tribler "wikipedia:Tribler")** — 4th generation file sharing system bittorrent client.

	[http://www.tribler.org](http://www.tribler.org) || [tribler](https://aur.archlinux.org/packages/tribler/)

###### libktorrent backend

*   **[Ktorrent](/index.php/Ktorrent "Ktorrent")** — Feature-rich BitTorrent client for KDE.

	[http://ktorrent.org/](http://ktorrent.org/) || [ktorrent](https://www.archlinux.org/packages/?name=ktorrent)

###### others

*   **Tixati** — P2P client that uses the BitTorrent protocol.

	[http://www.tixati.com](http://www.tixati.com) || [tixati](https://aur.archlinux.org/packages/tixati/)

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with daemon version, GTK+, Qt GUI, web and CLI front-ends.

	[http://transmissionbt.com/](http://transmissionbt.com/) || [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk) [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt) [transmission-remote-gtk](https://aur.archlinux.org/packages/transmission-remote-gtk/) (remote clients work with the daemon in the -cli package)

*   **[Vuze](https://en.wikipedia.org/wiki/Vuze "wikipedia:Vuze")** — Feature-rich BitTorrent client written in Java (formerly Azureus).

	[https://www.vuze.com/](https://www.vuze.com/) || [vuze](https://aur.archlinux.org/packages/vuze/)

*   **Vuze Plus Extreme Mod** — A modded version of the Vuze BitTorrent client with multiple spoofing capabilities.

	[http://www.sb-innovation.de/f41/vuze-extreme-mod-sb-innovation-5-6-1-3-a-32315/](http://www.sb-innovation.de/f41/vuze-extreme-mod-sb-innovation-5-6-1-3-a-32315/) || [vuze-extreme-mod](https://aur.archlinux.org/packages/vuze-extreme-mod/)

#### Other P2P networks

See also [Wikipedia:Comparison of eDonkey software](https://en.wikipedia.org/wiki/Comparison_of_eDonkey_software "wikipedia:Comparison of eDonkey software").

*   **[aMule](/index.php/AMule "AMule")** — Well-known eDonkey/Kad client with a daemon version and GTK+, web, and CLI front-ends.

	[http://www.amule.org/](http://www.amule.org/) || [amule](https://www.archlinux.org/packages/?name=amule)

*   **KaMule** — KDE graphical front-end for aMule.

	[http://kde-apps.org/content/show.php?content=150270](http://kde-apps.org/content/show.php?content=150270) || [kamule](https://aur.archlinux.org/packages/kamule/)

*   **MlDonkey** — A multi-network P2P client.

	[http://mldonkey.sourceforge.net/](http://mldonkey.sourceforge.net/) || [mldonkey](https://www.archlinux.org/packages/?name=mldonkey)

*   **Sendanywhere** — GTK2 client for the cross platform P2P file sharing service, Sendanywhere. Allow users to send files of any type and size to other Android, iOS, and Desktop devices.

	[https://www.send-anywhere.com](https://www.send-anywhere.com) || [sendanywhere](https://aur.archlinux.org/packages/sendanywhere/)

*   **[Sharelin](https://en.wikipedia.org/wiki/Sharelin "wikipedia:Sharelin")** — Gnutella2 only client with a web UI.

	[https://sourceforge.net/projects/sharelin/](https://sourceforge.net/projects/sharelin/) || [sharelin](https://aur.archlinux.org/packages/sharelin/)

#### Video downloaders

*   **youtube-dl** — Download videos from YouTube and many other platforms.

	[http://rg3.github.io/youtube-dl](http://rg3.github.io/youtube-dl) || [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl)

*   **You-Get** — Dumb downloader that scrapes the web.

	[https://you-get.org/](https://you-get.org/) || [you-get](https://www.archlinux.org/packages/?name=you-get)

### Communication

#### Email clients

See also [Wikipedia:Comparison of e-mail clients](https://en.wikipedia.org/wiki/Comparison_of_e-mail_clients "wikipedia:Comparison of e-mail clients").

##### Console

*   **alot** — An experimental terminal MUA based on [notmuch mail](http://notmuchmail.org/). It is written in python using the [urwid](http://urwid.org/) toolkit.

	[https://github.com/pazz/alot](https://github.com/pazz/alot) || [alot](https://aur.archlinux.org/packages/alot/)

*   **[Alpine](/index.php/Alpine "Alpine")** — Fast, easy-to-use and Apache-licensed email client based on [Pine](https://en.wikipedia.org/wiki/Pine_(email_client) "wikipedia:Pine (email client)").

	[http://patches.freeiz.com/alpine/](http://patches.freeiz.com/alpine/) || [alpine](https://aur.archlinux.org/packages/alpine/)

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

	[http://gnus.org/](http://gnus.org/) || [emacs-gnus-git](https://aur.archlinux.org/packages/emacs-gnus-git/)

*   **[S-nail](/index.php/S-nail "S-nail")** — a mail processing system with a command syntax reminiscent of *ed* with lines replaced by messages. Provides the functionality of [mailx](https://en.wikipedia.org/wiki/mailx "wikipedia:mailx").

	[https://www.sdaoden.eu/code.html#s-mailx](https://www.sdaoden.eu/code.html#s-mailx) || [s-nail](https://www.archlinux.org/packages/?name=s-nail)

*   **mu/mu4e** — Email indexer (mu) and client for emacs (mu4e). Xapian based for fast searches.

	[http://www.djcbsoftware.nl/code/mu/mu4e.html](http://www.djcbsoftware.nl/code/mu/mu4e.html) || [mu](https://aur.archlinux.org/packages/mu/)

*   **[Mutt](/index.php/Mutt "Mutt")** — Small but very powerful text-based mail client.

	[http://www.mutt.org/](http://www.mutt.org/) || [mutt](https://www.archlinux.org/packages/?name=mutt)

*   **[nmh](/index.php/Nmh "Nmh")** — A modular mail handling system.

	[http://www.nongnu.org/nmh/](http://www.nongnu.org/nmh/) || [nmh](https://aur.archlinux.org/packages/nmh/) [nmh-git](https://aur.archlinux.org/packages/nmh-git/)

*   **[notmuch](/index.php/Notmuch "Notmuch")** — A fast mail indexer built on top of *xapian*.

	[http://notmuchmail.org/](http://notmuchmail.org/) || [notmuch](https://www.archlinux.org/packages/?name=notmuch) [notmuch-vim](https://www.archlinux.org/packages/?name=notmuch-vim) [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt)

*   **[Sup](/index.php/Sup "Sup")** — CLI mail client with very fast searching, tagging, threading and GMail like operation.

	[https://sup-heliotrope.github.io/](https://sup-heliotrope.github.io/) || [sup](https://aur.archlinux.org/packages/sup/)

*   **Wanderlust** — Email client and news reader for Emacs.

	[http://www.gohome.org/wl/](http://www.gohome.org/wl/) || [wanderlust](https://www.archlinux.org/packages/?name=wanderlust)

##### Graphical

*   **Balsa** — Simple and light email client that is part of the Gnome project.

	[http://pawsa.fedorapeople.org/balsa/](http://pawsa.fedorapeople.org/balsa/) || [balsa](https://www.archlinux.org/packages/?name=balsa)

*   **[Claws Mail](https://en.wikipedia.org/wiki/Claws_Mail "wikipedia:Claws Mail")** — Lightweight GTK-based email client and news reader.

	[http://claws-mail.org/](http://claws-mail.org/) || [claws-mail](https://www.archlinux.org/packages/?name=claws-mail)

*   **[Evolution](/index.php/Evolution "Evolution")** — Mature and feature-rich e-mail client used in GNOME by default. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution](https://www.archlinux.org/packages/?name=evolution)

*   **FossaMail** — FossaMail is a Mozilla Thunderbird-based mail, news and chat client by the Pale Moon developers.

	[http://www.fossamail.org](http://www.fossamail.org) || [fossamail-bin](https://aur.archlinux.org/packages/fossamail-bin/)

*   **Geary** — Simple desktop mail client built in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

	[https://wiki.gnome.org/Apps/Geary](https://wiki.gnome.org/Apps/Geary) || [geary](https://www.archlinux.org/packages/?name=geary)

*   **[Kmail](https://en.wikipedia.org/wiki/Kmail "wikipedia:Kmail")** — Mature and feature-rich email client. Part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[http://kde.org/applications/internet/kmail/](http://kde.org/applications/internet/kmail/) || [kmail](https://www.archlinux.org/packages/?name=kmail)

*   **Manitou Mail** — Database-driven email system.

	[http://www.manitou-mail.org/](http://www.manitou-mail.org/) || [manitou-mdx](https://aur.archlinux.org/packages/manitou-mdx/) [manitou-ui](https://aur.archlinux.org/packages/manitou-ui/)

*   **N1** — A new mail client, built on the modern web and designed to be extended.

	[https://www.nylas.com/N1/](https://www.nylas.com/N1/) || [n1](https://aur.archlinux.org/packages/n1/)

*   **Roundcubemail** — Browser-based multilingual IMAP client with a native application-like user interface.

	[http://roundcube.net/](http://roundcube.net/) || [roundcubemail](https://www.archlinux.org/packages/?name=roundcubemail)

*   **[SeaMonkey Mail & Newsgroups](https://en.wikipedia.org/wiki/SeaMonkey#Mail "wikipedia:SeaMonkey")** — Email client included in the SeaMonkey suite.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

*   **[Sylpheed](https://en.wikipedia.org/wiki/Sylpheed "wikipedia:Sylpheed")** — Lightweight and user-friendly GTK+ email client.

	[http://sylpheed.sraoss.jp/en/](http://sylpheed.sraoss.jp/en/) || [sylpheed](https://www.archlinux.org/packages/?name=sylpheed)

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Feature-rich email client from Mozilla written in GTK+.

	[http://www.mozilla.org/thunderbird/](http://www.mozilla.org/thunderbird/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

*   **Trojitá** — Qt IMAP email client. Only supports one IMAP account.

	[http://trojita.flaska.net/](http://trojita.flaska.net/) || [trojita](https://www.archlinux.org/packages/?name=trojita)

*   **WMail** — The missing desktop client for Gmail & Google Inbox

	[http://thomas101.github.io/wmail/](http://thomas101.github.io/wmail/) || [wmail-bin](https://aur.archlinux.org/packages/wmail-bin/)

#### Instant messaging

See also [Wikipedia:Comparison of instant messaging protocols](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_protocols "wikipedia:Comparison of instant messaging protocols").

This section lists all software with [instant messaging](https://en.wikipedia.org/wiki/Instant_messaging "wikipedia:Instant messaging") support. Particularly, that are client and server applications.

##### IRC clients

See also [Wikipedia:Comparison of Internet Relay Chat clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients "wikipedia:Comparison of Internet Relay Chat clients").

**Note:** Most web browsers and many IM clients also support IRC.

###### Console

*   **[BitchX](https://en.wikipedia.org/wiki/BitchX "wikipedia:BitchX")** — Console-based IRC client developed from the popular [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

	[http://www.bitchx.org/](http://www.bitchx.org/) || [bitchx-git](https://aur.archlinux.org/packages/bitchx-git/)

*   **ERC** — Powerful, modular, and extensible IRC client for [Emacs](/index.php/Emacs "Emacs").

	[http://savannah.gnu.org/projects/erc/](http://savannah.gnu.org/projects/erc/) || included with [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)")** — Featherweight IRC client, literally `tail -f` the conversation and `echo` back your replies to a file.

	[http://tools.suckless.org/ii](http://tools.suckless.org/ii) || [ii](https://aur.archlinux.org/packages/ii/)

*   **Ircfs** — File system interface to IRC written in [Limbo](http://limbo.cat-v.org).

	[http://www.ueber.net/code/r/ircfs](http://www.ueber.net/code/r/ircfs) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=ircfs)</small>

*   **[Irssi](/index.php/Irssi "Irssi")** — Highly-configurable ncurses-based IRC client.

	[http://irssi.org/](http://irssi.org/) || [irssi](https://www.archlinux.org/packages/?name=irssi)

*   **ScrollZ** — Advanced IRC client based on [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

	[http://www.scrollz.info/](http://www.scrollz.info/) || [scrollz](https://aur.archlinux.org/packages/scrollz/)

*   **sic** — Extremely simple IRC client, similar to [ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)").

	[http://tools.suckless.org/sic](http://tools.suckless.org/sic) || [sic](https://aur.archlinux.org/packages/sic/)

*   **[WeeChat](https://en.wikipedia.org/wiki/WeeChat "wikipedia:WeeChat")** — Modular, lightweight ncurses-based IRC client.

	[http://weechat.org/](http://weechat.org/) || [weechat](https://www.archlinux.org/packages/?name=weechat)

###### Graphical

*   **[ChatZilla](https://en.wikipedia.org/wiki/ChatZilla "wikipedia:ChatZilla")** — Clean, easy to use and highly extensible Internet Relay Chat (IRC) client, built on the Mozilla platform using [XULRunner](https://en.wikipedia.org/wiki/XULRunner "wikipedia:XULRunner").

	[http://chatzilla.hacksrus.com/](http://chatzilla.hacksrus.com/) || [chatzilla](https://aur.archlinux.org/packages/chatzilla/)

*   **HexChat** — Fork of XChat for Linux and Windows.

	[http://hexchat.github.io/](http://hexchat.github.io/) || [hexchat](https://www.archlinux.org/packages/?name=hexchat)

*   **[Konversation](https://en.wikipedia.org/wiki/Konversation "wikipedia:Konversation")** — Qt-based IRC client for the KDE desktop.

	[http://konversation.kde.org/](http://konversation.kde.org/) || [konversation](https://www.archlinux.org/packages/?name=konversation)

*   **[KVIrc](https://en.wikipedia.org/wiki/KVIrc "wikipedia:KVIrc")** — Qt-based IRC client featuring extensive themes support.

	[http://kvirc.net/](http://kvirc.net/) || [kvirc](https://www.archlinux.org/packages/?name=kvirc)

*   **Loqui** — GTK+ IRC client with only one dependency: [GNet](https://wiki.gnome.org/Projects/GNetLibrary).

	[https://launchpad.net/loqui](https://launchpad.net/loqui) || [loqui](https://aur.archlinux.org/packages/loqui/)

*   **LostIRC** — Simple GTK+ IRC client with tab-autocompletion, multiple server support, logging and others.

	[http://lostirc.sourceforge.net](http://lostirc.sourceforge.net) || [lostirc](https://aur.archlinux.org/packages/lostirc/)

*   **pcw** — Frontend for [ii](http://tools.suckless.org/ii) that opens a new terminal for each channel.

	[https://bitbucket.org/emg/pcw](https://bitbucket.org/emg/pcw) || [pcw-hg](https://aur.archlinux.org/packages/pcw-hg/)

*   **Polari** — Simple IRC client by the GNOME project.

	[https://wiki.gnome.org/Apps/Polari/](https://wiki.gnome.org/Apps/Polari/) || [polari](https://www.archlinux.org/packages/?name=polari)

*   **[Quassel](/index.php/Quassel "Quassel")** — Modern, cross-platform, distributed IRC client.

	[http://quassel-irc.org/](http://quassel-irc.org/) || [quassel-core](https://www.archlinux.org/packages/?name=quassel-core) [quassel-client](https://www.archlinux.org/packages/?name=quassel-client) [quassel-monolithic](https://www.archlinux.org/packages/?name=quassel-monolithic)

*   **[Smuxi](https://en.wikipedia.org/wiki/Smuxi "wikipedia:Smuxi")** — Cross-platform IRC client for the GNOME desktop inspired by [Irssi](/index.php/Irssi "Irssi").

	[http://smuxi.org/](http://smuxi.org/) || [smuxi](https://www.archlinux.org/packages/?name=smuxi)

*   **[XChat](https://en.wikipedia.org/wiki/XChat "wikipedia:XChat")** — GTK-based IRC client that works on both Linux and Windows.

	[http://xchat.org/](http://xchat.org/) || [xchat](https://www.archlinux.org/packages/?name=xchat)

##### XMPP (Jabber)

See also [Wikipedia:XMPP](https://en.wikipedia.org/wiki/XMPP "wikipedia:XMPP") and [Wikipedia:Comparison of instant messaging clients#XMPP-related features](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients#XMPP-related_features "wikipedia:Comparison of instant messaging clients").

###### Command line

*   **jp** — CLI frontend for Salut à Toi, multi-purpose XMPP client

	[https://salut-a-toi.org](https://salut-a-toi.org) || [sat-jp](https://aur.archlinux.org/packages/sat-jp/)

###### Console clients

*   **Freetalk** — Console-based Jabber client.

	[https://gnu.org/s/freetalk/](https://gnu.org/s/freetalk/) || [freetalk](https://www.archlinux.org/packages/?name=freetalk)

*   **jabber.el** — Minimal Jabber client for [Emacs](/index.php/Emacs "Emacs").

	[http://emacs-jabber.sourceforge.net/](http://emacs-jabber.sourceforge.net/) || [emacs-jabber](https://aur.archlinux.org/packages/emacs-jabber/)

*   **[MCabber](https://en.wikipedia.org/wiki/MCabber "wikipedia:MCabber")** — Small Jabber console client, includes features: SSL, PGP, MUC, OTR, and UTF8.

	[http://mcabber.com/](http://mcabber.com/) || [mcabber](https://www.archlinux.org/packages/?name=mcabber)

*   **Poezio** — XMPP client with IRC feeling

	[https://poez.io/](https://poez.io/) || [poezio](https://aur.archlinux.org/packages/poezio/)

*   **Primitivus** — Console frontend for Salut à Toi, multi-purpose XMPP client

	[https://salut-a-toi.org](https://salut-a-toi.org) || [sat-primitivus](https://aur.archlinux.org/packages/sat-primitivus/)

*   **Profanity** — A console based Jabber client inspired by Irssi.

	[http://www.profanity.im/](http://www.profanity.im/) || [profanity](https://www.archlinux.org/packages/?name=profanity)

*   **xmpp-client** — A minimalist XMPP client with OTR support.

	[https://github.com/agl/xmpp-client](https://github.com/agl/xmpp-client) || [go-xmpp-client](https://aur.archlinux.org/packages/go-xmpp-client/)

###### Graphical clients

*   **[Gajim](https://en.wikipedia.org/wiki/Gajim "wikipedia:Gajim")** — Jabber client written in PyGTK.

	[https://gajim.org/](https://gajim.org/) || [gajim](https://www.archlinux.org/packages/?name=gajim)

*   **[Psi](https://en.wikipedia.org/wiki/Psi_(instant_messaging_client) "wikipedia:Psi (instant messaging client)")** — Qt-based Jabber client which supports video conferencing.

	[http://psi-im.org/](http://psi-im.org/) || [psi](https://www.archlinux.org/packages/?name=psi) [psimedia](https://www.archlinux.org/packages/?name=psimedia)

*   **Psi+** — Enhanced version of the Psi Jabber client with many new [features](http://psi-plus.com/wiki/en:features#differences_between_psi_beta_version_and_the_official_psi_015-dev_version).

	[http://psi-plus.com/](http://psi-plus.com/) || [psi-plus-git](https://aur.archlinux.org/packages/psi-plus-git/)

*   **[Tkabber](https://en.wikipedia.org/wiki/Tkabber "wikipedia:Tkabber")** — Easy to hack feature-rich XMPP client by the author of the ejabberd XMPP server.

	[http://tkabber.jabber.ru/](http://tkabber.jabber.ru/) || [tkabber](https://www.archlinux.org/packages/?name=tkabber)

###### Servers

See also [Wikipedia:Comparison of XMPP server software](https://en.wikipedia.org/wiki/Comparison_of_XMPP_server_software "wikipedia:Comparison of XMPP server software").

*   **[Prosody](/index.php/Prosody "Prosody")** — An XMPP server written in the [Lua](http://www.lua.org/) programming language. Prosody is designed to be lightweight and highly extensible. It is licensed under a permissive [MIT license](http://prosody.im/source/mit).

	[http://prosody.im/](http://prosody.im/) || [prosody](https://www.archlinux.org/packages/?name=prosody)

*   **Ejabberd** — Jabber server written in Erlang

	[http://www.ejabberd.im/](http://www.ejabberd.im/) || [ejabberd](https://www.archlinux.org/packages/?name=ejabberd)

*   **[Jabberd2](/index.php/Jabberd2 "Jabberd2")** — An XMPP server written in the C language and licensed under the GNU General Public License. It was inspired by jabberd14.

	[http://jabberd2.org](http://jabberd2.org) || [jabberd2](https://aur.archlinux.org/packages/jabberd2/)

*   **Openfire** — An XMPP IM multiplatform server written in Java

	[http://www.igniterealtime.org/projects/openfire/](http://www.igniterealtime.org/projects/openfire/) || [openfire](https://www.archlinux.org/packages/?name=openfire)

##### Multi-protocol clients

See also [Wikipedia:Comparison of instant messaging clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients").

**Note:** All messengers, that support several networks by means of direct connections to them, belong to this section.

Many clients listed here (including Pidgin and all its forks) support multiple IM networks via [libpurple](https://en.wikipedia.org/wiki/libpurple "wikipedia:libpurple"). The number of networks supported by these clients is very large but they (like any multiprotocol clients) usually have very limited or no support for network-specific features.

###### Console

*   **BarnOwl** — Ncurses-based chat client with support for the Zephyr, AIM, Jabber, IRC, and Twitter protocols.

	[http://barnowl.mit.edu/](http://barnowl.mit.edu/) || [barnowl](https://aur.archlinux.org/packages/barnowl/)

*   **[Bitlbee](/index.php/Bitlbee "Bitlbee")** — IRC client that provides a gateway to popular chat networks (XMPP, MSN, Yahoo, AIM, ICQ and Twitter).

	[http://bitlbee.org/](http://bitlbee.org/) || [bitlbee](https://www.archlinux.org/packages/?name=bitlbee)

*   **[CenterIM](https://en.wikipedia.org/wiki/Centericq "wikipedia:Centericq")** — Fork of CenterICQ, a text mode menu- and window-driven IM interface.

	[http://centerim.org/](http://centerim.org/) || [centerim](https://www.archlinux.org/packages/?name=centerim)

*   **[Finch](/index.php/Pidgin "Pidgin")** — Ncurses-based chat client that uses libpurple and supports all its protocols.

	[http://developer.pidgin.im/wiki/Using%20Finch](http://developer.pidgin.im/wiki/Using%20Finch) || [finch](https://www.archlinux.org/packages/?name=finch)

*   **[naim](https://en.wikipedia.org/wiki/naim_(software) "wikipedia:naim (software)")** — Ncurses chat client with support for AOL, ICQ, IRC and the Lily CMC.

	[http://naim.n.ml.org/](http://naim.n.ml.org/) || [naim](https://www.archlinux.org/packages/?name=naim)

*   **pork** — Programmable, ncurses-based AIM and IRC client that mostly looks and feels like ircII.

	[http://dev.ojnk.net/](http://dev.ojnk.net/) || [pork](https://www.archlinux.org/packages/?name=pork)

*   **[Tox](/index.php/Tox "Tox")** — Tox is a distributed, secure messenger with audio and video chat capabilities.

	[https://tox.chat/](https://tox.chat/) || see [Tox](/index.php/Tox "Tox")

###### Graphical

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) framework.

	[https://wiki.gnome.org/Apps/Empathy](https://wiki.gnome.org/Apps/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **[Instantbird](https://en.wikipedia.org/wiki/Instantbird "wikipedia:Instantbird")** — Multi-protocol chat client using Mozilla's XUL and libpurple.

	[http://instantbird.com/](http://instantbird.com/) || [instantbird](https://aur.archlinux.org/packages/instantbird/)

*   **[Kopete](https://en.wikipedia.org/wiki/Kopete "wikipedia:Kopete")** — User-friendly IM supporting AIM, ICQ, Windows Live Messenger, Yahoo, Jabber, Gadu-Gadu, Novell GroupWise Messenger, and other IM networks. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[http://kopete.kde.org/](http://kopete.kde.org/) || [kdenetwork-kopete](https://www.archlinux.org/packages/?name=kdenetwork-kopete)

*   **[KDE Telepathy](/index.php/KDE#KDE_Telepathy "KDE")** — KDE instant messaging client using the [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) framework. Meant as a replacement for Kopete.

	[http://community.kde.org/Real-Time_Communication_and_Collaboration/](http://community.kde.org/Real-Time_Communication_and_Collaboration/) || [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta)

*   **Licq** — Instant messaging client for UNIX supporting multiple protocols (currently ICQ, MSN and Jabber).

	[http://www.licq.org](http://www.licq.org) || [licq](https://www.archlinux.org/packages/?name=licq)

*   **Mikutter** — An open-source Twitter client using [GTK+](/index.php/GTK%2B "GTK+") and Ruby.

	[http://mikutter.hachune.net/](http://mikutter.hachune.net/) || [mikutter](https://aur.archlinux.org/packages/mikutter/) [mikutter-git](https://aur.archlinux.org/packages/mikutter-git/)

*   **[Pidgin](/index.php/Pidgin "Pidgin")** — Multi-protocol instant messaging client.

	[http://pidgin.im/](http://pidgin.im/) || [pidgin](https://www.archlinux.org/packages/?name=pidgin) [pidgin-light](https://aur.archlinux.org/packages/pidgin-light/)

*   **qutIM** — Simple and user-friendly IM supporting ICQ, Jabber, Mail.Ru, IRC and VKontakte messaging.

	[http://qutim.org/](http://qutim.org/) || [qutim](https://aur.archlinux.org/packages/qutim/)

##### Lan messengers

See also: [Comparison of LAN messengers](https://en.wikipedia.org/wiki/Comparison_of_LAN_messengers "wikipedia:Comparison of LAN messengers").

*   **iptux** — Lan communication software, compatible with IP Messenger.

	[https://github.com/iptux-src/iptux](https://github.com/iptux-src/iptux) || [iptux](https://aur.archlinux.org/packages/iptux/)

#### VoIP / Softphone

See also [Wikipedia:Comparison of VoIP software](https://en.wikipedia.org/wiki/Comparison_of_VoIP_software "wikipedia:Comparison of VoIP software") and [Wikipedia:List of SIP software](https://en.wikipedia.org/wiki/List_of_SIP_software "wikipedia:List of SIP software").

##### Clients

**Note:** Some [IM clients](#Instant_messaging) also offer voice and video communication

###### SIP

*   **[Blink](https://en.wikipedia.org/wiki/Blink_(software) "wikipedia:Blink (software)")** — State of the art, easy to use SIP client.

	[http://www.icanblink.com/](http://www.icanblink.com/) || [blink-darcs](https://aur.archlinux.org/packages/blink-darcs/)

*   **[Ekiga](https://en.wikipedia.org/wiki/Ekiga "wikipedia:Ekiga")** — VoIP and video conferencing application with full SIP and H.323 support (formerly known as GNOME Meeting).

	[http://www.ekiga.org/](http://www.ekiga.org/) || [ekiga](https://www.archlinux.org/packages/?name=ekiga)

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) "wikipedia:Empathy (software)")** — GNOME instant messenger client using the Telepathy framework with SIP support (using the Sofia-SIP library).

	[https://wiki.gnome.org/Apps/Empathy](https://wiki.gnome.org/Apps/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **[Jitsi](https://en.wikipedia.org/wiki/Jitsi "wikipedia:Jitsi")** — Audio/video SIP VoIP phone and instant messenger written in Java (formerly SIP-Communicator).

	[https://jitsi.org/](https://jitsi.org/) || [jitsi](https://aur.archlinux.org/packages/jitsi/)

*   **[KPhone](https://en.wikipedia.org/wiki/KPhone "wikipedia:KPhone")** — Qt SIP User Agent with voice, video and text messaging support.

	[http://sourceforge.net/projects/kphone/](http://sourceforge.net/projects/kphone/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=kphone)</small>

*   **[Linphone](https://en.wikipedia.org/wiki/Linphone "wikipedia:Linphone")** — VoIP phone application that allows you to to communicate freely with people over the internet, with voice, video, and text instant messaging.

	[http://www.linphone.org/](http://www.linphone.org/) || [linphone](https://www.archlinux.org/packages/?name=linphone)

*   **Minisip** — SIP User Agent with focus on security (supports TLS, end-to-end security, SRTP, MIKEY (DH, PSK, PKE)).

	[http://www.minisip.org/](http://www.minisip.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=minisip)</small>

*   **[Twinkle](https://en.wikipedia.org/wiki/Twinkle_(software) "wikipedia:Twinkle (software)")** — Qt softphone for VoIP and IM communication using SIP.

	[http://www.twinklephone.com/](http://www.twinklephone.com/) || [twinkle](https://aur.archlinux.org/packages/twinkle/)

*   **[X-Lite](https://en.wikipedia.org/wiki/X-Lite "wikipedia:X-Lite")** — Proprietary freeware VoIP soft phone that uses SIP.

	[http://www.counterpath.net/x-lite](http://www.counterpath.net/x-lite) || [xlite_bin](https://aur.archlinux.org/packages/xlite_bin/)

*   **[Zfone](https://en.wikipedia.org/wiki/Zfone "wikipedia:Zfone")** — Softphone application for secure voice communication over the Internet (VoIP), using the ZRTP protocol.

	[http://zfoneproject.com/](http://zfoneproject.com/) || [zfone](https://aur.archlinux.org/packages/zfone/)

###### IAX2

*   **Kiax** — Qt-based IAX/2 Softphone.

	[http://www.forschung-direkt.eu/projects/kiax2/](http://www.forschung-direkt.eu/projects/kiax2/) || [kiax](https://aur.archlinux.org/packages/kiax/)

###### Skype

*   **[Skype](/index.php/Skype "Skype")** — Popular but proprietary application for high-quality voice communication.

	[http://www.skype.com/](http://www.skype.com/) || [skype](https://aur.archlinux.org/packages/skype/)

###### Other

*   **Hangups** — A third-party instant messaging client for Google Hangouts

	[https://github.com/tdryer/hangups](https://github.com/tdryer/hangups) || [hangups-git](https://aur.archlinux.org/packages/hangups-git/)

*   **[Mumble](https://en.wikipedia.org/wiki/Mumble_(software) "wikipedia:Mumble (software)")** — Voice chat application similar to TeamSpeak.

	[http://mumble.sourceforge.net/](http://mumble.sourceforge.net/) || [mumble](https://www.archlinux.org/packages/?name=mumble)

*   **[TeamSpeak](/index.php/TeamSpeak "TeamSpeak")** — Proprietary VoIP application with gamers as its target audience.

	[http://www.teamspeak.com/](http://www.teamspeak.com/) || [teamspeak3](https://www.archlinux.org/packages/?name=teamspeak3)

*   **[Discord](https://en.wikipedia.org/wiki/Discord_(software) "wikipedia:Discord (software)")** — All-in-one voice and text chat for gamers that’s free, secure, and works on both your desktop and phone.

	[https://discordapp.com/](https://discordapp.com/) || [discord-canary](https://aur.archlinux.org/packages/discord-canary/)

###### Multi-protocol

*   **[Ring](https://en.wikipedia.org/wiki/Ring_(software) "wikipedia:Ring (software)")** — Open-source SIP/IAX2 compatible softphone with PulseAudio support (formerly known as SFLphone).

	[http://ring.cx/](http://ring.cx/) || [ring-daemon](https://aur.archlinux.org/packages/ring-daemon/)

##### Utilities

*   **Gladstone** — Educational ITU-T G.729 compliant codec with a GStreamer plugin.

	[https://github.com/drizzt/gladstone](https://github.com/drizzt/gladstone) || [gladstone-drizztbsd-git](https://aur.archlinux.org/packages/gladstone-drizztbsd-git/)

*   **SIPp** — Open source test tool and traffic generator for the SIP protocol.

	[http://sipp.sourceforge.net/](http://sipp.sourceforge.net/) || [sipp](https://aur.archlinux.org/packages/sipp/)

#### Speech recognition

See [Speech recognition#List of speech recognition applications](/index.php/Speech_recognition#List_of_speech_recognition_applications "Speech recognition").

### News, RSS, and blogs

#### News aggregators

See also [Wikipedia:Comparison of feed aggregators](https://en.wikipedia.org/wiki/Comparison_of_feed_aggregators "wikipedia:Comparison of feed aggregators").

##### Console

*   **[Canto](https://en.wikipedia.org/wiki/Canto_(news_aggregator) "wikipedia:Canto (news aggregator)")** — Ncurses RSS aggregator.

	[http://codezen.org/canto/](http://codezen.org/canto/) || [canto-next-git](https://aur.archlinux.org/packages/canto-next-git/)

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

	[http://gnus.org/](http://gnus.org/) || [emacs-gnus-git](https://aur.archlinux.org/packages/emacs-gnus-git/)

*   **Newsbeuter** — Ncurses RSS aggregator with layout and keybinding similar to the [Mutt](/index.php/Mutt "Mutt") email client.

	[http://newsbeuter.org](http://newsbeuter.org) || [newsbeuter](https://www.archlinux.org/packages/?name=newsbeuter)

*   **Rawdog** — "RSS Aggregator Without Delusions Of Grandeur" that parses RSS/CDF/Atom feeds into a static HTML page of articles in chronological order.

	[http://offog.org/code/rawdog.html](http://offog.org/code/rawdog.html) || [rawdog](https://www.archlinux.org/packages/?name=rawdog)

*   **Snownews** — Text mode RSS news reader.

	[http://kiza.kcore.de/software/snownews/](http://kiza.kcore.de/software/snownews/) || [snownews](https://www.archlinux.org/packages/?name=snownews)

##### Graphical

*   **[Akregator](https://en.wikipedia.org/wiki/Kontact#News_Feed_Aggregator "wikipedia:Kontact")** — News aggregator for KDE, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[http://kde.org/applications/internet/akregator/](http://kde.org/applications/internet/akregator/) || [akregator](https://www.archlinux.org/packages/?name=akregator)

*   **Blam** — Simple newsreader for GNOME written in C Sharp.

	[https://git.gnome.org/browse/blam](https://git.gnome.org/browse/blam) || [blam](https://www.archlinux.org/packages/?name=blam)

*   **[Evolution](/index.php/Evolution "Evolution") RSS** — Plugin for Evolution Mail that enables reading of RSS/RDF/ATOM feeds.

	[http://gnome.eu.org/index.php/Evolution_RSS_Reader_Plugin](http://gnome.eu.org/index.php/Evolution_RSS_Reader_Plugin) || [evolution-rss](https://aur.archlinux.org/packages/evolution-rss/)

*   **[Liferea](https://en.wikipedia.org/wiki/Liferea "wikipedia:Liferea")** — GTK+ news aggregator for online news feeds and weblogs.

	[http://liferea.sourceforge.net](http://liferea.sourceforge.net) || [liferea](https://www.archlinux.org/packages/?name=liferea)

*   **RSS Guard** — Very tiny RSS and ATOM news reader developed using Qt framework.

	[https://github.com/martinrotter/rssguard](https://github.com/martinrotter/rssguard) || [rssguard](https://aur.archlinux.org/packages/rssguard/)

*   **[RSSOwl](https://en.wikipedia.org/wiki/RSSOwl "wikipedia:RSSOwl")** — Powerful aggregator for RSS and Atom feeds, written in Java using Eclipse Rich Client Platform and SWT as a widget toolkit.

	[http://boreal.rssowl.org](http://boreal.rssowl.org) || [rssowl](https://aur.archlinux.org/packages/rssowl/)

*   **[SeaMonkey Mail & Newsgroups](https://en.wikipedia.org/wiki/SeaMonkey#Mail "wikipedia:SeaMonkey")** — Email client included in the SeaMonkey suite which also functions as a pretty nice news aggregator.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Email client from Mozilla which also functions as a pretty nice news aggregator.

	[http://www.mozilla.org/thunderbird/](http://www.mozilla.org/thunderbird/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

*   **Tickr (formerly News)** — GTK-based RSS Reader that displays feeds as a smooth scrolling line on your Desktop, as known from TV stations.

	[http://newsrssticker.com/](http://newsrssticker.com/) || [tickr](https://aur.archlinux.org/packages/tickr/)

*   **Urssus** — Cross platform GUI news aggregator.

	[https://code.google.com/archive/p/urssus/](https://code.google.com/archive/p/urssus/) || [urssus](https://aur.archlinux.org/packages/urssus/)

*   **QuiteRSS** — RSS/Atom feed reader written on Qt/С++.

	[http://quiterss.org/](http://quiterss.org/) || [quiterss](https://aur.archlinux.org/packages/quiterss/)

#### Podcast clients

*   **gPodder** — A podcast client and feed aggregator (GTK+ and CLI interface).

	[http://gpodder.org/](http://gpodder.org/) || [gpodder3](https://aur.archlinux.org/packages/gpodder3/)

*   **Greg** — A command-line podcast aggregator.

	[https://github.com/manolomartinez/greg](https://github.com/manolomartinez/greg) || [greg-git](https://aur.archlinux.org/packages/greg-git/)

*   **Marrie** — A simple podcast client that runs on the Command Line Interface.

	[https://github.com/rafaelmartins/marrie/](https://github.com/rafaelmartins/marrie/) || [marrie-git](https://aur.archlinux.org/packages/marrie-git/)

*   **PodCastXDL** — A simple podcast Downloader for the terminal.

	[https://github.com/levi0x0/PodCastXDL](https://github.com/levi0x0/PodCastXDL) || [podcastxdl-git](https://aur.archlinux.org/packages/podcastxdl-git/)

*   **Vocal** — Simple Podcast Client for the Modern Desktop (GTK+).

	[https://launchpad.net/vocal](https://launchpad.net/vocal) || [vocal-bzr](https://aur.archlinux.org/packages/vocal-bzr/)

#### Usenet newsreaders & newsgrabbers

Some [email clients](#Email_clients) also support NNTP. This section mainly lists NNTP-only client.

See also: [Wikipedia:List of Usenet newsreaders](https://en.wikipedia.org/wiki/List_of_Usenet_newsreaders "wikipedia:List of Usenet newsreaders"), [Wikipedia:Comparison of Usenet newsreaders](https://en.wikipedia.org/wiki/Comparison_of_Usenet_newsreaders "wikipedia:Comparison of Usenet newsreaders").

*   **lottanzb** — A *SABnzbd+* (Usenet binary downloader) GUI front-end written in PyGTK

	[http://www.lottanzb.org/](http://www.lottanzb.org/) || [lottanzb](https://aur.archlinux.org/packages/lottanzb/)

*   **nn** — Alternative more user-friendly(curses-based) Usenet newsreader for UNIX.

	[http://www.nndev.org/](http://www.nndev.org/) || [nn](https://aur.archlinux.org/packages/nn/)

*   **[NZBGet](/index.php/NZBGet "NZBGet")** — CLI Utility to grab Usenet binary file using .nzb files.

	[http://nzbget.sourceforge.net/](http://nzbget.sourceforge.net/) || [nzbget](https://www.archlinux.org/packages/?name=nzbget)

*   **[pan](https://en.wikipedia.org/wiki/Pan_(newsreader) "wikipedia:Pan (newsreader)")** — A GTK2 Usenet newsreader that's good at both text and binaries.

	[http://pan.rebelbase.com/](http://pan.rebelbase.com/) || [pan](https://www.archlinux.org/packages/?name=pan)

*   **[slrn](https://en.wikipedia.org/wiki/slrn "wikipedia:slrn")** — An open source text-based news client.

	[http://www.slrn.org/](http://www.slrn.org/) || [slrn](https://www.archlinux.org/packages/?name=slrn)

*   **[tin](https://en.wikipedia.org/wiki/Tin_(newsreader) "wikipedia:Tin (newsreader)")** — A cross-platform threaded NNTP and spool based UseNet newsreader.

	[http://tin.org/](http://tin.org/) || [tin](https://aur.archlinux.org/packages/tin/)

*   **trn** — A text-based Threaded Usenet newsreader.

	[http://trn.sourceforge.net/](http://trn.sourceforge.net/) || [trn](https://aur.archlinux.org/packages/trn/)

*   **xrn** — Usenet newsreader for X Window System.

	[http://www.mit.edu/people/jik/software/xrn.html](http://www.mit.edu/people/jik/software/xrn.html) || [xrn](https://aur.archlinux.org/packages/xrn/)

#### Blog software

See also [Wikipedia:Blog software](https://en.wikipedia.org/wiki/Blog_software "wikipedia:Blog software") and [Wikipedia:List of content management systems](https://en.wikipedia.org/wiki/List_of_content_management_systems "wikipedia:List of content management systems").

*   **[Drupal](/index.php/Drupal "Drupal")** — An open source content management platform powering millions of websites and applications. It is built, used, and supported by an active and diverse community of people around the world.

	[http://drupal.org/](http://drupal.org/) || [drupal](https://www.archlinux.org/packages/?name=drupal)

*   **[Ghost](/index.php/Ghost "Ghost")** — Blogging platform written in JavaScript and distributed under the MIT License, designed to simplify the process of online publishing for individual bloggers as well as online publications.

	[https://ghost.org/](https://ghost.org/) || [ghost](https://aur.archlinux.org/packages/ghost/)

*   **Hexo** — A fast, simple & powerful blog framework, powered by Node.js.

	[http://hexo.io](http://hexo.io) || [nodejs-hexo](https://aur.archlinux.org/packages/nodejs-hexo/)

*   **[Jekyll](/index.php/Jekyll "Jekyll")** — A static blog engine, written in Ruby, which supports Markdown, textile and other formats.

	[http://jekyllrb.com/](http://jekyllrb.com/) || [ruby-jekyll](https://aur.archlinux.org/packages/ruby-jekyll/)

*   **Nanoblogger** — A small weblog engine written in Bash for the command line. It uses common UNIX tools such as cat, grep, and sed to create static HTML content. It is not mantained anymore.

	[http://nanoblogger.sourceforge.net/](http://nanoblogger.sourceforge.net/) || [nanoblogger](https://www.archlinux.org/packages/?name=nanoblogger)

*   **Nikola** — A static site generator written in Python, with incremental rebuilds and multiple markup formats.

	[https://getnikola.com/](https://getnikola.com/) || [python-nikola](https://aur.archlinux.org/packages/python-nikola/)

*   **Pelican** — A static site generator, powered by Python.

	[http://docs.getpelican.com/en/3.5.0/](http://docs.getpelican.com/en/3.5.0/) || [pelican](https://www.archlinux.org/packages/?name=pelican)

*   **[Wordpress](/index.php/Wordpress "Wordpress")** — An easy to setup and administer FLOSS content management system featuring a strong and vibrant community with thousands of plugins and themes.

	[http://wordpress.org/](http://wordpress.org/) || [wordpress](https://www.archlinux.org/packages/?name=wordpress)

#### Microblogging clients

See also [Wikipedia:List of Twitter services and applications](https://en.wikipedia.org/wiki/List_of_Twitter_services_and_applications "wikipedia:List of Twitter services and applications").

*   **Birdie** — A beautiful Twitter client for GNU/Linux.

	[http://birdieapp.github.io/](http://birdieapp.github.io/) || [birdie-git](https://aur.archlinux.org/packages/birdie-git/)

*   **Choqok** — Microblogging client for KDE that supports Twitter.com, Pump.io, GNU social and opendesktop.org services.

	[http://choqok.gnufolks.org/](http://choqok.gnufolks.org/) || [choqok](https://www.archlinux.org/packages/?name=choqok)

*   **Corebird** — Native Gtk+ Twitter client for the Linux desktop.

	[http://corebird.baedert.org/](http://corebird.baedert.org/) || [corebird-git](https://aur.archlinux.org/packages/corebird-git/)

*   **Polly** — Linux Twitter client designed for multiple columns of multiple accounts.

	[https://launchpad.net/polly/](https://launchpad.net/polly/) || [polly](https://aur.archlinux.org/packages/polly/)

*   **Pumpa** — Pump.io client written in C++ and Qt.

	[https://pumpa.branchable.com/](https://pumpa.branchable.com/) || [pumpa-git](https://aur.archlinux.org/packages/pumpa-git/)

*   **Rainbowstream** — A powerful and fully-featured console Twitter client written in Python.

	[http://www.rainbowstream.org/](http://www.rainbowstream.org/) || [rainbowstream](https://aur.archlinux.org/packages/rainbowstream/)

*   **ttytter** — Easily scriptable Twitter client written in Perl.

	[http://www.floodgap.com/software/ttytter/](http://www.floodgap.com/software/ttytter/) || [ttytter](https://aur.archlinux.org/packages/ttytter/)

*   **Turpial** — Multi-interface Twitter client written in Python.

	[https://github.com/satanas/Turpial](https://github.com/satanas/Turpial) || [turpial-git](https://aur.archlinux.org/packages/turpial-git/)

*   **turses** — Twitter client for the console based off *tyrs* with major improvements.

	[http://turses.rtfd.org/](http://turses.rtfd.org/) || [turses](https://aur.archlinux.org/packages/turses/)

### Remote desktop

See also [Wikipedia:Remote desktop software](https://en.wikipedia.org/wiki/Remote_desktop_software "wikipedia:Remote desktop software") and [Wikipedia:Comparison of remote desktop software](https://en.wikipedia.org/wiki/Comparison_of_remote_desktop_software "wikipedia:Comparison of remote desktop software").

#### Remote desktop clients

*   **[GNOME Boxes](https://en.wikipedia.org/wiki/GNOME_Boxes "wikipedia:GNOME Boxes")** — A simple GNOME 3 application to access remote or virtual systems. Supports VNC and SPICE.

	[https://wiki.gnome.org/Apps/Boxes](https://wiki.gnome.org/Apps/Boxes) || [gnome-boxes](https://www.archlinux.org/packages/?name=gnome-boxes)

*   **GVncViewer** — Simple VNC Client on Gtk-VNC.

	[https://wiki.gnome.org/Projects/gtk-vnc](https://wiki.gnome.org/Projects/gtk-vnc) || [gtk-vnc](https://www.archlinux.org/packages/?name=gtk-vnc)

*   **[KRDC](https://en.wikipedia.org/wiki/KRDC "wikipedia:KRDC")** — Remote Desktop Client for KDE. Supports RDP and VNC. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[https://www.kde.org/applications/internet/krdc/](https://www.kde.org/applications/internet/krdc/) || [krdc](https://www.archlinux.org/packages/?name=krdc)

*   **[Remmina](/index.php/Remmina "Remmina")** — Remote desktop client written in GTK+. Supports RDP, VNC, NX, XDMCP and SSH.

	[http://www.remmina.org/](http://www.remmina.org/) || [remmina](https://www.archlinux.org/packages/?name=remmina)

*   **[vncviewer (TigerVNC)](/index.php/TigerVNC "TigerVNC")** — VNC viewer for X.

	[http://tigervnc.org/](http://tigervnc.org/) || [tigervnc](https://www.archlinux.org/packages/?name=tigervnc)

*   **[Vinagre](https://en.wikipedia.org/wiki/Vinagre "wikipedia:Vinagre")** — Remote desktop viewer for GNOME. Supports RDP, VNC, SPICE and SSH. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Vinagre](https://wiki.gnome.org/Apps/Vinagre) || [vinagre](https://www.archlinux.org/packages/?name=vinagre)

*   **xfreerdp** — FreeRDP X11 client.

	[http://www.freerdp.com/](http://www.freerdp.com/) || [freerdp](https://www.archlinux.org/packages/?name=freerdp)

*   **[X2Go](/index.php/X2Go "X2Go") Client** — A graphical client (Qt4) for the X2Go system that uses the [NX technology](https://en.wikipedia.org/wiki/NX_technology "w:NX technology") protocol.

	[http://wiki.x2go.org/doku.php](http://wiki.x2go.org/doku.php) || [x2goclient](https://www.archlinux.org/packages/?name=x2goclient)

#### Remote desktop servers

*   **Krfb** — VNC server for KDE. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[https://www.kde.org/applications/system/krfb](https://www.kde.org/applications/system/krfb) || [krfb](https://www.archlinux.org/packages/?name=krfb)

*   **[Vino](/index.php/Vino "Vino")** — VNC server for GNOME. Part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

	[https://wiki.gnome.org/Projects/Vino](https://wiki.gnome.org/Projects/Vino) || [vino](https://www.archlinux.org/packages/?name=vino)

*   **[x0vncserver (TigerVNC)](/index.php/TigerVNC "TigerVNC")** — VNC Server for X displays.

	[http://tigervnc.org/](http://tigervnc.org/) || [tigervnc](https://www.archlinux.org/packages/?name=tigervnc)

*   **[x11vnc](/index.php/X11vnc "X11vnc")** — VNC server for real X displays.

	[http://www.karlrunge.com/x11vnc/](http://www.karlrunge.com/x11vnc/) || [x11vnc](https://www.archlinux.org/packages/?name=x11vnc)

*   **[X2Go](/index.php/X2Go "X2Go") Server** — An open source remote desktop software that uses the [NX technology](https://en.wikipedia.org/wiki/NX_technology "w:NX technology") protocol.

	[http://wiki.x2go.org/doku.php](http://wiki.x2go.org/doku.php) || [x2goserver](https://www.archlinux.org/packages/?name=x2goserver)

### Pastebin clients

See also [Wikipedia:Pastebin](https://en.wikipedia.org/wiki/Pastebin "wikipedia:Pastebin").

Pastebin services are often used to quote text or images while collaborating and troubleshooting. Pastebin clients provide a convenient way to post from the command line.

**Tip:** You can access the [ptpb.pw](https://ptpb.pw), [sprunge.us](http://sprunge.us/) and [ix.io](http://ix.io/) pastebins using curl. For example pipe the output of a command to ptpb: `*command* | curl -F c=@- https://ptpb.pw ` or upload a file (including images): `curl -F c=@- https://ptpb.pw < *file*` 

**Note:** [pastebin.com](http://pastebin.com/) is blocked for some people and has a history of annoying issues (javascript, adverts, poor formatting, etc). Do *not* use it.

*   **Elmer** — Pastebin client similar to wgetpaste and curlpaste, except written in Perl and usable with wget or curl. Servers: [codepad.org](http://codepad.org/), [rafb.me](http://rafb.me/), [sprunge.us](http://sprunge.us/).

	[https://github.com/sudokode/elmer](https://github.com/sudokode/elmer) || [elmer](https://aur.archlinux.org/packages/elmer/)

*   **Fb-client** — Client for the [paste.xinu.at](http://paste.xinu.at/) pastebin.

	[http://paste.xinu.at](http://paste.xinu.at) || [fb-client](https://www.archlinux.org/packages/?name=fb-client)

*   **Gist** — Command-line interface for the [gist.github.com](https://gist.github.com/) pastebin service.

	[https://github.com/defunkt/gist](https://github.com/defunkt/gist) || [gist](https://www.archlinux.org/packages/?name=gist)

*   **Haste** — Universal pastebin tool, written in Haskell. Servers: [hpaste.org](http://hpaste.org/), [paste2.org](http://paste2.org/), [pastebin.com](http://pastebin.com/) and others.

	[http://hackage.haskell.org/package/haste](http://hackage.haskell.org/package/haste) || [haste](https://aur.archlinux.org/packages/haste/)

*   **Hg-paste** — Pastebin extension for Mercurial which can send diffs to various pastebin websites for easy sharing. Servers: [dpaste.com](http://dpaste.com/) and [dpaste.org](http://dpaste.org/).

	[http://bitbucket.org/sjl/hg-paste](http://bitbucket.org/sjl/hg-paste) || [hg-paste](https://aur.archlinux.org/packages/hg-paste/)

*   **imgur** — A CLI client which can upload image to [imgur.com](http://imgur.com) image sharing service.

	[http://imgur.com/apps](http://imgur.com/apps) || [imgur](https://aur.archlinux.org/packages/imgur/)

*   **Ix** — Client for the ix.io pastebin.

	[http://ix.io](http://ix.io) || [ix](https://aur.archlinux.org/packages/ix/)

*   **Npaste-client** — Client for the [npaste.de](http://npaste.de/) pastebin.

	[http://npaste.de](http://npaste.de) || [npaste-client](https://aur.archlinux.org/packages/npaste-client/)

*   **Pastebinit** — Really small Python script that acts as a Pastebin client. Servers: [pastie.org](http://pastie.org/), [paste.kde.org](http://paste.kde.org/), [paste.debian.net](http://paste.debian.net/), [paste.ubuntu.com](http://paste.ubuntu.com/) and others (for a full list see `pastebinit -l`).

	[http://launchpad.net/pastebinit](http://launchpad.net/pastebinit) || [pastebinit](https://www.archlinux.org/packages/?name=pastebinit)

*   **paste-binouse** — C++ standalone pastebin web server

	[https://github.com/abique/paste-binouse](https://github.com/abique/paste-binouse) || [paste-binouse-git](https://aur.archlinux.org/packages/paste-binouse-git/)

*   **pb** — A very fast, lightweight pastebin and general file uploader written in python with a ton of features.

	[https://ptpb.pw](https://ptpb.pw) || [ptpb](https://aur.archlinux.org/packages/ptpb/)

*   **[pbpst](/index.php/Pbpst "Pbpst")** — A small tool to interact with pb instances (eg [ptpb.pw](https://ptpb.pw)).

	[https://github.com/HalosGhost/pbpst](https://github.com/HalosGhost/pbpst) || [pbpst](https://www.archlinux.org/packages/?name=pbpst) [pbpst-git](https://aur.archlinux.org/packages/pbpst-git/)

*   **ruby-haste** — Client for [hastebin.com](http://hastebin.com/).

	[https://github.com/seejohnrun/haste-client](https://github.com/seejohnrun/haste-client) || [ruby-haste](https://aur.archlinux.org/packages/ruby-haste/) [ruby-haste-git](https://aur.archlinux.org/packages/ruby-haste-git/)

*   **Uppity** — The pastebin client with an attitude.

	[https://github.com/Kiwi/Uppity](https://github.com/Kiwi/Uppity) || [uppity-git](https://aur.archlinux.org/packages/uppity-git/)

*   **Vim-gist** — Vim script for [gist.github.com](https://gist.github.com/).

	[http://www.vim.org/scripts/script.php?script_id=2423](http://www.vim.org/scripts/script.php?script_id=2423) || [vim-gist](https://aur.archlinux.org/packages/vim-gist/)

*   **Vim-paster** — Vim plugin to paste to any pastebin service using curl.

	[http://eugeneciurana.com/site.php?page=tools](http://eugeneciurana.com/site.php?page=tools) || [vim-paster](https://aur.archlinux.org/packages/vim-paster/)

*   **Wgetpaste** — Bash script that automates pasting to a number of pastebin services. Servers: [pastebin.ca](http://pastebin.ca/), [codepad.org](http://codepad.org/), [dpaste.com](http://dpaste.com/) and [pastebin.osuosl.org](http://pastebin.osuosl.org/).

	[http://wgetpaste.zlin.dk/](http://wgetpaste.zlin.dk/) || [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste)

### Bitcoin

See the main article: [Bitcoin](/index.php/Bitcoin "Bitcoin").

*   **Armory** — Bitcoin client with features such as support for multiple wallets, importing keys and backups.

	[https://github.com/etotheipi/BitcoinArmory](https://github.com/etotheipi/BitcoinArmory) || [armory-git](https://aur.archlinux.org/packages/armory-git/)

*   **[Bitcoin](/index.php/Bitcoin "Bitcoin")** — Official tool to manage Bitcoins, a P2P currency.

	[http://bitcoin.org/](http://bitcoin.org/) || [bitcoin-daemon](https://www.archlinux.org/packages/?name=bitcoin-daemon) [bitcoin-cli](https://www.archlinux.org/packages/?name=bitcoin-cli) [bitcoin-qt](https://www.archlinux.org/packages/?name=bitcoin-qt) [bitcoin-tx](https://www.archlinux.org/packages/?name=bitcoin-tx)

*   **Electrum** — An easy to use Bitcoin client.

	[http://electrum.org/](http://electrum.org/) || [electrum](https://www.archlinux.org/packages/?name=electrum)

*   **MultiBit** — A lightweight Bitcoin desktop client powered by the BitCoinJ library.

	[https://multibit.org/](https://multibit.org/) || [multibit](https://www.archlinux.org/packages/?name=multibit)

### Surveying

*   **[LimeSurvey](https://en.wikipedia.org/wiki/LimeSurvey "wikipedia:LimeSurvey")** — An open source on-line survey application. As a web server-based software it enables users to develop and publish on-line surveys, and collect responses, with no programming.

	[https://www.limesurvey.org/](https://www.limesurvey.org/) || [limesurvey](https://aur.archlinux.org/packages/limesurvey/)

## Multimedia

### Codecs

See the main article: [Codecs](/index.php/Codecs "Codecs").

### Image

#### Image viewers

See also [Wikipedia:Comparison of image viewers](https://en.wikipedia.org/wiki/Comparison_of_image_viewers "wikipedia:Comparison of image viewers").

##### Console

*   **fbi** — Image viewer for the linux framebuffer console.

	[https://www.kraxel.org/blog/linux/fbida/](https://www.kraxel.org/blog/linux/fbida/) || [fbida](https://www.archlinux.org/packages/?name=fbida)

*   **fbv** — Very simple graphic file viewer for the framebuffer console.

	[http://s-tech.elsat.net.pl/fbv/](http://s-tech.elsat.net.pl/fbv/) || [fbv](https://www.archlinux.org/packages/?name=fbv)

*   **fim** — Highly customizable and scriptable framebuffer image viewer based on fbi.

	[http://www.nongnu.org/fbi-improved/](http://www.nongnu.org/fbi-improved/) || [fim](https://aur.archlinux.org/packages/fim/)

*   **jfbview** — Framebuffer PDF and image viewer based on Imlib2\. Features include Vim-like controls, rotation and zoom, zoom-to-fit, and fast multi-threaded rendering.

	[http://seasonofcode.com/pages/jfbview.html](http://seasonofcode.com/pages/jfbview.html) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

##### Graphical

*   **Deepin Image Viewer** — Image viewer for the Deepin desktop environment.

	[https://github.com/linuxdeepin/deepin-image-viewer](https://github.com/linuxdeepin/deepin-image-viewer) || [deepin-image-viewer](https://www.archlinux.org/packages/?name=deepin-image-viewer)

*   **Ephoto** — A light image viewer based on EFL.

	[https://www.enlightenment.org/about-ephoto](https://www.enlightenment.org/about-ephoto) || [ephoto-git](https://aur.archlinux.org/packages/ephoto-git/)

*   **[Eye of GNOME](https://en.wikipedia.org/wiki/Eye_of_GNOME "wikipedia:Eye of GNOME")** — Image viewing and cataloging program, which is a part of the GNOME desktop environment.

	[https://wiki.gnome.org/Apps/EyeOfGnome](https://wiki.gnome.org/Apps/EyeOfGnome) || [eog](https://www.archlinux.org/packages/?name=eog)

*   **Eye of MATE** — Simple graphics viewer for the MATE desktop.

	[https://github.com/mate-desktop/eom](https://github.com/mate-desktop/eom) || GTK+ 2: [eom](https://www.archlinux.org/packages/?name=eom), GTK+ 3: [eom-gtk3](https://www.archlinux.org/packages/?name=eom-gtk3)

*   **EyeSight** — Image viewer for the Hawaii desktop environment.

	[http://hawaiios.org/projects/eyesight/](http://hawaiios.org/projects/eyesight/) || [eyesight](https://aur.archlinux.org/packages/eyesight/)

*   **[feh](/index.php/Feh "Feh")** — Fast, lightweight image viewer that uses imlib2.

	[http://feh.finalrewind.org](http://feh.finalrewind.org) || [feh](https://www.archlinux.org/packages/?name=feh)

*   **GalaPix** — OpenGL-based image viewer for simultaneously viewing and zooming large collections of image files,

	[https://github.com/Galapix/galapix](https://github.com/Galapix/galapix) || [galapix](https://aur.archlinux.org/packages/galapix/)

*   **[Geeqie](https://en.wikipedia.org/wiki/Geeqie "wikipedia:Geeqie")** — Image browser and viewer (fork of GQview) that adds additional functionality such as support for RAW files.

	[http://geeqie.org/](http://geeqie.org/) || [geeqie](https://www.archlinux.org/packages/?name=geeqie)

*   **Gimmage** — Gtkmm image viewer.

	[https://sourceforge.net/projects/gimmage.berlios/](https://sourceforge.net/projects/gimmage.berlios/) || [gimmage](https://www.archlinux.org/packages/?name=gimmage)

*   **GNOME Photos** — Access, organize, and share your photos on GNOME.

	[https://wiki.gnome.org/Apps/Photos](https://wiki.gnome.org/Apps/Photos) || [gnome-photos](https://www.archlinux.org/packages/?name=gnome-photos)

*   **GPicView** — Simple and fast image viewer for X, which is part of the [LXDE](/index.php/LXDE "LXDE") desktop.

	[http://lxde.sourceforge.net/gpicview/](http://lxde.sourceforge.net/gpicview/) || GTK+ 2: [gpicview](https://www.archlinux.org/packages/?name=gpicview), GTK+ 3: [gpicview-gtk3](https://aur.archlinux.org/packages/gpicview-gtk3/)

*   **[GQview](https://en.wikipedia.org/wiki/GQview "wikipedia:GQview")** — Image browser that features single click access to view images and move around the directory tree

	[http://gqview.sourceforge.net/](http://gqview.sourceforge.net/) || [gqview-devel](https://aur.archlinux.org/packages/gqview-devel/)

*   **[gThumb](https://en.wikipedia.org/wiki/GThumb "wikipedia:GThumb")** — Image viewer for the GNOME desktop.

	[https://wiki.gnome.org/Apps/gthumb](https://wiki.gnome.org/Apps/gthumb) || [gthumb](https://www.archlinux.org/packages/?name=gthumb)

*   **[Gwenview](https://en.wikipedia.org/wiki/Gwenview "wikipedia:Gwenview")** — Fast and easy to use image viewer for the KDE desktop.

	[http://gwenview.sourceforge.net/](http://gwenview.sourceforge.net/) || [gwenview](https://www.archlinux.org/packages/?name=gwenview)

*   **imv** — Lightweight image viewer with support for Wayland and animated GIFs.

	[https://www.github.com/eXeC64/imv/](https://www.github.com/eXeC64/imv/) || [imv](https://aur.archlinux.org/packages/imv/)

*   **LxImage-Qt** — The LXQt image viewer.

	[https://github.com/lxde/lximage-qt](https://github.com/lxde/lximage-qt) || [lximage-qt](https://aur.archlinux.org/packages/lximage-qt/)

*   **meh** — meh is a small, simple, super fast image viewer using raw XLib.

	[http://www.johnhawthorn.com/meh/](http://www.johnhawthorn.com/meh/) || [meh-git](https://aur.archlinux.org/packages/meh-git/)

*   **Mirage** — PyGTK image viewer featuring support for crop and resize, custom actions and a thumbnail panel.

	[https://sourceforge.net/projects/mirageiv.berlios/](https://sourceforge.net/projects/mirageiv.berlios/) || [mirage](https://www.archlinux.org/packages/?name=mirage)

*   **nomacs** — Free (GPLv3) Qt image viewer for many operating systems. It is feature-rich but starts fast and can be configured to show additional widgets or only the image.

	[http://www.nomacs.org/](http://www.nomacs.org/) || [nomacs](https://www.archlinux.org/packages/?name=nomacs)

*   **Pantheon Photos** — Image viewer for Pantheon.

	[https://launchpad.net/pantheon-photos](https://launchpad.net/pantheon-photos) || [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos)

*   **Phototonic** — Fast and functional image viewer and organizer (Qt).

	[http://oferkv.github.io/phototonic/](http://oferkv.github.io/phototonic/) || [phototonic](https://aur.archlinux.org/packages/phototonic/)

*   **PhotoQt** — Fast and highly configurable image viewer with a simple and nice interface.

	[http://photoqt.org/](http://photoqt.org/) || [photoqt](https://aur.archlinux.org/packages/photoqt/)

*   **Quick Image Viewer** — Very small and fast image viewer based on GTK+ and imlib2.

	[http://spiegl.de/qiv/](http://spiegl.de/qiv/) || [qiv](https://www.archlinux.org/packages/?name=qiv)

*   **Ristretto** — Fast and lightweight image viewer for the Xfce desktop environment.

	[http://goodies.xfce.org/projects/applications/ristretto](http://goodies.xfce.org/projects/applications/ristretto) || [ristretto](https://www.archlinux.org/packages/?name=ristretto)

*   **Shotwell** — A digital photo organizer designed for the GNOME desktop environment

	[https://wiki.gnome.org/Apps/Shotwell](https://wiki.gnome.org/Apps/Shotwell) || [shotwell](https://www.archlinux.org/packages/?name=shotwell)

*   **[sxiv](/index.php/Sxiv "Sxiv")** — Simple image viewer based on imlib2 that works well with tiling window managers.

	[https://github.com/muennich/sxiv](https://github.com/muennich/sxiv) || [sxiv](https://www.archlinux.org/packages/?name=sxiv)

*   **Viewnior** — Minimalistic GTK+ image viewer featuring support for flipping, rotating, animations and configurable mouse actions.

	[http://siyanpanayotov.com/project/viewnior/](http://siyanpanayotov.com/project/viewnior/) || [viewnior](https://www.archlinux.org/packages/?name=viewnior)

*   **Xloadimage** — Classic X image viewer.

	[http://sioseis.ucsd.edu/xloadimage.html](http://sioseis.ucsd.edu/xloadimage.html) || [xloadimage](https://www.archlinux.org/packages/?name=xloadimage)

*   **[XnView MP](https://en.wikipedia.org/wiki/XnView "wikipedia:XnView")** — Efficient proprietary image viewer, browser and converter.

	[http://www.xnview.com/en/xnviewmp/](http://www.xnview.com/en/xnviewmp/) || [xnviewmp](https://aur.archlinux.org/packages/xnviewmp/)

*   **[xv](https://en.wikipedia.org/wiki/Xv_(software) "wikipedia:Xv (software)")** — Shareware program written by John Bradley to display and modify digital images under the X Window System. Last released in 1994.

	[http://www.trilon.com/xv/](http://www.trilon.com/xv/) || [xv](https://www.archlinux.org/packages/?name=xv)

#### Graphics and image manipulation

##### Raster editors

See also [Wikipedia:Comparison of raster graphics editors](https://en.wikipedia.org/wiki/Comparison_of_raster_graphics_editors "wikipedia:Comparison of raster graphics editors").

*   **AzPainter** — A Painting software.

	[http://azpainter.sourceforge.jp/](http://azpainter.sourceforge.jp/) || [azpainter](https://aur.archlinux.org/packages/azpainter/)

*   **[darktable](https://en.wikipedia.org/wiki/darktable "wikipedia:darktable")** — Photography workflow and RAW development application.

	[http://www.darktable.org//](http://www.darktable.org//) || [darktable](https://www.archlinux.org/packages/?name=darktable)

*   **dcraw** — Converts many camera RAW formats.

	[http://www.cybercom.net/~dcoffin/dcraw/](http://www.cybercom.net/~dcoffin/dcraw/) || [dcraw](https://www.archlinux.org/packages/?name=dcraw)

*   **[digiKam](https://en.wikipedia.org/wiki/digiKam "wikipedia:digiKam")** — KDE-based image organizer with built-in editing features via a plugin architecture. digiKam asserts it is more full featured than similar applications with a larger set of image manipulation features including RAW image import and manipulation.

	[http://www.digikam.org/](http://www.digikam.org/) || [digikam](https://www.archlinux.org/packages/?name=digikam)

*   **[GIMP](/index.php/GIMP "GIMP")** — Image editing suite in the vein of proprietary editors such as [Adobe Photoshop](https://en.wikipedia.org/wiki/Adobe_Photoshop "wikipedia:Adobe Photoshop"). GIMP ([GNU](/index.php/GNU "GNU") Image Manipulation Program) has been started in the mid 1990s and has acquired a large number of [plugins](/index.php/CMYK_support_in_The_GIMP "CMYK support in The GIMP") and additional tools.

	[http://www.gimp.org/](http://www.gimp.org/) || [gimp](https://www.archlinux.org/packages/?name=gimp)

*   **[Gpaint](https://en.wikipedia.org/wiki/GNU_Paint "wikipedia:GNU Paint")** — [Paintbrush](https://en.wikipedia.org/wiki/PC_Paintbrush "wikipedia:PC Paintbrush") clone for GNOME.

	[http://www.gnu.org/software/gpaint/](http://www.gnu.org/software/gpaint/) || [gpaint](https://aur.archlinux.org/packages/gpaint/)

*   **[GraphicsMagick](https://en.wikipedia.org/wiki/GraphicsMagick "wikipedia:GraphicsMagick")** — Fork of ImageMagick designed to have API and command-line stability. It also supports multi-CPU for enhanced performance and thus is used by some large commercial sites (Flickr, etsy) for its performance.

	[http://www.graphicsmagick.org/](http://www.graphicsmagick.org/) || [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick)

*   **[ImageMagick](https://en.wikipedia.org/wiki/ImageMagick "wikipedia:ImageMagick")** — Command-line image manipulation program. It is known for its accurate format conversions with support for over 100 formats. Its API enables it to be scripted and it is usually used as a backend processor.

	[http://www.imagemagick.org/script/index.php](http://www.imagemagick.org/script/index.php) || [imagemagick](https://www.archlinux.org/packages/?name=imagemagick)

*   **[KolourPaint](https://en.wikipedia.org/wiki/KolourPaint "wikipedia:KolourPaint")** — Free raster graphics editor for KDE, similar to Microsoft's Paint application before Windows 7, but with some additional features such as support for transparency. Part of [kde-applications](https://www.archlinux.org/groups/x86_64/kde-applications/) and [kdegraphics](https://www.archlinux.org/groups/x86_64/kdegraphics/) groups.

	[http://kolourpaint.org](http://kolourpaint.org) || [kolourpaint](https://www.archlinux.org/packages/?name=kolourpaint)

*   **[Krita](https://en.wikipedia.org/wiki/Krita "wikipedia:Krita")** — Digital painting and illustration software included based on the KDE platform.

	[http://krita.org/](http://krita.org/) || [krita](https://www.archlinux.org/packages/?name=krita)

*   **Luminance HDR** — Open source graphical user interface application that aims to provide a workflow for HDR imaging.

	[http://qtpfsgui.sourceforge.net/](http://qtpfsgui.sourceforge.net/) || [luminancehdr](https://www.archlinux.org/packages/?name=luminancehdr)

*   **mtPaint** — Graphics editing program geared towards creating indexed palette images and pixel art.

	[http://mtpaint.sourceforge.net/](http://mtpaint.sourceforge.net/) || [mtpaint](https://www.archlinux.org/packages/?name=mtpaint)

*   **[MyPaint](https://en.wikipedia.org/wiki/MyPaint "wikipedia:MyPaint")** — Free software graphics application for digital painters.

	[http://mypaint.org](http://mypaint.org) || [mypaint](https://www.archlinux.org/packages/?name=mypaint)

*   **[Pinta](https://en.wikipedia.org/wiki/Pinta_(software) "wikipedia:Pinta (software)")** — Drawing and editing program modeled after [Paint.NET](https://en.wikipedia.org/wiki/Paint.net "wikipedia:Paint.net"). Its goal is to provide a simplified alternative to GIMP for casual users.

	[http://pinta-project.com/](http://pinta-project.com/) || [pinta](https://www.archlinux.org/packages/?name=pinta)

*   **[XPaint](https://en.wikipedia.org/wiki/XPaint "wikipedia:XPaint")** — Color image editing tool which features most standard paint program options.

	[http://sourceforge.net/projects/sf-xpaint/](http://sourceforge.net/projects/sf-xpaint/) || [xpaint](https://aur.archlinux.org/packages/xpaint/)

Some image viewers like Ephoto, GNOME Photos, [gThumb](https://en.wikipedia.org/wiki/GThumb and [XnView MP](https://en.wikipedia.org/wiki/XnView "wikipedia:XnView") also provide some basic image manipulation functionality.

##### Vector graphics - illustration

See also [Wikipedia:Comparison of vector graphics editors](https://en.wikipedia.org/wiki/Comparison_of_vector_graphics_editors "wikipedia:Comparison of vector graphics editors").

*   **[Asymptote](https://en.wikipedia.org/wiki/Asymptote_(vector_graphics_language) "wikipedia:Asymptote (vector graphics language)")** — A descriptive vector graphics language (like PGF/TikZ and Metapost) with a C-like syntax and LaTeX support.

	[http://asymptote.sourceforge.net](http://asymptote.sourceforge.net) || [asymptote](https://www.archlinux.org/packages/?name=asymptote)

*   **[Dia](https://en.wikipedia.org/wiki/Dia_(software) "wikipedia:Dia (software)")** — GTK+-based diagram creation program.

	[https://wiki.gnome.org/Apps/Dia](https://wiki.gnome.org/Apps/Dia) || [dia](https://www.archlinux.org/packages/?name=dia)

*   **[Graphviz](https://en.wikipedia.org/wiki/Graphviz "wikipedia:Graphviz")** — Set of tools for drawing graphs in the descriptive DOT language.

	[http://www.graphviz.org](http://www.graphviz.org) || [graphviz](https://www.archlinux.org/packages/?name=graphviz)

*   **[Inkscape](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")** — Vector graphics editor, with capabilities similar to [Illustrator](https://en.wikipedia.org/wiki/Adobe_Illustrator "wikipedia:Adobe Illustrator"), [CorelDraw](https://en.wikipedia.org/wiki/CorelDRAW "wikipedia:CorelDRAW"), or [Xara X](https://en.wikipedia.org/wiki/Xara_X "wikipedia:Xara X"), using the SVG (Scalable Vector Graphics) file format. Inkscape supports many advanced SVG features (markers, clones, alpha blending, etc.) and great care is taken in designing a streamlined interface. It is very easy to edit nodes, perform complex path operations, trace bitmaps and much more. It's developers also aim to maintain a thriving user and developer community by using open, community-oriented development.

	[http://inkscape.org/](http://inkscape.org/) || [inkscape](https://www.archlinux.org/packages/?name=inkscape)

*   **[Karbon](https://en.wikipedia.org/wiki/Karbon_(software) "wikipedia:Karbon (software)")** — Vector graphics editor, part of the Calligra Suite. Part of [calligra](https://www.archlinux.org/groups/x86_64/calligra/) group.

	[http://www.calligra-suite.org/karbon/](http://www.calligra-suite.org/karbon/) || [calligra-karbon](https://www.archlinux.org/packages/?name=calligra-karbon)

*   **[Pencil Project](https://en.wikipedia.org/wiki/Pencil2D "wikipedia:Pencil2D")** — An open-source GUI prototyping and mockup tool.

	[http://pencil.evolus.vn/](http://pencil.evolus.vn/) || [pencil](https://aur.archlinux.org/packages/pencil/)

*   **qasm2circ** — Quantum circuit generator for latex

	[http://www.media.mit.edu/quanta/qasm2circ/](http://www.media.mit.edu/quanta/qasm2circ/) || [qasm2circ](https://aur.archlinux.org/packages/qasm2circ/)

*   **[sK1](https://en.wikipedia.org/wiki/SK1_(program) "wikipedia:SK1 (program)")** — Replacement for Adobe Illustrator or CorelDraw, oriented for "prepress ready" PostScript & PDF output.

	[http://sk1project.org/](http://sk1project.org/) || [sk1](https://www.archlinux.org/packages/?name=sk1)

*   **[Xara LX](https://en.wikipedia.org/wiki/Xara_Xtreme_LX "wikipedia:Xara Xtreme LX")** — Advanced vector graphics program, the open source version of the commercial Xara X.

	[http://www.xaraxtreme.org/](http://www.xaraxtreme.org/) || [xaralx](https://aur.archlinux.org/packages/xaralx/)

*   **[yEd](https://en.wikipedia.org/wiki/yEd "wikipedia:yEd")** — General-purpose diagramming program for flowcharts, network diagrams, UML diagrams, BPMN diagrams, mind maps, organization charts, and Entity Relationship diagrams.

	[http://www.yworks.com/en/products_yed_about.html](http://www.yworks.com/en/products_yed_about.html) || [yed](https://aur.archlinux.org/packages/yed/)

##### Vector graphics - CAD

See also [Wikipedia:List of computer-aided design editors](https://en.wikipedia.org/wiki/List_of_computer-aided_design_editors "wikipedia:List of computer-aided design editors").

*   **[BRL-CAD](https://en.wikipedia.org/wiki/BRL-CAD "wikipedia:BRL-CAD")** — Constructive solid geometry (CSG) solid modeling computer-aided design (CAD) system that includes an interactive geometry editor, ray tracing support for graphics rendering and geometric analysis, computer network distributed framebuffer support, scripting, image-processing and signal-processing tools.

	[http://brlcad.org/](http://brlcad.org/) || [brlcad](https://aur.archlinux.org/packages/brlcad/)

*   **DraftSight** — Dassault Systemes' freeware 2D CAD application. DraftSight allows users to access DWG/DXF files, regardless of which CAD software was originally used to create them.

	[http://www.3ds.com/products-services/draftsight/overview/](http://www.3ds.com/products-services/draftsight/overview/) || [draftsight](https://aur.archlinux.org/packages/draftsight/)

*   **[FreeCAD](https://en.wikipedia.org/wiki/FreeCAD "wikipedia:FreeCAD")** — CAD/CAE program, based on OpenCascade, Qt and Python with features such as macro recording, workbenches and the ability to run as server.

	[http://sourceforge.net/projects/free-cad/](http://sourceforge.net/projects/free-cad/) || [freecad](https://www.archlinux.org/packages/?name=freecad)

*   **LeoCAD** — CAD program for creating virtual LEGO models. It has an easy to use interface and currently includes over 6000 different pieces created by the LDraw community.

	[http://leocad.org](http://leocad.org) || [leocad](https://aur.archlinux.org/packages/leocad/)

*   **[LibreCAD](https://en.wikipedia.org/wiki/LibreCAD "wikipedia:LibreCAD")** — Powerful 2D CAD application based on Qt. It has been forked from QCad Community Edition.

	[http://www.librecad.org/](http://www.librecad.org/) || [librecad](https://www.archlinux.org/packages/?name=librecad)

*   **[OpenSCAD](https://en.wikipedia.org/wiki/OpenSCAD "wikipedia:OpenSCAD")** — Open source 2D/3D CAD using programmers approach.

	[http://www.openscad.org](http://www.openscad.org) || [openscad](https://www.archlinux.org/packages/?name=openscad) [openscad-git](https://aur.archlinux.org/packages/openscad-git/)

*   **[QCAD](https://en.wikipedia.org/wiki/QCad "wikipedia:QCad")** — Powerful 2D CAD application that began in 1999\. QCaD includes DFX standard file format and supports HPGL format.

	[http://www.qcad.org/](http://www.qcad.org/) || [qcad](https://www.archlinux.org/packages/?name=qcad)

##### 3D modeling/rendering

See also [Wikipedia:Comparison of 3D computer graphics software](https://en.wikipedia.org/wiki/Comparison_of_3D_computer_graphics_software "wikipedia:Comparison of 3D computer graphics software").

*   **[Art of Illusion](https://en.wikipedia.org/wiki/Art_of_Illusion "wikipedia:Art of Illusion")** — 3D modeling and rendering studio written in Java.

	[http://www.artofillusion.org/](http://www.artofillusion.org/) || [aoi](https://aur.archlinux.org/packages/aoi/)

*   **[Blender](https://en.wikipedia.org/wiki/Blender_(software) "wikipedia:Blender (software)")** — fully integrated 3D graphics creation suite capable of 3D modeling, texturing, and animation, among other things.

	[http://www.blender.org/](http://www.blender.org/) || [blender](https://www.archlinux.org/packages/?name=blender)

*   **[MakeHuman™](https://en.wikipedia.org/wiki/MakeHuman "wikipedia:MakeHuman")** — Parametrical modeling program for creating human bodies.

	[http://www.makehuman.org/](http://www.makehuman.org/) || [makehuman](https://aur.archlinux.org/packages/makehuman/)

*   **[POV-Ray](https://en.wikipedia.org/wiki/POV-Ray "wikipedia:POV-Ray")** — Script-based raytracer for creating 3D graphics.

	[http://www.povray.org/](http://www.povray.org/) || [povray](https://www.archlinux.org/packages/?name=povray)

*   **[Wings 3D](https://en.wikipedia.org/wiki/Wings3d "wikipedia:Wings3d")** — Advanced subdivision modeler that is both powerful and easy to use.

	[http://www.wings3d.com/](http://www.wings3d.com/) || [wings3d](https://www.archlinux.org/packages/?name=wings3d)

#### Screen capture

See also: [Taking a screenshot](/index.php/Taking_a_screenshot "Taking a screenshot").

### Audio

#### Audio systems

See the main article: [Sound system](/index.php/Sound_system "Sound system").

See also [Wikipedia:Sound server](https://en.wikipedia.org/wiki/Sound_server "wikipedia:Sound server").

*   **wineasio** — Provides an ASIO to JACK driver for *wine*. ASIO is the most common Windows low-latency driver, so is commonly used in audio workstation programs.

	[http://sourceforge.net/projects/wineasio/](http://sourceforge.net/projects/wineasio/) || [wineasio](https://aur.archlinux.org/packages/wineasio/)

#### Audio players

See also [Wikipedia:Comparison of audio player software](https://en.wikipedia.org/wiki/Comparison_of_audio_player_software "wikipedia:Comparison of audio player software").

##### Music player daemons and clients

See also: [List of MPD clients](/index.php/Music_Player_Daemon#Clients "Music Player Daemon")

*   **[Music Player Daemon](/index.php/Music_Player_Daemon "Music Player Daemon")** — Lightweight and scalable choice for music management.

	[http://www.musicpd.org/](http://www.musicpd.org/) || [mpd](https://www.archlinux.org/packages/?name=mpd)

*   **[XMMS2](https://en.wikipedia.org/wiki/XMMS2 "wikipedia:XMMS2")** — Complete rewrite of the popular music player.

	[https://xmms2.org](https://xmms2.org) || [xmms2](https://www.archlinux.org/packages/?name=xmms2)

##### Command-line players

*   **[cmus](/index.php/Cmus "Cmus")** — Very feature-rich ncurses-based music player.

	[http://cmus.github.io/](http://cmus.github.io/) || [cmus](https://www.archlinux.org/packages/?name=cmus)

*   **Cplay** — Curses front-end for various audio players (ogg123, mpg123, mpg321, splay, madplay, and mikmod, xmp, and sox).

	[http://directory.fsf.org/wiki/Cplay](http://directory.fsf.org/wiki/Cplay) || [cplay](https://aur.archlinux.org/packages/cplay/)

*   **Herrie** — Minimalistic console-based music player with native AudioScrobbler support.

	[http://herrie.info/](http://herrie.info/) || [herrie](https://aur.archlinux.org/packages/herrie/)

*   **[MOC](/index.php/Moc "Moc")** — Ncurses console audio player with support for the MP3, OGG, and WAV formats.

	[http://moc.daper.net/](http://moc.daper.net/) || [moc](https://www.archlinux.org/packages/?name=moc)

*   **MPFC** — Gstreamer-based audio player with curses interface.

	[https://code.google.com/archive/p/mpfc/](https://code.google.com/archive/p/mpfc/) || [mpfc](https://aur.archlinux.org/packages/mpfc/)

*   **[mpg123](https://en.wikipedia.org/wiki/Mpg123 "wikipedia:Mpg123")** — Fast free MP3 console audio player for Linux, FreeBSD, Solaris, HP-UX and nearly all other UNIX systems (also decodes MP1 and MP2 files).

	[http://www.mpg123.org/](http://www.mpg123.org/) || [mpg123](https://www.archlinux.org/packages/?name=mpg123)

*   **mps-youtube** — Terminal based YouTube jukebox with playlist management. Plays audio/video through mplayer/mpv.

	[https://github.com/mps-youtube/mps-youtube](https://github.com/mps-youtube/mps-youtube) || [mps-youtube](https://www.archlinux.org/packages/?name=mps-youtube)

*   **pancake** — Cli pandora client built with urwid.

	[https://github.com/osum4est/pancake/](https://github.com/osum4est/pancake/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[pianobar](/index.php/Pianobar "Pianobar")** — Console-based frontend for Pandora.

	[http://6xq.net/projects/pianobar/](http://6xq.net/projects/pianobar/) || [pianobar](https://www.archlinux.org/packages/?name=pianobar)

*   **shell-fm** — Console-based player for the streams provided by [last.fm](http://www.last.fm/).

	[https://github.com/jkramer/shell-fm/](https://github.com/jkramer/shell-fm/) || [shell-fm](https://aur.archlinux.org/packages/shell-fm/)

*   **[VLC](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Highly portable multimedia player with ncurses interface module, and multimedia framework capable of reading most audio and video formats as well as DVDs, Audio CDs, VCDs, and various streaming protocols.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **whistle** — a curses-based commandline audio player.

	[https://github.com/ap0calypse/whistle/](https://github.com/ap0calypse/whistle/) || [whistle-git](https://aur.archlinux.org/packages/whistle-git/)

##### GUI players

*   **[Amarok](/index.php/Amarok "Amarok")** — Mature Qt-based player known for its plethora of features.

	[http://amarok.kde.org/](http://amarok.kde.org/) || [amarok](https://www.archlinux.org/packages/?name=amarok)

*   **[Audacious](/index.php/Audacious "Audacious")** — [Winamp](https://en.wikipedia.org/wiki/Winamp "wikipedia:Winamp") clone like Beep and old XMMS versions.

	[http://audacious-media-player.org/](http://audacious-media-player.org/) || [audacious](https://www.archlinux.org/packages/?name=audacious)

*   **[Banshee](https://en.wikipedia.org/wiki/Banshee_(media_player) "wikipedia:Banshee (media player)")** — [iTunes](https://en.wikipedia.org/wiki/iTunes "wikipedia:iTunes") clone, built with GTK+ and [Mono](/index.php/Mono "Mono"), feature-rich and more actively developed.

	[http://banshee.fm/](http://banshee.fm/) || [banshee](https://www.archlinux.org/packages/?name=banshee)

*   **[Clementine](https://en.wikipedia.org/wiki/Clementine_(software) "wikipedia:Clementine (software)")** — Amarok 1.4 clone, ported to Qt 4.

	[http://www.clementine-player.org/](http://www.clementine-player.org/) || [clementine](https://www.archlinux.org/packages/?name=clementine)

*   **Cuberok** — Music player and collection manager with a lightweight interface.

	[https://code.google.com/archive/p/cuberok/](https://code.google.com/archive/p/cuberok/) || [cuberok](https://aur.archlinux.org/packages/cuberok/)

*   **DeaDBeeF** — Light and fast music player with many features, no GNOME or KDE dependencies, supports console-only, as well as a GTK+ GUI, comes with many plugins, and has a metadata editor.

	[http://deadbeef.sourceforge.net/](http://deadbeef.sourceforge.net/) || [deadbeef](https://www.archlinux.org/packages/?name=deadbeef)

*   **[Exaile](/index.php/Exaile "Exaile")** — GTK+ clone of Amarok.

	[http://www.exaile.org/](http://www.exaile.org/) || [exaile](https://aur.archlinux.org/packages/exaile/)

*   **gmusicbrowser** — Open-source jukebox for large collections of MP3/OGG/FLAC files.

	[http://gmusicbrowser.org/](http://gmusicbrowser.org/) || [gmusicbrowser](https://aur.archlinux.org/packages/gmusicbrowser/)

*   **GNOME Music** — Music is the new GNOME music playing application. It aims to combine an elegant and immersive browsing experience with simple and straightforward controls.

	[https://wiki.gnome.org/Apps/Music](https://wiki.gnome.org/Apps/Music) || [gnome-music](https://www.archlinux.org/packages/?name=gnome-music)

*   **Goggles Music Manager** — Music collection manager and player that automatically categorizes your music, supports gapless playback, features easy tag editing, and internet radio support. Uses the [Fox toolkit](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit").

	[http://gogglesmm.github.io/](http://gogglesmm.github.io/) || [gogglesmm](https://www.archlinux.org/packages/?name=gogglesmm)

*   **Guayadeque** — Full featured media player that can easily manage large collections and uses the GStreamer media framework.

	[http://guayadeque.org/](http://guayadeque.org/) || [guayadeque](https://aur.archlinux.org/packages/guayadeque/)

*   **[JuK](https://en.wikipedia.org/wiki/JuK "wikipedia:JuK")** — JuK is an audio jukebox application, supporting collections of MP3, Ogg Vorbis, and FLAC audio files.

	[https://www.kde.org/applications/multimedia/juk/](https://www.kde.org/applications/multimedia/juk/) || [kdemultimedia-juk](https://www.archlinux.org/packages/?name=kdemultimedia-juk)

*   **Listen** — Listen is a Music player and management for GNOME written in python.

	[https://launchpad.net/listen](https://launchpad.net/listen) || [listen](https://aur.archlinux.org/packages/listen/)

*   **Lollypop** — A GNOME music player.

	[https://gnumdk.github.io/lollypop-web/](https://gnumdk.github.io/lollypop-web/) || [lollypop](https://www.archlinux.org/packages/?name=lollypop)

*   **LXMusic** — A minimalist xmms2-based music player.

	[http://wiki.lxde.org/en/LXMusic](http://wiki.lxde.org/en/LXMusic) || [lxmusic](https://www.archlinux.org/packages/?name=lxmusic)

*   **Miam-player** — Cross-platform open source music player.

	[http://miam-player.org/](http://miam-player.org/) || [miam-player](https://aur.archlinux.org/packages/miam-player/)

*   **Musique** — Just another music player, only better.

	[http://flavio.tordini.org/musique](http://flavio.tordini.org/musique) || [musique](https://aur.archlinux.org/packages/musique/)

*   **[Nightingale](https://en.wikipedia.org/wiki/Nightingale_(software) "wikipedia:Nightingale (software)")** — Open source clone of iTunes-based on [Songbird](https://en.wikipedia.org/wiki/Songbird_(software) "wikipedia:Songbird (software)"), that uses Mozilla technologies and the GStreamer framework.

	[http://getnightingale.com/](http://getnightingale.com/) || [nightingale-git](https://aur.archlinux.org/packages/nightingale-git/)

*   **Noise** — Simple, fast, and good looking music player.

	[https://launchpad.net/noise](https://launchpad.net/noise) || [noise-player](https://www.archlinux.org/packages/?name=noise-player)

*   **Nuvola Player** — Integrated Google Music, 8tracks and Hype Machine player.

	[http://nuvolaplayer.fenryxo.cz/](http://nuvolaplayer.fenryxo.cz/) || [nuvolaplayer](https://aur.archlinux.org/packages/nuvolaplayer/)

*   **Potamus** — Lightweight, intuitive GTK+ audio player with an emphasis on high audio quality.

	[http://offog.org/code/potamus.html](http://offog.org/code/potamus.html) || [potamus](https://aur.archlinux.org/packages/potamus/)

*   **Pragha** — GTK+ music manager. (fork of the Consonance Music Manager)

	[https://pragha-music-player.github.io/](https://pragha-music-player.github.io/) || [pragha](https://www.archlinux.org/packages/?name=pragha)

*   **Qmmp** — Qt-based multimedia player with a user interface that is similar to Winamp or XMMS.

	[http://qmmp.ylsoftware.com/](http://qmmp.ylsoftware.com/) || [qmmp](https://www.archlinux.org/packages/?name=qmmp)

*   **[Quod Libet](https://en.wikipedia.org/wiki/Quod_Libet_(software) "wikipedia:Quod Libet (software)")** — Audio player written with PyGTK and GStreamer with support for regular expressions in playlists.

	[https://github.com/quodlibet/quodlibet/](https://github.com/quodlibet/quodlibet/) || [quodlibet](https://www.archlinux.org/packages/?name=quodlibet)

*   **[Rhythmbox](https://en.wikipedia.org/wiki/Rhythmbox "wikipedia:Rhythmbox")** — GTK+ clone of iTunes, used by default in GNOME.

	[https://wiki.gnome.org/Apps/Rhythmbox](https://wiki.gnome.org/Apps/Rhythmbox) || [rhythmbox](https://www.archlinux.org/packages/?name=rhythmbox)

*   **[Spotify](/index.php/Spotify "Spotify")** — Proprietary music streaming service. It supports local playback and streaming from Spotify's vast library (requires a free account).

	[http://www.spotify.com/](http://www.spotify.com/) || [spotify](https://aur.archlinux.org/packages/spotify/)

*   **[SpotCommander](/index.php/SpotCommander "SpotCommander")** — A remote control for Spotify, optimized for mobile devices. It works on any device with a modern browser, and it's free and open source.

	[http://olejon.github.io/spotcommander/](http://olejon.github.io/spotcommander/) || [spotcommander](https://aur.archlinux.org/packages/spotcommander/)

*   **Tomahawk** — Music player application written in C++/Qt. It decouples the name of the song from the source it was shared from - and fulfills the request using all of your available sources.

	[http://www.tomahawk-player.org/](http://www.tomahawk-player.org/) || [tomahawk](https://aur.archlinux.org/packages/tomahawk/)

*   **[VLC](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Highly portable multimedia player and multimedia framework capable of reading most audio and video formats as well as DVDs, Audio CDs, VCDs, and various streaming protocols.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **[XMMS](https://en.wikipedia.org/wiki/XMMS "wikipedia:XMMS")** — Skinnable GTK+ standalone media player similar to Winamp.

	[http://legacy.xmms2.org/](http://legacy.xmms2.org/) || [xmms](https://aur.archlinux.org/packages/xmms/)

#### Volume managers

*   **GVolWheel** — An audio mixer which lets you control the volume through a tray icon.

	[http://sourceforge.net/projects/gvolwheel/](http://sourceforge.net/projects/gvolwheel/) || [gvolwheel](https://aur.archlinux.org/packages/gvolwheel/)

*   **GVTray** — A master volume mixer for the system tray.

	[https://code.google.com/archive/p/gtk-tray-utils/](https://code.google.com/archive/p/gtk-tray-utils/) || [gvtray](https://aur.archlinux.org/packages/gvtray/)

*   **pa-applet** — PulseAudio system tray applet with volume bar.

	[https://github.com/fernandotcl/pa-applet](https://github.com/fernandotcl/pa-applet) || [pa-applet-git](https://aur.archlinux.org/packages/pa-applet-git/)

*   **PNMixer** — A fork of Obmixer. It has many new features such as ALSA channel selection, connect/disconnect detection, shortcuts, etc.

	[https://github.com/nicklan/pnmixer/wiki](https://github.com/nicklan/pnmixer/wiki) || [pnmixer](https://aur.archlinux.org/packages/pnmixer/)

*   **Volctl** — Per-application volume control for GNU/Linux desktops.

	[https://buzz.github.io/volctl/](https://buzz.github.io/volctl/) || [volctl](https://aur.archlinux.org/packages/volctl/)

*   **[Volnoti](/index.php/Volnoti "Volnoti")** — A lightweight volume notification daemon for GNU/Linux and other POSIX operating systems.

	[https://github.com/davidbrazdil/volnoti](https://github.com/davidbrazdil/volnoti) || [volnoti](https://aur.archlinux.org/packages/volnoti/)

*   **Volti** — A GTK application for controlling audio volume from system tray with an internal mixer and support for multimedia keys that uses only ALSA.

	[https://github.com/gen2brain/volti](https://github.com/gen2brain/volti) || [volti](https://aur.archlinux.org/packages/volti/)

*   **VolumeIcon** — Another volume control for your system tray with channel selection, themes and an external mixer.

	[http://softwarebakery.com/maato/volumeicon.html](http://softwarebakery.com/maato/volumeicon.html) || [volumeicon](https://www.archlinux.org/packages/?name=volumeicon)

*   **VolWheel** — A little application which lets you control the sound volume easily through a tray icon you can scroll on.

	[http://oliwer.net/b/volwheel.html](http://oliwer.net/b/volwheel.html) || [volwheel](https://www.archlinux.org/packages/?name=volwheel)

#### CD ripping

See [Optical disc drive#CD 2](/index.php/Optical_disc_drive#CD_2 "Optical disc drive").

#### Visualization

*   **[ProjectM](https://en.wikipedia.org/wiki/MilkDrop "wikipedia:MilkDrop")** — Music visualizer which uses 3D accelerated iterative image-based rendering.

	[http://projectm.sourceforge.net/](http://projectm.sourceforge.net/) || [projectm](https://www.archlinux.org/packages/?name=projectm)

*   **[VSXu](https://en.wikipedia.org/wiki/VSXu "wikipedia:VSXu")** — Free to use program that lets you create and perform real-time audio visual presets.

	[http://www.vsxu.com/](http://www.vsxu.com/) || [vsxu](https://aur.archlinux.org/packages/vsxu/)

*   **cava** — Console-based audio visualizer for Alsa, MPD and PulseAudio.

	[https://karlstav.github.io/cava/](https://karlstav.github.io/cava/) || [cava](https://aur.archlinux.org/packages/cava/)

#### Audio tag editors

*   **Audio Tag Tool** — Tool to edit tags in MP3 and Ogg Vorbis files.

	[http://tagtool.sourceforge.net/](http://tagtool.sourceforge.net/) || [tagtool](https://aur.archlinux.org/packages/tagtool/)

*   **Cowbell** — Elegant music organizer that supports many audio formats including MP3, Ogg/FLAC, and MusePack.

	[http://more-cowbell.org/](http://more-cowbell.org/) || [cowbell](https://aur.archlinux.org/packages/cowbell/)

*   **[EasyTag](https://en.wikipedia.org/wiki/EasyTag "wikipedia:EasyTag")** — Utility for viewing, editing and writing ID3 tags of music files, supports many audio formats.

	[http://easytag.sourceforge.net/](http://easytag.sourceforge.net/) || [easytag](https://www.archlinux.org/packages/?name=easytag)

*   **[Ex Falso](https://en.wikipedia.org/wiki/Ex_Falso_(software) "wikipedia:Ex Falso (software)")** — Cross-platform free and open source audio tag editor and library organizer.

	[https://github.com/quodlibet/quodlibet/](https://github.com/quodlibet/quodlibet/) || [exfalso](https://aur.archlinux.org/packages/exfalso/)

*   **ID3 Mass Tagger** — Command-line utility to edit ID3 1.x and 2.x tags.

	[http://squell.github.io/id3/](http://squell.github.io/id3/) || [id3](https://www.archlinux.org/packages/?name=id3)

*   **Kid3** — MP3, Ogg/Vorbis, FLAC, MPC, MP4/AAC, MP2, Speex, TrueAudio, WavPack, WMA, WAV and AIFF files tag editor.

	[http://kid3.sourceforge.net/](http://kid3.sourceforge.net/) || [kid3](https://www.archlinux.org/packages/?name=kid3)

*   **MP3Info** — MP3 technical info viewer and ID3 1.x tag editor.

	[http://ibiblio.org/mp3info/](http://ibiblio.org/mp3info/) || [mp3info](https://www.archlinux.org/packages/?name=mp3info)

*   **[MusicBrainz Picard](https://en.wikipedia.org/wiki/MusicBrainz_Picard "wikipedia:MusicBrainz Picard")** — Cross-platform audio tag editor written in Python (the official MusicBrainz tagger).

	[http://musicbrainz.org/doc/MusicBrainz_Picard](http://musicbrainz.org/doc/MusicBrainz_Picard) || [picard](https://www.archlinux.org/packages/?name=picard)

*   **[Puddletag](https://en.wikipedia.org/wiki/Puddletag "wikipedia:Puddletag")** — Replacement for the famous MP3tag for Windows.

	[http://puddletag.sourceforge.net/](http://puddletag.sourceforge.net/) || [puddletag](https://www.archlinux.org/packages/?name=puddletag)

*   **taffy** — Simple command-line tag editor for many audio formats.

	[https://github.com/jangler/taffy](https://github.com/jangler/taffy) || [taffy](https://aur.archlinux.org/packages/taffy/)

*   **Tag Editor** — A tag editor with Qt 5 GUI and command-line interface supporting MP4/AAC (iTunes), ID3v1, ID3v2, Ogg/Vorbis and Matroska.

	[https://github.com/Martchus/tageditor](https://github.com/Martchus/tageditor) || [tageditor](https://aur.archlinux.org/packages/tageditor/)

*   **Qoobar** — Universal QT-based audio tagger (specialized for classical music)

	[http://qoobar.sourceforge.net/en/index.htm](http://qoobar.sourceforge.net/en/index.htm) || [qoobar](https://aur.archlinux.org/packages/qoobar/)

#### Sound editing

*   **[Ardour](https://en.wikipedia.org/wiki/Ardour_(software) "wikipedia:Ardour (software)")** — Multichannel hard disk recorder and digital audio workstation.

	[http://ardour.org/](http://ardour.org/) || [ardour](https://www.archlinux.org/packages/?name=ardour)

*   **[Audacity](https://en.wikipedia.org/wiki/Audacity_(audio_editor) "wikipedia:Audacity (audio editor)")** — Program that lets you manipulate digital audio waveforms.

	[http://audacity.sourceforge.net/](http://audacity.sourceforge.net/) || [audacity](https://www.archlinux.org/packages/?name=audacity)

*   **Bitwig Studio** — Proprietary professional digital audio workstation.

	[http://bitwig.com/](http://bitwig.com/) || [bitwig-studio-demo](https://aur.archlinux.org/packages/bitwig-studio-demo/)

*   **Gnac** — Audio converter for GNOME.

	[http://gnac.sourceforge.net/](http://gnac.sourceforge.net/) || [gnac](https://www.archlinux.org/packages/?name=gnac)

*   **GNOME Sound Recorder** — The Sound Recorder application enables you to record and play .flac, .ogg (OGG audio, or .oga), and .wav sound files.

	[https://wiki.gnome.org/Design/Apps/SoundRecorder](https://wiki.gnome.org/Design/Apps/SoundRecorder) || [gnome-sound-recorder](https://www.archlinux.org/packages/?name=gnome-sound-recorder)

*   **[Jokosher](https://en.wikipedia.org/wiki/Jokosher "wikipedia:Jokosher")** — Non-linear multi-track digital audio editor that is being developed in Python, using the GTK+ interface and GStreamer as an audio back-end.

	[https://launchpad.net/jokosher/](https://launchpad.net/jokosher/) || [jokosher](https://aur.archlinux.org/packages/jokosher/)

*   **KWave** — Sound editor for KDE.

	[http://kwave.sourceforge.net/](http://kwave.sourceforge.net/) || [kwave-git](https://aur.archlinux.org/packages/kwave-git/)

*   **[LMMS](/index.php/LMMS "LMMS")** — The Linux MultiMedia Studio. Free cross-platform software which allows you to produce music with your computer.

	[http://lmms.sourceforge.net/](http://lmms.sourceforge.net/) || [lmms](https://www.archlinux.org/packages/?name=lmms)

*   **[Qtractor](https://en.wikipedia.org/wiki/Qtractor "wikipedia:Qtractor")** — Qt-based hard disk recorder and digital audio workstation application that aims to provide digital audio workstation software simple enough for the average home user, and yet powerful enough for the professional user.

	[http://qtractor.sourceforge.net/qtractor-index.html](http://qtractor.sourceforge.net/qtractor-index.html) || [qtractor](https://www.archlinux.org/packages/?name=qtractor)

*   **[Rosegarden](https://en.wikipedia.org/wiki/Rosegarden "wikipedia:Rosegarden")** — Digital audio workstation program developed with ALSA and Qt that acts as an audio and MIDI sequencer, scorewriter and musical composition and editing tool.

	[http://www.rosegardenmusic.com/](http://www.rosegardenmusic.com/) || [rosegarden](https://www.archlinux.org/packages/?name=rosegarden)

*   **XCFA** — Tool to extract the contens of audio CDs and convert them to various formats.

	[http://www.xcfa.tuxfamily.org/](http://www.xcfa.tuxfamily.org/) || [xcfa](https://aur.archlinux.org/packages/xcfa/)

### Video

#### Video players

See also [Wikipedia:Comparison of video player software](https://en.wikipedia.org/wiki/Comparison_of_video_player_software "wikipedia:Comparison of video player software").

##### Console

*   **[FFplay](/index.php/FFmpeg "FFmpeg")** — Very simple and portable media player using the FFmpeg libraries and the SDL library.

	[http://ffmpeg.org/](http://ffmpeg.org/) || [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)

*   **[gst-play-1.0](/index.php/GStreamer "GStreamer")** — Simple command line playback testing tool for GStreamer.

	[https://gstreamer.freedesktop.org/](https://gstreamer.freedesktop.org/) || [gst-plugins-base-libs](https://www.archlinux.org/packages/?name=gst-plugins-base-libs)

*   **[MPlayer](/index.php/MPlayer "MPlayer")** — Video player that supports a complete and versatile array of video and audio formats.

	[http://www.mplayerhq.hu/design7/news.html](http://www.mplayerhq.hu/design7/news.html) || [mplayer](https://www.archlinux.org/packages/?name=mplayer)

*   **[mpv](/index.php/Mpv "Mpv")** — Movie player based on MPlayer and mplayer2.

	[http://mpv.io](http://mpv.io) || [mpv](https://www.archlinux.org/packages/?name=mpv)

*   **[xine-ui](https://en.wikipedia.org/wiki/xine "wikipedia:xine")** — Free multimedia player.

	[http://www.xine-project.org](http://www.xine-project.org) || [xine-ui](https://www.archlinux.org/packages/?name=xine-ui)

*   **[VLC media player (Ncurses interface)](/index.php/VLC_media_player "VLC media player")** — Command-line version of the famous video player that can play smoothly high definition videos in the TTY. Can be launched with `vlc -I ncurses`.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

##### Graphical

See also: [MPlayer#Frontends/GUIs](/index.php/MPlayer#Frontends.2FGUIs "MPlayer"), [mpv#Front ends](/index.php/Mpv#Front_ends "Mpv").

*   **Deepin Movie** — Movie player based on QtAV.

	[https://github.com/linuxdeepin/deepin-movie](https://github.com/linuxdeepin/deepin-movie) || [deepin-movie](https://www.archlinux.org/packages/?name=deepin-movie)

*   **[Dragon Player](https://en.wikipedia.org/wiki/Kdemultimedia#Dragon_Player "wikipedia:Kdemultimedia")** — Simple video player for KDE. Part of the [kdemultimedia](https://www.archlinux.org/groups/x86_64/kdemultimedia/) group.

	[http://www.kde.org/applications/multimedia/dragonplayer/](http://www.kde.org/applications/multimedia/dragonplayer/) || [dragon](https://www.archlinux.org/packages/?name=dragon)

*   **[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")** — Media player (audio and video) for the GNOME desktop that uses GStreamer. Part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

	[https://wiki.gnome.org/Apps/Videos](https://wiki.gnome.org/Apps/Videos) || [totem](https://www.archlinux.org/packages/?name=totem)

*   **[Kaffeine](https://en.wikipedia.org/wiki/Kaffeine "wikipedia:Kaffeine")** — Very versatile KDE media player that, by default, utilizes VLC as its backend and has excellent support of digital TV (DVB).

	[http://kaffeine.kde.org/](http://kaffeine.kde.org/) || [kaffeine](https://www.archlinux.org/packages/?name=kaffeine)

*   **Parole** — Modern media player based on the GStreamer framework.

	[http://goodies.xfce.org/projects/applications/parole/](http://goodies.xfce.org/projects/applications/parole/) || [parole](https://www.archlinux.org/packages/?name=parole)

*   **Rage** — Video and audio player written with Enlightenment Foundation Libraries with some extra bells and whistles.

	[http://www.enlightenment.org/p.php?p=about/rage](http://www.enlightenment.org/p.php?p=about/rage) || [rage](https://aur.archlinux.org/packages/rage/)

*   **Snappy** — Powerful media player with a minimalistic interface that uses GStreamer.

	[https://wiki.gnome.org/Apps/Snappy](https://wiki.gnome.org/Apps/Snappy) || [snappy-player](https://www.archlinux.org/packages/?name=snappy-player)

*   **QMLPlayer** — Simple media player based on QtAV.

	[http://www.qtav.org/](http://www.qtav.org/) || [qtav](https://www.archlinux.org/packages/?name=qtav)

*   **QMPlay2** — QMPlay2 is a QT based video player. It can play and stream all formats supported by ffmpeg and libmodplug. It has on integrated module system, which includes a Youtube browser.

	[http://qt-apps.org/content/show.php/QMPlay2?content=153339](http://qt-apps.org/content/show.php/QMPlay2?content=153339) || [qmplay2](https://aur.archlinux.org/packages/qmplay2/)

*   **[VLC media player](/index.php/VLC_media_player "VLC media player")** — Middleweight video player with support for a wide variety of audio and video formats.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **Whaaw! Media Player** — Lightweight GStreamer-based audio and video player that can serve as a good alternative to Totem for those who do not like all of those GNOME dependencies.

	[http://home.gna.org/whaawmp/](http://home.gna.org/whaawmp/) || [whaawmp](https://www.archlinux.org/packages/?name=whaawmp)

*   **Xnoise** — GTK+ and GStreamer-based media player for both audio and video with "a slick GUI, great speed and lots of features." (development ceased)

	[http://www.xnoise-media-player.com/](http://www.xnoise-media-player.com/) || [xnoise](https://www.archlinux.org/packages/?name=xnoise)

#### Subtitles

*   **Gaupol** — Full-featured subtitle editor.

	[http://home.gna.org/gaupol](http://home.gna.org/gaupol) || [gaupol](https://www.archlinux.org/packages/?name=gaupol)

*   **[Gnome Subtitles](https://en.wikipedia.org/wiki/Gnome_Subtitles "wikipedia:Gnome Subtitles")** — Video subtitle editor for GNOME.

	[http://www.gnomesubtitles.org/](http://www.gnomesubtitles.org/) || [gnome-subtitles](https://www.archlinux.org/packages/?name=gnome-subtitles)

*   **Penguin Subtitle Player** — Penguin Subtitle Player is an open-source, cross-platform standalone subtitle player, as an alternative to Greenfish Subtitle Player, SrtViewer (Mac), SRTPlayer, JustSubsPlayer and Free Subtitle Player.

	[https://github.com/carsonip/Penguin-Subtitle-Player](https://github.com/carsonip/Penguin-Subtitle-Player) || [penguin-subtitle-player-git](https://aur.archlinux.org/packages/penguin-subtitle-player-git/)

*   **subdl** — Automatic subtitle downloader.

	[https://github.com/akexakex/subdl](https://github.com/akexakex/subdl) || [subdl](https://www.archlinux.org/packages/?name=subdl)

*   **SubtitlesPrinter** — Print subtitles above a X-screen, independently of the video player.

	[https://github.com/OlivierMarty/SubtitlesPrinter](https://github.com/OlivierMarty/SubtitlesPrinter) || [subtitles-printer-git](https://aur.archlinux.org/packages/subtitles-printer-git/)

*   **Subtitle Composer** — open-source Subtitle editor with Qt 5 based GUI supporting various formats, features different player backends, able to display wave form

	[https://github.com/maxrd2/subtitlecomposer](https://github.com/maxrd2/subtitlecomposer) || [subtitlecomposer](https://aur.archlinux.org/packages/subtitlecomposer/)

#### DVD ripping

See [Optical disc drive#DVD 2](/index.php/Optical_disc_drive#DVD_2 "Optical disc drive").

#### Video editors

See also [Wikipedia:Comparison of video editing software](https://en.wikipedia.org/wiki/Comparison_of_video_editing_software "wikipedia:Comparison of video editing software").

##### Console

*   **[Avidemux](https://en.wikipedia.org/wiki/Avidemux "wikipedia:Avidemux")** — Free video editor designed for simple cutting, filtering and encoding tasks.

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-cli](https://www.archlinux.org/packages/?name=avidemux-cli)

*   **[FFmpeg](/index.php/FFmpeg "FFmpeg")** — Complete, cross-platform solution to record, convert and stream audio and video.

	[http://ffmpeg.org/](http://ffmpeg.org/) || [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)

*   **HandBrake-CLI** — Simple yet powerful video transcoder ideal for batch mkv/x264 ripping.

	[http://handbrake.fr/](http://handbrake.fr/) || [handbrake-cli](https://www.archlinux.org/packages/?name=handbrake-cli)

##### Graphical

*   **[Avidemux](https://en.wikipedia.org/wiki/Avidemux "wikipedia:Avidemux")** — Free video editor designed for simple cutting, filtering and encoding tasks.

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-gtk](https://www.archlinux.org/packages/?name=avidemux-gtk) [avidemux-qt](https://www.archlinux.org/packages/?name=avidemux-qt)

*   **[Cinelerra (Community Version)](https://en.wikipedia.org/wiki/Cinelerra "wikipedia:Cinelerra")** — Professional video editing and compositing environment.

	[http://cinelerra.org/](http://cinelerra.org/) || [cinelerra-cv](https://www.archlinux.org/packages/?name=cinelerra-cv)

*   **Flowblade** — Flowblade is a multitrack non-linear video editor for Linux, designed to provide a fast, robust editing experience.

	[https://github.com/jliljebl/flowblade](https://github.com/jliljebl/flowblade) || [flowblade](https://aur.archlinux.org/packages/flowblade/)

*   **HandBrake** — Simple yet powerful video transcoder ideal for batch mkv/x264 ripping. GTK+ version.

	[http://handbrake.fr/](http://handbrake.fr/) || [handbrake](https://www.archlinux.org/packages/?name=handbrake)

*   **[Kdenlive](https://en.wikipedia.org/wiki/Kdenlive "wikipedia:Kdenlive")** — Non-linear video editor designed for basic to semi-professional work.

	[http://kdenlive.org/](http://kdenlive.org/) || [kdenlive](https://www.archlinux.org/packages/?name=kdenlive)

*   **[Lightworks](https://en.wikipedia.org/wiki/Lightworks "wikipedia:Lightworks")** — A proprietary professional non-linear editing system for editing and mastering digital video in various formats.

	[http://www.lwks.com/](http://www.lwks.com/) || [lwks](https://aur.archlinux.org/packages/lwks/)

*   **[LiVES](https://en.wikipedia.org/wiki/LiVES "wikipedia:LiVES")** — Video editor and VJ (live performance) platform.

	[http://lives-video.com/](http://lives-video.com/) || [lives](https://aur.archlinux.org/packages/lives/)

*   **[Open Shot](https://en.wikipedia.org/wiki/OpenShot_Video_Editor "wikipedia:OpenShot Video Editor")** — Non-linear video editor based on MLT framework.

	[http://www.openshotvideo.com/](http://www.openshotvideo.com/) || [openshot](https://www.archlinux.org/packages/?name=openshot)

*   **[PiTiVi](https://en.wikipedia.org/wiki/Pitivi "wikipedia:Pitivi")** — Video editor designed to be intuitive and integrate well in the GNOME desktop.

	[http://www.pitivi.org/](http://www.pitivi.org/) || [pitivi](https://www.archlinux.org/packages/?name=pitivi)

*   **[Shotcut](https://en.wikipedia.org/wiki/Shotcut "wikipedia:Shotcut")** — Shotcut is a free, open source, cross-platform video editor.

	[http://www.shotcut.org/](http://www.shotcut.org/) || [shotcut-bin](https://aur.archlinux.org/packages/shotcut-bin/)

*   **Transmageddon** — Simple python application for transcoding video into formats supported by GStreamer.

	[http://www.linuxrising.org/](http://www.linuxrising.org/) || [transmageddon](https://www.archlinux.org/packages/?name=transmageddon)

#### Screencast

See also [Wikipedia:Comparison of screencasting software](https://en.wikipedia.org/wiki/Comparison_of_screencasting_software "wikipedia:Comparison of screencasting software").

Screencast utilities allow you to create a video of your desktop or individual windows.

*   **byzanz** — Simple screencast tool that produces GIF animations.

	[http://blogs.gnome.org/otte/2009/08/30/byzanz-0-2-0/](http://blogs.gnome.org/otte/2009/08/30/byzanz-0-2-0/) || [byzanz](https://aur.archlinux.org/packages/byzanz/)

*   **glc** — Screencast tool that can capture the sound and video from OpenGL applications, such as games, where regular X11 screencast tools produce choppy results.

	[https://github.com/nullkey/glc](https://github.com/nullkey/glc) || [glc](https://aur.archlinux.org/packages/glc/)

*   **Istanbul** — Simple desktop session recorder that produces ogg videos.

	[https://wiki.gnome.org/Projects/Istanbul](https://wiki.gnome.org/Projects/Istanbul) || [istanbul](https://aur.archlinux.org/packages/istanbul/)

*   **Kazam** — Screencasting program with design in mind. Handles multiscreen setups.

	[https://launchpad.net/kazam](https://launchpad.net/kazam) || [kazam](https://aur.archlinux.org/packages/kazam/)

*   **OBS** — Free and open source software for video recording and live streaming.

	[https://obsproject.com/](https://obsproject.com/) || [obs-studio](https://www.archlinux.org/packages/?name=obs-studio)

*   **[RecordMyDesktop](https://en.wikipedia.org/wiki/RecordMyDesktop "wikipedia:RecordMyDesktop")** — An easy to use utility that records your desktop into the ogg format with a CLI, Qt or GTK+ interface.

	[http://recordmydesktop.sourceforge.net/](http://recordmydesktop.sourceforge.net/) || [recordmydesktop](https://www.archlinux.org/packages/?name=recordmydesktop) [gtk-recordmydesktop](https://www.archlinux.org/packages/?name=gtk-recordmydesktop) [qt-recordmydesktop](https://www.archlinux.org/packages/?name=qt-recordmydesktop)

*   **simplescreenrecorder** — A feature-rich screen recorder written in C++/Qt4 that supports X11 and OpenGL.

	[http://www.maartenbaert.be/simplescreenrecorder/](http://www.maartenbaert.be/simplescreenrecorder/) || [simplescreenrecorder](https://www.archlinux.org/packages/?name=simplescreenrecorder)

*   **vokoscreen** — Simple screencast tool, GUI ffmpeg.

	[http://www.kohaupt-online.de/hp](http://www.kohaupt-online.de/hp) || [vokoscreen](https://aur.archlinux.org/packages/vokoscreen/)

*   **[XVidCap](https://en.wikipedia.org/wiki/XVidCap "wikipedia:XVidCap")** — Application used for recording a screencast or digital recording of an X Window System screen output with an audio narration.

	[http://xvidcap.sourceforge.net/](http://xvidcap.sourceforge.net/) || [xvidcap](https://aur.archlinux.org/packages/xvidcap/)

*   **FFcast** — FFmpeg-based screencast tool written in Bash.

	[https://github.com/lolilolicon/FFcast](https://github.com/lolilolicon/FFcast) || [ffcast](https://aur.archlinux.org/packages/ffcast/)

### Mobile phone managers

*   **[gnokii](https://en.wikipedia.org/wiki/Gnokii "wikipedia:Gnokii")** — Tools and user space driver for use with mobile phones.

	[http://www.gnokii.org/](http://www.gnokii.org/) || [gnokii](https://www.archlinux.org/packages/?name=gnokii)

*   **GNOME Phone Manager** — Control your mobile phone from your GNOME desktop.

	[https://wiki.gnome.org/PhoneManager](https://wiki.gnome.org/PhoneManager) || [gnome-phone-manager](https://www.archlinux.org/packages/?name=gnome-phone-manager)

*   **KDE Connect** — A project that aims to communicate all your devices.

	[http://community.kde.org/KDEConnect](http://community.kde.org/KDEConnect) || [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect)

*   **Moto4Lin** — File manager and seem editor for Motorola P2K phones (like C380/C650).

	[http://sourceforge.net/projects/moto4lin/](http://sourceforge.net/projects/moto4lin/) || [moto4lin](https://aur.archlinux.org/packages/moto4lin/)

### Digital camera managers

See [Digital Cameras#Other frontend applications for libgphoto2](/index.php/Digital_Cameras#Other_frontend_applications_for_libgphoto2 "Digital Cameras").

### Optical media burning

See [Optical disc drive#Burning CD/DVD/BD with a GUI](/index.php/Optical_disc_drive#Burning_CD.2FDVD.2FBD_with_a_GUI "Optical disc drive").

### Podcasts

see [Podcast clients](/index.php/List_of_applications/Internet#Podcast_clients "List of applications/Internet")

### Collection managers

*   **[Beets](/index.php/Beets "Beets")** — Music library organizer, tagger and more.

	[http://beets.radbox.org/](http://beets.radbox.org/) || [beets](https://www.archlinux.org/packages/?name=beets)

*   **Demlo** — Batch music tagger, encoder, renamer and more.

	[http://ambrevar.bitbucket.org/demlo/](http://ambrevar.bitbucket.org/demlo/) || [demlo](https://aur.archlinux.org/packages/demlo/)

*   **[GCstar](https://en.wikipedia.org/wiki/GCstar "wikipedia:GCstar")** — GNOME application for organizing various collections (board games, comic books, movies, stamps, etc.).

	[http://www.gcstar.org/](http://www.gcstar.org/) || [gcstar](https://www.archlinux.org/packages/?name=gcstar)

*   **[Kodi](/index.php/Kodi "Kodi")** — Application for organizing various collections and automatically retrieving info about them (video, music, photos).

	[https://kodi.tv/](https://kodi.tv/) || [kodi](https://www.archlinux.org/packages/?name=kodi)

*   **[Tellico](https://en.wikipedia.org/wiki/Tellico "wikipedia:Tellico")** — KDE application for organizing various collections (books, video, music, coins, etc.).

	[http://tellico-project.org/](http://tellico-project.org/) || [tellico](https://www.archlinux.org/packages/?name=tellico)

### Lyrics fetchers

*   **clyrics** — An extensible lyrics fetcher, with daemon support for cmus and mocp.

	[http://beets.radbox.org/](http://beets.radbox.org/) || [clyrics](https://aur.archlinux.org/packages/clyrics/)

## Utilities

### Partitioning tools

See [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").

### Mount tools

*   **9mount** — Mount 9p filesystems.

	[http://sqweek.net/code/9mount/](http://sqweek.net/code/9mount/) || [9mount](https://aur.archlinux.org/packages/9mount/)

*   **cryptmount** — Mount an encrypted file system as a regular user.

	[http://cryptmount.sourceforge.net/](http://cryptmount.sourceforge.net/) || [cryptmount](https://aur.archlinux.org/packages/cryptmount/)

*   **ldm** — A lightweight daemon that mounts drives automagically using *udev*

	[https://github.com/LemonBoy/ldm](https://github.com/LemonBoy/ldm) || [ldm](https://aur.archlinux.org/packages/ldm/)

*   **pmount** — Mount *source* as a regular user to an automatically created destination `/media/*source_name*`.

	[http://pmount.alioth.debian.org/](http://pmount.alioth.debian.org/) || [pmount](https://aur.archlinux.org/packages/pmount/)

*   **pmount-safe-removal** — Mount removable devices as regular user with safe removal

	[http://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device](http://mywaytoarch.tumblr.com/post/13111098534/pmount-safe-removal-of-usb-device) || [pmount-safe-removal](https://aur.archlinux.org/packages/pmount-safe-removal/)

*   **udevil** — Mounts removable devices as a regular user, show device info, and monitor device changes. Only depends on *udev* and glib.

	[http://ignorantguru.github.io/udevil](http://ignorantguru.github.io/udevil) || [udevil](https://www.archlinux.org/packages/?name=udevil)

*   **ws** — Mount Windows network shares ([CIFS](https://en.wikipedia.org/wiki/Server_Message_Block "wikipedia:Server Message Block") and [VFS](https://en.wikipedia.org/wiki/Virtual_file_system "wikipedia:Virtual file system")).

	[http://winshares.sourceforge.net/](http://winshares.sourceforge.net/) || [ws](https://aur.archlinux.org/packages/ws/)

*   **zulucrypt** — A GUI frontend for cryptsetup to create, manage and mount encrypted volumes; supports encfs as well

	[http://mhogomchungu.github.io/zuluCrypt/](http://mhogomchungu.github.io/zuluCrypt/) || [zulucrypt](https://aur.archlinux.org/packages/zulucrypt/)

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

	[http://www.gnu.org/software/coreutils](http://www.gnu.org/software/coreutils) || [coreutils](https://www.archlinux.org/packages/?name=coreutils)

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

	[http://bluej.org/](http://bluej.org/) || [bluej](https://aur.archlinux.org/packages/bluej/)

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "wikipedia:Brackets (text editor)")** — A free open-source editor written in HTML, CSS, and Javascript with a primary focus on Web Development. It was created by Adobe Systems, licensed under the MIT License, and is currently maintained on GitHub.

	[http://brackets.io/](http://brackets.io/) || [brackets](https://aur.archlinux.org/packages/brackets/)

*   **[Builder](https://en.wikipedia.org/wiki/GNOME_Builder "wikipedia:GNOME Builder")** — General purpose IDE for GNOME.

	[https://wiki.gnome.org/Apps/Builder](https://wiki.gnome.org/Apps/Builder) || [gnome-builder](https://www.archlinux.org/packages/?name=gnome-builder)

*   **[Code::Blocks](https://en.wikipedia.org/wiki/Code::Blocks "wikipedia:Code::Blocks")** — Open source and cross-platform C/C++ IDE.

	[http://www.codeblocks.org/](http://www.codeblocks.org/) || [codeblocks](https://www.archlinux.org/packages/?name=codeblocks)

*   **[Cloud9](https://en.wikipedia.org/wiki/Cloud9_IDE "wikipedia:Cloud9 IDE")** — State-of-the-art IDE that runs in your browser and lives in the cloud, allowing you to run, debug and deploy applications from anywhere, anytime.

	[https://c9.io/](https://c9.io/) || [c9.core](https://aur.archlinux.org/packages/c9.core/)

*   **[Eclipse](/index.php/Eclipse "Eclipse")** — Open source community project, which aims to provide a universal development platform.

	[http://eclipse.org/](http://eclipse.org/) || [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java), [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp), [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php)

*   **[Editra](https://en.wikipedia.org/wiki/Editra "wikipedia:Editra")** — Multi-platform text editor with an implementation that focuses on creating an easy to use interface and features that aid in code development.

	[http://www.editra.org](http://www.editra.org) || [editra-svn](https://aur.archlinux.org/packages/editra-svn/)

*   **[Eric](https://en.wikipedia.org/wiki/Eric_Python_IDE "wikipedia:Eric Python IDE")** — Full-featured Python and Ruby IDE in PyQt5.

	[http://eric-ide.python-projects.org/](http://eric-ide.python-projects.org/) || [eric](https://www.archlinux.org/packages/?name=eric)

*   **[Gambas](/index.php/Gambas "Gambas")** — Free development environment based on a Basic interpreter with object extensions.

	[http://gambas.sourceforge.net/en/main.html](http://gambas.sourceforge.net/en/main.html) || [gambas3-ide](https://www.archlinux.org/packages/?name=gambas3-ide)

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — Text editor using the GTK+ toolkit with basic features of an integrated development environment.

	[https://geany.org](https://geany.org) || [geany](https://www.archlinux.org/packages/?name=geany)

*   **IEP** — Cross-platform Python IDE focused on interactivity and introspection, which makes it very suitable for scientific computing.

	[http://iep-project.org/](http://iep-project.org/) || [iep](https://aur.archlinux.org/packages/iep/)

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

*   **[QDevelop](https://en.wikipedia.org/wiki/QDevelop "wikipedia:QDevelop")** — Free and cross-platform IDE for Qt.

	[https://code.google.com/archive/p/qdevelop/](https://code.google.com/archive/p/qdevelop/) || [qdevelop-svn](https://aur.archlinux.org/packages/qdevelop-svn/)

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

See also [Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators").

Power users use terminal emulators quite often, so unsurprisingly lots of X11 terminal emulators exist. Most of them emulate Xterm that emulates VT102, which emulates typewriter, so you will have to read the [Wikipedia article](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator") and [other sources](https://google.com/search?q=linux+terminal+emulators) to get a hold on these things.

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

	[http://rxvt.sourceforge.net/](http://rxvt.sourceforge.net/) || [rxvt](https://www.archlinux.org/packages/?name=rxvt)

*   **shellinabox** — A web-based SSH Terminal

	[https://github.com/shellinabox/shellinabox](https://github.com/shellinabox/shellinabox) || [shellinabox-git](https://aur.archlinux.org/packages/shellinabox-git/)

*   **[st](/index.php/St "St")** — Simple terminal implementation for X.

	[http://st.suckless.org](http://st.suckless.org) || [st](https://www.archlinux.org/packages/?name=st)

*   **Terminal** — A terminal emulator, that supports multiple windows, scroll buffer and all the expected features. A part of GNUstep.

	[http://gap.nongnu.org/terminal/index.html](http://gap.nongnu.org/terminal/index.html) || [gnustep-terminal](https://aur.archlinux.org/packages/gnustep-terminal/)

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

	[http://calno.com/evilvte/](http://calno.com/evilvte/) || [evilvte](https://aur.archlinux.org/packages/evilvte/)

*   **Germinal** — Minimalist terminal emulator which provides a borderless maximized terminal, attached to a tmux session by default, hence providing tabs and panels.

	[http://www.imagination-land.org/tags/germinal.html](http://www.imagination-land.org/tags/germinal.html) || [germinal](https://aur.archlinux.org/packages/germinal/)

*   **[GNOME Terminal](https://en.wikipedia.org/wiki/GNOME_Terminal "wikipedia:GNOME Terminal")** — A terminal emulator included in the [GNOME](/index.php/GNOME "GNOME") desktop with support for Unicode and pseudo-transparency.

	[https://wiki.gnome.org/Apps/Terminal](https://wiki.gnome.org/Apps/Terminal) || [gnome-terminal](https://www.archlinux.org/packages/?name=gnome-terminal)

*   **[Guake](/index.php/Guake "Guake")** — Drop-down terminal for the GNOME desktop.

	[http://guake-project.org/](http://guake-project.org/) || [guake](https://www.archlinux.org/packages/?name=guake)

*   **Terra** — is a GTK+3.0 based terminal emulator with useful user interface, it also supports multiple terminals with splitting screen horizontally or vertically -- (similar to guake).

	[https://github.com/ozcan/terra-terminal](https://github.com/ozcan/terra-terminal) || [terra](https://aur.archlinux.org/packages/terra/)

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

	[https://code.google.com/archive/p/stjerm-terminal-emulator/](https://code.google.com/archive/p/stjerm-terminal-emulator/) || [stjerm-git](https://aur.archlinux.org/packages/stjerm-git/)

*   **[Terminal](https://en.wikipedia.org/wiki/Terminal_(Xfce) "wikipedia:Terminal (Xfce)")** — Terminal emulator included in the [Xfce](/index.php/Xfce "Xfce") desktop with support for a colorized prompt and a tabbed interface.

	[http://docs.xfce.org/apps/terminal/start](http://docs.xfce.org/apps/terminal/start) || [xfce4-terminal](https://www.archlinux.org/packages/?name=xfce4-terminal)

*   **Terminix** — A tiling terminal emulator for Linux using GTK+ 3

	[https://github.com/gnunn1/terminix](https://github.com/gnunn1/terminix) || [terminix](https://aur.archlinux.org/packages/terminix/), [terminix-git](https://aur.archlinux.org/packages/terminix-git/)

*   **Termit** — Simple terminal emulator based on the vte library that includes tabs, bookmarks, and the ability to switch encodings.

	[https://github.com/nonstop/termit/wiki](https://github.com/nonstop/termit/wiki) || [termit](https://aur.archlinux.org/packages/termit/)

*   **[Termite](/index.php/Termite "Termite")** — A keyboard-centric VTE-based terminal, aimed at use within a window manager with tiling and/or tabbing support.

	[https://github.com/thestinger/termite](https://github.com/thestinger/termite) || [termite](https://www.archlinux.org/packages/?name=termite)

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

*   **[Dolphin](/index.php/Dolphin "Dolphin")** — File manager included in the KDE4 desktop.

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

	[http://www.konqueror.org/](http://www.konqueror.org/) || [kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)

*   **[Krusader](https://en.wikipedia.org/wiki/Krusader "wikipedia:Krusader")** — Advanced twin panel (Midnight Commander style) file manager for the KDE desktop.

	[http://www.krusader.org/](http://www.krusader.org/) || [krusader](https://www.archlinux.org/packages/?name=krusader)

*   **muCommander** — A lightweight, cross-platform file manager with a dual-pane interface written in Java.

	[http://www.mucommander.com/](http://www.mucommander.com/) || [mucommander](https://aur.archlinux.org/packages/mucommander/)

*   **[Nemo](/index.php/Nemo "Nemo")** — Nemo is the file manager of the Cinnamon desktop. A good alternative to Nautilus.

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

#### Desktop search engines

See also [Wikipedia:List of search engines#Desktop search engines](https://en.wikipedia.org/wiki/List_of_search_engines#Desktop_search_engines "wikipedia:List of search engines").

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

*   **Pinot** — Personal search and metasearch tool

	[https://code.google.com/archive/p/pinot-search/](https://code.google.com/archive/p/pinot-search/) || [pinot](https://www.archlinux.org/packages/?name=pinot)

*   **Recoll** — Full text search tool based on Xapian backend

	[http://www.lesbonscomptes.com/recoll/](http://www.lesbonscomptes.com/recoll/) || [recoll](https://www.archlinux.org/packages/?name=recoll)

*   **Searchmonkey** — A powerful GUI search utility for matching regex patterns

	[http://searchmonkey.sourceforge.net/](http://searchmonkey.sourceforge.net/) || [searchmonkey](https://aur.archlinux.org/packages/searchmonkey/)

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

*   **Xarchive** — Generic GTK2 front-end that uses external wrappers around commandline archiving tools.

	[http://xarchive.sourceforge.net/](http://xarchive.sourceforge.net/) || [xarchive](https://aur.archlinux.org/packages/xarchive/)

*   **[Xarchiver](https://en.wikipedia.org/wiki/Xarchiver "wikipedia:Xarchiver")** — Lightweight desktop independent archive manager built with GTK+.

	[https://github.com/ib/xarchiver](https://github.com/ib/xarchiver) || [xarchiver](https://www.archlinux.org/packages/?name=xarchiver)

#### Comparison, diff, merge

See also [Wikipedia:Comparison of file comparison tools](https://en.wikipedia.org/wiki/Comparison_of_file_comparison_tools "wikipedia:Comparison of file comparison tools").

*   **Beyond Compare** — A graphical tool for comparing files and folders, and generating reports.

	[http://www.scootersoftware.com/](http://www.scootersoftware.com/) || [beyond-compare](https://aur.archlinux.org/packages/beyond-compare/)

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

### Disk cleaning

*   **[BleachBit](https://en.wikipedia.org/wiki/BleachBit "wikipedia:BleachBit")** — It frees disk space and guards your privacy; frees cache, deletes cookies, clears Internet history, shreds temporary files, deletes logs, and discards junk you didn't know was there.

	[http://bleachbit.sourceforge.net/](http://bleachbit.sourceforge.net/) || [bleachbit](https://www.archlinux.org/packages/?name=bleachbit)

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

### Clock synchronization

*   **[NTPd](/index.php/NTPd "NTPd")** — Network Time Protocol reference implementation.

	[http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project](http://support.ntp.org/bin/view/Main/WebHome#The_NTP_Project) || [ntp](https://www.archlinux.org/packages/?name=ntp)

*   **[Chrony](/index.php/Chrony "Chrony")** — Lightweight NTP client and server.

	[http://chrony.tuxfamily.org/](http://chrony.tuxfamily.org/) || [chrony](https://www.archlinux.org/packages/?name=chrony)

*   **[OpenNTPD](/index.php/OpenNTPD "OpenNTPD")** — Free, easy to use implementation of the Network Time Protocol.

	[http://www.openntpd.org/](http://www.openntpd.org/) || [openntpd](https://www.archlinux.org/packages/?name=openntpd)

### System maintenance

*   **cylon** — Updates, Maintenance , anti-malware , backups and system checks in a menu driven Bash script.

	[https://github.com/gavinlyonsrepo/cylon](https://github.com/gavinlyonsrepo/cylon) || [cylon](https://aur.archlinux.org/packages/cylon/)

### System monitoring

See also [Category:Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification").

*   **adesklet SystemMonitor** — Collection of modular stackable system monitors for [adesklets](https://en.wikipedia.org/wiki/Adesklets "wikipedia:Adesklets").

	[http://adesklets.sourceforge.net/desklets.html](http://adesklets.sourceforge.net/desklets.html) || [adesklet-systemmonitor](https://aur.archlinux.org/packages/adesklet-systemmonitor/)

*   **candybar** — WebKit-based status line for tiling window managers.

	[https://github.com/Lokaltog/candybar](https://github.com/Lokaltog/candybar) || [candybar-git](https://aur.archlinux.org/packages/candybar-git/)

*   **[Conky](/index.php/Conky "Conky")** — Lightweight, scriptable system monitor.

	[https://github.com/brndnmtthws/conky](https://github.com/brndnmtthws/conky) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **Collectd** — A simple, extensible system monitoring daemon based on [rrdtool](http://oss.oetiker.ch/rrdtool/). It has a small footprint and can be set up either stand-alone or as a server/client application.

	[https://collectd.org/](https://collectd.org/) || [collectd](https://www.archlinux.org/packages/?name=collectd)

*   **dstat** — Versatile resource statistics tool.

	[http://dag.wieers.com/home-made/dstat/](http://dag.wieers.com/home-made/dstat/) || [dstat](https://www.archlinux.org/packages/?name=dstat)

*   **[GKrellM](https://en.wikipedia.org/wiki/GKrellM "wikipedia:GKrellM")** — Simple, flexible system monitor package for [GTK+](/index.php/GTK%2B "GTK+") with many plug-ins.

	[http://billw2.github.io/gkrellm/gkrellm.html](http://billw2.github.io/gkrellm/gkrellm.html) || [gkrellm](https://www.archlinux.org/packages/?name=gkrellm)

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

*   **archey3-git** — Python script to display system infomation alongside the Arch Linux logo.

	[http://www.generictestdomain.net/archey3/](http://www.generictestdomain.net/archey3/) || [archey3-git](https://aur.archlinux.org/packages/archey3-git/)

*   **dmidecode** — It reports information about your system's hardware as described in your system BIOS according to the SMBIOS/DMI standard.

	[http://www.nongnu.org/dmidecode/](http://www.nongnu.org/dmidecode/) || [dmidecode](https://www.archlinux.org/packages/?name=dmidecode)|

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

### Trash management

*   **trash-cli** — A command-line interface implementing FreeDesktop.org's Trash specification.

	[https://github.com/andreafrancia/trash-cli](https://github.com/andreafrancia/trash-cli) || [trash-cli](https://www.archlinux.org/packages/?name=trash-cli)

### File synchronization

See [Synchronization and backup programs#Data synchronization](/index.php/Synchronization_and_backup_programs#Data_synchronization "Synchronization and backup programs").

### Finders

*   **fuzzy-find** — Fuzzy completion for finding files.

	[https://github.com/silentbicycle/ff](https://github.com/silentbicycle/ff) || [ff-git](https://aur.archlinux.org/packages/ff-git/)

*   **fzf** — General-purpose command-line fuzzy finder.

	[https://github.com/junegunn/fzf](https://github.com/junegunn/fzf) || [fzf](https://www.archlinux.org/packages/?name=fzf) [fzf-git](https://aur.archlinux.org/packages/fzf-git/)

*   **rmlint** — Tool to quickly find (and optionally remove) duplicate files and other lint

	[https://rmlint.readthedocs.org/en/latest/](https://rmlint.readthedocs.org/en/latest/) || [rmlint](https://www.archlinux.org/packages/?name=rmlint)

## Documents and texts

### Office suites

See also [Wikipedia:Comparison of office suites](https://en.wikipedia.org/wiki/Comparison_of_office_suites "wikipedia:Comparison of office suites").

*   **[Calligra](https://en.wikipedia.org/wiki/Calligra_Suite "wikipedia:Calligra Suite")** — Actively developed fork of KOffice, the [KDE](/index.php/KDE "KDE") office suite. It offers most of the features of OpenOffice while also having versions for smartphones (Calligra Mobile) and tablets (Calligra Active).

	[https://www.calligra.org/](https://www.calligra.org/) || [calligra](https://www.archlinux.org/groups/x86_64/calligra/)

*   **[LibreOffice](/index.php/LibreOffice "LibreOffice")** — More actively developed fork of OpenOffice.

	[https://www.libreoffice.org/](https://www.libreoffice.org/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice](/index.php/OpenOffice "OpenOffice")** — Open-source office software suite for word processing, spreadsheets, presentations, graphics, databases and more, under the Apache Licence.

	[http://www.openoffice.org/](http://www.openoffice.org/) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **[Siag Office](https://en.wikipedia.org/wiki/Siag_Office "wikipedia:Siag Office")** — Extremely lightweight office suite that provides a word processor, spreadsheet, text editor, file manager and previewer.

	[http://siag.nu/](http://siag.nu/) || [siag-office](https://aur.archlinux.org/packages/siag-office/)

*   **[SoftMaker Office](https://en.wikipedia.org/wiki/SoftMaker_Office "wikipedia:SoftMaker Office")** — A complete, reliable, lightning-fast and Microsoft Office-compatible office suite with a word processor, spreadsheet, and presentation graphics software.

	[http://www.freeoffice.com/](http://www.freeoffice.com/) || [freeoffice](https://aur.archlinux.org/packages/freeoffice/)

*   **[WPS Office](https://en.wikipedia.org/wiki/Kingsoft_Office "wikipedia:Kingsoft Office")** — Proprietary office productivity suite, previously known as Kingsoft Office.

	[http://www.wps.com/](http://www.wps.com/) || [wps-office](https://aur.archlinux.org/packages/wps-office/)

### Word processors

See also [Wikipedia:Comparison of word processors](https://en.wikipedia.org/wiki/Comparison_of_word_processors "wikipedia:Comparison of word processors").

*   **[Abiword](/index.php/Abiword "Abiword")** — Full-featured word processor.

	[http://www.abisource.com/](http://www.abisource.com/) || [abiword](https://www.archlinux.org/packages/?name=abiword)

*   **[BlueGriffon](https://en.wikipedia.org/wiki/BlueGriffon "wikipedia:BlueGriffon")** — WYSIWYG content editor for the World Wide Web.

	[http://www.bluegriffon.com/](http://www.bluegriffon.com/) || [bluegriffon](https://www.archlinux.org/packages/?name=bluegriffon)

*   **[Calligra Words](https://en.wikipedia.org/wiki/Calligra_Words "wikipedia:Calligra Words")** — Powerful word processor included in the Calligra Suite.

	[http://www.calligra.org/words/](http://www.calligra.org/words/) || [calligra-words](https://www.archlinux.org/packages/?name=calligra-words)

*   **gLabels** — program for creating labels and business cards.

	[http://glabels.org/](http://glabels.org/) || [glabels](https://www.archlinux.org/packages/?name=glabels)

*   **[KompoZer](https://en.wikipedia.org/wiki/KompoZer "wikipedia:KompoZer")** — A Dreamweaver style WYSIWYG web editor; Nvu unofficial bug-fix release.

	[http://kompozer.net/](http://kompozer.net/) || [kompozer](https://www.archlinux.org/packages/?name=kompozer)

*   **[LibreOffice Writer](/index.php/LibreOffice "LibreOffice")** — Full-featured word processor included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/writer](https://www.libreoffice.org/discover/writer) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still)

*   **[OpenOffice Writer](/index.php/OpenOffice "OpenOffice")** — Full-featured word processor included in the OpenOffice suite.

	[http://www.openoffice.org/](http://www.openoffice.org/) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **Pathetic Writer** — X-based rich text processor included in Siag Office.

	[http://siag.nu/pw/](http://siag.nu/pw/) || [siag-office](https://aur.archlinux.org/packages/siag-office/)

*   **[Scribus](https://en.wikipedia.org/wiki/Scribus "wikipedia:Scribus")** — Desktop publishing program.

	[http://www.scribus.net/canvas/Scribus](http://www.scribus.net/canvas/Scribus) || [scribus](https://www.archlinux.org/packages/?name=scribus)

*   **[SeaMonkey Composer](https://en.wikipedia.org/wiki/SeaMonkey#Composer "wikipedia:SeaMonkey")** — Powerful yet simple HTML editor included in the SeaMonkey suite.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

*   **[Ted](https://en.wikipedia.org/wiki/Ted_(word_processor) "wikipedia:Ted (word processor)")** — Easy to use GTK+-based rich text processor (with footnote support).

	[http://www.nllgg.nl/Ted/](http://www.nllgg.nl/Ted/) || [ted](https://aur.archlinux.org/packages/ted/)

### Document markup languages

See also [Wikipedia:Comparison of document markup languages](https://en.wikipedia.org/wiki/Comparison_of_document_markup_languages "wikipedia:Comparison of document markup languages").

*   **[asciidoc](https://en.wikipedia.org/wiki/AsciiDoc "wikipedia:AsciiDoc")** — Human-readable text document format. Used by Arch for generating *pacman* 's man pages[[2]](https://www.archlinux.org/pacman/pacman.8.html).

	[http://asciidoc.org/](http://asciidoc.org/) || [asciidoc](https://www.archlinux.org/packages/?name=asciidoc)

*   **Asciidoctor** — An asciidoc implementation written in Ruby, with many extra features.

	[http://asciidoctor.org/](http://asciidoctor.org/) || [asciidoctor](https://aur.archlinux.org/packages/asciidoctor/)

*   **[Markdown](https://en.wikipedia.org/wiki/Markdown "wikipedia:Markdown")** — Text-to-HTML conversion tool that allows you to write using a simple plain text format.

	[http://daringfireball.net/projects/markdown](http://daringfireball.net/projects/markdown) || [markdown](https://www.archlinux.org/packages/?name=markdown)

*   **[Pandoc](https://en.wikipedia.org/wiki/Pandoc "wikipedia:Pandoc")** — Swiss-army knife for converting one markup format into another.

	[http://johnmacfarlane.net/pandoc](http://johnmacfarlane.net/pandoc) || [pandoc](https://www.archlinux.org/packages/?name=pandoc)

*   **[Sphinx](https://en.wikipedia.org/wiki/Sphinx_(documentation_generator) "wikipedia:Sphinx (documentation generator)")** — A documentation generation system using [reStructuredText](https://en.wikipedia.org/wiki/ReStructuredText "wikipedia:ReStructuredText") to generate output in multiple formats (primary documentation system for the Python project).

	[http://sphinx-doc.org](http://sphinx-doc.org) || [python-sphinx](https://www.archlinux.org/packages/?name=python-sphinx)

*   **[txt2tags](https://en.wikipedia.org/wiki/Txt2tags "wikipedia:Txt2tags")** — Dead-simple, KISS-compliant lightweight, human-readable markup language to produce rich format content out of plain text files.

	[http://txt2tags.sourceforge.net](http://txt2tags.sourceforge.net) || [txt2tags](https://www.archlinux.org/packages/?name=txt2tags)

### Spreadsheets

See also [Wikipedia:Comparison of spreadsheet software](https://en.wikipedia.org/wiki/Comparison_of_spreadsheet_software "wikipedia:Comparison of spreadsheet software").

*   **[Calligra Sheets](https://en.wikipedia.org/wiki/Calligra_Sheets "wikipedia:Calligra Sheets")** — Powerful spreadsheet application included in the Calligra Suite

	[http://www.calligra.org/sheets/](http://www.calligra.org/sheets/) || [calligra-sheets](https://www.archlinux.org/packages/?name=calligra-sheets)

*   **[Gnumeric](/index.php/Gnumeric "Gnumeric")** — Spreadsheet program that is part of the GNOME desktop.

	[http://www.gnumeric.org/](http://www.gnumeric.org/) || [gnumeric](https://www.archlinux.org/packages/?name=gnumeric)

*   **[LibreOffice Calc](/index.php/LibreOffice "LibreOffice")** — Full-featured spreadsheet application included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/calc/](https://www.libreoffice.org/discover/calc/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still)

*   **[OpenOffice Calc](/index.php/OpenOffice "OpenOffice")** — Full-featured spreadsheet application included in the OpenOffice suite.

	[http://openoffice.org/product/calc.html](http://openoffice.org/product/calc.html) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **Pyspread** — Pyspread is a non-traditional spreadsheet application that is based on and written in the programming language Python.

	[http://manns.github.io/pyspread/index.html](http://manns.github.io/pyspread/index.html) || [pyspread](https://aur.archlinux.org/packages/pyspread/)

*   **[sc](/index.php?title=Sc&action=edit&redlink=1 "Sc (page does not exist)")** — curses-based lightweight spreadsheet.

	[http://ibiblio.org/pub/linux/apps/financial/spreadsheet/!INDEX.html](http://ibiblio.org/pub/linux/apps/financial/spreadsheet/!INDEX.html) || [sc](https://www.archlinux.org/packages/?name=sc)

*   **Siag** — Spreadsheet application based on the X Window System and the Scheme programming language included in Siag Office.

	[http://siag.nu/siag/](http://siag.nu/siag/) || [siag-office](https://aur.archlinux.org/packages/siag-office/)

### Scientific documents

With [TeX, LaTeX and friends](/index.php/TeX_Live "TeX Live"), creation of any scientific document, article, journal, etc. is made commonplace.

See also [Wikipedia:Comparison of TeX editors](https://en.wikipedia.org/wiki/Comparison_of_TeX_editors "wikipedia:Comparison of TeX editors") and [the LaTeX Wikibook](https://en.wikibooks.org/wiki/LaTeX/Installation#Editors).

*   **[AUCTeX](https://en.wikipedia.org/wiki/AUCTEX "wikipedia:AUCTEX")** — Together with RefTex, AUCTeX provices an extensible environment for writing and formatting TeX files in Emacs.

	[https://www.gnu.org/software/auctex/](https://www.gnu.org/software/auctex/) || [auctex](https://www.archlinux.org/packages/?name=auctex)

*   **EqualX** — LaTeX equation editor with real time preview.

	[http://equalx.sourceforge.net/index.html](http://equalx.sourceforge.net/index.html) || [equalx](https://aur.archlinux.org/packages/equalx/)

*   **gedit-latex** — Add code-completion to gedit and allows for compiling LaTeX documents and managing BibTeX bibliographies.

	[http://www.gnome.org/](http://www.gnome.org/) || [gedit-latex](https://aur.archlinux.org/packages/gedit-latex/)

*   **[Gummi](https://en.wikipedia.org/wiki/Gummi_(software) "wikipedia:Gummi (software)")** — Lightweight TeX/LaTeX GTK+-based editor. It features a continuous preview mode, integrated BibTeX support, extendable snippet interface and multi-document support.

	[https://github.com/alexandervdm/gummi/](https://github.com/alexandervdm/gummi/) || [gummi](https://www.archlinux.org/packages/?name=gummi)

*   **JabRef** — Java GUI frontend for managing BibTeX and other bibliographies.

	[http://jabref.sourceforge.net/index.php](http://jabref.sourceforge.net/index.php) || [jabref](https://aur.archlinux.org/packages/jabref/) [jabref-git](https://aur.archlinux.org/packages/jabref-git/)

*   **[Kile](https://en.wikipedia.org/wiki/Kile "wikipedia:Kile")** — User-friendly TeX/LaTeX editor for the KDE desktop with many features.

	[http://kile.sourceforge.net/](http://kile.sourceforge.net/) || [kile](https://www.archlinux.org/packages/?name=kile)

*   **Ktikz** — GUI making diagrams with [PGF/TikZ](http://pgf.sourceforge.net/) easier.

	[http://www.hackenberger.at/blog/ktikz-editor-for-the-tikz-language/](http://www.hackenberger.at/blog/ktikz-editor-for-the-tikz-language/) || [ktikz](https://aur.archlinux.org/packages/ktikz/)

*   **LaTeXila** — LaTeX editor for the GNOME Desktop including support for code completion, compiling and project management.

	[https://wiki.gnome.org/Apps/LaTeXila](https://wiki.gnome.org/Apps/LaTeXila) || [latexila](https://aur.archlinux.org/packages/latexila/)

*   **[LyX](https://en.wikipedia.org/wiki/LyX "wikipedia:LyX")** — Document processor that encourages an approach to writing based on the structure of your documents (WYSIWYM) and not simply their appearance (WYSIWYG).

	[http://www.lyx.org/](http://www.lyx.org/) || [lyx](https://www.archlinux.org/packages/?name=lyx)

*   **[TeXmacs](https://en.wikipedia.org/wiki/GNU_TeXmacs "wikipedia:GNU TeXmacs")** — WYSIWYW (what you see is what you want) editing platform with special features for scientists.

	[http://www.texmacs.org/](http://www.texmacs.org/) || [texmacs](https://www.archlinux.org/packages/?name=texmacs)

*   **[Texmaker](https://en.wikipedia.org/wiki/Texmaker "wikipedia:Texmaker")** — Cross-platform, light and easy-to-use LaTeX IDE. It integrates many tools needed to develop documents with LaTeX, in just one application

	[http://www.xm1math.net/texmaker/](http://www.xm1math.net/texmaker/) || [texmaker](https://www.archlinux.org/packages/?name=texmaker)

*   **TeXstudio** — Fork of TeXMaker including support for code completion of bibtex items, grammar check and automatic detection of the need for multiple LaTeX runs.

	[http://texstudio.sourceforge.net/](http://texstudio.sourceforge.net/) || [texstudio](https://www.archlinux.org/packages/?name=texstudio)

*   **[Vim-LaTeX-suite](/index.php/Vim "Vim")** — Customizable LaTeX environment for Vim.

	[http://vim-latex.sourceforge.net/](http://vim-latex.sourceforge.net/) || [vim-latexsuite](https://www.archlinux.org/packages/?name=vim-latexsuite)

*   **[Vimtex](/index.php/Vim "Vim")** — This vim plugin is a fork of [LaTeX-Box](https://github.com/LaTeX-Box-Team/LaTeX-Box). It provides automatic syntax-based folding, omni-completion (for citations and labels), latexmk-based compilation and synctex functionality for [zathura](https://www.archlinux.org/packages/?name=zathura) and [mupdf](https://www.archlinux.org/packages/?name=mupdf).

	[https://github.com/lervag/vimtex/](https://github.com/lervag/vimtex/) ||

*   **WhizzyTeX** — WhizzyTeX provides a nice live preview editor for Emacs.

	[http://www.emacswiki.org/emacs/WhizzyTeX/](http://www.emacswiki.org/emacs/WhizzyTeX/) || [whizzytex](https://aur.archlinux.org/packages/whizzytex/)

*   **Zotero** — This is a free, easy-to-use tool to help you collect, organize, cite, and share your research sources. There is a stand-alone version and a Firefox add-on available.

	[https://www.zotero.org/](https://www.zotero.org/) || [zotero](https://aur.archlinux.org/packages/zotero/)

### Translation and localization

*   **[Apertium](https://en.wikipedia.org/wiki/Apertium "wikipedia:Apertium")** — Free and open source rule-based machine translation platform with available language data. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, TMX, MediaWiki and others.

	[http://apertium.org/](http://apertium.org/) || [apertium](https://aur.archlinux.org/packages/apertium/)

*   **[Gtranslator](https://en.wikipedia.org/wiki/Gtranslator "wikipedia:Gtranslator")** — Enhanced gettext po file editor for the GNOME. It handles all forms of gettext po files and includes very useful features.

	[https://wiki.gnome.org/Apps/Gtranslator](https://wiki.gnome.org/Apps/Gtranslator) || [gtranslator](https://www.archlinux.org/packages/?name=gtranslator)

*   **[Lokalize](https://en.wikipedia.org/wiki/Lokalize "wikipedia:Lokalize")** — Standard [KDE](/index.php/KDE "KDE") tool for software translation. It includes basic editing of PO files, support for glossary, translation memory, project managing, etc. It belongs to [kdesdk](https://www.archlinux.org/groups/x86_64/kdesdk/)

	[http://userbase.kde.org/Lokalize](http://userbase.kde.org/Lokalize) || [lokalize](https://www.archlinux.org/packages/?name=lokalize)

*   **[Moses](https://en.wikipedia.org/wiki/Moses_(machine_translation) "wikipedia:Moses (machine translation)")** — Statistical machine translation tool (language data not included).

	[http://statmt.org/moses](http://statmt.org/moses) || [mosesdecoder](https://aur.archlinux.org/packages/mosesdecoder/) [mosesdecoder-git](https://aur.archlinux.org/packages/mosesdecoder-git/)

*   **[OmegaT](https://en.wikipedia.org/wiki/OmegaT "wikipedia:OmegaT")** — General translator's tool which contains a lot of translation memory features and can give suggestions from Google Translate. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, XLIFF/Okapi, MediaWiki, plain text, TMX and others.

	[http://omegat.org](http://omegat.org) || [omegat](https://aur.archlinux.org/packages/omegat/)

*   **[Poedit](https://en.wikipedia.org/wiki/Poedit "wikipedia:Poedit")** — Simple gettext/po-based translation tool.

	[http://poedit.net](http://poedit.net) || [poedit](https://www.archlinux.org/packages/?name=poedit)

*   **Pology** — Set of Python tools for dealing with gettext/po-files.

	[http://techbase.kde.org/Localization/Tools/Pology](http://techbase.kde.org/Localization/Tools/Pology) || [pology](https://aur.archlinux.org/packages/pology/)

*   **[Virtaal](https://en.wikipedia.org/wiki/Virtaal and others.

	[http://translate.sourceforge.net/wiki/virtaal](http://translate.sourceforge.net/wiki/virtaal) || [virtaal](https://aur.archlinux.org/packages/virtaal/)

### Text editors

See also [Wikipedia:Comparison of text editors](https://en.wikipedia.org/wiki/Comparison_of_text_editors "wikipedia:Comparison of text editors").

Some of the lighter-weight [Integrated development environments](/index.php/List_of_applications/Utilities#Integrated_development_environments "List of applications/Utilities") can also serve as text editors.

#### Console

*   **e3** — Tiny editor without dependencies, written in assembly.

	[http://sites.google.com/site/e3editor/](http://sites.google.com/site/e3editor/) || [e3](https://www.archlinux.org/packages/?name=e3)

*   **ee** — A classic curse-based text editor. Born in HP-UX, used in FreeBSD.

	[http://www.users.qwest.net/~hmahon/](http://www.users.qwest.net/~hmahon/) || [ee-editor](https://aur.archlinux.org/packages/ee-editor/)

*   **dex** — Small and easy to use text editor with support for ctags and parsing compiler errors.

	[https://github.com/tihirvon/dex](https://github.com/tihirvon/dex) || [dex-editor-git](https://aur.archlinux.org/packages/dex-editor-git/)

*   **[Emacs-nox](/index.php/Emacs "Emacs")** — The extensible, customizable, self-documenting real-time display editor, without X11 support.

	[http://www.gnu.org/software/emacs/emacs.html](http://www.gnu.org/software/emacs/emacs.html) || [emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox)

*   **[JED](https://en.wikipedia.org/wiki/JED_(text_editor) "wikipedia:JED (text editor)")** — Text editor that makes extensive use of the [S-Lang library](https://en.wikipedia.org/wiki/S-Lang_(programming_library) "wikipedia:S-Lang (programming library)"). Includes a console version (jed) and an X-window version (xjed).

	[http://jedsoft.org/jed/](http://jedsoft.org/jed/) || [jed](https://aur.archlinux.org/packages/jed/)

*   **[Joe](/index.php/Joe "Joe") (Joe's Own Editor)** — Terminal-based text editor designed to be easy to use.

	[http://joe-editor.sourceforge.net/](http://joe-editor.sourceforge.net/) || [joe](https://www.archlinux.org/packages/?name=joe)

*   **[mcedit](https://en.wikipedia.org/wiki/Midnight_Commander "wikipedia:Midnight Commander")** — Useful text editor that comes with Midnight Commander file manager.

	[http://www.ibiblio.org/mc/](http://www.ibiblio.org/mc/) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **[MicroEmacs](https://en.wikipedia.org/wiki/MicroEMACS "wikipedia:MicroEMACS")** — Ncurses-based text editor. Includes a console version (me -n) and an X-window version (me).

	[http://www.jasspa.com/](http://www.jasspa.com/) || [jasspa-me](https://aur.archlinux.org/packages/jasspa-me/)

*   **[mg](https://en.wikipedia.org/wiki/mg_(editor) "wikipedia:mg (editor)")** — Small, fast, and portable Emacs-like editor.

	[http://homepage.boetes.org/software/mg](http://homepage.boetes.org/software/mg) || [mg](https://www.archlinux.org/packages/?name=mg)

*   **mp** — Minimum Profit is a text editor for programmers. It helps you definitively abandon vi, emacs and other six-legged freaks.

	[http://triptico.com/software/mp.html](http://triptico.com/software/mp.html) || [mp](https://aur.archlinux.org/packages/mp/)

*   **[nano](/index.php/Nano "Nano")** — Console text editor based on pico with on-screen key bindings help.

	[http://nano-editor.org/](http://nano-editor.org/) || [nano](https://www.archlinux.org/packages/?name=nano)

*   **Ne** — Minimalist text editor with Windows-like key-bindings.

	[http://ne.di.unimi.it/](http://ne.di.unimi.it/) || [ne](https://aur.archlinux.org/packages/ne/)

*   **Slap** — Sublime-like terminal-based text editor.

	[https://github.com/slap-editor/slap](https://github.com/slap-editor/slap) || [slap](https://aur.archlinux.org/packages/slap/)

*   **[vile](https://en.wikipedia.org/wiki/Vile_(editor) "wikipedia:Vile (editor)")** — A lightweight Emacs clone with *vi*-like key bindings.

	[http://invisible-island.net/vile/vile.html](http://invisible-island.net/vile/vile.html) || [vile](https://www.archlinux.org/packages/?name=vile)

*   **[Zile](https://en.wikipedia.org/wiki/Zile_(editor) "wikipedia:Zile (editor)")** — A lightweight Emacs clone.

	[https://gnu.org/s/zile/](https://gnu.org/s/zile/) || [zile](https://www.archlinux.org/packages/?name=zile)

##### Vi text editors

*   **[Neovim](/index.php/Neovim "Neovim")** — Vim's rebirth for the 21st century

	[http://neovim.io/](http://neovim.io/) || [neovim](https://www.archlinux.org/packages/?name=neovim)

*   **[Vi](/index.php/Vi "Vi")** — The original ex/vi text editor.

	[http://ex-vi.sourceforge.net/](http://ex-vi.sourceforge.net/) || [vi](https://www.archlinux.org/packages/?name=vi)

*   **[Vim](/index.php/Vim "Vim") (Vi IMproved)** — Advanced text editor that seeks to provide the power of the de-facto Unix editor 'vi', with a more complete feature set.

	[http://www.vim.org/](http://www.vim.org/) || [vim](https://www.archlinux.org/packages/?name=vim)

#### Graphical

*   **[Acme](https://en.wikipedia.org/wiki/Acme_(text_editor) "wikipedia:Acme (text editor)")** — Minimalist and flexible programming environment developed by Rob Pike for the Plan 9 operating system.

	[http://acme.cat-v.org](http://acme.cat-v.org) || [plan9port](https://www.archlinux.org/packages/?name=plan9port)

*   **[Atom](/index.php/Atom "Atom")** — A promising text editor developed by GitHub. With support for plug-ins written in Node.js and embedded [Git](/index.php/Git "Git") Control.

	[https://atom.io](https://atom.io) || [atom](https://www.archlinux.org/packages/?name=atom)

*   **Beaver** — A GTK+ editor designed to be modular, lightweight and stylish.

	[http://beaver-editor.sourceforge.net](http://beaver-editor.sourceforge.net) || [beaver](https://www.archlinux.org/packages/?name=beaver)

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "w:Brackets (text editor)")** — An open source code editor for the web, written in JavaScript, HTML and CSS.

	[http://brackets.io](http://brackets.io) || [brackets](https://aur.archlinux.org/packages/brackets/)

*   **[Cream](https://en.wikipedia.org/wiki/Cream_(software) "wikipedia:Cream (software)")** — A user-friendly editor atop of gVim.

	[http://cream.sourceforge.net](http://cream.sourceforge.net) || [cream](https://aur.archlinux.org/packages/cream/)

*   **Edile** — PyGTK code and scripting editor implemented in one file.

	[https://code.google.com/archive/p/edile/](https://code.google.com/archive/p/edile/) || [edile](https://aur.archlinux.org/packages/edile/)

*   **ePad** — A simple text editor written in Python and EFL.

	[https://github.com/JeffHoogland/ePad](https://github.com/JeffHoogland/ePad) || [epad](https://aur.archlinux.org/packages/epad/)

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — A text editor using the GTK2 toolkit with basic features of an integrated development environment. It has support for TeX-based documents.

	[https://www.geany.org](https://www.geany.org) || [geany](https://www.archlinux.org/packages/?name=geany)

*   **[Gedit](https://en.wikipedia.org/wiki/Gedit "wikipedia:Gedit")** — GTK+ editor for the GNOME desktop with syntax highlighting, automatic indentation, matching brackets, etc., and a number of add-ons to increase functionality.

	[https://wiki.gnome.org/Apps/Gedit](https://wiki.gnome.org/Apps/Gedit) || [gedit](https://www.archlinux.org/packages/?name=gedit)

*   **[GNU Emacs](/index.php/GNU_Emacs "GNU Emacs")** — The extensible, customizable, self-documenting real-time display editor.

	[https://gnu.org/s/emacs](https://gnu.org/s/emacs) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[gVim](/index.php/GVim "GVim")** — Graphical interface for Vim.

	[http://www.vim.org](http://www.vim.org) || [gvim](https://www.archlinux.org/packages/?name=gvim)

*   **Jedit** — Text editor for programmers, written in Java.

	[http://www.jedit.org](http://www.jedit.org) || [jedit](https://www.archlinux.org/packages/?name=jedit)

*   **[JuffEd](https://en.wikipedia.org/wiki/JuffEd "wikipedia:JuffEd")** — Simple tabbed text editor with syntax highlighting, written in Qt.

	[http://juffed.com/en/index.html](http://juffed.com/en/index.html) || [juffed](https://aur.archlinux.org/packages/juffed/)

*   **[Kate](https://en.wikipedia.org/wiki/Kate_(text_editor) "wikipedia:Kate (text editor)")** — Full-featured programmer's editor for the KDE desktop with MDI and a filesystem browser.

	[https://kate-editor.org](https://kate-editor.org) || [kate](https://www.archlinux.org/packages/?name=kate)

*   **[KWrite](https://en.wikipedia.org/wiki/KWrite "wikipedia:KWrite")** — Lightweight text editor for the KDE desktop that uses the same editor widget as Kate.

	[https://kde.org/applications/utilities/kwrite](https://kde.org/applications/utilities/kwrite) || [kwrite](https://www.archlinux.org/packages/?name=kwrite)

*   **[Leafpad](https://en.wikipedia.org/wiki/Leafpad "wikipedia:Leafpad")** — Notepad clone for GTK+ that emphasizes simplicity.

	[http://tarot.freeshell.org/leafpad](http://tarot.freeshell.org/leafpad) || [leafpad](https://www.archlinux.org/packages/?name=leafpad)

*   **L3afpad** — Simple text editor forked from Leafpad, supports GTK+ 3.

	[https://github.com/stevenhoneyman/l3afpad](https://github.com/stevenhoneyman/l3afpad) || [l3afpad](https://www.archlinux.org/packages/?name=l3afpad)

*   **Medit** — Programming and around-programming text editor.

	[http://mooedit.sourceforge.net](http://mooedit.sourceforge.net) || [medit](https://www.archlinux.org/packages/?name=medit)

*   **[Mousepad](https://en.wikipedia.org/wiki/Xfce#Mousepad "wikipedia:Xfce")** — Fast text editor for the Xfce Desktop Environment.

	[https://www.xfce.org](https://www.xfce.org) || [mousepad](https://www.archlinux.org/packages/?name=mousepad)

*   **[Nedit](https://en.wikipedia.org/wiki/NEdit "wikipedia:NEdit")** — Text editor for the [lesstif](https://www.archlinux.org/packages/?name=lesstif) environment.

	[http://www.nedit.org](http://www.nedit.org) || [nedit](https://www.archlinux.org/packages/?name=nedit)

*   **[Pluma](/index.php/MATE "MATE")** — A powerful text editor for MATE.

	[http://mate-desktop.org](http://mate-desktop.org) || [pluma](https://www.archlinux.org/packages/?name=pluma)

*   **[PyRoom](https://en.wikipedia.org/wiki/PyRoom "wikipedia:PyRoom")** — Great distractionless PyGTK text editor, a clone of the infamous WriteRoom.

	[http://pyroom.org](http://pyroom.org) || [pyroom](https://aur.archlinux.org/packages/pyroom/)

*   **QEdit** — A multi-purpose text editor based on NEdit using Qt.

	[http://hugo.pereira.free.fr/software/index.php?page=package&package_list=software_list_qt4&package=qedit](http://hugo.pereira.free.fr/software/index.php?page=package&package_list=software_list_qt4&package=qedit) || [qedit](https://aur.archlinux.org/packages/qedit/)

*   **QSciTE** — Qt clone of the SciTE text and code editor.

	[https://code.google.com/archive/p/qscite/](https://code.google.com/archive/p/qscite/) || [qscite](https://aur.archlinux.org/packages/qscite/)

*   **QXmlEdit** — Simple Qt XML editor and XSD viewer.

	[http://qxmledit.org](http://qxmledit.org) || [qxmledit](https://aur.archlinux.org/packages/qxmledit/)

*   **[Sam](https://en.wikipedia.org/wiki/Sam_(text_editor) "wikipedia:Sam (text editor)")** — Minimalist text editor with a graphical user interface, a very powerful command language and remote editing capabilities, developed by Rob Pike.

	[http://sam.cat-v.org](http://sam.cat-v.org) || [plan9port](https://www.archlinux.org/packages/?name=plan9port) or [9base](https://www.archlinux.org/packages/?name=9base)

*   **[SciTE](https://en.wikipedia.org/wiki/SciTE "wikipedia:SciTE")** — Generally useful editor with facilities for building and running programs.

	[http://scintilla.org/SciTE.html](http://scintilla.org/SciTE.html) || [scite](https://www.archlinux.org/packages/?name=scite)

*   **Scribes** — An ultra minimalist text editor that combines simplicity with power.

	[http://scribes.sourceforge.net](http://scribes.sourceforge.net) || [scribes](https://www.archlinux.org/packages/?name=scribes)

*   **[Sublime Text 2](https://en.wikipedia.org/wiki/Sublime_Text "wikipedia:Sublime Text")** — Closed-source C++ and Python-based editor with many advanced features and plugins while staying lightweight and pretty.

	[https://www.sublimetext.com](https://www.sublimetext.com) || [sublime-text](https://aur.archlinux.org/packages/sublime-text/)

*   **[Sublime Text 3](https://en.wikipedia.org/wiki/Sublime_Text "wikipedia:Sublime Text")** — Closed-source C++ and Python-based editor with many advanced features and plugins while staying lightweight and pretty.

	[https://www.sublimetext.com](https://www.sublimetext.com) || [sublime-text-dev](https://aur.archlinux.org/packages/sublime-text-dev/)

*   **Tea** — Qt-based feature rich text editor.

	[http://semiletov.org/tea](http://semiletov.org/tea) || [tea](https://www.archlinux.org/packages/?name=tea)

*   **[Textadept](/index.php/Textadept "Textadept")** — Lua-extensible feature rich text editor based on Scintilla and written in C.

	[http://foicica.com/textadept](http://foicica.com/textadept) || [textadept](https://aur.archlinux.org/packages/textadept/)

*   **[Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code")** — Editor for building and debugging modern web and cloud applications.

	[https://code.visualstudio.com](https://code.visualstudio.com) || [visual-studio-code](https://aur.archlinux.org/packages/visual-studio-code/)/[visual-studio-code-oss](https://aur.archlinux.org/packages/visual-studio-code-oss/) (open-source version)

*   **XEdit** — Simple text editor for the X Window System.

	[https://www.x.org/wiki](https://www.x.org/wiki) || [xorg-xedit](https://www.archlinux.org/packages/?name=xorg-xedit)

##### Collaborative text editors

*   **Gobby** — Collaborative editor supporting multiple documents in one session and a multi-user chat.

	[https://gobby.github.io](https://gobby.github.io) || [gobby](https://www.archlinux.org/packages/?name=gobby)

### Readers and Viewers

#### E-book applications

**Note:** Some [PDF and DjVu viewers](#PDF_and_DjVu) also support other e-book formats.

*   **[Calibre](https://en.wikipedia.org/wiki/Calibre_(software) "wikipedia:Calibre (software)")** — E-book library management application that can also convert between different formats and sync with a variety of e-book readers. Supported formats include CBZ, CBR, CBC, CHM, DJVU, EPUB, FictionBook, HTML, HTMLZ, LIT, LRF, Mobipocket, ODT, PDF, PRC, PDB, PML, RB, RTF, SNB, TCR, TXT and TXTZ.

	[http://calibre-ebook.com/](http://calibre-ebook.com/) || [calibre](https://www.archlinux.org/packages/?name=calibre)

*   **Cool Reader** — E-book viewer with many supported formats such as EPUB (non-DRM), FictionBook, TXT, RTF, HTML, CHM and TCR.

	[http://crengine.sourceforge.net/](http://crengine.sourceforge.net/) || [coolreader3-git](https://aur.archlinux.org/packages/coolreader3-git/)

*   **epub** — A console EPUB reader using Python and Curses.

	[https://pypi.python.org/pypi/epub](https://pypi.python.org/pypi/epub) || [python-epub](https://aur.archlinux.org/packages/python-epub/)

*   **[FBReader](https://en.wikipedia.org/wiki/FBReader "wikipedia:FBReader")** — E-book viewer with many supported formats such as EPUB, FictionBook, HTML, plucker, PalmDoc, zTxt, TCR, CHM, RTF, OEB, Mobipocket (non-DRM) and TXT.

	[http://fbreader.org/](http://fbreader.org/) || [fbreader](https://www.archlinux.org/packages/?name=fbreader)

*   **pPub** — Simple EPUB reader using Python, GTK3 and WebKit.

	[https://github.com/sakisds/pPub](https://github.com/sakisds/pPub) || [ppub](https://aur.archlinux.org/packages/ppub/)

*   **[Sigil](https://en.wikipedia.org/wiki/Sigil_(application) "wikipedia:Sigil (application)")** — WYSIWYG ebook editor.

	[http://sigil-ebook.com/](http://sigil-ebook.com/) || [sigil](https://www.archlinux.org/packages/?name=sigil)

##### Book organizers

for more collection apps, see also [Multimedia#Collection managers](/index.php/Multimedia#Collection_managers "Multimedia")

*   **Alexandria** — GNOME application to help manage your book collection.

	[http://alexandria.rubyforge.org/](http://alexandria.rubyforge.org/) || [alexandria](https://aur.archlinux.org/packages/alexandria/)

*   **[Koha](https://en.wikipedia.org/wiki/Koha_(software) "wikipedia:Koha (software)")** — Open source Integrated Library System (ILS), used world-wide by public, school and special libraries.

	[http://koha-community.org/](http://koha-community.org/) || [koha](https://aur.archlinux.org/packages/koha/)

#### PDF and DjVu

**Note:** [PDF forms](https://en.wikipedia.org/wiki/Portable_Document_Format#Interactive_elements "wikipedia:Portable Document Format") support:

*   [acroread](https://aur.archlinux.org/packages/acroread/) is able to save both AcroForms and XFA forms into PDF files.
*   Poppler-based readers such as [evince](https://www.archlinux.org/packages/?name=evince) and [kdegraphics-okular](https://www.archlinux.org/packages/?name=kdegraphics-okular) support AcroForms, but not full XFA forms. [[3]](https://bugs.freedesktop.org/show_bug.cgi?id=18935) [[4]](https://bugs.launchpad.net/ubuntu/+source/poppler/+bug/321720)
*   For CJK(Chinese, Japanese, Korean) support in poppler-based readers such as [evince](https://www.archlinux.org/packages/?name=evince) and [kdegraphics-okular](https://www.archlinux.org/packages/?name=kdegraphics-okular), install [poppler-data](https://www.archlinux.org/packages/?name=poppler-data). poppler-data is an optional dependency of poppler which is an indirect dependency of evince and okular.

See also [Wikipedia:List of PDF software](https://en.wikipedia.org/wiki/List_of_PDF_software "wikipedia:List of PDF software") and [Wikipedia:DjVu](https://en.wikipedia.org/wiki/DjVu "wikipedia:DjVu").

##### Console

*   **fbpdf** — Small framebuffer PDF and DjVu viewer based off of MuPDF, with [Vim](/index.php/Vim "Vim") keybindings and written in C

	[http://repo.or.cz/w/fbpdf.git](http://repo.or.cz/w/fbpdf.git) || [fbpdf-git](https://aur.archlinux.org/packages/fbpdf-git/)

*   **jfbview** — Framebuffer PDF and image viewer. Features include Vim-like controls, zoom-to-fit, a TOC (outline) view, fast multi-threaded rendering and asynchronous pre-caching. Originally a fork of *fbpdf* called *jfbpdf*, now completely rewritten.

	[http://seasonofcode.com/pages/jfbview.html](http://seasonofcode.com/pages/jfbview.html) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

##### Graphical

**Note:** Some [web browsers](/index.php/List_of_applications/Internet#Web_browsers "List of applications/Internet") have support for displaying PDF files, either built-in or via plugin.

*   **acroread** — A PDF file viewer offered by Adobe (closed source).

	[http://www.adobe.com/products/reader.html](http://www.adobe.com/products/reader.html) || [acroread](https://aur.archlinux.org/packages/acroread/)

*   **apvlv** — Lightweight PDF/DjVu/UMD/TXT viewer with [Vim](/index.php/Vim "Vim") keybindings.

	[http://naihe2010.github.com/apvlv/](http://naihe2010.github.com/apvlv/) || [apvlv](https://www.archlinux.org/packages/?name=apvlv)

*   **Atril** — Simple multi-page document viewer for MATE.

	[https://github.com/mate-desktop/atril](https://github.com/mate-desktop/atril) || [atril](https://www.archlinux.org/packages/?name=atril)

*   **ePDFView** — Free lightweight PDF document viewer using the Poppler and GTK+ libraries. Development stopped.

	[http://freecode.com/projects/epdfview](http://freecode.com/projects/epdfview) || [epdfview](https://www.archlinux.org/packages/?name=epdfview)

*   **[Evince](https://en.wikipedia.org/wiki/Evince "wikipedia:Evince")** — Document viewer for multiple document formats. Supports PDF, PostScript, DjVu, TIFF and DVI.

	[https://wiki.gnome.org/Apps/Evince](https://wiki.gnome.org/Apps/Evince) || [evince](https://www.archlinux.org/packages/?name=evince)

*   **[Foxit Reader](https://en.wikipedia.org/wiki/Foxit_Reader "wikipedia:Foxit Reader")** — Small, fast (compared to Acrobat) PDF viewer. (closed source)

	[http://www.foxitsoftware.com/pdf/desklinux/](http://www.foxitsoftware.com/pdf/desklinux/) || [foxitreader](https://aur.archlinux.org/packages/foxitreader/)

*   **gv** — Graphical user interface for the Ghostscript interpreter that allows to view and navigate through PostScript and PDF documents.

	[http://www.gnu.org/software/gv/](http://www.gnu.org/software/gv/) || [gv](https://www.archlinux.org/packages/?name=gv)

*   **[llpp](/index.php/Llpp "Llpp")** — Very fast PDF reader based off of MuPDF, that supports continuous page scrolling, bookmarking, and text search through the whole document.

	[http://repo.or.cz/w/llpp.git](http://repo.or.cz/w/llpp.git) || [llpp](https://aur.archlinux.org/packages/llpp/)

*   **[MuPDF](/index.php/MuPDF "MuPDF")** — Very fast PDF and XPS viewer and toolkit written in portable C. Features CJK font support.

	[http://mupdf.com](http://mupdf.com) || [mupdf](https://www.archlinux.org/packages/?name=mupdf)

*   **[Okular](https://en.wikipedia.org/wiki/Okular "wikipedia:Okular")** — Universal PDF viewer for KDE.

	[http://okular.kde.org/](http://okular.kde.org/) || [kdegraphics-okular](https://www.archlinux.org/packages/?name=kdegraphics-okular)

*   **PdfMod** — You can reorder, rotate, and remove pages, export images from a document, edit the title, subject, author, and keywords, and combine documents via drag and drop.

	[https://wiki.gnome.org/Apps/PdfMod](https://wiki.gnome.org/Apps/PdfMod) || [pdfmod](https://www.archlinux.org/packages/?name=pdfmod)

*   **PDF Shuffler** — Combine, split, roatate and reorder PDF documents. Uses Python and GTK3.

	[https://sourceforge.net/projects/pdfshuffler/](https://sourceforge.net/projects/pdfshuffler/) || [pdfshuffler-git](https://aur.archlinux.org/packages/pdfshuffler-git/)

*   **PDF Studio** — All-in-one PDF editor similar to Adobe Acrobat (proprietary).

	[http://www.qoppa.com/pdfstudio/](http://www.qoppa.com/pdfstudio/) || [pdfstudio](https://aur.archlinux.org/packages/pdfstudio/)

*   **qpdfview** — Tabbed document viewer. It uses Poppler for PDF support, libspectre for PS support, DjVuLibre for DjVu support, CUPS for printing support and the Qt toolkit for its interface.

	[https://launchpad.net/qpdfview](https://launchpad.net/qpdfview) || [qpdfview](https://aur.archlinux.org/packages/qpdfview/)

*   **[Xournal](https://en.wikipedia.org/wiki/Xournal "wikipedia:Xournal")** — Pdf viewer/note taking application.

	[http://xournal.sourceforge.net/](http://xournal.sourceforge.net/) || [xournal](https://www.archlinux.org/packages/?name=xournal)

*   **[Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf")** — Viewer that can decode LZW and read encrypted PDFs.

	[http://www.foolabs.com/xpdf/](http://www.foolabs.com/xpdf/) || [xpdf](https://www.archlinux.org/packages/?name=xpdf)

*   **[zathura](https://en.wikipedia.org/wiki/Zathura_(document_viewer) "wikipedia:Zathura (document viewer)")** — Highly customizable and functional PDF/DjVu/PostScript/ComicBook viewer (plugin based).

	[http://pwmt.org/projects/zathura/](http://pwmt.org/projects/zathura/) || [zathura](https://www.archlinux.org/packages/?name=zathura) [zathura-pdf-mupdf](https://www.archlinux.org/packages/?name=zathura-pdf-mupdf) [zathura-djvu](https://www.archlinux.org/packages/?name=zathura-djvu)

#### Terminal pagers

See also [Wikipedia:Terminal pager](https://en.wikipedia.org/wiki/Terminal_pager "wikipedia:Terminal pager").

*   [more](https://en.wikipedia.org/wiki/More_(command) — A simple and feature-light pager. It is a part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package.
*   **[less](/index.php/Core_utilities#less "Core utilities")** — A program similar to more, but with support for both forward and backward scrolling, as well as partial loading of files.

	[http://www.gnu.org/software/less](http://www.gnu.org/software/less) || [less](https://www.archlinux.org/packages/?name=less)

*   **[most](https://en.wikipedia.org/wiki/Most_(Unix) "wikipedia:Most (Unix)")** — A pager with support for multiple windows, left and right scrolling, and built-in colour support

	[http://www.jedsoft.org/most/](http://www.jedsoft.org/most/) || [most](https://www.archlinux.org/packages/?name=most)

*   **mcview** — A pager with mouse and colour support. It is bundled with midnight commander.

	[http://www.midnight-commander.org](http://www.midnight-commander.org) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **vimpager** — A script that turns vim into a pager. As a result, you get various vim features such as colour schemes, mouse support, split screens, etc.

	[https://github.com/rkitover/vimpager](https://github.com/rkitover/vimpager) || [vimpager](https://www.archlinux.org/packages/?name=vimpager)

#### CHM

See also [Wikipedia:Microsoft Compiled HTML Help](https://en.wikipedia.org/wiki/Microsoft_Compiled_HTML_Help "wikipedia:Microsoft Compiled HTML Help").

*   **ChmSee** — CHM viewer based on xulrunner.

	[https://code.google.com/archive/p/chmsee/](https://code.google.com/archive/p/chmsee/) || [chmsee](https://aur.archlinux.org/packages/chmsee/)

*   **Kchmviewer** — Qt-based CHM viewer that uses chmlib and borrows some ideas from xchm. It does not depend on [KDE](/index.php/KDE "KDE"), but it can be compiled to integrate with it.

	[http://www.ulduzsoft.com/kchmviewer/](http://www.ulduzsoft.com/kchmviewer/) || [kchmviewer](https://www.archlinux.org/packages/?name=kchmviewer)

*   **[xCHM](https://en.wikipedia.org/wiki/xCHM "wikipedia:xCHM")** — Lightweight CHM viewer, based on chmlib.

	[http://xchm.sf.net/](http://xchm.sf.net/) || [xchm](https://www.archlinux.org/packages/?name=xchm)

#### Comic book (comix/manga)

*   **[MComix](https://en.wikipedia.org/wiki/MComix "wikipedia:MComix")** — GTK2 image viewer specifically designed to handle comic book archives (fork of Comix). Also includes library manager.

	[https://sourceforge.net/projects/mcomix/](https://sourceforge.net/projects/mcomix/) || [mcomix](https://www.archlinux.org/packages/?name=mcomix)

*   **QComicBook** — Lightweight comic book viewer written in C++ and Qt4.

	[https://github.com/stolowski/QComicBook](https://github.com/stolowski/QComicBook) || [qcomicbook](https://aur.archlinux.org/packages/qcomicbook/)

*   **YACReader** — Comic book viewer written in C++ and Qt5\. Comes with YACReaderLibrary for managing comics.

	[http://yacreader.com/](http://yacreader.com/) || [yacreader](https://aur.archlinux.org/packages/yacreader/)

### Scanning software

See [SANE#Install a frontend](/index.php/SANE#Install_a_frontend "SANE").

### OCR software

See also [Wikipedia:Comparison of optical character recognition software](https://en.wikipedia.org/wiki/Comparison_of_optical_character_recognition_software "wikipedia:Comparison of optical character recognition software").

#### Engines

*   **CuneiForm** — Command line OCR system originally developed and open sourced by Cognitive technologies. Supported languages: eng, ger, fra, rus, swe, spa, ita, ruseng, ukr, srp, hrv, pol, dan, por, dut, cze, rum, hun, bul, slo, lav, lit, est, tur.

	[https://launchpad.net/cuneiform-linux](https://launchpad.net/cuneiform-linux) || [cuneiform](https://www.archlinux.org/packages/?name=cuneiform)

*   **GOCR/JOCR** — OCR engine which also supports barcode recognition.

	[http://jocr.sourceforge.net/](http://jocr.sourceforge.net/) || [gocr](https://www.archlinux.org/packages/?name=gocr)

*   **Ocrad** — OCR program based on a feature extraction method.

	[http://www.gnu.org/software/ocrad/](http://www.gnu.org/software/ocrad/) || [ocrad](https://www.archlinux.org/packages/?name=ocrad)

*   **Tesseract** — Accurate open source OCR engine. Package splitted, you need install some datafiles for each language ([tesseract-data-eng](https://www.archlinux.org/packages/?name=tesseract-data-eng) for example).

	[https://github.com/tesseract-ocr](https://github.com/tesseract-ocr) || [tesseract](https://www.archlinux.org/packages/?name=tesseract)

#### Layout analyzers and user interfaces

*   **gImageReader** — Graphical GTK frontend to Tesseract.

	[http://gimagereader.sourceforge.net/](http://gimagereader.sourceforge.net/) || [gimagereader](https://aur.archlinux.org/packages/gimagereader/)

*   **gscan2pdf** — Scans, runs an OCR engine, minor post-processing, creates a document.

	[http://gscan2pdf.sourceforge.net/](http://gscan2pdf.sourceforge.net/) || [gscan2pdf](https://aur.archlinux.org/packages/gscan2pdf/)

*   **OCRFeeder** — Python GUI for Gnome which performs document analysis and rendition, and can use either CuneiForm, GOCR, Ocrad or Tesseract as OCR engines. It can import from PDF or image files, and export to HTML or OpenDocument.

	[https://wiki.gnome.org/Apps/OCRFeeder](https://wiki.gnome.org/Apps/OCRFeeder) || [ocrfeeder](https://www.archlinux.org/packages/?name=ocrfeeder)

*   **OCRopy** — OCR *platform*, modules exist for document layout analysis, OCR engines (it can use Tesseract or its own engine), natural language modeling, etc.

	[https://github.com/tmbdev/ocropy](https://github.com/tmbdev/ocropy) || [ocropy](https://aur.archlinux.org/packages/ocropy/)

*   **[YAGF](/index.php/YAGF "YAGF")** — Graphical interface for the CuneiForm text recognition program on the Linux platform.

	[http://symmetrica.net/cuneiform-linux/yagf-en.html](http://symmetrica.net/cuneiform-linux/yagf-en.html) || [yagf](https://www.archlinux.org/packages/?name=yagf)

### Note taking organizers

See also [Wikipedia:Comparison of notetaking software](https://en.wikipedia.org/wiki/Comparison_of_notetaking_software "wikipedia:Comparison of notetaking software").

#### Console

*   **deft** — Manage notes within emacs

	[http://jblevins.org/projects/deft/](http://jblevins.org/projects/deft/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **hnb (hierarchical notebook)** — Program to organize many kinds of data (addresses, to-do lists, ideas, book reviews, etc.) in one place using the XML format.

	[http://hnb.sourceforge.net/](http://hnb.sourceforge.net/) || [hnb](https://aur.archlinux.org/packages/hnb/)

*   **pynote** — Manage notes on the commandline

	[https://github.com/rumpelsepp/pynote](https://github.com/rumpelsepp/pynote) || [pynote](https://aur.archlinux.org/packages/pynote/)

#### Graphical

*   **[BasKet](https://en.wikipedia.org/wiki/BasKet_Note_Pads "wikipedia:BasKet Note Pads")** — Application for organizing, sharing, and taking notes. It can manage various types of information such as to-do lists, links, pictures, and other types, similar to a scrapbook.

	[http://basket.kde.org/](http://basket.kde.org/) || [basket](https://www.archlinux.org/packages/?name=basket)

*   **Cherrytree** — Hierarchical note taking application, featuring rich text and syntax highlighting, storing data in a single xml or sqlite file.

	[http://giuspen.com/cherrytree/](http://giuspen.com/cherrytree/) || [cherrytree](https://www.archlinux.org/packages/?name=cherrytree)

*   **[Gnote](https://en.wikipedia.org/wiki/Gnote "wikipedia:Gnote")** — Experimental port of Tomboy to C++.

	[https://wiki.gnome.org/Apps/Gnote](https://wiki.gnome.org/Apps/Gnote) || [gnote](https://www.archlinux.org/packages/?name=gnote)

*   **KeepNote** — Cross-platform GTK+ note-taking application with rich text formatting.

	[http://keepnote.org](http://keepnote.org) || [keepnote](https://www.archlinux.org/packages/?name=keepnote)

*   **KNotes** — A program that lets you write the computer equivalent of sticky notes.

	[https://www.kde.org/applications/utilities/knotes/](https://www.kde.org/applications/utilities/knotes/) || [knotes](https://www.archlinux.org/packages/?name=knotes)

*   **Laverna** — A JavaScript note taking application with Markdown editor and encryption support. Consider it like open source alternative to Evernote.

	[https://laverna.cc/](https://laverna.cc/) || [laverna](https://aur.archlinux.org/packages/laverna/)

*   **NoteCase** — Portable hierarchical note manager, coded in C++ using bindings to the GTK+ toolkit.

	[http://notecase.sourceforge.net](http://notecase.sourceforge.net) || [notecase](https://aur.archlinux.org/packages/notecase/)

*   **[org-mode](https://en.wikipedia.org/wiki/org-mode "wikipedia:org-mode")** — [Emacs](/index.php/Emacs "Emacs") mode for notes, project planning and authoring.

	[http://orgmode.org](http://orgmode.org) || [emacs-org-mode](https://aur.archlinux.org/packages/emacs-org-mode/)

*   **[Tomboy](https://en.wikipedia.org/wiki/Tomboy_(software) "wikipedia:Tomboy (software)")** — Desktop note-taking application for Linux and Unix with a wiki-like linking system to connect notes together.

	[https://wiki.gnome.org/Apps/Tomboy](https://wiki.gnome.org/Apps/Tomboy) || [tomboy](https://www.archlinux.org/packages/?name=tomboy)

*   **wiznote** — Opensource cross-platform cloud based note-taking client.

	[http://www.wiznote.com/](http://www.wiznote.com/) || [wiznote](https://www.archlinux.org/packages/?name=wiznote)

*   **[zim](/index.php/Zim "Zim")** — WYSIWYG text editor that aims at bringing the concept of a wiki to the desktop.

	[http://zim-wiki.org/](http://zim-wiki.org/) || [zim](https://www.archlinux.org/packages/?name=zim)

*   **znotes** — A lightweight crossplatform application for notes managment with simple interface, use qt4 libraries.

	[http://znotes.sourceforge.net/](http://znotes.sourceforge.net/) || [znotes](https://aur.archlinux.org/packages/znotes/)

### Mind-mapping tools

*   **FreeMind** — Premier free mind-mapping software written in Java.

	[http://freemind.sourceforge.net](http://freemind.sourceforge.net) || [freemind](https://www.archlinux.org/packages/?name=freemind)

*   **Freeplane** — Free and open source software application that supports thinking, sharing information and getting things done at work, in school and at home. The software can be used for mind mapping and analyzing the information contained in mind maps.

	[http://freeplane.sourceforge.net](http://freeplane.sourceforge.net) || [freeplane](https://aur.archlinux.org/packages/freeplane/)

*   **Labyrinth** — Lightweight mind-mapping tool with support for image import and drawing.

	[https://github.com/labyrinth-team/labyrinth](https://github.com/labyrinth-team/labyrinth) || [labyrinth](https://www.archlinux.org/packages/?name=labyrinth)

*   **Semantik** — A mind-mapping application for KDE.

	[https://ita1024.github.io/semantik/](https://ita1024.github.io/semantik/) || [semantik](https://aur.archlinux.org/packages/semantik/)

*   **TreeSheets** — The ultimate replacement for spreadsheets, mind mappers, outliners, PIMs, text editors and small databases.

	[http://strlen.com/treesheets/](http://strlen.com/treesheets/) || [treesheets-git](https://aur.archlinux.org/packages/treesheets-git/)

*   **View Your Mind** — Tool to generate and manipulate maps which show your thoughts. Such maps can help you to improve your creativity and effectivity. You can use them for time management, to organize tasks, to get an overview over complex contexts, to sort your ideas etc.

	[http://www.insilmaril.de/vym/](http://www.insilmaril.de/vym/) || [vym](https://www.archlinux.org/packages/?name=vym)

*   **Visual Understanding Environment** — Open Source project focused on creating flexible tools for managing and integrating digital resources in support of teaching, learning and research.

	[http://vue.tufts.edu](http://vue.tufts.edu) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **XMind** — Brainstorming and mind mapping application. It provides a rich set of different visualization styles, and allows sharing of created mind maps via their website.

	[http://www.xmind.net](http://www.xmind.net) || [xmind](https://www.archlinux.org/packages/?name=xmind)

### Character Selector

*   **GNOME Characters** — Character map application for GNOME

	[https://wiki.gnome.org/Design/Apps/CharacterMap](https://wiki.gnome.org/Design/Apps/CharacterMap) || [gnome-characters](https://www.archlinux.org/packages/?name=gnome-characters)

*   **gucharmap** — A GTK+ 3 Character Selector, distributed with GNOME desktop.

	[https://wiki.gnome.org/Apps/Gucharmap](https://wiki.gnome.org/Apps/Gucharmap) || [gucharmap](https://www.archlinux.org/packages/?name=gucharmap)

*   **kdeutils-kcharselect** — A tool to select special characters from all installed fonts and copy them into the clipboard. Distributed with KDE.

	[http://utils.kde.org/projects/kcharselect/](http://utils.kde.org/projects/kcharselect/) || [kcharselect](https://www.archlinux.org/packages/?name=kcharselect)

### Stylus notes taking

*   **Write** — a word processor for hand writing.

	[http://www.styluslabs.com/](http://www.styluslabs.com/) || [write_stylus](https://aur.archlinux.org/packages/write_stylus/)

*   **Gournal** — note-taking application written for usage on Tablet-PC, written in perl.

	[http://www.adebenham.com/old-stuff/gournal/](http://www.adebenham.com/old-stuff/gournal/) || [gournal](https://aur.archlinux.org/packages/gournal/)

*   **Xournal** — an application for notetaking, sketching, keeping a journal using a stylus.

	[http://xournal.sourceforge.net/](http://xournal.sourceforge.net/) || [xournal](https://www.archlinux.org/packages/?name=xournal)

### Bibliographic reference managers

See also [Wikipedia:Comparison of reference management software](https://en.wikipedia.org/wiki/Comparison_of_reference_management_software "wikipedia:Comparison of reference management software").

*   **Bibus** — A bibliographic database that can directly insert references in OpenOffice.org/LibreOffice and generate the bibliographic index.

	[http://bibus-biblio.sourceforge.net](http://bibus-biblio.sourceforge.net) || [bibus](https://aur.archlinux.org/packages/bibus/)

*   **DocEar** — Docear is an academic literature suite for searching, organizing and creating academic literature, built upon the mind mapping software Freeplane and the reference manager JabRef.

	[https://www.docear.org](https://www.docear.org) || [docear](https://aur.archlinux.org/packages/docear/)

*   **JabRef** — GUI frontend for BibTeX, written in Java.

	[http://jabref.sourceforge.net](http://jabref.sourceforge.net) || [jabref](https://aur.archlinux.org/packages/jabref/)

*   **Zotero** — Zotero Standalone. Is a free, easy-to-use tool to help you collect, organize, cite, and share your research sources.

	[http://www.zotero.org](http://www.zotero.org) || [zotero](https://aur.archlinux.org/packages/zotero/)

## Security

For detailed guides, see the main ArchWiki page, [Security](/index.php/Security "Security").

#### Firewalls

See the main article: [Firewalls](/index.php/Firewalls "Firewalls").

See also [Wikipedia:Comparison of firewalls](https://en.wikipedia.org/wiki/Comparison_of_firewalls "wikipedia:Comparison of firewalls").

#### Network security

*   **[Arpwatch](https://en.wikipedia.org/wiki/Arpwatch "wikipedia:Arpwatch")** — Tool that monitors ethernet activity and keeps a database of Ethernet/IP address pairings.

	[http://ee.lbl.gov/](http://ee.lbl.gov/) || [arpwatch](https://www.archlinux.org/packages/?name=arpwatch)

*   **Bro** — Powerful network analysis framework that is much different from the typical IDS you may know.

	[https://www.bro.org/](https://www.bro.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **EtherApe** — Graphical network monitor for Unix modeled after etherman. Featuring link layer, IP and TCP modes, it displays network activity graphically. Hosts and links change in size with traffic. Color coded protocols display.

	[http://etherape.sourceforge.net/](http://etherape.sourceforge.net/) || [etherape](https://www.archlinux.org/packages/?name=etherape)

*   **[Honeyd](/index.php/Honeyd "Honeyd")** — Tool that allows the user to set up and run multiple virtual hosts on a computer network.

	[http://www.honeyd.org/](http://www.honeyd.org/) || [honeyd](https://aur.archlinux.org/packages/honeyd/)

*   **IPTraf** — Console-based network monitoring utility.

	[https://fedorahosted.org/iptraf-ng/](https://fedorahosted.org/iptraf-ng/) || [iptraf-ng](https://www.archlinux.org/packages/?name=iptraf-ng)

*   **Kismet** — 802.11 layer2 wireless network detector, sniffer, and intrusion detection system.

	[http://www.kismetwireless.net/](http://www.kismetwireless.net/) || [kismet](https://www.archlinux.org/packages/?name=kismet)

*   **Nemesis** — Command-line network packet crafting and injection utility.

	[http://nemesis.sourceforge.net/](http://nemesis.sourceforge.net/) || [nemesis](https://www.archlinux.org/packages/?name=nemesis)

*   **[Nmap](/index.php/Nmap "Nmap")** — Security scanner used to discover hosts and services on a computer network, thus creating a "map" of the network.

	[http://nmap.org/](http://nmap.org/) || [nmap](https://www.archlinux.org/packages/?name=nmap)

*   **[Ntop](/index.php/Ntop "Ntop")** — Network probe that shows network usage in a way similar to what top does for processes.

	[http://www.ntop.org/](http://www.ntop.org/) || [ntop](https://www.archlinux.org/packages/?name=ntop)

*   **[Snort](/index.php/Snort "Snort")** — Network intrusion prevention and detection system.

	[http://www.snort.org/](http://www.snort.org/) || [snort](https://aur.archlinux.org/packages/snort/)

*   **Spectools** — A set of utilities for spectrum analyzer hardware including Wi-Spy devices.

	[https://www.kismetwireless.net/spectools/](https://www.kismetwireless.net/spectools/) || [spectools](https://aur.archlinux.org/packages/spectools/)

*   **[Sshguard](/index.php/Sshguard "Sshguard")** — Daemon that protects SSH and other services against brute-force attacts, similar to Fail2ban.

	[http://www.sshguard.net/](http://www.sshguard.net/) || [sshguard](https://www.archlinux.org/packages/?name=sshguard)

*   **[Suricata](/index.php/Suricata "Suricata")** — High performance Network IDS, IPS and Network Security Monitoring engine.

	[http://suricata-ids.org/](http://suricata-ids.org/) || [suricata](https://aur.archlinux.org/packages/suricata/)

*   **[Tcpdump](https://en.wikipedia.org/wiki/tcpdump "wikipedia:tcpdump")** — Common console-based packet analyzer that allows the user to intercept and display TCP/IP and other packets being transmitted or received over a network.

	[http://www.tcpdump.org/](http://www.tcpdump.org/) || [tcpdump](https://www.archlinux.org/packages/?name=tcpdump)

*   **[vnStat](/index.php/VnStat "VnStat")** — Console-based network traffic monitor that keeps a log of network traffic for the selected interfaces.

	[http://humdi.net/vnstat/](http://humdi.net/vnstat/) || [vnstat](https://www.archlinux.org/packages/?name=vnstat)

*   **[Wireshark](/index.php/Wireshark "Wireshark")** — Network protocol analyzer that lets you capture and interactively browse the traffic running on a computer network.

	[http://www.wireshark.org/](http://www.wireshark.org/) || [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt) [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk)

#### Threat and vulnerability detection

*   **AFICK** — Security tool that allows to monitor the changes on your files systems, and so can detect intrusions.

	[http://afick.sourceforge.net/](http://afick.sourceforge.net/) || [afick](https://aur.archlinux.org/packages/afick/)

*   **Lynis** — Security and system auditing tool to harden Unix/Linux systems.

	[https://cisofy.com/lynis/](https://cisofy.com/lynis/) || [lynis](https://www.archlinux.org/packages/?name=lynis)

*   **[Metasploit Framework](/index.php/Metasploit_Framework "Metasploit Framework")** — An advanced open-source platform for developing, testing, and using exploit code.

	[http://www.metasploit.com/](http://www.metasploit.com/) || [metasploit](https://www.archlinux.org/packages/?name=metasploit)

*   **[Nessus](/index.php/Nessus "Nessus")** — Comprehensive vulnerability scanning program.

	[http://www.nessus.org/products/nessus](http://www.nessus.org/products/nessus) || [nessus](https://aur.archlinux.org/packages/nessus/)

*   **[OpenVAS](/index.php/OpenVAS "OpenVAS")** — Framework of several services and tools offering a comprehensive and powerful vulnerability scanning and vulnerability management solution. FOSS Nessus fork.

	[http://www.openvas.org/](http://www.openvas.org/) || [openvas](https://www.archlinux.org/groups/x86_64/openvas/)

*   **Osiris** — Tool for monitoring system integrity and changes across a network.

	[https://launchpad.net/osiris](https://launchpad.net/osiris) || [osiris](https://www.archlinux.org/packages/?name=osiris)

*   **OSSEC** — Open Source Host-based Intrusion Detection System that performs log analysis, file integrity checking, policy monitoring, rootkit detection, real-time alerting and active response.

	[https://ossec.github.io/](https://ossec.github.io/) || [ossec-agent](https://aur.archlinux.org/packages/ossec-agent/) [ossec-local](https://aur.archlinux.org/packages/ossec-local/) [ossec-server](https://aur.archlinux.org/packages/ossec-server/)

*   **Samhain** — Host-based intrusion detection system (HIDS) provides file integrity checking and log file monitoring/analysis, as well as rootkit detection, port monitoring, detection of rogue SUID executables, and hidden processes.

	[http://www.la-samhna.de/samhain/index.html](http://www.la-samhna.de/samhain/index.html) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Tiger** — Security tool that can be use both as a security audit and intrusion detection system.

	[http://www.nongnu.org/tiger/](http://www.nongnu.org/tiger/) || [tiger](https://aur.archlinux.org/packages/tiger/)

*   **[Tripwire](https://en.wikipedia.org/wiki/Open_Source_Tripwire "wikipedia:Open Source Tripwire")** — Intrusion detection system.

	[https://github.com/Tripwire/tripwire-open-source](https://github.com/Tripwire/tripwire-open-source) || [tripwire](https://aur.archlinux.org/packages/tripwire/)

#### File security

*   **[AIDE](/index.php/AIDE "AIDE")** — File and directory integrity checker.

	[http://aide.sourceforge.net/](http://aide.sourceforge.net/) || [aide](https://www.archlinux.org/packages/?name=aide)

*   **Logcheck** — Simple utility which is designed to allow a system administrator to view the logfiles which are produced upon hosts under their control.

	[https://logcheck.alioth.debian.org/](https://logcheck.alioth.debian.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Logwatch](/index.php/Logwatch "Logwatch")** — Customizable log analysis system.

	[http://sourceforge.net/projects/logwatch/](http://sourceforge.net/projects/logwatch/) || [logwatch](https://www.archlinux.org/packages/?name=logwatch)

*   **OpenDLP** — OpenDLP is a free and open source, agent- and agentless-based, centrally-managed, massively distributable data loss prevention tool.

	[https://code.google.com/archive/p/opendlp/](https://code.google.com/archive/p/opendlp/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Swatch** — Utility that can monitor just about any type of log.

	[http://swatch.sourceforge.net/](http://swatch.sourceforge.net/) || [swatch](https://aur.archlinux.org/packages/swatch/)

#### Anti malware

*   **chkrootkit** — Locally checks for signs of a rootkit.

	[http://www.chkrootkit.org/](http://www.chkrootkit.org/) || [chkrootkit](https://aur.archlinux.org/packages/chkrootkit/)

*   **[ClamAV](/index.php/ClamAV "ClamAV")** — Open source antivirus engine for detecting trojans, viruses, malware & other malicious threats.

	[http://www.clamav.net/](http://www.clamav.net/) || [clamav](https://www.archlinux.org/packages/?name=clamav)

*   **Linux Malware Detect** — Malware scanner designed around the threats faced in shared hosted environments.

	[https://www.rfxn.com/projects/linux-malware-detect/](https://www.rfxn.com/projects/linux-malware-detect/) || [maldet](https://aur.archlinux.org/packages/maldet/)

*   **Rootkit Hunter** — Checks machines for the presence of rootkits and other unwanted tools.

	[http://rkhunter.sourceforge.net/](http://rkhunter.sourceforge.net/) || [rkhunter](https://www.archlinux.org/packages/?name=rkhunter)

#### Backup programs

See the main article: [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs").

See also [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software").

#### Screen lockers

**Warning:** Only *sflock*, *physlock*, *Cinnamon Screensaver*, *MATE Screensaver* and *GNOME Screensaver* are able to block tty access.

*   **Cinnamon Screensaver** — Screen locker for the Cinnamon desktop.

	[https://github.com/linuxmint/cinnamon-screensaver](https://github.com/linuxmint/cinnamon-screensaver) || [cinnamon-screensaver](https://www.archlinux.org/packages/?name=cinnamon-screensaver)

*   **GNOME Screensaver** — Screen locker for the GNOME Flashback desktop.

	[https://wiki.gnome.org/Projects/GnomeScreensaver](https://wiki.gnome.org/Projects/GnomeScreensaver) || [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver)

*   **i3lock** — A simple screen locker. Provides user feedback, uses PAM authentication, supports DPMS. The background can be set to an image or solid color.

	[http://i3wm.org/i3lock/](http://i3wm.org/i3lock/) || [i3lock](https://www.archlinux.org/packages/?name=i3lock)

*   **i3lock-blur** — Fork of *i3lock* which can use your desktop with the blur effect applied as a background.

	[https://github.com/karulont/i3lock-blur](https://github.com/karulont/i3lock-blur) || [i3lock-blur](https://aur.archlinux.org/packages/i3lock-blur/)

*   **i3lock-wrapper** — A simple wrapper around *i3lock* which sets up a blurred screenshot of the desktop as a background image.

	[https://github.com/ashinkarov/i3-extras](https://github.com/ashinkarov/i3-extras) || [i3lock-wrapper](https://aur.archlinux.org/packages/i3lock-wrapper/)

*   **Light-locker** — A simple locker (forked from *gnome-screensaver*) that aims to have simple, sane, secure defaults and be well integrated with the desktop while not carrying any desktop-specific dependencies. It relies on [LightDM](/index.php/LightDM "LightDM") for locking and unlocking your session via ConsoleKit/UPower or *logind/systemd*

	[https://github.com/the-cavalry/light-locker](https://github.com/the-cavalry/light-locker) || [light-locker](https://www.archlinux.org/packages/?name=light-locker)

*   **MATE Screensaver** — Screensaver and locker for MATE Desktop Environment.

	[https://github.com/mate-desktop/mate-screensaver](https://github.com/mate-desktop/mate-screensaver) || [mate-screensaver](https://www.archlinux.org/packages/?name=mate-screensaver)

*   **physlock** — Screen and console locker.

	[https://github.com/muennich/physlock](https://github.com/muennich/physlock) || [physlock](https://aur.archlinux.org/packages/physlock/)

*   **sflock** — Simple screen locker utility for X, based on slock. Provides a very basic user feedback.

	[https://github.com/benruijl/sflock](https://github.com/benruijl/sflock) || [sflock-git](https://aur.archlinux.org/packages/sflock-git/)

*   **slock** — Very simple and lightweight X screen locker. Offers only a black background when locked, there are no animations or text fields.

	[http://tools.suckless.org/slock](http://tools.suckless.org/slock) || [slock](https://www.archlinux.org/packages/?name=slock)

*   **sxlock** — Fork of sflock with a few enhancements. Provides basic user feedback, uses PAM authentication, supports DPMS and RandR. Supports `sxlock.service` to lock the screen on suspend/hibernation. See the [README](https://github.com/lahwaacz/sxlock/blob/master/README.md) for more information.

	[https://github.com/lahwaacz/sxlock](https://github.com/lahwaacz/sxlock) || [sxlock-git](https://aur.archlinux.org/packages/sxlock-git/)

*   **vlock** — TTY locker. A mirror of the [original vlock](https://lists.archlinux.org/pipermail/aur-general/2013-July/024662.html) is available at [github](https://github.com/WorMzy/vlock).

	[http://www.kbd-project.org](http://www.kbd-project.org) || [kbd](https://www.archlinux.org/packages/?name=kbd)

*   **xlockmore** — Simple X11 screen lock with PAM support.

	[http://www.tux.org/~bagleyd/xlockmore.html](http://www.tux.org/~bagleyd/xlockmore.html) || [xlockmore](https://www.archlinux.org/packages/?name=xlockmore)

*   **[XScreenSaver](/index.php/XScreenSaver "XScreenSaver")** — Screen saver and locker for the X Window System.

	[http://www.jwz.org/xscreensaver/](http://www.jwz.org/xscreensaver/) || [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)

*   **XSecureLock** — X11 screen lock utility designed with the primary goal of security.

	[https://github.com/google/xsecurelock](https://github.com/google/xsecurelock) || [xsecurelock-git](https://aur.archlinux.org/packages/xsecurelock-git/)

#### Hash checkers

*   **cfv** — Tiny utility to both test and create checksum files, support `.sfv`, `.csv`, `.crc`, `.md5`, `md5sum`, `sha1sum`, `.torrent`, `par`, and `.par2` files.

	[http://cfv.sourceforge.net/](http://cfv.sourceforge.net/) || [cfv](https://www.archlinux.org/packages/?name=cfv)

*   **GtkHash** — A GTK+ utility for computing message digests or checksums

	[http://gtkhash.sourceforge.net/](http://gtkhash.sourceforge.net/) || [gtkhash](https://aur.archlinux.org/packages/gtkhash/)

*   **hashdeep** — A cross-platform tools to computer hashes, or message digests, for any number of files

	[http://md5deep.sourceforge.net/](http://md5deep.sourceforge.net/) || [md5deep](https://aur.archlinux.org/packages/md5deep/)

*   **Parano** — A GNOME frontend for creating/editing/checking MD5 and SFV files

	[http://parano.berlios.de/](http://parano.berlios.de/) || [parano](https://aur.archlinux.org/packages/parano/)

*   **Quick Hash GUI** — A GUI to enable the rapid selection and subsequent hashing of files (individually or recursively throughout a folder structure) text and (on Linux) disks.

	[http://sourceforge.net/projects/quickhash/](http://sourceforge.net/projects/quickhash/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **RHash** — Utility for verifying hash sums (SFV, CRC, etc). Supports lots of algorithms.

	[http://rhash.anz.ru/](http://rhash.anz.ru/) || [rhash](https://www.archlinux.org/packages/?name=rhash)

*   **MassHash** — A set of file hashing tools (both CLI and GTK+ GUI) written in Python. Supported algorithms include MD5, SHA-1, SHA-224, SHA-256, SHA-384, SHA-512.

	[http://jdleicher.github.io/MassHash/](http://jdleicher.github.io/MassHash/) || [masshash](https://aur.archlinux.org/packages/masshash/)

#### Encryption, signing, steganography

*   **ccrypt** — A command-line utility for encrypting and decrypting files and streams.

	[http://ccrypt.sourceforge.net/](http://ccrypt.sourceforge.net/) || [ccrypt](https://www.archlinux.org/packages/?name=ccrypt)

*   **[Enigmail](https://en.wikipedia.org/wiki/Enigmail "wikipedia:Enigmail")** — *a security extension to Mozilla Thunderbird and Seamonkey. It enables you to write and receive email messages signed and/or encrypted with the OpenPGP standard.*

	[https://enigmail.net](https://enigmail.net) || [thunderbird-enigmail](https://aur.archlinux.org/packages/thunderbird-enigmail/)

*   **[GnuPG](/index.php/GnuPG "GnuPG")** — The GNU project's complete and free implementation of the OpenPGP standard as defined by RFC4880\. Free and Open Source replacement of PGP, mostly used for digital signing of packages.

	[http://gnupg.org/](http://gnupg.org/) || [gnupg](https://www.archlinux.org/packages/?name=gnupg)

*   **gzsteg** — A utiltiy that can hide data in gzip compressed files

	[http://www.nic.funet.fi/pub/crypt/steganography/](http://www.nic.funet.fi/pub/crypt/steganography/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=gzsteg)</small>

*   **[KGpg](https://en.wikipedia.org/wiki/KGPG "wikipedia:KGPG")** — *a simple interface for GnuPG* for KDE.

	[https://www.kde.org/applications/utilities/kgpg/](https://www.kde.org/applications/utilities/kgpg/) || [kdeutils-kgpg](https://www.archlinux.org/packages/?name=kdeutils-kgpg)

*   **[Seahorse](https://en.wikipedia.org/wiki/Seahorse_(software) "wikipedia:Seahorse (software)")** — *GNOME application for managing encryption keys and passwords in the GnomeKeyring.*

	[https://wiki.gnome.org/Apps/Seahorse/](https://wiki.gnome.org/Apps/Seahorse/) || [seahorse](https://www.archlinux.org/packages/?name=seahorse)

*   **silenteye** — A steganography application written in C++, use Qt4 library.

	[http://www.silenteye.org/](http://www.silenteye.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=silenteye)</small>

*   **snow** — Steganography program for concealing messages in text files

	[http://www.darkside.com.au/snow/](http://www.darkside.com.au/snow/) || [snow](https://aur.archlinux.org/packages/snow/)

*   **steghide** — A steganography utility that is able to hide data in various kinds of image and audio files.

	[http://steghide.sourceforge.net](http://steghide.sourceforge.net) || [steghide](https://www.archlinux.org/packages/?name=steghide)

*   **stegparty** — A steganography utility hides text by typoing text existing text files.

	[https://github.com/countrygeek/stegparty](https://github.com/countrygeek/stegparty) || [stegparty](https://aur.archlinux.org/packages/stegparty/)

#### Password managers

*   **Console Password Manager** — Curses based password manager using PGP-encryption.

	[https://github.com/comotion/cpm](https://github.com/comotion/cpm) || [cpm](https://aur.archlinux.org/packages/cpm/)

*   **Enpass** — A multiplatform password manager

	[https://www.enpass.io/](https://www.enpass.io/) || [enpass-bin](https://aur.archlinux.org/packages/enpass-bin/)

*   **Figaro's Password Manager 2** — GTK2 port of [Figaro's Password Manager](http://fpm.sourceforge.net/) with some new enhancements.

	[http://als.regnet.cz/fpm2/](http://als.regnet.cz/fpm2/) || [fpm2](https://aur.archlinux.org/packages/fpm2/)

*   **GPass** — Password manegement software for GNOME2 desktop.

	[https://github.com/raffael-sfm/gpass](https://github.com/raffael-sfm/gpass) || [gpass](https://aur.archlinux.org/packages/gpass/)

*   **GPassword Manager** — Simple, lightweight and cross-platform utility for managing and accessing passwords.

	[http://sourceforge.net/projects/gpasswordman/](http://sourceforge.net/projects/gpasswordman/) || [gpasswordman](https://aur.archlinux.org/packages/gpasswordman/)

*   **Gtkpass** — Gtkpass is a GTK and Libkpass-based password manager for KeePass 1.x databases.

	[https://sourceforge.net/projects/gtkpass/](https://sourceforge.net/projects/gtkpass/) || [gtkpass](https://aur.archlinux.org/packages/gtkpass/)

*   **Ked Password Manager** — A password manager that helps to manage large numbers of passwords.

	[http://kedpm.sourceforge.net](http://kedpm.sourceforge.net) || [kedpm](https://aur.archlinux.org/packages/kedpm/)

*   **[KeePass Password Safe](/index.php/KeePass "KeePass")** — Free open source Mono-based password manager, which helps you to manage your passwords in a secure way.

	[http://keepass.info/](http://keepass.info/) || [keepass](https://www.archlinux.org/packages/?name=keepass)

*   **KeePassC** — KeePassC is a curses-based password manager compatible to KeePass v.1.x and KeePassX.

	[https://raymontag.github.com/keepassc](https://raymontag.github.com/keepassc) || [keepassc](https://aur.archlinux.org/packages/keepassc/)

*   **KeePassX** — Free and open source Qt-based password manager. Compatible with KeePass v.1.x and KeePass v.2.x.

	[http://www.keepassx.org/](http://www.keepassx.org/) || [keepassx](https://www.archlinux.org/packages/?name=keepassx) [keepassx2](https://www.archlinux.org/packages/?name=keepassx2)

*   **MyPasswords** — What you need for managing your passwords, including the passwords of your online accounts, bank accounts and ... with the corresponding URLs.

	[http://sourceforge.net/projects/mypasswords7/](http://sourceforge.net/projects/mypasswords7/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **MyPasswordSafe** — Easy-to-use QT based password manager, compatible with Password Safe files (and therefore pwsafe).

	[http://www.semanticgap.com/myps/](http://www.semanticgap.com/myps/) || [mypasswordsafe](https://aur.archlinux.org/packages/mypasswordsafe/)

*   **Pasaffe** — Easy to use password manager for Gnome with a Password Safe 3.0 compatible database.

	[https://launchpad.net/pasaffe](https://launchpad.net/pasaffe) || [pasaffe](https://aur.archlinux.org/packages/pasaffe/)

*   **[pass](/index.php/Pass "Pass")** — Simple console based password manager

	[http://www.passwordstore.org/](http://www.passwordstore.org/) || [pass](https://www.archlinux.org/packages/?name=pass)

*   **Password Gorilla** — A cross-platform password manager.

	[https://github.com/zdia/gorilla/wiki/](https://github.com/zdia/gorilla/wiki/) || [password-gorilla](https://aur.archlinux.org/packages/password-gorilla/)

*   **Password Safe** — Simple and secure password manager.

	[http://passwordsafe.sourceforge.net/](http://passwordsafe.sourceforge.net/) || [passwordsafe](https://aur.archlinux.org/packages/passwordsafe/)

*   **pwsafe** — Unix commandline program that manages encrypted password databases.

	[http://nsd.dyndns.org/pwsafe/](http://nsd.dyndns.org/pwsafe/) || [pwsafe](https://www.archlinux.org/packages/?name=pwsafe)

*   **QPass** — Easy to use password manager with built-in password generator.

	[http://qpass.sourceforge.net](http://qpass.sourceforge.net) || [qpass](https://aur.archlinux.org/packages/qpass/)

*   **Revelation** — Password manager for the GNOME desktop.

	[http://revelation.olasagasti.info/](http://revelation.olasagasti.info/) || [revelation](https://aur.archlinux.org/packages/revelation/)

*   **spm** — Simple Password Manager written entirely in POSIX shell using PGP. Fast, lightweight and easily scriptable.

	[https://notabug.org/kl3/spm/](https://notabug.org/kl3/spm/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **Seahorse** — GNOME application for managing encryption keys and passwords in the GnomeKeyring.

	[https://wiki.gnome.org/Apps/Seahorse](https://wiki.gnome.org/Apps/Seahorse) || [seahorse](https://www.archlinux.org/packages/?name=seahorse)

*   **Universal Password Manager** — Allows you to store usernames, passwords, URLs and generic notes in an encrypted database protected by one master password.

	[http://upm.sourceforge.net/](http://upm.sourceforge.net/) || [upm](https://aur.archlinux.org/packages/upm/)

## Science

**Note:** For possibly more up to date selection of scientific applications, try checking the [AUR 'science' category](https://aur.archlinux.org/packages.php?O=0&do_Search=Go&detail=1&C=15&SeB=nd&SB=v&SO=d&PP=50)

### Scientific documents

See the main article: [List of applications/Documents#Scientific documents](/index.php/List_of_applications/Documents#Scientific_documents "List of applications/Documents").

### Mathematics

#### Calculator

See also [Wikipedia:Comparison of software calculators](https://en.wikipedia.org/wiki/Comparison_of_software_calculators "wikipedia:Comparison of software calculators").

*   **[bc](https://en.wikipedia.org/wiki/bc_programming_language "wikipedia:bc programming language")** — Arbitrary precision calculator language.

	[http://www.gnu.org/software/bc/](http://www.gnu.org/software/bc/) || [bc](https://www.archlinux.org/packages/?name=bc)

*   **calc** — Arbitrary precision console calculator.

	[http://www.isthe.com/chongo/tech/comp/calc/](http://www.isthe.com/chongo/tech/comp/calc/) || [calc](https://www.archlinux.org/packages/?name=calc)

*   **Extcalc** — Qt-based scientfic graphical calculator.

	[http://extcalc-linux.sourceforge.net/](http://extcalc-linux.sourceforge.net/) || [extcalc](https://aur.archlinux.org/packages/extcalc/)

*   **galculator** — GTK+ based scientific calculator.

	[http://galculator.sourceforge.net/](http://galculator.sourceforge.net/) || [galculator](https://www.archlinux.org/packages/?name=galculator) [galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)

*   **[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")** — Scientific calculator included in the GNOME desktop.

	[https://wiki.gnome.org/Apps/Calculator](https://wiki.gnome.org/Apps/Calculator) || [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)

*   **[GCalctool](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")** — Scientific calculator included in the GNOME desktop (old GTK2 version).

	[http://www.gnome.org](http://www.gnome.org) || [gcalctool-oldgui](https://aur.archlinux.org/packages/gcalctool-oldgui/)

*   **KAlgebra** — Calculator and 3D plotter included in KDE EDU.

	[http://www.kde.org/applications/education/kalgebra/](http://www.kde.org/applications/education/kalgebra/) || [kalgebra](https://www.archlinux.org/packages/?name=kalgebra)

*   **[KCalc](https://en.wikipedia.org/wiki/KCalc "wikipedia:KCalc")** — Scientific calculator included in the KDE desktop.

	[http://kde.org/applications/utilities/kcalc/](http://kde.org/applications/utilities/kcalc/) || [kcalc](https://www.archlinux.org/packages/?name=kcalc)

*   **Qalculate** — Calculator and equation solver with fault-tolerant parsing, constant recognition and units.

	[http://qalculate.github.io/](http://qalculate.github.io/) || [libqalculate](https://www.archlinux.org/packages/?name=libqalculate)

*   **SpeedCrunch** — Fast, high precision and powerful cross-platform calculator.

	[http://speedcrunch.org](http://speedcrunch.org) || [speedcrunch](https://www.archlinux.org/packages/?name=speedcrunch)

*   **[xcalc](https://en.wikipedia.org/wiki/xcalc "wikipedia:xcalc")** — Scientific calculator for X with algebraic and reverse polish notation modes.

	[http://xorg.freedesktop.org/](http://xorg.freedesktop.org/) || [xorg-xcalc](https://www.archlinux.org/packages/?name=xorg-xcalc)

#### Computer algebra system

See also [Wikipedia:Comparison of computer algebra systems](https://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems "wikipedia:Comparison of computer algebra systems").

*   **[AXIOM](https://en.wikipedia.org/wiki/Axiom_(computer_algebra_system) "wikipedia:Axiom (computer algebra system)")** — FriCAS: derivative of the powerful AXIOM-CAS

	[http://fricas.sourceforge.net](http://fricas.sourceforge.net) || [fricas](https://aur.archlinux.org/packages/fricas/)

*   **[Fermat](https://en.wikipedia.org/wiki/Fermat_(computer_algebra_system) "wikipedia:Fermat (computer algebra system)")** — Computer algebra system that does arithmetic of arbitrarily long integers and fractions, multivariate polynomials, symbolic calculations, matrices over polynomial rings, graphics, and other numerical calculations.

	[http://home.bway.net/lewis/](http://home.bway.net/lewis/) || [fermat](https://aur.archlinux.org/packages/fermat/)

*   **[GAP](https://en.wikipedia.org/wiki/GAP_(computer_algebra_system) "wikipedia:GAP (computer algebra system)")** — Computer algebra system for computational discrete algebra with particular emphasis on computational group theory.

	[http://www.gap-system.org](http://www.gap-system.org) || [gap](https://www.archlinux.org/packages/?name=gap)

*   **[Maple](/index.php/Maple "Maple")** — Famous commercial CAS. Often used in education.

	[http://www.maplesoft.com/products/maple/](http://www.maplesoft.com/products/maple/) ||

*   **Mathics** — A free CAS for symbolic mathematical computations which uses [Python](/index.php/Python "Python") as its main language. It aims at achieving a Mathematica-compatible syntax and functions. It relies mostly on Sympy for most mathematical tasks and, optionally, Sage for more advanced functionality.

	[http://www.mathics.org/](http://www.mathics.org/) || [mathics](https://aur.archlinux.org/packages/mathics/)

*   **[Mathomatic](https://en.wikipedia.org/wiki/Mathomatic "wikipedia:Mathomatic")** — General purpose Computer Algebra System written in C.

	[http://www.mathomatic.org/](http://www.mathomatic.org/) || [mathomatic](https://www.archlinux.org/packages/?name=mathomatic)

*   **[Maxima](https://en.wikipedia.org/wiki/Maxima_(software) "wikipedia:Maxima (software)")** — [Maple](https://en.wikipedia.org/wiki/Maple_(software) "wikipedia:Maple (software)")/[Mathematica](https://en.wikipedia.org/wiki/Wolfram_Mathematica "wikipedia:Wolfram Mathematica")-like program with a wxWidgets based frontend.

	[http://maxima.sourceforge.net/](http://maxima.sourceforge.net/) || [maxima](https://www.archlinux.org/packages/?name=maxima) [wxmaxima](https://www.archlinux.org/packages/?name=wxmaxima)

*   **[PARI/GP](https://en.wikipedia.org/wiki/PARI/GP "wikipedia:PARI/GP")** — Computer algebra system designed for fast computations in number theory.

	[http://pari.math.u-bordeaux.fr/](http://pari.math.u-bordeaux.fr/) || [pari](https://www.archlinux.org/packages/?name=pari)

*   **[Xcas](https://en.wikipedia.org/wiki/Xcas "wikipedia:Xcas")** — User interface to Giac, a free, basic computer algebra system.

	[http://www-fourier.ujf-grenoble.fr/~parisse/giac.html](http://www-fourier.ujf-grenoble.fr/~parisse/giac.html) || [xcas](https://www.archlinux.org/packages/?name=xcas)

#### Scientific or technical computing

See also [Wikipedia:Comparison of numerical analysis software](https://en.wikipedia.org/wiki/Comparison_of_numerical_analysis_software "wikipedia:Comparison of numerical analysis software").

*   **EngLab** — Cross-compile mathematical platform with a C like syntax.

	[http://englab.bugfest.net](http://englab.bugfest.net) || [englab](https://aur.archlinux.org/packages/englab/)

*   **[FreeMat](https://en.wikipedia.org/wiki/FreeMat "wikipedia:FreeMat")** — Matlab-like program that supports many of its functions and features a codeless interface to external C, C++, and Fortran code, further parallel distributed algorithm development (via MPI), and 3D visualization capabilities.

	[http://freemat.sourceforge.net/](http://freemat.sourceforge.net/) || [freemat](https://www.archlinux.org/packages/?name=freemat)

*   **[GNU Radio](/index.php/GNU_Radio "GNU Radio")** — Software development toolkit that provides signal processing blocks to implement software radios.

	[http://gnuradio.org/redmine/projects/gnuradio/wiki](http://gnuradio.org/redmine/projects/gnuradio/wiki) || [gnuradio](https://www.archlinux.org/packages/?name=gnuradio)

*   **[matplotlib (PyLab)](https://en.wikipedia.org/wiki/matplotlib "wikipedia:matplotlib")** — Collection of Python modules (pyplot, numpy, etc.) used for scientific calculations.

	[http://www.scipy.org/](http://www.scipy.org/) || [python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib)

*   **[Octave](/index.php/Octave "Octave")** — [Matlab](/index.php/Matlab "Matlab")-like language and interface for numerical computations.

	[http://www.gnu.org/software/octave/](http://www.gnu.org/software/octave/) || [octave](https://www.archlinux.org/packages/?name=octave)

*   **[Sage-mathematics](/index.php/Sage-mathematics "Sage-mathematics")** — Mathematics software system, that combines many existing open-source packages into a common Python interface. Alternative to Magma, Maple, Mathematica and Matlab.

	[http://www.sagemath.org](http://www.sagemath.org) || [sagemath](https://www.archlinux.org/packages/?name=sagemath)

*   **[Scilab](https://en.wikipedia.org/wiki/Scilab "wikipedia:Scilab")** — Matlab alternative used for numerical computations. Its syntax is not equivalent to that of Matlab, but it can be easily converted.

	[http://www.scilab.org/](http://www.scilab.org/) || [scilab](https://aur.archlinux.org/packages/scilab/)

#### Statistics

See also [Wikipedia:Comparison of statistical packages](https://en.wikipedia.org/wiki/Comparison_of_statistical_packages "wikipedia:Comparison of statistical packages").

*   **[JAGS](https://en.wikipedia.org/wiki/Just_another_Gibbs_sampler "wikipedia:Just another Gibbs sampler") (Just another Gibbs sampler)** — Cross-platform program for analysis of Bayesian hierarchical models using Markov Chain Monte Carlo (MCMC) simulation.

	[http://mcmc-jags.sourceforge.net/](http://mcmc-jags.sourceforge.net/) || [jags](https://aur.archlinux.org/packages/jags/)

*   **[Python Data Analysis Library (pandas)](https://en.wikipedia.org/wiki/Pandas_(software) "wikipedia:Pandas (software)")** — Providing high-performance, easy-to-use data structures and data analysis tools with Python programming language.

	[http://pandas.pydata.org/](http://pandas.pydata.org/) || [python2-pandas](https://www.archlinux.org/packages/?name=python2-pandas) [python-pandas](https://www.archlinux.org/packages/?name=python-pandas)

*   **[PSPP](https://en.wikipedia.org/wiki/PSPP "wikipedia:PSPP")** — Free SPSS implementation.

	[http://www.gnu.org/software/pspp/](http://www.gnu.org/software/pspp/) || [pspp](https://aur.archlinux.org/packages/pspp/)

*   **[R](/index.php/R "R")** — Software environment for statistical computing and graphics.

	[http://cran.r-project.org/](http://cran.r-project.org/) || [r](https://www.archlinux.org/packages/?name=r)

*   **[RKWard](https://en.wikipedia.org/wiki/RKWard "wikipedia:RKWard")** — Frontend for the statistical language R.

	[http://rkward.sourceforge.net/](http://rkward.sourceforge.net/) || [rkward](https://aur.archlinux.org/packages/rkward/)

*   **[RStudio](https://en.wikipedia.org/wiki/RStudio "wikipedia:RStudio")** — A powerful and productive IDE for R written in Qt.

	[http://www.rstudio.com/](http://www.rstudio.com/) || [rstudio-desktop-bin](https://aur.archlinux.org/packages/rstudio-desktop-bin/)

#### Data evaluation

See also [Wikipedia:List of information graphics software](https://en.wikipedia.org/wiki/List_of_information_graphics_software "wikipedia:List of information graphics software").

*   **[Fityk](https://en.wikipedia.org/wiki/Fityk "wikipedia:Fityk")** — Curve fitting and data analysis application, predominantly used to fit analytical, bell-shaped functions to experimental data.

	[http://fityk.nieto.pl/](http://fityk.nieto.pl/) || [fityk](https://aur.archlinux.org/packages/fityk/)

*   **[Gnuplot](https://en.wikipedia.org/wiki/gnuplot "wikipedia:gnuplot")** — Command-line program that can generate 2D and 3D plots of functions, data, and data fits.

	[http://www.gnuplot.info/](http://www.gnuplot.info/) || [gnuplot](https://www.archlinux.org/packages/?name=gnuplot)

*   **[Grace](https://en.wikipedia.org/wiki/Grace_(plotting_tool) "wikipedia:Grace (plotting tool)")** — WYSIWYG 2D graph plotting tool.

	[http://plasma-gate.weizmann.ac.il/Grace/](http://plasma-gate.weizmann.ac.il/Grace/) || [grace](https://www.archlinux.org/packages/?name=grace) [qtgrace](https://aur.archlinux.org/packages/qtgrace/) [gracegtk](https://aur.archlinux.org/packages/gracegtk/)

*   **[LabPlot](https://en.wikipedia.org/wiki/LabPlot "wikipedia:LabPlot")** — Free software data analysis and visualization application, similar to SciDAVis.

	[https://labplot.kde.org/](https://labplot.kde.org/) || [labplot-kf5](https://aur.archlinux.org/packages/labplot-kf5/)

*   **[QtiPlot](https://en.wikipedia.org/wiki/QtiPlot or [SigmaPlot](https://en.wikipedia.org/wiki/SigmaPlot "wikipedia:SigmaPlot").

	[http://www.qtiplot.com/](http://www.qtiplot.com/) || [qtiplot](https://www.archlinux.org/packages/?name=qtiplot)

*   **[ROOT](https://en.wikipedia.org/wiki/ROOT "wikipedia:ROOT")** — Data analysis program and library (originally for particle physics) developed by CERN.

	[http://root.cern.ch/drupal/](http://root.cern.ch/drupal/) || [root](https://aur.archlinux.org/packages/root/)

*   **[SciDAVis](https://en.wikipedia.org/wiki/SciDAVis "wikipedia:SciDAVis")** — Fork of QtiPlot with the goal of being better documented and more user friendly.

	[http://scidavis.sourceforge.net/](http://scidavis.sourceforge.net/) || [scidavis](https://aur.archlinux.org/packages/scidavis/)

See also [List of applications#Spreadsheets](/index.php/List_of_applications#Spreadsheets "List of applications")

### Chemistry and biology

#### Computational biology and bioinformatics

See also [Wikipedia:List of open source bioinformatics software](https://en.wikipedia.org/wiki/List_of_open_source_bioinformatics_software "wikipedia:List of open source bioinformatics software").

*   **[BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL") (Biochemical Algorithms Library)** — Application framework in C++ that provides an extensive set of data structures as well as classes for molecular mechanics, advanced solvation methods, comparison and analysis of protein structures, file import/export, and visualization.

	[http://www.ball-project.org/](http://www.ball-project.org/) || [ball](https://aur.archlinux.org/packages/ball/)

*   **[BioJava](https://en.wikipedia.org/wiki/BioJava "wikipedia:BioJava")** — Set of Java tools for computational biology, as well as bioinformatics.

	[http://biojava.org](http://biojava.org) || [biojava](https://aur.archlinux.org/packages/biojava/)

*   **[Biopython](https://en.wikipedia.org/wiki/Biopython "wikipedia:Biopython")** — Python package with tools for computational biology, as well as bioinformatics.

	[http://biopython.org/wiki/Biopython](http://biopython.org/wiki/Biopython) || [python-biopython](https://www.archlinux.org/packages/?name=python-biopython) [python2-biopython](https://www.archlinux.org/packages/?name=python2-biopython)

*   **[EMBOSS](https://en.wikipedia.org/wiki/EMBOSS "wikipedia:EMBOSS") (European Molecular Biology Open Software Suite)** — Open source software analysis package specially developed for the needs of the molecular biology and bioinformatics user community.

	[http://emboss.sourceforge.net/](http://emboss.sourceforge.net/) || [emboss](https://aur.archlinux.org/packages/emboss/)

*   **[MEGA](https://en.wikipedia.org/wiki/MEGA,_Molecular_Evolutionary_Genetics_Analysis "wikipedia:MEGA, Molecular Evolutionary Genetics Analysis") (Molecular Evolutionary Genetics Analysis)** — Integrated tool for conducting automatic and manual sequence alignment, inferring phylogenetic trees, mining web-based databases, estimating rates of molecular evolution, inferring ancestral sequences, and testing evolutionary hypotheses.

	[http://www.megasoftware.net/](http://www.megasoftware.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[MUMmer](https://en.wikipedia.org/wiki/MUMmer "wikipedia:MUMmer")** — Bioinformatics software system for sequence alignment based on suffix trees.

	[http://mummer.sourceforge.net/](http://mummer.sourceforge.net/) || [mummer](https://aur.archlinux.org/packages/mummer/)

*   **[UGENE](https://en.wikipedia.org/wiki/UGENE "wikipedia:UGENE")** — Application that integrates dozens of well-known biological tools and algorithms, providing both graphical user and command-line interfaces.

	[http://ugene.unipro.ru/](http://ugene.unipro.ru/) || [ugene](https://aur.archlinux.org/packages/ugene/)

#### Molecules

##### Viewers

See also [Wikipedia:List of molecular graphics systems](https://en.wikipedia.org/wiki/List_of_molecular_graphics_systems "wikipedia:List of molecular graphics systems").

*   **[Avogadro](https://en.wikipedia.org/wiki/Avogadro_(software) "wikipedia:Avogadro (software)")** — Editor, viewer and simulator for 3D molecule structures (also supports downloading files from the [Protein Data Bank](https://en.wikipedia.org/wiki/Protein_Data_Bank "wikipedia:Protein Data Bank")).

	[http://avogadro.openmolecules.net/wiki/Main_Page](http://avogadro.openmolecules.net/wiki/Main_Page) || [avogadro](https://www.archlinux.org/packages/?name=avogadro)

*   **BALLView** — Standalone molecular modeling and visualization application, part of the [BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL") framework.

	[http://www.ballview.org/](http://www.ballview.org/) || [ball](https://aur.archlinux.org/packages/ball/)

*   **[Ghemical](https://en.wikipedia.org/wiki/Ghemical "wikipedia:Ghemical")** — Computational chemistry software package used to edit, view and simulate molecular structures.

	[http://bioinformatics.org/ghemical/ghemical/index.html](http://bioinformatics.org/ghemical/ghemical/index.html) || [ghemical](https://aur.archlinux.org/packages/ghemical/)

*   **[PyMOL](https://en.wikipedia.org/wiki/PyMOL "wikipedia:PyMOL")** — Open-source molecular visualization system that can produce high quality 3D images of small molecules and biological macromolecules, such as proteins.

	[http://pymol.org](http://pymol.org) || [pymol](https://www.archlinux.org/packages/?name=pymol)

*   **[RasMol](https://en.wikipedia.org/wiki/RasMol "wikipedia:RasMol")** — Computer program written for molecular graphics visualization intended and used primarily for the depiction and exploration of biological macromolecule structures.

	[http://www.rasmol.org/](http://www.rasmol.org/) || [rasmol](https://aur.archlinux.org/packages/rasmol/)

##### Drawing

*   **[BKChem](https://en.wikipedia.org/wiki/BKchem "wikipedia:BKchem")** — Practical and goodlooking skeletal formula molecule drawing program.

	[http://bkchem.zirael.org/](http://bkchem.zirael.org/) || [bkchem](https://aur.archlinux.org/packages/bkchem/)

*   **[Chemtool](https://en.wikipedia.org/wiki/Chemtool "wikipedia:Chemtool")** — GTK+-based program for drawing chemical structural formulas.

	[http://ruby.chemie.uni-freiburg.de/~martin/chemtool/chemtool.html](http://ruby.chemie.uni-freiburg.de/~martin/chemtool/chemtool.html) || [chemtool](https://www.archlinux.org/packages/?name=chemtool)

*   **EasyChem** — Simple skeletal formula molecule drawing program with a focus on producing press-quality figures.

	[http://easychem.sourceforge.net/](http://easychem.sourceforge.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=easychem)</small>

*   **[Gabedit](https://en.wikipedia.org/wiki/Gabedit "wikipedia:Gabedit")** — Graphical user interface to computational chemistry packages like [GAMESS](https://en.wikipedia.org/wiki/GAMESS_(US) "wikipedia:GAMESS (US)"), [Gaussian](https://en.wikipedia.org/wiki/Gaussian_(software) "wikipedia:Gaussian (software)"), [MOLCAS](https://en.wikipedia.org/wiki/MOLCAS "wikipedia:MOLCAS"), [MOLPRO](https://en.wikipedia.org/wiki/MOLPRO "wikipedia:MOLPRO"), [MPQC](https://en.wikipedia.org/wiki/MPQC "wikipedia:MPQC"), [OpenMopac](https://en.wikipedia.org/wiki/MOPAC "wikipedia:MOPAC"), [Firefly](https://en.wikipedia.org/wiki/PC_GAMESS "wikipedia:PC GAMESS") (previously PC GAMESS) and [Q-Chem](https://en.wikipedia.org/wiki/Q-Chem "wikipedia:Q-Chem").

	[http://gabedit.sourceforge.net/](http://gabedit.sourceforge.net/) || [gabedit](https://aur.archlinux.org/packages/gabedit/)

##### Modeling

*   **[GROMACS](/index.php/GROMACS "GROMACS") (GROningen MAchine for Chemical Simulations)** — Versatile package to perform molecular dynamics, i.e. simulate the Newtonian equations of motion for systems with hundreds to millions of particles.

	[http://www.gromacs.org](http://www.gromacs.org) || [gromacs](https://aur.archlinux.org/packages/gromacs/)

*   **[Quantum ESPRESSO](https://en.wikipedia.org/wiki/Quantum_ESPRESSO "wikipedia:Quantum ESPRESSO")** — Integrated suite of applications for electronic-structure calculations and materials modeling at nanoscale. It is based on density-functional theory, plane waves, and pseudopotentials (both norm-conserving and ultrasoft).

	[http://www.quantum-espresso.org/](http://www.quantum-espresso.org/) || [quantum-espresso](https://aur.archlinux.org/packages/quantum-espresso/)

#### Periodic table

*   **eperiodique** — A simple Periodic Table Of Elements viewer using the EFL.

	[http://eperiodique.sourceforge.net/](http://eperiodique.sourceforge.net/) || [eperiodique](https://aur.archlinux.org/packages/eperiodique/)

*   **gElemental** — Periodic table of the elements with additional information.

	[http://freshmeat.net/projects/gelemental](http://freshmeat.net/projects/gelemental) || [gelemental](https://aur.archlinux.org/packages/gelemental/)

*   **[Kalzium](https://en.wikipedia.org/wiki/Kalzium "wikipedia:Kalzium")** — Periodic table of the elements with molecule editor and equation solver from the [KDE](/index.php/KDE "KDE") desktop.

	[http://edu.kde.org/kalzium/](http://edu.kde.org/kalzium/) || [kdeedu-kalzium](https://www.archlinux.org/packages/?name=kdeedu-kalzium)

#### Biochemistry

*   **[Bioclipse](https://en.wikipedia.org/wiki/Bioclipse "wikipedia:Bioclipse")** — Java-based visual platform for biochemistry that uses the Eclipse Rich Client Platform (RCP).

	[http://www.bioclipse.net/](http://www.bioclipse.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=bioclipse)</small>

#### Image manipulation

*   **[ImageJ](https://en.wikipedia.org/wiki/ImageJ "wikipedia:ImageJ")** — Java-based image processing and analysing program that provides extensibility via plugins and macros. It is widely used in microscopy (e.g. for cell counting).

	[http://rsb.info.nih.gov/ij](http://rsb.info.nih.gov/ij) || [imagej](https://aur.archlinux.org/packages/imagej/)

*   **[Fiji](https://en.wikipedia.org/wiki/FIJI_(software) "wikipedia:FIJI (software)")** — ImageJ distribution (and soon ImageJ2) with a lot of plugins organized into a coherent menu structure.

	[http://fiji.sc](http://fiji.sc) || [fiji-binary](https://aur.archlinux.org/packages/fiji-binary/)

### Astronomy

*   **[Celestia](https://en.wikipedia.org/wiki/Celestia "wikipedia:Celestia")** — 3D astronomy simulation program that allows users to travel through an extensive universe, modeled after reality, at any speed, in any direction and at any time in history.

	[http://www.shatters.net/celestia/](http://www.shatters.net/celestia/) || [celestia](https://www.archlinux.org/packages/?name=celestia)

*   **GIMP Astronomy Plugins** — Set of GIMP plugins for astronomical image processing.

	[http://hennigbuam.de/georg/gimp.html](http://hennigbuam.de/georg/gimp.html) || [gimp-plugin-astronomy](https://aur.archlinux.org/packages/gimp-plugin-astronomy/)

*   **GoQat** — Camera acquisition software, especially for QSI cameras, that provides other features such as autoguiding, focusing help and others.

	[http://canburytech.net/GoQat/](http://canburytech.net/GoQat/) || [goqat](https://aur.archlinux.org/packages/goqat/)

*   **[KStars](https://en.wikipedia.org/wiki/KStars "wikipedia:KStars")** — Planetarium application that provides an accurate graphical simulation of the night sky, from any location on Earth, at any date and time. It is included in KDE Edu.

	[http://edu.kde.org/kstars/](http://edu.kde.org/kstars/) || [kstars](https://www.archlinux.org/packages/?name=kstars)

*   **Open PHD Guiding** — Telescope autoguiding software based on the famous PHD Guiding.

	[http://openphdguiding.org/](http://openphdguiding.org/) || [open-phd-guiding-svn](https://aur.archlinux.org/packages/open-phd-guiding-svn/)

*   **Qastrocam-g2** — Webcam acquisition software for planetary imaging.

	[http://sourceforge.net/projects/qastrocam-g2/](http://sourceforge.net/projects/qastrocam-g2/) || [qastrocam-g2](https://aur.archlinux.org/packages/qastrocam-g2/)

*   **[Skychart / Cartes du Ciel](https://en.wikipedia.org/wiki/Cartes_du_Ciel "wikipedia:Cartes du Ciel")** — Planetarium that maps out and labels most of the constellations, planets, and objects you can see with a telescope. It can also download Digitized Sky Survey Charts and superimpose images over these charts.

	[http://www.ap-i.net/skychart/start/](http://www.ap-i.net/skychart/start/) || [skychart](https://aur.archlinux.org/packages/skychart/)

*   **StarPlot** — 3-dimensional star chart viewer.

	[http://starplot.org/](http://starplot.org/) || [starplot](https://aur.archlinux.org/packages/starplot/)

*   **[Stellarium](https://en.wikipedia.org/wiki/Stellarium_(computer_program) "wikipedia:Stellarium (computer program)")** — Beautiful 3D planetarium that uses OpenGL to render a realistic sky in real time.

	[http://www.stellarium.org/](http://www.stellarium.org/) || [stellarium](https://www.archlinux.org/packages/?name=stellarium)

*   **Where Is M13** — Application to visualize the locations and physical properties of deep sky objects.

	[http://www.thinkastronomy.com/M13/](http://www.thinkastronomy.com/M13/) || [where-is-m13](https://aur.archlinux.org/packages/where-is-m13/)

*   **[XEphem](https://en.wikipedia.org/wiki/XEphem "wikipedia:XEphem")** — Motif-based ephemeris and planetarium program.

	[http://www.clearskyinstitute.com/xephem/xephem.html](http://www.clearskyinstitute.com/xephem/xephem.html) || [xephem](https://aur.archlinux.org/packages/xephem/)

### Physics

#### Electronics

See also [Wikipedia:Comparison of EDA software](https://en.wikipedia.org/wiki/Comparison_of_EDA_software "wikipedia:Comparison of EDA software").

##### Digital logic

Digital logic software are mainly simple educational tools that intended for only designing and simulating logic circuits.

*   **glogic** — An educational graphical logic circuit simulator.

	[https://launchpad.net/glogic](https://launchpad.net/glogic) || [glogic](https://aur.archlinux.org/packages/glogic/)

*   **Logisim** — Educational digital logic design and simulation software, written in Java, officially its development has stopped.

	[http://sourceforge.net/projects/circuit/](http://sourceforge.net/projects/circuit/) || [logisim](https://aur.archlinux.org/packages/logisim/)

*   **Logisim Evolution** — Project which continue the development of the original Logisim with new features, written in Java.

	[https://github.com/reds-heig/logisim-evolution](https://github.com/reds-heig/logisim-evolution) || [logisim-evolution-git](https://aur.archlinux.org/packages/logisim-evolution-git/)

*   **SmartSim** — Simple and beautiful digital logic circuit design and simulation software, mainly target teachers and students, very lightweight and cross platform, GPL licensed, written in Vala.

	[http://smartsim.org.uk](http://smartsim.org.uk) || [smartsim-git](https://aur.archlinux.org/packages/smartsim-git/)

##### HDL

*   **[Altera Design Software](/index.php/Altera_Design_Software "Altera Design Software")** — A set of design tools for Altera's FPGA chips that includes Quartus II and ModelSim-Altera.

	[http://www.altera.com/products/software/sfw-index.jsp](http://www.altera.com/products/software/sfw-index.jsp) || see [Altera Design Software](/index.php/Altera_Design_Software "Altera Design Software")

*   **[Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK")** — FPGA programmable logic design suit.

	[http://www.xilinx.com/products/design-tools/ise-design-suite/ise-webpack.html](http://www.xilinx.com/products/design-tools/ise-design-suite/ise-webpack.html) || see [Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK")

##### MCU IDE

*   **[Arduino](/index.php/Arduino "Arduino")** — Arduino prototyping platform SDK.

	[http://arduino.cc/en/Main/Software](http://arduino.cc/en/Main/Software) || [arduino](https://aur.archlinux.org/packages/arduino/)

##### Schematic capture editor

*   **[gEDA](/index.php/GEDA "GEDA")** — Full suite and toolkit of Electronic Design Automation tools that are used for electrical circuit design, schematic capture, simulation, prototyping, and production.

	[http://www.geda-project.org/](http://www.geda-project.org/) || [geda-gaf](https://www.archlinux.org/packages/?name=geda-gaf)

*   **[KiCAD](https://en.wikipedia.org/wiki/KiCAD "wikipedia:KiCAD")** — Software suite for electronic design automation (EDA) that facilitates the design of schematics for electronic circuits and their conversion to PCB (printed circuit board).

	[http://www.kicad-pcb.org/display/KICAD/KiCad+EDA+Software+Suite](http://www.kicad-pcb.org/display/KICAD/KiCad+EDA+Software+Suite) || [kicad](https://www.archlinux.org/packages/?name=kicad)

*   **[Oregano](https://en.wikipedia.org/wiki/Oregano_(software) "wikipedia:Oregano (software)")** — Graphical software application for schematic capture and simulation of electrical circuits. The actual simulation is done by the [ngspice](https://en.wikipedia.org/wiki/Ngspice "wikipedia:Ngspice") or [Gnucap](https://en.wikipedia.org/wiki/GNU_Circuit_Analysis_Package "wikipedia:GNU Circuit Analysis Package") engines.

	[https://github.com/drahnr/oregano](https://github.com/drahnr/oregano) || [oregano](https://aur.archlinux.org/packages/oregano/)

*   **QElectroTech** — Application used to draw advanced electrical circuits.

	[http://qelectrotech.org/](http://qelectrotech.org/) || [qelectrotech](https://aur.archlinux.org/packages/qelectrotech/)

*   **[Qucs](https://en.wikipedia.org/wiki/Quite_Universal_Circuit_Simulator "wikipedia:Quite Universal Circuit Simulator")** — Electronics circuit simulator application that gives you the ability to set up a circuit with a graphical user interface and simulate its large-signal, small-signal and noise behaviour.

	[http://qucs.sourceforge.net/](http://qucs.sourceforge.net/) || [qucs](https://www.archlinux.org/packages/?name=qucs)

#### Physics simulation

*   **[Code_Aster](https://en.wikipedia.org/wiki/Code_Aster "wikipedia:Code Aster")** — Software package for Civil and Structural Engineering finite element analysis and numeric simulation in structural mechanics.

	[http://www.code-aster.org/V2/spip.php?rubrique2](http://www.code-aster.org/V2/spip.php?rubrique2) || [aster](https://aur.archlinux.org/packages/aster/)

*   **[EPANET](https://en.wikipedia.org/wiki/EPANET "wikipedia:EPANET")** — EPANET performs extended period simulation of the water movement and quality behavior within pressurized pipe networks.

	[http://www.epa.gov/](http://www.epa.gov/) || [epanet2-git](https://aur.archlinux.org/packages/epanet2-git/)

*   **[Step](https://en.wikipedia.org/wiki/Step_(software) "wikipedia:Step (software)")** — Two-dimensional physics simulation engine that is included in the KDE desktop as part of KDE Edu.

	[http://edu.kde.org/step/](http://edu.kde.org/step/) || [step](https://www.archlinux.org/packages/?name=step)

*   **[SWMM](https://en.wikipedia.org/wiki/SWMM "wikipedia:SWMM")** — Storm Water Management Model is a dynamic rainfall-runoff-subsurface runoff simulation model used for simulation of the surface/subsurface hydrology quantity and quality.

	[http://www.epa.gov/](http://www.epa.gov/) || [swmm5-git](https://aur.archlinux.org/packages/swmm5-git/)

#### Unit conversion

*   **ConvertAll** — Unit conversion application that allows one to combine units in any way (e.g. inches per decade), even if it does not make sense.

	[http://convertall.bellz.org/](http://convertall.bellz.org/) || [convertall](https://aur.archlinux.org/packages/convertall/)

*   **Gonvert** — Conversion utility that allows conversion between many units like CGS, Ancient, Imperial with many categories like length, mass, numbers, etc.

	[http://www.unihedron.com/projects/gonvert/](http://www.unihedron.com/projects/gonvert/) || [gonvert](https://aur.archlinux.org/packages/gonvert/)

*   **[Units](https://en.wikipedia.org/wiki/GNU_Units "wikipedia:GNU Units")** — Command-line unit converter and calculator that can handle multiplicative scale changes, nonlinear conversions such as Fahrenheit to Celsius or wire gauge and others.

	[http://www.gnu.org/s/units/](http://www.gnu.org/s/units/) || [units](https://www.archlinux.org/packages/?name=units)

### Geography

*   **GNOME Maps** — A simple map client for GNOME. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Maps](https://wiki.gnome.org/Apps/Maps) || [gnome-maps](https://www.archlinux.org/packages/?name=gnome-maps)

*   **JOSM** — An editor for OpenStreetMap written in Java.

	[http://josm.openstreetmap.de/](http://josm.openstreetmap.de/) || [josm](https://www.archlinux.org/packages/?name=josm)

*   **Marble** — Virtual Globe and World Atlas that can be used to learn more about the Earth. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://www.kde.org/applications/education/marble](https://www.kde.org/applications/education/marble) || [marble](https://www.archlinux.org/packages/?name=marble)

*   **Merkaartor** — OpenStreetMap editor.

	[http://merkaartor.be/](http://merkaartor.be/) || [merkaartor](https://www.archlinux.org/packages/?name=merkaartor)

*   **Viking** — GTK+2 application to manage GPS data.

	[http://viking.sourceforge.net/](http://viking.sourceforge.net/) || [viking](https://www.archlinux.org/packages/?name=viking)

## Others

### Work environment

The default installation of Arch provides Bash as shell interpreter and does not contain any Desktop Environment, therefore forces users to choose one themselves. Most Arch boxes run some X11 Window Manager and/or Desktop Environment, but of course there are still people who prefer doing everyday tasks in bare console.

#### Bootsplash

See also [Wikipedia:Bootsplash](https://en.wikipedia.org/wiki/Bootsplash "wikipedia:Bootsplash").

*   **[Fbsplash](/index.php/Fbsplash "Fbsplash")** — Gentoo implementation as bootsplash program

	[http://wiki.gentoo.org/wiki/Fbsplash](http://wiki.gentoo.org/wiki/Fbsplash) || [fbsplash](https://aur.archlinux.org/packages/fbsplash/)

*   **[Plymouth](/index.php/Plymouth "Plymouth")** — The new graphical boot process for Fedora, replacing the aging Red Hat Graphical Boot

	[http://www.freedesktop.org/wiki/Software/Plymouth/](http://www.freedesktop.org/wiki/Software/Plymouth/) || [plymouth](https://aur.archlinux.org/packages/plymouth/)

*   **[Splashy](/index.php/Splashy "Splashy")** — A graphical boot process designed to replace the aging Bootsplash program

	[https://alioth.debian.org/projects/splashy/](https://alioth.debian.org/projects/splashy/) || [splashy-full](https://aur.archlinux.org/packages/splashy-full/)

#### Command shells

See the main article: [Command-line shell](/index.php/Command-line_shell "Command-line shell").

See also [Wikipedia:Comparison of command shells](https://en.wikipedia.org/wiki/Comparison_of_command_shells "wikipedia:Comparison of command shells").

#### Terminal multiplexers

*   **abduco** — Tool for session attach and detach support which allows a process to run independently from its controlling terminal.

	[http://www.brain-dump.org/projects/abduco/](http://www.brain-dump.org/projects/abduco/) || [abduco](https://aur.archlinux.org/packages/abduco/)

*   **dtach** — Program that emulates the detach feature of [screen](/index.php/Screen "Screen").

	[http://dtach.sourceforge.net/](http://dtach.sourceforge.net/) || [dtach](https://www.archlinux.org/packages/?name=dtach)

*   **[GNU Screen](/index.php/GNU_Screen "GNU Screen")** — Full-screen window manager that multiplexes a physical terminal.

	[https://gnu.org/s/screen/](https://gnu.org/s/screen/) || [screen](https://www.archlinux.org/packages/?name=screen)

*   **[tmux](/index.php/Tmux "Tmux")** — BSD licensed terminal multiplexer.

	[http://tmux.github.io/](http://tmux.github.io/) || [tmux](https://www.archlinux.org/packages/?name=tmux)

*   **[byobu](https://en.wikipedia.org/wiki/Byobu_(software) "wikipedia:Byobu (software)")** — An GPLv3 licensed addon for tmux or screen. It requires a terminal multiplexer installed.

	[http://byobu.co/](http://byobu.co/) || [byobu](https://aur.archlinux.org/packages/byobu/)

#### Desktop environments

See the main article: [Desktop environment#List of desktop environments](/index.php/Desktop_environment#List_of_desktop_environments "Desktop environment").

See also [Wikipedia:Comparison of X Window System desktop environments](https://en.wikipedia.org/wiki/Comparison_of_X_Window_System_desktop_environments "wikipedia:Comparison of X Window System desktop environments").

#### Window managers

##### Console

See also [#Terminal multiplexers](#Terminal_multiplexers), which offer some of the functions of window managers for the console.

*   **dvtm** — [dwm](/index.php/Dwm "Dwm")-style window manager in the console.

	[http://brain-dump.org/projects/dvtm/](http://brain-dump.org/projects/dvtm/) || [dvtm](https://www.archlinux.org/packages/?name=dvtm)

*   **twin** — Text-mode window manager.

	[http://sourceforge.net/projects/twin/](http://sourceforge.net/projects/twin/) || [twin](https://www.archlinux.org/packages/?name=twin)

##### Graphical

See the main article: [Window manager#List of window managers](/index.php/Window_manager#List_of_window_managers "Window manager").

See also [Wikipedia:Comparison of X window managers](https://en.wikipedia.org/wiki/Comparison_of_X_window_managers "wikipedia:Comparison of X window managers").

#### Window tilers

*   **PyTyle3** — An automatic tiler that is compatible with Openbox Multihead with faster action and lower memory footprint.

	[https://github.com/BurntSushi/pytyle3](https://github.com/BurntSushi/pytyle3) || [pytyle3-git](https://aur.archlinux.org/packages/pytyle3-git/)

*   **PyWO** — Allows you to easily organize windows on the desktop using keyboard shortcuts.

	[https://code.google.com/archive/p/pywo/](https://code.google.com/archive/p/pywo/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **QuickTile** — Lightweight standalone alternative to Compiz Grid plugin.

	[http://ssokolow.com/quicktile/](http://ssokolow.com/quicktile/) || [quicktile-git](https://aur.archlinux.org/packages/quicktile-git/)

*   **stiler** — A simple python script to convert any wm to tiling wm.

	[https://bbs.archlinux.org/viewtopic.php?id=64100](https://bbs.archlinux.org/viewtopic.php?id=64100) || [stiler-grid-git](https://aur.archlinux.org/packages/stiler-grid-git/) [stiler](https://aur.archlinux.org/packages/stiler/)

*   **[Tile-windows](/index.php/Tile-windows "Tile-windows")** — Tool for tiling windows horizontally or vertically.

	[http://www.sourcefiles.org/Utilities/Miscellaneous/tile_0.7.4.tar.gz.shtml](http://www.sourcefiles.org/Utilities/Miscellaneous/tile_0.7.4.tar.gz.shtml) || [tile-windows](https://aur.archlinux.org/packages/tile-windows/)

*   **wumwum** — The Window Manager manager. It can turn emwh compliant window managers into a tiling window manager while retaining all initial functionalities.

	[http://wumwum.sourceforge.net/](http://wumwum.sourceforge.net/) || [wumwum](https://aur.archlinux.org/packages/wumwum/)

#### Virtual desktop pagers

See also [Wikipedia:Pager (GUI)](https://en.wikipedia.org/wiki/Pager_(GUI) "wikipedia:Pager (GUI)").

*   **bbpager** — Dockable pager for [blackbox](/index.php/Blackbox "Blackbox") and other window managers.

	[http://bbtools.sourceforge.net/download.php?file=6](http://bbtools.sourceforge.net/download.php?file=6) || [bbpager](https://www.archlinux.org/packages/?name=bbpager)

*   **fbpager** — Virtual desktop pager for fluxbox.

	[http://www.fluxbox.org/fbpager](http://www.fluxbox.org/fbpager) || [fbpager-git](https://aur.archlinux.org/packages/fbpager-git/)

*   **IPager** — A configurable pager with transparency, originally developed for Fluxbox.

	[http://useperl.ru/ipager/index.en.html](http://useperl.ru/ipager/index.en.html) || [ipager](https://aur.archlinux.org/packages/ipager/)

*   **Neap** — An non-intrusive and light pager that runs in the notification area of your panel.

	[https://github.com/vzxwco/neap](https://github.com/vzxwco/neap) || [neap](https://aur.archlinux.org/packages/neap/)

*   **Netwmpager** — A NetWM/EWMH compatible pager.

	[http://sourceforge.net/projects/sf-xpaint/files/netwmpager/](http://sourceforge.net/projects/sf-xpaint/files/netwmpager/) || [netwmpager](https://aur.archlinux.org/packages/netwmpager/)

*   **obpager** — Pager for [Openbox](/index.php/Openbox "Openbox") writen in C++.

	[http://obpager.sourceforge.net/](http://obpager.sourceforge.net/) || [obpager](https://aur.archlinux.org/packages/obpager/)

*   **Pager** — A highly configurable pager compatible with Openbox Multihead.

	[https://github.com/BurntSushi/pager-multihead](https://github.com/BurntSushi/pager-multihead) || [pager-multihead-git](https://aur.archlinux.org/packages/pager-multihead-git/)

#### Support applications

##### Login managers

See the main article: [Display manager#List of display managers](/index.php/Display_manager#List_of_display_managers "Display manager").

##### Composite managers

See the main article: [Xorg#List of composite managers](/index.php/Xorg#List_of_composite_managers "Xorg").

##### Taskbars / panels / docks

*   **[Avant Window Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")** — Lightweight dock which sits at the bottom of the screen.

	[http://launchpad.net/awn](http://launchpad.net/awn) || [avant-window-navigator](https://aur.archlinux.org/packages/avant-window-navigator/)

*   **[Bmpanel](/index.php/Bmpanel "Bmpanel")** — Lightweight, NETWM compliant panel.

	[https://github.com/nsf/bmpanel2](https://github.com/nsf/bmpanel2) || [bmpanel2](https://aur.archlinux.org/packages/bmpanel2/)

*   **[Cairo-Dock](/index.php/Cairo-Dock "Cairo-Dock")** — Highly customizable dock and launcher application.

	[http://www.glx-dock.org/](http://www.glx-dock.org/) || [cairo-dock](https://www.archlinux.org/packages/?name=cairo-dock)

*   **Daisy** — KDE Plasma widget which acts as a dock.

	[http://cdlszm.org/](http://cdlszm.org/) || [kdeplasma-applets-daisy](https://aur.archlinux.org/packages/kdeplasma-applets-daisy/)

*   **Docker** — Docking application which acts as a system tray.

	[http://icculus.org/openbox/2/docker/](http://icculus.org/openbox/2/docker/) || [docker-tray](https://aur.archlinux.org/packages/docker-tray/)

*   **[Docky](https://en.wikipedia.org/wiki/Docky "wikipedia:Docky")** — Full fledged dock application that makes opening common applications and managing windows easier and quicker.

	[http://wiki.go-docky.com/](http://wiki.go-docky.com/) || [docky](https://www.archlinux.org/packages/?name=docky)

*   **[fbpanel](/index.php/Fbpanel "Fbpanel")** — Lightweight, NETWM compliant desktop panel.

	[http://fbpanel.sourceforge.net/](http://fbpanel.sourceforge.net/) || [fbpanel](https://www.archlinux.org/packages/?name=fbpanel)

*   **[GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")** — Panel included in the [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") desktop.

	[https://wiki.gnome.org/Projects/GnomePanel](https://wiki.gnome.org/Projects/GnomePanel) || [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)

*   **KoolDock** — KDE3 docker with great effects that tries to resemble the OS X dock.

	[http://sourceforge.net/projects/kooldock](http://sourceforge.net/projects/kooldock) || [kooldock-svn](https://aur.archlinux.org/packages/kooldock-svn/)

*   **LXPanel** — Lightweight X11 desktop panel and part of the LXDE desktop.

	[http://lxde.org/lxpanel](http://lxde.org/lxpanel) || [lxpanel](https://www.archlinux.org/packages/?name=lxpanel)

*   **MATE Panel** — Panel included in the [MATE](/index.php/MATE "MATE") desktop.

	[https://github.com/mate-desktop/mate-panel/](https://github.com/mate-desktop/mate-panel/) || [mate-panel](https://www.archlinux.org/packages/?name=mate-panel)

*   **PerlPanel** — The ideal accompaniment to a light-weight Window Manager such as OpenBox, or a desktop-drawing program like iDesk.

	[http://savannah.nongnu.org/projects/perlpanel](http://savannah.nongnu.org/projects/perlpanel) || [perlpanel](https://www.archlinux.org/packages/?name=perlpanel)

*   **[Plank](/index.php/Plank "Plank")** — Elegant, simple, clean dock from [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

	[https://launchpad.net/plank](https://launchpad.net/plank) || [plank](https://www.archlinux.org/packages/?name=plank)

*   **[PyPanel](/index.php/PyPanel "PyPanel")** — Lightweight panel/taskbar written in Python and C.

	[http://pypanel.sourceforge.net/](http://pypanel.sourceforge.net/) || [pypanel](https://www.archlinux.org/packages/?name=pypanel)

*   **qtpanel** — Project to create useful and beautiful panel in Qt.

	[https://gitorious.org/qtpanel/qtpanel](https://gitorious.org/qtpanel/qtpanel) || [qtpanel-git](https://aur.archlinux.org/packages/qtpanel-git/)

*   **[Stalonetray](/index.php/Stalonetray "Stalonetray")** — Stand-alone system tray.

	[http://stalonetray.sourceforge.net/](http://stalonetray.sourceforge.net/) || [stalonetray](https://www.archlinux.org/packages/?name=stalonetray)

*   **[Tint2](/index.php/Tint2 "Tint2")** — Simple panel/taskbar developed specifically for Openbox.

	[https://gitlab.com/o9000/tint2](https://gitlab.com/o9000/tint2) || [tint2](https://www.archlinux.org/packages/?name=tint2)

*   **Trayer** — Lightweight GTK+-based systray.

	[https://gna.org/projects/fvwm-crystal/](https://gna.org/projects/fvwm-crystal/) || [trayer](https://www.archlinux.org/packages/?name=trayer)

*   **wbar** — Quick launch bar developed with speed in mind.

	[http://freecode.com/projects/wbar/](http://freecode.com/projects/wbar/) || [wbar](https://www.archlinux.org/packages/?name=wbar)

*   **Xfce Panel** — Panel included in the [Xfce](/index.php/Xfce "Xfce") desktop.

	[http://docs.xfce.org/xfce/xfce4-panel/start](http://docs.xfce.org/xfce/xfce4-panel/start) || [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)

##### Application launchers

See also [Wikipedia:Comparison of desktop application launchers](https://en.wikipedia.org/wiki/Comparison_of_desktop_application_launchers "wikipedia:Comparison of desktop application launchers").

*   **ADeskBar** — Easy, simple and unobtrusive application launcher for Openbox.

	[http://adeskbar.tuxfamily.org/](http://adeskbar.tuxfamily.org/) || [adeskbar](https://aur.archlinux.org/packages/adeskbar/)

*   **Albert** — An application launcher inspired by Alfred.

	[https://github.com/manuelschneid3r/albert](https://github.com/manuelschneid3r/albert) || [albert](https://aur.archlinux.org/packages/albert/)

*   **Bashrun2** — Provides a different, barebones approach to a run dialog, using a specialized Bash session within a small xterm window.

	[http://henning-bekel.de/bashrun2/](http://henning-bekel.de/bashrun2/) || [bashrun2](https://aur.archlinux.org/packages/bashrun2/)

*   **[dmenu](/index.php/Dmenu "Dmenu")** — Fast and lightweight dynamic menu for X which is also useful as an application launcher.

	[http://tools.suckless.org/dmenu/](http://tools.suckless.org/dmenu/) || [dmenu](https://www.archlinux.org/packages/?name=dmenu)

*   **dmenu-extended** — An extension to *dmenu* for quickly opening files and folders.

	[https://github.com/markjones112358/dmenu-extended](https://github.com/markjones112358/dmenu-extended) || [dmenu-extended](https://aur.archlinux.org/packages/dmenu-extended/)

*   **dmenu-launch** — Simple *dmenu*-based application launcher. Launches binaries and XDG shortcuts.

	[https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch](https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch) || [dmenu-launch](https://aur.archlinux.org/packages/dmenu-launch/)

*   **dswitcher** — *dmenu*-based window switcher that works regardless of workspace or minimization.

	[https://github.com/Antithesisx/dswitcher](https://github.com/Antithesisx/dswitcher) || [dswitcher-git](https://aur.archlinux.org/packages/dswitcher-git/)

*   **Fehlstart** — Small GTK+-based application launcher.

	[https://gitlab.com/fehlstart/fehlstart](https://gitlab.com/fehlstart/fehlstart) || [fehlstart-git](https://aur.archlinux.org/packages/fehlstart-git/)

*   **[Gmrun](/index.php/Gmrun "Gmrun")** — Lightweight GTK+-based application launcher, with the ability to run programs inside a terminal and other handy features.

	[http://sourceforge.net/projects/gmrun/](http://sourceforge.net/projects/gmrun/) || [gmrun](https://www.archlinux.org/packages/?name=gmrun)

*   **[GNOME Do](https://en.wikipedia.org/wiki/GNOME_Do with many plugins, originally developed for the GNOME desktop.

	[http://do.cooperteam.net/](http://do.cooperteam.net/) || [gnome-do](https://www.archlinux.org/packages/?name=gnome-do)

*   **j4-dmenu-desktop** — Very fast dmenu application launcher.

	[https://github.com/enkore/j4-dmenu-desktop](https://github.com/enkore/j4-dmenu-desktop) || [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/)

*   **higgins** — A desktop agnostic application launcher, file finder, calculator and more. Plugin based and freely and easily extendable via user-written plugins

	[https://github.com/kokoko3k/higgins](https://github.com/kokoko3k/higgins) || [higgins-git](https://aur.archlinux.org/packages/higgins-git/)

*   **Kupfer** — Convenient command and access tool for the GNOME desktop that can launch applications, open documents and access different types of objects and act on them.

	[https://wiki.gnome.org/Apps/Kupfer](https://wiki.gnome.org/Apps/Kupfer) || [kupfer](https://aur.archlinux.org/packages/kupfer/)

*   **[Launchy](https://en.wikipedia.org/wiki/Launchy "wikipedia:Launchy")** — Very popular cross-platform application launcher with a plugin-based system used to provide extra functionality.

	[http://www.launchy.net/](http://www.launchy.net/) || [launchy](https://www.archlinux.org/packages/?name=launchy)

*   **Lighthouse** — A simple scriptable popup dialog to run on X.

	[https://github.com/emgram769/lighthouse](https://github.com/emgram769/lighthouse) || [lighthouse-git](https://aur.archlinux.org/packages/lighthouse-git/)

*   **[rofi](/index.php/Rofi "Rofi")** — A popup window switcher roughly based on superswitcher, requiring only xlib and pango.

	[http://davedavenport.github.io/rofi/](http://davedavenport.github.io/rofi/) || [rofi](https://www.archlinux.org/packages/?name=rofi)

*   **slingshot** — An application launcher has a clear look, part of [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

	[https://launchpad.net/slingshot](https://launchpad.net/slingshot) || [slingshot-launcher](https://aur.archlinux.org/packages/slingshot-launcher/)

*   **Runa** — Fast and light dmenu-driven application launcher, suitable for use standalone, integrated into file manager context menus, or as an 'xdg-open' replacement. Favourite applications can also be configured.

	[http://appstogo.mcfadzean.org.uk/linux.html#runa](http://appstogo.mcfadzean.org.uk/linux.html#runa) || [runa](https://aur.archlinux.org/packages/runa/)

*   **Synapse** — Synapse is a semantic launcher written in Vala that you can use to start applications as well as find and access relevant documents and files by making use of the Zeitgeist engine.

	[https://launchpad.net/synapse-project](https://launchpad.net/synapse-project) || [synapse](https://www.archlinux.org/packages/?name=synapse)

*   **Whippet** — A launcher and xdg-open replacement for control freaks. Opens files and URLs with applications associated by name and/or mimetype. Applications and associations may be customized using an SQLite database. Uses dmenu to manage its menus.

	[http://appstogo.mcfadzean.org.uk/linux.html#whippet](http://appstogo.mcfadzean.org.uk/linux.html#whippet) || [whippet](https://aur.archlinux.org/packages/whippet/)

*   **xboomx** — Light *dmenu* wrapper that reorders commands based on popularity, written in Python.

	[https://bitbucket.org/dehun/xboomx](https://bitbucket.org/dehun/xboomx) || [xboomx](https://aur.archlinux.org/packages/xboomx/)

*   **xfce4-appfinder** — An eazy-to-use application launcher from Xfce.

	[http://docs.xfce.org/xfce/xfce4-appfinder/start](http://docs.xfce.org/xfce/xfce4-appfinder/start) || [xfce4-appfinder](https://www.archlinux.org/packages/?name=xfce4-appfinder)

*   **Yeganesh** — Light *dmenu* wrapper that reorders commands based on popularity, written in Haskell.

	[http://dmwit.com/yeganesh](http://dmwit.com/yeganesh) || [yeganesh](https://aur.archlinux.org/packages/yeganesh/)

##### Logout dialogue

A few simple shutdown managers are available:

*   **exitx-polkit** — A GTK logout dialog for Openbox with PolicyKit support.

	[https://github.com/z0id/exitx-polkit](https://github.com/z0id/exitx-polkit) || [exitx-polkit-git](https://aur.archlinux.org/packages/exitx-polkit-git/)

*   **exitx-systemd** — A GTK logout dialog for Openbox with systemd support.

	[https://github.com/z0id/exitx-systemd](https://github.com/z0id/exitx-systemd) || [exitx-systemd-git](https://aur.archlinux.org/packages/exitx-systemd-git/)

*   **oblogout** — A graphical logout script for [Openbox](/index.php/Openbox "Openbox") that may be used with other WMs.

	[https://launchpad.net/oblogout](https://launchpad.net/oblogout) || [oblogout](https://www.archlinux.org/packages/?name=oblogout)

*   **obshutdown** — A great GTK/Cairo based shutdown manager for Openbox and other window managers.

	[https://github.com/panjandrum/obshutdown](https://github.com/panjandrum/obshutdown) || [obshutdown](https://aur.archlinux.org/packages/obshutdown/)

#### Accessibility

##### Screen reading

*   **Mimic** — Text-to-speech voice synthesis from the Mycroft project

	[https://mimic.mycroft.ai/](https://mimic.mycroft.ai/) || [mimic-git](https://aur.archlinux.org/packages/mimic-git/)

*   **Orca** — Screen reader for individuals who are blind or visually impaired

	[http://www.gnome.org/projects/orca](http://www.gnome.org/projects/orca) || [orca](https://www.archlinux.org/packages/?name=orca)

*   **[Simple Orca Plugin System](/index.php/Simple_Orca_Plugin_System "Simple Orca Plugin System")** — Plug-in extension for the Orca screen reader

	[https://stormdragon.tk/orca-plugins/index.php](https://stormdragon.tk/orca-plugins/index.php) || [simpleorcapluginsystem-git](https://aur.archlinux.org/packages/simpleorcapluginsystem-git/)

##### Speech recognition

See the main article [Speech recognition](/index.php/Speech_recognition "Speech recognition") for applications.

### Finance

See also [Wikipedia:Comparison of accounting software](https://en.wikipedia.org/wiki/Comparison_of_accounting_software "wikipedia:Comparison of accounting software").

*   **Beancount** — Beancount is a Ledger-like CLI double-entry accounting system. It is written in Python and has more features, like multi-currency support, than Ledger.

	[http://furius.ca/beancount/](http://furius.ca/beancount/) || [beancount-hg](https://aur.archlinux.org/packages/beancount-hg/)

*   **esniper** — Simple, lightweight tool for [sniping](https://en.wikipedia.org/wiki/Auction_sniping "wikipedia:Auction sniping") eBay auctions.

	[http://esniper.sourceforge.net/](http://esniper.sourceforge.net/) || [esniper](https://aur.archlinux.org/packages/esniper/)

*   **[GnuCash](https://en.wikipedia.org/wiki/GnuCash "wikipedia:GnuCash")** — Financial application that implements a double-entry book-keeping system with features for small business accounting.

	[http://www.gnucash.org/](http://www.gnucash.org/) || [gnucash](https://www.archlinux.org/packages/?name=gnucash)

*   **Grisbi** — Personal finance system which manages third party, expenditure and receipt categories, as well as budgetary lines, financial years, and other information that makes it suitable for associations.

	[http://www.grisbi.org/](http://www.grisbi.org/) || [grisbi](https://aur.archlinux.org/packages/grisbi/)

*   **[HomeBank](https://en.wikipedia.org/wiki/HomeBank "wikipedia:HomeBank")** — Easy to use finance manager that can analyse your personal finance in detail using powerful filtering tools and graphs.

	[http://homebank.free.fr/](http://homebank.free.fr/) || [homebank](https://www.archlinux.org/packages/?name=homebank)

*   **[KMyMoney](https://en.wikipedia.org/wiki/KMyMoney "wikipedia:KMyMoney")** — Personal finance manager that operates in a similar way to [Microsoft Money](https://en.wikipedia.org/wiki/Microsoft_Money "wikipedia:Microsoft Money"). It supports different account types, categorisation of expenses and incomes, reconciliation of bank accounts and import/export to the “QIF” file format.

	[http://kmymoney2.sourceforge.net/index-home.html](http://kmymoney2.sourceforge.net/index-home.html) || [kmymoney](https://www.archlinux.org/packages/?name=kmymoney)

*   **Ledger** — Ledger is a powerful, double-entry accounting system that is accessed from the UNIX command-line.

	[http://ledger-cli.org/](http://ledger-cli.org/) || [ledger](https://aur.archlinux.org/packages/ledger/)

*   **hledger** — An accounting program for tracking money, time, or any other commodity, using double-entry accounting and a simple, editable file format. hledger is inspired by and largely compatible with ledger.

	[http://hledger.org/](http://hledger.org/) || [hledger-git](https://aur.archlinux.org/packages/hledger-git/)

*   **Moneychanger** — An intuitive QT/C++ system tray client for *Open-Transactions*

	[https://github.com/Open-Transactions/Moneychanger](https://github.com/Open-Transactions/Moneychanger) || [moneychanger-git](https://aur.archlinux.org/packages/moneychanger-git/)

*   **Manager Accounting** — Manager is free accounting software for small business.

	[http://www.manager.io/](http://www.manager.io/) || [manager-accounting](https://aur.archlinux.org/packages/manager-accounting/)

*   **Money Manager EX** — An easy-to-use personal finance suite

	[http://www.moneymanagerex.org/](http://www.moneymanagerex.org/) || [moneymanagerex](https://www.archlinux.org/packages/?name=moneymanagerex)

*   **Skrooge** — Personal finances manager for the KDE desktop.

	[http://skrooge.org/](http://skrooge.org/) || [skrooge](https://www.archlinux.org/packages/?name=skrooge)

*   **openerp** — Open source erp system purely in python.

	[http://openerp.com/](http://openerp.com/) || [openerp](https://aur.archlinux.org/packages/openerp/)

*   **Open-Transactions** — A financial cryptography library used for issuing currencies, stock, paying dividends, creating asset accounts, sending/receiving digital cash, trading on markets and escrow.

	[https://github.com/Open-Transactions/Open-Transactions](https://github.com/Open-Transactions/Open-Transactions) || [open-transactions-git](https://aur.archlinux.org/packages/open-transactions-git/)

### Flashcards

*   **[Anki](/index.php/Anki "Anki")** — Anki is a program which makes remembering things easy.

	[http://ankisrs.net/](http://ankisrs.net/) || [anki](https://www.archlinux.org/packages/?name=anki)

*   **iGNUit** — Memorization aid based on the Leitner flashcard system.

	[http://homepages.ihug.co.nz/~trmusson/programs.html#ignuit](http://homepages.ihug.co.nz/~trmusson/programs.html#ignuit) || [ignuit](https://aur.archlinux.org/packages/ignuit/)

*   **[Mnemosyne](/index.php/Mnemosyne "Mnemosyne")** — Free flash-card tool which optimizes your learning process.

	[http://mnemosyne-proj.org/](http://mnemosyne-proj.org/) || [mnemosyne](https://aur.archlinux.org/packages/mnemosyne/)

### Time management

#### Console

*   **Calcurse** — Text-based ncurses calendar and scheduling system.

	[http://calcurse.org/](http://calcurse.org/) || [calcurse](https://www.archlinux.org/packages/?name=calcurse)

*   **Doneyet** — Ncurses-based hierarchical To-do list manager written in C++.

	[https://github.com/gtaubman/doneyet](https://github.com/gtaubman/doneyet) || [doneyet](https://aur.archlinux.org/packages/doneyet/)

*   **Pal** — Very lightweight calendar with both interactive and non-interactive interfaces.

	[http://palcal.sourceforge.net/](http://palcal.sourceforge.net/) || [pal](https://aur.archlinux.org/packages/pal/)

*   **[Remind](/index.php/Remind "Remind")** — Highly sophisticated text-based calendaring and notification system.

	[http://roaringpenguin.com/products/remind](http://roaringpenguin.com/products/remind) || [remind](https://www.archlinux.org/packages/?name=remind)

*   **[Taskwarrior](https://en.wikipedia.org/wiki/Taskwarrior "wikipedia:Taskwarrior")** — Command-line To-do list application with support for lua customization and more.

	[http://taskwarrior.org/](http://taskwarrior.org/) || [task](https://www.archlinux.org/packages/?name=task)

*   **Todo.txt** — Small command-line To-do manager.

	[http://ginatrapani.github.com/todo.txt-cli/](http://ginatrapani.github.com/todo.txt-cli/) || [todotxt](https://aur.archlinux.org/packages/todotxt/)

*   **TuDu** — Ncurses-based hierarchical To-do list manager with vim-like keybindings.

	[http://code.meskio.net/tudu/](http://code.meskio.net/tudu/) || [tudu](https://aur.archlinux.org/packages/tudu/)

*   **When** — Simple personal calendar program.

	[http://lightandmatter.com/when/when.html](http://lightandmatter.com/when/when.html) || [when](https://www.archlinux.org/packages/?name=when)

*   **Wyrd** — Text-based front-end to Remind, a calendar and alarm program used on UNIX and Linux computers.

	[http://pessimization.com/software/wyrd/](http://pessimization.com/software/wyrd/) || [wyrd](https://www.archlinux.org/packages/?name=wyrd)

*   **mail2rem** — Small script for importing *.ics calendars from Maildir to Remind calendar.

	[https://github.com/esovetkin/mail2rem](https://github.com/esovetkin/mail2rem) || [mail2rem-git](https://aur.archlinux.org/packages/mail2rem-git/)

*   **DevTodo** — Is a small command line application for maintaining lists of tasks.

	[http://swapoff.org/devtodo1.html](http://swapoff.org/devtodo1.html) || [devtodo](https://aur.archlinux.org/packages/devtodo/)

#### Graphical

*   **Calendar** — Calendar application for GNOME.

	[https://wiki.gnome.org/Apps/Calendar](https://wiki.gnome.org/Apps/Calendar) || [gnome-calendar](https://www.archlinux.org/packages/?name=gnome-calendar)

*   **Clocks** — Clocks application for GNOME.

	[https://wiki.gnome.org/Apps/Clocks](https://wiki.gnome.org/Apps/Clocks) || [gnome-clocks](https://www.archlinux.org/packages/?name=gnome-clocks)

*   **Day Planner** — Program designed to help you easily plan and manage your time. It can manage appointments, birthdays and more.

	[http://www.day-planner.org/](http://www.day-planner.org/) || [dayplanner](https://aur.archlinux.org/packages/dayplanner/)

*   **etm (Event and Task Manager)** — Simple application with a "Getting Things Done!" approach to handling events, tasks, activities, reminders and projects.

	[http://duke.edu/~dgraham/ETM/](http://duke.edu/~dgraham/ETM/) || [etm](https://aur.archlinux.org/packages/etm/)

*   **etmtk (Event and Task Manager second generation)** — Simple application with a "Getting Things Done!" approach to handling events, tasks, activities, reminders and projects. A newer version of etm.

	[http://duke.edu/~dgraham/ETMtk/](http://duke.edu/~dgraham/ETMtk/) || [etmtk](https://aur.archlinux.org/packages/etmtk/)

*   **Glista** — Simple GTK+ To-do list manager with notes support.

	[http://arr.gr/glista/](http://arr.gr/glista/) || [glista](https://aur.archlinux.org/packages/glista/)

*   **GNOME Break Timer** — Keeps track of how much you are using the computer, and it reminds you to take regular breaks.

	[https://wiki.gnome.org/Apps/GnomeBreakTimer](https://wiki.gnome.org/Apps/GnomeBreakTimer) || [gnome-break-timer](https://aur.archlinux.org/packages/gnome-break-timer/)

*   **GTG (Getting Things GNOME!)** — Personal tasks and To-do list items organizer for the GNOME desktop.

	[http://gtgnome.net/](http://gtgnome.net/) || [gtg](https://aur.archlinux.org/packages/gtg/)

*   **Hamster** — Time tracking application that helps you to keep track on how much time you have spent during the day on activities you choose to track.

	[http://projecthamster.org/](http://projecthamster.org/) || [hamster-time-tracker](https://www.archlinux.org/packages/?name=hamster-time-tracker)

*   **[KOrganizer](https://en.wikipedia.org/wiki/Kontact#Organizer "wikipedia:Kontact")** — Calendar and scheduling program, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[http://www.kde.org/applications/office/korganizer/](http://www.kde.org/applications/office/korganizer/) || [korganizer](https://www.archlinux.org/packages/?name=korganizer)

*   **[Lightning](https://en.wikipedia.org/wiki/Lightning_(software) "wikipedia:Lightning (software)")** — Extension to Mozilla Thunderbird that provides calendar and task support.

	[http://www.mozilla.org/projects/calendar/lightning/](http://www.mozilla.org/projects/calendar/lightning/) || [lightning](https://aur.archlinux.org/packages/lightning/)

*   **Orage** — GTK+ calendar and task manager often seen integrated with Xfce.

	[http://www.xfce.org/projects](http://www.xfce.org/projects) || [orage](https://www.archlinux.org/packages/?name=orage)

*   **Osmo** — GTK+ personal organizer, which includes calendar, tasks manager and address book modules.

	[http://clayo.org/osmo/](http://clayo.org/osmo/) || [osmo](https://www.archlinux.org/packages/?name=osmo)

*   **Outspline** — Extensible outliner with advanced time management features, supporting events with complex recurrence schemes.

	[https://kynikos.github.io/outspline/](https://kynikos.github.io/outspline/) || [outspline](https://aur.archlinux.org/packages/outspline/)

*   **QTodoTxt** — A cross-platform UI client for `todo.txt` files (see [project's page](http://todotxt.com/))

	[https://github.com/mNantern/QTodoTxt](https://github.com/mNantern/QTodoTxt) || [qtodotxt](https://aur.archlinux.org/packages/qtodotxt/) [qtodotxt-git](https://aur.archlinux.org/packages/qtodotxt-git/)

*   **Rachota** — Portable time tracker for personal projects.

	[http://rachota.sourceforge.net/](http://rachota.sourceforge.net/) || [rachota](https://aur.archlinux.org/packages/rachota/)

*   **Task Coach** — Simple open source To-do manager to manage personal tasks and To-do lists.

	[http://taskcoach.org](http://taskcoach.org) || [taskcoach](https://aur.archlinux.org/packages/taskcoach/)

*   **[Tasque](https://en.wikipedia.org/wiki/Tasque_(software) "wikipedia:Tasque (software)")** — Easy quick task management app written in C Sharp.

	[https://wiki.gnome.org/Apps/Tasque](https://wiki.gnome.org/Apps/Tasque) || [tasque](https://www.archlinux.org/packages/?name=tasque)

*   **Tider** — Lightweight time tracking application (GTK+)

	[http://pusto.org/en/tider/](http://pusto.org/en/tider/) || [tider-git](https://aur.archlinux.org/packages/tider-git/)

*   **TkRemind** — Sophisticated calendar and alarm program.

	[http://www.roaringpenguin.com/products/remind](http://www.roaringpenguin.com/products/remind) || [remind](https://www.archlinux.org/packages/?name=remind)

*   **[Workrave](https://en.wikipedia.org/wiki/Workrave "wikipedia:Workrave")** — A tool to help RSI.

	[http://www.workrave.org/](http://www.workrave.org/) || [workrave](https://www.archlinux.org/packages/?name=workrave)

*   **wxRemind** — Python text and graphical frontend to Remind.

	[http://duke.edu/~dgraham/wxRemind/](http://duke.edu/~dgraham/wxRemind/) || [wxremind](https://aur.archlinux.org/packages/wxremind/)

### Emulators

An emulator is a program which serves to replicate the functions of another platform or system so as to allow applications and games to be run in environments they were not programmed for.

**Note:** For possibly more up to date selection of emulators, try checking the [AUR 'emulators' category](https://aur.archlinux.org/packages.php?O=0&K=&do_Search=Go&detail=1&L=0&C=5&SeB=nd&SB=n&SO=a&PP=25)

**Warning:** Owning a high-level emulator is not illegal, but distribution of any type of copyrighted ROMs and unauthorized emulation (without written permission of the copyright holder allowing the user to do so) are **illegal**. Consequently, Arch Linux does not distribute this copyrighted content, including game ROMs and ripped console BIOSs. You are fully responsible for whatever usage of the emulators obtained from the [official repositories](/index.php/Official_repositories "Official repositories") or the [Arch User Repository](/index.php/Arch_User_Repository "Arch User Repository") you make, as well as any legal repercussion that result. Arch Linux bears no responsibility at all.

#### Consoles

See also [Wikipedia:List of video game console emulators](https://en.wikipedia.org/wiki/List_of_video_game_console_emulators "wikipedia:List of video game console emulators").

*   **Citra** — Nintendo 3DS emulator.

	[http://citra-emu.org/](http://citra-emu.org/) || [citra-git](https://aur.archlinux.org/packages/citra-git/)

*   **DeSmuME** — Nintendo DS emulator.

	[http://desmume.org/](http://desmume.org/) || [desmume](https://www.archlinux.org/packages/?name=desmume)

*   **[Dolphin](/index.php/Dolphin_emulator "Dolphin emulator")** — Very capable GameCube and Wii emulator.

	[http://dolphin-emu.org/](http://dolphin-emu.org/) || [dolphin-emu](https://www.archlinux.org/packages/?name=dolphin-emu)

*   **epsxe** — Emulator for the PlayStation video game console for x86-based PC hardware.

	[http://www.epsxe.com/](http://www.epsxe.com/) || [epsxe](https://aur.archlinux.org/packages/epsxe/)

*   **fakenes** — NES (Nintendo Famicom) emulator.

	[http://fakenes.sourceforge.net/](http://fakenes.sourceforge.net/) || [fakenes](https://aur.archlinux.org/packages/fakenes/)

*   **FCEUX** — NTSC and PAL 8 bit Nintendo/Famicom emulator that is an evolution of the original FCE Ultra emulator. It is accurate, compatible and actively maintained.

	[http://fceux.com/](http://fceux.com/) || [fceux](https://www.archlinux.org/packages/?name=fceux)

*   **Gens2** — Emulator for Sega Genesis, Sega CD and 32X that is written in assembly language and no longer actively developed.

*   activate OpenGL, set video resolution per custom to 1024x600 for streched full-screen or 800x600 for non-streched;
*   use "Normal" renderer, I couldn't find a visible advantage with the other ones.

	[http://www.gens.me/](http://www.gens.me/) || [gens](https://www.archlinux.org/packages/?name=gens)

*   **Gens-GS** — Gens2, rewritten in C++, combining features from various Gens forks.

	[http://segaretro.org/Gens/GS](http://segaretro.org/Gens/GS) || [gens-gs](https://www.archlinux.org/packages/?name=gens-gs)

*   **gngeo** — Command-line NeoGeo emulator.

	[http://gngeo.googlecode.com](http://gngeo.googlecode.com) || [gngeo](https://aur.archlinux.org/packages/gngeo/)

*   **higan** — Multisystem emulator focusing on accuracy, supporting SNES, NES, GB, GBC, GBA.

	[https://code.google.com/archive/p/higan/](https://code.google.com/archive/p/higan/) || [higan](https://www.archlinux.org/packages/?name=higan)

*   **mednafen** — Command line driven multi system emulator.

	[http://mednafen.sourceforge.net/](http://mednafen.sourceforge.net/) || [mednafen](https://www.archlinux.org/packages/?name=mednafen)

*   **Mupen64Plus** — Highly compatible Nintendo 64 emulator with plugin system.

	[http://www.mupen64plus.org/](http://www.mupen64plus.org/) || [mupen64plus](https://www.archlinux.org/packages/?name=mupen64plus) or a graphical front-end, such as [m64py](https://aur.archlinux.org/packages/m64py/) or [cutemupen](https://aur.archlinux.org/packages/cutemupen/).

*   **pSX** — A not plugin-based PlayStation emulator with fairly high compatibility.

	[http://psxemulator.gazaxian.com/](http://psxemulator.gazaxian.com/) || [psx](https://aur.archlinux.org/packages/psx/)

*   **PCSXR** — PlayStation emulator; Debian fork of the abandoned original PCSX

	[http://pcsxr.codeplex.com/](http://pcsxr.codeplex.com/) || [pcsxr](https://www.archlinux.org/packages/?name=pcsxr)

*   **PCSX2** — PlayStation 2 emulator. It is still being maintained and developed. It requires BIOS files.

	[http://www.pcsx2.net/](http://www.pcsx2.net/) || [pcsx2](https://www.archlinux.org/packages/?name=pcsx2)

*   **PPSSPP** — PlayStation Portable emulator.

	[http://ppsspp.org/](http://ppsspp.org/) || [ppsspp](https://www.archlinux.org/packages/?name=ppsspp)

*   **snes-9x** — Portable, freeware Super Nintendo Entertainment System (SNES) emulator.

	[http://www.snes9x.com/](http://www.snes9x.com/) || [snes9x](https://www.archlinux.org/packages/?name=snes9x)

*   **[Visual Boy Advance](/index.php/Visual_Boy_Advance "Visual Boy Advance")** — Game Boy emulator with Game Boy Advance, Game Boy Color, and Super Game Boy support.

	[http://vba.ngemu.com/](http://vba.ngemu.com/) || [vbam-gtk](https://www.archlinux.org/packages/?name=vbam-gtk)

*   **ZSNES** — Highly compatible Super Nintendo emulator.

	[http://www.zsnes.com/](http://www.zsnes.com/) || [zsnes](https://www.archlinux.org/packages/?name=zsnes)

#### Other

*   **DOSBox** — Open-source DOS emulator which primarily focuses on running DOS Games.

	[http://www.dosbox.com/](http://www.dosbox.com/) || [dosbox](https://www.archlinux.org/packages/?name=dosbox)

*   **DOSEmu** — Open-source DOS emulator.

	[http://www.dosemu.org/](http://www.dosemu.org/) || [dosemu](https://www.archlinux.org/packages/?name=dosemu)

*   **MAME** — Multiple Arcade Machine Emulator.

	[http://mamedev.org/](http://mamedev.org/) || [sdlmame](https://www.archlinux.org/packages/?name=sdlmame)

*   **ResidualVM** — Cross-platform 3D game interpreter which allows you to play LucasArts' Lua-based 3D adventures.

	[http://residualvm.org/](http://residualvm.org/) || [residualvm](https://aur.archlinux.org/packages/residualvm/)

*   **[RetroArch](/index.php/RetroArch "RetroArch")** — Frontend to libretro (emulation library, using modified versions of existing emulators as plugins).

	[http://www.libretro.com/](http://www.libretro.com/) || [retroarch](https://www.archlinux.org/packages/?name=retroarch)

*   **ScummVM** — Virtual machine for old school adventures.

	[http://www.scummvm.org/](http://www.scummvm.org/) || [scummvm](https://www.archlinux.org/packages/?name=scummvm)

*   **X Neko Project II** — PC-9801 emulator.

	[http://www.asahi-net.or.jp/~aw9k-nnk/np2/](http://www.asahi-net.or.jp/~aw9k-nnk/np2/) || [xnp2](https://aur.archlinux.org/packages/xnp2/)

### Amateur radio

See the main article: [Amateur radio#Software list](/index.php/Amateur_radio#Software_list "Amateur radio").

See also [Wikipedia:List of software-defined radios](https://en.wikipedia.org/wiki/List_of_software-defined_radios "wikipedia:List of software-defined radios").

### Display calibration

#### Console

*   **Argyll CMS** — An ICC compatible color management system with support for different colorimeter hardware.

	[http://www.argyllcms.com/](http://www.argyllcms.com/) || [argyllcms](https://www.archlinux.org/packages/?name=argyllcms)

#### Graphical

*   **DisplayCAL** — A graphical user interface for the display calibration and profiling tools of Argyll CMS.

	[http://displaycal.net/](http://displaycal.net/) || [displaycal](https://www.archlinux.org/packages/?name=displaycal)

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