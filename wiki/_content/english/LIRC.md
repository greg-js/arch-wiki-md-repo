Related articles

*   [LIRC/Quick start guide](/index.php/LIRC/Quick_start_guide "LIRC/Quick start guide")

From the [official website](http://lirc.org/):

	**LIRC** (Linux Infrared Remote Control) is a package that decodes and sends infra-red signals of many (but not all) commonly used remote controls.

**Note:** Since 4.18 the kernel can decode the signals of some IR remote controls using BPF, making LIRC sometimes redundant.[[1]](https://lwn.net/Articles/759188/)

This article covers setup and usage of LIRC with serial or USB infrared devices.

LIRC is a daemon that can translate key presses on a supported remote into program specific commands. In this context, the term, "program specific" means that a key press can do different things depending on which program is running and taking commands from LIRC.

1.  A button on the remote is pressed causing it to transmit an IR or RF signal.
2.  The signal is received by the receiver connected to the Linux computer.
3.  The kernel (via the correct module) use presents pulse data from the remote on a device like `/dev/lirc0`, `/dev/input/eventX`, `/dev/ttyUSBX` or `/dev/ttyS0`.
4.  `/usr/bin/lircd` uses the information from `/etc/lirc/lircd.conf.d/foo.conf` to convert the pulse data into button press information.
5.  Programs that use LIRC translate the button press info from `/usr/bin/lircd` into user-defined actions according to `~/.config/lircrc` or to program-specific mappings.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 Scancode mapping](#Scancode_mapping)
        *   [2.1.1 Remotes database](#Remotes_database)
        *   [2.1.2 Creating remote configurations](#Creating_remote_configurations)
    *   [2.2 Application-specific actions](#Application-specific_actions)
*   [3 Usage](#Usage)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Remote functions as a keyboard](#Remote_functions_as_a_keyboard)
        *   [4.1.1 When using Xorg](#When_using_Xorg)
        *   [4.1.2 On an ARM device not using Xorg](#On_an_ARM_device_not_using_Xorg)
    *   [4.2 Changing default configuration](#Changing_default_configuration)
        *   [4.2.1 Example](#Example)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lirc](https://www.archlinux.org/packages/?name=lirc) package.

## Configuration

**Note:** This section is a quick summary. Complete documentation is available [upstream](http://lirc.sourceforge.net/lirc.org/html/index.html).

The driver and/or the device for the LIRC service may need to be specified in order to run properly. Look for messages like these in the [journalctl](/index.php/Journalctl "Journalctl") output if the service abruptly stops while running LIRC-dependent programs such as *irrecord*:

```
Driver `devinput' not found or not loadable (wrong or missing -U/--plugindir?).
readlink() failed for "auto": No such file or directory

```

Set these in the config file and then restart the service.

 `/etc/lirc/lirc_options.conf` 
```
[lircd]
driver = *driver-name*
device = /dev/*path-to-dev*
```

### Scancode mapping

`/etc/lirc/lircd.conf.d/foo.conf` is the system-wide configuration translating scancodes to keycodes. This directory may contain multiple conf files and each one is specific to each remote control/receiver on the system. These files are user-created config files and not directly supplied by [lirc](https://www.archlinux.org/packages/?name=lirc).

The definition of scancodes to keycodes is required to allow LIRC to manage a remote.

#### Remotes database

LIRC provides configuration files for many remote controls in the [remotes database](http://lirc-remotes.sourceforge.net/remotes-table.html). Use [irdb-get(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/irdb-get.1) to search the database or simply browse to the URL and do the same.

Refer to [creating remote configurations](#Creating_remote_configurations) if configs for your specific hardware are not in either location.

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

#### Creating remote configurations

Remote control configurations can easily be created using [irrecord(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/irrecord.1), which guides users along the needed process. If using a detected remote, invoke it like so:

```
# irrecord --device=/dev/lirc0 MyRemote

```

The program will instruct users to begin hitting keys on the remote in an attempt to learn it, ultimately mapping out every button and its corresponding scancode. When finished, save the resulting file to `/etc/lirc/lircd.conf.d/foo.conf` and proceed.

**Tip:** Consider sending the finished config file to the email address mentioned in the program so it can be made available to others.

### Application-specific actions

Bind keycodes to application-specific actions by placing their respective configuration files in `~/.config/lircrc/` which should be created manually if desired, see [lircrc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lircrc.5). This only works for LIRC-aware applications, like [MPlayer](/index.php/MPlayer "MPlayer"), [VLC](/index.php/VLC "VLC"), [MythTV](/index.php/MythTV "MythTV") and [totem](https://www.archlinux.org/packages/?name=totem) ([Kodi](/index.php/Kodi "Kodi") also supports LIRC but does so in a non-standard way, see [Kodi#Using a remote control](/index.php/Kodi#Using_a_remote_control "Kodi")).

Define these application-specific configurations in separate files and include them in *lircrc*, like:

```
include "~/.config/lircrc/mplayer"
include "~/.config/lircrc/mythtv"
include "~/.config/lircrc/vlc"

```

**Tip:** Many application-specific lircrc files are available on the internet.

## Usage

[Start/enable](/index.php/Start/enable "Start/enable") `lircd.service`.

Test the remote using [irw(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/irw.1), which simply echos anything received by LIRC when users push buttons on the remote to stdout.

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

## Troubleshooting

### Remote functions as a keyboard

#### When using Xorg

[Xorg](/index.php/Xorg "Xorg") detects some remotes, such as the Streamzap USB PC Remote, as a Human Interface Device (HID) which means some or all of the keys will show up as key strokes as if entered from the physical keyboard. This behavior will present problems if LIRC is to be used to manage the device.

To disable, create the following file and restart X:

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

### Changing default configuration

Users not getting any output from `irw` may have the default configuration in `/etc/lirc/lirc_options.conf` incorrectly setup (or might have been overwritten by an update).

First, check if `/dev/lirc0` is present:

```
$ mode2 --driver default --device /dev/lirc0

```

Watch the output while pressing buttons on the remote. If output is present, edit `/etc/lirc/lirc_options.conf` changing the **driver** and **device** appropriately.

If no output is presented, the task becomes locating the correct driver/device combination. First check what combination lirc detected by default. Run `ir-keytable` from the [v4l-utils](https://www.archlinux.org/packages/?name=v4l-utils) package. and check the output. It will look similar to this:

```
 Found /sys/class/rc/rc0/ (/dev/input/event5) with:
       Driver ite-cir, table rc-rc6-mce
       Supported protocols: unknown other lirc rc-5 jvc sony nec sanyo mce-kbd rc-6 sharp xmp
       Enabled protocols: lirc
       Extra capabilities: <access denied>

```

In this case, LIRC automatically detected `/dev/input/event5` as the IR device, which uses the `devinput` driver. Check if this combination is working by running:

```
$ mode2 --driver devinput --device /dev/input/event5

```

Now try pressing buttons on the remote. If there is no output, try different driver and device combinations. Once a working combination has been identified, change **driver** and **device** in `/etc/lirc/lirc_options.conf` appropriately.

#### Example

An example configuration for a MCE RC6 compatible receiver:

 `/etc/lirc/lirc_options.conf` 
```
[lircd]
nodaemon        = False
driver          = default
device          = /dev/lirc0
output          = /var/run/lirc/lircd
pidfile         = /var/run/lirc/lircd.pid
plugindir       = /usr/lib/lirc/plugins
permission      = 666
allow-simulate  = No
repeat-max      = 600

[lircmd]
uinput          = False
nodaemon        = False
```

## See also

*   [Upstream documentation](http://lirc.sourceforge.net/lirc.org/html/index.html)
*   [Remotes database](http://lirc-remotes.sourceforge.net/remotes-table.html)
*   [Project site](http://sf.net/p/lirc)
*   [Upstream Configuration Guide](http://lirc.org/html/configuration-guide.html)
*   [MythTV Wiki:Remotes article](http://www.mythtv.org/wiki/Category:Remote_Controls)
*   [Official list of supported hardware](http://lirc-remotes.sourceforge.net/remotes-table.html)
*   [Linux Streamzap config files](https://github.com/graysky2/streamzap)