# LIRC

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Related articles

*   [LIRC Device Examples](/index.php/LIRC_Device_Examples "LIRC Device Examples")

This article covers setup and usage of [LIRC](http://lirc.org/) "Linux Infrared Remote Control" with serial or USB infrared devices.

LIRC is a daemon that can translate key presses on a supported remote into program specific commands. In this context, the term, "program specific" means that a key press can do different things depending on which program is running and taking commands from LIRC.

The Central Dogma of LIRC (an allusion to the [flow of information](http://www.ncbi.nlm.nih.gov/Class/MLACourse/Modules/MolBioReview/central_dogma.html) in biological systems) is summarized below wherein the flow of information from the remote to the application is summarized with LIRC at the center of it all:

*   User hits a button on the remote causing it to transmit an IR or RF signal.
*   The signal is received by the receiver connected to the Linux box.
*   The kernel (via the correct module) use presents pulse data from the remote on a device like /dev/lirc0, /dev/input/eventX, /dev/ttyUSBX or /dev/ttyS0.
*   `/usr/bin/lircd` uses the information from `/etc/lirc/lircd.conf.d/foo.conf` to convert the pulse data into button press information.
*   Programs that use LIRC translate the button press info from `/usr/bin/lircd` into user-defined actions according to `~/.lircrc` or to program-specific mappings.

## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Upstream provided](#Upstream_provided)
    *   [2.2 User created](#User_created)
    *   [2.3 Optional files](#Optional_files)
*   [3 Usage](#Usage)
*   [4 Program Specific Configuration](#Program_Specific_Configuration)
*   [5 Troubleshooting](#Troubleshooting)
    *   [5.1 Remote functions as a keyboard](#Remote_functions_as_a_keyboard)
        *   [5.1.1 When using Xorg](#When_using_Xorg)
        *   [5.1.2 On an ARM device not using Xorg](#On_an_ARM_device_not_using_Xorg)
*   [6 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lirc](https://www.archlinux.org/packages/?name=lirc) package.

## Configuration

**Note:** This section is a quick summary. Complete documentation is available [upstream](http://lirc.sourceforge.net/lirc.org/html/index.html).

`/etc/lirc/lircd.conf.d/foo.conf` is the system-wide configuration translating scancodes --> keys. This directory may contain multiple conf files and each one is specific to each remote control/receiver on the system. These files are user-created config files and not directly supplied by [lirc](https://www.archlinux.org/packages/?name=lirc).

The definition of scancodes to keymaps is required to allow LIRC to manage a remote. Users have several options to obtain one.

### Upstream provided

Identify which remote/receiver is to be used and see if there is a known config for it. One can use `irdb-get` to search the [remotes database](http://lirc-remotes.sourceforge.net/remotes-table.html) or simply browse to the URL and do the same.

An example using `irdb-get` to find a config file for a Streamzap remote:

```
$ irdb-get find stream
atiusb/atiusb.lircd.conf
digital_stream/DTX9900.lircd.conf
snapstream/Firefly-Mini.lircd.conf
streamzap/PC_Remote.lircd.conf
streamzap/streamzap.lircd.conf
x10/atiusb.lircd.conf

$ irdb-get download streamzap/streamzap.lircd.conf 
Downloaded sourceforge.net/p/lirc-remotes/code/ci/master/tree/remotes/streamzap/streamzap.lircd.conf as streamzap.lircd.conf

```

Once identified, copy the needed conf to `/etc/lirc/lircd.conf.d/` to allow the daemon to initialize support for it.

```
# cp streamzap.lircd.conf /etc/lirc/lircd.conf.d/

```

### User created

Users with unsupported hardware will need to either find a config file someone else has created (i.e. google) or create one. Creating one is fairly straightforward using `/usr/bin/irrecord` which guides users along the needed process. If using a detected remote, invoke it like so:

```
# irrecord --device=/dev/lirc0 MyRemote

```

The program will instruct users to begin hitting keys on the remote in an attempt to learn it, ultimately mapping out every button and its corresponding scancode. The process should take no more than 10 minutes. When finished, save the resulting file to `/etc/lirc/lircd.conf.d/foo.conf` and proceed.

**Note:** Consider sending the finished config file to the email address mentioned in the program so it can be made available to others.

### Optional files

Depending on the application using LIRC, the following are optional. For example, [mplayer](https://www.archlinux.org/packages/?name=mplayer) and [mythtv](https://www.archlinux.org/packages/?name=mythtv) use the these files to define key maps and actions. Some other programs such as [kodi](https://www.archlinux.org/packages/?name=kodi) for example do not make use of this at all but do have an internal system to achieve these mappings. Users should consult the documentation for the specific application to know if modifications to `~/.lircrc` are needed.

*   `~/.lircrc` - File containing an **include** statement pointing to each program's lirc map, i.e., `~/.lirc/foo`, `~/.lirc/bar`, etc.
*   `~/.lirc/foo` - User-level config translating of keys --> actions. Is specific to each remote and to application foo.

## Usage

[Start](/index.php/Start "Start") `lircd.service` and [enable](/index.php/Enable "Enable") it to run at boot time/shutdown (recommended).

Test the remote using `/usr/bin/irw`, which simply echos anything received by LIRC when users push buttons on the remote to stdout.

Example:

```
$ irw
000000037ff07bfe 00 One mceusb
000000037ff07bfd 00 Two mceusb
000000037ff07bfd 01 Two mceusb
000000037ff07bf2 00 Home mceusb
000000037ff07bf2 01 Home mceusb

```

If `irw` gives no output, double check the config files in `/etc/lirc/lircd.conf.d/` for errors.

## Program Specific Configuration

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [LIRC#Optional](/index.php/LIRC#Optional "LIRC").**

**Notes:** or the other way around (Discuss in [Talk:LIRC#](https://wiki.archlinux.org/index.php/Talk:LIRC))

LIRC has the ability to allow for different programs to use the same keypress and result in unique commands. In other words, one can setup different programs to respond differently to a given key press.

*   Decide which programs are to use LIRC commands.

**Note:** Common programs include: [mplayer](https://www.archlinux.org/packages/?name=mplayer), [mythtv](https://www.archlinux.org/packages/?name=mythtv), [totem](https://www.archlinux.org/packages/?name=totem), [vlc](https://www.archlinux.org/packages/?name=vlc), and [kodi](https://www.archlinux.org/packages/?name=kodi) but not all programs will use this particular method to map keys. [kodi](https://www.archlinux.org/packages/?name=kodi) for example, implements LIRC in a non-standard way. Users must edit `~/.xbmc/userdata/Lircmap.xml` which is a unique xml file, rather than the LIRC standard files the rest of the programs use. Interested users should consult [Kodi#Using a remote control](/index.php/Kodi#Using_a_remote_control "Kodi").

*   Create the expected files showing LIRC where the various program-specific maps reside:

```
$ mkdir ~/.lirc
$ touch ~/.lircrc

```

*   Populate `~/.lirc` with the program specific config files named for each program.

Example:

```
$ ls ~/.lirc
mplayer
mythtv
vlc

```

**Tip:** Many pre-made files unique to each remote/program are available via googling. Providing an exhaustive listing of keymaps for each program is beyond the scope of this article.

*   Edit `~/.lircrc` to contain an **include** statement pointing to `~/.lirc/foo` and repeat for each program that is to be controlled by LIRC.

Example:

 `~/.lircrc` 

```
include "~/.lirc/mplayer"
include "~/.lirc/mythtv"
include "~/.lirc/vlc"

```

## Troubleshooting

### Remote functions as a keyboard

#### When using Xorg

Xorg detects some remotes, such as the Streamzap USB PC Remote, as a Human Interface Device (HID) which means some or all of the keys will show up as key strokes as if entered from the physical keyboard. This behavior will present problems if LIRC is to be used to manage the device. To disable, create the following file and restart X:

 `/etc/X11/xorg.conf.d/90-streamzap.conf` 

```
Section "InputClass"
  Identifier "Ignore Streamzap IR"
  MatchProduct "Streamzap"
  MatchIsKeyboard "true"
  Option "Ignore" "true"
EndSection
```

Do not forget to alter the `MatchProduct` property according to one shown in `Name` from output of

```
$ cat /proc/bus/input/devices | grep -e IR

```

For example `WinFast` for `N: Name="cx88 IR (WinFast DTV2000 H rev."`

#### On an ARM device not using Xorg

Blacklist the offending modules by creating `/etc/modprobed.d/streamzap.conf` to suppress this behavior. An example is provided for the Streamzap remote.

```
install ir_sharp_decoder /bin/false
install ir_xmp_decoder /bin/false
install ir_rc5_decoder /bin/false
install ir_nec_decoder /bin/false
install ir_sony_decoder /bin/false
install ir_mce_kbd_decoder /bin/false
install ir_jvc_decoder /bin/false
install ir_rc6_decoder /bin/false
install ir_sanyo_decoder /bin/false

```

## See also

*   [Upstream documentation](http://lirc.sourceforge.net/lirc.org/html/index.html)
*   [Remotes database](http://lirc-remotes.sourceforge.net/remotes-table.html)
*   [Project site](http://sf.net/p/lirc)
*   [Upstream Configuration Guide](http://lirc.org/html/configuration-guide.html)
*   [MythTV Wiki:Remotes article](http://www.mythtv.org/wiki/Category:Remote_Controls)
*   [Official list of supported hardware](http://lirc-remotes.sourceforge.net/remotes-table.html)
*   [Linux Streamzap config files](https://github.com/graysky2/streamzap)

Retrieved from "[https://wiki.archlinux.org/index.php?title=LIRC&oldid=409132](https://wiki.archlinux.org/index.php?title=LIRC&oldid=409132)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Other hardware](/index.php/Category:Other_hardware "Category:Other hardware")

Hidden category:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")