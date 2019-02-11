The HP Zbook Studio G5 is a workstation replacement laptop.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Booting from live media](#Booting_from_live_media)
*   [2 Configuration](#Configuration)
    *   [2.1 Touchpad](#Touchpad)
    *   [2.2 Thunderbolt](#Thunderbolt)
    *   [2.3 External monitors](#External_monitors)
        *   [2.3.1 Bumblebee](#Bumblebee)

## Installation

Installation is generally pretty straight forward, however, there are some things to consider. Follow the general instructions of the [installation|guide](/index.php/Installation_guide "Installation guide")

### Booting from live media

The laptop does not boot with Nouveau graphics therefore, add this to the grub options

```
 i915.modeset=1
 nouveau.modeset=0

```

## Configuration

### Touchpad

You will have to disable i2c-hid to get the touchpad to work, this forces a fallback to the ps2 drivers. Create a file containing "blacklist i2c_hid" (e.g. "i2c.conf") in the modprobe.d directory (/etc/modprobe.d/) to disable it.

```
 blacklist i2c_hid

```

save & reboot.

### Thunderbolt

Since the Zbook does not allow a no security option for Thunderbolt in the bios, a thunderbolt manager has to be installed see [bolt](https://www.archlinux.org/packages/?name=bolt).

### External monitors

All external displays are routed to the Nvidia gpu. The internal display is routed to the internal Intel gpu therefore, Nvidia drivers or nouveau has to be installed to use external displays.

```
 # pacman -S nvidia

```

#### Bumblebee

To make use of both the onboard graphics and the Nvidia gpu, install bumblebee. For an output on the ports connected to the Nvidia chip, the chip always needs to be powered on. To do this change the following options in bumblebee.conf file in /etc/bumblebee.

```
 KeepUnusedXServer=true

```

```
 [driver-nvidia]
 PMMethod=none

```

This prevents the nvidia chip from powering off after turning on. Next in xorg.conf.nvidia edit the following:

```
 Option      "AutoAddDevices" "true"

```

```
 Option "UseEDID" "true"
 Option "AllowEmptyInitialConfiguration"
 #Option "UseDisplayDevice" "none"

```

Next a virtual output needs to be added to the intel gpu. Change to the /etc/X11/xorg.conf.d folder and edit or create an entry for the intel gpu (e.g. 20-intel.conf).

```
 Section "Device"
     Identifier "intelgpu0"
     Driver "intel"
     Option "VirtualHeads" "1"
 EndSection

```

Thats all the configuration, now to enable external monitor:

```
 $ optirun true
 $ intel-virtual-output

```

*   recommended to put this in a script and create a desktop entry or similar to quickly enable the external display(s).