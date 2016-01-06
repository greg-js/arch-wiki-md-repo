# List of applications/Internet

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

**[List of applications](/index.php/List_of_applications "List of applications")**

* * *

**Internet** – [Multimedia](/index.php/List_of_applications/Multimedia "List of applications/Multimedia") – [Utilities](/index.php/List_of_applications/Utilities "List of applications/Utilities") – [Documents](/index.php/List_of_applications/Documents "List of applications/Documents") – [Security](/index.php/List_of_applications/Security "List of applications/Security") – [Science](/index.php/List_of_applications/Science "List of applications/Science") – [Other](/index.php/List_of_applications/Other "List of applications/Other")

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
    *   [1.3 Downloaders](#Downloaders)
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
        *   [1.3.3 eDonkey clients](#eDonkey_clients)
        *   [1.3.4 Gnutella](#Gnutella)
        *   [1.3.5 Video downloaders](#Video_downloaders)
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

## Internet

**Note:** For possibly more up to date selection of applications, try checking the [AUR 'network' category](https://aur.archlinux.org/packages.php?O=0&K=&do_Search=Go&detail=1&C=13&SeB=nd&SB=n&SO=a&PP=50)

### Network managers

*   **[Connman](/index.php/Connman "Connman")** — Daemon for managing internet connections within embedded devices running the Linux operating system. Comes with a command-line client, plus Enlightenment, GTK and Dmenu clients are available.

[https://connman.net/](https://connman.net/) || [connman](https://www.archlinux.org/packages/?name=connman)

*   **[netctl](/index.php/Netctl "Netctl")** — Simple and robust tool to manage network connections via profiles. Intended for use with [systemd](/index.php/Systemd "Systemd").

[https://projects.archlinux.org/netctl.git/](https://projects.archlinux.org/netctl.git/) || [netctl](https://www.archlinux.org/packages/?name=netctl)

*   **[NetworkManager](/index.php/NetworkManager "NetworkManager")** — Manager that provides wired, wireless, mobile broadband and OpenVPN detection with configuration and automatic connection.

[https://wiki.gnome.org/Projects/NetworkManager](https://wiki.gnome.org/Projects/NetworkManager) || [networkmanager](https://www.archlinux.org/packages/?name=networkmanager)

*   **[systemd-networkd](/index.php/Systemd-networkd "Systemd-networkd")** — Native [systemd](/index.php/Systemd "Systemd") daemon that manages network configuration. It includes support for basic network configuration through udev and networkd. The service is available with systemd > 210.

[http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html](http://www.freedesktop.org/software/systemd/man/systemd-networkd.service.html) || [systemd](https://www.archlinux.org/packages/?name=systemd)

*   **[Wicd](/index.php/Wicd "Wicd")** — Wireless and wired connection manager with few dependencies. Comes with an ncurses interface, and a GTK interface [wicd-gtk](https://www.archlinux.org/packages/?name=wicd-gtk) is available.

[http://wicd.sourceforge.net/](http://wicd.sourceforge.net/) || [wicd](https://www.archlinux.org/packages/?name=wicd)

### Web browsers

See also [Wikipedia:Comparison of web browsers](https://en.wikipedia.org/wiki/Comparison_of_web_browsers "wikipedia:Comparison of web browsers").

#### Console

*   **[ELinks](https://en.wikipedia.org/wiki/ELinks "wikipedia:ELinks")** — Advanced and well-established feature-rich text mode web browser (Links fork, barely supported since 2009).

[http://elinks.or.cz/](http://elinks.or.cz/) || [elinks](https://www.archlinux.org/packages/?name=elinks)

*   **[Links](https://en.wikipedia.org/wiki/Links_(web_browser) "wikipedia:Links (web browser)")** — Text WWW browser. Includes a console version [links] similar to Lynx, and a graphical X-window/framebuffer version [links -g] (must be compiled in, Arch has both) with CSS, image rendering, pull-down menus.

[http://links.twibright.com/](http://links.twibright.com/) || [links](https://www.archlinux.org/packages/?name=links)

*   **[Lynx](https://en.wikipedia.org/wiki/Lynx_(web_browser) "wikipedia:Lynx (web browser)")** — Text browser for the World Wide Web.

[http://lynx.isc.org](http://lynx.isc.org) || [lynx](https://www.archlinux.org/packages/?name=lynx)

*   **retawq** — Interactive, multi-threaded network client (web browser) for text terminals.

[http://retawq.sourceforge.net/](http://retawq.sourceforge.net/) || [retawq](https://aur.archlinux.org/packages/retawq/)<sup><small>AUR</small></sup>

*   **[w3m](https://en.wikipedia.org/wiki/W3m "wikipedia:W3m")** — Pager/text-based web browser. It has vim-like keybindings, and is able to display images. It has javascript support too.

[http://w3m.sourceforge.net/](http://w3m.sourceforge.net/) || [w3m](https://www.archlinux.org/packages/?name=w3m)

#### Graphical

##### Gecko-based

See also [Wikipedia:Gecko (software)](https://en.wikipedia.org/wiki/Gecko_(software) "wikipedia:Gecko (software)").

*   **[Conkeror](https://en.wikipedia.org/wiki/Conkeror "wikipedia:Conkeror")** — Keyboard-based browser modeled after [Emacs](/index.php/Emacs "Emacs") using [XULRunner](https://en.wikipedia.org/wiki/XULRunner "wikipedia:XULRunner"). Customizable via JavaScript.

[http://repo.or.cz/w/conkeror.git/](http://repo.or.cz/w/conkeror.git/) || [conkeror-git](https://aur.archlinux.org/packages/conkeror-git/)<sup><small>AUR</small></sup>

*   **[Firefox](/index.php/Firefox "Firefox")** — Extensible browser from Mozilla based on Gecko with fast rendering.

[https://mozilla.com/firefox](https://mozilla.com/firefox) || [firefox](https://www.archlinux.org/packages/?name=firefox)

*   **Seamonkey** — Continuation of the Mozilla Internet Suite.

[http://www.seamonkey-project.org/](http://www.seamonkey-project.org/) || [seamonkey](https://www.archlinux.org/packages/?name=seamonkey)

###### Firefox forks

**Warning:** The following browsers are third-party builds of Firefox. Please direct any support requests to their respective creators.

*   **[GNU IceCat](https://en.wikipedia.org/wiki/GNU_IceCat "wikipedia:GNU IceCat")** — Web browser distributed by the GNU Project, stripped of non-free components and with additional privacy extensions. Release cycle may be delayed compared to Mozilla Firefox.

[https://www.gnu.org/software/gnuzilla/](https://www.gnu.org/software/gnuzilla/) || [icecat](https://aur.archlinux.org/packages/icecat/)<sup><small>AUR</small></sup>

*   **[Iceweasel](https://en.wikipedia.org/wiki/Mozilla_Corporation_software_rebranded_by_the_Debian_project#Iceweasel "wikipedia:Mozilla Corporation software rebranded by the Debian project")** — Fork of Firefox developed by Debian Linux. The main difference is that it does not include any trademarked Mozilla artwork. See [glandium](http://web.glandium.org/blog/?p=97) for more information on Iceweasel's existence.

[https://wiki.debian.org/Iceweasel](https://wiki.debian.org/Iceweasel) || [iceweasel](https://aur.archlinux.org/packages/iceweasel/)<sup><small>AUR</small></sup>

*   **[Pale Moon](https://en.wikipedia.org/wiki/Pale_Moon_(web_browser) "wikipedia:Pale Moon (web browser)")** — Fork based on Firefox, using a Firefox 3+ interface through selective use of add-ons. Firefox add-ons may not be compatible. [[1]](https://addons.palemoon.org/firefox/incompatible/) Compiled for SSE2, with disabled optional code and no support for newer Firefox features such as cache2, e10s, and OTMC.

[http://www.palemoon.org/](http://www.palemoon.org/) || [palemoon-bin](https://aur.archlinux.org/packages/palemoon-bin/)<sup><small>AUR</small></sup>

##### Blink-based

See also [Wikipedia:Blink (layout engine)](https://en.wikipedia.org/wiki/Blink_(layout_engine) "wikipedia:Blink (layout engine)").

*   **[Chromium](/index.php/Chromium "Chromium")** — Web browser developed by Google, the open source project behind Google Chrome.

[http://www.chromium.org/](http://www.chromium.org/) || [chromium](https://www.archlinux.org/packages/?name=chromium)

*   **[Opera](/index.php/Opera "Opera")** — Highly customizable browser with focuses on an adherence to web rendering standards.

[http://opera.com](http://opera.com) || [opera](https://www.archlinux.org/packages/?name=opera)

##### Webkit-based

See also [Wikipedia:Webkit](https://en.wikipedia.org/wiki/Webkit "wikipedia:Webkit").

*   **[Arora](https://en.wikipedia.org/wiki/Arora_(browser) "wikipedia:Arora (browser)")** — Cross-platform web browser built using QtWebKit. Development stopped in January 2012.

[https://code.google.com/p/arora/](https://code.google.com/p/arora/) || [arora](https://aur.archlinux.org/packages/arora/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): package not found]</sup>

*   **[dwb](/index.php/Dwb "Dwb")** — Lightweight, highly customizable web browser based on the WebKit engine with _vi_-like shortcuts and tiling layouts. As of October 2014 _dwb_ is [unmaintained](https://bitbucket.org/portix/dwb/pull-request/22/several-cleanups-to-increase-portability/diff#comment-3217936).

[http://portix.bitbucket.org/dwb/](http://portix.bitbucket.org/dwb/) || [dwb](https://www.archlinux.org/packages/?name=dwb)

*   **[GNOME Web](/index.php/GNOME_Web "GNOME Web")** — Browser which uses the WebKitGTK+ rendering engine, part of [gnome](https://www.archlinux.org/groups/x86_64/gnome/).

[https://wiki.gnome.org/Apps/Web/](https://wiki.gnome.org/Apps/Web/) || [epiphany](https://www.archlinux.org/packages/?name=epiphany)

*   **[Jumanji](/index.php/Jumanji "Jumanji")** — Highly customizable and functional web browser.

[http://pwmt.org/projects/jumanji](http://pwmt.org/projects/jumanji) || [jumanji](https://aur.archlinux.org/packages/jumanji/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/jumanji)]</sup>

*   **[Luakit](/index.php/Luakit "Luakit")** — Highly configurable, micro-browser framework based on the WebKit engine and the GTK+ toolkit. It is very fast, extensible by Lua and licensed under the GNU GPLv3 license.

[http://mason-larobina.github.com/luakit/](http://mason-larobina.github.com/luakit/) || [luakit](https://www.archlinux.org/packages/?name=luakit)

*   **Maxthon** — A browser that combines a minimal design with sophisticated technology to make the web faster, safer, and easier.

[http://www.maxthon.cn/](http://www.maxthon.cn/) || [maxthon-browser](https://aur.archlinux.org/packages/maxthon-browser/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/maxthon-browser)]</sup>

*   **[Midori](https://en.wikipedia.org/wiki/Midori_(web_browser) "wikipedia:Midori (web browser)")** — Lightweight web browser based on GTK+ and WebKit.

[http://midori-browser.org/](http://midori-browser.org/) || [midori](https://www.archlinux.org/packages/?name=midori)

*   **Otter-browser** — Browser aiming to recreate classic Opera (12.x) UI using Qt5.

[http://otter-browser.org/](http://otter-browser.org/) || [otter-browser](https://aur.archlinux.org/packages/otter-browser/)<sup><small>AUR</small></sup>

*   **[QupZilla](https://en.wikipedia.org/wiki/QupZilla "wikipedia:QupZilla")** — New and very fast open source browser based on WebKit core, written in Qt framework.

[http://www.qupzilla.com](http://www.qupzilla.com) || [qupzilla](https://www.archlinux.org/packages/?name=qupzilla)

*   **[qutebrowser](/index.php/Qutebrowser "Qutebrowser")** — A keyboard-driven, [vim](/index.php/Vim "Vim")-like browser based on PyQt5 and QtWebKit.

[https://github.com/The-Compiler/qutebrowser](https://github.com/The-Compiler/qutebrowser) || [qutebrowser](https://aur.archlinux.org/packages/qutebrowser/)<sup><small>AUR</small></sup>

*   **[Rekonq](https://en.wikipedia.org/wiki/Rekonq "wikipedia:Rekonq")** — WebKit-based web browser for KDE.

[http://rekonq.kde.org/](http://rekonq.kde.org/) || [rekonq](https://www.archlinux.org/packages/?name=rekonq)

*   **Sb** — Very lightweight WebKit-based browser that uses keybindings to perform most things the URL bar would usually do.

[https://github.com/mutantturkey/sb/](https://github.com/mutantturkey/sb/) || [sb-git](https://aur.archlinux.org/packages/sb-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sb-git)]</sup>

*   **SlimBoat** — Fast, free secure and powerful web browser based on QtWebkit.

[http://www.slimboat.com/](http://www.slimboat.com/) || [slimboat](https://aur.archlinux.org/packages/slimboat/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/slimboat)]</sup>

*   **Surf** — Lightweight WebKit-based browser, which follows the [suckless ideology](http://suckless.org/philosophy) (basically, the browser itself is a single C source file).

[http://surf.suckless.org](http://surf.suckless.org) || [surf](https://www.archlinux.org/packages/?name=surf)

*   **[Uzbl](https://en.wikipedia.org/wiki/Uzbl "wikipedia:Uzbl")** — Group of web interface tools which adhere to the Unix philosophy.

[http://uzbl.org/](http://uzbl.org/) || [uzbl-browser](https://www.archlinux.org/packages/?name=uzbl-browser)

*   **vimb** — Fast and lightweight vim like web browser based on the webkit web browser engine and the GTK toolkit.

[https://fanglingsu.github.io/vimb/](https://fanglingsu.github.io/vimb/) || [vimb](https://aur.archlinux.org/packages/vimb/)<sup><small>AUR</small></sup>

*   **[Vimprobable](/index.php/Vimprobable "Vimprobable")** — Browser that behaves like the Vimperator plugin available for Mozilla Firefox. It is based on the WebKit engine and uses the GTK+ bindings.

[http://sourceforge.net/apps/trac/vimprobable/](http://sourceforge.net/apps/trac/vimprobable/) || [vimprobable-git](https://aur.archlinux.org/packages/vimprobable-git/)<sup><small>AUR</small></sup>

*   **[Xombrero](https://en.wikipedia.org/wiki/Xombrero "wikipedia:Xombrero") (formerly known as _xxxterm_)** — Webkit minimalist web browser with sophisticated security features designed-in, BSD style.

[https://opensource.conformal.com/wiki/xombrero](https://opensource.conformal.com/wiki/xombrero) || [xombrero-git](https://aur.archlinux.org/packages/xombrero-git/)<sup><small>AUR</small></sup>

##### Other

*   **[Abaco](https://en.wikipedia.org/wiki/Abaco_(web_browser) "wikipedia:Abaco (web browser)")** — Multi-page graphical web browser for the Plan 9 OS.

[http://lab-fgb.com/abaco/](http://lab-fgb.com/abaco/) || [abaco](https://aur.archlinux.org/packages/abaco/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/abaco)]</sup>

*   **[Dillo](https://en.wikipedia.org/wiki/Dillo "wikipedia:Dillo")** — Small, fast graphical web browser built on [FLTK](https://en.wikipedia.org/wiki/Fltk "wikipedia:Fltk").

[http://dillo.org/](http://dillo.org/) || [dillo](https://www.archlinux.org/packages/?name=dillo)

*   **[Konqueror](https://en.wikipedia.org/wiki/Konqueror "wikipedia:Konqueror")** — Web browser based on Qt and KHTML, part of [kdebase](https://www.archlinux.org/groups/x86_64/kdebase/).

[http://konqueror.org/](http://konqueror.org/) || [kdebase-konqueror](https://www.archlinux.org/packages/?name=kdebase-konqueror)

*   **[NetSurf](https://en.wikipedia.org/wiki/NetSurf "wikipedia:NetSurf")** — Featherweight browser written in C, notable for its slowly developing JavaScript support and fast rendering through its own custom rendering engine.

[http://netsurf-browser.org](http://netsurf-browser.org) || [netsurf](https://www.archlinux.org/packages/?name=netsurf)

### Downloaders

#### FTP

##### FTP clients

See also [Wikipedia:Comparison of FTP client software](https://en.wikipedia.org/wiki/Comparison_of_FTP_client_software "wikipedia:Comparison of FTP client software").

*   **[CurlFtpFS](/index.php/CurlFtpFS "CurlFtpFS")** — Filesystem for accessing FTP hosts; based on FUSE and libcurl.

[http://curlftpfs.sourceforge.net/](http://curlftpfs.sourceforge.net/) || [curlftpfs](https://www.archlinux.org/packages/?name=curlftpfs)

*   **FatRat** — Download manager with support for HTTP, FTP, SFTP, BitTorrent, RapidShare and more.

[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat-git](https://aur.archlinux.org/packages/fatrat-git/)<sup><small>AUR</small></sup>

*   **[FileZilla](https://en.wikipedia.org/wiki/FileZilla "wikipedia:FileZilla")** — Fast and reliable FTP, FTPS and SFTP client.

[http://filezilla-project.org/](http://filezilla-project.org/) || [filezilla](https://www.archlinux.org/packages/?name=filezilla)

*   **[fuseftp](/index.php/FtpFs#Fuseftp "FtpFs")** — FTP filesystem written in Perl, using [FUSE](https://en.wikipedia.org/wiki/Filesystem_in_Userspace "wikipedia:Filesystem in Userspace").

[http://freshmeat.net/projects/fuseftp/](http://freshmeat.net/projects/fuseftp/) || [fuseftp](https://aur.archlinux.org/packages/fuseftp/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/fuseftp)]</sup>

*   **[gFTP](https://en.wikipedia.org/wiki/gFTP "wikipedia:gFTP")** — Multithreaded FTP client for Linux.

[http://gftp.seul.org/](http://gftp.seul.org/) || [gftp](https://www.archlinux.org/packages/?name=gftp)

*   **[LFTP](https://en.wikipedia.org/wiki/Lftp "wikipedia:Lftp")** — Sophisticated command-line FTP client.

[http://lftp.yar.ru/](http://lftp.yar.ru/) || [lftp](https://www.archlinux.org/packages/?name=lftp)

*   **LftpFS** — Read-only filesystem based on lftp (also supports HTTP, FISH, SFTP, HTTPS, FTPS and proxies).

[http://lftpfs.sourceforge.net/](http://lftpfs.sourceforge.net/) || [lftpfs](https://aur.archlinux.org/packages/lftpfs/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/lftpfs)]</sup>

*   **ncftp** — A set of free application programs implementing FTP.

[http://www.ncftp.com/](http://www.ncftp.com/) || [ncftp](https://www.archlinux.org/packages/?name=ncftp)

*   **[tnftp](https://en.wikipedia.org/wiki/tnftp "wikipedia:tnftp")** — FTP client with several advanced features for [NetBSD](https://en.wikipedia.org/wiki/NetBSD "wikipedia:NetBSD").

[http://freecode.com/projects/tnftp](http://freecode.com/projects/tnftp) || [tnftp](https://www.archlinux.org/packages/?name=tnftp)

Some file managers like Dolphin, [GNOME Files](/index.php/GNOME_Files "GNOME Files") and [Thunar](/index.php/Thunar "Thunar") also provide FTP functionality.

##### FTP servers

*   **bftpd** — Small, easy-to-configure FTP server

[http://bftpd.sourceforge.net/](http://bftpd.sourceforge.net/) || [bftpd](https://www.archlinux.org/packages/?name=bftpd)

*   **[proFTPd](/index.php/Proftpd "Proftpd")** — A secure and configurable FTP server

[http://www.proftpd.org/](http://www.proftpd.org/) || [proftpd](https://aur.archlinux.org/packages/proftpd/)<sup><small>AUR</small></sup>

*   **[Pure-FTPd](/index.php/Pure-FTPd "Pure-FTPd")** — Free (BSD-licensed), secure, production-quality and standard-compliant FTP server.

[http://www.pureftpd.org/project/pure-ftpd](http://www.pureftpd.org/project/pure-ftpd) || [pure-ftpd](https://aur.archlinux.org/packages/pure-ftpd/)<sup><small>AUR</small></sup>

*   **[vsftpd](/index.php/Vsftpd "Vsftpd")** — Lightweight, stable and secure FTP server for UNIX-like systems.

[https://security.appspot.com/vsftpd.html](https://security.appspot.com/vsftpd.html) || [vsftpd](https://www.archlinux.org/packages/?name=vsftpd)

#### BitTorrent clients

See also [Wikipedia:Comparison of BitTorrent clients](https://en.wikipedia.org/wiki/Comparison_of_BitTorrent_clients "wikipedia:Comparison of BitTorrent clients").

##### Console

###### Command line / backend

Can be used as-is via command line, but all have a choice of front-end options as well.

*   **[aria2](/index.php/Aria2 "Aria2")** — Lightweight download utility that supports simultaneous adaptive downloading via HTTP(S), FTP, BitTorrent (DHT, PEX, MSE/PE) protocols and Metalink. It can run as a daemon controlled via a built-in JSON-RPC or XML-RPC interface.

[http://aria2.sourceforge.net/](http://aria2.sourceforge.net/) || [aria2](https://www.archlinux.org/packages/?name=aria2)

*   **[Ctorrent](/index.php?title=Ctorrent&action=edit&redlink=1 "Ctorrent (page does not exist)")** — CTorrent is a BitTorrent client implemented in C++ to be lightweight and quick.

[http://www.rahul.net/dholmes/ctorrent/](http://www.rahul.net/dholmes/ctorrent/) || [enhanced-ctorrent](https://aur.archlinux.org/packages/enhanced-ctorrent/)<sup><small>AUR</small></sup>

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

[http://fatrat.dolezel.info/](http://fatrat.dolezel.info/) || [fatrat-git](https://aur.archlinux.org/packages/fatrat-git/)<sup><small>AUR</small></sup>

*   **[qBittorrent](https://en.wikipedia.org/wiki/qBittorrent "wikipedia:qBittorrent")** — Open source (GPLv2) BitTorrent client that strongly resembles µtorrent.

[http://www.qbittorrent.org/](http://www.qbittorrent.org/) || [qbittorrent](https://www.archlinux.org/packages/?name=qbittorrent)

*   **[Tribler](https://en.wikipedia.org/wiki/Tribler "wikipedia:Tribler")** — 4th generation file sharing system bittorrent client.

[http://www.tribler.org](http://www.tribler.org) || [tribler](https://aur.archlinux.org/packages/tribler/)<sup><small>AUR</small></sup>

###### libktorrent backend

*   **[KGet](https://en.wikipedia.org/wiki/KGet "wikipedia:KGet")** — Download manager for KDE that supports HTTP(S), FTP and BitTorrent. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

[http://www.kde.org/applications/internet/kget/](http://www.kde.org/applications/internet/kget/) || [kdenetwork-kget](https://www.archlinux.org/packages/?name=kdenetwork-kget)

*   **[Ktorrent](/index.php/Ktorrent "Ktorrent")** — Feature-rich BitTorrent client for KDE.

[http://ktorrent.org/](http://ktorrent.org/) || [ktorrent](https://www.archlinux.org/packages/?name=ktorrent)

###### others

*   **Tixati** — P2P client that uses the BitTorrent protocol.

[http://www.tixati.com](http://www.tixati.com) || [tixati](https://aur.archlinux.org/packages/tixati/)<sup><small>AUR</small></sup>

*   **[Transmission](/index.php/Transmission "Transmission")** — Simple and easy-to-use BitTorrent client with daemon version, GTK+, Qt GUI, web and CLI front-ends.

[http://transmissionbt.com/](http://transmissionbt.com/) || [transmission-gtk](https://www.archlinux.org/packages/?name=transmission-gtk) [transmission-qt](https://www.archlinux.org/packages/?name=transmission-qt) [transmission-remote-gtk](https://aur.archlinux.org/packages/transmission-remote-gtk/)<sup><small>AUR</small></sup> (remote clients work with the daemon in the -cli package)

*   **[Vuze](https://en.wikipedia.org/wiki/Vuze "wikipedia:Vuze")** — Feature-rich BitTorrent client written in Java (formerly Azureus).

[https://www.vuze.com/](https://www.vuze.com/) || [vuze](https://aur.archlinux.org/packages/vuze/)<sup><small>AUR</small></sup>

*   **Vuze Plus Extreme Mod** — A modded version of the Vuze BitTorrent client with multiple spoofing capabilities.

[http://www.sb-innovation.de/f41/vuze-extreme-mod-sb-innovation-5-6-1-3-a-32315/](http://www.sb-innovation.de/f41/vuze-extreme-mod-sb-innovation-5-6-1-3-a-32315/) || [vuze-extreme-mod](https://aur.archlinux.org/packages/vuze-extreme-mod/)<sup><small>AUR</small></sup>

#### eDonkey clients

eDonkey is still the second-largest p2p network (see [Internet Study 2008/2009](http://ipoque.com/en/resources/internet-studies)).

See also [Wikipedia:Comparison of eDonkey software](https://en.wikipedia.org/wiki/Comparison_of_eDonkey_software "wikipedia:Comparison of eDonkey software").

*   **[aMule](/index.php/AMule "AMule")** — Well-known eDonkey/Kad client with a daemon version and GTK+, web, and CLI front-ends.

[http://www.amule.org/](http://www.amule.org/) || [amule](https://www.archlinux.org/packages/?name=amule)

*   **KaMule** — KDE graphical front-end for aMule.

[http://kde-apps.org/content/show.php?content=150270](http://kde-apps.org/content/show.php?content=150270) || [kamule](https://aur.archlinux.org/packages/kamule/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kamule)]</sup>

*   **MlDonkey** — A multi-network P2P client.

[http://mldonkey.sourceforge.net/](http://mldonkey.sourceforge.net/) || [mldonkey](https://www.archlinux.org/packages/?name=mldonkey)

#### Gnutella

*   **[Sharelin](https://en.wikipedia.org/wiki/Sharelin "wikipedia:Sharelin")** — Gnutella2 only client with a web UI.

[http://sourceforge.net/apps/mediawiki/sharelin](http://sourceforge.net/apps/mediawiki/sharelin) || [sharelin](https://aur.archlinux.org/packages/sharelin/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sharelin)]</sup>

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

[https://github.com/pazz/alot](https://github.com/pazz/alot) || [alot](https://aur.archlinux.org/packages/alot/)<sup><small>AUR</small></sup> [alot-git](https://aur.archlinux.org/packages/alot-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/alot-git)]</sup>

*   **[Alpine](/index.php/Alpine "Alpine")** — Fast, easy-to-use and Apache-licensed email client based on [Pine](https://en.wikipedia.org/wiki/Pine_(email_client) "wikipedia:Pine (email client)").

[http://patches.freeiz.com/alpine/](http://patches.freeiz.com/alpine/) || [alpine](https://aur.archlinux.org/packages/alpine/)<sup><small>AUR</small></sup>

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

[http://gnus.org/](http://gnus.org/) || [emacs-gnus-git](https://aur.archlinux.org/packages/emacs-gnus-git/)<sup><small>AUR</small></sup>

*   **[S-nail](/index.php/S-nail "S-nail")** — a mail processing system with a command syntax reminiscent of _ed_ with lines replaced by messages. Provides the functionality of [mailx](https://en.wikipedia.org/wiki/mailx "wikipedia:mailx").

[http://sourceforge.net/projects/s-nail/](http://sourceforge.net/projects/s-nail/) || [s-nail](https://www.archlinux.org/packages/?name=s-nail)

*   **mu/mu4e** — Email indexer (mu) and client for emacs (mu4e). Xapian based for fast searches.

[http://www.djcbsoftware.nl/code/mu/mu4e.html](http://www.djcbsoftware.nl/code/mu/mu4e.html) || [mu](https://aur.archlinux.org/packages/mu/)<sup><small>AUR</small></sup>

*   **[Mutt](/index.php/Mutt "Mutt")** — Small but very powerful text-based mail client.

[http://www.mutt.org/](http://www.mutt.org/) || [mutt](https://www.archlinux.org/packages/?name=mutt)

*   **[nmh](/index.php/Nmh "Nmh")** — A modular mail handling system.

[http://www.nongnu.org/nmh/](http://www.nongnu.org/nmh/) || [nmh](https://aur.archlinux.org/packages/nmh/)<sup><small>AUR</small></sup> [nmh-git](https://aur.archlinux.org/packages/nmh-git/)<sup><small>AUR</small></sup>

*   **[notmuch](/index.php/Notmuch "Notmuch")** — A fast mail indexer built on top of _xapian_.

[http://notmuchmail.org/](http://notmuchmail.org/) || [notmuch](https://www.archlinux.org/packages/?name=notmuch) [notmuch-vim](https://www.archlinux.org/packages/?name=notmuch-vim) [notmuch-mutt](https://www.archlinux.org/packages/?name=notmuch-mutt)

*   **[Sup](/index.php/Sup "Sup")** — CLI mail client with very fast searching, tagging, threading and GMail like operation.

[http://supmua.org/](http://supmua.org/) || [sup](https://aur.archlinux.org/packages/sup/)<sup><small>AUR</small></sup>

*   **Wanderlust** — Email client and news reader for Emacs.

[http://www.gohome.org/wl/](http://www.gohome.org/wl/) || [wanderlust](https://www.archlinux.org/packages/?name=wanderlust)

##### Graphical

*   **[Balsa](/index.php/Balsa "Balsa")** — Simple and light email client that is part of the Gnome project.

[http://pawsa.fedorapeople.org/balsa/](http://pawsa.fedorapeople.org/balsa/) || [balsa](https://www.archlinux.org/packages/?name=balsa)

*   **[Claws Mail](https://en.wikipedia.org/wiki/Claws_Mail "wikipedia:Claws Mail")** — Lightweight GTK-based email client and news reader.

[http://claws-mail.org/](http://claws-mail.org/) || [claws-mail](https://www.archlinux.org/packages/?name=claws-mail)

*   **[Evolution](/index.php/Evolution "Evolution")** — Mature and feature-rich e-mail client used in GNOME by default. Part of [gnome-extra](https://www.archlinux.org/groups/x86_64/gnome-extra/).

[https://wiki.gnome.org/Apps/Evolution](https://wiki.gnome.org/Apps/Evolution) || [evolution](https://www.archlinux.org/packages/?name=evolution)

*   **FossaMail** — FossaMail is a Mozilla Thunderbird-based mail, news and chat client by the Pale Moon developers.

[http://www.fossamail.org](http://www.fossamail.org) || [fossamail-bin](https://aur.archlinux.org/packages/fossamail-bin/)<sup><small>AUR</small></sup>

*   **Geary** — Simple desktop mail client built in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

[https://wiki.gnome.org/Apps/Geary](https://wiki.gnome.org/Apps/Geary) || [geary](https://www.archlinux.org/packages/?name=geary)

*   **[Kmail](https://en.wikipedia.org/wiki/Kmail "wikipedia:Kmail")** — Mature and feature-rich email client. Part of [kdepim](https://www.archlinux.org/groups/x86_64/kdepim/).

[http://kde.org/applications/internet/kmail/](http://kde.org/applications/internet/kmail/) || [kmail](https://www.archlinux.org/packages/?name=kmail)

*   **Manitou Mail** — Database-driven email system.

[http://www.manitou-mail.org/](http://www.manitou-mail.org/) || [manitou-mdx](https://aur.archlinux.org/packages/manitou-mdx/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/manitou-mdx)]</sup> [manitou-ui](https://aur.archlinux.org/packages/manitou-ui/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/manitou-ui)]</sup>

*   **Roundcubemail** — Browser-based multilingual IMAP client with a native application-like user interface.

[http://roundcube.net/](http://roundcube.net/) || [roundcubemail](https://www.archlinux.org/packages/?name=roundcubemail)

*   **[Sylpheed](https://en.wikipedia.org/wiki/Sylpheed "wikipedia:Sylpheed")** — Lightweight and user-friendly GTK+ email client.

[http://sylpheed.sraoss.jp/en/](http://sylpheed.sraoss.jp/en/) || [sylpheed](https://www.archlinux.org/packages/?name=sylpheed)

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Feature-rich email client from Mozilla written in GTK+.

[http://www.mozilla.org/thunderbird/](http://www.mozilla.org/thunderbird/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

*   **Trojitá** — Qt IMAP email client. Only supports one IMAP account.

[http://trojita.flaska.net/](http://trojita.flaska.net/) || [trojita](https://www.archlinux.org/packages/?name=trojita)

#### Instant messaging

See also [Wikipedia:Comparison of instant messaging protocols](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_protocols "wikipedia:Comparison of instant messaging protocols").

This section lists all software with [instant messaging](https://en.wikipedia.org/wiki/Instant_messaging "wikipedia:Instant messaging") support. Particularly, that are client and server applications.

##### IRC clients

See also [Wikipedia:Comparison of Internet Relay Chat clients](https://en.wikipedia.org/wiki/Comparison_of_Internet_Relay_Chat_clients "wikipedia:Comparison of Internet Relay Chat clients").

**Note:** Most web browsers and many IM clients also support IRC.

###### Console

*   **[BitchX](https://en.wikipedia.org/wiki/BitchX "wikipedia:BitchX")** — Console-based IRC client developed from the popular [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

[http://www.bitchx.org/](http://www.bitchx.org/) || [bitchx-git](https://aur.archlinux.org/packages/bitchx-git/)<sup><small>AUR</small></sup>

*   **ERC** — Powerful, modular, and extensible IRC client for [Emacs](/index.php/Emacs "Emacs").

[http://savannah.gnu.org/projects/erc/](http://savannah.gnu.org/projects/erc/) || [erc-git](https://aur.archlinux.org/packages/erc-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/erc-git)]</sup>

*   **[ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)")** — Featherweight IRC client, literally `tail -f` the conversation and `echo` back your replies to a file.

[http://tools.suckless.org/ii](http://tools.suckless.org/ii) || [ii](https://aur.archlinux.org/packages/ii/)<sup><small>AUR</small></sup>

*   **Ircfs** — File system interface to IRC written in [Limbo](http://limbo.cat-v.org).

[http://www.ueber.net/code/r/ircfs](http://www.ueber.net/code/r/ircfs) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=ircfs)</small>

*   **[Irssi](/index.php/Irssi "Irssi")** — Highly-configurable ncurses-based IRC client.

[http://irssi.org/](http://irssi.org/) || [irssi](https://www.archlinux.org/packages/?name=irssi)

*   **ScrollZ** — Advanced IRC client based on [ircII](https://en.wikipedia.org/wiki/ircII "wikipedia:ircII").

[http://www.scrollz.info/](http://www.scrollz.info/) || [scrollz](https://aur.archlinux.org/packages/scrollz/)<sup><small>AUR</small></sup>

*   **sic** — Extremely simple IRC client, similar to [ii](https://en.wikipedia.org/wiki/Ii_(IRC_client) "wikipedia:Ii (IRC client)").

[http://tools.suckless.org/sic](http://tools.suckless.org/sic) || [sic](https://aur.archlinux.org/packages/sic/)<sup><small>AUR</small></sup>}}

*   **[WeeChat](https://en.wikipedia.org/wiki/WeeChat "wikipedia:WeeChat")** — Modular, lightweight ncurses-based IRC client.

[http://weechat.org/](http://weechat.org/) || [weechat](https://www.archlinux.org/packages/?name=weechat)

###### Graphical

*   **HexChat** — Fork of XChat for Linux and Windows.

[http://hexchat.github.io/](http://hexchat.github.io/) || [hexchat](https://www.archlinux.org/packages/?name=hexchat)

*   **[Konversation](https://en.wikipedia.org/wiki/Konversation "wikipedia:Konversation")** — Qt-based IRC client for the KDE desktop.

[http://konversation.kde.org/](http://konversation.kde.org/) || [konversation](https://www.archlinux.org/packages/?name=konversation)

*   **[KVIrc](https://en.wikipedia.org/wiki/KVIrc "wikipedia:KVIrc")** — Qt-based IRC client featuring extensive themes support.

[http://kvirc.net/](http://kvirc.net/) || [kvirc](https://www.archlinux.org/packages/?name=kvirc)

*   **Loqui** — GTK+ IRC client with only one dependency: [GNet](https://wiki.gnome.org/Projects/GNetLibrary).

[https://launchpad.net/loqui](https://launchpad.net/loqui) || [loqui](https://aur.archlinux.org/packages/loqui/)<sup><small>AUR</small></sup>

*   **LostIRC** — Simple GTK+ IRC client with tab-autocompletion, multiple server support, logging and others.

[http://lostirc.sourceforge.net](http://lostirc.sourceforge.net) || [lostirc](https://aur.archlinux.org/packages/lostirc/)<sup><small>AUR</small></sup>

*   **pcw** — Frontend for [ii](http://tools.suckless.org/ii) that opens a new terminal for each channel.

[https://bitbucket.org/emg/pcw](https://bitbucket.org/emg/pcw) || [pcw-hg](https://aur.archlinux.org/packages/pcw-hg/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pcw-hg)]</sup>

*   **Polari** — Simple IRC client by the GNOME project.

[https://wiki.gnome.org/Apps/Polari/](https://wiki.gnome.org/Apps/Polari/) || [polari](https://www.archlinux.org/packages/?name=polari)

*   **[Quassel](https://en.wikipedia.org/wiki/Quassel_IRC "wikipedia:Quassel IRC")** — Modern, cross-platform, distributed IRC client.

[http://quassel-irc.org/](http://quassel-irc.org/) || [quassel-core](https://www.archlinux.org/packages/?name=quassel-core) [quassel-client](https://www.archlinux.org/packages/?name=quassel-client)

*   **[Smuxi](https://en.wikipedia.org/wiki/Smuxi "wikipedia:Smuxi")** — Cross-platform IRC client for the GNOME desktop inspired by [Irssi](/index.php/Irssi "Irssi").

[http://smuxi.org/](http://smuxi.org/) || [smuxi](https://www.archlinux.org/packages/?name=smuxi)

*   **[XChat](https://en.wikipedia.org/wiki/XChat "wikipedia:XChat")** — GTK-based IRC client that works on both Linux and Windows.

[http://xchat.org/](http://xchat.org/) || [xchat](https://www.archlinux.org/packages/?name=xchat)

##### XMPP (Jabber)

See also [Wikipedia:XMPP](https://en.wikipedia.org/wiki/XMPP "wikipedia:XMPP") and [Wikipedia:Comparison of instant messaging clients#XMPP-related features](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients#XMPP-related_features "wikipedia:Comparison of instant messaging clients").

###### Console clients

*   **Freetalk** — Console-based Jabber client.

[https://gnu.org/s/freetalk/](https://gnu.org/s/freetalk/) || [freetalk](https://www.archlinux.org/packages/?name=freetalk)

*   **jabber.el** — Minimal Jabber client for [Emacs](/index.php/Emacs "Emacs").

[http://emacs-jabber.sourceforge.net/](http://emacs-jabber.sourceforge.net/) || [emacs-jabber](https://aur.archlinux.org/packages/emacs-jabber/)<sup><small>AUR</small></sup>

*   **[MCabber](https://en.wikipedia.org/wiki/MCabber "wikipedia:MCabber")** — Small Jabber console client, includes features: SSL, PGP, MUC, OTR, and UTF8.

[http://mcabber.com/](http://mcabber.com/) || [mcabber](https://www.archlinux.org/packages/?name=mcabber)

*   **Profanity** — A console based Jabber client inspired by Irssi.

[http://www.profanity.im/](http://www.profanity.im/) || [profanity](https://www.archlinux.org/packages/?name=profanity)

*   **Poezio** — XMPP client with IRC feeling

[https://poez.io/](https://poez.io/) || [poezio](https://aur.archlinux.org/packages/poezio/)<sup><small>AUR</small></sup>

###### Graphical clients

*   **[Gajim](https://en.wikipedia.org/wiki/Gajim "wikipedia:Gajim")** — Jabber client written in PyGTK.

[https://gajim.org/](https://gajim.org/) || [gajim](https://www.archlinux.org/packages/?name=gajim)

*   **Jabbim** — Jabber client written in PyQt.

[http://www.jabbim.com/](http://www.jabbim.com/) || [jabbim-svn](https://aur.archlinux.org/packages/jabbim-svn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/jabbim-svn)]</sup>

*   **[Psi](https://en.wikipedia.org/wiki/Psi_(instant_messaging_client) "wikipedia:Psi (instant messaging client)")** — Qt-based Jabber client which supports video conferencing (since version 0.13).

[http://psi-im.org/](http://psi-im.org/) || [psi](https://www.archlinux.org/packages/?name=psi) [psimedia](https://www.archlinux.org/packages/?name=psimedia)

*   **Psi+** — Enhanced version of the Psi Jabber client with many new [features](http://psi-plus.com/wiki/en:features#differences_between_psi_beta_version_and_the_official_psi_015-dev_version).

[http://psi-plus.com/](http://psi-plus.com/) || [psi-plus-git](https://aur.archlinux.org/packages/psi-plus-git/)<sup><small>AUR</small></sup>

*   **[Tkabber](https://en.wikipedia.org/wiki/Tkabber "wikipedia:Tkabber")** — Easy to hack feature-rich XMPP client by the author of the ejabberd XMPP server.

[http://tkabber.jabber.ru/](http://tkabber.jabber.ru/) || [tkabber](https://www.archlinux.org/packages/?name=tkabber)

###### Servers

See also [Wikipedia:Comparison of XMPP server software](https://en.wikipedia.org/wiki/Comparison_of_XMPP_server_software "wikipedia:Comparison of XMPP server software").

*   **[Prosody](/index.php/Prosody "Prosody")** — An XMPP server written in the [Lua](http://www.lua.org/) programming language. Prosody is designed to be lightweight and highly extensible. It is licensed under a permissive [MIT license](http://prosody.im/source/mit).

[http://prosody.im/](http://prosody.im/) || [prosody](https://www.archlinux.org/packages/?name=prosody)

*   **Ejabberd** — Jabber server written in Erlang

[http://www.ejabberd.im/](http://www.ejabberd.im/) || [ejabberd](https://www.archlinux.org/packages/?name=ejabberd)

*   **[Jabberd2](/index.php/Jabberd2 "Jabberd2")** — An XMPP server written in the C language and licensed under the GNU General Public License. It was inspired by jabberd14.

[http://jabberd2.org](http://jabberd2.org) || [jabberd2](https://aur.archlinux.org/packages/jabberd2/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/jabberd2)]</sup>

*   **Openfire** — An XMPP IM multiplatform server written in Java

[http://www.igniterealtime.org/projects/openfire/](http://www.igniterealtime.org/projects/openfire/) || [openfire](https://www.archlinux.org/packages/?name=openfire)

##### Multi-protocol clients

See also [Wikipedia:Comparison of instant messaging clients](https://en.wikipedia.org/wiki/Comparison_of_instant_messaging_clients "wikipedia:Comparison of instant messaging clients").

**Note:** All messengers, that support several networks by means of direct connections to them, belong to this section.

Many clients listed here (including Pidgin and all its forks) support multiple IM networks via [libpurple](https://en.wikipedia.org/wiki/libpurple "wikipedia:libpurple"). The number of networks supported by these clients is very large but they (like any multiprotocol clients) usually have very limited or no support for network-specific features.

###### Console

*   **BarnOwl** — Ncurses-based chat client with support for the Zephyr, AIM, Jabber, IRC, and Twitter protocols.

[http://barnowl.mit.edu/](http://barnowl.mit.edu/) || [barnowl](https://aur.archlinux.org/packages/barnowl/)<sup><small>AUR</small></sup>

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

[https://tox.chat/](https://tox.chat/) || [tox-git](https://aur.archlinux.org/packages/tox-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tox-git)]</sup>

###### Graphical

*   **Carrier** — Pidgin fork providing minor GUI enhancements (formerly FunPidgin).

[http://funpidgin.sourceforge.net/](http://funpidgin.sourceforge.net/) || [carrier](https://aur.archlinux.org/packages/carrier/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/carrier)]</sup>

*   **[Emesene](https://en.wikipedia.org/wiki/Emesene "wikipedia:Emesene")** — PyGTK instant messenger for the Windows Live Messenger network, also compatible with Jabber, Facebook and Google Talk.

[http://emesene.org/](http://emesene.org/) || [emesene](https://aur.archlinux.org/packages/emesene/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/emesene)]</sup>

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) "wikipedia:Empathy (software)")** — GNOME instant messaging client using the [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) "wikipedia:Telepathy (software)") framework.

[https://wiki.gnome.org/Apps/Empathy](https://wiki.gnome.org/Apps/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **Galaxium Messenger** — Messenger application designed for the GNOME desktop.

[https://code.google.com/p/galaxium/](https://code.google.com/p/galaxium/) || [galaxium](https://aur.archlinux.org/packages/galaxium/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/galaxium)]</sup>

*   **[Instantbird](https://en.wikipedia.org/wiki/Instantbird "wikipedia:Instantbird")** — Multi-protocol chat client using Mozilla's XUL and libpurple.

[http://instantbird.com/](http://instantbird.com/) || [instantbird](https://aur.archlinux.org/packages/instantbird/)<sup><small>AUR</small></sup>

*   **[Kopete](https://en.wikipedia.org/wiki/Kopete "wikipedia:Kopete")** — User-friendly IM supporting AIM, ICQ, Windows Live Messenger, Yahoo, Jabber, Gadu-Gadu, Novell GroupWise Messenger, and other IM networks. Part of [kdenetwork](https://www.archlinux.org/groups/x86_64/kdenetwork/).

[http://kopete.kde.org/](http://kopete.kde.org/) || [kdenetwork-kopete](https://www.archlinux.org/packages/?name=kdenetwork-kopete)

*   **[KDE Telepathy](/index.php/KDE#KDE_Telepathy "KDE")** — KDE instant messaging client using the [Telepathy](https://en.wikipedia.org/wiki/Telepathy_(software) "wikipedia:Telepathy (software)") framework. Meant as a replacement for Kopete.

[http://community.kde.org/Real-Time_Communication_and_Collaboration/](http://community.kde.org/Real-Time_Communication_and_Collaboration/) || [telepathy-kde-meta](https://www.archlinux.org/packages/?name=telepathy-kde-meta)

*   **Licq** — Instant messaging client for UNIX supporting multiple protocols (currently ICQ, MSN and Jabber).

[http://www.licq.org](http://www.licq.org) || [licq](https://www.archlinux.org/packages/?name=licq)

*   **Mikutter** — An open-source Twitter client using [GTK+](/index.php/GTK%2B "GTK+") and Ruby.

[http://mikutter.hachune.net/](http://mikutter.hachune.net/) || [mikutter](https://aur.archlinux.org/packages/mikutter/)<sup><small>AUR</small></sup> [mikutter-git](https://aur.archlinux.org/packages/mikutter-git/)<sup><small>AUR</small></sup>

*   **[Pidgin](/index.php/Pidgin "Pidgin")** — Multi-protocol instant messaging client.

[http://pidgin.im/](http://pidgin.im/) || [pidgin](https://www.archlinux.org/packages/?name=pidgin) [pidgin-light](https://aur.archlinux.org/packages/pidgin-light/)<sup><small>AUR</small></sup>

*   **qutIM** — Simple and user-friendly IM supporting ICQ, Jabber, Mail.Ru, IRC and VKontakte messaging.

[http://qutim.org/](http://qutim.org/) || [qutim-stable](https://aur.archlinux.org/packages/qutim-stable/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qutim-stable)]</sup>

##### Lan messengers

See also: [Comparison of LAN messengers](https://en.wikipedia.org/wiki/Comparison_of_LAN_messengers "wikipedia:Comparison of LAN messengers").

*   **iptux** — Lan communication software, compatible with IP Messenger.

[https://github.com/iptux-src/iptux](https://github.com/iptux-src/iptux) || [iptux](https://aur.archlinux.org/packages/iptux/)<sup><small>AUR</small></sup>

#### VoIP / Softphone

See also [Wikipedia:Comparison of VoIP software](https://en.wikipedia.org/wiki/Comparison_of_VoIP_software "wikipedia:Comparison of VoIP software") and [Wikipedia:List of SIP software](https://en.wikipedia.org/wiki/List_of_SIP_software "wikipedia:List of SIP software").

##### Clients

**Note:** Some [IM clients](#Instant_messaging) also offer voice and video communication

###### SIP

*   **[Blink](https://en.wikipedia.org/wiki/Blink_(software) "wikipedia:Blink (software)")** — State of the art, easy to use SIP client.

[http://www.icanblink.com/](http://www.icanblink.com/) || [blink-darcs](https://aur.archlinux.org/packages/blink-darcs/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/blink-darcs)]</sup>

*   **[Ekiga](https://en.wikipedia.org/wiki/Ekiga "wikipedia:Ekiga")** — VoIP and video conferencing application with full SIP and H.323 support (formerly known as GNOME Meeting).

[http://www.ekiga.org/](http://www.ekiga.org/) || [ekiga](https://www.archlinux.org/packages/?name=ekiga)

*   **[Empathy](https://en.wikipedia.org/wiki/Empathy_(software) "wikipedia:Empathy (software)")** — GNOME instant messenger client using the Telepathy framework with SIP support (using the Sofia-SIP library).

[https://wiki.gnome.org/Apps/Empathy](https://wiki.gnome.org/Apps/Empathy) || [empathy](https://www.archlinux.org/packages/?name=empathy)

*   **[Jitsi](https://en.wikipedia.org/wiki/Jitsi "wikipedia:Jitsi")** — Audio/video SIP VoIP phone and instant messenger written in Java (formerly SIP-Communicator).

[https://jitsi.org/](https://jitsi.org/) || [jitsi](https://aur.archlinux.org/packages/jitsi/)<sup><small>AUR</small></sup>

*   **[KPhone](https://en.wikipedia.org/wiki/KPhone "wikipedia:KPhone")** — Qt SIP User Agent with voice, video and text messaging support.

[http://sourceforge.net/projects/kphone/](http://sourceforge.net/projects/kphone/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=kphone)</small>

*   **[Linphone](https://en.wikipedia.org/wiki/Linphone "wikipedia:Linphone")** — VoIP phone application that allows you to to communicate freely with people over the internet, with voice, video, and text instant messaging.

[http://www.linphone.org/](http://www.linphone.org/) || [linphone](https://www.archlinux.org/packages/?name=linphone)

*   **Minisip** — SIP User Agent with focus on security (supports TLS, end-to-end security, SRTP, MIKEY (DH, PSK, PKE)).

[http://www.minisip.org/](http://www.minisip.org/) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=minisip)</small>

*   **[QuteCom](https://en.wikipedia.org/wiki/QuteCom "wikipedia:QuteCom")** — Softphone which allows you to make free PC to PC video and voice calls, and to integrate all your IM contacts in one place (formerly Wengo Phone).

[http://trac.qutecom.org/](http://trac.qutecom.org/) || [qutecom](https://aur.archlinux.org/packages/qutecom/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qutecom)]</sup>

*   **[Twinkle](https://en.wikipedia.org/wiki/Twinkle_(software) "wikipedia:Twinkle (software)")** — Qt softphone for VoIP and IM communication using SIP.

[http://www.twinklephone.com/](http://www.twinklephone.com/) || [twinkle](https://aur.archlinux.org/packages/twinkle/)<sup><small>AUR</small></sup>

*   **[X-Lite](https://en.wikipedia.org/wiki/X-Lite "wikipedia:X-Lite")** — Proprietary freeware VoIP soft phone that uses SIP.

[http://www.counterpath.net/x-lite](http://www.counterpath.net/x-lite) || [xlite_bin](https://aur.archlinux.org/packages/xlite_bin/)<sup><small>AUR</small></sup>

*   **[Zfone](https://en.wikipedia.org/wiki/Zfone "wikipedia:Zfone")** — Softphone application for secure voice communication over the Internet (VoIP), using the ZRTP protocol.

[http://zfoneproject.com/](http://zfoneproject.com/) || [zfone](https://aur.archlinux.org/packages/zfone/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/zfone)]</sup>

###### IAX2

*   **Kiax** — Qt-based IAX/2 Softphone.

[http://www.forschung-direkt.eu/projects/kiax2/](http://www.forschung-direkt.eu/projects/kiax2/) || [kiax](https://aur.archlinux.org/packages/kiax/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/kiax)]</sup>

###### Skype

*   **[Skype](/index.php/Skype "Skype")** — Popular but proprietary application for high-quality voice communication.

[http://www.skype.com/](http://www.skype.com/) || [skype](https://www.archlinux.org/packages/?name=skype)

###### Other

*   **Hangups** — A third-party instant messaging client for Google Hangouts

[https://github.com/tdryer/hangups](https://github.com/tdryer/hangups) || [hangups-git](https://aur.archlinux.org/packages/hangups-git/)<sup><small>AUR</small></sup>

*   **[Mumble](https://en.wikipedia.org/wiki/Mumble_(software) "wikipedia:Mumble (software)")** — Voice chat application similar to TeamSpeak.

[http://mumble.sourceforge.net/](http://mumble.sourceforge.net/) || [mumble](https://www.archlinux.org/packages/?name=mumble)

*   **[TeamSpeak](/index.php/TeamSpeak "TeamSpeak")** — Proprietary VoIP application with gamers as its target audience.

[http://www.teamspeak.com/](http://www.teamspeak.com/) || [teamspeak3](https://www.archlinux.org/packages/?name=teamspeak3)

*   **Webex** — Proprietary conferencing software.

[http://www.webex.com/](http://www.webex.com/) || [webex](https://aur.archlinux.org/packages/webex/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/webex)]</sup>

###### Multi-protocol

*   **[SFLPhone](https://en.wikipedia.org/wiki/SFLphone "wikipedia:SFLphone")** — Open-source SIP/IAX2 compatible softphone with PulseAudio support.

[http://sflphone.org/](http://sflphone.org/) || [sflphone](https://aur.archlinux.org/packages/sflphone/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sflphone)]</sup>

##### Utilities

*   **Gladstone** — Educational ITU-T G.729 compliant codec with a GStreamer plugin.

[https://gitorious.org/gladstone](https://gitorious.org/gladstone) || [gladstone-drizztbsd-git](https://aur.archlinux.org/packages/gladstone-drizztbsd-git/)<sup><small>AUR</small></sup>

*   **SIPp** — Open source test tool and traffic generator for the SIP protocol.

[http://sipp.sourceforge.net/](http://sipp.sourceforge.net/) || [sipp](https://aur.archlinux.org/packages/sipp/)<sup><small>AUR</small></sup>

*   **Sipsak** — Small command-line tool for developers and administrators of SIP applications.

[http://sipsak.org/](http://sipsak.org/) || [sipsak](https://aur.archlinux.org/packages/sipsak/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/sipsak)]</sup>

#### Speech recognition

See [Speech recognition#List of speech recognition applications](/index.php/Speech_recognition#List_of_speech_recognition_applications "Speech recognition").

### News, RSS, and blogs

#### News aggregators

See also [Wikipedia:Comparison of feed aggregators](https://en.wikipedia.org/wiki/Comparison_of_feed_aggregators "wikipedia:Comparison of feed aggregators").

##### Console

*   **[Canto](https://en.wikipedia.org/wiki/Canto_(news_aggregator) "wikipedia:Canto (news aggregator)")** — Ncurses RSS aggregator.

[http://codezen.org/canto/](http://codezen.org/canto/) || [canto-next-git](https://aur.archlinux.org/packages/canto-next-git/)<sup><small>AUR</small></sup>

*   **[Gnus](https://en.wikipedia.org/wiki/Gnus "wikipedia:Gnus")** — Email, NNTP and RSS client for Emacs.

[http://gnus.org/](http://gnus.org/) || [emacs-gnus-git](https://aur.archlinux.org/packages/emacs-gnus-git/)<sup><small>AUR</small></sup>

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

*   **[BlogBridge](https://en.wikipedia.org/wiki/BlogBridge "wikipedia:BlogBridge")** — Excellent Java-based aggregator, which gives users the option to synchronize their feeds across multiple computers. Though according to the official website, project is not being supported any more.

[http://blogbridge.com](http://blogbridge.com) || [blogbridge](https://aur.archlinux.org/packages/blogbridge/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/blogbridge)]</sup>

*   **[Liferea](https://en.wikipedia.org/wiki/Liferea "wikipedia:Liferea")** — GTK+ news aggregator for online news feeds and weblogs.

[http://liferea.sourceforge.net](http://liferea.sourceforge.net) || [liferea](https://www.archlinux.org/packages/?name=liferea)

*   **RSS Guard** — Very tiny RSS and ATOM news reader developed using Qt framework.

[https://bitbucket.org/skunkos/rssguard](https://bitbucket.org/skunkos/rssguard) || [rssguard](https://aur.archlinux.org/packages/rssguard/)<sup><small>AUR</small></sup>

*   **[RSSOwl](https://en.wikipedia.org/wiki/RSSOwl "wikipedia:RSSOwl")** — Powerful aggregator for RSS and Atom feeds, written in Java using Eclipse Rich Client Platform and SWT as a widget toolkit.

[http://boreal.rssowl.org](http://boreal.rssowl.org) || [rssowl](https://aur.archlinux.org/packages/rssowl/)<sup><small>AUR</small></sup>

*   **[Thunderbird](/index.php/Thunderbird "Thunderbird")** — Email client from Mozilla which also functions as a pretty nice news aggregator.

[http://www.mozilla.org/thunderbird/](http://www.mozilla.org/thunderbird/) || [thunderbird](https://www.archlinux.org/packages/?name=thunderbird)

*   **Tickr (formerly News)** — GTK-based RSS Reader that displays feeds as a smooth scrolling line on your Desktop, as known from TV stations.

[http://newsrssticker.com/](http://newsrssticker.com/) || [tickr](https://aur.archlinux.org/packages/tickr/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tickr)]</sup>

*   **Urssus** — Cross platform GUI news aggregator.

[https://code.google.com/p/urssus/](https://code.google.com/p/urssus/) || [urssus](https://aur.archlinux.org/packages/urssus/)<sup><small>AUR</small></sup>

*   **QuiteRSS** — RSS/Atom feed reader written on Qt/С++.

[http://quiterss.org/](http://quiterss.org/) || [quiterss](https://aur.archlinux.org/packages/quiterss/)<sup><small>AUR</small></sup>

#### Podcast clients

*   **gPodder** — A podcast client and feed aggregator (GTK+ and CLI interface).

[http://gpodder.org/](http://gpodder.org/) || [gpodder3](https://aur.archlinux.org/packages/gpodder3/)<sup><small>AUR</small></sup>

*   **Greg** — A command-line podcast aggregator.

[https://github.com/manolomartinez/greg](https://github.com/manolomartinez/greg) || [greg-git](https://aur.archlinux.org/packages/greg-git/)<sup><small>AUR</small></sup>

*   **Marrie** — A simple podcast client that runs on the Command Line Interface.

[https://github.com/rafaelmartins/marrie/](https://github.com/rafaelmartins/marrie/) || [marrie-git](https://aur.archlinux.org/packages/marrie-git/)<sup><small>AUR</small></sup>

*   **PodCastXDL** — A simple podcast Downloader for the terminal.

[https://github.com/levi0x0/PodCastXDL](https://github.com/levi0x0/PodCastXDL) || [podcastxdl-git](https://aur.archlinux.org/packages/podcastxdl-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/podcastxdl-git)]</sup>

*   **Vocal** — Simple Podcast Client for the Modern Desktop (GTK+).

[https://launchpad.net/vocal](https://launchpad.net/vocal) || [vocal-bzr](https://aur.archlinux.org/packages/vocal-bzr/)<sup><small>AUR</small></sup>

#### Usenet newsreaders & newsgrabbers

Some [email clients](#Email_clients) also support NNTP. This section mainly lists NNTP-only client.

See also: [Wikipedia:List of Usenet newsreaders](https://en.wikipedia.org/wiki/List_of_Usenet_newsreaders "wikipedia:List of Usenet newsreaders"), [Wikipedia:Comparison of Usenet newsreaders](https://en.wikipedia.org/wiki/Comparison_of_Usenet_newsreaders "wikipedia:Comparison of Usenet newsreaders").

*   **lottanzb** — A _SABnzbd+_ (Usenet binary downloader) GUI front-end written in PyGTK

[http://www.lottanzb.org/](http://www.lottanzb.org/) || [lottanzb](https://aur.archlinux.org/packages/lottanzb/)<sup><small>AUR</small></sup>

*   **nn** — Alternative more user-friendly(curses-based) Usenet newsreader for UNIX.

[http://www.nndev.org/](http://www.nndev.org/) || [nn](https://aur.archlinux.org/packages/nn/)<sup><small>AUR</small></sup>

*   **[NZBGet](/index.php/NZBGet "NZBGet")** — CLI Utility to grab Usenet binary file using .nzb files.

[http://nzbget.sourceforge.net/](http://nzbget.sourceforge.net/) || [nzbget](https://www.archlinux.org/packages/?name=nzbget)

*   **[pan](https://en.wikipedia.org/wiki/Pan_(newsreader) "wikipedia:Pan (newsreader)")** — A GTK2 Usenet newsreader that's good at both text and binaries.

[http://pan.rebelbase.com/](http://pan.rebelbase.com/) || [pan](https://aur.archlinux.org/packages/pan/)<sup><small>AUR</small></sup>

*   **[slrn](https://en.wikipedia.org/wiki/slrn "wikipedia:slrn")** — An open source text-based news client.

[http://www.slrn.org/](http://www.slrn.org/) || [slrn](https://www.archlinux.org/packages/?name=slrn)

*   **[tin](https://en.wikipedia.org/wiki/Tin_(newsreader) "wikipedia:Tin (newsreader)")** — A cross-platform threaded NNTP and spool based UseNet newsreader.

[http://tin.org/](http://tin.org/) || [tin](https://aur.archlinux.org/packages/tin/)<sup><small>AUR</small></sup>

*   **trn** — A text-based Threaded Usenet newsreader.

[http://trn.sourceforge.net/](http://trn.sourceforge.net/) || [trn](https://aur.archlinux.org/packages/trn/)<sup><small>AUR</small></sup>

*   **[XPN](https://en.wikipedia.org/wiki/XPN_(newsreader) "wikipedia:XPN (newsreader)")** — A graphical newsreader use PyGTK.

[http://xpn.altervista.org/index-en.html](http://xpn.altervista.org/index-en.html) || [xpn](https://aur.archlinux.org/packages/xpn/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xpn)]</sup>

*   **xrn** — Usenet newsreader for X Window System.

[http://www.mit.edu/people/jik/software/xrn.html](http://www.mit.edu/people/jik/software/xrn.html) || [xrn](https://aur.archlinux.org/packages/xrn/)<sup><small>AUR</small></sup>

#### Blog software

See also [Wikipedia:Blog software](https://en.wikipedia.org/wiki/Blog_software "wikipedia:Blog software") and [Wikipedia:List of content management systems](https://en.wikipedia.org/wiki/List_of_content_management_systems "wikipedia:List of content management systems").

*   **[Drupal](/index.php/Drupal "Drupal")** — An open source content management platform powering millions of websites and applications. It is built, used, and supported by an active and diverse community of people around the world.

[http://drupal.org/](http://drupal.org/) || [drupal](https://www.archlinux.org/packages/?name=drupal)

*   **[Ghost](/index.php/Ghost "Ghost")** — Blogging platform written in JavaScript and distributed under the MIT License, designed to simplify the process of online publishing for individual bloggers as well as online publications.

[https://ghost.org/](https://ghost.org/) || [ghost](https://aur.archlinux.org/packages/ghost/)<sup><small>AUR</small></sup>

*   **Hexo** — A fast, simple & powerful blog framework, powered by Node.js.

[http://hexo.io](http://hexo.io) || [nodejs-hexo](https://aur.archlinux.org/packages/nodejs-hexo/)<sup><small>AUR</small></sup>

*   **[Jekyll](/index.php/Jekyll "Jekyll")** — A static blog engine, written in Ruby, which supports Markdown, textile and other formats.

[http://jekyllrb.com/](http://jekyllrb.com/) || [ruby-jekyll](https://aur.archlinux.org/packages/ruby-jekyll/)<sup><small>AUR</small></sup>

*   **Nanoblogger** — A small weblog engine written in Bash for the command line. It uses common UNIX tools such as cat, grep, and sed to create static HTML content. It is not mantained anymore.

[http://nanoblogger.sourceforge.net/](http://nanoblogger.sourceforge.net/) || [nanoblogger](https://www.archlinux.org/packages/?name=nanoblogger)

*   **Nikola** — A static site generator written in Python, with incremental rebuilds and multiple markup formats.

[https://getnikola.com/](https://getnikola.com/) || [python-nikola](https://aur.archlinux.org/packages/python-nikola/)<sup><small>AUR</small></sup>

*   **Pelican** — A static site generator, powered by Python.

[http://docs.getpelican.com/en/3.5.0/](http://docs.getpelican.com/en/3.5.0/) || [pelican](https://aur.archlinux.org/packages/pelican/)<sup><small>AUR</small></sup>

*   **[Wordpress](/index.php/Wordpress "Wordpress")** — An easy to setup and administer FLOSS content management system featuring a strong and vibrant community with thousands of plugins and themes.

[http://wordpress.org/](http://wordpress.org/) || [wordpress](https://www.archlinux.org/packages/?name=wordpress)

#### Microblogging clients

See also [Wikipedia:List of Twitter services and applications](https://en.wikipedia.org/wiki/List_of_Twitter_services_and_applications "wikipedia:List of Twitter services and applications").

*   **Birdie** — A beautiful Twitter client for GNU/Linux, currently [under active development](http://www.birdieapp.eu/2014/10/26/birdie-2-status.html).

[http://birdieapp.github.io/](http://birdieapp.github.io/) || [birdie](https://aur.archlinux.org/packages/birdie/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/birdie)]</sup>

*   **Choqok** — Microblogging client for KDE that supports Twitter.com, Pump.io, GNU social and opendesktop.org services.

[http://choqok.gnufolks.org/](http://choqok.gnufolks.org/) || [choqok](https://www.archlinux.org/packages/?name=choqok)

*   **Corebird** — Native Gtk+ Twitter client for the Linux desktop.

[http://corebird.baedert.org/](http://corebird.baedert.org/) || [corebird-git](https://aur.archlinux.org/packages/corebird-git/)<sup><small>AUR</small></sup>

*   **[Gwibber](https://en.wikipedia.org/wiki/Gwibber "wikipedia:Gwibber")** — GTK-based microblogging client with support for Facebook, Identi.ca, Twitter, Flickr, Foursquare, Sina and Sohu.

[http://gwibber.com/](http://gwibber.com/) || [gwibber](https://aur.archlinux.org/packages/gwibber/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/gwibber)]</sup>

*   **[Hotot](https://en.wikipedia.org/wiki/Hotot_(program) "wikipedia:Hotot (program)")** — Lightweight and open source microblogging client with support for Twitter and Identi.ca and integration with various image sharing services and URL shorteners [(discontinued)](http://hotot.org/).

[http://hotot.org](http://hotot.org) || [hotot](https://aur.archlinux.org/packages/hotot/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/hotot)]</sup>

*   **Pino** — Simple and fast client for Twitter and Identi.ca written in [Vala](https://en.wikipedia.org/wiki/Vala_(programming_language) "wikipedia:Vala (programming language)").

[http://pino-app.appspot.com/](http://pino-app.appspot.com/) || [pino](https://aur.archlinux.org/packages/pino/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/pino)]</sup>

*   **Polly** — Linux Twitter client designed for multiple columns of multiple accounts.

[https://launchpad.net/polly/](https://launchpad.net/polly/) || [polly](https://aur.archlinux.org/packages/polly/)<sup><small>AUR</small></sup>

*   **Pumpa** — Pump.io client written in C++ and Qt.

[https://pumpa.branchable.com/](https://pumpa.branchable.com/) || [pumpa-git](https://aur.archlinux.org/packages/pumpa-git/)<sup><small>AUR</small></sup>

*   **Qwit** — Cross-platform client for Twitter using the Qt toolkit.

[http://code.google.com/p/qwit/](http://code.google.com/p/qwit/) || [qwit](https://aur.archlinux.org/packages/qwit/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/qwit)]</sup>

*   **ttytter** — Easily scriptable twitter client written in Perl.

[http://www.floodgap.com/software/ttytter/](http://www.floodgap.com/software/ttytter/) || [ttytter](https://www.archlinux.org/packages/?name=ttytter)

*   **Turpial** — Multi-interface Twitter client written in Python.

[http://turpial.org.ve/](http://turpial.org.ve/) || [turpial-git](https://aur.archlinux.org/packages/turpial-git/)<sup><small>AUR</small></sup>

*   **turses** — Twitter client for the console based off [tyrs](https://aur.archlinux.org/packages/tyrs/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tyrs)]</sup> with major improvements.

[http://turses.rtfd.org/](http://turses.rtfd.org/) || [turses](https://aur.archlinux.org/packages/turses/)<sup><small>AUR</small></sup>

### Pastebin clients

See also [Wikipedia:Pastebin](https://en.wikipedia.org/wiki/Pastebin "wikipedia:Pastebin").

Pastebin services are often used to quote text or images while collaborating and troubleshooting. Pastebin clients provide a convenient way to post from the command line.

**Tip:** You can access the [ptpb.pw](https://ptpb.pw), [sprunge.us](http://sprunge.us/) and [ix.io](http://ix.io/) pastebins using curl. For example pipe the output of a command to ptpb: `_command_ | curl -F c=@- https://ptpb.pw ` or upload a file (including images): `curl -F c=@- https://ptpb.pw < _file_` 

**Note:** [pastebin.com](http://pastebin.com/) is blocked for some people and has a history of annoying issues (javascript, adverts, poor formatting, etc).

*   **codepad-git** — A codepad.org pastebin client written in python.

[http://www.codepad.org](http://www.codepad.org) || [codepad-git](https://aur.archlinux.org/packages/codepad-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/codepad-git)]</sup>

*   **Elmer** — Pastebin client similar to wgetpaste and curlpaste, except written in Perl and usable with wget or curl. Servers: [codepad.org](http://codepad.org/), [rafb.me](http://rafb.me/), [sprunge.us](http://sprunge.us/).

[https://github.com/sudokode/elmer](https://github.com/sudokode/elmer) || [elmer](https://aur.archlinux.org/packages/elmer/)<sup><small>AUR</small></sup>

*   **Fb-client** — Client for the [paste.xinu.at](http://paste.xinu.at/) pastebin.

[http://paste.xinu.at](http://paste.xinu.at) || [fb-client](https://www.archlinux.org/packages/?name=fb-client)

*   **Gist** — Command-line interface for the [gist.github.com](https://gist.github.com/) pastebin service.

[http://github.com/defunkt/gist](http://github.com/defunkt/gist) || [gist](https://www.archlinux.org/packages/?name=gist)

*   **Haste** — Universal pastebin tool, written in Haskell. Servers: [hpaste.org](http://hpaste.org/), [paste2.org](http://paste2.org/), [pastebin.com](http://pastebin.com/) and others.

[http://hackage.haskell.org/package/haste](http://hackage.haskell.org/package/haste) || [haste](https://aur.archlinux.org/packages/haste/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/haste)]</sup>

*   **Hg-paste** — Pastebin extension for Mercurial which can send diffs to various pastebin websites for easy sharing. Servers: [dpaste.com](http://dpaste.com/) and [dpaste.org](http://dpaste.org/).

[http://bitbucket.org/sjl/hg-paste](http://bitbucket.org/sjl/hg-paste) || [hg-paste](https://aur.archlinux.org/packages/hg-paste/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/hg-paste)]</sup>

*   **imgur** — A CLI client which can upload image to [imgur.com](http://imgur.com) image sharing service.

[http://imgur.com/apps](http://imgur.com/apps) || [imgur](https://aur.archlinux.org/packages/imgur/)<sup><small>AUR</small></sup>

*   **Ix** — Client for the ix.io pastebin.

[http://ix.io](http://ix.io) || [ix](https://aur.archlinux.org/packages/ix/)<sup><small>AUR</small></sup>

*   **Npaste-client** — Client for the [npaste.de](http://npaste.de/) pastebin.

[http://npaste.de](http://npaste.de) || [npaste-client](https://aur.archlinux.org/packages/npaste-client/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/npaste-client)]</sup>

*   **Pastebinit** — Really small Python script that acts as a Pastebin client. Servers: [pastie.org](http://pastie.org/), [paste.kde.org](http://paste.kde.org/), [paste.debian.net](http://paste.debian.net/), [paste.ubuntu.com](http://paste.ubuntu.com/) and others (for a full list see `pastebinit -l`).

[http://launchpad.net/pastebinit](http://launchpad.net/pastebinit) || [pastebinit](https://www.archlinux.org/packages/?name=pastebinit)

*   **paste-binouse** — C++ standalone pastebin web server

[https://github.com/abique/paste-binouse](https://github.com/abique/paste-binouse) || [paste-binouse](https://aur.archlinux.org/packages/paste-binouse/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/paste-binouse)]</sup>

*   **pb** — A very fast, lightweight pastebin and general file uploader written in python with a ton of features.

[https://ptpb.pw](https://ptpb.pw) || [ptpb](https://aur.archlinux.org/packages/ptpb/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ptpb)]</sup>

*   **ruby-haste** — Client for [hastebin.com](http://hastebin.com/).

[https://github.com/seejohnrun/haste-client](https://github.com/seejohnrun/haste-client) || [ruby-haste](https://aur.archlinux.org/packages/ruby-haste/)<sup><small>AUR</small></sup> [ruby-haste-git](https://aur.archlinux.org/packages/ruby-haste-git/)<sup><small>AUR</small></sup>

*   **Uppity** — The pastebin client with an attitude.

[https://github.com/Kiwi/Uppity](https://github.com/Kiwi/Uppity) || [uppity-git](https://aur.archlinux.org/packages/uppity-git/)<sup><small>AUR</small></sup>

*   **Vim-gist** — Vim script for [gist.github.com](https://gist.github.com/).

[http://www.vim.org/scripts/script.php?script_id=2423](http://www.vim.org/scripts/script.php?script_id=2423) || [vim-gist](https://aur.archlinux.org/packages/vim-gist/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/vim-gist)]</sup>

*   **Vim-paster** — Vim plugin to paste to any pastebin service using curl.

[http://eugeneciurana.com/site.php?page=tools](http://eugeneciurana.com/site.php?page=tools) || [vim-paster](https://aur.archlinux.org/packages/vim-paster/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/vim-paster)]</sup>

*   **Wgetpaste** — Bash script that automates pasting to a number of pastebin services. Servers: [pastebin.ca](http://pastebin.ca/), [codepad.org](http://codepad.org/), [dpaste.com](http://dpaste.com/) and [pastebin.osuosl.org](http://pastebin.osuosl.org/).

[http://wgetpaste.zlin.dk/](http://wgetpaste.zlin.dk/) || [wgetpaste](https://www.archlinux.org/packages/?name=wgetpaste)

### Bitcoin

See the main article: [Bitcoin](/index.php/Bitcoin "Bitcoin").

*   **Armory** — Bitcoin client with features such as support for multiple wallets, importing keys and backups.

[https://github.com/etotheipi/BitcoinArmory](https://github.com/etotheipi/BitcoinArmory) || [armory-git](https://aur.archlinux.org/packages/armory-git/)<sup><small>AUR</small></sup>

*   **[Bitcoin](/index.php/Bitcoin "Bitcoin")** — Official tool to manage Bitcoins, a P2P currency.

[http://bitcoin.org/](http://bitcoin.org/) || [bitcoin-daemon](https://www.archlinux.org/packages/?name=bitcoin-daemon) [bitcoin-qt](https://www.archlinux.org/packages/?name=bitcoin-qt)

*   **Electrum** — An easy to use Bitcoin client.

[http://electrum.org/](http://electrum.org/) || [electrum](https://www.archlinux.org/packages/?name=electrum)

*   **MultiBit** — A lightweight Bitcoin desktop client powered by the BitCoinJ library.

[https://multibit.org/](https://multibit.org/) || [multibit](https://www.archlinux.org/packages/?name=multibit)

### Surveying

*   **[LimeSurvey](https://en.wikipedia.org/wiki/LimeSurvey "wikipedia:LimeSurvey")** — An open source on-line survey application. As a web server-based software it enables users to develop and publish on-line surveys, and collect responses, with no programming.

[https://www.limesurvey.org/](https://www.limesurvey.org/) || [limesurvey](https://aur.archlinux.org/packages/limesurvey/)<sup><small>AUR</small></sup>

Retrieved from "[https://wiki.archlinux.org/index.php?title=List_of_applications/Internet&oldid=414482](https://wiki.archlinux.org/index.php?title=List_of_applications/Internet&oldid=414482)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Internet applications](/index.php/Category:Internet_applications "Category:Internet applications")