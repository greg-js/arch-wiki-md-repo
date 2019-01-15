Thunderbolt 3 works out of the box with recent Linux kernel versions. The Linux kernel, starting with version 4.13, supports Thunderbolt Security, too.

## Thunderbolt Security

Modern Thunderbolt devices implement security modes that require user authorization when connecting devices - this is to protect from malicious devices performing [DMA attacks](https://en.wikipedia.org/wiki/DMA_attack) or otherwise interfering with the hardware (see [Thunderstrike 2](https://trmm.net/Thunderstrike_2)).

The modes currently supported on Linux are:

*   `none` - no security, all devices are connected and initialized by default
*   `user` - user authorization is required every time a device is connected
*   `secure` - user authorization is required, but the device is then remembered and does not require re-authorization
*   `dponly` - DisplayPort functionality only, no other devices are allowed

The security level is normally configured at firmware level; it's recommended to set it to at least `secure`.

GNOME has native support for authorizing devices from the UI since version 3.30; Plasma integration is in the works ([[1]](https://phabricator.kde.org/T9012), [[2]](https://bugs.kde.org/show_bug.cgi?id=395304)). Users in other environments can use [bolt](https://www.archlinux.org/packages/?name=bolt) or [tbt](https://aur.archlinux.org/packages/tbt/) to authorize devices.

## See also

*   [bolt GitHub page](https://github.com/gicmo/bolt)
*   [Introducing bolt: Thunderbolt 3 security levels for GNU/Linux](https://christian.kellner.me/2017/12/14/introducing-bolt-thunderbolt-3-security-levels-for-gnulinux/)
*   [Tunderbolt Support in GNOME](https://christian.kellner.me/2018/04/23/the-state-of-thunderbolt-3-in-fedora-28/)
*   [tbtadm](https://daenney.github.io/2017/11/16/linux-thunberbolt-security)