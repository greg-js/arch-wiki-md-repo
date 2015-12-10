# Lenovo ThinkPad X250

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

The Lenovo ThinkPad X250 is the successor to the [Lenovo ThinkPad X240](/index.php/Lenovo_ThinkPad_X240 "Lenovo ThinkPad X240"). Major differences include the physical TrackPoint buttons above the touchpad mouse as well as the Broadwell line of Intel CPUs.

## Contents

*   [1 Tested Configuration](#Tested_Configuration)
*   [2 System Configuration](#System_Configuration)
    *   [2.1 Mouse](#Mouse)
    *   [2.2 Fingerprint](#Fingerprint)
    *   [2.3 Backlight and Keyboard](#Backlight_and_Keyboard)
    *   [2.4 Sound and Volume Control](#Sound_and_Volume_Control)
    *   [2.5 Bluetooth](#Bluetooth)

#### Tested Configuration

**Tip:** Below were the tested configurations at the current time.

<table class="wikitable sortable">

<tbody>

<tr>

<th>Feature</th>

<th>Configuration</th>

</tr>

<tr>

<td>System</td>

<td>X250</td>

</tr>

<tr>

<td>CPU</td>

<td>Intel(R) Core(TM) i5-5200U CPU @ 2.20GHz</td>

</tr>

<tr>

<td>Graphics</td>

<td>Intel HD 5400 - Broadwell</td>

</tr>

<tr>

<td>Ram</td>

<td>8 GB</td>

</tr>

<tr>

<td>Disk</td>

<td>180 GB Solid State Drive Opal 2.0 - XCapable</td>

</tr>

<tr>

<td>Display</td>

<td>12.5" IPS FHD (1920x1080) non-touch</td>

</tr>

<tr>

<td>Wireless</td>

<td>Intel Corporation Wireless 7265</td>

</tr>

<tr>

<td>Built-in Battery</td>

<td>9 Cell</td>

</tr>

<tr>

<td>Additional Plugable Battery</td>

<td>6 Cell 19+</td>

</tr>

<tr>

<td>Backlight Keyboard</td>

<td>Yes</td>

</tr>

<tr>

<td>ThinkLight</td>

<td>No</td>

</tr>

<tr>

<td>Fingerprint Scanner</td>

<td>Yes</td>

</tr>

<tr>

<td>Bluetooth</td>

<td>Yes</td>

</tr>

<tr>

<td>Camera</td>

<td>Yes</td>

</tr>

</tbody>

</table>

### System Configuration

#### Mouse

The touchpad and TrackPoint work out of the box, but the physical buttons for the trackpoint do not. You will need to install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

**Note:** The most recent Linux kernels (at least 4.0.5) support TrackPoint buttons out of the box. The following information pertains only to older versions of the kernel.

If you would rather not install a recent kernel, there is a work around for Linux 3.19.2-ARCH. If you add `options psmouse proto=imps` to `/etc/modprobe.d/x250.conf`, you can force the mouse module to use a more basic protocol than the built in one for the TrackPoint, which needs a patch. The effect is that the touchpad and mouse are treated as one device, but synaptics is not supported. If you want two finger scrolling, for example, you will need to either deal with the broken TrackPoint buttons are install the new module.

#### Fingerprint

The fingerprint reader works out of the box with [fprintd](https://www.archlinux.org/packages/?name=fprintd).

#### Backlight and Keyboard

In order to get the backlight to work, I added `options thinkpad_acpi force-load=1` to `/etc/modprobe.d/x250.conf`. This forces the thinkpad_acpi module to load, which is needed for controlling the backlight vPkgia [xorg-xbacklight](https://www.archlinux.org/packages/?name=xorg-xbacklight) as well as enable some of the extra media keys.

#### Sound and Volume Control

With [acpid](https://www.archlinux.org/packages/?name=acpid) and [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) installed, you can map the volume buttons to change the volume. Here are some samples:

`/etc/acpi/events/volumemute`:

```
event=button/mute
action=amixer -c 1 sset Master toggle -q

```

`/etc/acpi/events/volumedown`:

```
event=button/volumedown
action=amixer -c 1 sset -M Master 5%%- unmute -q

```

`/etc/acpi/events/volumeup`:

```
event=button/volumeup
action=amixer -c 1 sset -M Master 5%%+ unmute -q

```

`/etc/acpi/events/mutemic`:

```
event=button/f20
action=amixer -c 1 sset Mic toggle -q

```

[PulseAudio](/index.php/PulseAudio "PulseAudio") and [pavucontrol](https://www.archlinux.org/packages/?name=pavucontrol) are also great tools for fixing volume issues.

#### Bluetooth

Bluetooth was not tested.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X250&oldid=378133](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_X250&oldid=378133)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")