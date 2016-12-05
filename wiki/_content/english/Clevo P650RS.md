The P650RS is a device by the taiwanese OEM manufacturer Clevo. It is also sold as Sager NP8153-S and many other names. The hardware is configurable and includes an Intel Skylake Core i7, NVIDIA 1070M graphics, USB-C connectors, a fingerprint reader, mini DisplayPort as well as HDMI connections, and more.

## Contents

*   [1 Installation](#Installation)
*   [2 Graphics](#Graphics)
    *   [2.1 Switchable / Optimus](#Switchable_.2F_Optimus)
    *   [2.2 Discrete only](#Discrete_only)
*   [3 Power management](#Power_management)
*   [4 WiFi](#WiFi)
*   [5 Webcam](#Webcam)

## Installation

Installing Archlinux requires kernel parameter `nouveau.modeset=0`.

**Tip:** This kernel parameter needs to be kept for the final installation until the proprietary driver is installed or nouveau gains better support for this card.

## Graphics

This laptop has switchable graphics, but the BIOS includes an option to disable the integrated card. These instructions apply to the switchable configuration, i.e. `MSHYBRID` in BIOS.

### Switchable / Optimus

Xorg may not work out of the box with a `no screens found` error.

Xorg selects the dGPU when in fact it's the integrated one that has the control of the screen. This is probably an issue only fixable with a BIOS update (testing against v1.05.03, it won't work).

To overcome this a xorg configuration file needs to be created telling xorg the correct address and driver combination. This can be done by creating (or adding the line with `BusID` in:

 `/etc/X11/xorg.conf.d/20-intel.conf` 
```
Section "Device"
        Identifier "Intel Graphics"
        Driver     "intel"
        BusID      "PCI:x:x:x"    # <<<< replace with correct address
EndSection

```

Details and further advice can be found in pages [Intel_graphics](/index.php/Intel_graphics "Intel graphics") and [Xorg](/index.php/Xorg "Xorg").

This will yield a working setup, but the dGPU will not be useable at all and will still be on and consuming quite a lot of energy.

To enable the use of the dedicated graphics card see [Bumblebee](/index.php/Bumblebee "Bumblebee").

**Note:** Automatic turn off of dGPU through [bbswitch](https://www.archlinux.org/packages/?name=bbswitch) will not work with current version. This is a known issue, see [Bumblebee#Broken_power_management_with_kernel_4.8s](/index.php/Bumblebee#Broken_power_management_with_kernel_4.8s "Bumblebee") for details. Insisting on using it may result in a hang boot.

All DisplayPort and HDMI ports seem to be connected to the dGPU which involves extra steps to get them working.

### Discrete only

Given this laptop has a mux, it does not require PRIME configuration to make use of the dedicated graphics card in full even though it should be possible. Installation should follow [NVIDIA](/index.php/NVIDIA "NVIDIA") after setting and booting with `DISCRETE` BIOS option.

Using the NVIDIA proprietary driver (testing with 375.20) the backlight may not come back on after the display has gone to sleep. A workaround is to drop to console (e.g. Ctrl-Alt-F2) and then back to X.

## Power management

Using switchable graphics and standard [TLP](/index.php/TLP "TLP") configuration, this laptop should manage ~10-14W of static load. YMMV of course.

The dGPU cannot be turned off automatically as a function of being in use at this moment though (see [#Switchable / Optimus](#Switchable_.2F_Optimus)). If left on, the system will take >20W on idle though.

You can combine functionality and power managment by using TLP and no bbswitch:

*   Boot in battery mode: Bumblebee cannot turn dGPU on and fails to load driver.
*   Boot in AC mode: Bumblebee works fine. dGPU will not turn off and subsequent use of optirun in battery mode works at the expense of no power management. Low power mode is possible after a reboot.

**Tip:** Always boot in AC to maximize functionality and reboot after using the dGPU for lower power consumption.

## WiFi

WiFi seems to work well and coexist nicely with bluetooth. Consider enabling antenna aggregation to take the most out of the hardware: [iwlwifi](/index.php/Wireless_network_configuration#iwlwifi "Wireless network configuration").

The `Fn+F11` combination to toggle air plane mode doesn't work.

## Webcam

As with the [Clevo W840SU](/index.php/Clevo_W840SU "Clevo W840SU") the webcam must be activated with `Fn-F10` before it will show up in the device list. This survives a reboot.