**<a class="mw-selflink selflink">List of applications</a>**

* * *

[Internet](/index.php/List_of_applications/Internet "List of applications/Internet") – [Multimedia](/index.php/List_of_applications/Multimedia "List of applications/Multimedia") – [Utilities](/index.php/List_of_applications/Utilities "List of applications/Utilities") – [Documents](/index.php/List_of_applications/Documents "List of applications/Documents") – [Security](/index.php/List_of_applications/Security "List of applications/Security") – [Science](/index.php/List_of_applications/Science "List of applications/Science") – [Other](/index.php/List_of_applications/Other "List of applications/Other")

Related articles

*   [Core utilities](/index.php/Core_utilities "Core utilities")
*   [List of games](/index.php/List_of_games "List of games")

This article is a general list of applications sorted by category, as a reference for those looking for packages. Many sections are split between console and graphical applications.

**Tip:**

*   This page exists primarily to make it easier to search for alternatives to an application that you do not know under which section has been added. Use the links in the template at the top to view the main sections as separate pages.
*   Please consider [installing](/index.php/Installing "Installing") the [pkgstats](/index.php/Pkgstats "Pkgstats") package, which provides a timer that sends a list of the packages installed on your system, along with the architecture and the mirrors you use, to the Arch Linux developers in order to help them prioritize their efforts and make the distribution even better. The information is sent anonymously and cannot be used to identify you. You can view the collected data at the [Statistics page](https://www.archlinux.de/?page=Statistics). More information is available in [this forum thread](https://bbs.archlinux.org/viewtopic.php?id=105431).
*   Daemon packages usually include the relevant systemd unit file to [start](/index.php/Start "Start"); some packages even include different ones. After installation `pacman -Qql *package* | grep -Fe .service -e .socket` can be used to check and find the relevant one.

**Note:** Applications listed in "Console" sections can have graphical front-ends. Official ones are currently omitted.

## Contents

*   [1 Internet](#Internet)
    *   [1.1 Network connection](#Network_connection)
        *   [1.1.1 Network managers](#Network_managers)
        *   [1.1.2 VPN clients](#VPN_clients)
        *   [1.1.3 Anonymizing networks](#Anonymizing_networks)
    *   [1.2 Web browsers](#Web_browsers)
        *   [1.2.1 Console](#Console)
        *   [1.2.2 Graphical](#Graphical)
            *   [1.2.2.1 Gecko-based](#Gecko-based)
                *   [1.2.2.1.1 Firefox spin-offs](#Firefox_spin-offs)
            *   [1.2.2.2 Blink-based](#Blink-based)
                *   [1.2.2.2.1 Chromium spin-offs](#Chromium_spin-offs)
                *   [1.2.2.2.2 Browsers based on qt5-webengine](#Browsers_based_on_qt5-webengine)
                *   [1.2.2.2.3 Browsers based on electron/muon](#Browsers_based_on_electron.2Fmuon)
            *   [1.2.2.3 WebKit-based](#WebKit-based)
                *   [1.2.2.3.1 Browsers based on webkit2gtk](#Browsers_based_on_webkit2gtk)
                *   [1.2.2.3.2 Browsers based on qt5-webkit](#Browsers_based_on_qt5-webkit)
            *   [1.2.2.4 Other](#Other)
    *   [1.3 Web servers](#Web_servers)
    *   [1.4 File sharing](#File_sharing)
        *   [1.4.1 Download managers](#Download_managers)
            *   [1.4.1.1 Console](#Console_2)
            *   [1.4.1.2 Graphical](#Graphical_2)
        *   [1.4.2 Cloud storage servers](#Cloud_storage_servers)
        *   [1.4.3 Cloud synchronization clients](#Cloud_synchronization_clients)
        *   [1.4.4 File transfer clients](#File_transfer_clients)
        *   [1.4.5 File transfer servers](#File_transfer_servers)
        *   [1.4.6 BitTorrent clients](#BitTorrent_clients)
            *   [1.4.6.1 Console](#Console_3)
            *   [1.4.6.2 Graphical](#Graphical_3)
                *   [1.4.6.2.1 libtorrent-rasterbar backend](#libtorrent-rasterbar_backend)
                *   [1.4.6.2.2 Other](#Other_2)
        *   [1.4.7 Other P2P networks](#Other_P2P_networks)
        *   [1.4.8 Pastebin clients](#Pastebin_clients)
    *   [1.5 Communication](#Communication)
        *   [1.5.1 Email clients](#Email_clients)
            *   [1.5.1.1 Console](#Console_4)
            *   [1.5.1.2 Graphical](#Graphical_4)
        *   [1.5.2 Mail servers](#Mail_servers)
        *   [1.5.3 Instant messaging](#Instant_messaging)
            *   [1.5.3.1 IRC clients](#IRC_clients)
                *   [1.5.3.1.1 Console](#Console_5)
                *   [1.5.3.1.2 Graphical](#Graphical_5)
            *   [1.5.3.2 XMPP (Jabber) clients](#XMPP_.28Jabber.29_clients)
                *   [1.5.3.2.1 Console](#Console_6)
                *   [1.5.3.2.2 Graphical](#Graphical_6)
            *   [1.5.3.3 XMPP servers](#XMPP_servers)
            *   [1.5.3.4 Other](#Other_3)
            *   [1.5.3.5 Multi-protocol clients](#Multi-protocol_clients)
                *   [1.5.3.5.1 Console](#Console_7)
                *   [1.5.3.5.2 Graphical](#Graphical_7)
            *   [1.5.3.6 Lan messengers](#Lan_messengers)
        *   [1.5.4 VoIP / Softphone](#VoIP_.2F_Softphone)
            *   [1.5.4.1 Clients](#Clients)
                *   [1.5.4.1.1 SIP](#SIP)
                *   [1.5.4.1.2 Other](#Other_4)
                *   [1.5.4.1.3 Multi-protocol](#Multi-protocol)
            *   [1.5.4.2 Voice servers](#Voice_servers)
            *   [1.5.4.3 Utilities](#Utilities)
    *   [1.6 News, RSS, and blogs](#News.2C_RSS.2C_and_blogs)
        *   [1.6.1 News aggregators](#News_aggregators)
            *   [1.6.1.1 Console](#Console_8)
            *   [1.6.1.2 Graphical](#Graphical_8)
        *   [1.6.2 Podcast clients](#Podcast_clients)
        *   [1.6.3 Usenet newsreaders & newsgrabbers](#Usenet_newsreaders_.26_newsgrabbers)
        *   [1.6.4 Blog engines](#Blog_engines)
        *   [1.6.5 Microblogging clients](#Microblogging_clients)
    *   [1.7 Remote desktop](#Remote_desktop)
        *   [1.7.1 Remote desktop clients](#Remote_desktop_clients)
        *   [1.7.2 Remote desktop servers](#Remote_desktop_servers)
*   [2 Multimedia](#Multimedia)
    *   [2.1 Codecs](#Codecs)
    *   [2.2 Image](#Image)
        *   [2.2.1 Image viewers](#Image_viewers)
            *   [2.2.1.1 Console](#Console_9)
            *   [2.2.1.2 Graphical](#Graphical_9)
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
            *   [2.4.1.1 Console](#Console_10)
            *   [2.4.1.2 Graphical](#Graphical_10)
        *   [2.4.2 Subtitles](#Subtitles)
        *   [2.4.3 DVD ripping](#DVD_ripping)
        *   [2.4.4 Video editors](#Video_editors)
            *   [2.4.4.1 Console](#Console_11)
            *   [2.4.4.2 Graphical](#Graphical_11)
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
    *   [3.3 Terminal emulators](#Terminal_emulators)
        *   [3.3.1 VTE-based](#VTE-based)
        *   [3.3.2 KMS-based](#KMS-based)
        *   [3.3.3 framebuffer-based](#framebuffer-based)
    *   [3.4 Hex editors](#Hex_editors)
    *   [3.5 Integrated development environments](#Integrated_development_environments)
    *   [3.6 Build automation](#Build_automation)
    *   [3.7 Files](#Files)
        *   [3.7.1 File managers](#File_managers)
            *   [3.7.1.1 Console](#Console_12)
            *   [3.7.1.2 Graphical](#Graphical_12)
        *   [3.7.2 Trash management](#Trash_management)
        *   [3.7.3 File synchronization](#File_synchronization)
        *   [3.7.4 Archiving and compression tools](#Archiving_and_compression_tools)
            *   [3.7.4.1 Console](#Console_13)
            *   [3.7.4.2 Graphical](#Graphical_13)
        *   [3.7.5 Comparison, diff, merge](#Comparison.2C_diff.2C_merge)
        *   [3.7.6 Batch renamers](#Batch_renamers)
        *   [3.7.7 Finders](#Finders)
    *   [3.8 Disk cleaning](#Disk_cleaning)
    *   [3.9 Disk usage display](#Disk_usage_display)
    *   [3.10 Clock synchronization](#Clock_synchronization)
    *   [3.11 System monitoring](#System_monitoring)
    *   [3.12 System information viewers](#System_information_viewers)
        *   [3.12.1 Console](#Console_14)
        *   [3.12.2 Graphical](#Graphical_14)
    *   [3.13 Keyboard layout switchers](#Keyboard_layout_switchers)
    *   [3.14 Power management](#Power_management)
    *   [3.15 Clipboard managers](#Clipboard_managers)
    *   [3.16 Package management](#Package_management)
    *   [3.17 Input methods](#Input_methods)
*   [4 Documents and texts](#Documents_and_texts)
    *   [4.1 Office suites](#Office_suites)
    *   [4.2 Word processors](#Word_processors)
    *   [4.3 Document markup languages](#Document_markup_languages)
    *   [4.4 Spreadsheets](#Spreadsheets)
    *   [4.5 Scientific documents](#Scientific_documents)
    *   [4.6 Translation and localization](#Translation_and_localization)
    *   [4.7 Text editors](#Text_editors)
        *   [4.7.1 Console](#Console_15)
            *   [4.7.1.1 Vi text editors](#Vi_text_editors)
        *   [4.7.2 Graphical](#Graphical_15)
            *   [4.7.2.1 Collaborative text editors](#Collaborative_text_editors)
    *   [4.8 Readers and Viewers](#Readers_and_Viewers)
        *   [4.8.1 E-book applications](#E-book_applications)
        *   [4.8.2 PDF and DjVu](#PDF_and_DjVu)
            *   [4.8.2.1 Console](#Console_16)
            *   [4.8.2.2 Graphical](#Graphical_16)
        *   [4.8.3 Terminal pagers](#Terminal_pagers)
        *   [4.8.4 CHM](#CHM)
        *   [4.8.5 Comic book (comix/manga)](#Comic_book_.28comix.2Fmanga.29)
    *   [4.9 Scanning software](#Scanning_software)
    *   [4.10 OCR software](#OCR_software)
        *   [4.10.1 Engines](#Engines)
        *   [4.10.2 Layout analyzers and user interfaces](#Layout_analyzers_and_user_interfaces)
    *   [4.11 Note taking organizers](#Note_taking_organizers)
        *   [4.11.1 Console](#Console_17)
        *   [4.11.2 Graphical](#Graphical_17)
    *   [4.12 Mind-mapping tools](#Mind-mapping_tools)
    *   [4.13 Character Selector](#Character_Selector)
    *   [4.14 Stylus notes taking](#Stylus_notes_taking)
    *   [4.15 Bibliographic reference managers](#Bibliographic_reference_managers)
    *   [4.16 Barcode generators and readers](#Barcode_generators_and_readers)
        *   [4.16.1 Console](#Console_18)
        *   [4.16.2 Graphical](#Graphical_18)
*   [5 Security](#Security)
    *   [5.1 Network security](#Network_security)
    *   [5.2 Threat and vulnerability detection](#Threat_and_vulnerability_detection)
    *   [5.3 File security](#File_security)
    *   [5.4 Anti malware](#Anti_malware)
    *   [5.5 Backup programs](#Backup_programs)
    *   [5.6 Screen lockers](#Screen_lockers)
    *   [5.7 Hash checkers](#Hash_checkers)
    *   [5.8 Encryption, signing, steganography](#Encryption.2C_signing.2C_steganography)
    *   [5.9 Password managers](#Password_managers)
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
*   [7 Others](#Others)
    *   [7.1 Finance](#Finance)
    *   [7.2 Education](#Education)
        *   [7.2.1 Flashcards](#Flashcards)
        *   [7.2.2 Education management engines](#Education_management_engines)
        *   [7.2.3 Touch typing](#Touch_typing)
    *   [7.3 Time management](#Time_management)
        *   [7.3.1 Console](#Console_19)
        *   [7.3.2 Graphical](#Graphical_19)
    *   [7.4 Recipe management](#Recipe_management)
    *   [7.5 Accessibility](#Accessibility)
        *   [7.5.1 Screen reading](#Screen_reading)
        *   [7.5.2 Speech recognition](#Speech_recognition)
    *   [7.6 Amateur radio](#Amateur_radio)
    *   [7.7 Display calibration](#Display_calibration)
    *   [7.8 Display managers](#Display_managers)
    *   [7.9 Command shells](#Command_shells)
    *   [7.10 Terminal multiplexers](#Terminal_multiplexers)
    *   [7.11 Desktop environments](#Desktop_environments)
        *   [7.11.1 Window managers](#Window_managers)
            *   [7.11.1.1 Console](#Console_20)
            *   [7.11.1.2 Graphical](#Graphical_20)
            *   [7.11.1.3 Composite managers](#Composite_managers)
        *   [7.11.2 Window tilers](#Window_tilers)
        *   [7.11.3 Taskbars](#Taskbars)
        *   [7.11.4 Application launchers](#Application_launchers)
        *   [7.11.5 Wallpaper setters](#Wallpaper_setters)
        *   [7.11.6 Virtual desktop pagers](#Virtual_desktop_pagers)
        *   [7.11.7 Desktop widgets](#Desktop_widgets)
    *   [7.12 Dictionary and Thesaurus](#Dictionary_and_Thesaurus)
*   [8 See also](#See_also)

## Internet

### Network connection

#### Network managers

*   **[ConnMan](/index.php/ConnMan "ConnMan")** — Daemon for managing internet connections within embedded devices running the Linux operating system. Comes with a command-line client, plus Enlightenment, ncurses, GTK and Dmenu clients are available.

	[https://01.org/connman](https://01.org/connman) || [connman](https://www.archlinux.org/packages/?name=connman)

*   **[dhcpcd](/index.php/Dhcpcd "Dhcpcd")** — RFC2131 compliant DHCP client daemon.

	[https://roy.marples.name/projects/dhcpcd](https://roy.marples.name/projects/dhcpcd) || [dhcpcd](https://www.archlinux.org/packages/?name=dhcpcd)

*   **Kea** — An open source implementation of the Dynamic Host Configuration Protocol (DHCP) servers.

	[https://www.isc.org/kea/](https://www.isc.org/kea/) || [kea](https://www.archlinux.org/packages/?name=kea)

*   **[netctl](/index.php/Netctl "Netctl")** — Simple and robust tool to manage network connections via profiles. Intended for use with [systemd](/index.php/Systemd "Systemd").

	[https://projects.archlinux.org/netctl.git/](https://projects.archlinux.org/netctl.git/) || [netctl](https://www.archlinux.org/packages/?name=netctl)

*   **[NetworkManager](/index.php/NetworkManager "NetworkManager")** — Manager that provides wired, wireless, mobile broadband and OpenVPN detection with configuration and automatic connection.

	[https://wiki.gnome.org/Projects/NetworkManager](https://wiki.gnome.org/Projects/NetworkManager) || [networkmanager](https://www.archlinux.org/packages/?name=networkmanager)

*   **[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")** — Native [systemd](/index.php/Systemd "Systemd") daemon that manages network configuration. It includes support for basic network configuration through [udev](/index.php/Udev "Udev").

	[http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html) || [systemd](https://www.archlinux.org/packages/?name=systemd)

*   **[Wicd](/index.php/Wicd "Wicd")** — Wireless and wired connection manager with few dependencies. Comes with an ncurses interface, and a GTK interface [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) is available.

	[https://launchpad.net/wicd](https://launchpad.net/wicd) || [wicd](https://www.archlinux.org/packages/?name=wicd)

*   **[Wifi Radar](/index.php/Wifi_Radar "Wifi Radar")** — *WiFi Radar* is a Python/PyGTK2 utility for managing wireless (and **only** wireless) profiles. It enables you to scan for available networks and create profiles for your preferred networks.

	[http://wifi-radar.tuxfamily.org/](http://wifi-radar.tuxfamily.org/) || [wifi-radar](https://www.archlinux.org/packages/?name=wifi-radar)

See also [Network configuration#Network managers](/index.php/Network_configuration#Network_managers "Network configuration") and [Wireless network configuration#Automatic setup](/index.php/Wireless_network_configuration#Automatic_setup "Wireless network configuration") for feature comparisons.

#### VPN clients

*   **Libreswan** — A free software implementation of the most widely supported and standarized VPN protocol based on ("IPsec") and the Internet Key Exchange ("IKE").

	[https://libreswan.org/](https://libreswan.org/) || [libreswan](https://aur.archlinux.org/packages/libreswan/)

*   **[OpenConnect](/index.php/OpenConnect "OpenConnect")** — Supports Cisco and Juniper VPNs.

	[http://www.infradead.org/openconnect/](http://www.infradead.org/openconnect/) || [openconnect](https://www.archlinux.org/packages/?name=openconnect)

*   **[OpenVPN](/index.php/OpenVPN "OpenVPN")** — To connect to OpenVPN VPNs.

	[https://openvpn.net/](https://openvpn.net/) || [openvpn](https://www.archlinux.org/packages/?name=openvpn)

*   **[PPTP Client](/index.php/PPTP_Client "PPTP Client")** — To connect to PPTP VPNs, like Microsoft VPNs (MPPE). (insecure)

	[http://pptpclient.sourceforge.net/](http://pptpclient.sourceforge.net/) || [pptpclient](https://www.archlinux.org/packages/?name=pptpclient)

*   **[strongSwan](/index.php/StrongSwan "StrongSwan")** — IPsec-based VPN Solution.

	[https://www.strongswan.org/](https://www.strongswan.org/) || [strongswan](https://www.archlinux.org/packages/?name=strongswan)

*   **[tinc](/index.php/Tinc "Tinc")** — tinc is a free VPN daemon.

	[https://www.tinc-vpn.org/](https://www.tinc-vpn.org/) || [tinc](https://www.archlinux.org/packages/?name=tinc)

*   **[Vpnc](/index.php/Vpnc "Vpnc")** — To connect to Cisco 3000 VPN Concentrators.

	[https://www.unix-ag.uni-kl.de/~massar/vpnc/](https://www.unix-ag.uni-kl.de/~massar/vpnc/) || [vpnc](https://www.archlinux.org/packages/?name=vpnc)

#### Anonymizing networks

*   **[Freenet](/index.php/Freenet "Freenet")** — An encrypted network without censorship.

	[https://freenetproject.org](https://freenetproject.org) || [freenet](https://aur.archlinux.org/packages/freenet/)

*   **[GNUnet](/index.php/GNUnet "GNUnet")** — A framework for secure peer-to-peer networking.

	[http://gnunet.org](http://gnunet.org) || [gnunet](https://www.archlinux.org/packages/?name=gnunet)

*   **[I2P](/index.php/I2P "I2P")** — A distributed anonymous network.

	[https://geti2p.net](https://geti2p.net) || [i2p](https://aur.archlinux.org/packages/i2p/)

*   **[Lantern](/index.php/Lantern "Lantern")** — A free peer-to-peer internet censorship circumvention software.

	[https://getlantern.org/en_US/](https://getlantern.org/en_US/) || [lantern-bin](https://aur.archlinux.org/packages/lantern-bin/)

*   **[Tor](/index.php/Tor "Tor")** — Anonymizing overlay network.

	[http://www.torproject.org/](http://www.torproject.org/) || [tor](https://www.archlinux.org/packages/?name=tor)

### Web browsers

See also [Wikipedia:Comparison of web browsers](https://en.wikipedia.org/wiki/Comparison_of_web_browsers "wikipedia:Comparison of web browsers").

#### Console

*   **[ELinks](https://en.wikipedia.org/wiki/ELinks "wikipedia:ELinks")** — Advanced and well-established feature-rich text mode web browser (Links fork, barely supported since 2009).

	[http://elinks.or.cz/](http://elinks.or.cz/) || [elinks](https://www.archlinux.org/packages/?name=elinks)

*   **[Links](https://en.wikipedia.org/wiki/Links_(web_browser) "wikipedia:Links (web browser)")** — Text WWW browser. Includes a console version [links] similar to Lynx, and a graphical X-window/framebuffer version [xlinks -g] (must be compiled in, Arch has both) with CSS, image rendering, pull-down menus.

	[http://links.twibright.com/](http://links.twibright.com/) || [links](https://www.archlinux.org/packages/?name=links)

*   **[Lynx](https://en.wikipedia.org/wiki/Lynx_(web_browser) "wikipedia:Lynx (web browser)")** — Text browser for the World Wide Web.

	[http://lynx.invisible-island.net/](http://lynx.invisible-island.net/) || [lynx](https://www.archlinux.org/packages/?name=lynx)

*   **[w3m](https://en.wikipedia.org/wiki/W3m "wikipedia:W3m")** — Pager/text-based web browser. It has vim-like keybindings, and is able to display images.

	[http://w3m.sourceforge.net/](http://w3m.sourceforge.net/) || [w3m](https://www.archlinux.org/packages/?name=w3m)

#### Graphical

##### Gecko-based

See also [Wikipedia:Gecko (software)](https://en.wikipedia.org/wiki/Gecko_(software) "wikipedia:Gecko (software)").

*   **[Firefox](/index.php/Firefox "Firefox")** — Extensible browser from Mozilla based on Gecko with fast rendering.

	[https://mozilla.com/firefox](https://mozilla.com/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

*   **[SeaMonkey](https://en.wikipedia.org/wiki/SeaMonkey "wikipedia:SeaMonkey")** — Continuation of the Mozilla Internet Suite.

	[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

###### Firefox spin-offs

*   **[Cliqz](https://en.wikipedia.org/wiki/Cliqz "wikipedia:Cliqz")** — Firefox-based privacy aware web browser.

	[https://cliqz.com/](https://cliqz.com/) || [cliqz](https://aur.archlinux.org/packages/cliqz/) or [cliqz-bin](https://aur.archlinux.org/packages/cliqz-bin/)

*   **Cyberfox** — Fast and privacy oriented fork of Mozilla Firefox.

	[https://cyberfox.8pecxstudios.com/](https://cyberfox.8pecxstudios.com/) || [cyberfox-bin](https://aur.archlinux.org/packages/cyberfox-bin/)

*   **Waterfox** — Optimized fork of Mozilla Firefox, without data collection and allowing unsigned extensions and NPAPI plugins.

	[https://www.waterfoxproject.org/](https://www.waterfoxproject.org/) || [waterfox-bin](https://aur.archlinux.org/packages/waterfox-bin/) or [waterfox-git](https://aur.archlinux.org/packages/waterfox-git/)

*   **[GNU IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat")** — A customized build of Firefox ESR distributed by the GNU Project, stripped of non-free components and with additional privacy extensions. Release cycle may be delayed compared to Mozilla Firefox.

	[https://www.gnu.org/software/gnuzilla/](https://www.gnu.org/software/gnuzilla/) || [icecat](https://aur.archlinux.org/packages/icecat/) or [icecat-bin](https://aur.archlinux.org/packages/icecat-bin/)

##### Blink-based

See also [Wikipedia:Blink (web engine)](https://en.wikipedia.org/wiki/Blink_(web_engine) "wikipedia:Blink (web engine)").

*   **[Chromium](/index.php/Chromium "Chromium")** — Web browser developed by Google, the open source project behind Google Chrome.

	[https://www.chromium.org/](https://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

###### Chromium spin-offs

*   **[Google Chrome](/index.php/Google_Chrome "Google Chrome")** — Proprietary web browser developed by Google.

	[https://www.google.com/chrome/](https://www.google.com/chrome/) || [google-chrome](https://aur.archlinux.org/packages/google-chrome/)

*   **Inox** — A privacy-focused patchset for Chromium, which disables Google services, proprietary features, prevents "calling home" and unhides all extensions.

	[https://github.com/gcarq/inox-patchset](https://github.com/gcarq/inox-patchset) || [inox](https://aur.archlinux.org/packages/inox/) or [inox-bin](https://aur.archlinux.org/packages/inox-bin/)

*   **Iridium** — A privacy-focused [patchset](https://git.iridiumbrowser.de/cgit.cgi/iridium-browser/tree/?h=patchview) for Chromium. See [differences from Chromium](https://github.com/iridium-browser/tracker/wiki/Differences-between-Iridium-and-Chromium).

	[https://iridiumbrowser.de/](https://iridiumbrowser.de/) || [iridium](https://aur.archlinux.org/packages/iridium/)

*   **[Opera](/index.php/Opera "Opera")** — Proprietary browser developed by Opera Software.

	[https://opera.com](https://opera.com) || [opera](https://www.archlinux.org/packages/?name=opera)

*   **[Slimjet](https://en.wikipedia.org/wiki/SlimBrowser "wikipedia:SlimBrowser")** — Fast, smart and powerful proprietary browser based on Chromium.

	[http://www.slimjet.com/](http://www.slimjet.com/) || [slimjet](https://aur.archlinux.org/packages/slimjet/)

*   **Ungoogled Chromium** — Modifications to Google Chromium for removing Google integration and enhancing privacy, control, and transparency

	[https://github.com/Eloston/ungoogled-chromium](https://github.com/Eloston/ungoogled-chromium) || [ungoogled-chromium](https://aur.archlinux.org/packages/ungoogled-chromium/)

*   **[Vivaldi](/index.php/Vivaldi "Vivaldi")** — An advanced proprietary browser made with the power user in mind.

	[https://vivaldi.com/](https://vivaldi.com/) || [vivaldi](https://aur.archlinux.org/packages/vivaldi/)

*   **[Yandex Browser](https://en.wikipedia.org/wiki/Yandex_Browser "wikipedia:Yandex Browser")** — Proprietary browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier.

	[https://browser.yandex.com/](https://browser.yandex.com/) || [yandex-browser-beta](https://aur.archlinux.org/packages/yandex-browser-beta/)

###### Browsers based on qt5-webengine

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Web browser based on Qt toolkit and Qt WebEngine (or KHTML layout engine), part of [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/).

	[http://konqueror.org/](http://konqueror.org/) || [konqueror](https://www.archlinux.org/packages/?name=konqueror)

*   **Liri Browser** — A minimalistic material design web browser written for Liri.

	[https://github.com/lirios/browser](https://github.com/lirios/browser) || [liri-browser-git](https://aur.archlinux.org/packages/liri-browser-git/)

*   **[Otter Browser](/index.php/Otter_Browser "Otter Browser")** — Browser aiming to recreate classic Opera (12.x) UI using Qt5\. Experimental support for QtWebEngine is available.

	[http://otter-browser.org/](http://otter-browser.org/) || [otter-browser](https://aur.archlinux.org/packages/otter-browser/)

*   **Qt WebBrowser** — Browser for embedded devices developed using the capabilities of Qt and Qt WebEngine.

	[http://doc.qt.io/QtWebBrowser/](http://doc.qt.io/QtWebBrowser/) || [qtwebbrowser](https://aur.archlinux.org/packages/qtwebbrowser/)

*   **[QupZilla](https://en.wikipedia.org/wiki/QupZilla "wikipedia:QupZilla")** — New and very fast open source browser based on QtWebEngine, written in Qt framework.

	[http://www.qupzilla.com](http://www.qupzilla.com) || [qupzilla](https://www.archlinux.org/packages/?name=qupzilla)

*   **[qutebrowser](/index.php/Qutebrowser "Qutebrowser")** — A keyboard-driven, [vim](/index.php/Vim "Vim")-like browser based on PyQt5 and QtWebEngine.

	[https://github.com/The-Compiler/qutebrowser](https://github.com/The-Compiler/qutebrowser) || [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser)

###### Browsers based on electron/muon

*   **[Brave](https://en.wikipedia.org/wiki/Brave_(web_browser) "wikipedia:Brave (web browser)")** — Web browser that blocks ads and trackers by default. Based on the [Muon](https://github.com/brave/muon) platform (fork of Electron).

	[https://www.brave.com/](https://www.brave.com/) || [brave](https://aur.archlinux.org/packages/brave/) or [brave-bin](https://aur.archlinux.org/packages/brave-bin/)

*   **Min** — A smarter, faster web browser based on the [Electron](http://electron.atom.io/) platform.

	[https://minbrowser.github.io/min/](https://minbrowser.github.io/min/) || [min](https://www.archlinux.org/packages/?name=min)

##### WebKit-based

See also [Wikipedia:WebKit](https://en.wikipedia.org/wiki/WebKit "wikipedia:WebKit").

**Note:** webkitgtk, webkitgtk2 and qtwebkit-based browsers were removed from the list, because these are today considered insecure and outdated. More info [here](https://blogs.gnome.org/mcatanzaro/2016/02/01/on-webkit-security-updates/).

###### Browsers based on webkit2gtk

*   **Eolie** — Simple web browser for GNOME.

	[https://gnumdk.github.io/eolie-web/](https://gnumdk.github.io/eolie-web/) || [eolie](https://aur.archlinux.org/packages/eolie/)

*   **[GNOME Web](/index.php/GNOME_Web "GNOME Web")** — Browser which uses the WebKitGTK+ rendering engine, part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

	[https://wiki.gnome.org/Apps/Web/](https://wiki.gnome.org/Apps/Web/) || [epiphany](https://www.archlinux.org/packages/?name=epiphany)

*   **[Lariza](/index.php/Lariza "Lariza")** — A simple, experimental web browser using GTK+ 3, GLib and WebKit2GTK+.

	[https://www.uninformativ.de/projects/lariza/](https://www.uninformativ.de/projects/lariza/) || [lariza](https://aur.archlinux.org/packages/lariza/)

*   **[Luakit](/index.php/Luakit "Luakit")** — Fast, small, webkit based browser framework extensible by Lua.

	[http://luakit.org/](http://luakit.org/) || [luakit-git](https://aur.archlinux.org/packages/luakit-git/)

*   **[Midori](/index.php/Midori "Midori")** — Lightweight web browser based on GTK+ and WebKit.

	[http://midori-browser.org/](http://midori-browser.org/) || [midori](https://www.archlinux.org/packages/?name=midori)

*   **Poseidon** — Fast, minimal and lightweight browser.

	[https://github.com/sidus-dev/poseidon](https://github.com/sidus-dev/poseidon) || [poseidon](https://aur.archlinux.org/packages/poseidon/)

*   **[Surf](/index.php/Surf "Surf")** — Lightweight WebKit-based browser, which follows the [suckless ideology](https://suckless.org/philosophy) (basically, the browser itself is a single C source file).

	[https://surf.suckless.org/](https://surf.suckless.org/) || [surf](https://www.archlinux.org/packages/?name=surf)

*   **Surfer** — Simple keyboard based web browser.

	[https://github.com/nihilowy/surfer](https://github.com/nihilowy/surfer) || [surfer](https://aur.archlinux.org/packages/surfer/)

*   **[Uzbl](/index.php/Uzbl "Uzbl")** — Group of web interface tools which adhere to the Unix philosophy.

	[http://uzbl.org/](http://uzbl.org/) || [uzbl-browser](https://www.archlinux.org/packages/?name=uzbl-browser)

*   **Vimb** — A Vim-like web browser that is inspired by Pentadactyl and Vimprobable.

	[https://fanglingsu.github.io/vimb/](https://fanglingsu.github.io/vimb/) || [vimb-git](https://aur.archlinux.org/packages/vimb-git/)

###### Browsers based on qt5-webkit

*   **[Dooble](https://en.wikipedia.org/wiki/Dooble "wikipedia:Dooble")** — A safe WebKit Web browser.

	[http://dooble.sourceforge.net/](http://dooble.sourceforge.net/) || [dooble](https://aur.archlinux.org/packages/dooble/)

*   **OSPKit** — Webkit based html browser for printing.

	[http://osp.kitchen/tools/ospkit/](http://osp.kitchen/tools/ospkit/) || [ospkit-git](https://aur.archlinux.org/packages/ospkit-git/)

*   **[Otter Browser](/index.php/Otter_Browser "Otter Browser")** — Browser aiming to recreate classic Opera (12.x) UI using Qt5.

	[http://otter-browser.org/](http://otter-browser.org/) || [otter-browser](https://aur.archlinux.org/packages/otter-browser/)

*   **[qutebrowser](/index.php/Qutebrowser "Qutebrowser")** — A keyboard-driven, [vim](/index.php/Vim "Vim")-like browser based on PyQt5 with QtWebKit as an available backend.

	[https://github.com/The-Compiler/qutebrowser](https://github.com/The-Compiler/qutebrowser) || [qutebrowser](https://www.archlinux.org/packages/?name=qutebrowser)

*   **WCGBrowser** — A web browser for kiosk systems.

	[http://www.alandmoore.com/wcgbrowser/wcgbrowser.html](http://www.alandmoore.com/wcgbrowser/wcgbrowser.html) || [wcgbrowser-git](https://aur.archlinux.org/packages/wcgbrowser-git/)

##### Other

*   **[Dillo](https://en.wikipedia.org/wiki/Dillo "wikipedia:Dillo")** — Small, fast graphical web browser built on [FLTK](https://en.wikipedia.org/wiki/Fltk "wikipedia:Fltk"). Uses its own layout engine.

	[http://dillo.org/](http://dillo.org/) || [dillo](https://www.archlinux.org/packages/?name=dillo)

*   **[NetSurf](https://en.wikipedia.org/wiki/NetSurf "wikipedia:NetSurf")** — Featherweight browser written in C, notable for its slowly developing JavaScript support and fast rendering through its own layout engine.

	[http://netsurf-browser.org](http://netsurf-browser.org) || [netsurf](https://www.archlinux.org/packages/?name=netsurf)

*   **[Pale Moon](https://en.wikipedia.org/wiki/Pale_Moon_(web_browser) layout engine, a fork of Gecko. Firefox add-ons may not be compatible. [[1]](https://addons.palemoon.org/firefox/incompatible/) Without support for newer Firefox features such as cache2, e10s, and OTMC.

	[http://www.palemoon.org/](http://www.palemoon.org/) || [palemoon](https://aur.archlinux.org/packages/palemoon/) or [palemoon-bin](https://aur.archlinux.org/packages/palemoon-bin/)

### Web servers

See also [w:Comparison of web server software](https://en.wikipedia.org/wiki/Comparison_of_web_server_software "w:Comparison of web server software").

*   **[Apache](/index.php/Apache "Apache")** — A high performance Unix-based HTTP server.

	[http://www.apache.org/dist/httpd](http://www.apache.org/dist/httpd) || [apache](https://www.archlinux.org/packages/?name=apache)

*   **[Hiawatha](/index.php/Hiawatha "Hiawatha")** — Secure and advanced webserver.

	[https://www.hiawatha-webserver.org/](https://www.hiawatha-webserver.org/) || [hiawatha](https://www.archlinux.org/packages/?name=hiawatha)

*   **[Lighttpd](/index.php/Lighttpd "Lighttpd")** — A secure, fast, compliant and very flexible web-server.

	[http://www.lighttpd.net/](http://www.lighttpd.net/) || [lighttpd](https://www.archlinux.org/packages/?name=lighttpd)

*   **[nginx](/index.php/Nginx "Nginx")** — Lightweight HTTP server and IMAP/POP3 proxy server.

	[https://nginx.org/](https://nginx.org/) || [nginx](https://www.archlinux.org/packages/?name=nginx)

*   **Webfs** — Simple and instant http server for mostly static content.

	[http://linux.bytesex.org/misc/webfs.html](http://linux.bytesex.org/misc/webfs.html) || [webfs](https://www.archlinux.org/packages/?name=webfs)

*   **darkhttpd** — A small and secure static webserver

	[https://unix4lyfe.org/darkhttpd/](https://unix4lyfe.org/darkhttpd/) || [darkhttpd](https://www.archlinux.org/packages/?name=darkhttpd)

*   **yaws** — Web server/framework written in Erlang

	[http://yaws.hyber.org/](http://yaws.hyber.org/) || [yaws](https://www.archlinux.org/packages/?name=yaws)

*   **shttpd** — Supported fork of the thttpd web server

	[http://freecode.com/projects/shttpd](http://freecode.com/projects/shttpd) || [shttpd](https://aur.archlinux.org/packages/shttpd/)

### File sharing

#### Download managers

See also [Wikipedia:Comparison of download managers](https://en.wikipedia.org/wiki/Comparison_of_download_managers "wikipedia:Comparison of download managers").

##### Console

*   **[Aria2](/index.php/Aria2 "Aria2")** — Download utility that supports HTTP, FTP, SFTP, BitTorrent and Metalink.

	[https://aria2.github.io/](https://aria2.github.io/) || [aria2](https://www.archlinux.org/packages/?name=aria2)

*   **Axel** — Light command line download accelerator. Supports HTTP and FTP.

	[https://github.com/eribertomota/axel](https://github.com/eribertomota/axel) || [axel](https://www.archlinux.org/packages/?name=axel)

*   **[cURL](https://en.wikipedia.org/wiki/cURL "wikipedia:cURL")** — An URL retrieval utility and library. Supports HTTP, FTP and SFTP.

	[https://curl.haxx.se/](https://curl.haxx.se/) || [curl](https://www.archlinux.org/packages/?name=curl)

*   **[LFTP](https://en.wikipedia.org/wiki/Lftp "wikipedia:Lftp")** — Sophisticated file transfer program. Supports HTTP, FTP, SFTP, FISH, and BitTorrent.

	[http://lftp.yar.ru/](http://lftp.yar.ru/) || [lftp](https://www.archlinux.org/packages/?name=lftp)

*   **Plowshare** — A set of command-line tools designed for managing file-sharing websites (aka Hosters).

	[https://github.com/mcrapet/plowshare](https://github.com/mcrapet/plowshare) || [plowshare-git](https://aur.archlinux.org/packages/plowshare-git/)

*   **[pyLoad](/index.php/PyLoad "PyLoad")** — Downloader written in Python and designed to be extremely lightweight, easily extensible and fully manageable via web.

	[https://pyload.net/](https://pyload.net/) || [pyload](https://aur.archlinux.org/packages/pyload/)

*   **snarf** — Command-line URL retrieval tool. Supports HTTP and FTP.

	[http://www.xach.com/snarf/](http://www.xach.com/snarf/) || [snarf](https://www.archlinux.org/packages/?name=snarf)

*   **[Streamlink](/index.php/Streamlink "Streamlink")** — Launch streams from various streaming services in a custom video player.

	[https://streamlink.github.io/](https://streamlink.github.io/) || [streamlink](https://www.archlinux.org/packages/?name=streamlink)

*   **You-Get** — Download media contents (videos, audios, images) from the Web.

	[https://you-get.org/](https://you-get.org/) || [you-get](https://www.archlinux.org/packages/?name=you-get)

*   **youtube-dl** — Download videos from YouTube and many other web sites.

	[https://rg3.github.io/youtube-dl/](https://rg3.github.io/youtube-dl/) || [youtube-dl](https://www.archlinux.org/packages/?name=youtube-dl)

*   **[Wget](https://en.wikipedia.org/wiki/Wget "wikipedia:Wget")** — A network utility to retrieve files from the Web. Supports HTTP and FTP.

	[https://www.gnu.org/software/wget/](https://www.gnu.org/software/wget/) || [wget](https://www.archlinux.org/packages/?name=wget)

##### Graphical

*   **4K Video Downloader** — Quickly download videos from YouTube in high-quality..

	[https://www.4kdownload.com/products/product-videodownloader](https://www.4kdownload.com/products/product-videodownloader) || [4kvideodownloader](https://aur.archlinux.org/packages/4kvideodownloader/)

*   **ClipGrab** — Downloader and converter for YouTube, Vimeo and many other online video sites.

	[https://clipgrab.org/](https://clipgrab.org/) || [clipgrab-qt5](https://aur.archlinux.org/packages/clipgrab-qt5/)

*   **FatRat** — Download manager with support for HTTP, FTP, SFTP, BitTorrent and Metalink.

	[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat-git](https://aur.archlinux.org/packages/fatrat-git/)

*   **FreeRapid** — Java-based downloader that supports downloading from file-sharing services.

	[http://wordrider.net/freerapid/](http://wordrider.net/freerapid/) || [freerapid](https://aur.archlinux.org/packages/freerapid/)

*   **[Gwget](https://en.wikipedia.org/wiki/Wget#GWget "wikipedia:Wget")** — Download manager for GNOME. Supports HTTP and FTP.

	[https://projects.gnome.org/gwget/](https://projects.gnome.org/gwget/) || [gwget](https://www.archlinux.org/packages/?name=gwget)

*   **[JDownloader](/index.php/JDownloader "JDownloader")** — Java-based downloader for one-click hosting sites.

	[http://jdownloader.org/](http://jdownloader.org/) || [jdownloader2](https://aur.archlinux.org/packages/jdownloader2/)

*   **[KGet](https://en.wikipedia.org/wiki/KGet "wikipedia:KGet")** — Download manager for KDE. Supports HTTP, FTP, BitTorrent and Metalink. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[https://www.kde.org/applications/internet/kget/](https://www.kde.org/applications/internet/kget/) || [kget](https://www.archlinux.org/packages/?name=kget)

*   **Persepolis** — Graphical front-end for aria2 download manager with lots of features. Supports HTTP and FTP.

	[https://persepolisdm.github.io/](https://persepolisdm.github.io/) || [persepolis](https://aur.archlinux.org/packages/persepolis/)

*   **Steadyflow** — Simple download manager for GNOME. Supports HTTP and FTP.

	[https://launchpad.net/steadyflow](https://launchpad.net/steadyflow) || [steadyflow](https://www.archlinux.org/packages/?name=steadyflow)

*   **uGet** — GTK+ download manager featuring download classification and HTML import. Supports HTTP, FTP, BitTorrent and Metalink.

	[http://ugetdm.com/](http://ugetdm.com/) || [uget](https://www.archlinux.org/packages/?name=uget)

*   **Xtreme Download Manager** — Powerful tool to increase download speed up-to 500%. Supports HTTP and FTP. Video grabber works in a general way and is not limited to certain websites.

	[http://xdman.sourceforge.net/](http://xdman.sourceforge.net/) || [xdman](https://aur.archlinux.org/packages/xdman/)

#### Cloud storage servers

*   **[Cozy](/index.php/Cozy "Cozy")** — A personal cloud you can hack, host and delete.

	[https://cozy.io/](https://cozy.io/) || [cozy](https://aur.archlinux.org/packages/cozy/)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud")** — A cloud server to store your files centrally on a hardware controlled by you.

	[https://nextcloud.com](https://nextcloud.com) || [nextcloud](https://www.archlinux.org/packages/?name=nextcloud)

*   **[Pydio](/index.php/Pydio "Pydio")** — Mature open source web application for file sharing and synchronization.

	[https://pydio.com/](https://pydio.com/) || [pydio](https://aur.archlinux.org/packages/pydio/)

*   **[Seafile](/index.php/Seafile "Seafile")** — An online file storage and collaboration tool with advanced support for file syncing, privacy protection and teamwork.

	[https://www.seafile.com/](https://www.seafile.com/) || [seafile-server](https://aur.archlinux.org/packages/seafile-server/)

#### Cloud synchronization clients

*   **aws-cli** — CLI for Amazon Web Services, including efficient file transfers to and from Amazon S3.

	[https://aws.amazon.com/cli/](https://aws.amazon.com/cli/) || [aws-cli](https://www.archlinux.org/packages/?name=aws-cli)

*   **[Cozy](/index.php/Cozy "Cozy") Drive** — Desktop client for Cozy.

	[https://cozy-labs.github.io/cozy-desktop/](https://cozy-labs.github.io/cozy-desktop/) || [cozy-desktop-gui](https://aur.archlinux.org/packages/cozy-desktop-gui/)

*   **[CrashPlan](/index.php/CrashPlan "CrashPlan")** — Desktop client for CrashPlan.

	[https://www.crashplan.com/](https://www.crashplan.com/) || [crashplan](https://aur.archlinux.org/packages/crashplan/)

*   **[Dropbox](/index.php/Dropbox "Dropbox")** — Proprietary desktop client for Dropbox.

	[https://www.dropbox.com/](https://www.dropbox.com/) || [dropbox](https://aur.archlinux.org/packages/dropbox/)

*   **[Mega](https://en.wikipedia.org/wiki/Mega_(service) Sync Client** — Desktop client to sync files with Mega.

	[https://mega.nz/](https://mega.nz/) || [megasync](https://aur.archlinux.org/packages/megasync/)

*   **Megatools** — Unofficial CLI for Mega.

	[https://megatools.megous.com/](https://megatools.megous.com/) || [megatools](https://aur.archlinux.org/packages/megatools/)

*   **[Nextcloud](/index.php/Nextcloud "Nextcloud") Client** — Desktop client for Nextcloud.

	[https://nextcloud.com/](https://nextcloud.com/) || [nextcloud-client](https://aur.archlinux.org/packages/nextcloud-client/)

*   **Nutstore** — Desktop client for Nutstore.

	[https://www.jianguoyun.com/](https://www.jianguoyun.com/) || [nutstore](https://aur.archlinux.org/packages/nutstore/)

*   **OneDrive** — Unofficial CLI for [OneDrive](https://onedrive.live.com/about/).

	[https://skilion.github.io/onedrive/](https://skilion.github.io/onedrive/) || [onedrive-git](https://aur.archlinux.org/packages/onedrive-git/)

*   **[Pydio](/index.php/Pydio "Pydio")Sync** — Desktop client for Pydio.

	[https://pydio.com/](https://pydio.com/) || [pydio-sync](https://aur.archlinux.org/packages/pydio-sync/)

*   **S3cmd** — Unofficial CLI for Amazon S3.

	[http://s3tools.org/s3cmd](http://s3tools.org/s3cmd) || [s3cmd](https://www.archlinux.org/packages/?name=s3cmd)

*   **[Seafile](/index.php/Seafile "Seafile") Client** — GUI client for Seafile.

	[https://www.seafile.com/](https://www.seafile.com/) || [seafile-client](https://aur.archlinux.org/packages/seafile-client/)

*   **[SpiderOak](https://en.wikipedia.org/wiki/SpiderOak "wikipedia:SpiderOak") One** — Proprietary client for SpiderOak One.

	[https://spideroak.com/](https://spideroak.com/) || [spideroak-one](https://aur.archlinux.org/packages/spideroak-one/)

*   **[Yandex Disk](/index.php/Yandex_Disk "Yandex Disk")** — Proprietary CLI for Yandex Disk.

	[https://disk.yandex.ru/](https://disk.yandex.ru/) || [yandex-disk](https://aur.archlinux.org/packages/yandex-disk/)

#### File transfer clients

See also [Wikipedia:Comparison of FTP client software](https://en.wikipedia.org/wiki/Comparison_of_FTP_client_software "wikipedia:Comparison of FTP client software").

*   **[CurlFtpFS](/index.php/CurlFtpFS "CurlFtpFS")** — Filesystem for accessing FTP hosts; based on FUSE and libcurl.

	[http://curlftpfs.sourceforge.net/](http://curlftpfs.sourceforge.net/) || [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs)

*   **[FileZilla](https://en.wikipedia.org/wiki/FileZilla "wikipedia:FileZilla")** — Fast and reliable FTP, FTPS and SFTP client.

	[http://filezilla-project.org/](http://filezilla-project.org/) || [filezilla](https://www.archlinux.org/packages/?name=filezilla)

*   **[gFTP](https://en.wikipedia.org/wiki/gFTP "wikipedia:gFTP")** — Multithreaded FTP client for Linux.

	[http://gftp.seul.org/](http://gftp.seul.org/) || [gftp](https://www.archlinux.org/packages/?name=gftp)

*   **ncftp** — A set of free application programs implementing FTP.

	[http://www.ncftp.com/](http://www.ncftp.com/) || [ncftp](https://www.archlinux.org/packages/?name=ncftp)

*   **[SSHFS](/index.php/SSHFS "SSHFS")** — A network filesystem client to connect to SSH (SFTP) servers.

	[https://github.com/libfuse/sshfs/](https://github.com/libfuse/sshfs/) || [sshfs](https://www.archlinux.org/packages/?name=sshfs)

*   **[tnftp](https://en.wikipedia.org/wiki/tnftp "wikipedia:tnftp")** — FTP client with several advanced features for [NetBSD](https://en.wikipedia.org/wiki/NetBSD "wikipedia:NetBSD").

	[http://freecode.com/projects/tnftp](http://freecode.com/projects/tnftp) || [tnftp](https://www.archlinux.org/packages/?name=tnftp)

Some file managers like Dolphin, [GNOME Files](/index.php/GNOME_Files "GNOME Files") and [Thunar](/index.php/Thunar "Thunar") also provide FTP functionality.

#### File transfer servers

See also [Wikipedia:List of FTP server software](https://en.wikipedia.org/wiki/List_of_FTP_server_software "wikipedia:List of FTP server software").

*   **[bftpd](/index.php/Bftpd "Bftpd")** — Small, easy-to-configure FTP server

	[http://bftpd.sourceforge.net/](http://bftpd.sourceforge.net/) || [bftpd](https://www.archlinux.org/packages/?name=bftpd)

*   **[proFTPd](/index.php/Proftpd "Proftpd")** — A secure and configurable FTP server

	[http://www.proftpd.org/](http://www.proftpd.org/) || [proftpd](https://aur.archlinux.org/packages/proftpd/)

*   **[Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")** — Free (BSD-licensed), secure, production-quality and standard-compliant FTP server.

	[http://www.pureftpd.org/project/pure-ftpd](http://www.pureftpd.org/project/pure-ftpd) || [pure-ftpd](https://aur.archlinux.org/packages/pure-ftpd/)

*   **[vsftpd](/index.php/Vsftpd "Vsftpd")** — Lightweight, stable and secure FTP server for UNIX-like systems.

	[https://security.appspot.com/vsftpd.html](https://security.appspot.com/vsftpd.html) || [vsftpd](https://www.archlinux.org/packages/?name=vsftpd)

*   **[SSH](/index.php/SSH "SSH")** — SFTP is a network protocol that provides file access, file transfer, and file management over any reliable data stream.

	[https://www.openssh.com](https://www.openssh.com) || [openssh](https://www.archlinux.org/packages/?name=openssh)

#### BitTorrent clients

See also [Wikipedia:Comparison of BitTorrent clients](https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients "wikipedia:Comparison of BitTorrent clients").

##### Console

Can be used as-is via command line, but all have a choice of front-end options as well.

*   **[aria2](/index.php/Aria2 "Aria2")** — Lightweight download utility that supports simultaneous adaptive downloading via HTTP(S), FTP, BitTorrent (DHT, PEX, MSE/PE) protocols and Metalink. It can run as a daemon controlled via a built-in JSON-RPC or XML-RPC interface.

	[http://aria2.sourceforge.net/](http://aria2.sourceforge.net/) || [aria2](https://www.archlinux.org/packages/?name=aria2)

*   **btpd** — The BitTorrent Protocol Daemon.

	[https://github.com/btpd/btpd](https://github.com/btpd/btpd) || [btpd](https://aur.archlinux.org/packages/btpd/)

*   **Ctorrent** — CTorrent is a BitTorrent client implemented in C++ to be lightweight and quick.

	[http://www.rahul.net/dholmes/ctorrent/](http://www.rahul.net/dholmes/ctorrent/) || [enhanced-ctorrent](https://aur.archlinux.org/packages/enhanced-ctorrent/)

*   **[MLDonkey](https://en.wikipedia.org/wiki/MLDonkey "wikipedia:MLDonkey")** — Multi-protocol P2P client that supports BitTorrent, HTTP, FTP, eDonkey and Direct Connect.

	[http://mldonkey.sourceforge.net/](http://mldonkey.sourceforge.net/) || [mldonkey](https://www.archlinux.org/packages/?name=mldonkey)

*   **[rTorrent](/index.php/RTorrent "RTorrent")** — Simple and lightweight ncurses BitTorrent client. Requires [libtorrent](https://www.archlinux.org/packages/?name=libtorrent) backend.

	[https://rakshasa.github.io/rtorrent/](https://rakshasa.github.io/rtorrent/) || [rtorrent](https://www.archlinux.org/packages/?name=rtorrent)

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with a daemon version, GTK+, Qt GUI, web and CLI front-ends.

	[http://transmissionbt.com/](http://transmissionbt.com/) || [transmission-cli](https://www.archlinux.org/packages/?name=transmission-cli) (includes backend, daemon, command-line interface, and a Web UI interface)

##### Graphical

###### libtorrent-rasterbar backend

*   **[Deluge](/index.php/Deluge "Deluge")** — User-friendly BitTorrent client written in PyGTK that can run as a daemon.

	[http://deluge-torrent.org/](http://deluge-torrent.org/) || [deluge](https://www.archlinux.org/packages/?name=deluge)

*   **FatRat** — Qt based download manager with support for HTTP, FTP, SFTP, BitTorrent, rapidshare and more. Written in C++.

	[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat-git](https://aur.archlinux.org/packages/fatrat-git/)

*   **[qBittorrent](https://en.wikipedia.org/wiki/qBittorrent "wikipedia:qBittorrent")** — Open source (GPLv2) BitTorrent client that strongly resembles µtorrent.

	[http://www.qbittorrent.org/](http://www.qbittorrent.org/) || [qbittorrent](https://www.archlinux.org/packages/?name=qbittorrent) [qbittorrent-nox](https://www.archlinux.org/packages/?name=qbittorrent-nox)

*   **[Tribler](https://en.wikipedia.org/wiki/Tribler "wikipedia:Tribler")** — 4th generation file sharing system bittorrent client.

	[http://www.tribler.org](http://www.tribler.org) || [tribler](https://aur.archlinux.org/packages/tribler/)

###### Other

*   **[Ktorrent](/index.php/Ktorrent "Ktorrent")** — Feature-rich BitTorrent client for KDE.

	[https://www.kde.org/applications/internet/ktorrent/](https://www.kde.org/applications/internet/ktorrent/) || [ktorrent](https://www.archlinux.org/packages/?name=ktorrent)

*   **Tixati** — P2P client that uses the BitTorrent protocol.

	[http://www.tixati.com](http://www.tixati.com) || [tixati](https://aur.archlinux.org/packages/tixati/)

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with daemon version, GTK+, Qt GUI, web and CLI front-ends.

	[http://transmissionbt.com/](http://transmissionbt.com/) || [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk) [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt) [transmission-remote-gtk](https://www.archlinux.org/packages/?name=transmission-remote-gtk) (remote clients work with the daemon in the -cli package)

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

*   **Nicotine+** — A graphical client for the Soulseek P2P network.

	[https://www.nicotine-plus.org/](https://www.nicotine-plus.org/) || [nicotine-plus-git](https://aur.archlinux.org/packages/nicotine-plus-git/)

*   **Sendanywhere** — GTK2 client for the cross platform P2P file sharing service, Sendanywhere. Allow users to send files of any type and size to other Android, iOS, and Desktop devices.

	[https://www.send-anywhere.com](https://www.send-anywhere.com) || [sendanywhere](https://aur.archlinux.org/packages/sendanywhere/)

#### Pastebin clients

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

*   **imgur** — A CLI client which can upload image to [imgur.com](http://imgur.com) image sharing service.

	[http://imgur.com/apps](http://imgur.com/apps) || [imgur](https://aur.archlinux.org/packages/imgur/)

*   **Ix** — Client for the ix.io pastebin.

	[http://ix.io](http://ix.io) || [ix](https://aur.archlinux.org/packages/ix/)

*   **Pastebinit** — Really small Python script that acts as a Pastebin client. Servers: [pastie.org](http://pastie.org/), [paste.kde.org](https://paste.kde.org/), [paste.debian.net](http://paste.debian.net/), [paste.ubuntu.com](http://paste.ubuntu.com/) and others (for a full list see `pastebinit -l`).

	[http://launchpad.net/pastebinit](http://launchpad.net/pastebinit) || [pastebinit](https://www.archlinux.org/packages/?name=pastebinit)

*   **paste-binouse** — C++ standalone pastebin web server

	[https://github.com/abique/paste-binouse](https://github.com/abique/paste-binouse) || [paste-binouse-git](https://aur.archlinux.org/packages/paste-binouse-git/)

*   **[pbpst](/index.php/Pbpst "Pbpst")** — A small tool to interact with pb instances (eg [ptpb.pw](https://ptpb.pw)).

	[https://github.com/HalosGhost/pbpst](https://github.com/HalosGhost/pbpst) || [pbpst](https://www.archlinux.org/packages/?name=pbpst) [pbpst-git](https://aur.archlinux.org/packages/pbpst-git/)

*   **ruby-haste** — Client for [hastebin.com](http://hastebin.com/).

	[https://github.com/seejohnrun/haste-client](https://github.com/seejohnrun/haste-client) || [ruby-haste](https://aur.archlinux.org/packages/ruby-haste/) [ruby-haste-git](https://aur.archlinux.org/packages/ruby-haste-git/)

*   **Uppity** — The pastebin client with an attitude.

	[https://github.com/Kiwi/Uppity](https://github.com/Kiwi/Uppity) || [uppity-git](https://aur.archlinux.org/packages/uppity-git/)

*   **Wgetpaste** — Bash script that automates pasting to a number of pastebin services. Servers: [pastebin.ca](http://pastebin.ca/), [codepad.org](http://codepad.org/), [dpaste.com](http://dpaste.com/) and [pastebin.osuosl.org](http://pastebin.osuosl.org/).

	[http://wgetpaste.zlin.dk/](http://wgetpaste.zlin.dk/) || [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste)

### Communication

#### Email clients

See also [Wikipedia:Comparison of email clients](https://en.wikipedia.org/wiki/Comparison_of_email_clients "wikipedia:Comparison of email clients")

##### Console

*   **alot** — An experimental terminal MUA based on [notmuch mail](http://notmuchmail.org/). It is written in python using the [urwid](http://urwid.org/) toolkit.

	[https://github.com/pazz/alot](https://github.com/pazz/alot) || [alot](https://aur.archlinux.org/packages/alot/)

*   **[Alpine](/index.php/Alpine "Alpine")** — Fast, easy-to-use and Apache-licensed email client based on [Pine](https://en.wikipedia.org/wiki/Pine_(email_client) "wikipedia:Pine (email client)").

	[http://www.washington.edu/alpine/](http://www.washington.edu/alpine/) || [alpine](https://aur.archlinux.org/packages/alpine/)

*   **[S-nail](/index.php/S-nail "S-nail")** — a mail processing system with a command syntax reminiscent of *ed* with lines replaced by messages. Provides the functionality of [mailx](https://en.wikipedia.org/wiki/mailx "wikipedia:mailx").

	[https://www.sdaoden.eu/code.html#s-mailx](https://www.sdaoden.eu/code.html#s-mailx) || [s-nail](https://www.archlinux.org/packages/?name=s-nail)

*   **mu/mu4e** — Email indexer (mu) and client for emacs (mu4e). Xapian based for fast searches.

	[http://www.djcbsoftware.nl/code/mu/mu4e.html](http://www.djcbsoftware.nl/code/mu/mu4e.html) || [mu](https://www.archlinux.org/packages/?name=mu)

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

*   **Astroid** — A lightweight and blazingly fast e-mail client for [Notmuch](/index.php/Notmuch "Notmuch"). Written using C++ and the GTK+ toolkit.

	[https://github.com/astroidmail/astroid](https://github.com/astroidmail/astroid) || [astroid](https://aur.archlinux.org/packages/astroid/)

*   **Balsa** — Simple and light email client for GNOME.

	[https://pawsa.fedorapeople.org/balsa/](https://pawsa.fedorapeople.org/balsa/) || [balsa](https://www.archlinux.org/packages/?name=balsa)

*   **[Claws Mail](https://en.wikipedia.org/wiki/Claws_Mail "wikipedia:Claws Mail")** — Lightweight GTK-based email client and news reader.

	[http://claws-mail.org/](http://claws-mail.org/) || [claws-mail](https://www.archlinux.org/packages/?name=claws-mail)

*   **[Evolution](/index.php/Evolution "Evolution")** — Mature and feature-rich e-mail client that is part of the GNOME project. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution](https://www.archlinux.org/packages/?name=evolution)

*   **Geary** — Simple desktop mail client built in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

	[https://wiki.gnome.org/Apps/Geary](https://wiki.gnome.org/Apps/Geary) || [geary](https://www.archlinux.org/packages/?name=geary)

*   **Hiri** — An Exchange ready mail client aiming to replace Outlook (QT5)

	[https://www.hiri.com/](https://www.hiri.com/) || [hiri](https://aur.archlinux.org/packages/hiri/)

*   **[Kmail](https://en.wikipedia.org/wiki/Kmail "wikipedia:Kmail")** — Mature and feature-rich email client. Part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[https://www.kde.org/applications/internet/kmail/](https://www.kde.org/applications/internet/kmail/) || [kmail](https://www.archlinux.org/packages/?name=kmail)

*   **Mailspring** — Fork of Nylas Mail

	[https://getmailspring.com/](https://getmailspring.com/) || [mailspring](https://aur.archlinux.org/packages/mailspring/)

*   **Nylas Mail** — A new mail client, built on the modern web and designed to be extended.

	[https://www.nylas.com/nylas-mail/](https://www.nylas.com/nylas-mail/) || [nylas-mail-bin](https://aur.archlinux.org/packages/nylas-mail-bin/), [nylas-mail-git](https://aur.archlinux.org/packages/nylas-mail-git/)

*   **openWMail** — The missing desktop client for Gmail & Google Inbox.

	[https://openwmail.github.io/](https://openwmail.github.io/) || [openwmail](https://aur.archlinux.org/packages/openwmail/)

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

*   **Wavebox** — The next generation of web-desktop communication (non free, trial Pro for 14 days).

	[https://wavebox.io/](https://wavebox.io/) || [wavebox-bin](https://aur.archlinux.org/packages/wavebox-bin/)

#### Mail servers

See also [Wikipedia:Comparison of e-mail servers](https://en.wikipedia.org/wiki/Comparison_of_e-mail_servers "wikipedia:Comparison of e-mail servers").

*   **[Dovecot](/index.php/Dovecot "Dovecot")** — An IMAP and POP3 server written with security primarily in mind.

	[http://dovecot.org/](http://dovecot.org/) || [dovecot](https://www.archlinux.org/packages/?name=dovecot)

#### Instant messaging

See also [Wikipedia:Comparison of instant messaging protocols](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_protocols "wikipedia:Comparison of instant messaging protocols").

This section lists all software with [instant messaging](https://en.wikipedia.org/wiki/Instant_messaging "wikipedia:Instant messaging") support. Particularly, that are client and server applications.

##### IRC clients

See also [Wikipedia:Comparison of Internet Relay Chat clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients "wikipedia:Comparison of Internet Relay Chat clients").

**Note:** There are IRC web interfaces and many IM clients also support IRC.

###### Console

*   **[BitchX](https://en.wikipedia.org/wiki/BitchX "wikipedia:BitchX")** — Console-based IRC client developed from the popular [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

	[http://www.bitchx.org/](http://www.bitchx.org/) || [bitchx-git](https://aur.archlinux.org/packages/bitchx-git/)

*   **ERC** — Powerful, modular, and extensible IRC client for [Emacs](/index.php/Emacs "Emacs").

	[http://savannah.gnu.org/projects/erc/](http://savannah.gnu.org/projects/erc/) || included with [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)")** — Featherweight IRC client, literally `tail -f` the conversation and `echo` back your replies to a file.

	[https://tools.suckless.org/ii/](https://tools.suckless.org/ii/) || [ii](https://aur.archlinux.org/packages/ii/)

*   **Ircfs** — File system interface to IRC written in [Limbo](http://limbo.cat-v.org).

	[https://bitbucket.org/mjl/ircfs](https://bitbucket.org/mjl/ircfs) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=ircfs)</small>

*   **[Irssi](/index.php/Irssi "Irssi")** — Highly-configurable ncurses-based IRC client.

	[https://irssi.org/](https://irssi.org/) || [irssi](https://www.archlinux.org/packages/?name=irssi)

*   **ScrollZ** — Advanced IRC client based on [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

	[http://www.scrollz.info/](http://www.scrollz.info/) || [scrollz](https://aur.archlinux.org/packages/scrollz/)

*   **sic** — Extremely simple IRC client, similar to [ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)").

	[https://tools.suckless.org/sic/](https://tools.suckless.org/sic/) || [sic](https://aur.archlinux.org/packages/sic/)

*   **[WeeChat](https://en.wikipedia.org/wiki/WeeChat "wikipedia:WeeChat")** — Modular, lightweight ncurses-based IRC client.

	[https://weechat.org/](https://weechat.org/) || [weechat](https://www.archlinux.org/packages/?name=weechat)

###### Graphical

*   **[ChatZilla](https://en.wikipedia.org/wiki/ChatZilla "wikipedia:ChatZilla")** — Clean, easy to use and highly extensible Internet Relay Chat (IRC) client, built on the Mozilla platform using [XULRunner](https://en.wikipedia.org/wiki/XULRunner "wikipedia:XULRunner").

	[http://chatzilla.hacksrus.com/](http://chatzilla.hacksrus.com/) || [chatzilla](https://aur.archlinux.org/packages/chatzilla/)

*   **HexChat** — Fork of XChat for Linux and Windows.

	[https://hexchat.github.io/](https://hexchat.github.io/) || [hexchat](https://www.archlinux.org/packages/?name=hexchat)

*   **[Konversation](https://en.wikipedia.org/wiki/Konversation "wikipedia:Konversation")** — Qt-based IRC client for the KDE desktop.

	[https://konversation.kde.org/](https://konversation.kde.org/) || [konversation](https://www.archlinux.org/packages/?name=konversation)

*   **[KVIrc](https://en.wikipedia.org/wiki/KVIrc "wikipedia:KVIrc")** — Qt-based IRC client featuring extensive themes support.

	[http://kvirc.net/](http://kvirc.net/) || [kvirc-git](https://aur.archlinux.org/packages/kvirc-git/)

*   **Loqui** — GTK+ IRC client with only one dependency: [GNet](https://wiki.gnome.org/Projects/GNetLibrary).

	[https://launchpad.net/loqui](https://launchpad.net/loqui) || [loqui](https://aur.archlinux.org/packages/loqui/)

*   **LostIRC** — Simple GTK+ IRC client with tab-autocompletion, multiple server support, logging and others.

	[http://lostirc.sourceforge.net](http://lostirc.sourceforge.net) || [lostirc](https://aur.archlinux.org/packages/lostirc/)

*   **Polari** — Simple IRC client by the GNOME project.

	[https://wiki.gnome.org/Apps/Polari/](https://wiki.gnome.org/Apps/Polari/) || [polari](https://www.archlinux.org/packages/?name=polari)

*   **[Quassel](/index.php/Quassel "Quassel")** — Modern, cross-platform, distributed IRC client.

	[http://quassel-irc.org/](http://quassel-irc.org/) || [quassel-core](https://www.archlinux.org/packages/?name=quassel-core) [quassel-client](https://www.archlinux.org/packages/?name=quassel-client) [quassel-monolithic](https://www.archlinux.org/packages/?name=quassel-monolithic)

*   **[Smuxi](https://en.wikipedia.org/wiki/Smuxi "wikipedia:Smuxi")** — Cross-platform IRC client that also supports Twitter, Google Talk and Jabber / XMPP.

	[https://smuxi.im/](https://smuxi.im/) || [smuxi](https://www.archlinux.org/packages/?name=smuxi)

##### XMPP (Jabber) clients

See also [Wikipedia:XMPP](https://en.wikipedia.org/wiki/XMPP "wikipedia:XMPP") and [Wikipedia:Comparison of instant messaging clients#XMPP-related features](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients#XMPP-related_features "wikipedia:Comparison of instant messaging clients").

###### Console

*   **Freetalk** — Console-based Jabber client.

	[https://www.gnu.org/software/freetalk/](https://www.gnu.org/software/freetalk/) || [freetalk](https://www.archlinux.org/packages/?name=freetalk)

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

*   **sat-jp** — CLI frontend for Salut à Toi, multi-purpose XMPP client

	[https://salut-a-toi.org](https://salut-a-toi.org) || [sat-jp](https://aur.archlinux.org/packages/sat-jp/)

*   **xmpp-client** — A minimalist XMPP client with OTR support.

	[https://github.com/agl/xmpp-client](https://github.com/agl/xmpp-client) || [go-xmpp-client](https://aur.archlinux.org/packages/go-xmpp-client/)

###### Graphical

*   **Dino** — A modern, easy to use XMPP client, with PGP and OMEMO support.

	[https://github.com/dino/dino](https://github.com/dino/dino) || [dino-git](https://aur.archlinux.org/packages/dino-git/)

*   **[Gajim](/index.php/Gajim "Gajim")** — Jabber client written in PyGTK.

	[https://gajim.org/](https://gajim.org/) || [gajim](https://www.archlinux.org/packages/?name=gajim)

*   **[Psi](https://en.wikipedia.org/wiki/Psi_(instant_messaging_client) "wikipedia:Psi (instant messaging client)")** — Qt-based Jabber client which supports video conferencing.

	[http://psi-im.org/](http://psi-im.org/) || [psi-git](https://aur.archlinux.org/packages/psi-git/)

*   **Psi+** — Enhanced version of the Psi Jabber client with many new [features](http://psi-plus.com/wiki/en:features#differences_between_psi_beta_version_and_the_official_psi_015-dev_version).

	[http://psi-plus.com/](http://psi-plus.com/) || [psi-plus-git](https://aur.archlinux.org/packages/psi-plus-git/)

*   **[Tkabber](https://en.wikipedia.org/wiki/Tkabber "wikipedia:Tkabber")** — Easy to hack feature-rich XMPP client by the author of the ejabberd XMPP server.

	[http://tkabber.jabber.ru/](http://tkabber.jabber.ru/) || [tkabber](https://www.archlinux.org/packages/?name=tkabber)

##### XMPP servers

See also [Wikipedia:Comparison of XMPP server software](https://en.wikipedia.org/wiki/Comparison_of_XMPP_server_software "wikipedia:Comparison of XMPP server software").

*   **[Prosody](/index.php/Prosody "Prosody")** — An XMPP server written in the [Lua](http://www.lua.org/) programming language. Prosody is designed to be lightweight and highly extensible. It is licensed under a permissive [MIT license](http://prosody.im/source/mit).

	[http://prosody.im/](http://prosody.im/) || [prosody](https://www.archlinux.org/packages/?name=prosody)

*   **Ejabberd** — Robust, scalable and extensible XMPP Server written in Erlang

	[https://www.ejabberd.im/](https://www.ejabberd.im/) || [ejabberd](https://www.archlinux.org/packages/?name=ejabberd)

*   **[Jabberd2](/index.php/Jabberd2 "Jabberd2")** — An XMPP server written in the C language and licensed under the GNU General Public License. It was inspired by jabberd14.

	[http://jabberd2.org](http://jabberd2.org) || [jabberd2](https://aur.archlinux.org/packages/jabberd2/)

*   **[Openfire](/index.php/Openfire "Openfire")** — An XMPP IM multiplatform server written in Java

	[http://www.igniterealtime.org/projects/openfire/](http://www.igniterealtime.org/projects/openfire/) || [openfire](https://www.archlinux.org/packages/?name=openfire)

##### Other

*   **Ricochet** — Anonymous peer-to-peer instant messaging system built on [Tor](/index.php/Tor "Tor") hidden services.

	[https://ricochet.im/](https://ricochet.im/) || [ricochet](https://aur.archlinux.org/packages/ricochet/)

*   **Synapse** — Reference homeserver for the matrix protocol.

	[https://github.com/matrix-org/synapse](https://github.com/matrix-org/synapse) || [matrix-synapse](https://www.archlinux.org/packages/?name=matrix-synapse)

##### Multi-protocol clients

See also [Wikipedia:Comparison of instant messaging clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients").

**Note:** All messengers, that support several networks by means of direct connections to them, belong to this section.

Many clients listed here (including Pidgin and all its forks) support multiple IM networks via [libpurple](https://en.wikipedia.org/wiki/libpurple "wikipedia:libpurple"). The number of networks supported by these clients is very large but they (like any multiprotocol clients) usually have very limited or no support for network-specific features.

###### Console

*   **BarnOwl** — Ncurses-based chat client with support for the Zephyr, Jabber, IRC, and Twitter protocols.

	[http://barnowl.mit.edu/](http://barnowl.mit.edu/) || [barnowl](https://aur.archlinux.org/packages/barnowl/)

*   **[Bitlbee](/index.php/Bitlbee "Bitlbee")** — IRC client that provides a gateway to popular chat networks (XMPP, Yahoo, ICQ and Twitter).

	[http://bitlbee.org/](http://bitlbee.org/) || [bitlbee](https://www.archlinux.org/packages/?name=bitlbee)

*   **[CenterIM](https://en.wikipedia.org/wiki/Centericq "wikipedia:Centericq")** — Fork of CenterICQ, a text mode menu- and window-driven IM interface.

	[http://centerim.org/](http://centerim.org/) || [centerim](https://www.archlinux.org/packages/?name=centerim)

*   **[Finch](/index.php/Pidgin "Pidgin")** — Ncurses-based chat client that uses libpurple and supports all its protocols.

	[http://developer.pidgin.im/wiki/Using%20Finch](http://developer.pidgin.im/wiki/Using%20Finch) || [finch](https://www.archlinux.org/packages/?name=finch)

*   **[naim](https://en.wikipedia.org/wiki/naim_(software) "wikipedia:naim (software)")** — Ncurses chat client with support for ICQ, IRC and the Lily CMC.

	[https://github.com/nmlorg/naim](https://github.com/nmlorg/naim) || [naim](https://www.archlinux.org/packages/?name=naim)

*   **pork** — Programmable, ncurses-based IRC client that mostly looks and feels like ircII.

	[http://dev.ojnk.net/](http://dev.ojnk.net/) || [pork](https://www.archlinux.org/packages/?name=pork)

*   **[Tox](/index.php/Tox "Tox")** — Tox is a distributed, secure messenger with audio and video chat capabilities.

	[https://tox.chat/](https://tox.chat/) || see [Tox](/index.php/Tox "Tox")

###### Graphical

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) framework.

	[https://wiki.gnome.org/Apps/Empathy](https://wiki.gnome.org/Apps/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **[Instantbird](https://en.wikipedia.org/wiki/Instantbird "wikipedia:Instantbird")** — Multi-protocol chat client using Mozilla's XUL and libpurple.

	[http://instantbird.com/](http://instantbird.com/) || [instantbird](https://aur.archlinux.org/packages/instantbird/)

*   **[Kopete](https://en.wikipedia.org/wiki/Kopete "wikipedia:Kopete")** — User-friendly IM supporting ICQ, Yahoo, Jabber, Gadu-Gadu, Novell GroupWise Messenger, and other IM networks. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

	[https://userbase.kde.org/Kopete](https://userbase.kde.org/Kopete) || [kopete](https://www.archlinux.org/packages/?name=kopete)

*   **[KDE Telepathy](/index.php/KDE#KDE_Telepathy "KDE")** — KDE instant messaging client using the [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) framework. Meant as a replacement for Kopete.

	[https://userbase.kde.org/Telepathy](https://userbase.kde.org/Telepathy) || [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta)

*   **Licq** — Instant messaging client for UNIX supporting multiple protocols (currently ICQ and Jabber).

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

*   **[Blink](https://en.wikipedia.org/wiki/Blink_(SIP_client) "wikipedia:Blink (SIP client)")** — State of the art, easy to use SIP client.

	[http://icanblink.com/](http://icanblink.com/) || [blink](https://aur.archlinux.org/packages/blink/)

*   **[Ekiga](https://en.wikipedia.org/wiki/Ekiga "wikipedia:Ekiga")** — VoIP and video conferencing application with full SIP and H.323 support (formerly known as GNOME Meeting).

	[http://www.ekiga.org/](http://www.ekiga.org/) || [ekiga](https://www.archlinux.org/packages/?name=ekiga)

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) "wikipedia:Empathy (software)")** — GNOME instant messenger client using the Telepathy framework with SIP support (using the Sofia-SIP library).

	[https://wiki.gnome.org/Apps/Empathy](https://wiki.gnome.org/Apps/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **[Jitsi](https://en.wikipedia.org/wiki/Jitsi "wikipedia:Jitsi")** — Audio/video SIP VoIP phone and instant messenger written in Java (formerly SIP-Communicator).

	[https://jitsi.org/](https://jitsi.org/) || [jitsi](https://aur.archlinux.org/packages/jitsi/)

*   **[KPhone](https://en.wikipedia.org/wiki/KPhone "wikipedia:KPhone")** — Qt SIP User Agent with voice, video and text messaging support.

	[https://sourceforge.net/projects/kphone/](https://sourceforge.net/projects/kphone/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=kphone)</small>

*   **[Linphone](https://en.wikipedia.org/wiki/Linphone "wikipedia:Linphone")** — VoIP phone application for communicating freely with people over the internet, with voice, video, and text instant messaging.

	[http://www.linphone.org/](http://www.linphone.org/) || [linphone](https://www.archlinux.org/packages/?name=linphone)

*   **[Twinkle](https://en.wikipedia.org/wiki/Twinkle_(software) "wikipedia:Twinkle (software)")** — Qt softphone for VoIP and IM communication using SIP.

	[http://www.twinklephone.com/](http://www.twinklephone.com/) || [twinkle](https://aur.archlinux.org/packages/twinkle/)

*   **[X-Lite](https://en.wikipedia.org/wiki/X-Lite "wikipedia:X-Lite")** — Proprietary freeware VoIP soft phone that uses SIP.

	[http://www.counterpath.com/x-lite/](http://www.counterpath.com/x-lite/) || [xlite_bin](https://aur.archlinux.org/packages/xlite_bin/)

###### Other

*   **[Skype](/index.php/Skype "Skype")** — Popular but proprietary application for voice and video communication.

	[https://www.skype.com/](https://www.skype.com/) || [skypeforlinux-bin](https://aur.archlinux.org/packages/skypeforlinux-bin/)

*   **Hangups** — A third-party instant messaging client for Google Hangouts

	[https://github.com/tdryer/hangups](https://github.com/tdryer/hangups) || [hangups-git](https://aur.archlinux.org/packages/hangups-git/)

*   **[Mumble](/index.php/Mumble "Mumble")** — Voice chat application similar to TeamSpeak.

	[http://mumble.sourceforge.net/](http://mumble.sourceforge.net/) || [mumble](https://www.archlinux.org/packages/?name=mumble)

*   **[TeamSpeak](/index.php/TeamSpeak "TeamSpeak")** — Proprietary VoIP application with gamers as its target audience.

	[http://www.teamspeak.com/](http://www.teamspeak.com/) || [teamspeak3](https://www.archlinux.org/packages/?name=teamspeak3)

*   **[Discord](https://en.wikipedia.org/wiki/Discord_(software) "wikipedia:Discord (software)")** — All-in-one voice and text chat for gamers that’s free, secure, and works on both your desktop and phone.

	[https://discordapp.com/](https://discordapp.com/) || [discord](https://aur.archlinux.org/packages/discord/)

*   **GameVox** — Voice communication for your gaming community, partly based on Mumble source code.

	[https://www.gamevox.com/](https://www.gamevox.com/) || [gamevox](https://aur.archlinux.org/packages/gamevox/)

###### Multi-protocol

*   **[Ring](https://en.wikipedia.org/wiki/Ring_(software) "wikipedia:Ring (software)")** — Open-source SIP/IAX2 compatible softphone with PulseAudio support (formerly known as SFLphone).

	[https://ring.cx/](https://ring.cx/) || [ring-daemon](https://aur.archlinux.org/packages/ring-daemon/)

##### Voice servers

*   **[Murmur](/index.php/Murmur "Murmur")** — The voice chat application server for Mumble.

	[http://mumble.sourceforge.net/](http://mumble.sourceforge.net/) || [murmur](https://www.archlinux.org/packages/?name=murmur)

##### Utilities

*   **SIPp** — Open source test tool and traffic generator for the SIP protocol.

	[http://sipp.sourceforge.net/](http://sipp.sourceforge.net/) || [sipp](https://aur.archlinux.org/packages/sipp/)

### News, RSS, and blogs

#### News aggregators

[RSS](https://en.wikipedia.org/wiki/RSS aggregators. See also [Wikipedia:Comparison of feed aggregators](https://en.wikipedia.org/wiki/Comparison_of_feed_aggregators "wikipedia:Comparison of feed aggregators").

##### Console

*   **[Canto](https://en.wikipedia.org/wiki/Canto_(news_aggregator) "wikipedia:Canto (news aggregator)")** — Ncurses RSS aggregator.

	[http://codezen.org/canto/](http://codezen.org/canto/) || [canto-next-git](https://aur.archlinux.org/packages/canto-next-git/)

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

	[http://gnus.org/](http://gnus.org/) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[Newsbeuter](/index.php/Newsbeuter "Newsbeuter")** — Ncurses RSS aggregator with layout and keybinding similar to the [Mutt](/index.php/Mutt "Mutt") email client.

	[http://newsbeuter.org](http://newsbeuter.org) || [newsboat](https://www.archlinux.org/packages/?name=newsboat)

*   **Rawdog** — "RSS Aggregator Without Delusions Of Grandeur" that parses RSS/CDF/Atom feeds into a static HTML page of articles in chronological order.

	[http://offog.org/code/rawdog.html](http://offog.org/code/rawdog.html) || [rawdog](https://www.archlinux.org/packages/?name=rawdog)

*   **Snownews** — Text mode RSS news reader.

	[http://kiza.kcore.de/software/snownews/](http://kiza.kcore.de/software/snownews/) || [snownews](https://www.archlinux.org/packages/?name=snownews)

##### Graphical

*   **[Akregator](https://en.wikipedia.org/wiki/Kontact#News_Feed_Aggregator "wikipedia:Kontact")** — News aggregator for KDE, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[https://www.kde.org/applications/internet/akregator/](https://www.kde.org/applications/internet/akregator/) || [akregator](https://www.archlinux.org/packages/?name=akregator)

*   **[Evolution](/index.php/Evolution "Evolution") RSS** — Plugin for Evolution Mail that enables reading of RSS/RDF/ATOM feeds.

	[http://gnome.eu.org/index.php/Evolution_RSS_Reader_Plugin](http://gnome.eu.org/index.php/Evolution_RSS_Reader_Plugin) || [evolution-rss](https://www.archlinux.org/packages/?name=evolution-rss)

*   **FeedReader** — Modern desktop application designed to complement existing web-based RSS accounts.

	[http://jangernert.github.io/FeedReader/](http://jangernert.github.io/FeedReader/) || [feedreader](https://aur.archlinux.org/packages/feedreader/)

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

	[https://www.open-tickr.net/](https://www.open-tickr.net/) || [tickr](https://aur.archlinux.org/packages/tickr/)

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

*   **Vocal** — Simple Podcast Client for the Modern Desktop (GTK+).

	[https://launchpad.net/vocal](https://launchpad.net/vocal) || [vocal](https://aur.archlinux.org/packages/vocal/)

#### Usenet newsreaders & newsgrabbers

Some [email clients](#Email_clients) also support NNTP. This section mainly lists NNTP-only client.

See also: [Wikipedia:List of Usenet newsreaders](https://en.wikipedia.org/wiki/List_of_Usenet_newsreaders "wikipedia:List of Usenet newsreaders"), [Wikipedia:Comparison of Usenet newsreaders](https://en.wikipedia.org/wiki/Comparison_of_Usenet_newsreaders "wikipedia:Comparison of Usenet newsreaders").

*   **lottanzb** — A *SABnzbd* (Usenet binary downloader) GUI front-end written in PyGTK

	[https://launchpad.net/lottanzb/](https://launchpad.net/lottanzb/) || [lottanzb](https://aur.archlinux.org/packages/lottanzb/)

*   **nn** — Alternative more user-friendly(curses-based) Usenet newsreader for UNIX.

	[http://www.nndev.org/](http://www.nndev.org/) || [nn](https://aur.archlinux.org/packages/nn/)

*   **[NZBGet](/index.php/NZBGet "NZBGet")** — Usenet binary downloader for .nzb files with web and CLI interface.

	[https://nzbget.net/](https://nzbget.net/) || [nzbget](https://www.archlinux.org/packages/?name=nzbget)

*   **[pan](https://en.wikipedia.org/wiki/Pan_(newsreader) "wikipedia:Pan (newsreader)")** — A GTK2 Usenet newsreader that's good at both text and binaries.

	[http://pan.rebelbase.com/](http://pan.rebelbase.com/) || [pan](https://www.archlinux.org/packages/?name=pan)

*   **[SABnzbd](/index.php/SABnzbd "SABnzbd")** — An open-source binary newsreader written in Python.

	[https://sabnzbd.org/](https://sabnzbd.org/) || [sabnzbd](https://aur.archlinux.org/packages/sabnzbd/) [sabnzbd-git](https://aur.archlinux.org/packages/sabnzbd-git/)

*   **[tin](https://en.wikipedia.org/wiki/Tin_(newsreader) "wikipedia:Tin (newsreader)")** — A cross-platform threaded NNTP and spool based UseNet newsreader.

	[http://tin.org/](http://tin.org/) || [tin](https://aur.archlinux.org/packages/tin/)

*   **trn** — A text-based Threaded Usenet newsreader.

	[http://trn.sourceforge.net/](http://trn.sourceforge.net/) || [trn](https://aur.archlinux.org/packages/trn/)

*   **xrn** — Usenet newsreader for X Window System.

	[http://www.mit.edu/people/jik/software/xrn.html](http://www.mit.edu/people/jik/software/xrn.html) || [xrn](https://aur.archlinux.org/packages/xrn/)

#### Blog engines

See also [Wikipedia:Blog software](https://en.wikipedia.org/wiki/Blog_software "wikipedia:Blog software") and [Wikipedia:List of content management systems](https://en.wikipedia.org/wiki/List_of_content_management_systems "wikipedia:List of content management systems").

**Note:** Content managers, social networks, and blog publishers overlap in many functions.

*   **[Diaspora](/index.php/Diaspora "Diaspora")** — A distributed privacy aware social network.

	[https://diasporafoundation.org](https://diasporafoundation.org) || [diaspora-mysql](https://aur.archlinux.org/packages/diaspora-mysql/) or [diaspora-postgresql](https://aur.archlinux.org/packages/diaspora-postgresql/)

*   **[Drupal](/index.php/Drupal "Drupal")** — A PHP-based content management platform.

	[http://www.drupal.org/](http://www.drupal.org/) || [drupal](https://www.archlinux.org/packages/?name=drupal)

*   **[Ghost](/index.php/Ghost "Ghost")** — Blogging platform written in JavaScript and distributed under the MIT License, designed to simplify the process of online publishing for individual bloggers as well as online publications.

	[https://ghost.org/](https://ghost.org/) || [ghost](https://aur.archlinux.org/packages/ghost/)

*   **[Jekyll](/index.php/Jekyll "Jekyll")** — A static blog engine, written in Ruby, which supports Markdown, textile and other formats.

	[http://jekyllrb.com/](http://jekyllrb.com/) || [jekyll](https://aur.archlinux.org/packages/jekyll/)

*   **[Joomla](/index.php/Joomla "Joomla")** — A php Content Management System (CMS) which enables you to build websites and powerful online applications.

	[http://www.joomla.org/](http://www.joomla.org/) || [joomla](https://aur.archlinux.org/packages/joomla/)

*   **Nanoblogger** — A small weblog engine written in Bash for the command line. It uses common UNIX tools such as cat, grep, and sed to create static HTML content. It is not mantained anymore.

	[http://nanoblogger.sourceforge.net/](http://nanoblogger.sourceforge.net/) || [nanoblogger](https://www.archlinux.org/packages/?name=nanoblogger)

*   **Nikola** — A static site generator written in Python, with incremental rebuilds and multiple markup formats.

	[https://getnikola.com/](https://getnikola.com/) || [nikola](https://aur.archlinux.org/packages/nikola/)

*   **Pelican** — A static site generator, powered by Python.

	[http://docs.getpelican.com/en/3.5.0/](http://docs.getpelican.com/en/3.5.0/) || [pelican](https://www.archlinux.org/packages/?name=pelican)

*   **[Wordpress](/index.php/Wordpress "Wordpress")** — Blog tool and publishing platform.

	[https://wordpress.org/](https://wordpress.org/) || [wordpress](https://www.archlinux.org/packages/?name=wordpress)

#### Microblogging clients

See also [Wikipedia:List of Twitter services and applications](https://en.wikipedia.org/wiki/List_of_Twitter_services_and_applications "wikipedia:List of Twitter services and applications").

*   **Birdie** — A beautiful Twitter client for GNU/Linux.

	[http://birdieapp.github.io/](http://birdieapp.github.io/) || [birdie-git](https://aur.archlinux.org/packages/birdie-git/)

*   **Choqok** — Microblogging client for KDE that supports Twitter.com, Pump.io, GNU social and opendesktop.org services.

	[http://choqok.gnufolks.org/](http://choqok.gnufolks.org/) || [choqok](https://www.archlinux.org/packages/?name=choqok)

*   **Corebird** — Native Gtk+ Twitter client for the Linux desktop.

	[http://corebird.baedert.org/](http://corebird.baedert.org/) || [corebird](https://aur.archlinux.org/packages/corebird/)

*   **Polly** — Linux Twitter client designed for multiple columns of multiple accounts.

	[https://launchpad.net/polly/](https://launchpad.net/polly/) || [polly](https://aur.archlinux.org/packages/polly/)

*   **Pumpa** — Pump.io client written in C++ and Qt.

	[https://pumpa.branchable.com/](https://pumpa.branchable.com/) || [pumpa-git](https://aur.archlinux.org/packages/pumpa-git/)

*   **Rainbowstream** — A powerful and fully-featured console Twitter client written in Python.

	[https://github.com/orakaro/rainbowstream](https://github.com/orakaro/rainbowstream) || [rainbowstream](https://aur.archlinux.org/packages/rainbowstream/)

*   **oysttyer** — (official fork of ttytter) An interactive console text-based command-line Twitter client written in Perl.

	[https://github.com/oysttyer/oysttyer](https://github.com/oysttyer/oysttyer) || [oysttyer-git](https://aur.archlinux.org/packages/oysttyer-git/)

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

*   **TeamViewer** — Proprietary remote desktop client. It uses its own proprietary protocol.

	[http://www.teamviewer.com/](http://www.teamviewer.com/) || [teamviewer](https://aur.archlinux.org/packages/teamviewer/)

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

	[https://github.com/mate-desktop/eom](https://github.com/mate-desktop/eom) || [eom](https://www.archlinux.org/packages/?name=eom)

*   **EyeSight** — Image viewer for the Hawaii desktop environment.

	[http://hawaiios.org/projects/eyesight/](http://hawaiios.org/projects/eyesight/) || [eyesight](https://aur.archlinux.org/packages/eyesight/)

*   **[feh](/index.php/Feh "Feh")** — Fast, lightweight image viewer that uses imlib2.

	[https://feh.finalrewind.org/](https://feh.finalrewind.org/) || [feh](https://www.archlinux.org/packages/?name=feh)

*   **GalaPix** — OpenGL-based image viewer for simultaneously viewing and zooming large collections of image files,

	[https://github.com/Galapix/galapix](https://github.com/Galapix/galapix) || [galapix](https://aur.archlinux.org/packages/galapix/)

*   **[Geeqie](https://en.wikipedia.org/wiki/Geeqie "wikipedia:Geeqie")** — Image browser and viewer (fork of GQview) that adds additional functionality such as support for RAW files.

	[http://geeqie.org/](http://geeqie.org/) || [geeqie](https://www.archlinux.org/packages/?name=geeqie)

*   **Gimmage** — Gtkmm image viewer.

	[https://sourceforge.net/projects/gimmage.berlios/](https://sourceforge.net/projects/gimmage.berlios/) || [gimmage](https://www.archlinux.org/packages/?name=gimmage)

*   **GNOME Photos** — Access, organize, and share your photos on GNOME.

	[https://wiki.gnome.org/Apps/Photos](https://wiki.gnome.org/Apps/Photos) || [gnome-photos](https://www.archlinux.org/packages/?name=gnome-photos)

*   **GPicView** — Simple and fast image viewer for X, which is part of the [LXDE](/index.php/LXDE "LXDE") desktop.

	[http://lxde.sourceforge.net/gpicview/](http://lxde.sourceforge.net/gpicview/) || GTK+ 2: [gpicview](https://www.archlinux.org/packages/?name=gpicview), GTK+ 3: [gpicview-gtk3](https://www.archlinux.org/packages/?name=gpicview-gtk3)

*   **[GQview](https://en.wikipedia.org/wiki/GQview "wikipedia:GQview")** — Image browser that features single click access to view images and move around the directory tree

	[http://gqview.sourceforge.net/](http://gqview.sourceforge.net/) || [gqview-devel](https://aur.archlinux.org/packages/gqview-devel/)

*   **[gThumb](https://en.wikipedia.org/wiki/GThumb "wikipedia:GThumb")** — Image viewer for the GNOME desktop.

	[https://wiki.gnome.org/Apps/gthumb](https://wiki.gnome.org/Apps/gthumb) || [gthumb](https://www.archlinux.org/packages/?name=gthumb)

*   **[Gwenview](https://en.wikipedia.org/wiki/Gwenview "wikipedia:Gwenview")** — Fast and easy to use image viewer for the KDE desktop.

	[http://gwenview.sourceforge.net/](http://gwenview.sourceforge.net/) || [gwenview](https://www.archlinux.org/packages/?name=gwenview)

*   **imv** — Lightweight image viewer with support for Wayland and animated GIFs which uses FreeImage.

	[https://www.github.com/eXeC64/imv/](https://www.github.com/eXeC64/imv/) || [imv](https://www.archlinux.org/packages/?name=imv)

*   **LxImage-Qt** — The LXQt image viewer.

	[https://github.com/lxde/lximage-qt](https://github.com/lxde/lximage-qt) || [lximage-qt](https://www.archlinux.org/packages/?name=lximage-qt)

*   **meh** — meh is a small, simple, super fast image viewer using raw XLib.

	[http://www.johnhawthorn.com/meh/](http://www.johnhawthorn.com/meh/) || [meh-git](https://aur.archlinux.org/packages/meh-git/)

*   **Mirage** — PyGTK image viewer featuring support for crop and resize, custom actions and a thumbnail panel.

	[https://sourceforge.net/projects/mirageiv.berlios/](https://sourceforge.net/projects/mirageiv.berlios/) || [mirage](https://www.archlinux.org/packages/?name=mirage)

*   **nomacs** — Free (GPLv3) Qt image viewer for many operating systems. It is feature-rich but starts fast and can be configured to show additional widgets or only the image.

	[http://www.nomacs.org/](http://www.nomacs.org/) || [nomacs](https://www.archlinux.org/packages/?name=nomacs)

*   **Pantheon Photos** — Image viewer for Pantheon.

	[https://launchpad.net/pantheon-photos](https://launchpad.net/pantheon-photos) || [pantheon-photos](https://www.archlinux.org/packages/?name=pantheon-photos)

*   **Phototonic** — Fast and functional image viewer and organizer (Qt).

	[https://github.com/oferkv/phototonic/](https://github.com/oferkv/phototonic/) || [phototonic](https://aur.archlinux.org/packages/phototonic/)

*   **PhotoQt** — Fast and highly configurable image viewer with a simple and nice interface.

	[http://photoqt.org/](http://photoqt.org/) || [photoqt](https://aur.archlinux.org/packages/photoqt/)

*   **Quick Image Viewer** — Very small and fast image viewer based on GTK+ and imlib2.

	[http://spiegl.de/qiv/](http://spiegl.de/qiv/) || [qiv](https://www.archlinux.org/packages/?name=qiv)

*   **Ristretto** — Fast and lightweight image viewer for the Xfce desktop environment.

	[http://docs.xfce.org/apps/ristretto/start](http://docs.xfce.org/apps/ristretto/start) || [ristretto](https://www.archlinux.org/packages/?name=ristretto)

*   **Shotwell** — A digital photo organizer designed for the GNOME desktop environment

	[https://wiki.gnome.org/Apps/Shotwell](https://wiki.gnome.org/Apps/Shotwell) || [shotwell](https://www.archlinux.org/packages/?name=shotwell)

*   **shufti** — shufti non-destructively saves and restores the zoom level, rotation, window size, desktop location and viewing area on a per-image/file location basis

	[https://github.com/danboid/shufti](https://github.com/danboid/shufti) || [shufti](https://aur.archlinux.org/packages/shufti/)

*   **[sxiv](/index.php/Sxiv "Sxiv")** — Simple image viewer based on imlib2 that works well with tiling window managers.

	[https://github.com/muennich/sxiv](https://github.com/muennich/sxiv) || [sxiv](https://www.archlinux.org/packages/?name=sxiv)

*   **Viewnior** — Minimalistic GTK+ image viewer featuring support for flipping, rotating, animations and configurable mouse actions.

	[http://siyanpanayotov.com/project/viewnior/](http://siyanpanayotov.com/project/viewnior/) || [viewnior](https://www.archlinux.org/packages/?name=viewnior)

*   **Vimiv** — An image viewer with vim-like keybindings. It is written in python3 using the Gtk3 toolkit.

	[http://karlch.github.io/vimiv](http://karlch.github.io/vimiv) || [vimiv](https://www.archlinux.org/packages/?name=vimiv)

*   **Xloadimage** — Classic X image viewer.

	[http://sioseis.ucsd.edu/xloadimage.html](http://sioseis.ucsd.edu/xloadimage.html) || [xloadimage](https://www.archlinux.org/packages/?name=xloadimage)

*   **[XnView MP](https://en.wikipedia.org/wiki/XnView "wikipedia:XnView")** — Efficient proprietary image viewer, browser and converter.

	[http://www.xnview.com/en/xnviewmp/](http://www.xnview.com/en/xnviewmp/) || [xnviewmp](https://aur.archlinux.org/packages/xnviewmp/)

*   **[xv](https://en.wikipedia.org/wiki/Xv_(software) "wikipedia:Xv (software)")** — Shareware program written by John Bradley to display and modify digital images under the X Window System. Last released in 1994.

	[http://www.trilon.com/xv/](http://www.trilon.com/xv/) || [xv](https://aur.archlinux.org/packages/xv/)

#### Graphics and image manipulation

##### Raster editors

See also [Wikipedia:Comparison of raster graphics editors](https://en.wikipedia.org/wiki/Comparison_of_raster_graphics_editors "wikipedia:Comparison of raster graphics editors") and [libgphoto2 frontends](/index.php/Libgphoto2#Other_frontend_applications_for_libgphoto2 "Libgphoto2").

*   **AzPainter** — A Painting software.

	[http://azpainter.sourceforge.jp/](http://azpainter.sourceforge.jp/) || [azpainter](https://aur.archlinux.org/packages/azpainter/)

*   **[darktable](https://en.wikipedia.org/wiki/darktable "wikipedia:darktable")** — Photography workflow and RAW development application.

	[http://www.darktable.org/](http://www.darktable.org/) || [darktable](https://www.archlinux.org/packages/?name=darktable)

*   **[RawTherapee](https://en.wikipedia.org/wiki/RawTherapee "wikipedia:RawTherapee")** — A powerful cross-platform raw image processing program.

	[http://www.rawtherapee.com/](http://www.rawtherapee.com/) || [rawtherapee](https://www.archlinux.org/packages/?name=rawtherapee)

*   **dcraw** — Converts many camera RAW formats.

	[http://www.cybercom.net/~dcoffin/dcraw/](http://www.cybercom.net/~dcoffin/dcraw/) || [dcraw](https://www.archlinux.org/packages/?name=dcraw)

*   **[digiKam](https://en.wikipedia.org/wiki/digiKam "wikipedia:digiKam")** — KDE-based image organizer with built-in editing features via a plugin architecture. digiKam asserts it is more full featured than similar applications with a larger set of image manipulation features including RAW image import and manipulation.

	[http://www.digikam.org/](http://www.digikam.org/) || [digikam](https://www.archlinux.org/packages/?name=digikam)

*   **[GIMP](/index.php/GIMP "GIMP")** — Image editing suite in the vein of proprietary editors such as [Adobe Photoshop](https://en.wikipedia.org/wiki/Adobe_Photoshop "wikipedia:Adobe Photoshop"). GIMP ([GNU](/index.php/GNU "GNU") Image Manipulation Program) has been started in the mid 1990s and has acquired a large number of [plugins](/index.php/CMYK_support_in_The_GIMP "CMYK support in The GIMP") and additional tools.

	[http://www.gimp.org/](http://www.gimp.org/) || [gimp](https://www.archlinux.org/packages/?name=gimp)

*   **G'MIC** — Full-featured open-source framework for image processing, providing several different user interfaces to convert/manipulate/filter/visualize generic image datasets, ranging from 1d scalar signals to 3d+t sequences of multi-spectral volumetric images, including 2d color images.

	[http://www.gmic.eu/](http://www.gmic.eu/) || [gmic](https://www.archlinux.org/packages/?name=gmic)

*   **[Gpaint](https://en.wikipedia.org/wiki/GNU_Paint "wikipedia:GNU Paint")** — [Paintbrush](https://en.wikipedia.org/wiki/PC_Paintbrush "wikipedia:PC Paintbrush") clone for GNOME.

	[https://www.gnu.org/software/gpaint/](https://www.gnu.org/software/gpaint/) || [gpaint](https://aur.archlinux.org/packages/gpaint/)

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

	[https://sourceforge.net/projects/sf-xpaint/](https://sourceforge.net/projects/sf-xpaint/) || [xpaint](https://aur.archlinux.org/packages/xpaint/)

Some image viewers like Ephoto, GNOME Photos, [gThumb](https://en.wikipedia.org/wiki/GThumb and [XnView MP](https://en.wikipedia.org/wiki/XnView "wikipedia:XnView") also provide some basic image manipulation functionality.

##### Vector graphics - illustration

See also [Wikipedia:Comparison of vector graphics editors](https://en.wikipedia.org/wiki/Comparison_of_vector_graphics_editors "wikipedia:Comparison of vector graphics editors").

*   **[Asymptote](https://en.wikipedia.org/wiki/Asymptote_(vector_graphics_language) "wikipedia:Asymptote (vector graphics language)")** — A descriptive vector graphics language (like PGF/TikZ and Metapost) with a C-like syntax and LaTeX support.

	[http://asymptote.sourceforge.net](http://asymptote.sourceforge.net) || [asymptote](https://www.archlinux.org/packages/?name=asymptote)

*   **[Dia](https://en.wikipedia.org/wiki/Dia_(software) "wikipedia:Dia (software)")** — GTK+-based diagram creation program.

	[https://wiki.gnome.org/Apps/Dia](https://wiki.gnome.org/Apps/Dia) || [dia](https://www.archlinux.org/packages/?name=dia)

*   **[Graphviz](https://en.wikipedia.org/wiki/Graphviz "wikipedia:Graphviz")** — Set of tools for drawing graphs in the descriptive DOT language.

	[http://www.graphviz.org](http://www.graphviz.org) || [graphviz](https://www.archlinux.org/packages/?name=graphviz)

*   **Gravit** — Vector graphics design tool - For Users of All Skills and Profession

	[https://gravit.io/](https://gravit.io/) || [gravit](https://aur.archlinux.org/packages/gravit/)

*   **[Inkscape](https://en.wikipedia.org/wiki/Inkscape "wikipedia:Inkscape")** — Vector graphics editor, with capabilities similar to [Illustrator](https://en.wikipedia.org/wiki/Adobe_Illustrator "wikipedia:Adobe Illustrator"), [CorelDraw](https://en.wikipedia.org/wiki/CorelDRAW "wikipedia:CorelDRAW"), or [Xara X](https://en.wikipedia.org/wiki/Xara_X "wikipedia:Xara X"), using the SVG (Scalable Vector Graphics) file format. Inkscape supports many advanced SVG features (markers, clones, alpha blending, etc.) and great care is taken in designing a streamlined interface. It is very easy to edit nodes, perform complex path operations, trace bitmaps and much more. It's developers also aim to maintain a thriving user and developer community by using open, community-oriented development.

	[http://inkscape.org/](http://inkscape.org/) || [inkscape](https://www.archlinux.org/packages/?name=inkscape)

*   **Mockingbot** — Prototyping & collaboration design tool .

	[http://mockingbot.com/](http://mockingbot.com/) || [mockingbot](https://aur.archlinux.org/packages/mockingbot/)

*   **[Karbon](https://en.wikipedia.org/wiki/Karbon_(software) "wikipedia:Karbon (software)")** — Vector graphics editor, part of the Calligra Suite.

	[http://www.calligra-suite.org/karbon/](http://www.calligra-suite.org/karbon/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[Pencil Project](https://en.wikipedia.org/wiki/Pencil2D "wikipedia:Pencil2D")** — An open-source GUI prototyping and mockup tool.

	[http://pencil.evolus.vn/](http://pencil.evolus.vn/) || [pencil](https://aur.archlinux.org/packages/pencil/)

*   **qasm2circ** — Quantum circuit generator for latex

	[http://www.media.mit.edu/quanta/qasm2circ/](http://www.media.mit.edu/quanta/qasm2circ/) || [qasm2circ](https://aur.archlinux.org/packages/qasm2circ/)

*   **[sK1](https://en.wikipedia.org/wiki/SK1_(program) "wikipedia:SK1 (program)")** — Replacement for Adobe Illustrator or CorelDraw, oriented for "prepress ready" PostScript & PDF output.

	[http://sk1project.net/](http://sk1project.net/) || [sk1](https://www.archlinux.org/packages/?name=sk1)

*   **[yEd](https://en.wikipedia.org/wiki/yEd "wikipedia:yEd")** — General-purpose diagramming program for flowcharts, network diagrams, UML diagrams, BPMN diagrams, mind maps, organization charts, and Entity Relationship diagrams.

	[http://www.yworks.com/en/products_yed_about.html](http://www.yworks.com/en/products_yed_about.html) || [yed](https://aur.archlinux.org/packages/yed/)

##### Vector graphics - CAD

See also [Wikipedia:List of computer-aided design editors](https://en.wikipedia.org/wiki/List_of_computer-aided_design_editors "wikipedia:List of computer-aided design editors").

*   **[BRL-CAD](https://en.wikipedia.org/wiki/BRL-CAD "wikipedia:BRL-CAD")** — Constructive solid geometry (CSG) solid modeling computer-aided design (CAD) system that includes an interactive geometry editor, ray tracing support for graphics rendering and geometric analysis, computer network distributed framebuffer support, scripting, image-processing and signal-processing tools.

	[http://brlcad.org/](http://brlcad.org/) || [brlcad](https://aur.archlinux.org/packages/brlcad/)

*   **DraftSight** — Dassault Systemes' freeware 2D CAD application. DraftSight allows users to access DWG/DXF files, regardless of which CAD software was originally used to create them.

	[http://www.3ds.com/products-services/draftsight/overview/](http://www.3ds.com/products-services/draftsight/overview/) || [draftsight](https://aur.archlinux.org/packages/draftsight/)

*   **[FreeCAD](https://en.wikipedia.org/wiki/FreeCAD "wikipedia:FreeCAD")** — CAD/CAE program, based on OpenCascade, Qt and Python with features such as macro recording, workbenches and the ability to run as server.

	[https://github.com/FreeCAD/FreeCAD](https://github.com/FreeCAD/FreeCAD) || [freecad](https://www.archlinux.org/packages/?name=freecad)

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

*   **Art of Illusion** — 3D modeling and rendering studio written in Java.

	[http://www.artofillusion.org/](http://www.artofillusion.org/) || [aoi](https://aur.archlinux.org/packages/aoi/)

*   **[Blender](https://en.wikipedia.org/wiki/Blender_(software) "wikipedia:Blender (software)")** — Fully integrated 3D graphics creation suite capable of 3D modeling, texturing, and animation, among other things.

	[http://www.blender.org/](http://www.blender.org/) || [blender](https://www.archlinux.org/packages/?name=blender)

*   **Goxel** — Open Source 3D voxel editor.

	[https://guillaumechereau.github.io/goxel/](https://guillaumechereau.github.io/goxel/) || [goxel](https://aur.archlinux.org/packages/goxel/)

*   **[MakeHuman™](https://en.wikipedia.org/wiki/MakeHuman "wikipedia:MakeHuman")** — Parametrical modeling program for creating human bodies.

	[http://www.makehuman.org/](http://www.makehuman.org/) || [makehuman](https://aur.archlinux.org/packages/makehuman/)

*   **[Sweet Home 3D](https://en.wikipedia.org/wiki/Sweet_Home_3D "wikipedia:Sweet Home 3D")** — Interior design software application for the planning and development of floor plans

	[http://sweethome3d.com/](http://sweethome3d.com/) || [sweethome3d](https://www.archlinux.org/packages/?name=sweethome3d)

*   **[POV-Ray](https://en.wikipedia.org/wiki/POV-Ray "wikipedia:POV-Ray")** — Script-based raytracer for creating 3D graphics.

	[http://www.povray.org/](http://www.povray.org/) || [povray](https://www.archlinux.org/packages/?name=povray)

*   **VoxelShop** — Extremely intuitive and powerful software to modify and create voxel objects.

	[https://blackflux.com/node/11](https://blackflux.com/node/11) || [voxelshop](https://aur.archlinux.org/packages/voxelshop/)

*   **[Wings 3D](https://en.wikipedia.org/wiki/Wings3d "wikipedia:Wings3d")** — Advanced subdivision modeler that is both powerful and easy to use.

	[http://www.wings3d.com/](http://www.wings3d.com/) || [wings3d](https://www.archlinux.org/packages/?name=wings3d)

#### Screen capture

See also: [Taking a screenshot](/index.php/Taking_a_screenshot "Taking a screenshot").

### Audio

#### Audio systems

See also the main article [Sound system](/index.php/Sound_system "Sound system") and [Wikipedia:Sound server](https://en.wikipedia.org/wiki/Sound_server "wikipedia:Sound server").

*   **wineasio** — Provides an ASIO to JACK driver for *wine*. ASIO is the most common Windows low-latency driver, so is commonly used in audio workstation programs.

	[https://sourceforge.net/projects/wineasio/](https://sourceforge.net/projects/wineasio/) || [wineasio](https://aur.archlinux.org/packages/wineasio/)

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

	[https://cmus.github.io/](https://cmus.github.io/) || [cmus](https://www.archlinux.org/packages/?name=cmus)

*   **Cplay** — Curses front-end for various audio players (ogg123, mpg123, mpg321, splay, madplay, and mikmod, xmp, and sox).

	[https://directory.fsf.org/wiki/Cplay](https://directory.fsf.org/wiki/Cplay) || [cplay](https://aur.archlinux.org/packages/cplay/)

*   **Herrie** — Minimalistic console-based music player with native AudioScrobbler support.

	[https://github.com/EdSchouten/herrie](https://github.com/EdSchouten/herrie) || [herrie](https://aur.archlinux.org/packages/herrie/)

*   **[MOC](/index.php/Moc "Moc")** — Ncurses console audio player with support for the MP3, OGG, and WAV formats.

	[https://moc.daper.net/](https://moc.daper.net/) || [moc](https://www.archlinux.org/packages/?name=moc)

*   **MPFC** — Gstreamer-based audio player with curses interface.

	[https://code.google.com/archive/p/mpfc/](https://code.google.com/archive/p/mpfc/) || [mpfc](https://aur.archlinux.org/packages/mpfc/)

*   **[mpg123](https://en.wikipedia.org/wiki/Mpg123 "wikipedia:Mpg123")** — Fast free MP3 console audio player for Linux, FreeBSD, Solaris, HP-UX and nearly all other UNIX systems (also decodes MP1 and MP2 files).

	[https://www.mpg123.org/](https://www.mpg123.org/) || [mpg123](https://www.archlinux.org/packages/?name=mpg123)

*   **mps-youtube** — Terminal based YouTube jukebox with playlist management. Plays audio/video through mplayer/mpv.

	[https://github.com/mps-youtube/mps-youtube](https://github.com/mps-youtube/mps-youtube) || [mps-youtube](https://www.archlinux.org/packages/?name=mps-youtube)

*   **pancake** — Cli pandora client built with urwid.

	[https://github.com/osum4est/pancake/](https://github.com/osum4est/pancake/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[pianobar](/index.php/Pianobar "Pianobar")** — Console-based frontend for the online radio Pandora.

	[https://6xq.net/projects/pianobar/](https://6xq.net/projects/pianobar/) || [pianobar](https://www.archlinux.org/packages/?name=pianobar)

*   **[VLC](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Highly portable multimedia player with ncurses interface module, and multimedia framework capable of reading most audio and video formats as well as DVDs, Audio CDs, VCDs, and various streaming protocols.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **whistle** — a curses-based commandline audio player.

	[https://github.com/ap0calypse/whistle/](https://github.com/ap0calypse/whistle/) || [whistle-git](https://aur.archlinux.org/packages/whistle-git/)

##### GUI players

*   **[Amarok](/index.php/Amarok "Amarok")** — Mature Qt-based player known for its plethora of features.

	[https://amarok.kde.org/](https://amarok.kde.org/) || [amarok](https://www.archlinux.org/packages/?name=amarok)

*   **[Audacious](/index.php/Audacious "Audacious")** — [Winamp](https://en.wikipedia.org/wiki/Winamp "wikipedia:Winamp") clone like Beep and old XMMS versions.

	[http://audacious-media-player.org/](http://audacious-media-player.org/) || [audacious](https://www.archlinux.org/packages/?name=audacious)

*   **[Banshee](https://en.wikipedia.org/wiki/Banshee_(media_player) "wikipedia:Banshee (media player)")** — [iTunes](https://en.wikipedia.org/wiki/iTunes "wikipedia:iTunes") clone, built with GTK+ and [Mono](/index.php/Mono "Mono"), feature-rich.

	[http://banshee.fm/](http://banshee.fm/) || [banshee](https://aur.archlinux.org/packages/banshee/)

*   **[Clementine](https://en.wikipedia.org/wiki/Clementine_(software) "wikipedia:Clementine (software)")** — Amarok 1.4 clone, ported to Qt 4.

	[https://www.clementine-player.org/](https://www.clementine-player.org/) || [clementine](https://www.archlinux.org/packages/?name=clementine)

*   **Cuberok** — Music player and collection manager with a lightweight interface.

	[https://code.google.com/archive/p/cuberok/](https://code.google.com/archive/p/cuberok/) || [cuberok](https://aur.archlinux.org/packages/cuberok/)

*   **DeaDBeeF** — Light and fast music player with many features, no GNOME or KDE dependencies, supports console-only, as well as a GTK+ GUI, comes with many plugins, and has a metadata editor.

	[http://deadbeef.sourceforge.net/](http://deadbeef.sourceforge.net/) || [deadbeef](https://www.archlinux.org/packages/?name=deadbeef)

*   **[Exaile](/index.php/Exaile "Exaile")** — GTK+ clone of Amarok.

	[http://www.exaile.org/](http://www.exaile.org/) || [exaile](https://aur.archlinux.org/packages/exaile/)

*   **gmusicbrowser** — Open-source jukebox for large collections of MP3/OGG/FLAC files.

	[https://gmusicbrowser.org/](https://gmusicbrowser.org/) || [gmusicbrowser](https://aur.archlinux.org/packages/gmusicbrowser/)

*   **GNOME Music** — Music is the new GNOME music playing application. It aims to combine an elegant and immersive browsing experience with simple and straightforward controls.

	[https://wiki.gnome.org/Apps/Music](https://wiki.gnome.org/Apps/Music) || [gnome-music](https://www.archlinux.org/packages/?name=gnome-music)

*   **Goggles Music Manager** — Music collection manager and player that automatically categorizes your music, supports gapless playback, features easy tag editing, and internet radio support. Uses the [Fox toolkit](https://en.wikipedia.org/wiki/Fox_toolkit "wikipedia:Fox toolkit").

	[https://gogglesmm.github.io/](https://gogglesmm.github.io/) || [gogglesmm](https://www.archlinux.org/packages/?name=gogglesmm)

*   **Guayadeque** — Full featured media player that can easily manage large collections and uses the GStreamer media framework.

	[http://guayadeque.org/](http://guayadeque.org/) || [guayadeque](https://aur.archlinux.org/packages/guayadeque/)

*   **[JuK](https://en.wikipedia.org/wiki/JuK "wikipedia:JuK")** — JuK is an audio jukebox application, supporting collections of MP3, Ogg Vorbis, and FLAC audio files.

	[https://www.kde.org/applications/multimedia/juk/](https://www.kde.org/applications/multimedia/juk/) || [juk](https://www.archlinux.org/packages/?name=juk)

*   **Kaku** — An highly integrated music player supports different online platform like YouTube, SoundCloud, Vimeo and more.

	[https://github.com/EragonJ/Kaku](https://github.com/EragonJ/Kaku) || [kaku-bin](https://aur.archlinux.org/packages/kaku-bin/)

*   **Listen** — Listen is a Music player and management for GNOME written in python.

	[https://launchpad.net/listen](https://launchpad.net/listen) || [listen](https://aur.archlinux.org/packages/listen/)

*   **Lollypop** — A GNOME music player.

	[https://gnumdk.github.io/lollypop-web/](https://gnumdk.github.io/lollypop-web/) || [lollypop](https://www.archlinux.org/packages/?name=lollypop)

*   **LXMusic** — A minimalist xmms2-based music player.

	[https://wiki.lxde.org/en/LXMusic](https://wiki.lxde.org/en/LXMusic) || [lxmusic](https://www.archlinux.org/packages/?name=lxmusic)

*   **Miam-player** — Cross-platform open source music player.

	[https://miam-player.org/](https://miam-player.org/) || [miam-player](https://aur.archlinux.org/packages/miam-player/)

*   **Muine** — A music player written in C Sharp.

	[https://muine.gooeylinux.org/](https://muine.gooeylinux.org/) || [muine](https://www.archlinux.org/packages/?name=muine)

*   **Musique** — Just another music player, only better.

	[http://flavio.tordini.org/musique](http://flavio.tordini.org/musique) || [musique](https://aur.archlinux.org/packages/musique/)

*   **[Nightingale](https://en.wikipedia.org/wiki/Nightingale_(software) "wikipedia:Nightingale (software)")** — Open source clone of iTunes-based on [Songbird](https://en.wikipedia.org/wiki/Songbird_(software) "wikipedia:Songbird (software)"), that uses Mozilla technologies and the GStreamer framework.

	[https://getnightingale.com/](https://getnightingale.com/) || [nightingale-git](https://aur.archlinux.org/packages/nightingale-git/)

*   **Noise** — Simple, fast, and good looking music player. The official elementary music player.

	[https://launchpad.net/noise](https://launchpad.net/noise) || [pantheon-music](https://www.archlinux.org/packages/?name=pantheon-music)

*   **Nuvola Player** — Integrated Google Music, 8tracks and Hype Machine player.

	[https://tiliado.eu/nuvolaplayer/](https://tiliado.eu/nuvolaplayer/) || [nuvolaplayer-git](https://aur.archlinux.org/packages/nuvolaplayer-git/)

*   **pithos** — Python/GTK Pandora Radio desktop client.

	[https://pithos.github.io/](https://pithos.github.io/) || [pithos](https://aur.archlinux.org/packages/pithos/)

*   **Pragha** — GTK+ music manager. (fork of the Consonance Music Manager)

	[https://pragha-music-player.github.io/](https://pragha-music-player.github.io/) || [pragha](https://www.archlinux.org/packages/?name=pragha)

*   **Qmmp** — Qt-based multimedia player with a user interface that is similar to Winamp or XMMS.

	[http://qmmp.ylsoftware.com/](http://qmmp.ylsoftware.com/) || [qmmp](https://www.archlinux.org/packages/?name=qmmp)

*   **[Quod Libet](https://en.wikipedia.org/wiki/Quod_Libet_(software) "wikipedia:Quod Libet (software)")** — Audio player written with PyGTK and GStreamer with support for regular expressions in playlists.

	[https://github.com/quodlibet/quodlibet/](https://github.com/quodlibet/quodlibet/) || [quodlibet](https://www.archlinux.org/packages/?name=quodlibet)

*   **[Rhythmbox](https://en.wikipedia.org/wiki/Rhythmbox "wikipedia:Rhythmbox")** — GTK+ clone of iTunes, used by default in GNOME.

	[https://wiki.gnome.org/Apps/Rhythmbox](https://wiki.gnome.org/Apps/Rhythmbox) || [rhythmbox](https://www.archlinux.org/packages/?name=rhythmbox)

*   **Sayonara** — Sayonara is a small, clear and fast audio player for Linux written in C++, supported by the Qt framework.

	[https://sayonara-player.com/](https://sayonara-player.com/) || [sayonara-player](https://aur.archlinux.org/packages/sayonara-player/)

*   **[Spotify](/index.php/Spotify "Spotify")** — Proprietary music streaming service. It supports local playback and streaming from Spotify's vast library (requires a free account).

	[https://www.spotify.com/](https://www.spotify.com/) || [spotify](https://aur.archlinux.org/packages/spotify/)

*   **[SpotCommander](/index.php/SpotCommander "SpotCommander")** — A remote control for Spotify, optimized for mobile devices. It works on any device with a modern browser, and it's free and open source.

	[https://olejon.github.io/spotcommander/](https://olejon.github.io/spotcommander/) || [spotcommander](https://aur.archlinux.org/packages/spotcommander/)

*   **Tomahawk** — Music player application written in C++/Qt. It decouples the name of the song from the source it was shared from - and fulfills the request using all of your available sources.

	[https://www.tomahawk-player.org/](https://www.tomahawk-player.org/) || [tomahawk](https://aur.archlinux.org/packages/tomahawk/)

*   **[VLC](https://en.wikipedia.org/wiki/VLC_media_player "wikipedia:VLC media player")** — Highly portable multimedia player and multimedia framework capable of reading most audio and video formats as well as DVDs, Audio CDs, VCDs, and various streaming protocols.

	[https://www.videolan.org/vlc/](https://www.videolan.org/vlc/) || [vlc](https://www.archlinux.org/packages/?name=vlc)

*   **[XMMS](https://en.wikipedia.org/wiki/XMMS "wikipedia:XMMS")** — Skinnable GTK+ standalone media player similar to Winamp.

	[https://legacy.xmms2.org/](https://legacy.xmms2.org/) || [xmms](https://aur.archlinux.org/packages/xmms/)

#### Volume managers

*   **GVolWheel** — An audio mixer which lets you control the volume through a tray icon.

	[https://sourceforge.net/projects/gvolwheel/](https://sourceforge.net/projects/gvolwheel/) || [gvolwheel](https://aur.archlinux.org/packages/gvolwheel/)

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

*   **C.A.V.A.** — Console-based audio visualizer for Alsa, MPD and PulseAudio.

	[https://karlstav.github.io/cava/](https://karlstav.github.io/cava/) || [cava](https://aur.archlinux.org/packages/cava/)

*   **cli-visualizer** — A highly configurable CLI-based audio visualizer.

	[https://github.com/dpayne/cli-visualizer](https://github.com/dpayne/cli-visualizer) || [cli-visualizer](https://aur.archlinux.org/packages/cli-visualizer/)

#### Audio tag editors

*   **Audio Tag Tool** — Tool to edit tags in MP3 and Ogg Vorbis files.

	[http://tagtool.sourceforge.net/](http://tagtool.sourceforge.net/) || [tagtool](https://aur.archlinux.org/packages/tagtool/)

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

*   **Thunar Media Tags Plugin** — Adds special features for media files to the Thunar File Manager, including the ability to edit tags.

	[http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin) || [thunar-media-tags-plugin](https://www.archlinux.org/packages/?name=thunar-media-tags-plugin)

*   **Qoobar** — Universal QT-based audio tagger (specialized for classical music)

	[http://qoobar.sourceforge.net/en/index.htm](http://qoobar.sourceforge.net/en/index.htm) || [qoobar](https://aur.archlinux.org/packages/qoobar/)

#### Sound editing

See also [Professional audio](/index.php/Professional_audio "Professional audio").

*   **[Ardour](https://en.wikipedia.org/wiki/Ardour_(software) "wikipedia:Ardour (software)")** — Multichannel hard disk recorder and digital audio workstation.

	[http://ardour.org/](http://ardour.org/) || [ardour](https://www.archlinux.org/packages/?name=ardour)

*   **[Audacity](https://en.wikipedia.org/wiki/Audacity_(audio_editor) "wikipedia:Audacity (audio editor)")** — Program that lets you manipulate digital audio waveforms.

	[http://audacity.sourceforge.net/](http://audacity.sourceforge.net/) || [audacity](https://www.archlinux.org/packages/?name=audacity)

*   **Bitwig Studio** — Proprietary professional digital audio workstation.

	[http://bitwig.com/](http://bitwig.com/) || [bitwig-studio](https://aur.archlinux.org/packages/bitwig-studio/)

*   **Gnac** — Audio converter for GNOME.

	[http://gnac.sourceforge.net/](http://gnac.sourceforge.net/) || [gnac](https://www.archlinux.org/packages/?name=gnac)

*   **GNOME Sound Recorder** — The Sound Recorder application enables you to record and play .flac, .ogg (OGG audio, or .oga), and .wav sound files.

	[https://wiki.gnome.org/Design/Apps/SoundRecorder](https://wiki.gnome.org/Design/Apps/SoundRecorder) || [gnome-sound-recorder](https://www.archlinux.org/packages/?name=gnome-sound-recorder)

*   **[Jokosher](https://en.wikipedia.org/wiki/Jokosher "wikipedia:Jokosher")** — Non-linear multi-track digital audio editor that is being developed in Python, using the GTK+ interface and GStreamer as an audio back-end.

	[https://launchpad.net/jokosher/](https://launchpad.net/jokosher/) || [jokosher](https://aur.archlinux.org/packages/jokosher/)

*   **KWave** — Sound editor for KDE.

	[http://kwave.sourceforge.net/](http://kwave.sourceforge.net/) || [kwave](https://www.archlinux.org/packages/?name=kwave)

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

*   **[Dragon Player](https://en.wikipedia.org/wiki/Dragon_Player "wikipedia:Dragon Player")** — Simple video player for KDE. Part of the [kdemultimedia](https://www.archlinux.org/groups/x86_64/kdemultimedia/) group.

	[https://www.kde.org/applications/multimedia/dragonplayer/](https://www.kde.org/applications/multimedia/dragonplayer/) || [dragon](https://www.archlinux.org/packages/?name=dragon)

*   **[GNOME Videos](https://en.wikipedia.org/wiki/GNOME_Videos "wikipedia:GNOME Videos")** — Media player (audio and video) for the GNOME desktop that uses GStreamer. Part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/)

	[https://wiki.gnome.org/Apps/Videos](https://wiki.gnome.org/Apps/Videos) || [totem](https://www.archlinux.org/packages/?name=totem)

*   **[Kaffeine](https://en.wikipedia.org/wiki/Kaffeine "wikipedia:Kaffeine")** — Very versatile KDE media player that, by default, utilizes VLC as its backend and has excellent support of digital TV (DVB).

	[https://www.kde.org/applications/multimedia/kaffeine/](https://www.kde.org/applications/multimedia/kaffeine/) || [kaffeine](https://www.archlinux.org/packages/?name=kaffeine)

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

	[http://home.gna.org/whaawmp/](http://home.gna.org/whaawmp/) || [whaawmp](https://aur.archlinux.org/packages/whaawmp/)

*   **Xnoise** — GTK+ and GStreamer-based media player for both audio and video with "a slick GUI, great speed and lots of features." (development ceased)

	[http://www.xnoise-media-player.com/](http://www.xnoise-media-player.com/) || [xnoise](https://www.archlinux.org/packages/?name=xnoise)

#### Subtitles

*   **[Aegisub](https://en.wikipedia.org/wiki/Aegisub "wikipedia:Aegisub")** — Subtitle editor.

	[https://github.com/Aegisub/Aegisub](https://github.com/Aegisub/Aegisub) || [aegisub](https://www.archlinux.org/packages/?name=aegisub)

*   **Gaupol** — Full-featured subtitle editor.

	[http://home.gna.org/gaupol](http://home.gna.org/gaupol) || [gaupol](https://www.archlinux.org/packages/?name=gaupol)

*   **[Gnome Subtitles](https://en.wikipedia.org/wiki/Gnome_Subtitles "wikipedia:Gnome Subtitles")** — Video subtitle editor for GNOME.

	[http://www.gnomesubtitles.org/](http://www.gnomesubtitles.org/) || [gnome-subtitles](https://www.archlinux.org/packages/?name=gnome-subtitles)

*   **Jubler** — Open-source multiplatform subtitle editor written in Java.

	[http://www.jubler.org](http://www.jubler.org) || [jubler](https://aur.archlinux.org/packages/jubler/)

*   **Penguin Subtitle Player** — Penguin Subtitle Player is an open-source, cross-platform standalone subtitle player, as an alternative to Greenfish Subtitle Player, SrtViewer (Mac), SRTPlayer, JustSubsPlayer and Free Subtitle Player.

	[https://github.com/carsonip/Penguin-Subtitle-Player](https://github.com/carsonip/Penguin-Subtitle-Player) || [penguin-subtitle-player-git](https://aur.archlinux.org/packages/penguin-subtitle-player-git/)

*   **subdl** — Automatic subtitle downloader.

	[https://github.com/akexakex/subdl](https://github.com/akexakex/subdl) || [subdl](https://www.archlinux.org/packages/?name=subdl)

*   **Subtitle Composer** — open-source Subtitle editor with Qt 5 based GUI supporting various formats, features different player backends, able to display wave form

	[https://github.com/maxrd2/subtitlecomposer](https://github.com/maxrd2/subtitlecomposer) || [subtitlecomposer](https://aur.archlinux.org/packages/subtitlecomposer/)

*   **[Subtitle Edit](https://en.wikipedia.org/wiki/Subtitle_Edit "wikipedia:Subtitle Edit")** — Subtitle editing program. Written in C# using mono.

	[https://github.com/SubtitleEdit/subtitleedit](https://github.com/SubtitleEdit/subtitleedit) || [subtitleedit](https://aur.archlinux.org/packages/subtitleedit/)

*   **SubtitlesPrinter** — Print subtitles above a X-screen, independently of the video player.

	[https://github.com/OlivierMarty/SubtitlesPrinter](https://github.com/OlivierMarty/SubtitlesPrinter) || [subtitles-printer-git](https://aur.archlinux.org/packages/subtitles-printer-git/)

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

	[http://fixounet.free.fr/avidemux/](http://fixounet.free.fr/avidemux/) || [avidemux-qt](https://www.archlinux.org/packages/?name=avidemux-qt)

*   **[Cinelerra (Community Version)](https://en.wikipedia.org/wiki/Cinelerra "wikipedia:Cinelerra")** — Professional video editing and compositing environment.

	[http://cinelerra-cv.org/](http://cinelerra-cv.org/) || [cinelerra-cv](https://www.archlinux.org/packages/?name=cinelerra-cv)

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

*   **[Pitivi](https://en.wikipedia.org/wiki/Pitivi "wikipedia:Pitivi")** — Video editor designed to be intuitive and integrate well in the GNOME desktop.

	[http://www.pitivi.org/](http://www.pitivi.org/) || [pitivi](https://www.archlinux.org/packages/?name=pitivi)

*   **[Shotcut](https://en.wikipedia.org/wiki/Shotcut "wikipedia:Shotcut")** — Shotcut is a free, open source, cross-platform video editor.

	[http://www.shotcut.org/](http://www.shotcut.org/) || [shotcut-bin](https://aur.archlinux.org/packages/shotcut-bin/)

*   **Transmageddon** — Simple python application for transcoding video into formats supported by GStreamer.

	[http://www.linuxrising.org/](http://www.linuxrising.org/) || [transmageddon](https://www.archlinux.org/packages/?name=transmageddon)

*   **[Blender](https://en.wikipedia.org/wiki/Blender_(software)#Video_editing "wikipedia:Blender (software)")** — Fully integrated 3D graphics creation suite with a built-in non-linear video editor.

	[http://www.blender.org/](http://www.blender.org/) || [blender](https://www.archlinux.org/packages/?name=blender)

#### Screencast

See also [Wikipedia:Comparison of screencasting software](https://en.wikipedia.org/wiki/Comparison_of_screencasting_software "wikipedia:Comparison of screencasting software").

Screencast utilities allow you to create a video of your desktop or individual windows.

*   **byzanz** — Simple screencast tool that produces GIF animations.

	[http://blogs.gnome.org/otte/2009/08/30/byzanz-0-2-0/](http://blogs.gnome.org/otte/2009/08/30/byzanz-0-2-0/) || [byzanz](https://www.archlinux.org/packages/?name=byzanz)

*   **Green Recorder** — A simple yet functional desktop recorder for Linux systems.

	[https://github.com/green-project/green-recorder](https://github.com/green-project/green-recorder) || [green-recorder](https://aur.archlinux.org/packages/green-recorder/)

*   **Istanbul** — Simple desktop session recorder that produces ogg videos.

	[https://wiki.gnome.org/Projects/Istanbul](https://wiki.gnome.org/Projects/Istanbul) || [istanbul](https://aur.archlinux.org/packages/istanbul/)

*   **Kazam** — Screencasting program with design in mind. Handles multiscreen setups.

	[https://launchpad.net/kazam](https://launchpad.net/kazam) || [kazam](https://aur.archlinux.org/packages/kazam/)

*   **OBS** — Free and open source software for video recording and live streaming.

	[https://obsproject.com/](https://obsproject.com/) || [obs-studio](https://www.archlinux.org/packages/?name=obs-studio)

*   **[RecordMyDesktop](https://en.wikipedia.org/wiki/RecordMyDesktop "wikipedia:RecordMyDesktop")** — (inactive) An easy to use utility that records your desktop into the ogg format with a CLI, Qt or GTK+ interface.

	[http://recordmydesktop.sourceforge.net/](http://recordmydesktop.sourceforge.net/) || [recordmydesktop](https://www.archlinux.org/packages/?name=recordmydesktop) [gtk-recordmydesktop](https://www.archlinux.org/packages/?name=gtk-recordmydesktop) [qt-recordmydesktop](https://www.archlinux.org/packages/?name=qt-recordmydesktop)

*   **simplescreenrecorder** — A feature-rich screen recorder written in C++/Qt4 that supports X11 and OpenGL.

	[http://www.maartenbaert.be/simplescreenrecorder/](http://www.maartenbaert.be/simplescreenrecorder/) || [simplescreenrecorder](https://www.archlinux.org/packages/?name=simplescreenrecorder)

*   **vokoscreen** — Simple screencast tool, GUI ffmpeg.

	[http://www.kohaupt-online.de/hp](http://www.kohaupt-online.de/hp) || [vokoscreen](https://aur.archlinux.org/packages/vokoscreen/)

*   **[XVidCap](https://en.wikipedia.org/wiki/XVidCap "wikipedia:XVidCap")** — Application used for recording a screencast or digital recording of an X Window System screen output with an audio narration.

	[http://xvidcap.sourceforge.net/](http://xvidcap.sourceforge.net/) || [xvidcap](https://aur.archlinux.org/packages/xvidcap/)

*   **FFcast** — FFmpeg-based screencast tool written in Bash.

	[https://github.com/lolilolicon/FFcast](https://github.com/lolilolicon/FFcast) || [ffcast](https://aur.archlinux.org/packages/ffcast/)

*   **[FFmpeg](/index.php/FFmpeg#Screen_cast "FFmpeg")** — Complete, cross-platform solution to record, convert and stream audio and video.

	[http://www.ffmpeg.org/](http://www.ffmpeg.org/) || [ffmpeg](https://www.archlinux.org/packages/?name=ffmpeg)

*   **peek** — Simple screencast tool that produces GIF animations.

	[https://github.com/phw/peek](https://github.com/phw/peek) || [peek](https://aur.archlinux.org/packages/peek/)

### Mobile phone managers

*   **[gnokii](https://en.wikipedia.org/wiki/Gnokii "wikipedia:Gnokii")** — Tools and user space driver for use with mobile phones.

	[http://www.gnokii.org/](http://www.gnokii.org/) || [gnokii](https://www.archlinux.org/packages/?name=gnokii)

*   **GNOME Phone Manager** — Control your mobile phone from your GNOME desktop.

	[https://wiki.gnome.org/PhoneManager](https://wiki.gnome.org/PhoneManager) || [gnome-phone-manager](https://www.archlinux.org/packages/?name=gnome-phone-manager)

*   **KDE Connect** — A project that aims to communicate all your devices.

	[https://community.kde.org/KDEConnect](https://community.kde.org/KDEConnect) || [kdeconnect](https://www.archlinux.org/packages/?name=kdeconnect)

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

	[https://github.com/trizen/clyrics](https://github.com/trizen/clyrics) || [clyrics](https://aur.archlinux.org/packages/clyrics/)

## Utilities

### Partitioning tools

See [Partitioning#Partitioning tools](/index.php/Partitioning#Partitioning_tools "Partitioning").

### Mount tools

See also [udisks#Mount helpers](/index.php/Udisks#Mount_helpers "Udisks").

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

### Terminal emulators

Terminal emulators show a GUI Window that contains a terminal. Most emulate Xterm, which in turn emulates VT102, which emulates typewriter. For further background information, see [Wikipedia:Terminal emulator](https://en.wikipedia.org/wiki/Terminal_emulator "wikipedia:Terminal emulator").

For a comprehensive list, see [Wikipedia:List of terminal emulators](https://en.wikipedia.org/wiki/List_of_terminal_emulators "wikipedia:List of terminal emulators").

*   **Alacritty** — the fastest terminal emulator in existence.

	[https://github.com/jwilm/alacritty](https://github.com/jwilm/alacritty) || [alacritty-git](https://aur.archlinux.org/packages/alacritty-git/)

*   **aterm** — Xterm replacement with transparency support. It has been deprecated in favour of urxvt since 2008.

	[http://aterm.sourceforge.net/](http://aterm.sourceforge.net/) || [aterm](https://aur.archlinux.org/packages/aterm/)

*   **Cool Retro Term** — A good looking terminal emulator which mimics the old cathode display.

	[https://github.com/Swordfish90/cool-retro-term](https://github.com/Swordfish90/cool-retro-term) || [cool-retro-term](https://www.archlinux.org/packages/?name=cool-retro-term)

*   **Eterm** — Terminal emulator intended as a replacement for xterm and designed for the [Enlightenment](/index.php/Enlightenment "Enlightenment") desktop.

	[http://eterm.org](http://eterm.org) || [eterm](https://aur.archlinux.org/packages/eterm/)

*   **Gate One** — Web-based terminal emulator and SSH client.

	[https://github.com/liftoff/GateOne](https://github.com/liftoff/GateOne) || [gateone-git](https://aur.archlinux.org/packages/gateone-git/)

*   **Hyper** — A terminal with JS/CSS support.

	[https://github.com/zeit/hyper](https://github.com/zeit/hyper) || [hyper](https://aur.archlinux.org/packages/hyper/)

*   **[Konsole](https://en.wikipedia.org/wiki/Konsole "wikipedia:Konsole")** — Terminal emulator included in the [KDE](/index.php/KDE "KDE") desktop.

	[https://www.kde.org/applications/system/konsole/](https://www.kde.org/applications/system/konsole/) || [konsole](https://www.archlinux.org/packages/?name=konsole)

*   **kitty** — A modern, hackable, featureful, OpenGL based terminal emulator

	[https://github.com/kovidgoyal/kitty](https://github.com/kovidgoyal/kitty) || [kitty-git](https://aur.archlinux.org/packages/kitty-git/)

*   **mlterm** — A multi-lingual terminal emulator supporting various character sets and encodings in the world.

	[https://sourceforge.net/projects/mlterm/](https://sourceforge.net/projects/mlterm/) || [mlterm](https://aur.archlinux.org/packages/mlterm/)

*   **QTerminal** — A lightweight Qt-based terminal emulator.

	[https://github.com/qterminal/qterminal](https://github.com/qterminal/qterminal) || [qterminal](https://www.archlinux.org/packages/?name=qterminal)

*   **[rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt")** — Popular replacement for the xterm.

	[http://rxvt.sourceforge.net/](http://rxvt.sourceforge.net/) || [rxvt](https://aur.archlinux.org/packages/rxvt/)

*   **shellinabox** — A web-based SSH Terminal

	[https://github.com/shellinabox/shellinabox](https://github.com/shellinabox/shellinabox) || [shellinabox-git](https://aur.archlinux.org/packages/shellinabox-git/)

*   **[st](/index.php/St "St")** — Simple terminal implementation for X.

	[http://st.suckless.org](http://st.suckless.org) || [st](https://aur.archlinux.org/packages/st/)

*   **Terminology** — Terminal emulator by the Enlightenment project team with innovative features: file thumbnails and media play like a media player.

	[https://www.enlightenment.org/about-terminology](https://www.enlightenment.org/about-terminology) || [terminology](https://www.archlinux.org/packages/?name=terminology)

*   **[Tilda](/index.php/Tilda "Tilda")** — Terminal inspired by many classic terminals from first person shooter games such as Quake, Doom and Half-Life.

	[https://github.com/lanoxx/tilda/](https://github.com/lanoxx/tilda/) || [tilda](https://www.archlinux.org/packages/?name=tilda)

*   **[urxvt](/index.php/Urxvt "Urxvt")** — Highly extendable (with Perl) unicode enabled rxvt-clone terminal emulator featuring tabbing, url launching, a Quake style drop-down mode and pseudo-transparency.

	[http://software.schmorp.de/pkg/rxvt-unicode.html](http://software.schmorp.de/pkg/rxvt-unicode.html) || [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode)

*   **[xterm](/index.php/Xterm "Xterm")** — Simple terminal emulator for the X Window System. It provides DEC VT102 and Tektronix 4014 compatible terminals for programs that can't use the window system directly.

	[http://invisible-island.net/xterm/](http://invisible-island.net/xterm/) || [xterm](https://www.archlinux.org/packages/?name=xterm)

*   **[Yakuake](https://en.wikipedia.org/wiki/Yakuake "wikipedia:Yakuake")** — Drop-down terminal (Quake style) emulator based on Konsole.

	[https://yakuake.kde.org/](https://yakuake.kde.org/) || [yakuake](https://www.archlinux.org/packages/?name=yakuake)

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

*   **[Termite](/index.php/Termite "Termite")** — A keyboard-centric VTE-based terminal, aimed at use within a window manager with tiling and/or tabbing support.

	[https://github.com/thestinger/termite](https://github.com/thestinger/termite) || [termite](https://www.archlinux.org/packages/?name=termite)

*   **Tilix** — A tiling terminal emulator for Linux using GTK+ 3

	[https://github.com/gnunn1/tilix](https://github.com/gnunn1/tilix) || [tilix](https://aur.archlinux.org/packages/tilix/) [tilix-git](https://aur.archlinux.org/packages/tilix-git/)

*   **tinyterm** — Very lightweight terminal emulator based on VTE.

	[https://github.com/lahwaacz/tinyterm](https://github.com/lahwaacz/tinyterm) || [tinyterm-git](https://aur.archlinux.org/packages/tinyterm-git/)

#### KMS-based

The following terminal emulators are based on the [kernel mode setting](/index.php/Kernel_mode_setting "Kernel mode setting") that could be invoked without X.

*   **[KMSCON](/index.php/KMSCON "KMSCON")** — A KMS/DRM-based system console(getty) with an integrated terminal emulator for Linux operating systems.

	[https://github.com/dvdhrm/kmscon](https://github.com/dvdhrm/kmscon) || [kmscon](https://www.archlinux.org/packages/?name=kmscon)

#### framebuffer-based

In GNU/Linux world, the [framebuffer](https://en.wikipedia.org/wiki/Framebuffer "wikipedia:Framebuffer") could be refered to a virtual device in the Linux kernel (**fbdev**) or the virtual framebuffer system for X (**xvfb**). This section mainly lists the terminal emulators that based on the in-kernel virtual device, i.e. **fbdev**.

*   **yaft** — A simple terminal emulator for living without X, with UCS2 glyphs, wallpaper and 256color support.

	[https://github.com/uobikiemukot/yaft](https://github.com/uobikiemukot/yaft) || [yaft](https://aur.archlinux.org/packages/yaft/)

### Hex editors

See also [Wikipedia:Comparison of hex editors](https://en.wikipedia.org/wiki/Comparison_of_hex_editors "wikipedia:Comparison of hex editors").

*   **hyx** — A minimalistic but powerful (hex/ASCII, insert/replace/delete, copy/paste, undo/redo, search, colors, vim-inspired controls) console hex editor.

	[https://yx7.cc/code/](https://yx7.cc/code/) || [hyx](https://aur.archlinux.org/packages/hyx/)

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

*   **[CodeLite](https://en.wikipedia.org/wiki/CodeLite "wikipedia:CodeLite")** — Open source and cross-platform C/C++/PHP and Node.js IDE written in C++ .

	[http://www.codelite.org/](http://www.codelite.org/) || [codelite](https://aur.archlinux.org/packages/codelite/)

*   **[Cloud9](https://en.wikipedia.org/wiki/Cloud9_IDE "wikipedia:Cloud9 IDE")** — State-of-the-art IDE that runs in your browser and lives in the cloud, allowing you to run, debug and deploy applications from anywhere, anytime.

	[https://c9.io/](https://c9.io/) || [c9.core](https://aur.archlinux.org/packages/c9.core/)

*   **[Eclipse](/index.php/Eclipse "Eclipse")** — Open source community project, which aims to provide a universal development platform.

	[https://eclipse.org/](https://eclipse.org/) || [eclipse-java](https://www.archlinux.org/packages/?name=eclipse-java), [eclipse-cpp](https://www.archlinux.org/packages/?name=eclipse-cpp), [eclipse-php](https://www.archlinux.org/packages/?name=eclipse-php)

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

*   **[MonoDevelop](https://en.wikipedia.org/wiki/MonoDevelop "wikipedia:MonoDevelop")** — Cross-platform IDE targeted for the Mono and .NET frameworks.

	[http://monodevelop.com/](http://monodevelop.com/) || [monodevelop-git](https://aur.archlinux.org/packages/monodevelop-git/)

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

	[https://github.com/spyder-ide/spyder](https://github.com/spyder-ide/spyder) || [spyder2](https://www.archlinux.org/packages/?name=spyder2) (Python 2) or [spyder3](https://www.archlinux.org/packages/?name=spyder3) (Python 3)

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

### Files

#### File managers

See also [Wikipedia:Comparison of file managers](https://en.wikipedia.org/wiki/Comparison_of_file_managers "wikipedia:Comparison of file managers").

##### Console

*   **Clex** — File manager with full-screen user interface

	[http://www.clex.sk/](http://www.clex.sk/) || [clex](https://aur.archlinux.org/packages/clex/)

*   **[Dired](https://en.wikipedia.org/wiki/Dired "wikipedia:Dired")** — Directory editor integrated with [Emacs](/index.php/Emacs "Emacs").

	[https://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html](https://www.gnu.org/software/emacs/manual/html_node/emacs/Dired.html) || [emacs](https://www.archlinux.org/packages/?name=emacs)

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

*   **Caja** — The file manager for the MATE desktop.

	[https://github.com/mate-desktop/caja](https://github.com/mate-desktop/caja) || [caja](https://www.archlinux.org/packages/?name=caja)

*   **Deepin File Manager** — File manager developed for [Deepin](/index.php/Deepin "Deepin").

	[https://github.com/linuxdeepin/dde-file-manager](https://github.com/linuxdeepin/dde-file-manager) || [deepin-file-manager](https://www.archlinux.org/packages/?name=deepin-file-manager)

*   **[Dolphin](/index.php/Dolphin "Dolphin")** — File manager included in the KDE desktop.

	[https://userbase.kde.org/Dolphin](https://userbase.kde.org/Dolphin) || [dolphin](https://www.archlinux.org/packages/?name=dolphin)

*   **Double Commander** — File manager with two panels side by side. It is inspired by Total Commander and features some new ideas.

	[http://doublecmd.sourceforge.net//](http://doublecmd.sourceforge.net//) || [doublecmd-gtk2](https://www.archlinux.org/packages/?name=doublecmd-gtk2) [doublecmd-qt4](https://www.archlinux.org/packages/?name=doublecmd-qt4)

*   **[emelFM2](https://en.wikipedia.org/wiki/emelFM2 "wikipedia:emelFM2")** — File manager that implements the popular two-panel design.

	[http://emelfm2.net/](http://emelfm2.net/) || [emelfm2](https://www.archlinux.org/packages/?name=emelfm2)

*   **Gentoo** — A lightweight file manager for GTK.

	[http://www.obsession.se/gentoo/](http://www.obsession.se/gentoo/) || [gentoo](https://aur.archlinux.org/packages/gentoo/)

*   **[GNOME Commander](https://en.wikipedia.org/wiki/GNOME_Commander "wikipedia:GNOME Commander")** — A dual-paned file manager for the GNOME Desktop.

	[http://gcmd.github.io/](http://gcmd.github.io/) || [gnome-commander](https://aur.archlinux.org/packages/gnome-commander/)

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

	[http://www.qtfm.org/](http://www.qtfm.org/) || [qtfm](https://aur.archlinux.org/packages/qtfm/)

*   **ROX** — Small and fast file manager which can optionally manage the desktop background and panels.

	[http://rox.sourceforge.net](http://rox.sourceforge.net) || [rox](https://www.archlinux.org/packages/?name=rox)

*   **[SpaceFM](/index.php/SpaceFM "SpaceFM")** — GTK+ multi-panel tabbed file manager.

	[http://ignorantguru.github.com/spacefm/](http://ignorantguru.github.com/spacefm/) || [spacefm](https://aur.archlinux.org/packages/spacefm/)

*   **Sunflower** — Small and highly customizable twin-panel file manager for Linux with support for plugins.

	[http://sunflower-fm.org/](http://sunflower-fm.org/) || [sunflower](https://aur.archlinux.org/packages/sunflower/)

*   **[Thunar](/index.php/Thunar "Thunar")** — File manager that can be run as a daemon with excellent start up and directory load times.

	[http://docs.xfce.org/xfce/thunar/start](http://docs.xfce.org/xfce/thunar/start) || [thunar](https://www.archlinux.org/packages/?name=thunar)

*   **trolCommander** — Lightweight, cross-platform file manager written in Java (Successor of muCommander)

	[https://github.com/trol73/mucommander](https://github.com/trol73/mucommander) || [trolcommander](https://aur.archlinux.org/packages/trolcommander/)

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

	[https://www.gnu.org/software/cpio/](https://www.gnu.org/software/cpio/) || [cpio](https://www.archlinux.org/packages/?name=cpio)

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

	[https://www.gnu.org/software/tar/](https://www.gnu.org/software/tar/) || [tar](https://www.archlinux.org/packages/?name=tar)

*   **[zpaq](https://en.wikipedia.org/wiki/ZPAQ "wikipedia:ZPAQ")** — A high compression ratio archiver written in C++. Powered by Context-Model, LZ77 and BWT algorithm.

	[http://mattmahoney.net/dc/zpaq.html](http://mattmahoney.net/dc/zpaq.html) || [zpaq](https://aur.archlinux.org/packages/zpaq/)

*   **zopfli** — High compress ratio file compressor from Google, using a deflate-compatible algorithm called zopfli.

	[https://github.com/google/zopfli](https://github.com/google/zopfli) || [zopfli-git](https://aur.archlinux.org/packages/zopfli-git/)

*   **[zoo](https://en.wikipedia.org/wiki/Zoo_(file_format) "wikipedia:Zoo (file format)")** — Rarely used archiver that was mostly used in VMS world before PKZIP became popular.

	[http://www.ibiblio.org/pub/Linux/utils/compress/zoo-2.10-3.src.rpm](http://www.ibiblio.org/pub/Linux/utils/compress/zoo-2.10-3.src.rpm) || [zoo](https://aur.archlinux.org/packages/zoo/)

##### Graphical

*   **[Ark](https://en.wikipedia.org/wiki/Ark_(software) "wikipedia:Ark (software)")** — Archiving tool included in the KDE desktop.

	[https://www.kde.org/applications/utilities/ark/](https://www.kde.org/applications/utilities/ark/) || [ark](https://www.archlinux.org/packages/?name=ark)

*   **Engrampa** — Archive manager for [MATE](/index.php/MATE "MATE")

	[https://github.com/mate-desktop/engrampa](https://github.com/mate-desktop/engrampa) || [engrampa](https://www.archlinux.org/packages/?name=engrampa)

*   **[File Roller](https://en.wikipedia.org/wiki/File_Roller "wikipedia:File Roller")** — Archive manager included in the GNOME desktop.

	[http://fileroller.sourceforge.net/](http://fileroller.sourceforge.net/) || [file-roller](https://www.archlinux.org/packages/?name=file-roller)

*   **p7zip-gui** — The GUI belonging to the p7zip software.

	[http://p7zip.sourceforge.net/](http://p7zip.sourceforge.net/) || [p7zip-gui](https://aur.archlinux.org/packages/p7zip-gui/)

*   **[PeaZip](https://en.wikipedia.org/wiki/PeaZip "wikipedia:PeaZip")** — Open source file and archive manager.

	[http://www.peazip.org/peazip-linux.html](http://www.peazip.org/peazip-linux.html) || [peazip-gtk2](https://aur.archlinux.org/packages/peazip-gtk2/) [peazip-qt](https://aur.archlinux.org/packages/peazip-qt/)

*   **Squeeze** — Featherweight front-end for commandline archiving tools.

	[http://squeeze.xfce.org/](http://squeeze.xfce.org/) || [squeeze-git](https://aur.archlinux.org/packages/squeeze-git/)

*   **[Xarchiver](https://en.wikipedia.org/wiki/Xarchiver "wikipedia:Xarchiver")** — Lightweight desktop independent archive manager built with GTK+.

	[https://github.com/ib/xarchiver](https://github.com/ib/xarchiver) || [xarchiver](https://www.archlinux.org/packages/?name=xarchiver) or [xarchiver-gtk2](https://www.archlinux.org/packages/?name=xarchiver-gtk2)

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

#### Finders

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

	[https://help.gnome.org/users/gnome-search-tool/stable/gsearchtool-introduction.html.en](https://help.gnome.org/users/gnome-search-tool/stable/gsearchtool-introduction.html.en) || [gnome-search-tool](https://www.archlinux.org/packages/?name=gnome-search-tool)

*   **Gnome Search Tool No Nautilus** — *gnome-search-tool* to search for files without [GNOME Files](/index.php/GNOME_Files "GNOME Files") or *gnome-desktop*

	|| [gnome-search-tool-no-nautilus](https://aur.archlinux.org/packages/gnome-search-tool-no-nautilus/)

*   **Recoll** — Full text search tool based on Xapian backend

	[http://www.lesbonscomptes.com/recoll/](http://www.lesbonscomptes.com/recoll/) || [recoll](https://www.archlinux.org/packages/?name=recoll)

*   **Searchmonkey** — A powerful GUI search utility for matching regex patterns

	[http://searchmonkey.sourceforge.net/](http://searchmonkey.sourceforge.net/) || [searchmonkey](https://aur.archlinux.org/packages/searchmonkey/)

*   **[Tracker](https://en.wikipedia.org/wiki/Tracker_(search_software) "wikipedia:Tracker (search software)")** — All-in-one indexer, search tool and metadata database.

	[https://wiki.gnome.org/Projects/Tracker](https://wiki.gnome.org/Projects/Tracker) || [tracker](https://www.archlinux.org/packages/?name=tracker)

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

*   **duc** — A library and suite of tools for inspecting disk usage.

	[http://duc.zevv.nl/](http://duc.zevv.nl/) || [duc](https://aur.archlinux.org/packages/duc/)

*   **[Filelight](https://en.wikipedia.org/wiki/Filelight "wikipedia:Filelight")** — Disk usage analyzer that creates an interactive map of concentric, segmented rings that help visualise disk usage on your computer.

	[http://methylblue.com/filelight/](http://methylblue.com/filelight/) || [filelight](https://www.archlinux.org/packages/?name=filelight)

*   **GdMap** — Disk usage analyzer that draws a map of rectangles sized according to file or dir sizes.

	[http://gdmap.sourceforge.net/](http://gdmap.sourceforge.net/) || [gdmap](https://www.archlinux.org/packages/?name=gdmap)

*   **gt5** — Diff-capable "du-browser".

	[http://gt5.sourceforge.net](http://gt5.sourceforge.net) || [gt5](https://aur.archlinux.org/packages/gt5/)

*   **ncdu** — Simple ncurses disk usage analyzer.

	[http://dev.yorhel.nl/ncdu](http://dev.yorhel.nl/ncdu) || [ncdu](https://www.archlinux.org/packages/?name=ncdu)

*   **qdirstat** — Qt-based directory statistics (KDirStat/K4DirStat without any KDE - from the original KDirStat author).

	[https://github.com/shundhammer/qdirstat](https://github.com/shundhammer/qdirstat) || [qdirstat](https://aur.archlinux.org/packages/qdirstat/)

### Clock synchronization

See [Time#Time synchronization](/index.php/Time#Time_synchronization "Time").

### System monitoring

See also [Category:Status monitoring and notification](/index.php/Category:Status_monitoring_and_notification "Category:Status monitoring and notification")

*   **[Conky](/index.php/Conky "Conky")** — Lightweight, scriptable system monitor.

	[https://github.com/brndnmtthws/conky](https://github.com/brndnmtthws/conky) || [conky](https://www.archlinux.org/packages/?name=conky)

*   **Collectd** — A simple, extensible system monitoring daemon based on [rrdtool](http://oss.oetiker.ch/rrdtool/). It has a small footprint and can be set up either stand-alone or as a server/client application.

	[https://collectd.org/](https://collectd.org/) || [collectd](https://www.archlinux.org/packages/?name=collectd)

*   **collectl** — Collectl is a light-weight performance monitoring tool capable of reporting interactively as well as logging to disk. It reports statistics on cpu, disk, infiniband, lustre, memory, network, nfs, process, quadrics, slabs and more in easy to read format.

	[http://collectl.sourceforge.net/](http://collectl.sourceforge.net/) || [collectl](https://aur.archlinux.org/packages/collectl/)

*   **dstat** — Versatile resource statistics tool.

	[http://dag.wieers.com/home-made/dstat/](http://dag.wieers.com/home-made/dstat/) || [dstat](https://www.archlinux.org/packages/?name=dstat) or [dstat-py3](https://aur.archlinux.org/packages/dstat-py3/)

*   **[Fsniper](/index.php/Fsniper "Fsniper")** — Daemon to run scripts based on changes in files monitored by inotify.

	[http://projects.l3ib.org/fsniper/](http://projects.l3ib.org/fsniper/) || [fsniper](https://aur.archlinux.org/packages/fsniper/)

*   **[GKrellM](https://en.wikipedia.org/wiki/GKrellM "wikipedia:GKrellM")** — Simple, flexible system monitor package for [GTK+](/index.php/GTK%2B "GTK+") with many plug-ins.

	[http://billw2.github.io/gkrellm/gkrellm.html](http://billw2.github.io/gkrellm/gkrellm.html) || [gkrellm](https://www.archlinux.org/packages/?name=gkrellm)

*   **glances** — CLI curses-based monitoring tool in Python.

	[http://nicolargo.github.io/glances](http://nicolargo.github.io/glances) || [glances](https://www.archlinux.org/packages/?name=glances)

*   **gnome-system-monitor** — A system monitor for [GNOME](/index.php/GNOME "GNOME").

	[https://help.gnome.org/users/gnome-system-monitor/](https://help.gnome.org/users/gnome-system-monitor/) || [gnome-system-monitor](https://www.archlinux.org/packages/?name=gnome-system-monitor) [gnome-system-monitor-gtk2](https://aur.archlinux.org/packages/gnome-system-monitor-gtk2/)

*   **[htop](https://en.wikipedia.org/wiki/Htop "wikipedia:Htop")** — Simple, ncurses interactive process viewer.

	[http://htop.sourceforge.net/](http://htop.sourceforge.net/) || [htop](https://www.archlinux.org/packages/?name=htop)

*   **[KSysGuard](https://en.wikipedia.org/wiki/KDE_System_Guard "wikipedia:KDE System Guard")** — Also known as KSysguard, is the [KDE](/index.php/KDE "KDE") task manager and performance monitor.

	[https://userbase.kde.org/KSysGuard](https://userbase.kde.org/KSysGuard) || [ksysguard](https://www.archlinux.org/packages/?name=ksysguard) or as part of [kdebase-workspace](https://aur.archlinux.org/packages/kdebase-workspace/)

*   **linux process explorer** — Graphical process explorer for Linux.

	[https://sourceforge.net/projects/procexp/](https://sourceforge.net/projects/procexp/) || [procexp](https://aur.archlinux.org/packages/procexp/)

*   **LXTask** — Lightweight task manager for [LXDE](/index.php/LXDE "LXDE").

	[http://wiki.lxde.org/en/LXTask](http://wiki.lxde.org/en/LXTask) || [lxtask](https://www.archlinux.org/packages/?name=lxtask)

*   **mate-system-monitor** — A GTK2 system monitor for [MATE](/index.php/MATE "MATE").

	[https://github.com/mate-desktop/mate-system-monitor](https://github.com/mate-desktop/mate-system-monitor) || [mate-system-monitor](https://www.archlinux.org/packages/?name=mate-system-monitor)

*   **netdata** — A web-based real-time performance monitor

	[https://github.com/firehol/netdata/wiki](https://github.com/firehol/netdata/wiki) || [netdata](https://www.archlinux.org/packages/?name=netdata)

*   **Task Manager** — GTK2 process mangement application for [Xfce](/index.php/Xfce "Xfce").

	[http://goodies.xfce.org/projects/applications/xfce4-taskmanager](http://goodies.xfce.org/projects/applications/xfce4-taskmanager) || [xfce4-taskmanager](https://www.archlinux.org/packages/?name=xfce4-taskmanager)

*   **[Telegraf](/index.php/Telegraf "Telegraf")** — Telegraf is an agent written in Go for collecting, processing, aggregating, and writing metrics.

	[https://docs.influxdata.com/telegraf/latest/](https://docs.influxdata.com/telegraf/latest/) || [telegraf](https://aur.archlinux.org/packages/telegraf/)

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

*   **[archey3](/index.php/Archey3 "Archey3")** — Python script to display system infomation alongside the Arch Linux logo.

	[https://lclarkmichalek.github.io/archey3](https://lclarkmichalek.github.io/archey3) || [archey3](https://www.archlinux.org/packages/?name=archey3)

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

*   **hardinfo** — A small application that displays information about your hardware and operating system, it looks like the Device Manager in Windows.

	[http://hardinfo.berlios.de/HomePage](http://hardinfo.berlios.de/HomePage) || [hardinfo](https://www.archlinux.org/packages/?name=hardinfo)

*   **i-Nex** — An application that gathers information for hardware components available on your system and displays it using an user interface similar to the popular Windows tool CPU-Z.

	[http://i-nex.linux.pl/](http://i-nex.linux.pl/) || [i-nex-git](https://aur.archlinux.org/packages/i-nex-git/)

*   **lshw** — A small tool to provide detailed information on the hardware configuration of the machine with CLI and GTK interfaces.

	[http://ezix.org/project/wiki/HardwareLiSter](http://ezix.org/project/wiki/HardwareLiSter) || [lshw](https://www.archlinux.org/packages/?name=lshw)

*   **KDE Info Center** — Shows hardware and software information.

	[https://www.kde.org/applications/system/kinfocenter/](https://www.kde.org/applications/system/kinfocenter/) || [kinfocenter](https://www.archlinux.org/packages/?name=kinfocenter)

### Keyboard layout switchers

*   **fbxkb** — A NETWM compliant keyboard indicator and switcher. It shows a flag of current keyboard in a systray area and allows you to switch to another one.

	[http://fbxkb.sourceforge.net/](http://fbxkb.sourceforge.net/) || [fbxkb](https://aur.archlinux.org/packages/fbxkb/)

*   **xxkb** — A lightweight keyboard layout indicator and switcher.

	[https://sourceforge.net/projects/xxkb/](https://sourceforge.net/projects/xxkb/) || [xxkb](https://www.archlinux.org/packages/?name=xxkb)

*   **qxkb** — A keyboard switcher written in Qt.

	[https://github.com/disels/qxkb](https://github.com/disels/qxkb) || [qxkb](https://aur.archlinux.org/packages/qxkb/)

*   **[X Neural Switcher](https://en.wikipedia.org/wiki/X_Neural_Switcher "wikipedia:X Neural Switcher")** — A text analyser, it detects the language of the input and corrects the keyboard layout if needed.

	[http://www.xneur.ru/](http://www.xneur.ru/) || [xneur](https://aur.archlinux.org/packages/xneur/), [gxneur](https://aur.archlinux.org/packages/gxneur/) (GUI)

### Power management

See [Power management](/index.php/Power_management "Power management").

### Clipboard managers

See: [List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard").

### Package management

See [pacman tips#Utilities](/index.php/Pacman_tips#Utilities "Pacman tips").

### Input methods

See the main article: [Internationalization#Input methods in Xorg](/index.php/Internationalization#Input_methods_in_Xorg "Internationalization").

## Documents and texts

### Office suites

See also [Wikipedia:Comparison of office suites](https://en.wikipedia.org/wiki/Comparison_of_office_suites "wikipedia:Comparison of office suites").

*   **[Calligra](https://en.wikipedia.org/wiki/Calligra_Suite "wikipedia:Calligra Suite")** — Actively developed fork of KOffice, the [KDE](/index.php/KDE "KDE") office suite. It offers most of the features of OpenOffice while also having versions for smartphones (Calligra Mobile) and tablets (Calligra Active).

	[https://www.calligra.org/](https://www.calligra.org/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[LibreOffice](/index.php/LibreOffice "LibreOffice")** — More actively developed fork of OpenOffice.

	[https://www.libreoffice.org/](https://www.libreoffice.org/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice](/index.php/OpenOffice "OpenOffice")** — Open-source office software suite for word processing, spreadsheets, presentations, graphics, databases and more, under the Apache Licence.

	[http://www.openoffice.org/](http://www.openoffice.org/) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **[SoftMaker Office](https://en.wikipedia.org/wiki/SoftMaker_Office "wikipedia:SoftMaker Office")** — A complete, reliable, lightning-fast and Microsoft Office-compatible office suite with a word processor, spreadsheet, and presentation graphics software.

	[http://www.freeoffice.com/](http://www.freeoffice.com/) || [freeoffice](https://aur.archlinux.org/packages/freeoffice/)

*   **Unoconv** — Libreoffice-based document converter.

	[http://dag.wiee.rs/home-made/unoconv/](http://dag.wiee.rs/home-made/unoconv/) || [unoconv](https://www.archlinux.org/packages/?name=unoconv)

*   **[WPS Office](https://en.wikipedia.org/wiki/Kingsoft_Office "wikipedia:Kingsoft Office")** — Proprietary office productivity suite, previously known as Kingsoft Office.

	[http://www.wps.com/](http://www.wps.com/) || [wps-office](https://aur.archlinux.org/packages/wps-office/)

### Word processors

See also [Wikipedia:Comparison of word processors](https://en.wikipedia.org/wiki/Comparison_of_word_processors "wikipedia:Comparison of word processors").

*   **[Abiword](/index.php/Abiword "Abiword")** — Full-featured word processor.

	[http://www.abisource.com/](http://www.abisource.com/) || [abiword](https://www.archlinux.org/packages/?name=abiword)

*   **[Antiword](/index.php?title=Antiword&action=edit&redlink=1 "Antiword (page does not exist)")** — MS Word reader.

	[http://www.winfield.demon.nl/](http://www.winfield.demon.nl/) || [antiword](https://www.archlinux.org/packages/?name=antiword)

*   **[BlueGriffon](https://en.wikipedia.org/wiki/BlueGriffon "wikipedia:BlueGriffon")** — WYSIWYG content editor for the World Wide Web.

	[http://www.bluegriffon.com/](http://www.bluegriffon.com/) || [bluegriffon](https://www.archlinux.org/packages/?name=bluegriffon)

*   **[Calligra Words](https://en.wikipedia.org/wiki/Calligra_Words "wikipedia:Calligra Words")** — Powerful word processor included in the Calligra Suite.

	[https://www.calligra.org/words/](https://www.calligra.org/words/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **gLabels** — Program for creating labels and business cards.

	[http://glabels.org/](http://glabels.org/) || [glabels](https://www.archlinux.org/packages/?name=glabels)

*   **[KompoZer](https://en.wikipedia.org/wiki/KompoZer "wikipedia:KompoZer")** — A Dreamweaver style WYSIWYG web editor; Nvu unofficial bug-fix release.

	[http://kompozer.net/](http://kompozer.net/) || [kompozer](https://www.archlinux.org/packages/?name=kompozer)

*   **[LibreOffice Writer](/index.php/LibreOffice "LibreOffice")** — Full-featured word processor included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/writer](https://www.libreoffice.org/discover/writer) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice Writer](/index.php/OpenOffice "OpenOffice")** — Full-featured word processor included in the OpenOffice suite.

	[http://www.openoffice.org/](http://www.openoffice.org/) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

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

	[http://asciidoctor.org/](http://asciidoctor.org/) || [asciidoctor](https://www.archlinux.org/packages/?name=asciidoctor)

*   **[Markdown](https://en.wikipedia.org/wiki/Markdown "wikipedia:Markdown")** — Text-to-HTML conversion tool that allows you to write using a simple plain text format.

	[http://daringfireball.net/projects/markdown](http://daringfireball.net/projects/markdown) || [discount](https://www.archlinux.org/packages/?name=discount)

*   **[Pandoc](https://en.wikipedia.org/wiki/Pandoc "wikipedia:Pandoc")** — Swiss-army knife for converting one markup format into another.

	[http://johnmacfarlane.net/pandoc](http://johnmacfarlane.net/pandoc) || [pandoc](https://www.archlinux.org/packages/?name=pandoc)

*   **[Sphinx](https://en.wikipedia.org/wiki/Sphinx_(documentation_generator) "wikipedia:Sphinx (documentation generator)")** — A documentation generation system using [reStructuredText](https://en.wikipedia.org/wiki/ReStructuredText "wikipedia:ReStructuredText") to generate output in multiple formats (primary documentation system for the Python project).

	[http://sphinx-doc.org](http://sphinx-doc.org) || [python-sphinx](https://www.archlinux.org/packages/?name=python-sphinx)

*   **[txt2tags](https://en.wikipedia.org/wiki/Txt2tags "wikipedia:Txt2tags")** — Dead-simple, KISS-compliant lightweight, human-readable markup language to produce rich format content out of plain text files.

	[http://txt2tags.sourceforge.net](http://txt2tags.sourceforge.net) || [txt2tags](https://www.archlinux.org/packages/?name=txt2tags)

### Spreadsheets

See also [Wikipedia:Comparison of spreadsheet software](https://en.wikipedia.org/wiki/Comparison_of_spreadsheet_software "wikipedia:Comparison of spreadsheet software").

*   **[Calligra Sheets](https://en.wikipedia.org/wiki/Calligra_Sheets "wikipedia:Calligra Sheets")** — Powerful spreadsheet application included in the Calligra Suite

	[https://www.calligra.org/sheets/](https://www.calligra.org/sheets/) || [calligra](https://www.archlinux.org/packages/?name=calligra)

*   **[Gnumeric](/index.php/Gnumeric "Gnumeric")** — Spreadsheet program that is part of the GNOME desktop.

	[http://www.gnumeric.org/](http://www.gnumeric.org/) || [gnumeric](https://www.archlinux.org/packages/?name=gnumeric)

*   **[LibreOffice Calc](/index.php/LibreOffice "LibreOffice")** — Full-featured spreadsheet application included in the LibreOffice suite.

	[https://www.libreoffice.org/discover/calc/](https://www.libreoffice.org/discover/calc/) || [libreoffice-still](https://www.archlinux.org/packages/?name=libreoffice-still) or [libreoffice-fresh](https://www.archlinux.org/packages/?name=libreoffice-fresh)

*   **[OpenOffice Calc](/index.php/OpenOffice "OpenOffice")** — Full-featured spreadsheet application included in the OpenOffice suite.

	[http://openoffice.org/product/calc.html](http://openoffice.org/product/calc.html) || [openoffice](https://aur.archlinux.org/packages/openoffice/)

*   **Pyspread** — Pyspread is a non-traditional spreadsheet application that is based on and written in the programming language Python.

	[http://manns.github.io/pyspread/index.html](http://manns.github.io/pyspread/index.html) || [pyspread](https://aur.archlinux.org/packages/pyspread/)

*   **[sc](/index.php?title=Sc&action=edit&redlink=1 "Sc (page does not exist)")** — curses-based lightweight spreadsheet.

	[http://ibiblio.org/pub/linux/apps/financial/spreadsheet/!INDEX.html](http://ibiblio.org/pub/linux/apps/financial/spreadsheet/!INDEX.html) || [sc](https://www.archlinux.org/packages/?name=sc)

*   **sc-im** — spreadsheet program based on sc.

	[https://github.com/andmarti1424/sc-im/](https://github.com/andmarti1424/sc-im/) || [sc-im](https://aur.archlinux.org/packages/sc-im/)

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

*   **[JabRef](https://en.wikipedia.org/wiki/JabRef "wikipedia:JabRef")** — Java GUI frontend for managing BibTeX and other bibliographies.

	[http://jabref.sourceforge.net/index.php](http://jabref.sourceforge.net/index.php) || [jabref](https://aur.archlinux.org/packages/jabref/) [jabref-git](https://aur.archlinux.org/packages/jabref-git/)

*   **[Kile](https://en.wikipedia.org/wiki/Kile "wikipedia:Kile")** — User-friendly TeX/LaTeX editor for the KDE desktop with many features.

	[http://kile.sourceforge.net/](http://kile.sourceforge.net/) || [kile](https://www.archlinux.org/packages/?name=kile)

*   **Ktikz** — GUI making diagrams with [PGF/TikZ](http://pgf.sourceforge.net/) easier.

	[http://www.hackenberger.at/blog/ktikz-editor-for-the-tikz-language/](http://www.hackenberger.at/blog/ktikz-editor-for-the-tikz-language/) || [ktikz](https://aur.archlinux.org/packages/ktikz/)

*   **[LaTeXila](https://en.wikipedia.org/wiki/LaTeXila "wikipedia:LaTeXila")** — LaTeX editor for the GNOME Desktop including support for code completion, compiling and project management.

	[https://wiki.gnome.org/Apps/LaTeXila](https://wiki.gnome.org/Apps/LaTeXila) || [latexila](https://www.archlinux.org/packages/?name=latexila)

*   **[LyX](https://en.wikipedia.org/wiki/LyX "wikipedia:LyX")** — Document processor that encourages an approach to writing based on the structure of your documents (WYSIWYM) and not simply their appearance (WYSIWYG).

	[http://www.lyx.org/](http://www.lyx.org/) || [lyx](https://www.archlinux.org/packages/?name=lyx)

*   **[TeXmacs](https://en.wikipedia.org/wiki/GNU_TeXmacs "wikipedia:GNU TeXmacs")** — WYSIWYW (what you see is what you want) editing platform with special features for scientists.

	[http://www.texmacs.org/](http://www.texmacs.org/) || [texmacs](https://www.archlinux.org/packages/?name=texmacs)

*   **[Texmaker](https://en.wikipedia.org/wiki/Texmaker "wikipedia:Texmaker")** — Cross-platform, light and easy-to-use LaTeX IDE. It integrates many tools needed to develop documents with LaTeX, in just one application

	[http://www.xm1math.net/texmaker/](http://www.xm1math.net/texmaker/) || [texmaker](https://www.archlinux.org/packages/?name=texmaker)

*   **[TeXstudio](https://en.wikipedia.org/wiki/TeXstudio "wikipedia:TeXstudio")** — Fork of TeXMaker including support for code completion of bibtex items, grammar check and automatic detection of the need for multiple LaTeX runs.

	[http://texstudio.sourceforge.net/](http://texstudio.sourceforge.net/) || [texstudio](https://www.archlinux.org/packages/?name=texstudio)

*   **[Vim-LaTeX-suite](/index.php/Vim "Vim")** — Customizable LaTeX environment for Vim.

	[http://vim-latex.sourceforge.net/](http://vim-latex.sourceforge.net/) || [vim-latexsuite](https://www.archlinux.org/packages/?name=vim-latexsuite)

*   **[Vimtex](/index.php/Vim "Vim")** — This vim plugin is a fork of [LaTeX-Box](https://github.com/LaTeX-Box-Team/LaTeX-Box). It provides automatic syntax-based folding, omni-completion (for citations and labels), latexmk-based compilation and synctex functionality for [zathura](https://www.archlinux.org/packages/?name=zathura) and [mupdf](https://www.archlinux.org/packages/?name=mupdf).

	[https://github.com/lervag/vimtex/](https://github.com/lervag/vimtex/) ||

*   **[Zotero](https://en.wikipedia.org/wiki/Zotero "wikipedia:Zotero")** — This is a free, easy-to-use tool to help you collect, organize, cite, and share your research sources. There is a stand-alone version and a Firefox add-on available.

	[https://www.zotero.org/](https://www.zotero.org/) || [zotero](https://aur.archlinux.org/packages/zotero/)

### Translation and localization

*   **[Apertium](https://en.wikipedia.org/wiki/Apertium "wikipedia:Apertium")** — Free and open source rule-based machine translation platform with available language data. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, TMX, MediaWiki and others.

	[http://apertium.org/](http://apertium.org/) || [apertium](https://aur.archlinux.org/packages/apertium/)

*   **[Gtranslator](https://en.wikipedia.org/wiki/Gtranslator "wikipedia:Gtranslator")** — Enhanced gettext po file editor for the GNOME. It handles all forms of gettext po files and includes very useful features.

	[https://wiki.gnome.org/Apps/Gtranslator](https://wiki.gnome.org/Apps/Gtranslator) || [gtranslator](https://www.archlinux.org/packages/?name=gtranslator)

*   **Lokalize** — Standard [KDE](/index.php/KDE "KDE") tool for software translation. It includes basic editing of PO files, support for glossary, translation memory, project managing, etc. It belongs to [kdesdk](https://www.archlinux.org/groups/x86_64/kdesdk/)

	[https://userbase.kde.org/Lokalize](https://userbase.kde.org/Lokalize) || [lokalize](https://www.archlinux.org/packages/?name=lokalize)

*   **[Moses](https://en.wikipedia.org/wiki/Moses_(machine_translation) "wikipedia:Moses (machine translation)")** — Statistical machine translation tool (language data not included).

	[http://statmt.org/moses](http://statmt.org/moses) || [mosesdecoder](https://aur.archlinux.org/packages/mosesdecoder/) [mosesdecoder-git](https://aur.archlinux.org/packages/mosesdecoder-git/)

*   **[OmegaT](https://en.wikipedia.org/wiki/OmegaT "wikipedia:OmegaT")** — General translator's tool which contains a lot of translation memory features and can give suggestions from Google Translate. It supports the following formats: HTML, Microsoft Office 2007 XML, OpenDocument, XLIFF/Okapi, MediaWiki, plain text, TMX and others.

	[http://omegat.org](http://omegat.org) || [omegat](https://aur.archlinux.org/packages/omegat/)

*   **[Poedit](https://en.wikipedia.org/wiki/Poedit "wikipedia:Poedit")** — Simple gettext/po-based translation tool.

	[http://poedit.net](http://poedit.net) || [poedit](https://www.archlinux.org/packages/?name=poedit)

*   **Pology** — Set of Python tools for dealing with gettext/po-files.

	[https://techbase.kde.org/Localization/Tools/Pology](https://techbase.kde.org/Localization/Tools/Pology) || [pology](https://aur.archlinux.org/packages/pology/)

*   **[Virtaal](https://en.wikipedia.org/wiki/Virtaal and others.

	[http://virtaal.translatehouse.org/](http://virtaal.translatehouse.org/) || [virtaal](https://aur.archlinux.org/packages/virtaal/)

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

	[https://www.gnu.org/software/emacs/emacs.html](https://www.gnu.org/software/emacs/emacs.html) || [emacs-nox](https://www.archlinux.org/packages/?name=emacs-nox)

*   **[JED](https://en.wikipedia.org/wiki/JED_(text_editor) "wikipedia:JED (text editor)")** — Text editor that makes extensive use of the [S-Lang library](https://en.wikipedia.org/wiki/S-Lang_(programming_library) "wikipedia:S-Lang (programming library)"). Includes a console version (jed) and an X-window version (xjed).

	[http://jedsoft.org/jed/](http://jedsoft.org/jed/) || [jed](https://aur.archlinux.org/packages/jed/)

*   **Joe (Joe's Own Editor)** — Terminal-based text editor designed to be easy to use.

	[http://joe-editor.sourceforge.net/](http://joe-editor.sourceforge.net/) || [joe](https://www.archlinux.org/packages/?name=joe)

*   **[mcedit](https://en.wikipedia.org/wiki/Midnight_Commander "wikipedia:Midnight Commander")** — Useful text editor that comes with Midnight Commander file manager.

	[http://www.ibiblio.org/mc/](http://www.ibiblio.org/mc/) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **micro** — A modern and intuitive terminal-based text editor, written in go and extensible through plugins

	[https://micro-editor.github.io](https://micro-editor.github.io) || [micro](https://aur.archlinux.org/packages/micro/)

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

*   **Tilde** — An intuitive text editor with Windows-like key bindings.

	[http://os.ghalkes.nl/tilde/](http://os.ghalkes.nl/tilde/) || [tilde](https://aur.archlinux.org/packages/tilde/)

*   **[vile](https://en.wikipedia.org/wiki/Vile_(editor) "wikipedia:Vile (editor)")** — A lightweight Emacs clone with *vi*-like key bindings.

	[http://invisible-island.net/vile/vile.html](http://invisible-island.net/vile/vile.html) || [vile](https://www.archlinux.org/packages/?name=vile)

*   **[Zile](https://en.wikipedia.org/wiki/Zile_(editor) "wikipedia:Zile (editor)")** — A lightweight Emacs clone.

	[https://www.gnu.org/software/zile/](https://www.gnu.org/software/zile/) || [zile](https://www.archlinux.org/packages/?name=zile)

##### Vi text editors

*   **Kakoune** — Vim inspired. Fewer keystrokes. Multiple selections. Orthogonal design.

	[https://github.com/mawww/kakoune](https://github.com/mawww/kakoune) || [kakoune-git](https://aur.archlinux.org/packages/kakoune-git/)

*   **[Neovim](/index.php/Neovim "Neovim")** — Vim's rebirth for the 21st century

	[http://neovim.io/](http://neovim.io/) || [neovim](https://www.archlinux.org/packages/?name=neovim)

*   **[Vi](/index.php/Vi "Vi")** — The original ex/vi text editor.

	[http://ex-vi.sourceforge.net/](http://ex-vi.sourceforge.net/) || [vi](https://www.archlinux.org/packages/?name=vi)

*   **[Vim](/index.php/Vim "Vim") (Vi IMproved)** — Advanced text editor that seeks to provide the power of the de-facto Unix editor 'vi', with a more complete feature set.

	[http://www.vim.org/](http://www.vim.org/) || [vim](https://www.archlinux.org/packages/?name=vim)

*   **Vis** — modern, legacy free, simple yet efficient vim-like editor.

	[http://www.brain-dump.org/projects/vis/](http://www.brain-dump.org/projects/vis/) || [vis](https://www.archlinux.org/packages/?name=vis)

#### Graphical

*   **[Acme](https://en.wikipedia.org/wiki/Acme_(text_editor) "wikipedia:Acme (text editor)")** — Minimalist and flexible programming environment developed by Rob Pike for the Plan 9 operating system.

	[http://acme.cat-v.org](http://acme.cat-v.org) || [plan9port](https://www.archlinux.org/packages/?name=plan9port)

*   **[Atom](/index.php/Atom "Atom")** — A promising text editor developed by GitHub. With support for plug-ins written in Node.js and embedded [Git](/index.php/Git "Git") Control.

	[https://atom.io](https://atom.io) || [atom](https://www.archlinux.org/packages/?name=atom)

*   **Beaver** — A GTK+ editor designed to be modular, lightweight and stylish.

	[http://beaver-editor.sourceforge.net](http://beaver-editor.sourceforge.net) || [beaver](https://www.archlinux.org/packages/?name=beaver)

*   **[Brackets](https://en.wikipedia.org/wiki/Brackets_(text_editor) "w:Brackets (text editor)")** — An open source code editor for the web, written in JavaScript, HTML and CSS.

	[http://brackets.io](http://brackets.io) || [brackets](https://aur.archlinux.org/packages/brackets/)

*   **FeatherPad** — Minimal Qt5 plain text editor featuring a native dark theme and support for tabs, printing and syntax highlighting.

	[https://github.com/tsujan/FeatherPad](https://github.com/tsujan/FeatherPad) || [featherpad](https://aur.archlinux.org/packages/featherpad/)

*   **[Geany](https://en.wikipedia.org/wiki/Geany "wikipedia:Geany")** — A text editor using the GTK2 toolkit with basic features of an integrated development environment. It has support for TeX-based documents.

	[https://www.geany.org](https://www.geany.org) || [geany](https://www.archlinux.org/packages/?name=geany)

*   **[Gedit](https://en.wikipedia.org/wiki/Gedit "wikipedia:Gedit")** — GTK+ editor for the GNOME desktop with syntax highlighting, automatic indentation, matching brackets, etc., and a number of add-ons to increase functionality.

	[https://wiki.gnome.org/Apps/Gedit](https://wiki.gnome.org/Apps/Gedit) || [gedit](https://www.archlinux.org/packages/?name=gedit)

*   **[GNU Emacs](/index.php/GNU_Emacs "GNU Emacs")** — The extensible, customizable, self-documenting real-time display editor.

	[https://www.gnu.org/software/emacs/](https://www.gnu.org/software/emacs/) || [emacs](https://www.archlinux.org/packages/?name=emacs)

*   **[gVim](/index.php/GVim "GVim")** — Graphical interface for Vim.

	[http://www.vim.org](http://www.vim.org) || [gvim](https://www.archlinux.org/packages/?name=gvim)

*   **Jedit** — Text editor for programmers, written in Java.

	[http://www.jedit.org](http://www.jedit.org) || [jedit](https://www.archlinux.org/packages/?name=jedit)

*   **[JuffEd](https://en.wikipedia.org/wiki/JuffEd "wikipedia:JuffEd")** — Simple tabbed text editor with syntax highlighting, written in Qt.

	[http://juffed.com/en/index.html](http://juffed.com/en/index.html) || [juffed](https://aur.archlinux.org/packages/juffed/)

*   **[Kate](https://en.wikipedia.org/wiki/Kate_(text_editor) "wikipedia:Kate (text editor)")** — Full-featured programmer's editor for the KDE desktop with MDI and a filesystem browser.

	[https://kate-editor.org](https://kate-editor.org) || [kate](https://www.archlinux.org/packages/?name=kate)

*   **[KWrite](https://en.wikipedia.org/wiki/KWrite "wikipedia:KWrite")** — Lightweight text editor for the KDE desktop that uses the same editor widget as Kate.

	[https://www.kde.org/applications/utilities/kwrite](https://www.kde.org/applications/utilities/kwrite) || [kwrite](https://www.archlinux.org/packages/?name=kwrite)

*   **[Leafpad](https://en.wikipedia.org/wiki/Leafpad "wikipedia:Leafpad")** — Notepad clone for GTK+ that emphasizes simplicity.

	[http://tarot.freeshell.org/leafpad](http://tarot.freeshell.org/leafpad) || [leafpad](https://www.archlinux.org/packages/?name=leafpad)

*   **L3afpad** — Simple text editor forked from Leafpad, supports GTK+ 3.

	[https://github.com/stevenhoneyman/l3afpad](https://github.com/stevenhoneyman/l3afpad) || [l3afpad](https://www.archlinux.org/packages/?name=l3afpad)

*   **[LightTable](https://en.wikipedia.org/wiki/Light_Table_(software) "w:Light Table (software)")** — A modern open source text editor.

	[http://lighttable.com](http://lighttable.com) || [lighttable-bin](https://aur.archlinux.org/packages/lighttable-bin/)[lighttable-git](https://aur.archlinux.org/packages/lighttable-git/)

*   **Medit** — Programming and around-programming text editor.

	[http://mooedit.sourceforge.net](http://mooedit.sourceforge.net) || [medit](https://www.archlinux.org/packages/?name=medit)

*   **[Mousepad](https://en.wikipedia.org/wiki/Xfce#Mousepad "wikipedia:Xfce")** — Fast text editor for the Xfce Desktop Environment.

	[https://www.xfce.org](https://www.xfce.org) || [mousepad](https://www.archlinux.org/packages/?name=mousepad)

*   **[Nedit](https://en.wikipedia.org/wiki/NEdit "wikipedia:NEdit")** — Text editor for the Motif environment.

	[http://www.nedit.org](http://www.nedit.org) || [nedit](https://www.archlinux.org/packages/?name=nedit)

*   **[Pluma](/index.php/MATE "MATE")** — A powerful text editor for MATE.

	[http://mate-desktop.org](http://mate-desktop.org) || [pluma](https://www.archlinux.org/packages/?name=pluma)

*   **[PyRoom](https://en.wikipedia.org/wiki/PyRoom "wikipedia:PyRoom")** — Great distractionless PyGTK text editor, a clone of the infamous WriteRoom.

	[http://pyroom.org](http://pyroom.org) || [pyroom](https://aur.archlinux.org/packages/pyroom/)

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

	[https://www.sublimetext.com](https://www.sublimetext.com) || [sublime-text2](https://aur.archlinux.org/packages/sublime-text2/)

*   **[Sublime Text 3](https://en.wikipedia.org/wiki/Sublime_Text "wikipedia:Sublime Text")** — Closed-source C++ and Python-based editor with many advanced features and plugins while staying lightweight and pretty.

	[https://www.sublimetext.com](https://www.sublimetext.com) || [sublime-text-dev](https://aur.archlinux.org/packages/sublime-text-dev/)

*   **Tea** — Qt-based feature rich text editor.

	[http://semiletov.org/tea](http://semiletov.org/tea) || [tea](https://www.archlinux.org/packages/?name=tea)

*   **[Textadept](/index.php/Textadept "Textadept")** — Lua-extensible feature rich text editor based on Scintilla and written in C.

	[http://foicica.com/textadept](http://foicica.com/textadept) || [textadept](https://aur.archlinux.org/packages/textadept/)

*   **[Visual Studio Code](/index.php/Visual_Studio_Code "Visual Studio Code")** — Editor for building and debugging modern web and cloud applications.

	[https://code.visualstudio.com](https://code.visualstudio.com) || [visual-studio-code-bin](https://aur.archlinux.org/packages/visual-studio-code-bin/)

*   **XEdit** — Simple text editor for the X Window System.

	[https://www.x.org/wiki](https://www.x.org/wiki) || [xorg-xedit](https://www.archlinux.org/packages/?name=xorg-xedit)

##### Collaborative text editors

*   **Gobby** — Collaborative editor supporting multiple documents in one session and a multi-user chat.

	[https://gobby.github.io](https://gobby.github.io) || [gobby](https://www.archlinux.org/packages/?name=gobby)

### Readers and Viewers

#### E-book applications

**Note:** Some [PDF and DjVu viewers](#PDF_and_DjVu) also support other e-book formats.

*   **Bookworm** — eBook reader with epub, pdf, mobi, cbr support for Elementary OS.

	[https://babluboy.github.io/bookworm/](https://babluboy.github.io/bookworm/) || [bookworm](https://aur.archlinux.org/packages/bookworm/)

*   **[Calibre](https://en.wikipedia.org/wiki/Calibre_(software) "wikipedia:Calibre (software)")** — E-book library management application that can also convert between different formats and sync with a variety of e-book readers. Supported formats include CBZ, CBR, CBC, CHM, DJVU, EPUB, FictionBook, HTML, HTMLZ, LIT, LRF, Mobipocket, ODT, PDF, PRC, PDB, PML, RB, RTF, SNB, TCR, TXT and TXTZ.

	[https://calibre-ebook.com/](https://calibre-ebook.com/) || [calibre](https://www.archlinux.org/packages/?name=calibre)

*   **Cool Reader** — E-book viewer with many supported formats such as EPUB (non-DRM), FictionBook, TXT, RTF, HTML, CHM and TCR.

	[https://sourceforge.net/projects/crengine/](https://sourceforge.net/projects/crengine/) || [coolreader3-git](https://aur.archlinux.org/packages/coolreader3-git/)

*   **epub** — A console EPUB reader using Python and Curses.

	[https://pypi.python.org/pypi/epub](https://pypi.python.org/pypi/epub) || [python-epub](https://aur.archlinux.org/packages/python-epub/)

*   **[FBReader](https://en.wikipedia.org/wiki/FBReader "wikipedia:FBReader")** — E-book viewer with many supported formats such as EPUB, FictionBook, HTML, plucker, PalmDoc, zTxt, TCR, CHM, RTF, OEB, Mobipocket (non-DRM) and TXT.

	[https://fbreader.org/](https://fbreader.org/) || [fbreader](https://www.archlinux.org/packages/?name=fbreader)

*   **[Sigil](https://en.wikipedia.org/wiki/Sigil_(application) "wikipedia:Sigil (application)")** — WYSIWYG ebook editor.

	[https://sigil-ebook.com/](https://sigil-ebook.com/) || [sigil](https://www.archlinux.org/packages/?name=sigil)

#### PDF and DjVu

**Note:** [PDF forms](https://en.wikipedia.org/wiki/Portable_Document_Format#Interactive_elements "wikipedia:Portable Document Format") support:

*   [acroread](https://aur.archlinux.org/packages/acroread/) is able to save both AcroForms and XFA forms into PDF files.
*   Poppler-based readers such as [evince](https://www.archlinux.org/packages/?name=evince) and [okular](https://www.archlinux.org/packages/?name=okular) support AcroForms, but not full XFA forms. [[3]](https://bugs.freedesktop.org/show_bug.cgi?id=18935) [[4]](https://bugs.launchpad.net/ubuntu/+source/poppler/+bug/321720)
*   For CJK(Chinese, Japanese, Korean) support in poppler-based readers such as [evince](https://www.archlinux.org/packages/?name=evince) and [okular](https://www.archlinux.org/packages/?name=okular), install [poppler-data](https://www.archlinux.org/packages/?name=poppler-data). poppler-data is an optional dependency of poppler which is an indirect dependency of evince and okular.

See also [Wikipedia:List of PDF software](https://en.wikipedia.org/wiki/List_of_PDF_software "wikipedia:List of PDF software") and [Wikipedia:DjVu](https://en.wikipedia.org/wiki/DjVu "wikipedia:DjVu").

##### Console

*   **fbgs** — Poor man's PostScript/pdf viewer for the linux framebuffer console.

	[https://www.kraxel.org/blog/linux/fbida/](https://www.kraxel.org/blog/linux/fbida/) || [fbida](https://www.archlinux.org/packages/?name=fbida)

*   **fbpdf** — Small framebuffer PDF and DjVu viewer based off of MuPDF, with [Vim](/index.php/Vim "Vim") keybindings and written in C

	[http://repo.or.cz/w/fbpdf.git](http://repo.or.cz/w/fbpdf.git) || [fbpdf-git](https://aur.archlinux.org/packages/fbpdf-git/)

*   **ghostscript** — convert into PDF, reduce size of PDF documents with eg `gs -sDEVICE=pdfwrite -dCompatibilityLevel=1.4 -dPDFSETTINGS=/screen -dNOPAUSE -dQUIET -dBATCH -sOutputFile=output.pdf input.pdf`

	[https://www.ghostscript.com/](https://www.ghostscript.com/) || [ghostscript](https://www.archlinux.org/packages/?name=ghostscript)

*   **jfbview** — Framebuffer PDF and image viewer. Features include Vim-like controls, zoom-to-fit, a TOC (outline) view, fast multi-threaded rendering and asynchronous pre-caching. Originally a fork of *fbpdf* called *jfbpdf*, now completely rewritten.

	[https://seasonofcode.com/pages/jfbview.html](https://seasonofcode.com/pages/jfbview.html) || [jfbview](https://aur.archlinux.org/packages/jfbview/)

##### Graphical

**Note:** Some [web browsers](/index.php/List_of_applications/Internet#Web_browsers "List of applications/Internet") have support for displaying PDF files, either built-in or via plugin.

*   **acroread** — A PDF file viewer offered by Adobe (closed source).

	[http://www.adobe.com/products/reader.html](http://www.adobe.com/products/reader.html) || [acroread](https://aur.archlinux.org/packages/acroread/)

*   **apvlv** — Lightweight PDF/DjVu/UMD/TXT viewer with [Vim](/index.php/Vim "Vim") keybindings.

	[http://naihe2010.github.io/apvlv/](http://naihe2010.github.io/apvlv/) || [apvlv](https://www.archlinux.org/packages/?name=apvlv)

*   **Atril** — Simple multi-page document viewer for MATE.

	[https://github.com/mate-desktop/atril](https://github.com/mate-desktop/atril) || [atril](https://www.archlinux.org/packages/?name=atril)

*   **ePDFView** — Free lightweight PDF document viewer using the Poppler and GTK+ libraries. Development stopped.

	[http://freecode.com/projects/epdfview](http://freecode.com/projects/epdfview) || [epdfview](https://www.archlinux.org/packages/?name=epdfview)

*   **[Evince](https://en.wikipedia.org/wiki/Evince "wikipedia:Evince")** — Document viewer for multiple document formats. Supports PDF, PostScript, DjVu, TIFF and DVI.

	[https://wiki.gnome.org/Apps/Evince](https://wiki.gnome.org/Apps/Evince) || [evince](https://www.archlinux.org/packages/?name=evince)

*   **[Foxit Reader](https://en.wikipedia.org/wiki/Foxit_Reader "wikipedia:Foxit Reader")** — Small, fast (compared to Acrobat) PDF viewer. (closed source)

	[https://www.foxitsoftware.com/pdf-reader/](https://www.foxitsoftware.com/pdf-reader/) || [foxitreader](https://aur.archlinux.org/packages/foxitreader/)

*   **gv** — Graphical user interface for the Ghostscript interpreter that allows to view and navigate through PostScript and PDF documents.

	[https://www.gnu.org/software/gv/](https://www.gnu.org/software/gv/) || [gv](https://www.archlinux.org/packages/?name=gv)

*   **[llpp](/index.php/Llpp "Llpp")** — Very fast PDF reader based off of MuPDF, that supports continuous page scrolling, bookmarking, and text search through the whole document.

	[http://repo.or.cz/w/llpp.git](http://repo.or.cz/w/llpp.git) || [llpp](https://aur.archlinux.org/packages/llpp/)

*   **Master PDF Editor** — A functional proprietary PDF editor. Free non-commercial use. (closed source)

	[https://code-industry.net/free-pdf-editor/](https://code-industry.net/free-pdf-editor/) || [masterpdfeditor](https://aur.archlinux.org/packages/masterpdfeditor/)

*   **[MuPDF](/index.php/MuPDF "MuPDF")** — Very fast PDF, XPS, and EPUB viewer and toolkit written in portable C. Features CJK font support.

	[https://mupdf.com/](https://mupdf.com/) || [mupdf](https://www.archlinux.org/packages/?name=mupdf)

*   **[Okular](https://en.wikipedia.org/wiki/Okular "wikipedia:Okular")** — Universal PDF viewer for KDE.

	[https://okular.kde.org/](https://okular.kde.org/) || [okular](https://www.archlinux.org/packages/?name=okular)

*   **PDF Chain** — A graphical interface allowing to manipulate PDF documents (concatenate, burst, watermark, attach files...)

	[http://pdfchain.sourceforge.net/](http://pdfchain.sourceforge.net/) || [pdfchain](https://aur.archlinux.org/packages/pdfchain/)

*   **PdfMod** — You can reorder, rotate, and remove pages, export images from a document, edit the title, subject, author, and keywords, and combine documents via drag and drop.

	[https://wiki.gnome.org/Apps/PdfMod](https://wiki.gnome.org/Apps/PdfMod) || [pdfmod](https://www.archlinux.org/packages/?name=pdfmod)

*   **PDF Shuffler** — Combine, split, rotate and reorder PDF documents. Uses Python and GTK3.

	[https://sourceforge.net/projects/pdfshuffler/](https://sourceforge.net/projects/pdfshuffler/) || [pdfshuffler-git](https://aur.archlinux.org/packages/pdfshuffler-git/)

*   **PDF Studio** — All-in-one PDF editor similar to Adobe Acrobat (proprietary).

	[https://www.qoppa.com/pdfstudio/](https://www.qoppa.com/pdfstudio/) || [pdfstudio](https://aur.archlinux.org/packages/pdfstudio/)

*   **qpdfview** — Tabbed document viewer. It uses Poppler for PDF support, libspectre for PS support, DjVuLibre for DjVu support, CUPS for printing support and the Qt toolkit for its interface.

	[https://launchpad.net/qpdfview](https://launchpad.net/qpdfview) || [qpdfview](https://www.archlinux.org/packages/?name=qpdfview)

*   **[Xournal](https://en.wikipedia.org/wiki/Xournal "wikipedia:Xournal")** — Pdf viewer/note taking application.

	[http://xournal.sourceforge.net/](http://xournal.sourceforge.net/) || [xournal](https://www.archlinux.org/packages/?name=xournal)

*   **[Xpdf](https://en.wikipedia.org/wiki/Xpdf "wikipedia:Xpdf")** — Viewer that can decode LZW and read encrypted PDFs. Note that due to removal of all Type1 fonts from the gsfonts package, you will need to install them from an archive package - see [https://bugs.archlinux.org/task/50297](https://bugs.archlinux.org/task/50297)

	[http://www.xpdfreader.com/](http://www.xpdfreader.com/) || [xpdf](https://www.archlinux.org/packages/?name=xpdf) and [gsfonts-type1](https://aur.archlinux.org/packages/gsfonts-type1/)

*   **[zathura](https://en.wikipedia.org/wiki/Zathura_(document_viewer) "wikipedia:Zathura (document viewer)")** — Highly customizable and functional PDF/DjVu/PostScript/ComicBook viewer (plugin based).

	[https://pwmt.org/projects/zathura/](https://pwmt.org/projects/zathura/) || [zathura](https://www.archlinux.org/packages/?name=zathura) [zathura-pdf-mupdf](https://www.archlinux.org/packages/?name=zathura-pdf-mupdf) [zathura-djvu](https://www.archlinux.org/packages/?name=zathura-djvu)

#### Terminal pagers

See also [Wikipedia:Terminal pager](https://en.wikipedia.org/wiki/Terminal_pager "wikipedia:Terminal pager").

*   [more](https://en.wikipedia.org/wiki/More_(command) — A simple and feature-light pager. It is a part of the [util-linux](https://www.archlinux.org/packages/?name=util-linux) package.
*   **[less](/index.php/Core_utilities#less "Core utilities")** — A program similar to more, but with support for both forward and backward scrolling, as well as partial loading of files.

	[https://www.gnu.org/software/less/](https://www.gnu.org/software/less/) || [less](https://www.archlinux.org/packages/?name=less)

*   **[most](https://en.wikipedia.org/wiki/Most_(Unix) "wikipedia:Most (Unix)")** — A pager with support for multiple windows, left and right scrolling, and built-in colour support

	[http://www.jedsoft.org/most/](http://www.jedsoft.org/most/) || [most](https://www.archlinux.org/packages/?name=most)

*   **mcview** — A pager with mouse and colour support. It is bundled with midnight commander.

	[http://midnight-commander.org/](http://midnight-commander.org/) || [mc](https://www.archlinux.org/packages/?name=mc)

*   **vimpager** — A script that turns vim into a pager. As a result, you get various vim features such as colour schemes, mouse support, split screens, etc.

	[https://github.com/rkitover/vimpager](https://github.com/rkitover/vimpager) || [vimpager](https://www.archlinux.org/packages/?name=vimpager)

#### CHM

See also [Wikipedia:Microsoft Compiled HTML Help](https://en.wikipedia.org/wiki/Microsoft_Compiled_HTML_Help "wikipedia:Microsoft Compiled HTML Help").

*   **Archmage** — An extensible reader and decompiler for files in the CHM format.

	[https://github.com/dottedmag/archmage](https://github.com/dottedmag/archmage) || [archmage](https://aur.archlinux.org/packages/archmage/)

*   **ChmSee** — CHM viewer based on xulrunner.

	[https://code.google.com/archive/p/chmsee/](https://code.google.com/archive/p/chmsee/) || [chmsee](https://aur.archlinux.org/packages/chmsee/)

*   **Kchmviewer** — Qt-based CHM viewer that uses chmlib and borrows some ideas from xchm. It does not depend on [KDE](/index.php/KDE "KDE"), but it can be compiled to integrate with it.

	[http://www.ulduzsoft.com/linux/kchmviewer/](http://www.ulduzsoft.com/linux/kchmviewer/) || [kchmviewer](https://www.archlinux.org/packages/?name=kchmviewer)

*   **[xCHM](https://en.wikipedia.org/wiki/xCHM "wikipedia:xCHM")** — Lightweight CHM viewer, based on chmlib.

	[http://xchm.sourceforge.net/](http://xchm.sourceforge.net/) || [xchm](https://www.archlinux.org/packages/?name=xchm)

#### Comic book (comix/manga)

*   **[MComix](https://en.wikipedia.org/wiki/MComix "wikipedia:MComix")** — GTK2 image viewer specifically designed to handle comic book archives (fork of Comix). Also includes library manager.

	[https://sourceforge.net/projects/mcomix/](https://sourceforge.net/projects/mcomix/) || [mcomix](https://www.archlinux.org/packages/?name=mcomix)

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

	[https://www.gnu.org/software/ocrad/](https://www.gnu.org/software/ocrad/) || [ocrad](https://www.archlinux.org/packages/?name=ocrad)

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

	[https://userbase.kde.org/BasKet](https://userbase.kde.org/BasKet) || [basket](https://www.archlinux.org/packages/?name=basket)

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

*   **[org-mode](https://en.wikipedia.org/wiki/org-mode "wikipedia:org-mode")** — [Emacs](/index.php/Emacs "Emacs") mode for notes, project planning and authoring.

	[http://orgmode.org](http://orgmode.org) || [emacs-org-mode](https://aur.archlinux.org/packages/emacs-org-mode/)

*   **nixnote** — Evernote's third Opensource application, formerly called Nevernote.

	[http://www.sourceforge.net/projects/nevernote](http://www.sourceforge.net/projects/nevernote) || [nixnote2](https://aur.archlinux.org/packages/nixnote2/)

*   **[QOwnNotes](https://en.wikipedia.org/wiki/QOwnNotes "wikipedia:QOwnNotes")** — An open source notepad and todo list manager with markdown support and optional ownCloud integration built on qt5.

	[http://www.qownnotes.org/](http://www.qownnotes.org/) || [qownnotes](https://aur.archlinux.org/packages/qownnotes/)

*   **RedNotebook** — Modern journal, which lets you format, tag and search your entries.

	[http://rednotebook.sourceforge.net/](http://rednotebook.sourceforge.net/) || [rednotebook](https://aur.archlinux.org/packages/rednotebook/)

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

	[https://waf.io/semantik.html](https://waf.io/semantik.html) || [semantik](https://aur.archlinux.org/packages/semantik/)

*   **TreeSheets** — The ultimate replacement for spreadsheets, mind mappers, outliners, PIMs, text editors and small databases.

	[http://strlen.com/treesheets/](http://strlen.com/treesheets/) || [treesheets-git](https://aur.archlinux.org/packages/treesheets-git/)

*   **View Your Mind** — Tool to generate and manipulate maps which show your thoughts. Such maps can help you to improve your creativity and effectivity. You can use them for time management, to organize tasks, to get an overview over complex contexts, to sort your ideas etc.

	[http://www.insilmaril.de/vym/](http://www.insilmaril.de/vym/) || [vym](https://www.archlinux.org/packages/?name=vym)

*   **Visual Understanding Environment** — Open Source project focused on creating flexible tools for managing and integrating digital resources in support of teaching, learning and research.

	[http://vue.tufts.edu](http://vue.tufts.edu) || [vue](https://aur.archlinux.org/packages/vue/)

*   **XMind** — Brainstorming and mind mapping application. It provides a rich set of different visualization styles, and allows sharing of created mind maps via their website.

	[http://www.xmind.net](http://www.xmind.net) || [xmind](https://aur.archlinux.org/packages/xmind/)

### Character Selector

*   **GNOME Characters** — Character map application for GNOME

	[https://wiki.gnome.org/Design/Apps/CharacterMap](https://wiki.gnome.org/Design/Apps/CharacterMap) || [gnome-characters](https://www.archlinux.org/packages/?name=gnome-characters)

*   **gucharmap** — A GTK+ 3 Character Selector, distributed with GNOME desktop.

	[https://wiki.gnome.org/Apps/Gucharmap](https://wiki.gnome.org/Apps/Gucharmap) || [gucharmap](https://www.archlinux.org/packages/?name=gucharmap)

*   **kdeutils-kcharselect** — A tool to select special characters from all installed fonts and copy them into the clipboard. Distributed with KDE.

	[https://utils.kde.org/projects/kcharselect/](https://utils.kde.org/projects/kcharselect/) || [kcharselect](https://www.archlinux.org/packages/?name=kcharselect)

### Stylus notes taking

*   **Write** — A word processor for hand writing.

	[http://www.styluslabs.com/](http://www.styluslabs.com/) || [write_stylus](https://aur.archlinux.org/packages/write_stylus/)

*   **Gournal** — Note-taking application written for usage on Tablet-PC, written in perl.

	[http://www.adebenham.com/old-stuff/gournal/](http://www.adebenham.com/old-stuff/gournal/) || [gournal](https://aur.archlinux.org/packages/gournal/)

*   **Xournal** — An application for notetaking, sketching, keeping a journal using a stylus.

	[http://xournal.sourceforge.net/](http://xournal.sourceforge.net/) || [xournal](https://www.archlinux.org/packages/?name=xournal)

*   **Xournal++** — A C++ rewrite of Xournal.

	[https://github.com/xournalpp/xournalpp](https://github.com/xournalpp/xournalpp) || [xournalpp-git](https://aur.archlinux.org/packages/xournalpp-git/)

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

### Barcode generators and readers

#### Console

*   **barcode** — A tool to convert text strings to printed bars.

	[https://www.gnu.org/software/barcode/](https://www.gnu.org/software/barcode/) || [barcode](https://www.archlinux.org/packages/?name=barcode)

*   **iec16022** — Produce 2D barcodes often also referenced as DataMatrix.

	[https://datenfreihafen.org/projects/iec16022.html](https://datenfreihafen.org/projects/iec16022.html) || [iec16022](https://www.archlinux.org/packages/?name=iec16022)

*   **qrencode** — C library and command line tool for encoding data in a QR Code symbol.

	[https://fukuchi.org/works/qrencode/](https://fukuchi.org/works/qrencode/) || [qrencode](https://www.archlinux.org/packages/?name=qrencode)

*   **ZBar** — Application and library for reading bar codes from various sources.

	[http://zbar.sourceforge.net/](http://zbar.sourceforge.net/) || [zbar](https://www.archlinux.org/packages/?name=zbar)

*   **Zint** — Barcode encoding library and command line tool supporting over 50 symbologies.

	[http://zint.org.uk/](http://zint.org.uk/) || [zint](https://www.archlinux.org/packages/?name=zint)

#### Graphical

*   **gLabels** — Program for creating labels and business cards. It also supports creating barcodes.

	[http://glabels.org/](http://glabels.org/) || [glabels](https://www.archlinux.org/packages/?name=glabels)

*   **Qreator** — Create your own QR codes.

	[http://davidplanella.org/project-showcase/qreator/](http://davidplanella.org/project-showcase/qreator/) || [qreator](https://aur.archlinux.org/packages/qreator/)

*   **QtQR** — QR Code generator and decoder.

	[https://launchpad.net/qr-tools](https://launchpad.net/qr-tools) || [qtqr](https://aur.archlinux.org/packages/qtqr/)

*   **Zint Barcode Studio** — Barcode generator GUI.

	[http://zint.org.uk/](http://zint.org.uk/) || [zint-qt](https://www.archlinux.org/packages/?name=zint-qt)

## Security

For detailed guides, see the main ArchWiki page, [Security](/index.php/Security "Security").

#### Network security

*   **[Arpwatch](https://en.wikipedia.org/wiki/Arpwatch "wikipedia:Arpwatch")** — Tool that monitors ethernet activity and keeps a database of Ethernet/IP address pairings.

	[http://ee.lbl.gov/](http://ee.lbl.gov/) || [arpwatch](https://www.archlinux.org/packages/?name=arpwatch)

*   **Bro** — Powerful network analysis framework that is much different from the typical IDS you may know.

	[https://www.bro.org/](https://www.bro.org/) || [bro-git](https://aur.archlinux.org/packages/bro-git/)

*   **EtherApe** — Graphical network monitor for Unix modeled after etherman. Featuring link layer, IP and TCP modes, it displays network activity graphically. Hosts and links change in size with traffic. Color coded protocols display.

	[http://etherape.sourceforge.net/](http://etherape.sourceforge.net/) || [etherape](https://www.archlinux.org/packages/?name=etherape)

*   **[Honeyd](/index.php/Honeyd "Honeyd")** — Tool that allows the user to set up and run multiple virtual hosts on a computer network.

	[http://www.honeyd.org/](http://www.honeyd.org/) || [honeyd](https://aur.archlinux.org/packages/honeyd/)

*   **IPTraf** — Console-based network monitoring utility.

	[https://sourceforge.net/projects/iptraf-ng/](https://sourceforge.net/projects/iptraf-ng/) || [iptraf-ng](https://www.archlinux.org/packages/?name=iptraf-ng)

*   **Kismet** — 802.11 layer2 wireless network detector, sniffer, and intrusion detection system.

	[https://www.kismetwireless.net/](https://www.kismetwireless.net/) || [kismet](https://www.archlinux.org/packages/?name=kismet)

*   **Nemesis** — Command-line network packet crafting and injection utility.

	[http://nemesis.sourceforge.net/](http://nemesis.sourceforge.net/) || [nemesis](https://www.archlinux.org/packages/?name=nemesis)

*   **[Nmap](/index.php/Nmap "Nmap")** — Security scanner used to discover hosts and services on a computer network, thus creating a "map" of the network.

	[https://nmap.org/](https://nmap.org/) || [nmap](https://www.archlinux.org/packages/?name=nmap)

*   **[Ntop](/index.php/Ntop "Ntop")** — Network probe that shows network usage in a way similar to what top does for processes.

	[http://www.ntop.org/](http://www.ntop.org/) || [ntop](https://www.archlinux.org/packages/?name=ntop)

*   **[Snort](/index.php/Snort "Snort")** — Network intrusion prevention and detection system.

	[https://www.snort.org/](https://www.snort.org/) || [snort](https://aur.archlinux.org/packages/snort/)

*   **Spectools** — A set of utilities for spectrum analyzer hardware including Wi-Spy devices.

	[https://www.kismetwireless.net/spectools/](https://www.kismetwireless.net/spectools/) || [spectools](https://aur.archlinux.org/packages/spectools/)

*   **[Sshguard](/index.php/Sshguard "Sshguard")** — Daemon that protects SSH and other services against brute-force attacts, similar to Fail2ban.

	[https://www.sshguard.net/](https://www.sshguard.net/) || [sshguard](https://www.archlinux.org/packages/?name=sshguard)

*   **[Suricata](/index.php/Suricata "Suricata")** — High performance Network IDS, IPS and Network Security Monitoring engine.

	[https://suricata-ids.org/](https://suricata-ids.org/) || [suricata](https://aur.archlinux.org/packages/suricata/)

*   **[Tcpdump](https://en.wikipedia.org/wiki/tcpdump "wikipedia:tcpdump")** — Common console-based packet analyzer that allows the user to intercept and display TCP/IP and other packets being transmitted or received over a network.

	[http://www.tcpdump.org/](http://www.tcpdump.org/) || [tcpdump](https://www.archlinux.org/packages/?name=tcpdump)

*   **[vnStat](/index.php/VnStat "VnStat")** — Console-based network traffic monitor that keeps a log of network traffic for the selected interfaces.

	[http://humdi.net/vnstat/](http://humdi.net/vnstat/) || [vnstat](https://www.archlinux.org/packages/?name=vnstat)

*   **[Wireshark](/index.php/Wireshark "Wireshark")** — Network protocol analyzer that lets you capture and interactively browse the traffic running on a computer network.

	[https://www.wireshark.org/](https://www.wireshark.org/) || [wireshark-cli](https://www.archlinux.org/packages/?name=wireshark-cli) [wireshark-qt](https://www.archlinux.org/packages/?name=wireshark-qt) [wireshark-gtk](https://www.archlinux.org/packages/?name=wireshark-gtk)

#### Threat and vulnerability detection

*   **AFICK** — Security tool that allows to monitor the changes on your files systems, and so can detect intrusions.

	[http://afick.sourceforge.net/](http://afick.sourceforge.net/) || [afick](https://aur.archlinux.org/packages/afick/)

*   **[Lynis](https://en.wikipedia.org/wiki/Lynis "wikipedia:Lynis")** — Security and system auditing tool to harden Unix/Linux systems.

	[https://cisofy.com/lynis/](https://cisofy.com/lynis/) || [lynis](https://www.archlinux.org/packages/?name=lynis)

*   **[Metasploit Framework](/index.php/Metasploit_Framework "Metasploit Framework")** — An advanced open-source platform for developing, testing, and using exploit code.

	[https://www.metasploit.com/](https://www.metasploit.com/) || [metasploit](https://www.archlinux.org/packages/?name=metasploit)

*   **[Nessus](/index.php/Nessus "Nessus")** — Comprehensive vulnerability scanning program.

	[http://www.nessus.org/products/nessus](http://www.nessus.org/products/nessus) || [nessus](https://aur.archlinux.org/packages/nessus/)

*   **[OpenVAS](/index.php/OpenVAS "OpenVAS")** — Framework of several services and tools offering a comprehensive and powerful vulnerability scanning and vulnerability management solution. FOSS Nessus fork.

	[http://www.openvas.org/](http://www.openvas.org/) || [openvas](https://www.archlinux.org/groups/x86_64/openvas/)

*   **OSSEC** — Open Source Host-based Intrusion Detection System that performs log analysis, file integrity checking, policy monitoring, rootkit detection, real-time alerting and active response.

	[https://ossec.github.io/](https://ossec.github.io/) || [ossec-agent](https://aur.archlinux.org/packages/ossec-agent/) [ossec-local](https://aur.archlinux.org/packages/ossec-local/) [ossec-server](https://aur.archlinux.org/packages/ossec-server/)

*   **Samhain** — Host-based intrusion detection system (HIDS) provides file integrity checking and log file monitoring/analysis, as well as rootkit detection, port monitoring, detection of rogue SUID executables, and hidden processes.

	[http://www.la-samhna.de/samhain/index.html](http://www.la-samhna.de/samhain/index.html) || [samhain](https://aur.archlinux.org/packages/samhain/)

*   **[Tiger](https://en.wikipedia.org/wiki/Tiger_(security_software) "wikipedia:Tiger (security software)")** — Security tool that can be use both as a security audit and intrusion detection system.

	[http://www.nongnu.org/tiger/](http://www.nongnu.org/tiger/) || [tiger](https://aur.archlinux.org/packages/tiger/)

*   **[Tripwire](https://en.wikipedia.org/wiki/Open_Source_Tripwire "wikipedia:Open Source Tripwire")** — Intrusion detection system.

	[https://github.com/Tripwire/tripwire-open-source](https://github.com/Tripwire/tripwire-open-source) || [tripwire-git](https://aur.archlinux.org/packages/tripwire-git/)

#### File security

*   **[AIDE](/index.php/AIDE "AIDE")** — File and directory integrity checker.

	[http://aide.sourceforge.net/](http://aide.sourceforge.net/) || [aide](https://www.archlinux.org/packages/?name=aide)

*   **Logcheck** — Simple utility which is designed to allow a system administrator to view the logfiles which are produced upon hosts under their control.

	[https://logcheck.alioth.debian.org/](https://logcheck.alioth.debian.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[Logwatch](/index.php/Logwatch "Logwatch")** — Customizable log analysis system.

	[https://sourceforge.net/projects/logwatch/](https://sourceforge.net/projects/logwatch/) || [logwatch](https://www.archlinux.org/packages/?name=logwatch)

*   **OpenDLP** — OpenDLP is a free and open source, agent- and agentless-based, centrally-managed, massively distributable data loss prevention tool.

	[https://code.google.com/archive/p/opendlp/](https://code.google.com/archive/p/opendlp/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

#### Anti malware

*   **[ClamAV](/index.php/ClamAV "ClamAV")** — Open source antivirus engine for detecting trojans, viruses, malware & other malicious threats.

	[http://www.clamav.net/](http://www.clamav.net/) || [clamav](https://www.archlinux.org/packages/?name=clamav)

*   **Linux Malware Detect** — Malware scanner designed around the threats faced in shared hosted environments.

	[https://www.rfxn.com/projects/linux-malware-detect/](https://www.rfxn.com/projects/linux-malware-detect/) || [maldet](https://aur.archlinux.org/packages/maldet/)

*   **Rootkit Hunter** — Checks machines for the presence of rootkits and other unwanted tools.

	[http://rkhunter.sourceforge.net/](http://rkhunter.sourceforge.net/) || [rkhunter](https://www.archlinux.org/packages/?name=rkhunter)

*   **Hostsblock** — A script that downloads, sorts, and compiles multiple ad- and malware-blocking hosts files.

	[http://gaenserich.github.io/hostsblock/](http://gaenserich.github.io/hostsblock/) || [hostsblock](https://aur.archlinux.org/packages/hostsblock/)

#### Backup programs

See the main article: [Synchronization and backup programs](/index.php/Synchronization_and_backup_programs "Synchronization and backup programs").

See also [Wikipedia:Comparison of backup software](https://en.wikipedia.org/wiki/Comparison_of_backup_software "wikipedia:Comparison of backup software").

#### Screen lockers

**Warning:** Only *sflock*, *physlock*, *Cinnamon Screensaver*, *MATE Screensaver* and *GNOME Screensaver* are able to block tty access. See [Xorg#Block TTY access](/index.php/Xorg#Block_TTY_access "Xorg") on how to manually block tty access.

*   **Cinnamon Screensaver** — Screen locker for the Cinnamon desktop.

	[https://github.com/linuxmint/cinnamon-screensaver](https://github.com/linuxmint/cinnamon-screensaver) || [cinnamon-screensaver](https://www.archlinux.org/packages/?name=cinnamon-screensaver)

*   **GNOME Screensaver** — Screen locker for the GNOME Flashback desktop.

	[https://wiki.gnome.org/Projects/GnomeScreensaver](https://wiki.gnome.org/Projects/GnomeScreensaver) || [gnome-screensaver](https://www.archlinux.org/packages/?name=gnome-screensaver)

*   **i3lock** — A simple screen locker. Provides user feedback, uses PAM authentication, supports DPMS. The background can be set to an image or solid color.

	[https://i3wm.org/i3lock/](https://i3wm.org/i3lock/) || [i3lock](https://www.archlinux.org/packages/?name=i3lock)

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

*   **[slock](/index.php/Slock "Slock")** — Very simple and lightweight X screen locker. Offers only a black background when locked, there are no animations or text fields.

	[https://tools.suckless.org/slock/](https://tools.suckless.org/slock/) || [slock](https://www.archlinux.org/packages/?name=slock)

*   **sxlock** — Fork of sflock with a few enhancements. Provides basic user feedback, uses PAM authentication, supports DPMS and RandR. Supports `sxlock.service` to lock the screen on suspend/hibernation. See the [README](https://github.com/lahwaacz/sxlock/blob/master/README.md) for more information.

	[https://github.com/lahwaacz/sxlock](https://github.com/lahwaacz/sxlock) || [sxlock-git](https://aur.archlinux.org/packages/sxlock-git/)

*   **tsscreenlock** — Screen locker used in theShell. Shows music controls, and if used with theShell, also shows desktop notifications.

	[https://github.com/vicr123/tsscreenlock](https://github.com/vicr123/tsscreenlock) || [tsscreenlock](https://aur.archlinux.org/packages/tsscreenlock/)

*   **vlock** — TTY locker. A mirror of the [original vlock](https://lists.archlinux.org/pipermail/aur-general/2013-July/024662.html) is available at [github](https://github.com/WorMzy/vlock).

	[http://www.kbd-project.org](http://www.kbd-project.org) || [kbd](https://www.archlinux.org/packages/?name=kbd)

*   **xlockmore** — Simple X11 screen lock with PAM support.

	[http://sillycycle.com/xlockmore.html](http://sillycycle.com/xlockmore.html) || [xlockmore](https://www.archlinux.org/packages/?name=xlockmore)

*   **[XScreenSaver](/index.php/XScreenSaver "XScreenSaver")** — Screen saver and locker for the X Window System.

	[https://www.jwz.org/xscreensaver/](https://www.jwz.org/xscreensaver/) || [xscreensaver](https://www.archlinux.org/packages/?name=xscreensaver)

*   **XSecureLock** — X11 screen lock utility designed with the primary goal of security.

	[https://github.com/google/xsecurelock](https://github.com/google/xsecurelock) || [xsecurelock-git](https://aur.archlinux.org/packages/xsecurelock-git/)

*   **xtrlock** — Very lightweight X display locker. Keeps windows visible and displays lock icon instead of mouse cursor. Typing password followed by enter unlocks the screen.

	[https://packages.debian.org/sid/xtrlock](https://packages.debian.org/sid/xtrlock) || [xtrlock](https://www.archlinux.org/packages/?name=xtrlock)

#### Hash checkers

*   **cfv** — Tiny utility to both test and create checksum files, support `.sfv`, `.csv`, `.crc`, `.md5`, `md5sum`, `sha1sum`, `.torrent`, `par`, and `.par2` files.

	[http://cfv.sourceforge.net/](http://cfv.sourceforge.net/) || [cfv](https://www.archlinux.org/packages/?name=cfv)

*   **GtkHash** — A GTK+ utility for computing message digests or checksums

	[http://gtkhash.sourceforge.net/](http://gtkhash.sourceforge.net/) || [gtkhash](https://aur.archlinux.org/packages/gtkhash/)

*   **hashdeep** — A cross-platform tools to computer hashes, or message digests, for any number of files

	[http://md5deep.sourceforge.net/](http://md5deep.sourceforge.net/) || [hashdeep](https://aur.archlinux.org/packages/hashdeep/)

*   **Parano** — A GNOME frontend for creating/editing/checking MD5 and SFV files

	[http://parano.berlios.de/](http://parano.berlios.de/) || [parano](https://aur.archlinux.org/packages/parano/)

*   **Quick Hash GUI** — A GUI to enable the rapid selection and subsequent hashing of files (individually or recursively throughout a folder structure) text and (on Linux) disks.

	[https://sourceforge.net/projects/quickhash/](https://sourceforge.net/projects/quickhash/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **RHash** — Utility for verifying hash sums (SFV, CRC, etc). Supports lots of algorithms.

	[http://rhash.anz.ru/](http://rhash.anz.ru/) || [rhash](https://www.archlinux.org/packages/?name=rhash)

*   **MassHash** — A set of file hashing tools (both CLI and GTK+ GUI) written in Python. Supported algorithms include MD5, SHA-1, SHA-224, SHA-256, SHA-384, SHA-512.

	[http://jdleicher.github.io/MassHash/](http://jdleicher.github.io/MassHash/) || [masshash](https://aur.archlinux.org/packages/masshash/)

*   **Parchive** — Utility which creates and uses PAR2 files to detect damage in data files and repair them if necessary.

	[https://github.com/Parchive/par2cmdline](https://github.com/Parchive/par2cmdline) || [par2cmdline](https://www.archlinux.org/packages/?name=par2cmdline)

#### Encryption, signing, steganography

*   **ccrypt** — A command-line utility for encrypting and decrypting files and streams.

	[http://ccrypt.sourceforge.net/](http://ccrypt.sourceforge.net/) || [ccrypt](https://www.archlinux.org/packages/?name=ccrypt)

*   **[Enigmail](https://en.wikipedia.org/wiki/Enigmail "wikipedia:Enigmail")** — A security extension to Mozilla Thunderbird and Seamonkey. It enables you to write and receive email messages signed and/or encrypted with the OpenPGP standard.

	[https://enigmail.net](https://enigmail.net) || [thunderbird-enigmail](https://aur.archlinux.org/packages/thunderbird-enigmail/)

*   **GNOME Keysign** — A GTK/GNOME application to use GnuPG for signing other people's keys. Quickly, easily, and securely.

	[https://wiki.gnome.org/Apps/Keysign/](https://wiki.gnome.org/Apps/Keysign/) || [gnome-keysign](https://aur.archlinux.org/packages/gnome-keysign/)

*   **[GnuPG](/index.php/GnuPG "GnuPG")** — The GNU project's complete and free implementation of the OpenPGP standard as defined by RFC4880\. Free and Open Source replacement of PGP, mostly used for digital signing of packages.

	[https://gnupg.org/](https://gnupg.org/) || [gnupg](https://www.archlinux.org/packages/?name=gnupg)

*   **gzsteg** — A utiltiy that can hide data in gzip compressed files

	[http://www.nic.funet.fi/pub/crypt/steganography/](http://www.nic.funet.fi/pub/crypt/steganography/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=gzsteg)</small>

*   **[KGpg](https://en.wikipedia.org/wiki/KGPG "wikipedia:KGPG")** — *a simple interface for GnuPG* for KDE.

	[https://www.kde.org/applications/utilities/kgpg/](https://www.kde.org/applications/utilities/kgpg/) || [kgpg](https://www.archlinux.org/packages/?name=kgpg)

*   **[Seahorse](https://en.wikipedia.org/wiki/Seahorse_(software) "wikipedia:Seahorse (software)")** — GNOME application for managing encryption keys and passwords in the GnomeKeyring.

	[http://library.gnome.org/users/seahorse/stable/](http://library.gnome.org/users/seahorse/stable/) || [seahorse](https://www.archlinux.org/packages/?name=seahorse)

*   **steghide** — A steganography utility that is able to hide data in various kinds of image and audio files.

	[http://steghide.sourceforge.net](http://steghide.sourceforge.net) || [steghide](https://www.archlinux.org/packages/?name=steghide)

#### Password managers

*   **Encryptr** — Zero-knowledge, cloud-based password manager.

	[https://spideroak.com/encryptr/](https://spideroak.com/encryptr/) || [encryptr](https://aur.archlinux.org/packages/encryptr/)

*   **Enpass** — A multiplatform password manager

	[https://www.enpass.io/](https://www.enpass.io/) || [enpass-bin](https://aur.archlinux.org/packages/enpass-bin/)

*   **Figaro's Password Manager 2** — GTK2 port of [Figaro's Password Manager](http://fpm.sourceforge.net/) with some new enhancements.

	[https://als.regnet.cz/fpm2/](https://als.regnet.cz/fpm2/) || [fpm2](https://aur.archlinux.org/packages/fpm2/)

*   **GPass** — Password manegement software for GNOME2 desktop.

	[https://github.com/raffael-sfm/gpass](https://github.com/raffael-sfm/gpass) || [gpass](https://aur.archlinux.org/packages/gpass/)

*   **Ked Password Manager** — A password manager that helps to manage large numbers of passwords.

	[http://kedpm.sourceforge.net](http://kedpm.sourceforge.net) || [kedpm](https://aur.archlinux.org/packages/kedpm/)

*   **[KeePass Password Safe](/index.php/KeePass "KeePass")** — Free open source Mono-based password manager, which helps you to manage your passwords in a secure way.

	[https://keepass.info/](https://keepass.info/) || [keepass](https://www.archlinux.org/packages/?name=keepass)

*   **KeePassC** — KeePassC is a curses-based password manager compatible to KeePass v.1.x and KeePassX.

	[http://raymontag.github.io/keepassc/](http://raymontag.github.io/keepassc/) || [keepassc](https://aur.archlinux.org/packages/keepassc/)

*   **KeePassX** — Free and open source Qt-based password manager. Compatible with KeePass v.1.x and KeePass v.2.x.

	[https://www.keepassx.org/](https://www.keepassx.org/) || [keepassx](https://www.archlinux.org/packages/?name=keepassx) [keepassx2](https://www.archlinux.org/packages/?name=keepassx2)

*   **KeePassXC** — A community fork of KeePassX with more active development.

	[https://keepassxc.org/](https://keepassxc.org/) || [keepassxc](https://www.archlinux.org/packages/?name=keepassxc)

*   **LastPass** — Hosted password manager.

	[https://www.lastpass.com/](https://www.lastpass.com/) || [lastpass-cli](https://www.archlinux.org/packages/?name=lastpass-cli)

*   **MyPasswords** — What you need for managing your passwords, including the passwords of your online accounts, bank accounts and ... with the corresponding URLs.

	[https://sourceforge.net/projects/mypasswords7/](https://sourceforge.net/projects/mypasswords7/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **[pass](/index.php/Pass "Pass")** — Simple console based password manager

	[https://www.passwordstore.org/](https://www.passwordstore.org/) || [pass](https://www.archlinux.org/packages/?name=pass)

*   **Password Gorilla** — A cross-platform password manager.

	[https://github.com/zdia/gorilla/wiki](https://github.com/zdia/gorilla/wiki) || [password-gorilla](https://aur.archlinux.org/packages/password-gorilla/)

*   **Password Safe** — Simple and secure password manager.

	[https://pwsafe.org/](https://pwsafe.org/) || [passwordsafe](https://aur.archlinux.org/packages/passwordsafe/)

*   **pwsafe** — Unix commandline program that manages encrypted password databases.

	[http://nsd.dyndns.org/pwsafe/](http://nsd.dyndns.org/pwsafe/) || [pwsafe](https://www.archlinux.org/packages/?name=pwsafe)

*   **QPass** — Easy to use password manager with built-in password generator.

	[http://qpass.sourceforge.net](http://qpass.sourceforge.net) || [qpass](https://aur.archlinux.org/packages/qpass/)

*   **Revelation** — Password manager for the GNOME desktop.

	[https://revelation.olasagasti.info/](https://revelation.olasagasti.info/) || [revelation](https://aur.archlinux.org/packages/revelation/)

*   **spm** — Simple Password Manager written entirely in POSIX shell using PGP. Fast, lightweight and easily scriptable.

	[https://notabug.org/kl3/spm/](https://notabug.org/kl3/spm/) || [spm](https://aur.archlinux.org/packages/spm/)

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

	[https://www.gnu.org/software/bc/](https://www.gnu.org/software/bc/) || [bc](https://www.archlinux.org/packages/?name=bc)

*   **calc** — Arbitrary precision console calculator.

	[http://www.isthe.com/chongo/tech/comp/calc/](http://www.isthe.com/chongo/tech/comp/calc/) || [calc](https://www.archlinux.org/packages/?name=calc)

*   **Extcalc** — Qt-based scientfic graphical calculator.

	[http://extcalc-linux.sourceforge.net/](http://extcalc-linux.sourceforge.net/) || [extcalc](https://aur.archlinux.org/packages/extcalc/)

*   **galculator** — GTK+ based scientific calculator.

	[http://galculator.mnim.org/](http://galculator.mnim.org/) || GTK+ 3: [galculator](https://www.archlinux.org/packages/?name=galculator), GTK+ 2: [galculator-gtk2](https://www.archlinux.org/packages/?name=galculator-gtk2)

*   **[GNOME Calculator](https://en.wikipedia.org/wiki/GNOME_Calculator "wikipedia:GNOME Calculator")** — Scientific calculator included in the GNOME desktop.

	[https://wiki.gnome.org/Apps/Calculator](https://wiki.gnome.org/Apps/Calculator) || [gnome-calculator](https://www.archlinux.org/packages/?name=gnome-calculator)

*   **KAlgebra** — Calculator and 3D plotter included in KDE EDU.

	[https://www.kde.org/applications/education/kalgebra/](https://www.kde.org/applications/education/kalgebra/) || [kalgebra](https://www.archlinux.org/packages/?name=kalgebra)

*   **[KCalc](https://en.wikipedia.org/wiki/KCalc "wikipedia:KCalc")** — Scientific calculator included in the KDE desktop.

	[https://www.kde.org/applications/utilities/kcalc/](https://www.kde.org/applications/utilities/kcalc/) || [kcalc](https://www.archlinux.org/packages/?name=kcalc)

*   **MATE Calc** — Calculator for the MATE desktop environment.

	[https://mate-desktop.org/](https://mate-desktop.org/) || [mate-calc](https://www.archlinux.org/packages/?name=mate-calc)

*   **Qalculate** — Calculator and equation solver with fault-tolerant parsing, constant recognition and units.

	[http://qalculate.github.io/](http://qalculate.github.io/) || [qalculate-gtk](https://www.archlinux.org/packages/?name=qalculate-gtk)

*   **SpeedCrunch** — Fast, high precision and powerful cross-platform calculator.

	[http://speedcrunch.org](http://speedcrunch.org) || [speedcrunch](https://www.archlinux.org/packages/?name=speedcrunch)

*   **[xcalc](https://en.wikipedia.org/wiki/xcalc "wikipedia:xcalc")** — Scientific calculator for X with algebraic and reverse polish notation modes.

	[https://www.x.org/](https://www.x.org/) || [xorg-xcalc](https://www.archlinux.org/packages/?name=xorg-xcalc)

#### Computer algebra system

See also [Wikipedia:Comparison of computer algebra systems](https://en.wikipedia.org/wiki/Comparison_of_computer_algebra_systems "wikipedia:Comparison of computer algebra systems").

*   **[AXIOM](https://en.wikipedia.org/wiki/Axiom_(computer_algebra_system) "wikipedia:Axiom (computer algebra system)")** — FriCAS: derivative of the powerful AXIOM-CAS

	[http://fricas.sourceforge.net](http://fricas.sourceforge.net) || [fricas](https://aur.archlinux.org/packages/fricas/)

*   **[GAP](https://en.wikipedia.org/wiki/GAP_(computer_algebra_system) "wikipedia:GAP (computer algebra system)")** — Computer algebra system for computational discrete algebra with particular emphasis on computational group theory.

	[http://www.gap-system.org](http://www.gap-system.org) || [gap](https://www.archlinux.org/packages/?name=gap)

*   **[Maple](/index.php/Maple "Maple")** — Famous commercial CAS. Often used in education.

	[https://www.maplesoft.com/products/maple/](https://www.maplesoft.com/products/maple/) ||

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

*   **[FFTW](https://en.wikipedia.org/wiki/FFTW "wikipedia:FFTW")** — A [Fast Fourier Transform](https://en.wikipedia.org/wiki/Fast_Fourier_transform "wikipedia:Fast Fourier transform") library for computing discrete Fourier transforms. Used for a wide variety of numerical applications, which includes spectral methods.

	[https://www.fftw.org/](https://www.fftw.org/) || [fftw](https://www.archlinux.org/packages/?name=fftw) [fftw-mpi](https://aur.archlinux.org/packages/fftw-mpi/) [fftw-mpich](https://aur.archlinux.org/packages/fftw-mpich/)

*   **[FreeMat](https://en.wikipedia.org/wiki/FreeMat "wikipedia:FreeMat")** — Matlab-like program that supports many of its functions and features a codeless interface to external C, C++, and Fortran code, further parallel distributed algorithm development (via MPI), and 3D visualization capabilities.

	[http://freemat.sourceforge.net/](http://freemat.sourceforge.net/) || [freemat](https://www.archlinux.org/packages/?name=freemat)

*   **GeoGebra** — Dynamic mathematics software with interactive graphics, algebra and spreadsheet

	[https://www.geogebra.org/](https://www.geogebra.org/) || [geogebra](https://www.archlinux.org/packages/?name=geogebra)

*   **[GNU Radio](/index.php/GNU_Radio "GNU Radio")** — Software development toolkit that provides signal processing blocks to implement software radios.

	[https://www.gnuradio.org/](https://www.gnuradio.org/) || [gnuradio](https://www.archlinux.org/packages/?name=gnuradio)

*   **[matplotlib (PyLab)](https://en.wikipedia.org/wiki/matplotlib "wikipedia:matplotlib")** — Collection of Python modules (pyplot, numpy, etc.) used for scientific calculations.

	[https://www.scipy.org/](https://www.scipy.org/) || [python-matplotlib](https://www.archlinux.org/packages/?name=python-matplotlib)

*   **[Octave](/index.php/Octave "Octave")** — [Matlab](/index.php/Matlab "Matlab")-like language and interface for numerical computations.

	[https://www.gnu.org/software/octave/](https://www.gnu.org/software/octave/) || [octave](https://www.archlinux.org/packages/?name=octave)

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

	[https://www.gnu.org/software/pspp/](https://www.gnu.org/software/pspp/) || [pspp](https://aur.archlinux.org/packages/pspp/)

*   **[R](/index.php/R "R")** — Software environment for statistical computing and graphics.

	[https://cran.r-project.org/](https://cran.r-project.org/) || [r](https://www.archlinux.org/packages/?name=r)

*   **[RKWard](https://en.wikipedia.org/wiki/RKWard "wikipedia:RKWard")** — Frontend for the statistical language R.

	[https://rkward.kde.org/](https://rkward.kde.org/) || [rkward](https://aur.archlinux.org/packages/rkward/)

*   **[RStudio](https://en.wikipedia.org/wiki/RStudio "wikipedia:RStudio")** — A powerful and productive IDE for R written in Qt.

	[https://www.rstudio.com/](https://www.rstudio.com/) || [rstudio-desktop-bin](https://aur.archlinux.org/packages/rstudio-desktop-bin/)

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

	[https://root.cern.ch/](https://root.cern.ch/) || [root](https://aur.archlinux.org/packages/root/)

*   **[SciDAVis](https://en.wikipedia.org/wiki/SciDAVis "wikipedia:SciDAVis")** — Fork of QtiPlot with the goal of being better documented and more user friendly.

	[http://scidavis.sourceforge.net/](http://scidavis.sourceforge.net/) || [scidavis](https://aur.archlinux.org/packages/scidavis/)

See also [List of applications/Documents#Spreadsheets](/index.php/List_of_applications/Documents#Spreadsheets "List of applications/Documents")

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

	[http://ugene.net/](http://ugene.net/) || [ugene](https://aur.archlinux.org/packages/ugene/)

#### Molecules

##### Viewers

See also [Wikipedia:List of molecular graphics systems](https://en.wikipedia.org/wiki/List_of_molecular_graphics_systems "wikipedia:List of molecular graphics systems").

*   **[Avogadro](https://en.wikipedia.org/wiki/Avogadro_(software) "wikipedia:Avogadro (software)")** — Editor, viewer and simulator for 3D molecule structures (also supports downloading files from the [Protein Data Bank](https://en.wikipedia.org/wiki/Protein_Data_Bank "wikipedia:Protein Data Bank")).

	[http://avogadro.cc/](http://avogadro.cc/) || [avogadro](https://aur.archlinux.org/packages/avogadro/)

*   **BALLView** — Standalone molecular modeling and visualization application, part of the [BALL](https://en.wikipedia.org/wiki/BALL "wikipedia:BALL") framework.

	[http://www.ball-project.org/](http://www.ball-project.org/) || [ball](https://aur.archlinux.org/packages/ball/)

*   **[Ghemical](https://en.wikipedia.org/wiki/Ghemical "wikipedia:Ghemical")** — Computational chemistry software package used to edit, view and simulate molecular structures.

	[http://bioinformatics.org/ghemical/ghemical/index.html](http://bioinformatics.org/ghemical/ghemical/index.html) || [ghemical](https://aur.archlinux.org/packages/ghemical/)

*   **[PyMOL](https://en.wikipedia.org/wiki/PyMOL "wikipedia:PyMOL")** — Open-source molecular visualization system that can produce high quality 3D images of small molecules and biological macromolecules, such as proteins.

	[https://pymol.org/](https://pymol.org/) || [pymol](https://www.archlinux.org/packages/?name=pymol)

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

	[http://freecode.com/projects/gelemental](http://freecode.com/projects/gelemental) || [gelemental](https://aur.archlinux.org/packages/gelemental/)

*   **[Kalzium](https://en.wikipedia.org/wiki/Kalzium "wikipedia:Kalzium")** — Periodic table of the elements with molecule editor and equation solver from the [KDE](/index.php/KDE "KDE") desktop.

	[https://edu.kde.org/kalzium/](https://edu.kde.org/kalzium/) || [kalzium](https://www.archlinux.org/packages/?name=kalzium)

#### Biochemistry

*   **[Bioclipse](https://en.wikipedia.org/wiki/Bioclipse "wikipedia:Bioclipse")** — Java-based visual platform for biochemistry that uses the Eclipse Rich Client Platform (RCP).

	[http://www.bioclipse.net/](http://www.bioclipse.net/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=bioclipse)</small>

#### Image manipulation

*   **[ImageJ](https://en.wikipedia.org/wiki/ImageJ "wikipedia:ImageJ")** — Java-based image processing and analysing program that provides extensibility via plugins and macros. It is widely used in microscopy (e.g. for cell counting).

	[https://imagej.nih.gov/ij/](https://imagej.nih.gov/ij/) || [imagej](https://aur.archlinux.org/packages/imagej/)

*   **[Fiji](https://en.wikipedia.org/wiki/FIJI_(software) "wikipedia:FIJI (software)")** — ImageJ distribution (and soon ImageJ2) with a lot of plugins organized into a coherent menu structure.

	[http://fiji.sc](http://fiji.sc) || [fiji-binary](https://aur.archlinux.org/packages/fiji-binary/)

### Astronomy

*   **[Celestia](https://en.wikipedia.org/wiki/Celestia "wikipedia:Celestia")** — 3D astronomy simulation program that allows users to travel through an extensive universe, modeled after reality, at any speed, in any direction and at any time in history.

	[https://celestiaproject.net/](https://celestiaproject.net/) || [celestia](https://www.archlinux.org/packages/?name=celestia)

*   **GIMP Astronomy Plugins** — Set of GIMP plugins for astronomical image processing.

	[http://hennigbuam.de/georg/gimp.html](http://hennigbuam.de/georg/gimp.html) || [gimp-plugin-astronomy](https://aur.archlinux.org/packages/gimp-plugin-astronomy/)

*   **GoQat** — Camera acquisition software, especially for QSI cameras, that provides other features such as autoguiding, focusing help and others.

	[http://canburytech.net/GoQat/](http://canburytech.net/GoQat/) || [goqat](https://aur.archlinux.org/packages/goqat/)

*   **[KStars](https://en.wikipedia.org/wiki/KStars "wikipedia:KStars")** — Planetarium application that provides an accurate graphical simulation of the night sky, from any location on Earth, at any date and time. It is included in KDE Edu.

	[https://edu.kde.org/kstars/](https://edu.kde.org/kstars/) || [kstars](https://www.archlinux.org/packages/?name=kstars)

*   **Qastrocam-g2** — Webcam acquisition software for planetary imaging.

	[https://sourceforge.net/projects/qastrocam-g2/](https://sourceforge.net/projects/qastrocam-g2/) || [qastrocam-g2](https://aur.archlinux.org/packages/qastrocam-g2/)

*   **[Skychart / Cartes du Ciel](https://en.wikipedia.org/wiki/Cartes_du_Ciel "wikipedia:Cartes du Ciel")** — Planetarium that maps out and labels most of the constellations, planets, and objects you can see with a telescope. It can also download Digitized Sky Survey Charts and superimpose images over these charts.

	[https://www.ap-i.net/skychart/](https://www.ap-i.net/skychart/) || [skychart](https://aur.archlinux.org/packages/skychart/)

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

	[https://sourceforge.net/projects/circuit/](https://sourceforge.net/projects/circuit/) || [logisim](https://aur.archlinux.org/packages/logisim/)

*   **Logisim Evolution** — Project which continue the development of the original Logisim with new features, written in Java.

	[https://github.com/reds-heig/logisim-evolution](https://github.com/reds-heig/logisim-evolution) || [logisim-evolution-git](https://aur.archlinux.org/packages/logisim-evolution-git/)

*   **SmartSim** — Simple and beautiful digital logic circuit design and simulation software, mainly target teachers and students, very lightweight and cross platform, GPL licensed, written in Vala.

	[http://smartsim.org.uk](http://smartsim.org.uk) || [smartsim-git](https://aur.archlinux.org/packages/smartsim-git/)

##### HDL

*   **[Altera Design Software](/index.php/Altera_Design_Software "Altera Design Software")** — A set of design tools for Altera's FPGA chips that includes Quartus II and ModelSim-Altera.

	[https://www.altera.com/products/design-software/overview.html](https://www.altera.com/products/design-software/overview.html) || see [Altera Design Software](/index.php/Altera_Design_Software "Altera Design Software")

*   **[Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK")** — FPGA programmable logic design suit.

	[http://www.xilinx.com/products/design-tools/ise-design-suite/ise-webpack.html](http://www.xilinx.com/products/design-tools/ise-design-suite/ise-webpack.html) || see [Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK")

##### MCU IDE

*   **[Arduino](/index.php/Arduino "Arduino")** — Arduino prototyping platform SDK.

	[https://www.arduino.cc/en/Main/Software](https://www.arduino.cc/en/Main/Software) || [arduino](https://www.archlinux.org/packages/?name=arduino)

##### Schematic capture editor

*   **[gEDA](/index.php/GEDA "GEDA")** — Full suite and toolkit of Electronic Design Automation tools that are used for electrical circuit design, schematic capture, simulation, prototyping, and production.

	[http://www.geda-project.org/](http://www.geda-project.org/) || [geda-gaf](https://www.archlinux.org/packages/?name=geda-gaf)

*   **[KiCAD](https://en.wikipedia.org/wiki/KiCAD "wikipedia:KiCAD")** — Software suite for electronic design automation (EDA) that facilitates the design of schematics for electronic circuits and their conversion to PCB (printed circuit board).

	[http://kicad-pcb.org/](http://kicad-pcb.org/) || [kicad](https://www.archlinux.org/packages/?name=kicad)

*   **[Oregano](https://en.wikipedia.org/wiki/Oregano_(software) "wikipedia:Oregano (software)")** — Graphical software application for schematic capture and simulation of electrical circuits. The actual simulation is done by the [ngspice](https://en.wikipedia.org/wiki/Ngspice "wikipedia:Ngspice") or [Gnucap](https://en.wikipedia.org/wiki/GNU_Circuit_Analysis_Package "wikipedia:GNU Circuit Analysis Package") engines.

	[https://github.com/drahnr/oregano](https://github.com/drahnr/oregano) || [oregano](https://aur.archlinux.org/packages/oregano/)

*   **QElectroTech** — Application used to draw advanced electrical circuits.

	[https://qelectrotech.org/](https://qelectrotech.org/) || [qelectrotech](https://aur.archlinux.org/packages/qelectrotech/)

*   **[Qucs](https://en.wikipedia.org/wiki/Quite_Universal_Circuit_Simulator "wikipedia:Quite Universal Circuit Simulator")** — Electronics circuit simulator application that gives you the ability to set up a circuit with a graphical user interface and simulate its large-signal, small-signal and noise behaviour.

	[http://qucs.sourceforge.net/](http://qucs.sourceforge.net/) || [qucs](https://www.archlinux.org/packages/?name=qucs)

#### Physics simulation

*   **[Code_Aster](https://en.wikipedia.org/wiki/Code_Aster "wikipedia:Code Aster")** — Software package for Civil and Structural Engineering finite element analysis and numeric simulation in structural mechanics.

	[https://www.code-aster.org/V2/spip.php?rubrique2](https://www.code-aster.org/V2/spip.php?rubrique2) || [aster](https://aur.archlinux.org/packages/aster/)

*   **[EPANET](https://en.wikipedia.org/wiki/EPANET "wikipedia:EPANET")** — EPANET performs extended period simulation of the water movement and quality behavior within pressurized pipe networks.

	[https://www.epa.gov/](https://www.epa.gov/) || [epanet2-git](https://aur.archlinux.org/packages/epanet2-git/)

*   **[Step](https://en.wikipedia.org/wiki/Step_(software) "wikipedia:Step (software)")** — Two-dimensional physics simulation engine that is included in the KDE desktop as part of KDE Edu.

	[https://edu.kde.org/step/](https://edu.kde.org/step/) || [step](https://www.archlinux.org/packages/?name=step)

*   **[SWMM](https://en.wikipedia.org/wiki/SWMM "wikipedia:SWMM")** — Storm Water Management Model is a dynamic rainfall-runoff-subsurface runoff simulation model used for simulation of the surface/subsurface hydrology quantity and quality.

	[https://www.epa.gov/](https://www.epa.gov/) || [swmm5-git](https://aur.archlinux.org/packages/swmm5-git/)

#### Unit conversion

*   **ConvertAll** — Unit conversion application that allows one to combine units in any way (e.g. inches per decade), even if it does not make sense.

	[http://convertall.bellz.org/](http://convertall.bellz.org/) || [convertall](https://aur.archlinux.org/packages/convertall/)

*   **Gonvert** — Conversion utility that allows conversion between many units like CGS, Ancient, Imperial with many categories like length, mass, numbers, etc.

	[http://www.unihedron.com/projects/gonvert/](http://www.unihedron.com/projects/gonvert/) || [gonvert](https://aur.archlinux.org/packages/gonvert/)

*   **[Units](https://en.wikipedia.org/wiki/GNU_Units "wikipedia:GNU Units")** — Command-line unit converter and calculator that can handle multiplicative scale changes, nonlinear conversions such as Fahrenheit to Celsius or wire gauge and others.

	[https://www.gnu.org/software/units/](https://www.gnu.org/software/units/) || [units](https://www.archlinux.org/packages/?name=units)

### Geography

*   **BT747** — The swiss army knife for MTK GPS dataloggers.

	[https://sourceforge.net/projects/bt747/](https://sourceforge.net/projects/bt747/) || [bt747](https://www.archlinux.org/packages/?name=bt747)

*   **FoxtrotGPS** — Lightweight and fast mapping application.

	[https://www.foxtrotgps.org/](https://www.foxtrotgps.org/) || [foxtrotgps](https://www.archlinux.org/packages/?name=foxtrotgps)

*   **Geotag** — Match date/time information from photos with location information from a GPS unit or from a map.

	[http://geotag.sourceforge.net/](http://geotag.sourceforge.net/) || [geotag](https://www.archlinux.org/packages/?name=geotag)

*   **GNOME Maps** — A simple map client for GNOME. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

	[https://wiki.gnome.org/Apps/Maps](https://wiki.gnome.org/Apps/Maps) || [gnome-maps](https://www.archlinux.org/packages/?name=gnome-maps)

*   **GottenGeography** — Easy to use photo geotagging application for the GNOME desktop.

	[https://launchpad.net/gottengeography](https://launchpad.net/gottengeography) || [gottengeography](https://www.archlinux.org/packages/?name=gottengeography)

*   **GPSBabel** — Reads, writes, and manipulates GPS waypoints in a variety of formats.

	[https://www.gpsbabel.org/](https://www.gpsbabel.org/) || [gpsbabel](https://www.archlinux.org/packages/?name=gpsbabel)

*   **GPSCorrelate** — Correlate (geotagging) digital camera photos with GPS data in GPX format.

	[https://github.com/freefoote/gpscorrelate](https://github.com/freefoote/gpscorrelate) || [gpscorrelate](https://www.archlinux.org/packages/?name=gpscorrelate)

*   **GpsPrune** — View, edit and convert coordinate data from GPS systems.

	[https://activityworkshop.net/software/gpsprune/](https://activityworkshop.net/software/gpsprune/) || [gpsprune](https://www.archlinux.org/packages/?name=gpsprune)

*   **GPX Viewer** — Simple tool to visualize tracks and waypoints stored in a gpx file.

	[https://blog.sarine.nl/tag/gpxviewer/](https://blog.sarine.nl/tag/gpxviewer/) || [gpx-viewer](https://www.archlinux.org/packages/?name=gpx-viewer)

*   **[GRASS GIS](https://en.wikipedia.org/wiki/GRASS_GIS "wikipedia:GRASS GIS")** — Geospatial data management and analysis, image processing, graphics/maps production, spatial modeling and visualization.

	[https://grass.osgeo.org/](https://grass.osgeo.org/) || [grass](https://aur.archlinux.org/packages/grass/)

*   **JOSM** — An editor for OpenStreetMap written in Java.

	[http://josm.openstreetmap.de/](http://josm.openstreetmap.de/) || [josm](https://www.archlinux.org/packages/?name=josm)

*   **[Marble](https://en.wikipedia.org/wiki/Marble_(software) "wikipedia:Marble (software)")** — Virtual Globe and World Atlas that can be used to learn more about the Earth. Part of [kdeedu](https://www.archlinux.org/groups/x86_64/kdeedu/).

	[https://marble.kde.org/](https://marble.kde.org/) || KDE: [marble](https://www.archlinux.org/packages/?name=marble), Qt: [marble-qt](https://www.archlinux.org/packages/?name=marble-qt)

*   **Merkaartor** — OpenStreetMap editor.

	[http://merkaartor.be/](http://merkaartor.be/) || [merkaartor](https://www.archlinux.org/packages/?name=merkaartor)

*   **Navit** — Modular turn-by-turn car navigation system.

	[http://www.navit-project.org/](http://www.navit-project.org/) || [navit](https://www.archlinux.org/packages/?name=navit)

*   **QLandkarte GT** — Use your GPS with Linux.

	[http://qlandkarte.org/](http://qlandkarte.org/) || [qlandkartegt](https://www.archlinux.org/packages/?name=qlandkartegt)

*   **QMapShack** — Plan your next outdoor trip.

	[https://bitbucket.org/maproom/qmapshack](https://bitbucket.org/maproom/qmapshack) || [qmapshack](https://www.archlinux.org/packages/?name=qmapshack)

*   **QGIS** — Geographic Information System (GIS) that supports vector, raster & database formats.

	[https://qgis.org/](https://qgis.org/) || [qgis](https://aur.archlinux.org/packages/qgis/)

*   **Viking** — GTK+2 application to manage GPS data.

	[https://sourceforge.net/projects/viking/](https://sourceforge.net/projects/viking/) || [viking](https://www.archlinux.org/packages/?name=viking)

## Others

### Finance

See also [Wikipedia:Comparison of accounting software](https://en.wikipedia.org/wiki/Comparison_of_accounting_software "wikipedia:Comparison of accounting software").

*   **Beancount** — A double-entry bookkeeping computer language that lets you define financial transaction records in a text file, read them in memory, generate a variety of reports from them, and provides a web interface.

	[http://furius.ca/beancount/](http://furius.ca/beancount/) || [beancount-hg](https://aur.archlinux.org/packages/beancount-hg/)

*   **esniper** — Simple, lightweight tool for [sniping](https://en.wikipedia.org/wiki/Auction_sniping "wikipedia:Auction sniping") eBay auctions.

	[http://esniper.sourceforge.net/](http://esniper.sourceforge.net/) || [esniper](https://aur.archlinux.org/packages/esniper/)

*   **[GnuCash](https://en.wikipedia.org/wiki/GnuCash "wikipedia:GnuCash")** — Financial application that implements a double-entry book-keeping system with features for small business accounting.

	[http://www.gnucash.org/](http://www.gnucash.org/) || [gnucash](https://aur.archlinux.org/packages/gnucash/)

*   **Grisbi** — Personal finance system which manages third party, expenditure and receipt categories, as well as budgetary lines, financial years, and other information that makes it suitable for associations.

	[http://www.grisbi.org/](http://www.grisbi.org/) || [grisbi](https://aur.archlinux.org/packages/grisbi/)

*   **[HomeBank](https://en.wikipedia.org/wiki/HomeBank "wikipedia:HomeBank")** — Easy to use finance manager that can analyse your personal finance in detail using powerful filtering tools and graphs.

	[http://homebank.free.fr/](http://homebank.free.fr/) || [homebank](https://www.archlinux.org/packages/?name=homebank)

*   **[KMyMoney](https://en.wikipedia.org/wiki/KMyMoney "wikipedia:KMyMoney")** — Personal finance manager that operates in a similar way to [Microsoft Money](https://en.wikipedia.org/wiki/Microsoft_Money "wikipedia:Microsoft Money"). It supports different account types, categorisation of expenses and incomes, reconciliation of bank accounts and import/export to the “QIF” file format.

	[http://kmymoney2.sourceforge.net/index-home.html](http://kmymoney2.sourceforge.net/index-home.html) || [kmymoney](https://www.archlinux.org/packages/?name=kmymoney)

*   **[Ledger](/index.php/Ledger "Ledger")** — Ledger is a powerful, double-entry accounting system that is accessed from the UNIX command-line.

	[http://ledger-cli.org/](http://ledger-cli.org/) || [ledger](https://aur.archlinux.org/packages/ledger/)

*   **hledger** — An accounting program for tracking money, time, or any other commodity, using double-entry accounting and a simple, editable file format. hledger is inspired by and largely compatible with ledger.

	[http://hledger.org/](http://hledger.org/) || [hledger-git](https://aur.archlinux.org/packages/hledger-git/)

*   **Manager Accounting** — Manager is free accounting software for small business.

	[http://www.manager.io/](http://www.manager.io/) || [manager-accounting](https://aur.archlinux.org/packages/manager-accounting/)

*   **Money Manager EX** — An easy-to-use personal finance suite

	[http://www.moneymanagerex.org/](http://www.moneymanagerex.org/) || [moneymanagerex](https://www.archlinux.org/packages/?name=moneymanagerex)

*   **Skrooge** — Personal finances manager for the KDE desktop.

	[http://skrooge.org/](http://skrooge.org/) || [skrooge](https://www.archlinux.org/packages/?name=skrooge)

*   **openerp** — Open source erp system purely in python.

	[http://openerp.com/](http://openerp.com/) || [openerp](https://aur.archlinux.org/packages/openerp/)

### Education

#### Flashcards

See also [Wikipedia:List_of_flashcard_software](https://en.wikipedia.org/wiki/List_of_flashcard_software "wikipedia:List of flashcard software").

*   **[Anki](/index.php/Anki "Anki")** — Anki is a program which makes remembering things easy.

	[http://ankisrs.net/](http://ankisrs.net/) || [anki12](https://aur.archlinux.org/packages/anki12/) [anki20-bin](https://aur.archlinux.org/packages/anki20-bin/)

*   **iGNUit** — Memorization aid based on the Leitner flashcard system.

	[http://homepages.ihug.co.nz/~trmusson/programs.html#ignuit](http://homepages.ihug.co.nz/~trmusson/programs.html#ignuit) || [ignuit](https://aur.archlinux.org/packages/ignuit/)

*   **[Mnemosyne](/index.php/Mnemosyne "Mnemosyne")** — Free flash-card tool which optimizes your learning process.

	[http://mnemosyne-proj.org/](http://mnemosyne-proj.org/) || [mnemosyne](https://aur.archlinux.org/packages/mnemosyne/)

#### Education management engines

*   **[Moodle](/index.php/Moodle "Moodle")** — Moodle is a open-source software learning management system.

	[https://moodle.org/](https://moodle.org/) || [moodle](https://aur.archlinux.org/packages/moodle/)

#### Touch typing

*   **[KTouch](/index.php?title=KTouch&action=edit&redlink=1 "KTouch (page does not exist)")** — Touch Typing Tutor. It's a part of Plasma workspace.

	[https://www.kde.org/applications/education/ktouch](https://www.kde.org/applications/education/ktouch) || [ktouch](https://www.archlinux.org/packages/?name=ktouch), [kdeedu-ktouch-patched](https://aur.archlinux.org/packages/kdeedu-ktouch-patched/)

*   **[GNU Typist](/index.php?title=GNU_Typist&action=edit&redlink=1 "GNU Typist (page does not exist)")** — GNU Typist (also called gtypist) is a universal typing tutor.

	[https://www.gnu.org/software/gtypist/](https://www.gnu.org/software/gtypist/) || [gtypist](https://www.archlinux.org/packages/?name=gtypist), [gtypist-single-space](https://aur.archlinux.org/packages/gtypist-single-space/)

*   **[Klavaro](/index.php?title=Klavaro&action=edit&redlink=1 "Klavaro (page does not exist)")** — Klavaro is libre software for teaching touch typing that intends to be keyboard and language independent.

	[http://klavaro.sourceforge.net/](http://klavaro.sourceforge.net/) || [klavaro](https://www.archlinux.org/packages/?name=klavaro)

*   **[tipp10](/index.php?title=Tipp10&action=edit&redlink=1 "Tipp10 (page does not exist)")** — Intelligent typing tutor.

	[http://www.tipp10.com/](http://www.tipp10.com/) || [tipp10](https://www.archlinux.org/packages/?name=tipp10)

*   **[typespeed](/index.php?title=Typespeed&action=edit&redlink=1 "Typespeed (page does not exist)")** — Test your typing speed, and get your fingers' CPS.

	[http://typespeed.sourceforge.net](http://typespeed.sourceforge.net) || [typespeed](https://www.archlinux.org/packages/?name=typespeed)

*   **[amphetype-svn](/index.php?title=Amphetype-svn&action=edit&redlink=1 "Amphetype-svn (page does not exist)")** — A layout-agnostic typing program aimed at people who don't need an on-screen keyboard.

	[http://code.google.com/p/amphetype/](http://code.google.com/p/amphetype/) || [amphetype-svn](https://aur.archlinux.org/packages/amphetype-svn/)

*   **[dvorak7min](/index.php?title=Dvorak7min&action=edit&redlink=1 "Dvorak7min (page does not exist)")** — dvorak7min is a simple ncurses-based typing tutor for those trying to become fluent with the Dvorak keyboard layout.

	[http://packages.debian.org/unstable/games/dvorak7min](http://packages.debian.org/unstable/games/dvorak7min) || [dvorak7min](https://aur.archlinux.org/packages/dvorak7min/)

*   **[dvorakng](/index.php?title=Dvorakng&action=edit&redlink=1 "Dvorakng (page does not exist)")** — A Dvorak typing tutor. It's heavily based on Dvorak7min, but adds many improvements.

	[https://gitlab.com/atsb/dvorakng](https://gitlab.com/atsb/dvorakng) || [dvorakng](https://aur.archlinux.org/packages/dvorakng/)

*   **[psani-profi](/index.php?title=Psani-profi&action=edit&redlink=1 "Psani-profi (page does not exist)")** — Program that will teach you touchtyping (czech).

	[http://www.sallyx.org/sally/psani-vsemi-deseti/](http://www.sallyx.org/sally/psani-vsemi-deseti/) || [psani-profi](https://aur.archlinux.org/packages/psani-profi/)

*   **[touchtyper](/index.php?title=Touchtyper&action=edit&redlink=1 "Touchtyper (page does not exist)")** — typing trainer - an application suite for training and exercising touchtyping.

	[http://typingtrainer.sourceforge.net/](http://typingtrainer.sourceforge.net/) || [touchtyper](https://aur.archlinux.org/packages/touchtyper/)

*   **[tpgt](/index.php?title=Tpgt&action=edit&redlink=1 "Tpgt (page does not exist)")** — A ncurses-based typing trainer program.

	[http://szit.hu/tpgt/](http://szit.hu/tpgt/) || [tpgt](https://aur.archlinux.org/packages/tpgt/)

*   **[tuxtype](/index.php?title=Tuxtype&action=edit&redlink=1 "Tuxtype (page does not exist)")** — An educational typing tutorial game starring Tux.

	[http://tux4kids.alioth.debian.org/](http://tux4kids.alioth.debian.org/) || [tuxtype](https://aur.archlinux.org/packages/tuxtype/)

*   **[typingtest-git](/index.php?title=Typingtest-git&action=edit&redlink=1 "Typingtest-git (page does not exist)")** — A typing test program desktop program with customizability.

	[https://github.com/laelath/typingtest](https://github.com/laelath/typingtest) || [typingtest-git](https://aur.archlinux.org/packages/typingtest-git/)

### Time management

#### Console

*   **Calcurse** — Text-based ncurses calendar and scheduling system (supports CalDAV)

	[http://calcurse.org/](http://calcurse.org/) || [calcurse](https://www.archlinux.org/packages/?name=calcurse)

*   **khal** — Command-line (non-interactive) and ncurses (interactive) calendar system (supports CalDAV)

	[https://github.com/pimutils/khal](https://github.com/pimutils/khal) || [khal](https://aur.archlinux.org/packages/khal/)

*   **todoman** — Command-line To-do list manager (supports CalDAV)

	[https://github.com/pimutils/todoman](https://github.com/pimutils/todoman) || [todoman](https://aur.archlinux.org/packages/todoman/)

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

	[http://pessimization.com/software/wyrd/](http://pessimization.com/software/wyrd/) || [wyrd](https://aur.archlinux.org/packages/wyrd/)

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

*   **GNOME Break Timer** — Keeps track of how much you are using the computer, and it reminds you to take regular breaks.

	[https://wiki.gnome.org/Apps/GnomeBreakTimer](https://wiki.gnome.org/Apps/GnomeBreakTimer) || [gnome-break-timer](https://www.archlinux.org/packages/?name=gnome-break-timer)

*   **Hamster** — Time tracking application that helps you to keep track on how much time you have spent during the day on activities you choose to track.

	[http://projecthamster.org/](http://projecthamster.org/) || [hamster-time-tracker](https://www.archlinux.org/packages/?name=hamster-time-tracker)

*   **[KOrganizer](https://en.wikipedia.org/wiki/Kontact#Organizer "wikipedia:Kontact")** — Calendar and scheduling program, part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

	[https://www.kde.org/applications/office/korganizer/](https://www.kde.org/applications/office/korganizer/) || [korganizer](https://www.archlinux.org/packages/?name=korganizer)

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

### Recipe management

*   **GNOME Recipes** — Recipe management application for GNOME.

	[https://wiki.gnome.org/Apps/Recipes](https://wiki.gnome.org/Apps/Recipes) || [gnome-recipes](https://www.archlinux.org/packages/?name=gnome-recipes)

*   **Gourmet** — A simple but powerful recipe-managing application.

	[http://thinkle.github.io/gourmet/](http://thinkle.github.io/gourmet/) || [gourmet](https://www.archlinux.org/packages/?name=gourmet)

*   **KRecipes** — A tool designed to make organizing your personal recipes collection fast and easy.

	[https://www.kde.org/applications/utilities/krecipes/](https://www.kde.org/applications/utilities/krecipes/) || [krecipes](https://www.archlinux.org/packages/?name=krecipes)

### Accessibility

See [Accessibility](/index.php/Accessibility "Accessibility") for tips on operating the desktop and [Category:Accessibility](/index.php/Category:Accessibility "Category:Accessibility") for all available articles.

#### Screen reading

See [Speech recognition#List of text to speech applications](/index.php/Speech_recognition#List_of_text_to_speech_applications "Speech recognition").

#### Speech recognition

See [Speech recognition#List of speech recognition applications](/index.php/Speech_recognition#List_of_speech_recognition_applications "Speech recognition").

### Amateur radio

See the main article: [Amateur radio#Software list](/index.php/Amateur_radio#Software_list "Amateur radio").

See also [Wikipedia:List of software-defined radios](https://en.wikipedia.org/wiki/List_of_software-defined_radios "wikipedia:List of software-defined radios").

### Display calibration

See the main article: [ICC profiles](/index.php/ICC_profiles "ICC profiles").

### Display managers

See the main article: [Display manager#List of display managers](/index.php/Display_manager#List_of_display_managers "Display manager").

### Command shells

See the main article: [Command-line shell](/index.php/Command-line_shell "Command-line shell").

See also [Wikipedia:Comparison of command shells](https://en.wikipedia.org/wiki/Comparison_of_command_shells "wikipedia:Comparison of command shells").

### Terminal multiplexers

*   **abduco** — Tool for session attach and detach support which allows a process to run independently from its controlling terminal.

	[http://www.brain-dump.org/projects/abduco/](http://www.brain-dump.org/projects/abduco/) || [abduco](https://www.archlinux.org/packages/?name=abduco)

*   **[dtach](/index.php/Dtach "Dtach")** — Program that emulates the detach feature of [screen](/index.php/Screen "Screen").

	[http://dtach.sourceforge.net/](http://dtach.sourceforge.net/) || [dtach](https://www.archlinux.org/packages/?name=dtach)

*   **[GNU Screen](/index.php/GNU_Screen "GNU Screen")** — Full-screen window manager that multiplexes a physical terminal.

	[https://www.gnu.org/software/screen/](https://www.gnu.org/software/screen/) || [screen](https://www.archlinux.org/packages/?name=screen)

*   **[tmux](/index.php/Tmux "Tmux")** — BSD licensed terminal multiplexer.

	[http://tmux.github.io/](http://tmux.github.io/) || [tmux](https://www.archlinux.org/packages/?name=tmux)

*   **[byobu](https://en.wikipedia.org/wiki/Byobu_(software) "wikipedia:Byobu (software)")** — An GPLv3 licensed addon for tmux or screen. It requires a terminal multiplexer installed.

	[http://byobu.co/](http://byobu.co/) || [byobu](https://aur.archlinux.org/packages/byobu/)

### Desktop environments

See the main article: [Desktop environment#List of desktop environments](/index.php/Desktop_environment#List_of_desktop_environments "Desktop environment").

#### Window managers

##### Console

See also [#Terminal multiplexers](#Terminal_multiplexers), which offer some of the functions of window managers for the console.

*   **dvtm** — [dwm](/index.php/Dwm "Dwm")-style window manager in the console.

	[http://brain-dump.org/projects/dvtm/](http://brain-dump.org/projects/dvtm/) || [dvtm](https://www.archlinux.org/packages/?name=dvtm)

*   **twin** — Text-mode window manager.

	[https://sourceforge.net/projects/twin/](https://sourceforge.net/projects/twin/) || [twin](https://www.archlinux.org/packages/?name=twin)

*   **Wmutils** — A set of tools for X windows manipulation.

	[https://github.com/wmutils/core](https://github.com/wmutils/core) || [wmutils-git](https://aur.archlinux.org/packages/wmutils-git/)

##### Graphical

See the main article: [Window manager#List of window managers](/index.php/Window_manager#List_of_window_managers "Window manager").

##### Composite managers

See the main article: [Xorg#List of composite managers](/index.php/Xorg#List_of_composite_managers "Xorg").

#### Window tilers

*   **PyWO** — Allows you to easily organize windows on the desktop using keyboard shortcuts.

	[https://code.google.com/archive/p/pywo/](https://code.google.com/archive/p/pywo/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/)</small>

*   **QuickTile** — Lightweight standalone alternative to Compiz Grid plugin.

	[http://ssokolow.com/quicktile/](http://ssokolow.com/quicktile/) || [quicktile-git](https://aur.archlinux.org/packages/quicktile-git/)

*   **wumwum** — The Window Manager manager. It can turn emwh compliant window managers into a tiling window manager while retaining all initial functionalities.

	[http://wumwum.sourceforge.net/](http://wumwum.sourceforge.net/) || [wumwum](https://aur.archlinux.org/packages/wumwum/)

#### Taskbars

See also [Wikipedia:Taskbar](https://en.wikipedia.org/wiki/Taskbar "wikipedia:Taskbar").

*   **[Avant Window Navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")** — Lightweight dock which sits at the bottom of the screen.

	[http://launchpad.net/awn](http://launchpad.net/awn) || [avant-window-navigator](https://aur.archlinux.org/packages/avant-window-navigator/)

*   **[Bmpanel](/index.php/Bmpanel "Bmpanel")** — Lightweight, NETWM compliant panel.

	[https://github.com/nsf/bmpanel2](https://github.com/nsf/bmpanel2) || [bmpanel2](https://aur.archlinux.org/packages/bmpanel2/)

*   **[Cairo-Dock](/index.php/Cairo-Dock "Cairo-Dock")** — Highly customizable dock and launcher application.

	[http://www.glx-dock.org/](http://www.glx-dock.org/) || [cairo-dock](https://www.archlinux.org/packages/?name=cairo-dock)

*   **Docker** — Docking application which acts as a system tray.

	[http://icculus.org/openbox/2/docker/](http://icculus.org/openbox/2/docker/) || [docker-tray](https://aur.archlinux.org/packages/docker-tray/)

*   **[Docky](https://en.wikipedia.org/wiki/Docky "wikipedia:Docky")** — Full fledged dock application that makes opening common applications and managing windows easier and quicker.

	[http://wiki.go-docky.com/](http://wiki.go-docky.com/) || [docky](https://www.archlinux.org/packages/?name=docky)

*   **[fbpanel](/index.php/Fbpanel "Fbpanel")** — Lightweight, NETWM compliant desktop panel.

	[https://aanatoly.github.io/fbpanel/](https://aanatoly.github.io/fbpanel/) || [fbpanel](https://www.archlinux.org/packages/?name=fbpanel)

*   **[GNOME Panel](https://en.wikipedia.org/wiki/GNOME_Panel "wikipedia:GNOME Panel")** — Panel included in the [GNOME Flashback](/index.php/GNOME_Flashback "GNOME Flashback") desktop.

	[https://wiki.gnome.org/Projects/GnomePanel](https://wiki.gnome.org/Projects/GnomePanel) || [gnome-panel](https://www.archlinux.org/packages/?name=gnome-panel)

*   **LXPanel** — Lightweight X11 desktop panel and part of the LXDE desktop.

	[http://lxde.org/lxpanel](http://lxde.org/lxpanel) || [lxpanel](https://www.archlinux.org/packages/?name=lxpanel)

*   **MATE Panel** — Panel included in the [MATE](/index.php/MATE "MATE") desktop.

	[https://github.com/mate-desktop/mate-panel/](https://github.com/mate-desktop/mate-panel/) || [mate-panel](https://www.archlinux.org/packages/?name=mate-panel)

*   **PerlPanel** — The ideal accompaniment to a light-weight Window Manager such as OpenBox, or a desktop-drawing program like iDesk.

	[http://savannah.nongnu.org/projects/perlpanel](http://savannah.nongnu.org/projects/perlpanel) || [perlpanel-git](https://aur.archlinux.org/packages/perlpanel-git/)

*   **[Plank](/index.php/Plank "Plank")** — Elegant, simple, clean dock from [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

	[https://launchpad.net/plank](https://launchpad.net/plank) || [plank](https://www.archlinux.org/packages/?name=plank)

*   **[PyPanel](/index.php/PyPanel "PyPanel")** — Lightweight panel/taskbar written in Python and C.

	[http://pypanel.sourceforge.net/](http://pypanel.sourceforge.net/) || [pypanel](https://www.archlinux.org/packages/?name=pypanel)

*   **[Stalonetray](/index.php/Stalonetray "Stalonetray")** — Stand-alone system tray.

	[http://stalonetray.sourceforge.net/](http://stalonetray.sourceforge.net/) || [stalonetray](https://www.archlinux.org/packages/?name=stalonetray)

*   **[Tint2](/index.php/Tint2 "Tint2")** — Simple panel/taskbar developed specifically for Openbox.

	[https://gitlab.com/o9000/tint2](https://gitlab.com/o9000/tint2) || [tint2](https://www.archlinux.org/packages/?name=tint2)

*   **Trayer** — Lightweight GTK+-based systray.

	[https://gna.org/projects/fvwm-crystal/](https://gna.org/projects/fvwm-crystal/) || [trayer](https://www.archlinux.org/packages/?name=trayer)

*   **Xfce Panel** — Panel included in the [Xfce](/index.php/Xfce "Xfce") desktop.

	[http://docs.xfce.org/xfce/xfce4-panel/start](http://docs.xfce.org/xfce/xfce4-panel/start) || [xfce4-panel](https://www.archlinux.org/packages/?name=xfce4-panel)

*   **[xmobar](/index.php/Xmobar "Xmobar")** — A lightweight, text-based, status bar written in Haskell.

	[http://projects.haskell.org/xmobar/](http://projects.haskell.org/xmobar/) || [xmobar](https://www.archlinux.org/packages/?name=xmobar), [xmobar-git](https://aur.archlinux.org/packages/xmobar-git/)

#### Application launchers

See also [Wikipedia:Comparison of desktop application launchers](https://en.wikipedia.org/wiki/Comparison_of_desktop_application_launchers "wikipedia:Comparison of desktop application launchers").

*   **Albert** — A sophisticated, plugin based standalone keyboard launcher.

	[https://github.com/manuelschneid3r/albert](https://github.com/manuelschneid3r/albert) || [albert](https://aur.archlinux.org/packages/albert/)

*   **Bashrun2** — Provides a different, barebones approach to a run dialog, using a specialized Bash session within a small xterm window.

	[http://henning-bekel.de/bashrun2/](http://henning-bekel.de/bashrun2/) || [bashrun2](https://aur.archlinux.org/packages/bashrun2/)

*   **[dmenu](/index.php/Dmenu "Dmenu")** — Fast and lightweight dynamic menu for X which is also useful as an application launcher.

	[https://tools.suckless.org/dmenu/](https://tools.suckless.org/dmenu/) || [dmenu](https://www.archlinux.org/packages/?name=dmenu)

*   **dmenu-extended** — An extension to *dmenu* for quickly opening files and folders.

	[https://github.com/markjones112358/dmenu-extended](https://github.com/markjones112358/dmenu-extended) || [dmenu-extended-git](https://aur.archlinux.org/packages/dmenu-extended-git/)

*   **dmenu-launch** — Simple *dmenu*-based application launcher. Launches binaries and XDG shortcuts.

	[https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch](https://github.com/Wintervenom/Scripts/blob/master/file/launch/dmenu-launch) || [dmenu-launch](https://aur.archlinux.org/packages/dmenu-launch/)

*   **dmenu2** — Fork of dmenu with many useful patches applied and additional options like screen select, dim or opacity change.

	[https://bitbucket.org/melek/dmenu2](https://bitbucket.org/melek/dmenu2) || [dmenu2](https://aur.archlinux.org/packages/dmenu2/)

*   **dswitcher** — *dmenu*-based window switcher that works regardless of workspace or minimization.

	[https://github.com/Antithesisx/dswitcher](https://github.com/Antithesisx/dswitcher) || [dswitcher-git](https://aur.archlinux.org/packages/dswitcher-git/)

*   **Fehlstart** — Small GTK+-based application launcher.

	[https://gitlab.com/fehlstart/fehlstart](https://gitlab.com/fehlstart/fehlstart) || [fehlstart-git](https://aur.archlinux.org/packages/fehlstart-git/)

*   **[Gmrun](/index.php/Gmrun "Gmrun")** — Lightweight GTK+-based application launcher, with the ability to run programs inside a terminal and other handy features.

	[https://sourceforge.net/projects/gmrun/](https://sourceforge.net/projects/gmrun/) || [gmrun](https://www.archlinux.org/packages/?name=gmrun)

*   **[GNOME Do](https://en.wikipedia.org/wiki/GNOME_Do with many plugins, originally developed for the GNOME desktop.

	[http://do.cooperteam.net/](http://do.cooperteam.net/) || [gnome-do](https://www.archlinux.org/packages/?name=gnome-do)

*   **j4-dmenu-desktop** — Very fast dmenu application launcher.

	[https://github.com/enkore/j4-dmenu-desktop](https://github.com/enkore/j4-dmenu-desktop) || [j4-dmenu-desktop](https://aur.archlinux.org/packages/j4-dmenu-desktop/)

*   **higgins** — A desktop agnostic application launcher, file finder, calculator and more. Plugin based and freely and easily extendable via user-written plugins

	[https://github.com/kokoko3k/higgins](https://github.com/kokoko3k/higgins) || [higgins-git](https://aur.archlinux.org/packages/higgins-git/)

*   **Kupfer** — Convenient command and access tool for the GNOME desktop that can launch applications, open documents and access different types of objects and act on them.

	[https://wiki.gnome.org/Apps/Kupfer](https://wiki.gnome.org/Apps/Kupfer) || [kupfer](https://www.archlinux.org/packages/?name=kupfer)

*   **launch** — Simple command for launching applications from a terminal emulator.

	[https://github.com/silverhammermba/launch](https://github.com/silverhammermba/launch) || [launch-cmd](https://aur.archlinux.org/packages/launch-cmd/)

*   **[Launchy](https://en.wikipedia.org/wiki/Launchy "wikipedia:Launchy")** — Very popular cross-platform application launcher with a plugin-based system used to provide extra functionality.

	[http://www.launchy.net/](http://www.launchy.net/) || [launchy](https://www.archlinux.org/packages/?name=launchy)

*   **Lighthouse** — A simple scriptable popup dialog to run on X.

	[https://github.com/emgram769/lighthouse](https://github.com/emgram769/lighthouse) || [lighthouse-git](https://aur.archlinux.org/packages/lighthouse-git/)

*   **[rofi](/index.php/Rofi "Rofi")** — A popup window switcher roughly based on superswitcher, requiring only xlib and pango.

	[http://davedavenport.github.io/rofi/](http://davedavenport.github.io/rofi/) || [rofi](https://www.archlinux.org/packages/?name=rofi)

*   **slingshot** — An application launcher has a clear look, part of [pantheon](/index.php/Pantheon "Pantheon") desktop environment.

	[https://launchpad.net/slingshot](https://launchpad.net/slingshot) || [slingshot-launcher](https://aur.archlinux.org/packages/slingshot-launcher/)

*   **Runa** — Fast and light dmenu-driven desktop application launcher, suitable for use standalone, integrated into file manager context menus, or as an 'xdg-open' replacement. Favourite applications can also be configured.

	[http://appstogo.mcfadzean.org.uk/linux.html#runa](http://appstogo.mcfadzean.org.uk/linux.html#runa) || [runa](https://aur.archlinux.org/packages/runa/)

*   **Synapse** — Synapse is a semantic launcher written in Vala that you can use to start applications as well as find and access relevant documents and files by making use of the Zeitgeist engine.

	[https://launchpad.net/synapse-project](https://launchpad.net/synapse-project) || [synapse](https://www.archlinux.org/packages/?name=synapse)

*   **Whippet** — A launcher and xdg-open replacement for control freaks. Opens files and URLs with applications associated by name and/or mimetype. Applications and associations may be customized using an SQLite database. Uses dmenu to manage its menus.

	[http://appstogo.mcfadzean.org.uk/linux.html#whippet](http://appstogo.mcfadzean.org.uk/linux.html#whippet) || [whippet](https://aur.archlinux.org/packages/whippet/)

*   **xfce4-appfinder** — An eazy-to-use application launcher from Xfce.

	[http://docs.xfce.org/xfce/xfce4-appfinder/start](http://docs.xfce.org/xfce/xfce4-appfinder/start) || [xfce4-appfinder](https://www.archlinux.org/packages/?name=xfce4-appfinder)

#### Wallpaper setters

See also [Wikipedia:Wallpaper (computing)](https://en.wikipedia.org/wiki/Wallpaper_(computing) "wikipedia:Wallpaper (computing)").

*   **bgs** — An extremely fast and small background setter for X based on imlib2.

	[https://github.com/Gottox/bgs/](https://github.com/Gottox/bgs/) || [bgs-git](https://aur.archlinux.org/packages/bgs-git/)

*   **esetroot** — Eterm's root background setter, packaged separately.

	[http://www.eterm.org/](http://www.eterm.org/) || [esetroot](https://aur.archlinux.org/packages/esetroot/)

*   **[Feh](/index.php/Feh "Feh")** — A lightweight and powerful image viewer that can also be used to manage the desktop wallpaper.

	[http://linuxbrit.co.uk/software/feh/](http://linuxbrit.co.uk/software/feh/) || [feh](https://www.archlinux.org/packages/?name=feh)‎

*   **habak** — A background changing app.

	[http://fvwm-crystal.sourceforge.net/](http://fvwm-crystal.sourceforge.net/) || [habak](https://www.archlinux.org/packages/?name=habak)

*   **hsetroot** — A tool to create compose wallpapers.

	[https://packages.debian.org/sid/hsetroot](https://packages.debian.org/sid/hsetroot) || [hsetroot](https://aur.archlinux.org/packages/hsetroot/)

*   **[Nitrogen](/index.php/Nitrogen "Nitrogen")** — A fast and lightweight desktop background browser and setter for X windows.

	[http://projects.l3ib.org/nitrogen/](http://projects.l3ib.org/nitrogen/) || [nitrogen](https://www.archlinux.org/packages/?name=nitrogen)

*   **pybgsetter** — Multi-backend (hsetroot, Esetroot, habak, feh) to set desktop wallpaper.

	http://bbs.archlinux.org/viewtopic.php?id=88997 || [pybgsetter](https://aur.archlinux.org/packages/pybgsetter/)

*   **pywal** — Changes the wallpaper and creates matching colorschemes for various applications (rofi, i3, termials)

	[https://github.com/dylanaraps/pywal](https://github.com/dylanaraps/pywal) || [python-pywal](https://aur.archlinux.org/packages/python-pywal/)

*   **variety** — Changes the wallpaper on a regular interval using user-specified or automatically downloaded images.

	[http://peterlevi.com/variety/](http://peterlevi.com/variety/) || [variety](https://www.archlinux.org/packages/?name=variety)

*   **wallpaperd** — A small application that takes care of setting the background image.

	[https://projects.pekdon.net/projects/wallpaperd](https://projects.pekdon.net/projects/wallpaperd) || [wallpaperd](https://aur.archlinux.org/packages/wallpaperd/)

*   **xli** — An image display program for X.

	[https://packages.debian.org/sid/xli](https://packages.debian.org/sid/xli) || [xli](https://aur.archlinux.org/packages/xli/)

**Tip:** In order to avoid installing one more package, you may find convenient to use the `display` utility from [imagemagick](https://www.archlinux.org/packages/?name=imagemagick) or `gm display` from [graphicsmagick](https://www.archlinux.org/packages/?name=graphicsmagick). E.g.: `display -backdrop -background '#3f3f3f' -flatten -window root *image*`.

#### Virtual desktop pagers

See also [Wikipedia:Pager (GUI)](https://en.wikipedia.org/wiki/Pager_(GUI) "wikipedia:Pager (GUI)").

*   **bbpager** — Dockable pager for [blackbox](/index.php/Blackbox "Blackbox") and other window managers.

	[http://bbtools.sourceforge.net/download.php?file=6](http://bbtools.sourceforge.net/download.php?file=6) || [bbpager](https://www.archlinux.org/packages/?name=bbpager)

*   **fbpager** — Virtual desktop pager for fluxbox.

	[http://www.fluxbox.org/fbpager](http://www.fluxbox.org/fbpager) || [fbpager-git](https://aur.archlinux.org/packages/fbpager-git/)

*   **IPager** — A configurable pager with transparency, originally developed for Fluxbox.

	[http://useperl.ru/ipager/index.en.html](http://useperl.ru/ipager/index.en.html) || [ipager](https://aur.archlinux.org/packages/ipager/)

*   **Neap** — An non-intrusive and light pager that runs in the notification area of your panel.

	[https://github.com/vzxwco/neap](https://github.com/vzxwco/neap) || [neap-hotkey](https://aur.archlinux.org/packages/neap-hotkey/)

*   **Netwmpager** — A NetWM/EWMH compatible pager.

	[https://sourceforge.net/projects/sf-xpaint/files/netwmpager/](https://sourceforge.net/projects/sf-xpaint/files/netwmpager/) || [netwmpager](https://aur.archlinux.org/packages/netwmpager/)

#### Desktop widgets

*   **[gDesklets](https://en.wikipedia.org/wiki/gDesklets "wikipedia:gDesklets")** — System for bringing mini programs (desklets) onto your desktop.

	[https://launchpad.net/gdesklets](https://launchpad.net/gdesklets) || [gdesklets](https://www.archlinux.org/packages/?name=gdesklets)

*   **GPhotoFrame** — Photo frame gadget for the GNOME Desktop.

	[https://github.com/iblis17/gphotoframe](https://github.com/iblis17/gphotoframe) || [gphotoframe](https://aur.archlinux.org/packages/gphotoframe/)

*   **[Screenlets](https://en.wikipedia.org/wiki/Screenlets "wikipedia:Screenlets")** — Widget framework that consists of small owner-drawn applications.

	[https://launchpad.net/screenlets](https://launchpad.net/screenlets) || [screenlets-pack-basic](https://www.archlinux.org/packages/?name=screenlets-pack-basic)

### Dictionary and Thesaurus

*   **artha** — A free cross-platform English thesaurus that works completely off-line and is based on WordNet.

	[http://artha.sourceforge.net/wiki/index.php/Home](http://artha.sourceforge.net/wiki/index.php/Home) || [artha](https://aur.archlinux.org/packages/artha/)

## See also

**Generic software lists**

*   [Wikipedia:List of free and open source software packages](https://en.wikipedia.org/wiki/List_of_free_and_open_source_software_packages "wikipedia:List of free and open source software packages")
*   [Wikipedia:List of GNU packages](https://en.wikipedia.org/wiki/List_of_GNU_packages "wikipedia:List of GNU packages")
*   [Wikipedia:Portal:Free and open-source software](https://en.wikipedia.org/wiki/Portal:Free_and_open-source_software "wikipedia:Portal:Free and open-source software")
*   [alternativeto.net](https://alternativeto.net/platform/linux/) - Linux alternatives to popular programs
*   [Linux App Finder](https://linuxappfinder.com/all) - Linux applications directory
*   [Debian packages](https://packages.debian.org) and [screenshots](https://screenshots.debian.net)
*   [Linux Alternative Project](http://www.linuxalt.com/) - Linux equivalents to Windows software
*   [Open Source Alternative](https://www.osalt.com/) - Alternatives to commercial software
*   [Linux Links](http://www.linuxlinks.com/) - Application and articles directory

**Software [forges](https://en.wikipedia.org/wiki/Forge_(software) "wikipedia:Forge (software)")**

*   [Sourceforge.net](https://sourceforge.net/) - Open Source Software forge
*   [Launchpad.net](https://launchpad.net/projects/+all) - Open Source Software forge
*   [Gitlab.com](https://gitlab.com/explore) - Open Source Software forge
*   [GitHub.com](https://github.com/explore**) - Open Source Software forge

**Specialized software lists**

*   [K.Mandla's blog](https://kmandla.wordpress.com/software/) - Terminal applications screenshots and reviews
*   [Inconsolation](https://inconsolation.wordpress.com/index/) - Lightweight and minimalist software
*   [awesome-shell](https://github.com/alebcay/awesome-shell) - Command-line frameworks, toolkits and guides
*   [awesome-selfhosted](https://github.com/Kickball/awesome-selfhosted) - Network services and web applications
*   [Libre Projects](http://libreprojects.net/) - Open Source hosted Web services
*   [awesome-sysadmin](https://github.com/n1trux/awesome-sysadmin) - Software for system administrators
*   [awesome-linuxaudio](https://github.com/nodiscc/awesome-linuxaudio) - Software for audio/video/live production
*   [PRISM Break](https://prism-break.org/en/all/) - Software against mass surveillance
*   [Privacy Tools](https://www.privacytools.io/) - Knowledge and tools to protect your privacy against global mass surveillance.
*   [lin-app.com](http://lin-app.com/) - Commercial applications and games for Linux

**Arch Linux forum threads**

*   [Arch Linux Forums / LnF Awards 2011](https://bbs.archlinux.org/viewtopic.php?id=111878) - The best Light & Fast apps of 2011
*   [Arch Linux Forums / LnF Awards 2012](https://bbs.archlinux.org/viewtopic.php?id=138281) - The best Light & Fast apps of 2012
*   [Arch Linux Forums / most popular apps of 2013-2014](https://bbs.archlinux.org/viewtopic.php?id=174764)
*   [Arch Linux Forums / most popular apps of 2017+](https://bbs.archlinux.org/viewtopic.php?pid=1702332)