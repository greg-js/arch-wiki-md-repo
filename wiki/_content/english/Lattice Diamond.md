ArchLinux is not officially supported by Lattice Diamond, but as happens with other HDL suites like [Xilinx ISE WebPACK](/index.php/Xilinx_ISE_WebPACK "Xilinx ISE WebPACK") or [Xilinx Vivado](/index.php/Xilinx_Vivado "Xilinx Vivado"), most of its features can be used with a bit of hacking.

## Contents

*   [1 Prerequisites](#Prerequisites)
*   [2 Installation](#Installation)
    *   [2.1 Licensing](#Licensing)
*   [3 Troubleshooting](#Troubleshooting)
    *   [3.1 Place & Route fails](#Place_.26_Route_fails)
    *   [3.2 Programming with FTDI cables doesn't work](#Programming_with_FTDI_cables_doesn.27t_work)

## Prerequisites

Currently, the available AUR package, works only for the 64-bit version of the suite. So you will need a working 64-bit installation of Arch Linux.

## Installation

Just install [lattice-diamond](https://aur.archlinux.org/packages/lattice-diamond/). Note that the installation size is big (around 4 GB), so generating the package might take some time due to the compression stage. If you want to shorten building the package, edit the PKGBUILD file to avoid compressing it.

### Licensing

You can request a free license to [Lattice Semiconductor](http://www.latticesemi.com/licenseprocessing/flexlmlicense.cfm?p=diamond&api=true) (registration needed). These licenses are node-locked (tied to the MAC or your Ethernet card). Once you have the license file, copy it to `/usr/local/diamond/3.7_x64/license/license.dat`, or you will not be able to start the suite.

## Troubleshooting

### Place & Route fails

If Place & Route fails with message `ERROR - par: Switch "-msgsegset" is not allowed.`, try deleting the `promote.xml` file in the root directory of your project and launch it again. It should now run normally.

### Programming with FTDI cables doesn't work

Programming FPGAs with FTDI chip based cables will not work if `ftdi_sio` kernel module is loaded. **After** plugging the programmer run:

```
# rmmod ftdi_sio

```

Now the programmer should work until you re-attach it again (so you must run the command above every time the programmer is plugged).