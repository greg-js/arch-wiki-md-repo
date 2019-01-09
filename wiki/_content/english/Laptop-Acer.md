<a class="mw-selflink selflink">Acer</a> – [Apple](/index.php/Laptop/Apple "Laptop/Apple") – [ASUS](/index.php/Laptop/ASUS "Laptop/ASUS") – [Dell](/index.php/Laptop/Dell "Laptop/Dell") – [Fujitsu](/index.php/Laptop/Fujitsu "Laptop/Fujitsu") – [HP](/index.php/Laptop/HP "Laptop/HP") – [IBM/Lenovo](/index.php/Laptop/Lenovo "Laptop/Lenovo") – [MSI](/index.php/Laptop/MSI "Laptop/MSI") – [Samsung](/index.php/Laptop/Samsung "Laptop/Samsung") – [Sony](/index.php/Laptop/Sony "Laptop/Sony") – [Toshiba](/index.php/Laptop/Toshiba "Laptop/Toshiba") – [Other](/index.php/Laptop/Other "Laptop/Other")

## Model List

| Model version | Arch Linux
install CD version
 | Hardware support | Remarks |
| Video | Sound | Ethernet | Wireless | Bluetooth | Power management | Modem | Other |
| Aspire 5100-3825 | 0.8 (Voodoo) | ATI Radeon Xpress 1100 | Intel | Realtek | Atheros | n/a | untested | Hot keys: untested |
| Aspire 1501LMi | 0.9 (Don't Panic) | ATI Radeon 9600: HW acceleration only with proprietary driver | VIA: OK | Broadcom: OK | untested | none | Suspend to RAM: ??
Disk: Yes
Battery: Yes
CPU frequency scaling: Yes | untested | Hot keys: untested |
| Travelmate 6292 | Core Dump,
Overlord | Intel x3100: HW acceleration with Intel's open-source driver, ~1100 FPS in the glxgears | Intel HDA: OK (model=acer) | Broadcom BCM5787M: OK | Intel iwl4965: OK | Broadcom: OK | Suspend to RAM: ??
Disk: Ok
Battery: Yes
CPU frequency scaling: Yes | untested | Hot keys: untested
FireWire (Texas Instruments) TSB43AB23: OK(?) | FireWire detects well but I haven't tested it yet |
| Aspire 5024 | 0.7.2 | ATI Radeon X700
Runs Compiz on both fglrx ([catalyst](https://aur.archlinux.org/packages/catalyst/)) >= 8.02 and radeon driver | AC97: OK | Realtek: OK | Broadcom 4318
Needs *acer_apci* + firmware or ndiswrapper driver | N/A | Battery: Yes
Suspend: Video and Wi-Fi problems
CPU frequency scaling: powernow-k8 driver | untested |
| [Aspire 7720](/index.php/Acer_Aspire_7720 "Acer Aspire 7720") | 2009.02 | Intel i965 | ALC268: working OK | Broadcom BCM5787M (tg3): OK | Intel 3945: Needs microcode | Detected, works | Battery: Yes
Suspend: Seems to work ok
Hibernation: still flaky (often hangs in the middle of restoring) | With linuxant drivers, might work | Web cam driver: *uvcvideo*; card reader: only SD cards seem to work; special keys (Acer Arcade, direct access to browser/mail) seem to not work; volume knob at the side is seen as a multimedia key. | FireWire seems to be recognized, untested. For 64-bit, update BIOS to fix ACPI and wireless problems. |
| [Aspire E5-573](/index.php/Acer_Aspire_E5-573 "Acer Aspire E5-573") | 2015.12 | Intel i965 | OK | OK | OK | not detected | OK | not present | ... | ... |
| Aspire 7730 | 2009.08 i686 & x86_64 | Intel Mobile 4 Series
i810
Autoconfiguration works. Compiz OK, with indirect rendering. | ALC888
Playback & internal microphone: OK; microphone input socket: not tested
`options snd-hda-intel model=laptop` added to `/etc/modprobe.d/sound.conf` to get headphone output working | OK | OK, with iwlagn | None | Suspend to RAM: OK
Suspend to disk crashes on i686, OK on x86_64
CPU frequency scaling: OK
(using cpufreq) | Untested | Hot keys: OK
Web cam: OK
HDMI: untested
Card reader: untested | Problem booting install CD
Solved with `ln -sf /dev/sr0 /dev/archiso` at ramfs |
| TravelMate 8371G (TM8371G-944G32n) | 2010.05 x86_64 | Intel GM45, works with *i915*. Radeon HD 4330 listed but cannot switch to it. | OK | OK, works with *r8169* | OK, works with *iwlagn* | OK, works with *btusb* | s2ram works (see remarks), s2disk works, CPU scaling works, no fan control | No modem | Web cam works with *uvcvideo*.
Card reader works.
Fingerprint reader does not seem to have a driver! | Suspend to RAM only works with the `i8042.reset=1` kernel parameter. Otherwise, it fails to wake up, and ends up rebooting itself uncleanly!
Generally, this Acer seems to work quite well with Arch Linux :-) |
| Aspire 4935 | 2009.08 x86_64 | Nvidia GeForce 9300M GS | OK, Intel HDA | OK | OK | Untested | Suspend to RAM: OK
Suspend to disk: OK
Frequency scaling: OK
(using cpufreq) | Untested | Hot keys: OK
Audio touch panel NOT working
Web cam: OK
HDMI: OK | By "audio touch panel" I mean the illuminated plastic hot key touch panel on the right-hand side of the keyboard. |
| AspireOne D255e | Intel GMA 3150 | OK | OK, Atheros 8132 worked only with latest Archboot not official images | OK, Broadcom worked only with latest Archboot not official images | Untested | Untested | Untested | Hot keys: OK
Synaptic Touchpad: OK |
| Aspire 2920Z | 2009.2 | Intel Mobile GM965/GL960 Integrated Graphics Controller | OK, Intel 82801H | OK, Broadcom NetLink BCM5787M Gigabit Ethernet PCI Express | OK, Broadcom BCM4311 802.11b/g WLAN | n/a | Suspend to RAM: OK.
Suspend to disk: OK.
CPU frequency scaling: untested | Untested | Hot keys: web, mail, and wireless work. Blue *e* on the left: not working
Synaptic touchpad: OK
 | Not everything worked fine on fresh installation. Requires some work. |
| Aspire 5735z | archlinux-2014.09.03-dual | Intel GMA 4500M | OK | OK | OK | Untested | Suspend to RAM: OK.
Suspend to disk: OK.
CPU frequency scaling: untested | Untested | Hot keys: OK (except Bluetooth: untested)
Synaptic Touchpad: OK |
| TravelMate TimelineX 8473T | archlinux-2016.02.01-dual | Intel HD 3000 | OK | Untested | OK | Untested | Untested | Untested | Hot keys: Display/No Backlight/Disable Trackpad work
Sound, sleep, wireless, brightness not working out of box
Synaptic Touchpad: OK | Live Media boots in Gummiboot and attempts to load EFI media, even though MOBO supports legacy boot ONLY. Delete the /EFI partition on the boot media to force Grub (this may cause other problems) |
| Acer Aspire E1-531 | archlinux-2016.07.01-dual | Intel HD 2000 | OK | OK | OK | OK | OK(Using laptop-mode-tools) | Untested | Hot keys: Sound, sleep, wireless, brightness hotkeys(fn+f1/f2/...) not working out of box
Synaptic Touchpad: OK
Webcam: OK
HDMI: untested |
| Acer Aspire V3-572G | Current | Intel HD 5500
NVIDIA GeForce 840M working with bumblebee | OK | Realtek: OK | OK | OK | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
CPU frequency scaling: untested | Untested | Webcam: OK
Hotkeys: OK
Synaptic Touchpad: OK
HDMI: OK | Ran into trouble with suspend/resume + nvidia prop. drivers ("gpu has fallen off the bus"). Fix/workaround: appended `rcutree.rcu_idle_gp_delay=1 acpi_osi=! acpi_osi="Windows 2009"` to kernel parameters. |
| Acer Nitro VN7-791G-74DL | archlinux-2016.01.01-dual | Intel HD 530
Nvidia GeForce GTX 970M 3GB VRAM | OK | Realtek: OK | OK, Killer Wireless-AC 1535 | OK | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
CPU frequency scaling: Yes | N/A | Webcam: Yes
Hotkeys: OK
Synaptic Touchpad: OK
HDMI: Yes
Booting from NVME: Yes | Ran into trouble with with fun control, porting driver from windows is required. |
| Acer Nitro VN7-792G-710p | archlinux-2016.10.01-dual | Intel HD 530
Nvidia GeForce GTX 960M 2GB VRAM | OK | Realtek: OK | OK | OK | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
CPU frequency scaling: untested | Untested | Webcam: untested
Hotkeys: OK
Synaptic Touchpad: OK
HDMI: untested |
| Acer Nitro VN7-792G-751Y | archlinux-2016-12-01-dual | Intel HD 530
Nvidia GeForce GTX 960M 4GB VRAM | OK | Realtek: OK | OK | OK | Suspend to RAM: Yes
Disk: Yes
Battery: Yes
CPU frequency scaling: untested | Untested | Webcam: Yes
Hotkeys: OK
Synaptic Touchpad: OK
HDMI: **Does not work**
Microphone: **Does not work** |
| [Aspire One Cloudbook 11](/index.php/Acer_Cloudbook "Acer Cloudbook") | archlinux-201608 | Intel HD Graphics 400 | OK, HDA-Intel | N/A | OK, Qualcomm Atheros | OK | Suspend to RAM: Yes
Disk: Not tested
Battery: Yes
CPU frequency scaling: Ok | N/A | Webcam: Ok
Hotkeys: Some
Synaptic Touchpad: OK (Set to Basic in BIOS)
HDMI: untested | First boot after a UEFI install will typically stop with a "No media found" message. Go into BIOS and navigate to "Select an UEFI file as trusted". Note that a Supervisor password must be set to change these parameters. |
| Acer Aspire F5-573G-7791 | 2016.12.01 | OK, NVIDIA GeForce 940MX (NVIDIA Device 179c), [Bumblebee](/index.php/Bumblebee "Bumblebee") 2016.02.05 | OK, Intel Device 9d71
Driver: snd_hda_intel | OK, Realtek RTL8111/8168/8411 | OK, Intel Wireless 3165 | OK | Suspend to RAM: Yes
Disk: Not tested
Battery: Yes
CPU frequency scaling: Unknown | Untested (not present?) | Webcam: Untested
Hot keys: OK
Synaptic Touchpad: OK
HDMI: Untested
USB:

*   1x USB 2.0: OK
*   2x USB 3.0: OK
*   1x USB 3.1 Type-C: Untested

 | (BIOS v1.15) After UEFI installation, must set Supervisor password, add bootloader as trusted, and boot with SecureBoot. BIOS v1.25 reportedly has problems on similar E5 models that were fixed in 1.31 onward. |
| Acer Aspire E5-575G-5538 | 2017.02.01 | OK, Nvidia GeForce 940MX (NVIDIA Device 179c),

*   works with proprietary [NVIDIA](/index.php/NVIDIA "NVIDIA") drivers dkms version, [Bumblebee](/index.php/Bumblebee "Bumblebee") dkms version,
*   [Nouveau](/index.php/Nouveau "Nouveau") works too, gives better battery life but significantly less performance as of 10 Aug 2017

 | OK, HDA-Intel | OK, Realtek, needed to set MAC in a profile in NetworkManager settings | OK, Qualcomm Atheros | 

*   Pairing works
*   Sending files works
*   Receiving files works
*   Bluetooth PAN works

 | 

*   Suspend to RAM: Yes
*   Disk: Untested
*   Battery: Yes, but battery life is not great, needs [TLP](/index.php/TLP "TLP") installed for better battery life
*   CPU frequency scaling: Yes

 | Untested, USB modems should work out of the box | 

*   Webcam: OK
*   Hot keys: OK
*   Touchpad: Works with [synaptics](/index.php/Synaptics "Synaptics")/[Libinput](/index.php/Libinput "Libinput"). [Libinput](/index.php/Libinput "Libinput") works the best (and supports gestures).
*   HDMI: OK
*   USB:
    *   1x USB 2.0: OK
    *   2x USB 3.0: OK
    *   1x USB 3.1 Type-C: OK

 | USB drive detection took some work (looking in the BIOS, disabling secure boot). Installation was not successful on the first try. In order to boot I enabled secureboot, cleared trusted bootloaders at secureboot settings, saved, rebooted, entered BIOS, added GRUB as trusted UEFI file, saved, rebooted, entered BIOS, disabled secureboot. Grub will appear in the boot order list even if secureboot is disabled. Must be done at each firmware update. |
| Acer Aspire E5-553-T337 | 2018.08.07 | Perfectly OK,Amd radeon R5 | OK | OK | OK | OK | OK | OK | OK | Everything works fine.no complaints |