Thunderbolt 3 works out of the box with recent Linux kernel versions [[1]](https://www.kernel.org/doc/html/latest/admin-guide/thunderbolt.html). The Linux kernel, starting with version 4.13, supports Thunderbolt Security, too.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Obtain firmware updates](#Obtain_firmware_updates)
*   [2 User device authorization](#User_device_authorization)
    *   [2.1 Graphical front-ends](#Graphical_front-ends)
    *   [2.2 Automatically connect any device](#Automatically_connect_any_device)
    *   [2.3 Forcing power](#Forcing_power)
*   [3 See also](#See_also)

## Obtain firmware updates

Manufacturers often release firmware updates for Thunderbolt ports and devices to function properly, visit [https://thunderbolttechnology.net/updates](https://thunderbolttechnology.net/updates) for more details how to obtain upgrades for certain vendors.

**Note:** Some vendors use [fwupd](/index.php/Fwupd "Fwupd") to push firmware updates on Linux.

## User device authorization

Modern Thunderbolt devices implement security modes that require user authorization when connecting devices - this is to protect from malicious devices performing [DMA attacks](https://en.wikipedia.org/wiki/DMA_attack "wikipedia:DMA attack") or otherwise interfering with the hardware (see [Thunderstrike 2](https://trmm.net/Thunderstrike_2)).

The modes currently supported on Linux are:

*   `none` - No security, all devices are connected and initialized by default. In BIOS settings this is typically called *Legacy mode*.
*   `user` - User authorization is required every time a device is connected. In BIOS settings this is typically called *Unique ID*.
*   `secure` - User authorization is required, but the device is then remembered and does not require re-authorization. In BIOS settings this is typically called *One time saved key*.
*   `dponly` - DisplayPort functionality only, no other devices are allowed. In BIOS settings this is typically called *Display Port Only*.

The security level is normally configured at firmware level; it is recommended to set it to at least `secure`.

**Tip:** User-space solutions are available such as [bolt](https://www.archlinux.org/packages/?name=bolt) or [tbt](https://aur.archlinux.org/packages/tbt/) to authorize devices.

### Graphical front-ends

*   [GNOME](/index.php/GNOME "GNOME") has native support for authorizing devices from the UI since version 3.30
*   [Plasma](/index.php/Plasma "Plasma") integration is available from this [git repository](https://cgit.kde.org/plasma-thunderbolt.git/tree/README.md) and from [plasma-thunderbolt](https://www.archlinux.org/packages/?name=plasma-thunderbolt) package

### Automatically connect any device

Users who just want to connect any device without any sort of manual work can create a [udev rule](/index.php/Udev#About_udev_rules "Udev") as in `99-removable.rules`:

 `/etc/udev/rules.d/99-removable.rules`  `ACTION=="add", SUBSYSTEM=="thunderbolt", ATTR{authorized}=="0", ATTR{authorized}="1"` 

### Forcing power

Many OEMs include a method that can be used to force the power of a Thunderbolt controller to an *On* state. If supported by the machine this will be exposed by the WMI bus with a sysfs attribute called *force_power* [[2]](https://www.kernel.org/doc/html/latest/admin-guide/thunderbolt.html#forcing-power).

Forcing power may especially be useful when a connected device loses connection or the controller that switches itself off.

To force the power to be on/off, write 1 or 0 to this attribute, e.g. to force power:

```
# echo 1 > /sys/bus/wmi/devices/86CCFD48-205E-4A77-9C48-2021CBEDE341/force_power

```

**Note:** It is not possible to query the current `force_power` state.

## See also

*   [Linux kernel user's and administrator's guide on Thunderbolt](https://www.kernel.org/doc/html/latest/admin-guide/thunderbolt.html)
*   [bolt GitHub page](https://github.com/gicmo/bolt)
*   [Introducing bolt: Thunderbolt 3 security levels for GNU/Linux](https://christian.kellner.me/2017/12/14/introducing-bolt-thunderbolt-3-security-levels-for-gnulinux/)
*   [Tunderbolt Support in GNOME](https://christian.kellner.me/2018/04/23/the-state-of-thunderbolt-3-in-fedora-28/)
*   [tbtadm](https://daenney.github.io/2017/11/16/linux-thunberbolt-security)