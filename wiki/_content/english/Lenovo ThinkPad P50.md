The Lenvovo P50 is a quad core Intel Skylake Laptop.

## Contents

*   [1 Issues](#Issues)
    *   [1.1 Sluggish Graphics Performance with HD Graphics 530 (Skylake GT2)](#Sluggish_Graphics_Performance_with_HD_Graphics_530_.28Skylake_GT2.29)
        *   [1.1.1 High CPU chromium Bug](#High_CPU_chromium_Bug)
    *   [1.2 High Fan speed on low CPU load](#High_Fan_speed_on_low_CPU_load)
    *   [1.3 Prevent tap clicking while typing](#Prevent_tap_clicking_while_typing)

## Issues

### Sluggish Graphics Performance with HD Graphics 530 (Skylake GT2)

Running on tha native 4k Resolution Performance can appear Sluggish. This might improved in the UEFI BIOS by increasing the amout of RAM Intel Graphics should take from the DRAM from 256MB to the maximum 512MB.

#### High CPU chromium Bug

Chromium takes too long to even display the "new Tab" page with the small prevews and uses 100% cpu on all cores for several second if 5 to 6 new tabs get open simoultanously when using the Intel Graphics. This might be due to some hardware acceleration bug maybe related to: [Corruption/Unresponsiveness in Chromium and Firefox with Intel Graphics](/index.php/Intel_graphics#Corruption.2FUnresponsiveness_in_Chromium_and_Firefox "Intel graphics") but not tested yet. But it is simply enough to deactivate hardware acceleration in the chromium settings gui. Another workaround that seems to work with keeping hardware acceleration enabled is activating the flag

```
--ignore-gpu-blacklist

```

by creating the file ".config/chromium-flag" and adding the flag.

### High Fan speed on low CPU load

Even with just low CPU load and only a browser open the fan keeps to switch on and speed up to full power. This behaviour can be at least reduced a bit by only using Intel Graphics and completly powering down the NVIDIA optimus card that uses the same cooling system [Power down discrete GPU](/index.php/Hybrid_graphics#Fully_Power_Down_Discrete_GPU "Hybrid graphics").

### Prevent tap clicking while typing

The touchpad is very sensitive so it often happens that while typing the cursor is moved from unwanted clicks. Best solution is to deaktivate tap click for the touchpad and use the harware buttons.

This can be done either in the settings of your Grafical Desktop Enviroment (Gnome3 works after installing libinput drivers) or directly from the shell temporarely with:

```
synclient TapButton1=0

```

this change can be made permament by changing the Xorg configuration.