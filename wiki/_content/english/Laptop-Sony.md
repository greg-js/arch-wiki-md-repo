[Acer](/index.php/Laptop/Acer "Laptop/Acer") – [Apple](/index.php/Laptop/Apple "Laptop/Apple") – [ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") – [Dell](/index.php/Laptop/Dell "Laptop/Dell") – [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") – [HP](/index.php/Laptop/HP "Laptop/HP") – [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") – [MSI](/index.php/Laptop/MSI "Laptop/MSI") – [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") – <a class="mw-selflink selflink">Sony</a> – [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") – [Other](/index.php/Laptop/Other "Laptop/Other")

## Vaio

### Power management/Suspend and hibernate problems

You might have to add the [kernel parameter](/index.php/Kernel_parameter "Kernel parameter") `acpi_sleep=nonvs` to your bootloader.

### Overview of Vaio models and state of support

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| Vaio VGN-C2Z | Any | 3D with nvidia driver | Intel audio with [ALSA](/index.php/ALSA "ALSA") | Yes | Yes, ipw3945 | Modules look fine but due to lack of a Bluetooth client not tested | Suspend-to-RAM with vanilla kernel & [linux-ck](https://aur.archlinux.org/packages/linux-ck/) | Untested | Memory stick reader not tested | Everything else (Fn Keys, DVDRW drive, Firewire...) works without a hitch |
| Vaio VGN-NR320FH | 2008-06 | Intel GMA965/X3100 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver) | Intel audio with ALSA | Do not know, but works out-of-the-box | Atheros AR5006EG/AR242x (madwifi 0.9.4.3844-2) | No | acpi_cpufreq, sony-laptop | Untested | Memory stick might work | Fn keys with sony-laptop and sonypid. Using `vga` option in kernel line in [GRUB](/index.php/GRUB "GRUB") might give problems with resolution. Pretty cool laptop, everything works out-of-the-box except Fn keys for which I needed to do some research. |
| Vaio SV-S1511X9E/B | Any | nouveau kernel module loads only with option config=NvBios=PLATFORM | Intel audio with ALSA | Yes | Yes | Yes | Suspend-to-RAM perfect. Hibernate untested. Disk spindown untested. | Untested |
| Vaio SVT13 Touch | Any | Intel HD Graphics 4000 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver) | Intel audio with ALSA | Yes | Yes | Yes | Suspend to RAM works, both manually and on lid close, temperature, battery level work, fan speed control unsupported by hardware | Not available | SD card reader works, Memory Stick untested, touch works | Action keys seem to work, but only WEB is mapped to browser, ASSIST sends tilde(~) and VAIO does nothing. Fn keys work, but touchpad disable seems to do nothing |