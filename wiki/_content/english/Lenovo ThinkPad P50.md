The Lenvovo P50 is a quad core Intel Skylake Laptop.

## Issues

### Sluggish Graphics Performance with HD Graphics 530 (Skylake GT2)

Running on tha native 4k Resolution Performance appears Sluggish and even opening/scrolling Website Tabs can appear a bit delayed. However this can be improved in the UEFI BIOS by increasing the amout of RAM Intel Graphics should take from the DRAM from 256MB to the maximum 512MB.

### Prevent tap clicking while typing

The touchpad is very sensitive so it often happens that while typing the cursor is moved from unwanted clicks. Best solution is to deaktivate tap click for the touchpad and use the harware buttons.

This can be done either in the settings of your Grafical Desktop Enviroment (Gnome3 works after installing libinput drivers) or directly from the shell temporarely with:

```
synclient TapButton1=0

```

this change can be made permament by changing the Xorg configuration.