# Lenovo ThinkPad T520

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Laptop/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo").**

**Notes:** please use the second argument of the template to provide more detailed indications. (Discuss in [Talk:Lenovo ThinkPad T520#](https://wiki.archlinux.org/index.php/Talk:Lenovo_ThinkPad_T520))

## Contents

*   [1 Installation](#Installation)
*   [2 Graphics](#Graphics)
    *   [2.1 Integrated Graphics](#Integrated_Graphics)
    *   [2.2 Discrete Graphics](#Discrete_Graphics)
    *   [2.3 NVidia Optimus](#NVidia_Optimus)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Screen freezes before login prompt when using discrete graphics](#Screen_freezes_before_login_prompt_when_using_discrete_graphics)

## Installation

Installation worked without further setting adjustments.

## Graphics

The BIOS option Display->Graphics Device can be switched to these settings:

### Integrated Graphics

Use this with the xf86-video-intel driver. The nvidia card will be turned off, which means that the system will consume less power and you will not have to worry about installing the nvidia drivers.

The integrated graphics is fast enough to run some older games. It is a good option if you do not use demanding 3D applications

A major disadvantage of this mode is that the DisplayPort will not work, because it is hardwired to the Nvidia card.

### Discrete Graphics

This will give you good consistent 3D performance in all applications, without having to worry about the complexities of bumblebee. It is also a good option if you want an easy way to connect and use a DisplayPort monitor.

You will not get the power-savings of running from the intel-gfx and turning the discrete nvidia card off. Another disadvantage is that you cannot use this mode to run tripple-head with 2 external Monitors on VGA and DP. This is a hardware limitation, the discrete-nvidia and integrated-intel card can both only drive at most 2 different screens each.

### NVidia Optimus

If you choose this option, set "OS Detection for NVIDIA Optimus" BIOS Option to Disabled.

See the [Bumblebee](/index.php/Bumblebee "Bumblebee") page for details on how to use both cards with linux.

## Troubleshooting

### Screen freezes before login prompt when using discrete graphics

If you are using GRUB2 bootmanager, its framebuffer graphics mode can cause problems later on in the boot process. See [GRUB2#Disable framebuffer](/index.php/GRUB2#Disable_framebuffer "GRUB2").

You might also try to set the nomodeset kernel commandline flags:

[Kernel mode setting#Disabling modesetting](/index.php/Kernel_mode_setting#Disabling_modesetting "Kernel mode setting")

Although, currently (Oct 2013, kernel 3.11.6), my T520 boots in "Discrete Graphics" mode only when i disable the GRUB2 framebuffer, but **do not** set any of the nomodeset kernel options.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T520&oldid=412568](https://wiki.archlinux.org/index.php?title=Lenovo_ThinkPad_T520&oldid=412568)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Lenovo](/index.php/Category:Lenovo "Category:Lenovo")