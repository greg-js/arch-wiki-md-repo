# Amateur radio

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [GNU Radio](/index.php/GNU_Radio "GNU Radio")
*   [RTL-SDR](/index.php/RTL-SDR "RTL-SDR")

Amateur radio enthusiasts (sometimes called ham radio operators or "hams") have been at the forefront of experimentation and development since the earliest days of radio. A wide variety of communication modes are used on a vast range of frequencies that span the electromagnetic spectrum. This page lists software related to amateur radio that can be found in the [AUR](/index.php/AUR "AUR"). Some of it is stand-alone while the various digital communication applications require interfacing to radio hardware and possibly the computer soundcard. Interface hardware can be purchased from vendors or home-built.

**Warning:** International treaties require that users of amateur radio frequencies have a government-issued license. This only affects you if you have a transmitter and an antenna, receiving amateur radio or just downloading amateur radio software isn't illegal.

## Contents

*   [1 General information](#General_information)
*   [2 Software list](#Software_list)
    *   [2.1 AX.25](#AX.25)
    *   [2.2 WSJT](#WSJT)
    *   [2.3 WSPR](#WSPR)
    *   [2.4 Xastir](#Xastir)
    *   [2.5 Digital Voice](#Digital_Voice)
    *   [2.6 Analysis tools](#Analysis_tools)
    *   [2.7 Logging](#Logging)
    *   [2.8 Tools](#Tools)
    *   [2.9 Morse code training](#Morse_code_training)
    *   [2.10 Other](#Other)

## General information

Many of the following programs will need to access a serial port to key the transmitter (eg. /dev/ttyS0). This requires that the user belong to the uucp group. To add the user to the uucp group issue the following command as root:

```
# gpasswd -a _username_ uucp

```

then logoff and logon.

## Software list

*   **Hamlib** — provides an interface between hardware and radio control programs. It is a software layer to facilitate the control of radios and other hardware (eg. for logging, digital modes) and is not a stand-alone application.

[http://sourceforge.net/apps/mediawiki/hamlib/](http://sourceforge.net/apps/mediawiki/hamlib/) || [hamlib](https://aur.archlinux.org/packages/hamlib/)<sup><small>AUR</small></sup>

*   **Soundmodem** — was written by Tom Sailer (HB9JNX/AE4WA) to allow a standard PC soundcard to act as a packet radio modem for use with the various AX.25 communication modes. The data rate can be as high as 9600 baud depending on the hardware and application. Soundmodem can be used as a KISS modem on the serial port or as an AX.25 network device. To use soundmodem as an MKISS network device, the kernel must be re-built with MKISS modules. More information is in the [Xastir wiki](http://www.xastir.org/wiki/index.php/HowTo:SoundModem)

Run soundmodem as root:

 `# soundmodem` 

If you have configured soundmodem as a KISS modem, you will need to change permissions to make it user-readable:

 `# chmod 666 /dev/soundmodem0` 

[http://www.baycom.org/~tom/ham/soundmodem/](http://www.baycom.org/~tom/ham/soundmodem/) || [soundmodem](https://aur.archlinux.org/packages/soundmodem/)<sup><small>AUR</small></sup>

*   **Grig** — simple control program based on Hamlib

[http://groundstation.sourceforge.net/grig/](http://groundstation.sourceforge.net/grig/) || [grig](https://aur.archlinux.org/packages/grig/)<sup><small>AUR</small></sup>

*   **gMFSK** — is a user interface that supports a multitude of digital modes. It uses hamlib and xlog for logging

[http://gmfsk.connect.fi](http://gmfsk.connect.fi) || [gmfsk](https://aur.archlinux.org/packages/gmfsk/)<sup><small>AUR</small></sup>

*   **lysdr** — highly customizable radio interface

[https://github.com/gordonjcp/lysdr](https://github.com/gordonjcp/lysdr) || [lysdr-git](https://aur.archlinux.org/packages/lysdr-git/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/lysdr-git)]</sup>

*   **linrad** — Software defined radio by SM5BSZ

[http://www.sm5bsz.com/linuxdsp/linrad.htm](http://www.sm5bsz.com/linuxdsp/linrad.htm) || [linrad](https://aur.archlinux.org/packages/linrad/)<sup><small>AUR</small></sup>

*   **quisk** — Software defined radio by N2ADR

[http://james.ahlstrom.name/quisk/](http://james.ahlstrom.name/quisk/) || [quisk](https://aur.archlinux.org/packages/quisk/)<sup><small>AUR</small></sup>

*   **[owx](/index.php/Owx "Owx")** — command-line utility for programming Wouxun radios

[http://owx.chmurka.net](http://owx.chmurka.net) || [owx](https://aur.archlinux.org/packages/owx/)<sup><small>AUR</small></sup>

*   **twcw** — extension for cwirc

[http://wa0eir.home.mchsi.com/twcw.html](http://wa0eir.home.mchsi.com/twcw.html) || <small>not packaged? [search in AUR](https://aur.archlinux.org/packages/?K=twcw)</small>

*   **fldigi** — popular GUI developed by W1HKJ for a variety of digital communication modes

[http://w1hkj.com/Fldigi.html](http://w1hkj.com/Fldigi.html) || [fldigi](https://aur.archlinux.org/packages/fldigi/)<sup><small>AUR</small></sup>

*   **libfap** — APRS packet parser

[http://pakettiradio.net/libfap/](http://pakettiradio.net/libfap/) || [libfap](https://aur.archlinux.org/packages/libfap/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/libfap)]</sup>

*   **aprx** — lightweight APRS digipeater and i-Gate interface

[http://wiki.ham.fi/Aprx.en](http://wiki.ham.fi/Aprx.en) || [aprx-svn](https://aur.archlinux.org/packages/aprx-svn/)<sup><small>AUR</small></sup>

*   **xdx** — network client

[http://www.qsl.net/pg4i/linux/xdx.html](http://www.qsl.net/pg4i/linux/xdx.html) || [xdx](https://aur.archlinux.org/packages/xdx/)<sup><small>AUR</small></sup>

*   [d-rats](https://aur.archlinux.org/packages/d-rats/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/d-rats)]</sup> – D-STAR communication tool
*   [qsstv](https://aur.archlinux.org/packages/qsstv/)<sup><small>AUR</small></sup> – Slow-scan television
*   [linpsk](https://aur.archlinux.org/packages/linpsk/)<sup><small>AUR</small></sup> – PSK31
*   [psk31lx](https://aur.archlinux.org/packages/psk31lx/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/psk31lx)]</sup> – PSK31 using Pulseaudio
*   [twpsk](https://aur.archlinux.org/packages/twpsk/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/twpsk)]</sup> – Soundcard based program for PSK31
*   [xpsk31](https://aur.archlinux.org/packages/xpsk31/)<sup><small>AUR</small></sup> – PSK31 using a GUI rendered by GTK+

### AX.25

**[AX.25](https://en.wikipedia.org/wiki/AX.25 "wikipedia:AX.25")** — data link layer protocol that is used extensively in packet radio networks. It supports connected operation (eg. keyboard-to-keyboard contacts, access to local bulletin board systems, and DX clusters) as well as connectionless operation (eg. [APRS](https://en.wikipedia.org/wiki/APRS "wikipedia:APRS")). The Linux kernel includes native support for AX.25 networking. Please refer to this [guide](http://tldp.org/HOWTO/AX25-HOWTO/) for more information. The following software is available in the AUR:

*   [ax25-apps](https://aur.archlinux.org/packages/ax25-apps/)<sup><small>AUR</small></sup>
*   [ax25-tools](https://aur.archlinux.org/packages/ax25-tools/)<sup><small>AUR</small></sup>
*   [libax25](https://aur.archlinux.org/packages/libax25/)<sup><small>AUR</small></sup>
*   [node](https://aur.archlinux.org/packages/node/)<sup><small>AUR</small></sup>

[http://www.ax25.net/](http://www.ax25.net/) || present in stock kernel

### WSJT

**[WSJT](https://en.wikipedia.org/wiki/WSJT_(Amateur_radio_software) "wikipedia:WSJT (Amateur radio software)") (Weak Signal Communication by K1JT)** — offers offers a rich variety of features, including specific digital protocols optimized for meteor scatter, ionospheric scatter, and EME (moonbounce) at VHF/UHF, as well as HF skywave propagation. WSJT was developed by Nobel Prize winning physicist Joe Taylor, who has the amateur radio callsign K1JT. The program can decode fraction-of-a-second signals reflected from ionized meteor trails and steady signals 10 dB below the audible threshold.  
WSJT is in ongoing, active development by a team of programmers led by K1JT. WSJT (and the related program WSPR) has the option of being configured with

 `$ ./configure --enable-g95` 

or

 `$ ./configure --enable-gfortran` 

If you build with one and experience problems, edit PKGBUILD to try the other.  
WSJT requires access to the serial port; see the note in the Interfacing section above about the uucp group.

[http://www.physics.princeton.edu/pulsar/K1JT/](http://www.physics.princeton.edu/pulsar/K1JT/) || [wsjt-svn](https://aur.archlinux.org/packages/wsjt-svn/)<sup><small>AUR</small></sup>

### WSPR

**[WSPR](https://en.wikipedia.org/wiki/WSPR_(amateur_radio_software) "wikipedia:WSPR (amateur radio software)") (Weak Signal Propagation Reporter, pronounced whisper)** — enables the probing of propagation paths on the amateur radio bands using low power transmissions. It was introduced in 2008 by K1JT following the success and widespread adoption of WSJT by the amateur radio community. Stations with Internet access can automatically upload their reception reports to a central database called [WSPRnet](http://wsprnet.org/drupal/), which includes a [mapping facility](http://wsprnet.org/drupal/wsprnet/map)

[http://physics.princeton.edu/pulsar/K1JT/wspr.html](http://physics.princeton.edu/pulsar/K1JT/wspr.html) || [wspr-svn](https://aur.archlinux.org/packages/wspr-svn/)<sup><small>AUR</small></sup>

### Xastir

**Xastir** — stands for X Amateur Station and Information Reporting. It works with [APRS](https://en.wikipedia.org/wiki/APRS "wikipedia:APRS"), an amateur radio-based system for real time tactical digital communications. Xastir is an open-source program that provides full-featured, client-side access to APRS. It is currently in a state of active development.  
Xastir is highly flexible and there are a wide variety of ways it can be configured. For example, it can be evaluated without radio hardware if an Internet connection is available. The wiki at xastir.org is very thorough and gives excellent information on its range of capabilities and setup.  
An optional speech feature can be enabled with the [festival](https://www.archlinux.org/packages/?name=festival) package; you will also need a speaker package such as festival-en or festival-english. If you want this option, festival must be installed on your system before building xastir. Launch festival before the xastir program is started for speech to function properly:

 `$ festival --server` 

or you can write a simple script to automate the sequential starting process. There may be problems if other programs such as a media player are accessing sound simultaneously.  
The PKGBUILD automatically downloads an 850 kB bundle of .wav files and places them here: `/usr/share/xastir/sounds/`.  
These are audio alarm recordings of a North American English speaker that do not require the presence of festival to render. The audio play command `play' in the configure menu may not work; try `aplay' instead.

[http://www.xastir.org](http://www.xastir.org) || [xastir](https://aur.archlinux.org/packages/xastir/)<sup><small>AUR</small></sup>

### Digital Voice

**FreeDV** — is a Digital Voice mode for HF radio. It uses the free and open Codec2 voice codec to enable efficient narrow bandwith, low bitrate voice communication ideally suited for shortwave radio contacts. A SSB radio connected to a computer running the FreeDV GUI application are all that is needed to start using the FreeDV mode. FreeDV as well as Codec2 are available to Arch Linux via the AUR system. Both are needed for FreeDV to work!

*   [http://www.rowetel.com/codec2.html](http://www.rowetel.com/codec2.html) [codec2](https://aur.archlinux.org/packages/codec2/)<sup><small>AUR</small></sup>

[http://freedv.org](http://freedv.org) || [freedv](https://aur.archlinux.org/packages/freedv/)<sup><small>AUR</small></sup>

### Analysis tools

*   [fl_moxgen](https://aur.archlinux.org/packages/fl_moxgen/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/fl_moxgen)]</sup> – Moxon antenna designer
*   [geoid](https://aur.archlinux.org/packages/geoid/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/geoid)]</sup> – Geodetic calculator
*   [gpredict](https://aur.archlinux.org/packages/gpredict/)<sup><small>AUR</small></sup> – Real-time satellite tracking and orbit prediction application
*   [hamsolar](https://aur.archlinux.org/packages/hamsolar/)<sup><small>AUR</small></sup> – Small desktop display of the current solar indices
*   [splat](https://aur.archlinux.org/packages/splat/)<sup><small>AUR</small></sup> – rf signal propagation, loss, and terrain analysis
*   [sunclock](https://aur.archlinux.org/packages/sunclock/)<sup><small>AUR</small></sup> – Useful for predicting grayline propagation paths
*   [xnec2c](https://aur.archlinux.org/packages/xnec2c/)<sup><small>AUR</small></sup> – Electromagnetic antenna modeler

### Logging

*   [cqrlog](https://aur.archlinux.org/packages/cqrlog/)<sup><small>AUR</small></sup> – a popular Linux logging program
*   [fdlog](https://aur.archlinux.org/packages/fdlog/)<sup><small>AUR</small></sup> – a Field Day Logger with networked nodes
*   [klog](https://aur.archlinux.org/packages/klog/)<sup><small>AUR</small></sup> – a Ham radio logging program for Linux / KDE.
*   [qle](https://aur.archlinux.org/packages/qle/)<sup><small>AUR</small></sup> – QSO Logger and log Editor for amateur radio operators written in Perl
*   [tlf](https://aur.archlinux.org/packages/tlf/)<sup><small>AUR</small></sup> – a console mode networked logging and contest program
*   [trustedqsl](https://aur.archlinux.org/packages/trustedqsl/)<sup><small>AUR</small></sup> – QSL application for ARRL's Logbook of the World
*   [tucnak2](https://aur.archlinux.org/packages/tucnak2/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tucnak2)]</sup> – a multiplatform VHF/HF contest logbook
*   [xlog](https://aur.archlinux.org/packages/xlog/)<sup><small>AUR</small></sup> – a logging program for amateur radio operators.
*   [yfklog](https://aur.archlinux.org/packages/yfklog/)<sup><small>AUR</small></sup> – a general purpose ham radio logbook for *nix operating systems.
*   [yfktest](https://aur.archlinux.org/packages/yfktest/)<sup><small>AUR</small></sup> – a logbook program for ham radio contests.

### Tools

*   [callsign](https://aur.archlinux.org/packages/callsign/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/callsign)]</sup> – a small program for finding information about a ham radio based on his callsign
*   [cty](https://aur.archlinux.org/packages/cty/)<sup><small>AUR</small></sup> – package contains databases of entities (countries), prefixes and callsigns that are used by amateur radio logging software.
*   [dxcc](https://aur.archlinux.org/packages/dxcc/)<sup><small>AUR</small></sup> – a small program for determining ARRL DXCC entity of a ham radio callsign
*   [nato](https://aur.archlinux.org/packages/nato/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/nato)]</sup> – Python script to convert string into NATO alphabet representation
*   [tqsllib](https://aur.archlinux.org/packages/tqsllib/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/tqsllib)]</sup> – Trusted QSL library (supports ARRL Logbook of the World)

### Morse code training

*   [aldo](https://aur.archlinux.org/packages/aldo/)<sup><small>AUR</small></sup>
*   [cutecw](https://aur.archlinux.org/packages/cutecw/)<sup><small>AUR</small></sup>
*   [ebook2cw](https://aur.archlinux.org/packages/ebook2cw/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/ebook2cw)]</sup>
*   [gtkmmorse](https://aur.archlinux.org/packages/gtkmmorse/)<sup><small>AUR</small></sup>
*   [kochmorse](https://aur.archlinux.org/packages/kochmorse/)<sup><small>AUR</small></sup>
*   [qrq](https://aur.archlinux.org/packages/qrq/)<sup><small>AUR</small></sup>
*   [unixcw](https://aur.archlinux.org/packages/unixcw/)<sup><small>AUR</small></sup>

### Other

*   [cwirc](https://aur.archlinux.org/packages/cwirc/)<sup><small>AUR</small></sup> – Send and receive Morse code messages via IRC

Retrieved from "[https://wiki.archlinux.org/index.php?title=Amateur_radio&oldid=404340](https://wiki.archlinux.org/index.php?title=Amateur_radio&oldid=404340)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Telephony and voice](/index.php/Category:Telephony_and_voice "Category:Telephony and voice")