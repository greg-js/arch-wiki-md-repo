| [Laptop main page](/index.php/Laptop "Laptop") |
| [Acer](/index.php/Laptop/Acer "Laptop/Acer") - [Apple](/index.php/Laptop/Apple "Laptop/Apple") - [Asus](/index.php/Laptop/Asus "Laptop/Asus") - **Compaq** - [Dell](/index.php/Laptop/Dell "Laptop/Dell") - [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") - [HP](/index.php/Laptop/HP "Laptop/HP") - [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") - [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") - [Sony](/index.php/Laptop/Sony "Laptop/Sony") - [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") - [Other](/index.php/Laptop/Other "Laptop/Other") |

## Model List

| Model Version | Arch Linux
Install CD Version
 | Hardware Support | Remark |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power Management | Modem | Other |
| Compaq nx7300 | Duke/2007.5 | Intel 955GM + 3D/AIGLX | Intel HD audio with [ALSA](/index.php/ALSA "ALSA") | Yes | Yes, IPW3945 | YES | ACPI | Untested | Everything works fantastic. Easiest install of any Linux distribution |
| Compaq Presario F700 | 2009.02 | Nvidia 7000M driver: *nvidia* | Nvidia HD audio with ALSA | Nvidia: OK | Atheros: OK
driver: *ath5k* | none | ACPI
Suspend to RAM/disk: OK
Used pm-utils + uswsusp
CPU frequency scaling: OK | N/A | Hangs for 20-30s when loading ACPI modules when on battery power. Some hotkeys do not work. Need to turn `AutoAddDevices` to `false` in [Xorg](/index.php/Xorg "Xorg") configuration to fix keyboard layout problems. |
| Compaq Presario CQ60-420ED | 2009.08 | Nvidia GeForce 8200M driver: *nvidia* | nVidia MCP72XE/MCP72P/MCP78U/MCP78S HD Audio using ALSA | nVidia MCP77 Ethernet | Atheros AR5001 driver: *ath5k* | none | Using [laptop-mode-tools](https://aur.archlinux.org/packages/laptop-mode-tools/) and [cpupower](https://www.archlinux.org/packages/?name=cpupower) (replaces *cpufrequtils*), haven't properly tested yet | Untested | The console framebuffer is a bit slow (using `vga=773` in [GRUB](/index.php/GRUB "GRUB")) and the wireless LED indicator flickers red and blue. Touchpad (scrolling) works with GNOME |
| [Compaq Armada M300](/index.php/Compaq_Armada_M300 "Compaq Armada M300") | 2010.05 | ATI 3D Rage LT Pro driver: *mach64* | ESS Technology ES1978 Maestro 2E | Intel 82557/8/9/0/1 | none | none | ACPI + [cpupower](https://www.archlinux.org/packages/?name=cpupower) (replaces *cpufrequtils*) | Untested | Everything is perfect except for 3D support. |