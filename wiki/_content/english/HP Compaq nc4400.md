## Contents

*   [1 System specifications](#System_specifications)
*   [2 Configuration](#Configuration)
    *   [2.1 Graphics](#Graphics)
    *   [2.2 Touchpad](#Touchpad)
    *   [2.3 Wireless](#Wireless)
    *   [2.4 SD/MMC](#SD.2FMMC)
    *   [2.5 HDD failing sensors](#HDD_failing_sensors)

## System specifications

lshwd output:

```
00:00.0 Class 0600: Intel Corp.|Mobile Memory Controller Hub (intel-agp)
00:02.0 Class 0300: Intel Corp.|Mobile Integrated Graphics Controller (i810)
00:02.1 Class 0380: Intel Corp.|Mobile Integrated Graphics Controller (vesa)
00:1b.0 Class 0403: Intel Corp.|I/O Controller Hub High Definition Audio (snd-hda-intel)
00:1c.0 Class 0604: Intel Corp.|I/O Controller Hub PCI Express Port 1 (unknown)
00:1c.1 Class 0604: Intel Corp.|I/O Controller Hub PCI Express Port 2 (unknown)
00:1d.0 Class 0c03: Intel Corp.|I/O Controller Hub UHCI USB #1 (unknown)
00:1d.1 Class 0c03: Intel Corp.|I/O Controller Hub UHCI USB #2 (unknown)
00:1d.2 Class 0c03: Intel Corp.|I/O Controller Hub UHCI USB #3 (unknown)
00:1d.3 Class 0c03: Intel Corp.|I/O Controller Hub UHCI USB #4 (unknown)
00:1d.7 Class 0c03: Intel Corp.|I/O Controller Hub EHCI USB (unknown)
00:1e.0 Class 0604: Intel Corp.|82801 Hub Interface to PCI Bridge (hw_random)
00:1f.0 Class 0601: Intel Corp.|Mobile I/O Controller Hub LPC (i8xx_tco)
00:1f.1 Class 0101: Intel Corp.|I/O Controller Hub PATA (piix)
00:1f.2 Class 0106: Intel Corp.|Mobile I/O Controller Hub SATA cc=AHCI (ahci)
02:06.0 Class 0607: Texas Instruments|PCIxx12 CardBus Controller (yenta_socket)
02:06.2 Class 0180: Texas Instruments|5-in-1 Multimedia Card Reader (SD/MMC/MS/MS PRO/xD) (unknown)
02:06.3 Class 0805: Texas Instruments|5-in-1 Multimedia Card Reader (SD/MMC/MS/MS PRO/xD) (unknown)
02:06.4 Class 0780: Texas Instruments|5-in-1 Multimedia Card Reader (SD/MMC/MS/MS PRO/xD) (unknown)
08:00.0 Class 0200: Broadcom Corp.|NetXtreme BCM5753M Gigabit Ethernet PCI Express (tg3)
10:00.0 Class 0280: Intel Corporation|PRO/Wireless 3945ABG (ipw3945)

```

## Configuration

### Graphics

See [Intel Graphics](/index.php/Intel_Graphics "Intel Graphics").

### Touchpad

See [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics").

### Wireless

See [Wireless network configuration#iwlegacy](/index.php/Wireless_network_configuration#iwlegacy "Wireless network configuration")

### SD/MMC

This requires the *tifm* [kernel module](/index.php/Kernel_module "Kernel module").

```
# modprobe tifm_core
# modprobe tifm_7xx1
# modprobe tifm_sd

```

### HDD failing sensors

See [SMART](/index.php/SMART "SMART"). Example `/etc/smartd.conf`:

```
/dev/sda -a -d sat -m root@localhost

```