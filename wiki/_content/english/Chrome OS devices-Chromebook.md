Main article: [Chrome OS devices](/index.php/Chrome_OS_devices "Chrome OS devices").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Introduction](#Introduction)
    *   [1.1 First generation of Chromebooks](#First_generation_of_Chromebooks)
*   [2 Hardware comparisons](#Hardware_comparisons)
*   [3 See also](#See_also)

## Introduction

### First generation of Chromebooks

The first generation of Chromebooks: Google Cr-48, Samsung Series 5 500 and Acer AC700 use [Insyde H2O firmware](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/custom-firmware#TOC-H2C) and not Coreboot firmware. There are three approaches how to install Arch Linux on these devices:

*   Flash a custom H2C firmware (only available for Google Cr-48) and install Arch as on any other UEFI laptop.
*   Take the ChrUbuntu approach which uses the Chrome OS kernel and modules.
*   Build and sign your own kernel, see [[1]](https://plus.google.com/+OlofJohansson/posts/34PYU79eUqP).

## Hardware comparisons

**Warning:** The availability of SeaBIOS does not promise device compatibility for Linux or that the pre-installed SeaBIOS works properly. Before purchasing a device visit its page on the ArchWiki and look for Linux users' posts about that model.

<center>

<caption style="background:#BFD7FF">Chromebook Models</caption>
| Available | Brand | Model | Processor | RAM | Storage | Upgradable | Screen | Resolution | SeaBIOS | Remarks |
| Dec 2010 | Google | Cr-48 | 1.66 GHz Intel Atom N455 | 2GB
DDR3 | 16GB SSD | mSATA | 12.1 in
(30.7 cm) | 1280x800
(16:10) | Unavailable for
1st generation | [Custom H2C
firmware available](http://cr-48.wikispaces.com/Flash+BIOS) |
| Jun 2011 | Samsung | Series 5
XE500C21 | 1.66 GHz Intel Atom N570 | mSATA | Unavailable for
1st generation |
| Jul 2011 | Acer | AC700 | mSATA
Mini | 11.6 in
(29.5 cm) | 1366x768
(16:9) | Unavailable for
1st generation |
| May 2012 | Samsung | Series 5
XE550C22 | 1.3 GHz Intel Celeron 867
1.6 Ghz Intel Core i5 2467M | 4GB
DDR3 | mSATA | 12.1 in
(30.7 cm) | 1280x800
(16:10) | In custom
firmware only | Custom firmware
available |
| Oct 2012 | [Series 3
XE303C12](/index.php/Samsung_Chromebook_(ARM) "Samsung Chromebook (ARM)") | 1.7 GHz Samsung Exynos 5250 | 2GB
DDR3 | 16GB eMMC | No | 11.6 in
(29.5 cm) | 1366x768
(16:9) | Unavailable
on ARM | [Supported by
Arch Linux ARM](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook) |
| Nov 2012 | Acer | [C710](/index.php/Acer_C710_Chromebook "Acer C710 Chromebook") | 1.1 GHz Intel Celeron 847
1.5 GHz Intel Celeron 1007U | 2-4GB
DDR3 | 320GB HDD
16GB SSD | SATA
2.5" 7,9.5mm | In custom
firmware only | Custom firmware
available |
| Feb 2013 | HP | Pavilion 14
Chromebook | 1.1 GHz Intel Celeron 847 | SATA
2.5" 7,9.5mm | 14 in
(35.6 cm) | In custom
firmware only | Custom firmware
available |
| Lenovo | ThinkPad X131e
Chromebook | 1.5 GHz Intel Celeron 1007U | 4GB
DDR3 | 16GB SSD | mSATA | 11.6 in
(29.5 cm) | In custom
firmware only | Custom firmware
available |
| Google | Chromebook
Pixel | 1.8 GHz Intel Core i5 3427U | 4GB
DDR3 | 32GB iSSD
64GB iSSD | No | 12.85 in
(32.6 cm) | 2560x1700
(3:2) | Yes | Custom firmware
available |
| Oct 2013 | HP | Chromebook 11 | 1.7 GHz Samsung Exynos 5250 | 2GB
DDR3 | 16GB eMMC | No | 11.6 in
(29.5 cm) | 1366x768
(16:9) | Unavailable
on ARM | Unsupported by
Arch Linux ARM
installation identical to
[Samsung XE303C12](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook) |
| Nov 2013 | [Chromebook 14](/index.php/HP_Chromebook_14 "HP Chromebook 14") | 1.4 GHz Intel Celeron 2955U | 2GB DDR3
4GB DDR3 | 16GB SSD
32GB SSD | 42mm M.2
NGFF | 14 in
( 35.6 cm) | Yes | Custom firmware
available |
| Acer | [C720/C720P
Chromebook](/index.php/Acer_C720_Chromebook "Acer C720 Chromebook") | 1.4 GHz Intel Celeron 2955U
1.7 GHz Intel Core i3-4005U | 42mm M.2
NGFF | 11.6 in
(29.5 cm) | Yes | Custom firmware
available |
| Jan 2014 | Toshiba | CB30/CB35
Chromebook | 1.4 GHz Intel Celeron 2955U | 2GB DDR3 | 16GB eMMC | No | 13.3 in
(33.8 cm) | Yes | Custom firmware
available |
| Apr 2014 | Dell | [Chromebook 11](/index.php/Dell_Chromebook_11 "Dell Chromebook 11") | 1.4 GHz Intel Celeron 2955U
1.7 GHz Intel Core i3-4005U | 2GB DDR3
4GB DDR3 | 16GB eMMC | No | 11.6 in
(29.5 cm) | Requires stock
SeaBIOS patching | Custom firmware
available |
| Jun 2014 | Lenovo | N20/N20P
Chromebook | 2.1 GHz Intel BayTrail-M N2830 | 2GB DDR3 | No | 11.6 in
(29.5 cm) | Requires writing
SeaBIOS | Custom firmware
available |
| Asus | Chromebook
C200/C300 | 2GB DDR3
4GB DDR3 | 16GB eMMC
32GB eMMC | No | 11.6 in
(29.5 cm)
13.3 in
(33.8 cm) | Requires writing
SeaBIOS | Custom firmware
available |
| Lenovo | ThinkPad 11e
Chromebook | 1.83 GHz Intel BayTrail-M N2930 | 4GB DDR3 | 16GB eMMC | No | 11.6 in
(29.5 cm) | Requires writing
SeaBIOS | Custom firmware
available |
| ThinkPad Yoga 11e
Chromebook | No | Requires writing
SeaBIOS | Custom firmware
available |
| Samsung | Chromebook 2
XE503C12/C32 | 1.9 GHz Exynos 5 Octa 5420
2 GHz Exynos 5 Octa 5800 | No | 11.6 in
(29.5 cm)
13.3 in
(33.8 cm) | 1366x768
(16:9)
1920x1080
(16:9) | Unavailable
on ARM | [Supported by
Arch Linux ARM](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook-2) |
| Jul 2014 | HEXA | Chromebook Pi | 2.1 GHz Intel BayTrail-M N2830 | 32GB eMMC | No | 11.6 in
(29.5 cm) | 1366x768
(16:9) | No | Custom firmware
available |
| Aug 2014 | Acer | CB5-311
Chromebook 13 | 2.1 GHz Nvidia Tegra K1 | 2GB DDR3
4GB DDR3 | 16GB eMMC
32GB eMMC | No | 13.3 in
(33.8 cm) | 1366x768
(16:9)
1920x1080
(16:9) | Unavailable
on ARM | Unsupported by
Arch Linux ARM |
| Sep 2014 | Toshiba | [CB30/CB35
Chromebook 2](/index.php/Toshiba_Chromebook_2 "Toshiba Chromebook 2") | 2.16 GHz Intel BayTrail-M N2840 | 16GB eMMC | No | Requires writing
SeaBIOS | Custom firmware
available |
| Acer | [CB3-111](/index.php/CB3-111 "CB3-111")
Chromebook 11 | 2.1 GHz Intel BayTrail-M N2830 | 2GB DDR3 | No | 11.6 in
(29.5 cm) | 1366x768
(16:9) | Requires writing
SeaBIOS | Custom firmware
available |
| Oct 2014 | C730
Chromebook 11 | 2.16 GHz Intel BayTrail-M N2840 | 2GB DDR3
4GB DDR3 | 16GB eMMC
32GB eMMC | No | Requires writing
SeaBIOS | Custom firmware
available |
| HP | Chromebook 14
G3 | 2.1 GHz Nvidia Tegra K1 | No | 14 in
(35.6 cm) | 1366x768
(16:9)
1920x1080
(16:9) | Unavailable
on ARM | Unsupported by
Arch Linux ARM |
| Chromebook 11
G3 | 2.16 GHz Intel BayTrail-M N2840 | 16GB eMMC | No | 11.6 in
(29.5 cm) | 1366x768
(16:9) | Requires writing
SeaBIOS | Custom firmware
available |
| Samsung | Chromebook 2
XE500C12 | 2GB DDR3 | No | Requires writing
SeaBIOS | Custom firmware
available |
| Feb 2015 | Dell | Chromebook 11
3120 | 2GB DDR3
4GB DDR3 | No | Requires writing
SeaBIOS | Custom firmware
available |
| Acer | C740 (EDU)
Chromebook 11 | 1.5 GHz Intel Celeron 3205U
2.00 GHz Intel Core i3-5005U | 16GB SSD
32GB SSD | 42mm M.2
NGFF | Requires writing
SeaBIOS | Custom firmware
available |
| CB5-571
Chromebook 15 | 16GB
32GB | 42mm M.2
NGFF | 15.6 in
(39.6 cm) | 1366x768
(16:9)
1920x1080
(16:9) | Requires writing
SeaBIOS | Custom firmware
available |
| Mar 2015 | C910 (EDU)
Chromebook 15 | 1.5 GHz Intel Celeron 3205U
2.00 GHz Intel Core i3-5005U
2.2 GHz Intel Core i5-5200U | 4GB DDR3 | 16GB SSD
32GB SSD | [42mm M.2
NGFF](https://www.reddit.com/r/chromeos/comments/3asc4f/no_physical_differences_beteen_acer_chromebook/) | Requires writing
SeaBIOS | Custom firmware
available |
| Google | [Chromebook
Pixel 2](/index.php/Chromebook_Pixel_2 "Chromebook Pixel 2") | 2.2 GHz Intel Core i5-5200U
2.4 GHz Intel Core i7-5500U | 8GB DDR3
16GB DDR3 | 32GB
64GB | No | 12.85 in
(32.6 cm) | 2560x1700
(3:2) | Yes | Custom firmware
available |
| Lenovo | N21
Chromebook | 2.16 GHz Intel BayTrail-M N2840 | 2GB DDR3
4GB DDR3 | 16GB eMMC | No | 11.6 in
(29.5 cm) | 1366x768
(16:9) | Requires writing
SeaBIOS | Custom firmware
available |
| Haier | HR-166R
Chromebook 11 | 1.8 GHz Rockchip RK3288 | 2GB DDR3 | No | 11.6 in
(29.5 cm) | 1366x768
(16:9) | Unavailable
on ARM | Unsupported by
Arch Linux ARM |
| Hisense | Chromebook C11 | No | Unavailable
on ARM | [Supported by
Arch Linux ARM](http://archlinuxarm.org/platforms/armv7/rockchip/hisense-chromebook-c11) |
| June 2015 | Asus | C100PA
(Chromebook flip) | 2/4GB | No | 10.1 in | 1280 x 800
(16:10) | Unavailable
on ARM | [Supported by
Arch Linux ARM](https://archlinuxarm.org/platforms/armv7/rockchip/asus-chromebook-flip-c100p)<small>
[notes](/index.php/User_talk:Pierro78/Asus_chromebook_flip "User talk:Pierro78/Asus chromebook flip")</small> |
| Jan 2016 | Acer | [CB3-131-C8GZ
(Chromebook 11)](/index.php/Acer_CB3-131_Chromebook "Acer CB3-131 Chromebook") | 2.16 GHz
Intel Celeron CPU N2840
(Baytrail) | 4GB
DDR3 | 16GB
eMMC | No | 11.6 in
(29.5 cm) | 1366x768
(16:9) | Requires writing
SeaBIOS | Custom firmware
available |
| Oct 2017 | Google | [Pixelbook](/index.php?title=Pixelbook&action=edit&redlink=1 "Pixelbook (page does not exist)") | Intel Core i5-7Y57
Intel Core i5-7Y57
Intel Core i7-7Y75 | 8GB DDR3
8GB DDR3
16GB DDR3 | 128GB
256GB
512GB | No | 12.3 in
(31.2 cm) | 2400x1600
(3:2) | Yes | Custom firmware
available |
| March 2018 | Acer | [Chromebook 11 (C732)](/index.php/Chromebook_11_(C732) "Chromebook 11 (C732)")
Astronaut | Intel(R) Celeron(R) CPU N3450 @ 1.10GHz | 4GB LPDDR4
8GB LPDDR4 | 32GB
64GB | No | 11.6 in
(29.5 cm) | 1366 x 768 | Yes | Custom firmware
available |

</center>

## See also

*   [Gallium OS hardware compatibility](https://wiki.galliumos.org/Hardware_Compatibility) for Chromebooks