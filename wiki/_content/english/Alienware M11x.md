This wiki page documents the configuration and troubleshooting specific to the Alienware M11x laptop.

See the [Installation guide](/index.php/Installation_guide "Installation guide") for installation instructions.

## Contents

*   [1 Wireless](#Wireless)
*   [2 Sound](#Sound)
*   [3 Touchpad](#Touchpad)
*   [4 Video](#Video)
    *   [4.1 Bumblebee](#Bumblebee)
    *   [4.2 ACPI_CALL](#ACPI_CALL)
        *   [4.2.1 acpi_call Usage](#acpi_call_Usage)
        *   [4.2.2 m11rx2hack](#m11rx2hack)
        *   [4.2.3 m11rx3hack](#m11rx3hack)
    *   [4.3 VGA_SWITCHEROO](#VGA_SWITCHEROO)
    *   [4.4 Backlight Brightness](#Backlight_Brightness)
        *   [4.4.1 /sbin/backlight](#.2Fsbin.2Fbacklight)
    *   [4.5 Other applications](#Other_applications)

## Wireless

The Broadcom Corporation Device 4353 (rev 01)([14e4](http://wireless.kernel.org/en/users/Drivers/b43#Known_PCI_devices):[4353](http://www.aircrack-ng.org/doku.php?id=b43)) 802.11a/b/g/n MIMO adapter is the stock wireless device for the M11x (R1).

See [Broadcom wireless](/index.php/Broadcom_wireless "Broadcom wireless").

## Sound

Works out-of-the-box. See [ALSA](/index.php/ALSA "ALSA").

## Touchpad

See [Synaptics](/index.php/Synaptics "Synaptics").

## Video

**- For Alienware M11x R1 owners:** The Alienware M11x R1 has 2 video cards, and can be manually changed with the **system BIOS** (accessed by pushing **F2** during system POST) ::

*   *Switchable* => Linux will use the Intel 4500HD internal video
*   *Discrete* => Linux will use the NVIDIA GeForce GT 335M

Alienware M11x R1 users running Linux have some tools available which will interact with the hybrid video cards in this laptop.

*   [Bumblebee](/index.php/Bumblebee "Bumblebee") is a software implementation based on VirtualGL and a kernel driver to be able to use the dedicated GPU. Alienware M11x R1 users CAN use this method to switch between the Onboard/Intel and the Discrete/NVIDIA without a system reboot and/or BIOS change (yet the BIOS would need to be set for *Switchable*).
*   [acpi_call](http://github.com/mkottman/acpi_call) allows you to disable+power down the Discrete/NVIDIA card when the system is booted while BIOS Graphics mode is set to => *Switchable*
*   [vga_switcheroo](http://people.freedesktop.org/~airlied/vgaswitcheroo/) allows one to switch between the Onboard/Intel and the Discrete/NVIDIA without a system reboot and/or BIOS change (yet the BIOS would need to be set for *Switchable*). [vga_switcheroo](http://people.freedesktop.org/~airlied/vgaswitcheroo/) has been reported as non-functional at this state for Alienware M11x users.

[linux-hybrid-graphics.blogspot.com](http://linux-hybrid-graphics.blogspot.com/) is a great site to check out for up-to-date information regarding the state of hybrid graphics in Linux.

**- For Alienware M11x R2 owners:** There are [detailed instructions on how to switch on/off the discrete NVIDIA graphics card on the Optimus (R2) models for the Alienware M11x laptop.](http://linux-hybrid-graphics.blogspot.com/2010/10/howto-allienware-m11x-r2-nvidia-optimus.html)

**- For Alienware M11x R3 owners:** Many of the methods for running Optimus & bumblebeed on the M11xR3 are the same or similar to the M11xR2 however the acpi calls are different for this model.

### Bumblebee

> Bumblebee is a solution to Nvidia Optimus hybrid-graphics technology allowing to use the dedicated graphics card for rendering. It was started by Martin Juhl.

See [Bumblebee](/index.php/Bumblebee "Bumblebee") for details.

### ACPI_CALL

[ACPI_CALL](http://github.com/peberlein/acpi_call) is a kernel module that enables you to call parameterless ACPI methods by writing the method name to `/proc/acpi/call`, e.g. to turn off the discrete graphics card in a dual graphics environment. acpi_call works on the Alienware M11x R1 for disabling the discrete video card + powering it down successfully. Make sure you boot with BIOS set to *switchable' ::*

*   Grab the [acpi_call-git AUR package](https://aur.archlinux.org/packages.php?ID=39470)(IMHO it is working pretty stable), and skip the manual installation/compilation of acpi_call.
    *   OR you can grab [acpi_call](http://github.com/mkottman/acpi_call) and compile manually. Please see the [acpi_call](http://github.com/mkottman/acpi_call) site for details on compilation if you wish to compile manually.

#### acpi_call Usage

```
# modprobe acpi_call
# grep rate /proc/acpi/battery/BAT1/state
# echo '\_SB.PCI0.P0P2.PEGP._OFF' > /proc/acpi/call
# grep rate /proc/acpi/battery/BAT1/state

```

1.  Modprobe the acpi_call module
2.  Check the current battery mW usage (not necessary)
3.  Echo '\_SB.PCI0.P0P2.PEGP._OFF' to (the **now existing** since acpi_call was loaded) /proc/acpi/call
4.  Check the current battery mW usage again to see that it dropped (not necessary)

*   Both #2 and #4 as noted are *not necessary*, they just demonstrate that the battery usage is dropping as long as you do them in the order listed here.

#### m11rx2hack

[http://forums.fedoraforum.org/showpost.php?p=1402584&postcount=45](http://forums.fedoraforum.org/showpost.php?p=1402584&postcount=45)

#### m11rx3hack

```
#!/bin/sh
# Based on m11xr2hack by George Shearer

if ! lsmod | grep -q acpi_call; then
echo "Error: acpi_call module not loaded"
exit
fi

acpi_call () {
echo "$*" > /proc/acpi/call
cat /proc/acpi/call
}

case "$1" in
off)
echo NVOP $(acpi_call "\_SB.PCI0.PEG0.PEGP.NVOP 0 0x100 0x1A {255,255,255,255}")
echo _PS3 $(acpi_call "\_SB.PCI0.PEG0.PEGP._PS3")
;;
on)
echo _PS0 $(acpi_call "\_SB.PCI0.PEG0.PEGP._PS0")
;;
*)
echo "Usage: $0 [on|off]"
;;
esac

```

### VGA_SWITCHEROO

Currently, Alienware M11x R1 owner reports indicate the [vga_switcheroo](http://people.freedesktop.org/~airlied/vgaswitcheroo/) method is not functional.

This explains how-to use VGA_SWITCHEROO for troubleshooting ::

*   kernel configuration flag - ensure **CONFIG_VGA_SWITCHEROO** is set as module, or built-in :: **CONFIG_VGA_SWITCHEROO**=*y*/*m*

```
sudo modprobe vgaswitcheroo
sudo mount -t debugfs none /sys/kernel/debug
cd /sys/kernel/debug/vgaswitcheroo
cat switch
  0:+:Pwr:0000:00:02.0
  1: :Pwr:0000:01:00.0

```

`echo "DDIS" > /sys/kernel/debug/vgaswitcheroo/switch` <= switch to discrete card
`echo "DIGD" > /sys/kernel/debug/vgaswitcheroo/switch` <= switch to onboard card
`echo "OFF" > /sys/kernel/debug/vgaswitcheroo/switch` <= power-down the card not in use

Use 'nvidia-settings' to configure the video card, and multiple screens if using the discrete/NVIDIA card.

### Backlight Brightness

*   When booting into Arch Linux using NVIDIA/discrete video card just change brightness using the FUNCTION+F4 = brightness up, and FUNCTION+F5 = brightness down - also 'nvidia-settings' should allow brightness settings changes too.

*   When booting into Arch Linux using the INTEL/onboard video card, the only way to change brightness levels requires passing a command through 'setpci', the following script is adapted from [Samsung_N150-Backlight ArchWiki article](/index.php/Samsung_N150#Backlight "Samsung N150") works fine (ymmv). **REQUIREMENTS:** ***`bc`***, and ***`setpci`***

1.  create a file @ `/sbin/backlight`
2.  `sudo chown root:video /sbin/backlight`
3.  `sudo chmod 750 /sbin/backlight`
4.  make sure to add the username allowed to change the backlight settings to the **video** group in `/etc/group`
5.  create an alias in your shell startup, and turn the brightness up or down via command, in turn you could tie this to a button combination in your xwindow manager settings.

	.bashrc

```
alias brup='/sbin/backlight up'
alias brdown='/sbin/backlight down'
alias brget='/sbin/backlight get'

```

	.tcshrc

```
alias brup '/sbin/backlight up'
alias brdown '/sbin/backlight down'
alias brget '/sbin/backlight get'

```

#### /sbin/backlight

```
#!/bin/bash
# increase/decrease/set/get the backlight brightness (range 0-255) by 16
#
#get current brightness in hex and convert to decimal
#
# REQUIRES: bc, and setpci
var1=`sudo /usr/sbin/setpci -s 00:02.0 F4.B`
var1d=$((0x$var1))
 case "$1" in
       up)
              #calculate new brightness
              var2=`echo "ibase=10; obase=16; a=($var1d+16);if (a<255) print a else print 255" | bc`
              echo "$0: increasing brightness from 0x$var1 to 0x$var2"
              sudo /usr/sbin/setpci -s 00:02.0 F4.B=$var2
              ;;
       down)
              #calculate new brightness
              var2=`echo "ibase=10; obase=16; a=($var1d-16);if (a>15) print a else print 15" | bc`
              echo "$0: decreasing brightness from 0x$var1 to 0x$var2"
              sudo /usr/sbin/setpci -s 00:02.0 F4.B=$var2
              ;;
       set)
              #n.b. this does allow "set 0" i.e. backlight off
              echo "$0: setting brightness to 0x$2"
              sudo /usr/sbin/setpci -s 00:02.0 F4.B=$2
              ;;
       get)
              echo "$0: current brightness is 0x$var1"
              ;;
       toggle)
              if [ $var1d -eq 0 ] ; then
                      echo "toggling up"
                      sudo /usr/sbin/setpci -s 00:02.0 F4.B=FF
              else
                      echo "toggling down"
                      sudo /usr/sbin/setpci -s 00:02.0 F4.B=0
              fi
              ;;
       *)
              echo "usage: $0 {up|down|set <val>|get|toggle}"
              ;;
 esac
exit 0

```

### Other applications

*   A C-program which cycles through colors, plus information about how to understand it, can be found at [[1]](http://www.dettus.net/alienware).

*   [alienware-kbl](https://rafael.senties-martinelli.com/software/alienware-kbl) a software to manage the light colors with a graphical interface, python or bash commands.