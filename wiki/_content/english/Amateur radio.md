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
# gpasswd -a *username* uucp

```

then logoff and logon.

## Software list

*   **Hamlib** — provides an interface between hardware and radio control programs. It is a software layer to facilitate the control of radios and other hardware (eg. for logging, digital modes) and is not a stand-alone application.

	[https://sourceforge.net/projects/hamlib/](https://sourceforge.net/projects/hamlib/) || [hamlib](https://aur.archlinux.org/packages/hamlib/)

*   **Soundmodem** — was written by Tom Sailer (HB9JNX/AE4WA) to allow a standard PC soundcard to act as a packet radio modem for use with the various AX.25 communication modes. The data rate can be as high as 9600 baud depending on the hardware and application. Soundmodem can be used as a KISS modem on the serial port or as an AX.25 network device. To use soundmodem as an MKISS network device, the kernel must be re-built with MKISS modules. More information is in the [Xastir wiki](http://www.xastir.org/wiki/index.php/HowTo:SoundModem)

	Run soundmodem as root:

	 `# soundmodem` 

	If you have configured soundmodem as a KISS modem, you will need to change permissions to make it user-readable:

	 `# chmod 666 /dev/soundmodem0` 

	[http://www.baycom.org/~tom/ham/soundmodem/](http://www.baycom.org/~tom/ham/soundmodem/) || [soundmodem](https://aur.archlinux.org/packages/soundmodem/)

*   **Grig** — simple control program based on Hamlib

	[http://groundstation.sourceforge.net/grig/](http://groundstation.sourceforge.net/grig/) || [grig](https://aur.archlinux.org/packages/grig/)

*   **gMFSK** — is a user interface that supports a multitude of digital modes. It uses hamlib and xlog for logging

	[http://gmfsk.connect.fi](http://gmfsk.connect.fi) || [gmfsk](https://aur.archlinux.org/packages/gmfsk/)

*   **lysdr** — highly customizable radio interface

	[https://github.com/gordonjcp/lysdr](https://github.com/gordonjcp/lysdr) || [lysdr-git](https://aur.archlinux.org/packages/lysdr-git/)

*   **linrad** — Software defined radio by SM5BSZ

	[http://www.sm5bsz.com/linuxdsp/linrad.htm](http://www.sm5bsz.com/linuxdsp/linrad.htm) || [linrad](https://aur.archlinux.org/packages/linrad/)

*   **quisk** — Software defined radio by N2ADR

	[http://james.ahlstrom.name/quisk/](http://james.ahlstrom.name/quisk/) || [quisk](https://aur.archlinux.org/packages/quisk/)

*   **[owx](/index.php/Owx "Owx")** — command-line utility for programming Wouxun radios

	[http://owx.chmurka.net](http://owx.chmurka.net) || [owx](https://aur.archlinux.org/packages/owx/)

*   **fldigi** — popular GUI developed by W1HKJ for a variety of digital communication modes

	[http://w1hkj.com/Fldigi.html](http://w1hkj.com/Fldigi.html) || [fldigi](https://aur.archlinux.org/packages/fldigi/)

*   **libfap** — APRS packet parser

	[http://pakettiradio.net/libfap/](http://pakettiradio.net/libfap/) || [libfap](https://aur.archlinux.org/packages/libfap/)

*   **aprx** — lightweight APRS digipeater and i-Gate interface

	[http://wiki.ham.fi/Aprx.en](http://wiki.ham.fi/Aprx.en) || [aprx-svn](https://aur.archlinux.org/packages/aprx-svn/)

*   **xdx** — network client

	[http://www.qsl.net/pg4i/linux/xdx.html](http://www.qsl.net/pg4i/linux/xdx.html) || [xdx](https://aur.archlinux.org/packages/xdx/)

*   **qsstv** — Slow-scan television

	|| [qsstv](https://aur.archlinux.org/packages/qsstv/)

*   **linpsk** — PSK31

	|| [linpsk](https://aur.archlinux.org/packages/linpsk/)

*   **psk31lx** — PSK31 using Pulseaudio

	[http://wa0eir.bcts.info/](http://wa0eir.bcts.info/) || [psk31lx](https://aur.archlinux.org/packages/psk31lx/)

*   **twpsk** — Soundcard based program for PSK31

	[http://wa0eir.bcts.info/](http://wa0eir.bcts.info/) || [twpsk](https://aur.archlinux.org/packages/twpsk/)

*   **xpsk31** — PSK31 using a GUI rendered by GTK+

	[http://www.qsl.net/5b4az/pkg/psk31/xpsk31/xpsk31.html](http://www.qsl.net/5b4az/pkg/psk31/xpsk31/xpsk31.html) || [xpsk31](https://aur.archlinux.org/packages/xpsk31/)

### AX.25

**[AX.25](https://en.wikipedia.org/wiki/AX.25 "wikipedia:AX.25")** — data link layer protocol that is used extensively in packet radio networks. It supports connected operation (eg. keyboard-to-keyboard contacts, access to local bulletin board systems, and DX clusters) as well as connectionless operation (eg. [APRS](https://en.wikipedia.org/wiki/APRS "wikipedia:APRS")). The Linux kernel includes native support for AX.25 networking. Please refer to this [guide](http://tldp.org/HOWTO/AX25-HOWTO/) for more information. The following software is available in the AUR:

*   [ax25-apps](https://aur.archlinux.org/packages/ax25-apps/)
*   [ax25-tools](https://aur.archlinux.org/packages/ax25-tools/)
*   [libax25](https://aur.archlinux.org/packages/libax25/)
*   [node](https://aur.archlinux.org/packages/node/)

	[http://www.ax25.net/](http://www.ax25.net/) || present in stock kernel

### WSJT

**[WSJT](https://en.wikipedia.org/wiki/WSJT_(Amateur_radio_software) (Weak Signal Communication by K1JT)** — offers offers a rich variety of features, including specific digital protocols optimized for meteor scatter, ionospheric scatter, and EME (moonbounce) at VHF/UHF, as well as HF skywave propagation. WSJT was developed by Nobel Prize winning physicist Joe Taylor, who has the amateur radio callsign K1JT. The program can decode fraction-of-a-second signals reflected from ionized meteor trails and steady signals 10 dB below the audible threshold.
WSJT is in ongoing, active development by a team of programmers led by K1JT. WSJT (and the related program WSPR) has the option of being configured with

 `$ ./configure --enable-g95` 

or

 `$ ./configure --enable-gfortran` 

If you build with one and experience problems, edit PKGBUILD to try the other.
WSJT requires access to the serial port; see the note in the Interfacing section above about the uucp group.

	[http://www.physics.princeton.edu/pulsar/K1JT/](http://www.physics.princeton.edu/pulsar/K1JT/) || [wsjt-svn](https://aur.archlinux.org/packages/wsjt-svn/)

### WSPR

**[WSPR](https://en.wikipedia.org/wiki/WSPR_(amateur_radio_software) (Weak Signal Propagation Reporter, pronounced whisper)** — enables the probing of propagation paths on the amateur radio bands using low power transmissions. It was introduced in 2008 by K1JT following the success and widespread adoption of WSJT by the amateur radio community. Stations with Internet access can automatically upload their reception reports to a central database called [WSPRnet](http://wsprnet.org/drupal/), which includes a [mapping facility](http://wsprnet.org/drupal/wsprnet/map)

	[http://physics.princeton.edu/pulsar/K1JT/wspr.html](http://physics.princeton.edu/pulsar/K1JT/wspr.html) || [wspr-svn](https://aur.archlinux.org/packages/wspr-svn/)

### Xastir

**Xastir** — stands for X Amateur Station and Information Reporting. It works with [APRS](https://en.wikipedia.org/wiki/APRS "wikipedia:APRS"), an amateur radio-based system for real time tactical digital communications. Xastir is an open-source program that provides full-featured, client-side access to APRS. It is currently in a state of active development.
Xastir is highly flexible and there are a wide variety of ways it can be configured. For example, it can be evaluated without radio hardware if an Internet connection is available. The wiki at xastir.org is very thorough and gives excellent information on its range of capabilities and setup.
An optional speech feature can be enabled with the [festival](https://www.archlinux.org/packages/?name=festival) package; you will also need a speaker package such as festival-en or festival-english. If you want this option, festival must be installed on your system before building xastir. Launch festival before the xastir program is started for speech to function properly:

 `$ festival --server` 

or you can write a simple script to automate the sequential starting process. There may be problems if other programs such as a media player are accessing sound simultaneously.
The PKGBUILD automatically downloads an 850 kB bundle of .wav files and places them here: `/usr/share/xastir/sounds/`.
These are audio alarm recordings of a North American English speaker that do not require the presence of festival to render. The audio play command `play' in the configure menu may not work; try `aplay' instead.

	[http://www.xastir.org](http://www.xastir.org) || [xastir](https://aur.archlinux.org/packages/xastir/)

### Digital Voice

**FreeDV** — is a Digital Voice mode for HF radio. It uses the free and open Codec2 voice codec to enable efficient narrow bandwith, low bitrate voice communication ideally suited for shortwave radio contacts. A SSB radio connected to a computer running the FreeDV GUI application are all that is needed to start using the FreeDV mode. FreeDV as well as Codec2 are available to Arch Linux via the AUR system. Both are needed for FreeDV to work!

*   [http://www.rowetel.com/codec2.html](http://www.rowetel.com/codec2.html) [codec2](https://aur.archlinux.org/packages/codec2/)

	[http://freedv.org](http://freedv.org) || [freedv](https://aur.archlinux.org/packages/freedv/)

### Analysis tools

*   [fl_moxgen](https://aur.archlinux.org/packages/fl_moxgen/) – Moxon antenna designer
*   [geoid](https://aur.archlinux.org/packages/geoid/) – Geodetic calculator
*   [gpredict](https://aur.archlinux.org/packages/gpredict/) – Real-time satellite tracking and orbit prediction application
*   [hamsolar](https://aur.archlinux.org/packages/hamsolar/) – Small desktop display of the current solar indices
*   [splat](https://aur.archlinux.org/packages/splat/) – rf signal propagation, loss, and terrain analysis
*   [sunclock](https://aur.archlinux.org/packages/sunclock/) – Useful for predicting grayline propagation paths
*   [xnec2c](https://aur.archlinux.org/packages/xnec2c/) – Electromagnetic antenna modeler

### Logging

*   [cqrlog](https://aur.archlinux.org/packages/cqrlog/) – a popular Linux logging program
*   [fdlog](https://aur.archlinux.org/packages/fdlog/) – a Field Day Logger with networked nodes
*   [klog](https://aur.archlinux.org/packages/klog/) – a Ham radio logging program for Linux / KDE.
*   [qle](https://aur.archlinux.org/packages/qle/) – QSO Logger and log Editor for amateur radio operators written in Perl
*   [tlf](https://aur.archlinux.org/packages/tlf/) – a console mode networked logging and contest program
*   [trustedqsl](https://aur.archlinux.org/packages/trustedqsl/) – QSL application for ARRL's Logbook of the World
*   [tucnak2](https://aur.archlinux.org/packages/tucnak2/) – a multiplatform VHF/HF contest logbook
*   [xlog](https://aur.archlinux.org/packages/xlog/) – a logging program for amateur radio operators.
*   [yfklog](https://aur.archlinux.org/packages/yfklog/) – a general purpose ham radio logbook for *nix operating systems.
*   [yfktest](https://aur.archlinux.org/packages/yfktest/) – a logbook program for ham radio contests.

### Tools

*   [callsign](https://aur.archlinux.org/packages/callsign/) – a small program for finding information about a ham radio based on his callsign
*   [cty](https://aur.archlinux.org/packages/cty/) – package contains databases of entities (countries), prefixes and callsigns that are used by amateur radio logging software.
*   [dxcc](https://aur.archlinux.org/packages/dxcc/) – a small program for determining ARRL DXCC entity of a ham radio callsign
*   [nato](https://aur.archlinux.org/packages/nato/) – Python script to convert string into NATO alphabet representation
*   [tqsllib](https://aur.archlinux.org/packages/tqsllib/) – Trusted QSL library (supports ARRL Logbook of the World)

### Morse code training

*   [aldo](https://aur.archlinux.org/packages/aldo/)
*   [cutecw](https://aur.archlinux.org/packages/cutecw/)
*   [ebook2cw](https://aur.archlinux.org/packages/ebook2cw/)
*   [gtkmmorse](https://aur.archlinux.org/packages/gtkmmorse/)
*   [kochmorse](https://aur.archlinux.org/packages/kochmorse/)
*   [qrq](https://aur.archlinux.org/packages/qrq/)
*   [unixcw](https://aur.archlinux.org/packages/unixcw/)

### Other

*   [cwirc](https://aur.archlinux.org/packages/cwirc/) – Send and receive Morse code messages via IRC