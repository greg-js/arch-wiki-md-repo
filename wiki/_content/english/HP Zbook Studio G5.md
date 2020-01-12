The HP Zbook Studio G5 is a workstation replacement laptop.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Installation](#Installation)
    *   [1.1 Booting from live media](#Booting_from_live_media)
*   [2 Configuration](#Configuration)
    *   [2.1 Touchpad](#Touchpad)
    *   [2.2 Thunderbolt](#Thunderbolt)
    *   [2.3 Graphics rendering](#Graphics_rendering)
    *   [2.4 External monitors](#External_monitors)
        *   [2.4.1 Bumblebee](#Bumblebee)
    *   [2.5 Suspend/Hibernate/Resume](#Suspend/Hibernate/Resume)

## Installation

Installation is generally pretty straight forward, however, there are some things to consider. Follow the general instructions of the [installation|guide](/index.php/Installation_guide "Installation guide")

### Booting from live media

The laptop does not boot with Nouveau graphics therefore, add this to the grub options

```
 i915.modeset=1
 nouveau.modeset=0

```

Edit: I (a different user) found that laptop booted fine with no tweaks for the Manjaro live media, and also had an initially functional display without these options, when using Discrete graphics mode in BIOS per the original recommendation on this page. That led to nVidia being only GPU visible to OS, and nouveau the selected driver. But then the problem is OS can't see Intel GPU, no i915, etc... ultimately no functionality for video after resuming from suspend/hibernate. So if you want Intel GPU, it first must be enabled in BIOS (Hybrid graphics) and it seems modeset must be enabled for i915, and disabled for nouveau. In short, the recommended configs here are good for regular install too- not just live media. But Nouveau can be made to work with major caveats (e.g. no video after resume).

## Configuration

### Touchpad

You will have to disable i2c-hid to get the touchpad to work after resuming from suspend/hibernate (default install without this blacklist worked for at least one person prior to using suspend/hibernate, but after resuming, the problem manifests itself). This forces a fallback to the ps2 drivers. Create a file containing "blacklist i2c_hid" (e.g. "i2c.conf") in the modprobe.d directory (/etc/modprobe.d/) to disable it.

```
 blacklist i2c_hid

```

save & reboot.

edit: a friendlier name for the file (to remember why it's there) might be something like /etc/modprobe.d/make-touchpad-work-after-resume.conf

### Thunderbolt

Since the Zbook does not allow a no security option for Thunderbolt in the bios, a thunderbolt manager has to be installed see [bolt](https://www.archlinux.org/packages/?name=bolt).

### Graphics rendering

Use "Discrete" graphics in the bios. Auto and Hybrid was showing a blank screen. Installing nvidia drivers on discrete graphics worked flawlessly.

Edit: "Discrete" graphics in BIOS disables the onboard Intel GPU, so it's not seen in output of inxi -Gxx, and any features you are intending to configure with the i915 module won't work. To get around this, try using "Hybrid" graphics mode in BIOS (which leaves both Intel GPU and vNvidia GPU visible to the OS). This works perfectly (and fixed a problem I had with black screen after resume from suspend or hibernate) when only using the laptop screen. Wanted to get the bare laptop working correctly before I delve into tuning bumblebee and the nVidia driver for external monitors. I will update my recommendation in this section if I have problems there.

### External monitors

All external displays are routed to the Nvidia gpu. The internal display is routed to the internal Intel gpu therefore, Nvidia drivers or nouveau has to be installed to use external displays.

```
 # pacman -S nvidia

```

#### Bumblebee

To make use of both the onboard graphics and the Nvidia gpu, install bumblebee (and add user to bumblebee group and systemctl start bumblebeed.service). For an output on the ports connected to the Nvidia chip, the chip always needs to be powered on. To do this change the following options in bumblebee.conf file in /etc/bumblebee.

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

### Suspend/Hibernate/Resume

Make sure that BIOS has Hybrid enabled (not Discrete) if you want to use the onboard Intel GPU with i915 module. Follow guidance to enable early KMS for Intel (i915) module. I didn't test without it, but a recommendation to also include intel_agp is functional on my laptop. I didn't test without it. So I have the following line in /etc/mkinitcpio.conf: MODULES="intel_agp i915"

This appears to have resolved my issues with suspend/hibernate/resume, at least when external monitors are not part of the picture.