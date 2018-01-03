| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - [Compaq](/index.php/Laptop/Compaq "Laptop/Compaq") (discontinued) - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - <a class="mw-selflink selflink">Sony</a> - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other") |

## Model List

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| Vaio VGN-C2Z | Any | 3D with nvidia driver | Intel audio with [ALSA](/index.php/ALSA "ALSA") | Yes | Yes, ipw3945 | Modules look fine but due to lack of a Bluetooth client not tested | Suspend-to-RAM with vanilla kernel & [linux-ck](https://aur.archlinux.org/packages/linux-ck/) | Untested | Memory stick reader not tested | Everything else (Fn Keys, DVDRW drive, Firewire...) works without a hitch |
| Vaio VGN-NR320FH | 2008-06 | Intel GMA965/X3100 ([xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) driver) | Intel audio with ALSA | Do not know, but works out-of-the-box | Atheros AR5006EG/AR242x (madwifi 0.9.4.3844-2) | No | acpi_cpufreq, sony-laptop | Untested | Memory stick might work | Fn keys with sony-laptop and sonypid. Using `vga` option in kernel line in [GRUB](/index.php/GRUB "GRUB") might give problems with resolution. Pretty cool laptop, everything works out-of-the-box except Fn keys for which I needed to do some research. |
| Vaio SV-S1511X9E/B | Any | nouveau kernel module loads only with option config=NvBios=PLATFORM | Intel audio with ALSA | Yes | Yes | Yes | Suspend-to-RAM perfect. Hibernate untested. Disk spindown untested. | Untested |