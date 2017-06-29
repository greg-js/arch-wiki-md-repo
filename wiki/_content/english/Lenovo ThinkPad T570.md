## Contents

*   [1 Installation](#Installation)
*   [2 Configuration](#Configuration)
    *   [2.1 CPU](#CPU)
    *   [2.2 Bumblebee](#Bumblebee)

## Installation

Use the [Installation](/index.php/Installation "Installation") guide. Make sure that Secure Boot is disable in BIOS Setup.

## Configuration

### CPU

Install [this BIOS update](http://pcsupport.lenovo.com/de/de/downloads/ds120370) (or a newer one) to fix a [serious bug concerning hyperthreading](https://lists.debian.org/debian-devel/2017/06/msg00308.html).

### Bumblebee

[Until bbswitch is updated to support the new power management method](/index.php/Bumblebee#Broken_power_management_with_kernel_4.8 "Bumblebee"), add `pcie_port_pm=off` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").