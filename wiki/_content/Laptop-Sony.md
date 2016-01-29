# Laptop/Sony

| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - **Sony** - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other") |

## Model List

| Model Version | Arch Linux
Install CD Version
 | Hardware Support | Remark |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power Management | Modem | Other |
| Vaio VGN-S5M | Any | 3D with nvidia driver | Intel audio with [ALSA](/index.php/ALSA "ALSA") | Yes | Yes, ipw2200bg | -- | Suspend-to-RAM with suspend2 | Untested | Memory stick reader does not work | Everything else (Fn Keys, DVD-RW drive, FireWire...) works without a hitch |
| Vaio VGN-C2Z | Any | 3D with nvidia driver | Intel audio with [ALSA](/index.php/ALSA "ALSA") | Yes | Yes, ipw3945 | Modules look fine but due to lack of a Bluetooth client not tested | Suspend-to-RAM with vanilla kernel & [linux-ck](https://aur.archlinux.org/packages/linux-ck/)<sup><small>AUR</small></sup> | Untested | Memory stick reader not tested | Everything else (Fn Keys, DVDRW drive, Firewire...) works without a hitch |
| Vaio VGN-FS742/W
VGN-FS630/W | Kernel 2.6.23.12-3 | i810 | Intel audio with [ALSA](/index.php/ALSA "ALSA") | e100 | ipw2200 | No | acpi_cpufreq, sonyacpi | Untested | Memory stick might work | Fn keys with FSFN |
| Vaio VGN-NR320FH | 2008-06 | Intel GMA965/X3100 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver) | Intel audio with ALSA | Do not know, but works out-of-the-box | Atheros AR5006EG/AR242x (madwifi 0.9.4.3844-2) | No | acpi_cpufreq, sony-laptop | Untested | Memory stick might work | Fn keys with sony-laptop and sonypid. Using `vga` option in kernel line in [GRUB](/index.php/GRUB "GRUB") might give problems with resolution. Pretty cool laptop, everything works out-of-the-box except Fn keys for which I needed to do some research. |
| Vaio VGN-N130G | 2010 (right now with kernel 2.6.34) | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver | Intel audio with ALSA | Do not know, but works out-of-the-box | ipw3945 | No | Untested | Untested | Memory stick might work | The only problem I have had is with the Wi-Fi randomly cutting out (`netcfg -r` to reconnect). I think this is a problem with MY laptop, rather than this model in general. |

Retrieved from "[https://wiki.archlinux.org/index.php?title=Laptop/Sony&oldid=375512](https://wiki.archlinux.org/index.php?title=Laptop/Sony&oldid=375512)"