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
    *   [2.1 Receiver and transmitter configuration](#Receiver_and_transmitter_configuration)
        *   [2.1.1 Serial port](#Serial_port)
        *   [2.1.2 Sound card](#Sound_card)
    *   [2.2 Remote configuration](#Remote_configuration)
        *   [2.2.1 Searching for remote configuration](#Searching_for_remote_configuration)
        *   [2.2.2 Creating remote configuration](#Creating_remote_configuration)
    *   [2.3 Application-specific actions](#Application-specific_actions)
    *   [2.4 Running as a regular user rather than as root](#Running_as_a_regular_user_rather_than_as_root)
*   [3 Testing](#Testing)
    *   [3.1 Receiving commands](#Receiving_commands)
    *   [3.2 Transmitting commands](#Transmitting_commands)
*   [4 Troubleshooting](#Troubleshooting)
    *   [4.1 Remote functions as a keyboard](#Remote_functions_as_a_keyboard)
        *   [4.1.1 When using Xorg](#When_using_Xorg)
        *   [4.1.2 On an ARM device not using Xorg](#On_an_ARM_device_not_using_Xorg)
    *   [4.2 Changing default configuration](#Changing_default_configuration)
        *   [4.2.1 Example](#Example)
*   [5 See also](#See_also)

## Installation

[Install](/index.php/Install "Install") the [lirc](https://www.archlinux.org/packages/?name=lirc) package. If you need *audio* driver, install [lirc-git](https://aur.archlinux.org/packages/lirc-git/).

## Configuration

### Receiver and transmitter configuration

**Note:** This section is a quick summary. Complete documentation is available [upstream](http://lirc.sourceforge.net/lirc.org/html/index.html).

The *driver* and/or the *device* for the LIRC service may need to be specified in order to run properly. Look for messages like these in the [journalctl](/index.php/Journalctl "Journalctl") output if the service abruptly stops while running LIRC-dependent programs such as *irrecord*:

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

#### Serial port

**Tip:** For DIY schematic refer to serial port [receivers](http://www.lirc.org/receivers.html) and [transmitters](http://www.lirc.org/transmitters.html) documentation. Note that serial port device much more reliable than *audio_alsa* or *audio*.

Modern kernel has *serial_ir* module, which supersedes older *lirc_serial* driver. It supports even DIY receivers and transmitters, connected to the motherboard's serial port. Install [setserial](https://aur.archlinux.org/packages/setserial/) and run:

```
# setserial /dev/ttyS0 uart none
# modprobe serial_ir

```

After loading *serial_ir* module, device `/dev/lirc0` will be [created](https://github.com/torvalds/linux/blob/master/drivers/media/rc/serial_ir.c) by kernel. If not, check `dmesg | grep serial` for errors. An LIRC config example for serial device:

 `/etc/lirc/lirc_options.conf` 
```
[lircd]
driver          = default
device          = auto

[modinit]
code = /usr/bin/setserial /dev/ttyS0 uart none
code1 = /usr/sbin/modprobe serial_ir
```

#### Sound card

**Note:** Using sound card as infrared device has plenty pitfalls and doesn't gives advantage over other hardware setup.

Sound card with connected external DIY circuits can be used to [receive](http://www.lirc.org/ir-audio.html) and [transmit](https://web.archive.org/web/20150511192459/http://www.lirc.org:80/html/audio.html) IR codes.

*audio_alsa* [driver](http://www.lirc.org/html/audio-alsa.html) included in [lirc](https://www.archlinux.org/packages/?name=lirc), but supports only reception.

Unmute microphone input with `alsamixer` and set enough gain. You can check waveform and gain with [audacity](https://www.archlinux.org/packages/?name=audacity). There should be distinguishable square pulses: not flatlined, nor overloaded. Also good demodulated pulses easily perceptible by ear. Note that LIRC and `irrecord` reads *positive pulses in right audio channel*. Negative pulses won't work.

 `/etc/lirc/lirc_options.conf` 
```
driver          = audio_alsa
device          = default
```

*audio* [driver](https://web.archive.org/web/20150511192459/http://www.lirc.org:80/html/audio.html) included in [lirc-git](https://aur.archlinux.org/packages/lirc-git/) and supports both reception and transmission. Note, that default latency around 0.02 can cause "Warning: Output underflow" and corrupted transmission - receiver won't respond to it. Try a higher value like 0.05.

Increase sound card output loudness, otherwise LED signal will be weak and range is low. LED flash can be detected with smartphone camera, as it sensitive to infrared wavelengths.

 `/etc/lirc/lirc_options.conf` 
```
driver          = audio
device          = ALSA:default@48000:0.05
```

### Remote configuration

Directory `/etc/lirc/lircd.conf.d/` contains system-wide configuration files for remotes. Each **.conf* file corresponds to one device and describes it's protocol, scancodes and keycodes. It allows LIRC receive and send signals for specific hardware. These files aren't included in [lirc](https://www.archlinux.org/packages/?name=lirc) package and should be found somewhere or created by user.

#### Searching for remote configuration

Plenty of configuration files can be found in the [LIRC remotes database](http://lirc-remotes.sourceforge.net/remotes-table.html). Follow the url or use [irdb-get(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/irdb-get.1) to search the database.

An example using `irdb-get` to find a config file for a "Streamzap" remote:

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

#### Creating remote configuration

Remote control configurations can be created using [irrecord(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/irrecord.1), which guides users trough the process. If using a detected remote, invoke it like so:

```
# irrecord --device=/dev/lirc0 MyRemote

```

The program will instruct user to begin hitting keys on the remote in an attempt to learn it, ultimately mapping out every button and it's corresponding scancode. When finished, save the resulting file to `/etc/lirc/lircd.conf.d/foo.conf` and proceed. Consider sharing configuration file with others.

### Application-specific actions

**Tip:** Many application-specific lircrc files are available on the internet.

Bind keycodes to application-specific actions by placing their respective configuration files in `~/.config/lircrc/` which should be created manually if desired, see [lircrc(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/lircrc.5). This only works for LIRC-aware applications, like [MPlayer](/index.php/MPlayer "MPlayer"), [VLC](/index.php/VLC "VLC"), [MythTV](/index.php/MythTV "MythTV") and [totem](https://www.archlinux.org/packages/?name=totem) ([Kodi](/index.php/Kodi "Kodi") also supports LIRC but does so in a non-standard way, see [Kodi#Using a remote control](/index.php/Kodi#Using_a_remote_control "Kodi")).

Define these application-specific configurations in separate files and include them in *lircrc*, like:

```
include "~/.config/lircrc/mplayer"
include "~/.config/lircrc/mythtv"
include "~/.config/lircrc/vlc"

```

### Running as a regular user rather than as root

By default, lircd runs as user root. However, for increased stability and security, upstream recommends running it as a regular user. See Appendix 14 at [this](http://www.lirc.org/html/configuration-guide.html) link.

To do this, create and provision a lirc user:

```
# groupadd -r lirc
# useradd -r -g lirc -d /var/lib/lirc -s /usr/bin/nologin -c "LIRC daemon user" lirc
# usermod -a -G lock,input lirc

```

Augment the package-providing service unit by creating a lircd [Systemd#Drop-in files](/index.php/Systemd#Drop-in_files "Systemd"):

 `# systemctl edit lircd` 
```
[Service]
User=lirc
Group=lirc

CapabilityBoundingSet=CAP_SETEUID
MemoryDenyWriteExecute=true
NoNewPrivileges=true
PrivateTmp=true
ProtectHome=true
ProtectSystem=full

```

To allow `/dev/lirc*` devices to be accessible for the lirc group and to grant r/w access for the lirc group to USB devices using ACLs, copy the following udev rule into place:

```
# cp /usr/share/lirc/contrib/60-lirc.rules /etc/udev/rules.d/

```

To allow access to the lirc group to be able to create a PID file, create the following lircd tmpfile which will supersede the package provided one (which makes ownership only to root):

 `/etc/tmpfiles.d/lirc.conf` 
```
d /run/lirc 0755 lirc lirc -

```

Reboot the system to verify expected function.

## Testing

[Start/enable](/index.php/Start/enable "Start/enable") `lircd.service`.

### Receiving commands

Run [irw(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/irw.1), point remote to the receiver and press some buttons. Received codes will be printed to stdout.

```
$ irw
000000037ff07bfe 00 One mceusb
000000037ff07bfd 00 Two mceusb
000000037ff07bfd 01 Two mceusb
000000037ff07bf2 00 Home mceusb
000000037ff07bf2 01 Home mceusb

```

If `irw` gives no output:

*   Run *mode2* or *xmode2* to see if LIRC actually read something from IR sensor, if no - check the hardware
*   If *mode2* receives pulse data, check the config files in `/etc/lirc/lircd.conf.d/` for errors

### Transmitting commands

List registered remotes (config files):

```
$ irsend LIST "" ""
LG_6710CMAP01A

```

List available codes for the specific device:

```
$ irsend LIST LG_6710CMAP01A ""
0000000000007887 KEY_POWER
000000000000f807 KEY_MUTE
000000000000e817 KEY_VOLUMEUP
...

```

Choose discovered device `LG_6710CMAP01A` and send command `KEY_POWER`:

```
$ irsend SEND_ONCE LG_6710CMAP01A KEY_POWER

```

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

*   [Project site](http://sf.net/p/lirc)
*   [Upstream documentation](http://lirc.sourceforge.net/lirc.org/html/index.html)
*   [Upstream Configuration Guide](http://lirc.org/html/configuration-guide.html)
*   [Remotes database](http://lirc-remotes.sourceforge.net/remotes-table.html)
*   [MythTV Wiki:Remotes article](http://www.mythtv.org/wiki/Category:Remote_Controls)
*   [Linux Streamzap config files](https://github.com/graysky2/streamzap)