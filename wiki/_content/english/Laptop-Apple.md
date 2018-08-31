[Acer](/index.php/Laptop/Acer "Laptop/Acer") – <a class="mw-selflink selflink">Apple</a> – [ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") – [Dell](/index.php/Laptop/Dell "Laptop/Dell") – [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") – [HP](/index.php/Laptop/HP "Laptop/HP") – [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") – [MSI](/index.php/Laptop/MSI "Laptop/MSI") – [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") – [Sony](/index.php/Laptop/Sony "Laptop/Sony") – [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") – [Other](/index.php/Laptop/Other "Laptop/Other")

## Model List

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| MacBook Pro Rev3 | x86_64 2007.08 | Yes | Yes | Yes | Yes | Yes | Cpufreq + pm-utils | Not Used | - | - |
| MacBook Mid2007 | i686 2008.03 | Yes | Yes | Yes | Yes | Not used | Cpufreq + laptop-mode-tools | Not Used | - | Suspend-to-RAM working ok |
| MacBook Mid2007 | x86_64 2009.08 | Yes | Yes | Yes | Yes | Yes | pm-utils | Not Used | - | All works out-of-the box, except iSight |
| MacBook Pro 5,2 17" | x86_64 2009.08 | Yes | Yes | Yes | Yes | Not used | cpufreq + pm-util | Not Used | - | suspend,hibernate OK |
| Macbook Air 2013 | x86_64 2014.10.01 | Yes | Yes | Yes | Yes | Yes | Out of the box | Unknown | - | All works out of the box except webcam (no support for webcam at all) |
| Macbook Mid2006 | i686 2014.10.01 | Yes | Yes | Yes | Yes | Yes, with HID to HCI conversion | Out of the box | N/A | The synaptics driver allows triple click, a feature unavailable in OSX. | Everything except webcam, use isight-firmware-tools |
| Macbook Pro mid-2009 | x86_64 2016.08.01 | Yes | Yes | Yes | Yes | Yes | Unknown | N/A | Virtual console does not display when switching from a graphical session with proprietary nvidia drivers. This does not happen on nouveau drivers. | Everything except iSight works out of the box |
| Macbook Pro mid-2010 | x86_64 2017.04.01 | Yes | Yes | Yes | Yes | Yes | Unknown | N/A | Everything seemed to work. However, there were some unresolved heat issues. These could be solved with [mbpfan-git](https://aur.archlinux.org/packages/mbpfan-git/) | broadcom-wl drives were used for wifi |
| MacBook Pro (Mid-2012) | x86_64 2018.03.01 | Yes | Yes | Yes | Yes | Yes | laptop-mode-tools | N/A | - | You will need an Eth or Teather to install the BCM wireless drivers as they're non-free and don't ship with the kernel, more info can be found at [MacBookPro9,2 (Mid-2012)#Wireless](/index.php/MacBookPro9,2_(Mid-2012)#Wireless "MacBookPro9,2 (Mid-2012)"). |