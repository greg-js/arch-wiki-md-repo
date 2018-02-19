The Lenovo ThinkPad X220 is a small-form-factor laptop with Intel Mobile i5/i7 CPU, and Intel graphics. It has no optical drive. You can see full specs at [ThinkWiki](http://www.thinkwiki.org/wiki/Category:X220).

## Contents

*   [1 Configuration](#Configuration)
    *   [1.1 Battery](#Battery)
    *   [1.2 Fingerprint reader](#Fingerprint_reader)
    *   [1.3 Graphics](#Graphics)
    *   [1.4 Trackpoint and Clickpad](#Trackpoint_and_Clickpad)
    *   [1.5 Dock](#Dock)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Boot fails (UEFI/GPT)](#Boot_fails_.28UEFI.2FGPT.29)
    *   [2.2 Reboot loop after resume from suspend](#Reboot_loop_after_resume_from_suspend)
    *   [2.3 Microphone](#Microphone)
    *   [2.4 Multi-monitor setups with X](#Multi-monitor_setups_with_X)
    *   [2.5 Backlight](#Backlight)
    *   [2.6 X220 Touchpad cursor jump/imprecise](#X220_Touchpad_cursor_jump.2Fimprecise)
*   [3 See also](#See_also)

## Configuration

### Battery

Battery functions like charging thresholds can be controlled using the script [tpacpi-bat](https://www.archlinux.org/packages/?name=tpacpi-bat) together with the kernel module [acpi_call](https://www.archlinux.org/packages/?name=acpi_call). The [TLP](/index.php/TLP "TLP") power saving tool supports using acpi_call as backend for setting the thresholds as well.

### Fingerprint reader

The Upek fingerprint reader is supported by [Fingerprint-gui](/index.php/Fingerprint-gui "Fingerprint-gui").

### Graphics

The graphics driver is provided by the [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) package from the [Official repositories](/index.php/Official_repositories "Official repositories").

### Trackpoint and Clickpad

See [TrackPoint](/index.php/TrackPoint "TrackPoint").

### Dock

See [dockd](/index.php/Dockd "Dockd").

## Troubleshooting

### Boot fails (UEFI/GPT)

The laptop can not boot from a [GPT](/index.php/GPT "GPT") disk in `Legacy BIOS` mode, it is necessary to either switch to `UEFI` booting or create a [MBR Partition Table](/index.php/Partitioning#Master_Boot_Record "Partitioning").

Additional considerations from ThinkWiki:

*   The X220 cannot/will not boot GPT disks using `Legacy BIOS`, you must setup `UEFI`.
*   The X220 will not boot `/efi/*/*.efi` unless *signed(?)* into BIOS, you have to copy it to `/efi/boot/bootx64.efi`.
*   Disabling the BIOS setting `USB UEFI BIOS Support` disables **all** USB booting, ie, both `UEFI` and `Legacy BIOS`.

### Reboot loop after resume from suspend

This can be caused by the EFI storage getting too full. Run the following commands as root to free up some space.

```
 # First clear the pstore
 mkdir -p /dev/pstore
 mount -t pstore pstore /dev/pstore
 ls /dev/pstore # <- Nothing important should be here, but check first anyway
 rm /dev/pstore/*

```

```
 # Next some EFI variables. These are used/created by pstore, but I've had them even though 
 #I deleted the pstore data using the above commands. YMMV.
 rm /sys/firmware/efi/efivars/dump-type0-*

```

This information was taken from [the Lenovo forums](http://forums.lenovo.com/t5/X-Series-ThinkPad-Laptops/x220-does-not-resume-from-sleep/m-p/1083233/highlight/false#M48825)

### Microphone

The x220 internal microphone has been the source of many complaints across platforms. Specifically, it can generate a lot of static or hissing on top of any recorded audio. The workaround is to mute the right mic input channel (in audio control programs that allow independent channel setting) or to drag the balance slider in a GUI for the internal mic level fully to the left.

Note also that the audio jack is a combination headset/mic jack and will work with modern smartphone headsets with inline microphones, as an alternative.

### Multi-monitor setups with X

Some window managers, such as [qtile](/index.php/Qtile "Qtile") or [awesome](/index.php/Awesome "Awesome") don't seem to get along with the `sna` acceleration method of the [intel](/index.php/Intel "Intel") driver, which results in tiled and broken display of the environments, when using a multi-monitor setup (using internal monitor only, works just fine).

[Switching to uxa](/index.php/Intel_graphics#SNA_issues "Intel graphics") fixes this [[1]](https://bbs.archlinux.org/viewtopic.php?pid=1706248#p1706248).

It seems, that this issue does not occur in other desktop environments, such as [Xfce](/index.php/Xfce "Xfce"), however.

### Backlight

Since `linux 3.16`, some backlight-related kernel parameter defaults have been changed, causing the hardware brightness up/down keys to no longer function automatically. This can be worked around by setting `acpi_osi`, e.g.

```
 acpi_osi="!Windows 2012"

```

in the [kernel parameters](/index.php/Kernel_parameters "Kernel parameters"). More details can be found on [the Backlight page](/index.php/Backlight#Kernel_command-line_options "Backlight").

### X220 Touchpad cursor jump/imprecise

If the touchpad is jumpy/imprecise, copy the two lines below into a new file:

 `/etc/udev/hwdb.d/90-libinput-x220-touchpad-fw81.hwdb` 
```
libinput:name:SynPS/2 Synaptics TouchPad:dmi:*svnLENOVO:*:pvrThinkPadX220*
 LIBINPUT_MODEL_LENOVO_X220_TOUCHPAD_FW81=1
```

then run `udevadm hwdb --update` and reboot.

See [Fedora bug #1264453](https://bugzilla.redhat.com/show_bug.cgi?id=1264453) for more details.

## See also

*   Arch user blogs about the X220
    *   [Thinkpad X220 model 4287CTO](http://natalian.org/archives/2011/11/10/Thinkpad_X220/) using a msata SSD for 64 bit Archlinux
    *   [X220 i5](http://blog.jamiek.it/2011/10/arch-linux-on-thinkpad-x220.html)
*   [Thinkwiki X220 reference](http://www.thinkwiki.org/wiki/Category:X220)
*   [Power saving options for the X220 - Notebook Review Forum](http://forum.notebookreview.com/lenovo-ibm/575569-linux-x220-29.html#post8075286)
*   [thinkpad-scripts](https://aur.archlinux.org/packages/thinkpad-scripts/) for ThinkPad X220 Tablet rotation, docking, etc scripts