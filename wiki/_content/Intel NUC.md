# Intel NUC

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[Next Unit of Computing (NUC)](https://en.wikipedia.org/wiki/Next_Unit_of_Computing) is a small-form-factor (SFF) PC designed by Intel. Its first generation is based on the Sandy Bridge Celeron CPU. Its second-generation CPU is based on the Ivy Bridge Core i3 and Core i5 processors. Its third generation is based on the Haswell architecture. Its motherboard measures 4 × 4 inches (10.16 × 10.16 cm).

The barebone kits consist of the board, in a plastic case with a fan, an external power supply and VESA mounting plate. Intel does offer for sale just the NUC motherboards, which have a built-in CPU, although (as of 2013) the price of a NUC motherboard is very close to the corresponding cased kit; third-party cases for the NUC boards are also available.

## Contents

*   [1 Installation](#Installation)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 NUC brick-by-suspend issue](#NUC_brick-by-suspend_issue)
*   [3 Resources](#Resources)

## Installation

Follow usual [installation guide](/index.php/Installation_guide "Installation guide") procedures.

It is highly recommended to update the board BIOS prior to installation. See [official Intel BIOS update instructions](https://www-ssl.intel.com/content/www/us/en/support/boards-and-kits/000005636.html) for details.

## Troubleshooting

### NUC brick-by-suspend issue

**Warning:** There is a widely reported issue [[1]](https://communities.intel.com/thread/96168)[[2]](https://communities.intel.com/thread/93211)[[3]](https://www.reddit.com/r/intelnuc/comments/408rai/intel_nucs_getting_bricked_after_linux_sleep/) where Intel NUCs running Linux can become bricked by going into [sleep, suspend and/or hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate"). The source of this issue in unclear but according to some reports Arch Linux is affected as well.

The current recommended workaround is to never wake up the NUC from hibernation via the power button but only through alternative means such as wake-on-LAN or wake-on-USB.

If your NUC has become bricked, it might be possible to restore it by momentarily disconnecting the CMOS battery on the bottom side of the motherboard.

## Resources

*   [Official Intel NUC Support Community](https://communities.intel.com/community/tech/nuc)

Retrieved from "[https://wiki.archlinux.org/index.php?title=Intel_NUC&oldid=416140](https://wiki.archlinux.org/index.php?title=Intel_NUC&oldid=416140)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Mainboards and BIOS](/index.php/Category:Mainboards_and_BIOS "Category:Mainboards and BIOS")