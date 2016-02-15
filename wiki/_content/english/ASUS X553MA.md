This article covers configuration specific to this laptop's hardware.

| **Device** | **Status** | **Kernel modules** | **X.org modules** |
| Bluetooth adapter | Does not work | wl |
| GPU | Works | i915 | intel_drv |
| Touchpad | Works | psmouse | synaptics_drv |
| Wireless NIC | Works | wl |

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Bluetooth adapter](#Bluetooth_adapter)
    *   [1.2 GPU](#GPU)
    *   [1.3 Touchpad](#Touchpad)
    *   [1.4 Wireless NIC](#Wireless_NIC)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 ACPI](#ACPI)
        *   [2.1.1 Laptop freezes on boot](#Laptop_freezes_on_boot)

## Hardware

### Bluetooth adapter

Installing the [Broadcom wireless#broadcom-wl](/index.php/Broadcom_wireless#broadcom-wl "Broadcom wireless") driver will not help and the Bluetooth adapter is essentially inoperational.

### GPU

GPU has kernel support and works out of the box.

For X.org drivers, [install](/index.php/Install "Install") [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel).

### Touchpad

Install [xf86-input-synaptics](https://www.archlinux.org/packages/?name=xf86-input-synaptics).

**Note:** FocalTech touchpads are only properly supported in Linux 4.x.

### Wireless NIC

See [Broadcom wireless#broadcom-wl](/index.php/Broadcom_wireless#broadcom-wl "Broadcom wireless").

**Warning:** Using the proprietary driver in tandem with KMS leads to sporadic lockups. It is not known whether it is a kernel panic or an ACPI-related problem.

**Note:** The FLOSS driver `b43` does not support `LCN40` PHYs (as demonstrated that `BCM43142`, the chip this laptop sports, is one [here](https://wireless.wiki.kernel.org/en/users/drivers/b43#list_of_hardware)) yet.

## Troubleshooting

### ACPI

#### Laptop freezes on boot

Set the BIOS setting `OS Selection` in the `Advanced` menu to `Windows 7`.

It is possible to successfully boot by either disabling ACPI or overriding the DSDT, but some devices might no longer operate.