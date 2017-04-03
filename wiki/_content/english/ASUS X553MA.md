This article covers configuration specific to this laptop's hardware.

| **Device** | **Status** | **Kernel modules** | **X.org modules** |
| Bluetooth adapter | Does not work | wl |
| GPU | Works | i915 | modesetting |
| Touchpad | Works | psmouse | libinput |
| Wireless NIC | Works | wl |

## Contents

*   [1 Hardware](#Hardware)
    *   [1.1 Bluetooth adapter](#Bluetooth_adapter)
    *   [1.2 Touchpad](#Touchpad)
    *   [1.3 Wireless NIC](#Wireless_NIC)
*   [2 Troubleshooting](#Troubleshooting)
    *   [2.1 Laptop freezes on boot](#Laptop_freezes_on_boot)

## Hardware

### Bluetooth adapter

Installing the [Broadcom wireless#broadcom-wl](/index.php/Broadcom_wireless#broadcom-wl "Broadcom wireless") driver will not help and the Bluetooth adapter is essentially inoperational.

### Touchpad

Install [xf86-input-libinput](https://www.archlinux.org/packages/?name=xf86-input-libinput).

### Wireless NIC

See [Broadcom wireless#broadcom-wl](/index.php/Broadcom_wireless#broadcom-wl "Broadcom wireless").

**Warning:** Using the proprietary driver in tandem with KMS leads to sporadic lockups. See [this kernel bug report](https://bugzilla.kernel.org/show_bug.cgi?id=109051).

**Note:** The FLOSS driver `b43` does not support `LCN40` PHYs (as demonstrated that `BCM43142`, the chip this laptop sports, is one [here](https://wireless.wiki.kernel.org/en/users/drivers/b43#list_of_hardware)) yet.

## Troubleshooting

### Laptop freezes on boot

If your laptop freezes whilst booting Linux, usually, one of these solutions will help:

1.  Blacklist modules `dw_dmac` and `dw_dmac_core`:
    1.  By adding the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `modprobe.blacklist=dw_dmac,dw_dmac_core`.
    2.  By adding these lines to `/etc/modprobe.d/blacklist.conf`:

        ```
        blacklist dw_dmac
        blacklist dw_dmac_core
        ```

2.  Set the BIOS setting `OS Selection` in the `Advanced` menu to `Windows 7`.
3.  Update kernel to version which has a fix as described in [this kernel bug report](https://bugzilla.kernel.org/show_bug.cgi?id=101271).