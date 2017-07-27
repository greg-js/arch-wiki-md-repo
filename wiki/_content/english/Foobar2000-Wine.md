[foobar2000](https://www.foobar2000.org/) is an advanced freeware audio player for the Windows platform. It offers extensive features and flexibility through a modular architecture as well as an excellent compatibility with wine.

## Contents

*   [1 Installation](#Installation)
*   [2 Starting Foobar2000](#Starting_Foobar2000)
*   [3 Installing encoders](#Installing_encoders)
    *   [3.1 Adding Apple AAC and ALAC support](#Adding_Apple_AAC_and_ALAC_support)
*   [4 See also](#See_also)

## Installation

Install Wine as described in [Wine](/index.php/Wine "Wine").

Install [lib32-libpulse](https://www.archlinux.org/packages/?name=lib32-libpulse) or [lib32-alsa-lib](https://www.archlinux.org/packages/?name=lib32-alsa-lib) and [lib32-alsa-plugins](https://www.archlinux.org/packages/?name=lib32-alsa-plugins) from the [Multilib](/index.php/Multilib "Multilib") repository to have foobar2000 to find the audio outputs. See [foobar2000 in wine's appdb](https://appdb.winehq.org/objectManager.php?sClass=version&iId=18689) and [Wine#Sound](/index.php/Wine#Sound "Wine") for details.

Download the lastest installer from [https://www.foobar2000.org/download](https://www.foobar2000.org/download) and run:

```
$ wine ~/Downloads/foobar2000_v*.exe

```

to install foobar2000 in the defaut 64 bit wineprefix.

## Starting Foobar2000

A .desktop entry is automatically created but you can also use:

```
$ wine "$HOME/.wine/drive_c/Program Files (x86)/foobar2000.exe"

```

## Installing encoders

A pack of free audio encoders is provided by the foobar2000 devs and available [here](https://www.foobar2000.org/encoderpack). It notably includes FLAC and MP3 (LAME) encoders, both working out-of-the-box.
Install using:

```
$ wine "$HOME/Downloads/Free_Encoder_Pack_*.exe"

```

**Note:** As the developers points out:
"*Please note that this pack includes only encoders that we are legally allowed to distribute; that excludes AAC encoders (**included AAC encoders require external applications providing actual encoding functionality**).*"

### Adding Apple AAC and ALAC support

The AAC Apple encoder is considered as one of the best lossy encoder available [[1]](http://wiki.hydrogenaud.io/index.php?title=Apple_AAC) and is supported by most *Digital Audio Players*.
ALAC has a slight advantage over FLAC in terms of compression.

The following steps will give you functional Apple AAC and ALAC encoders ***without** having to install iTunes* (which doesn't work with wine anyway) or QuickTime, just by extracting and installing the required third party modules. [[2]](https://forum.dbpoweramp.com/showthread.php?30636-qAAC-%28iTunes-AAC-encoder%29-with-dBpoweramp)

Install the lastest version of the [Free Encoder Pack for foobar2000](https://www.foobar2000.org/encoderpack) which includes [qAAC](http://wiki.hydrogenaud.io/index.php?title=Apple_AAC#QAAC)

You need to download in the **same folder**:

1.  the lastest release of [iTunes](https://www.apple.com/itunes/download/) *or* [QuickTime](https://support.apple.com/kb/DL837?locale=en_US) for Windows 64 bit,
2.  the [makeportable.zip](https://sites.google.com/site/qaacpage/cabinet) archive provided by the qAAC developer,
3.  [7-Zip](http://www.7-zip.org/download.html) for Windows 64 bit.

**Note:** The following commands will assume you've downloaded everything in the "Program Files (x86)" folder of the default wineprefix.

Install 7-Zip:

```
$ wine "$HOME/.wine/drive_c/Program Files (x86)/7z1700-x64.exe"

```

Unzip makeportable.zip.
Then use:

```
$ wineconsole cmd

```

In the cmd terminal use :

```
$ cd "\<path to home>\.wine\drive_c\Program Files (x86)\"
$ makeportable.cmd

```

**Note:** Please note that in cmd the path is punctuated with backward slash "\" instead of forward slash "/".

Install the required third party modules:

```
$ wine msiexec /i "$HOME/.wine/drive_c/Program Files (x86)/AppleApplicationSupport64.msi"

```

You've successfully added support for foobar2000's AAC & ALAC encoders to your wine environment.

## See also

*   [Foobar2000's website](https://www.foobar2000.org/)
*   qAAC
    *   [On github](https://github.com/nu774/qaac/)
    *   [Dev's site](https://sites.google.com/site/qaacpage/)
*   [A post about AAC encoders & Foobar2000 describing how to install support for FDK AAC encoder](https://forum.videohelp.com/threads/370412-Looking-for-an-AAC-LC-encoder-from-Frauenhofer#post2376348)