In this page, i'll try to make your Arch installation on HP Pavillion dv1000 series as easy as i can, If you have something to add please contribute to this page

## Contents

*   [1 What does work?](#What_does_work.3F)
*   [2 What does not work?](#What_does_not_work.3F)
*   [3 Installation](#Installation)
*   [4 Configurations](#Configurations)
    *   [4.1 Graphic Card and Xorg](#Graphic_Card_and_Xorg)
*   [5 Modules](#Modules)
    *   [5.1 Wireless](#Wireless)
    *   [5.2 Sound](#Sound)
*   [6 External Links](#External_Links)

## What does work?

Wifi using ipw2200 drivers

Touchpad using synaptics drivers

Remote Control, when you'll have ur multimedia keys working, Remote control works out of the box

suspend to ram/swap

Texas Intrument card reader

## What does not work?

# Installation

Boot with your Arch CD without any option, u do not need acpi=off for this laptop, Partition the way you like but leave 204MB+ of free space **unpartioned** in order to install Quickplay later, You may need to follow any Installation guide on the wiki

# Configurations

## Graphic Card and Xorg

See [Intel graphics](/index.php/Intel_graphics "Intel graphics").

# Modules

## Wireless

You have to use the `ipw2200` driver; Arch stock kernel has it enabled, but you still need the firmware package [ipw2200-fw](https://www.archlinux.org/packages/?name=ipw2200-fw).

## Sound

The sound should work out of the box.

# External Links

*   [A Linux compatibility guide to the HP Pavillion DV1000 series](http://www.linlap.com/wiki/HP+Pavilion+dv1000)
*   This report is listed at the [Linux Laptop and Notebook Installation Guides Survey: Hewlett-Packard - HP](http://tuxmobil.org/hp.html).