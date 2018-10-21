[Lattice Diamond](http://www.latticesemi.com/latticediamond) is a design software for Lattice FPGA architectures.

Arch Linux is not officially supported by [Lattice Diamond](http://www.latticesemi.com/), but as happens with other HDL suites like [Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK") or [Xilinx Vivado](/index.php/Xilinx_Vivado "Xilinx Vivado"), most of its features can be used with a bit of hacking.

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
    *   [2.1 Licensing](#Licensing)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Place & Route fails](#Place_.26_Route_fails)
    *   [3.2 Programming with FTDI cables doesn't work](#Programming_with_FTDI_cables_doesn.27t_work)
    *   [3.3 Diamond crashes when FTDI based serial interface exists on a Lattice starter kit](#Diamond_crashes_when_FTDI_based_serial_interface_exists_on_a_Lattice_starter_kit)

## Prerequisites

Lattice provides only 64-bit builds of the suite. So you will need a working 64-bit installation of Arch Linux.

## Installation

Just install [lattice-diamond](https://aur.archlinux.org/packages/lattice-diamond/). Note that the installation size is big (around 4 GB), so generating the package might take some time due to the compression stage. If you want to shorten building the package, edit the PKGBUILD file to avoid compressing it.

### Licensing

You can request a free license to [Lattice Semiconductor](http://www.latticesemi.com/Support/Licensing.aspx) (registration needed). These licenses are node-locked (tied to the MAC of your Ethernet card). Once you have the license file, copy it to `/usr/local/diamond/3.10_x64/license/license.dat`, or you will not be able to start the suite.

## Troubleshooting

### Place & Route fails

If Place & Route fails with message `ERROR - par: Switch "-msgsegset" is not allowed.`, try deleting the `promote.xml` file in the root directory of your project and launch it again. It should now run normally.

### Programming with FTDI cables doesn't work

Programming FPGAs with FTDI chip based cables will not work if `ftdi_sio` kernel module is loaded. **After** plugging the programmer run:

```
# rmmod ftdi_sio

```

Now the programmer should work until you re-attach it again (so you must run the command above every time the programmer is plugged).

### Diamond crashes when FTDI based serial interface exists on a Lattice starter kit

The "Lattice Diamond 3.9 Installation Notice for Linux" document describes how to manually setup the serial driver but naming the udev rule as explained in that document does not work. Below are the instructions that work.

1\. Find your username which is given in /etc/group file. Log out if required. For example :

username:x:1000:

2\. Create a working file called 51-lattice.rules.

3\. Add the following information to the 51-lattice.rules file:

1.  Lattice - from Lattice Diamond 3.9 Installation Notice for Linux p.20 and [https://github.com/jandob/lattice-diamond-archlinux](https://github.com/jandob/lattice-diamond-archlinux) showing a higher number used for the .rules file

SUBSYSTEM=="usb",ACTION=="add",ATTRS{idVendor}=="1134",ATTRS{idProduct}=="8001",MODE=="0660",GROUP=="username:x:1000:",SYMLINK+="lattice-%n"

1.  FTDI

SUBSYSTEM=="usb",ACTION=="add",ATTRS{idVendor}=="0403",ATTRS{idProduct}=="6010",MODE=="0666",GROUP=="username:x:1000:",SYMLINK+="ftdi-%n" SUBSYSTEM=="usb",ATTRS{idVendor}=="0403",ATTRS{idProduct}=="6010",RUN+="/bin/sh -c 'basename %p > /sys/bus/usb/drivers/ftdi_sio/unbind'"