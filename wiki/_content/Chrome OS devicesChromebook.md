# Chrome OS devices/Chromebook

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

Main article: [Chrome OS devices](/index.php/Chrome_OS_devices "Chrome OS devices").

## Introduction

### First generation of Chromebooks

The first generation of Chromebooks: Google Cr-48, Samsung Series 5 500 and Acer AC700 use [Insyde H2O firmware](http://www.chromium.org/chromium-os/developer-information-for-chrome-os-devices/custom-firmware#TOC-H2C) and not Coreboot firmware. There are three approaches how to install Arch Linux on these devices:

*   Flash a custom H2C firmware (only available for Google Cr-48) and install Arch as on any other UEFI laptop.
*   Take the ChrUbuntu approach which uses the Chrome OS kernel and modules.
*   Build and sign your own kernel, see [[1]](https://plus.google.com/+OlofJohansson/posts/34PYU79eUqP).

## Hardware Comparisons

**Warning:** The availability of SeaBIOS doesn't promise device compatibility for Linux or that the pre-installed SeaBIOS works properly. Before purchasing a device visit its page on the ArchWiki and look for Linux users' posts about that model.

<center>

<table class="wikitable"><caption style="background:#BFD7FF">Chromebook Models</caption>

<tbody>

<tr>

<th>Available</th>

<th>Brand</th>

<th>Model</th>

<th>Processor</th>

<th>RAM</th>

<th>Storage</th>

<th>Upgradable</th>

<th>Screen</th>

<th>Resolution</th>

<th>SeaBIOS</th>

<th>Remarks</th>

</tr>

<tr>

<td>Dec 2010</td>

<td>Google</td>

<td>Cr-48</td>

<td>1.66 GHz Intel Atom N455</td>

<td rowspan="3">2GB  
DDR3</td>

<td rowspan="4">16GB SSD</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">mSATA</td>

<td rowspan="2">12.1 in  
(30.7 cm)</td>

<td rowspan="2">1280x800  
(16:10)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable for  
1st generation</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">[Custom H2C  
firmware available](http://cr-48.wikispaces.com/Flash+BIOS)</td>

</tr>

<tr>

<td>Jun 2011</td>

<td>Samsung</td>

<td>Series 5  
XE500C21</td>

<td rowspan="2">1.66 GHz Intel Atom N570</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">mSATA</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable for  
1st generation</td>

</tr>

<tr>

<td>Jul 2011</td>

<td>Acer</td>

<td>AC700</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">mSATA  
Mini</td>

<td>11.6 in  
(29.5 cm)</td>

<td>1366x768  
(16:9)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable for  
1st generation</td>

</tr>

<tr>

<td>May 2012</td>

<td rowspan="2">Samsung</td>

<td>Series 5  
XE550C22</td>

<td>1.3 GHz Intel Celeron 867  
1.6 Ghz Intel Core i5 2467M</td>

<td>4GB  
DDR3</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">mSATA</td>

<td>12.1 in  
(30.7 cm)</td>

<td>1280x800  
(16:10)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">In custom  
firmware only</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td>Oct 2012</td>

<td>[Series 3  
XE303C12](/index.php/Samsung_Chromebook_(ARM) "Samsung Chromebook (ARM)")</td>

<td>1.7 GHz Samsung Exynos 5250</td>

<td>2GB  
DDR3</td>

<td>16GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td rowspan="2">11.6 in  
(29.5 cm)</td>

<td rowspan="4">1366x768  
(16:9)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable  
on ARM</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">[Supported by  
Arch Linux ARM](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook)</td>

</tr>

<tr>

<td>Nov 2012</td>

<td>Acer</td>

<td>[C710](/index.php/Acer_C710_Chromebook "Acer C710 Chromebook")</td>

<td>1.1 GHz Intel Celeron 847  
1.5 GHz Intel Celeron 1007U</td>

<td rowspan="2">2-4GB  
DDR3</td>

<td rowspan="2">320GB HDD  
16GB SSD</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">SATA  
2.5" 7,9.5mm</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">In custom  
firmware only</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td rowspan="3">Feb 2013</td>

<td>HP</td>

<td>Pavilion 14  
Chromebook</td>

<td>1.1 GHz Intel Celeron 847</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">SATA  
2.5" 7,9.5mm</td>

<td>14 in  
(35.6 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">In custom  
firmware only</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td>Lenovo</td>

<td>ThinkPad X131e  
Chromebook</td>

<td>1.5 GHz Intel Celeron 1007U</td>

<td>4GB  
DDR3</td>

<td>16GB SSD</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">mSATA</td>

<td>11.6 in  
(29.5 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">In custom  
firmware only</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td>Google</td>

<td>Chromebook  
Pixel</td>

<td>1.8 GHz Intel Core i5 3427U</td>

<td>4GB  
DDR3</td>

<td>32GB iSSD  
64GB iSSD</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>12.85 in  
(32.6 cm)</td>

<td>2560x1700  
(3:2)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td>Oct 2013</td>

<td rowspan="2">HP</td>

<td>Chromebook 11</td>

<td>1.7 GHz Samsung Exynos 5250</td>

<td>2GB  
DDR3</td>

<td>16GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>11.6 in  
(29.5 cm)</td>

<td rowspan="9">1366x768  
(16:9)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable  
on ARM</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unsupported by  
Arch Linux ARM  
installation identical to  
[Samsung XE303C12](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook)</td>

</tr>

<tr>

<td rowspan="2">Nov 2013</td>

<td>[Chromebook 14](/index.php/HP_Chromebook_14 "HP Chromebook 14")</td>

<td>1.4 GHz Intel Celeron 2955U</td>

<td rowspan="2">2GB DDR3  
4GB DDR3</td>

<td rowspan="2">16GB SSD  
32GB SSD</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">42mm M.2  
NGFF</td>

<td>14 in  
( 35.6 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td>Acer</td>

<td>[C720/C720P  
Chromebook](/index.php/Acer_C720_Chromebook "Acer C720 Chromebook")</td>

<td>1.4 GHz Intel Celeron 2955U  
1.7 GHz Intel Core i3-4005U</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">42mm M.2  
NGFF</td>

<td>11.6 in  
(29.5 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td>Jan 2014</td>

<td>Toshiba</td>

<td>CB30/CB35  
Chromebook</td>

<td>1.4 GHz Intel Celeron 2955U</td>

<td>2GB DDR3</td>

<td>16GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>13.3 in  
(33.8 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td>Apr 2014</td>

<td>Dell</td>

<td>[Chromebook 11](/index.php/Dell_Chromebook_11 "Dell Chromebook 11")</td>

<td>1.4 GHz Intel Celeron 2955U  
1.7 GHz Intel Core i3-4005U</td>

<td>2GB DDR3  
4GB DDR3</td>

<td rowspan="2">16GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>11.6 in  
(29.5 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires stock  
SeaBIOS patching</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
available</td>

</tr>

<tr>

<td rowspan="5">Jun 2014</td>

<td>Lenovo</td>

<td>N20/N20P  
Chromebook</td>

<td rowspan="2">2.1 GHz Intel BayTrail-M N2830</td>

<td>2GB DDR3</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>11.6 in  
(29.5 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td>Asus</td>

<td>Chromebook  
C200/C300</td>

<td>2GB DDR3  
4GB DDR3</td>

<td>16GB eMMC  
32GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>11.6 in  
(29.5 cm)  
13.3 in  
(33.8 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td rowspan="2">Lenovo</td>

<td>ThinkPad 11e  
Chromebook</td>

<td rowspan="2">1.83 GHz Intel BayTrail-M N2930</td>

<td rowspan="4">4GB DDR3</td>

<td rowspan="3">16GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td rowspan="2">11.6 in  
(29.5 cm)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td>ThinkPad Yoga 11e  
Chromebook</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td>Samsung</td>

<td>Chromebook 2  
XE503C12/C32</td>

<td>1.9 GHz Exynos 5 Octa 5420  
2 GHz Exynos 5 Octa 5800</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>11.6 in  
(29.5 cm)  
13.3 in  
(33.8 cm)</td>

<td>1366x768  
(16:9)  
1920x1080  
(16:9)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable  
on ARM</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">[Supported by  
Arch Linux ARM](http://archlinuxarm.org/platforms/armv7/samsung/samsung-chromebook-2)</td>

</tr>

<tr>

<td>Jul 2014</td>

<td>HEXA</td>

<td>Chromebook Pi</td>

<td>2.1 GHz Intel BayTrail-M N2830</td>

<td>32GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>11.6 in  
(29.5 cm)</td>

<td>1366x768  
(16:9)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware  
not available yet</td>

</tr>

<tr>

<td>Aug 2014</td>

<td>Acer</td>

<td>CB5-311  
Chromebook 13</td>

<td>2.1 GHz Nvidia Tegra K1</td>

<td rowspan="2">2GB DDR3  
4GB DDR3</td>

<td>16GB eMMC  
32GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td rowspan="2">13.3 in  
(33.8 cm)</td>

<td rowspan="2">1366x768  
(16:9)  
1920x1080  
(16:9)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable  
on ARM</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unsupported by  
Arch Linux ARM</td>

</tr>

<tr>

<td rowspan="2">Sep 2014</td>

<td>Toshiba</td>

<td>[CB30/CB35  
Chromebook 2](/index.php/Toshiba_Chromebook_2 "Toshiba Chromebook 2")</td>

<td>2.16 GHz Intel BayTrail-M N2840</td>

<td rowspan="2">16GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td rowspan="2">Acer</td>

<td>CB3-111  
Chromebook 11</td>

<td>2.1 GHz Intel BayTrail-M N2830</td>

<td>2GB DDR3</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td rowspan="2">11.6 in  
(29.5 cm)</td>

<td rowspan="2">1366x768  
(16:9)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td rowspan="4">Oct 2014</td>

<td>C730  
Chromebook 11</td>

<td>2.16 GHz Intel BayTrail-M N2840</td>

<td rowspan="3">2GB DDR3  
4GB DDR3</td>

<td rowspan="2">16GB eMMC  
32GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td rowspan="2">HP</td>

<td>Chromebook 14  
G3</td>

<td>2.1 GHz Nvidia Tegra K1</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>14 in  
(35.6 cm)</td>

<td>1366x768  
(16:9)  
1920x1080  
(16:9)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable  
on ARM</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unsupported by  
Arch Linux ARM</td>

</tr>

<tr>

<td>Chromebook 11  
G3</td>

<td rowspan="3">2.16 GHz Intel BayTrail-M N2840</td>

<td rowspan="3">16GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td rowspan="4">11.6 in  
(29.5 cm)</td>

<td rowspan="4">1366x768  
(16:9)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td>Samsung</td>

<td>Chromebook 2  
XE500C12</td>

<td>2GB DDR3</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td rowspan="3">Feb 2015</td>

<td>Dell</td>

<td>Chromebook 11  
3120</td>

<td rowspan="3">2GB DDR3  
4GB DDR3</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td rowspan="3">Acer</td>

<td>C740 (EDU)  
Chromebook 11</td>

<td rowspan="2">1.5 GHz Intel Celeron 3205U  
2.00 GHz Intel Core i3-5005U</td>

<td>16GB SSD  
32GB SSD</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">42mm M.2  
NGFF</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to RW_LEGACY</td>

</tr>

<tr>

<td>CB5-571  
Chromebook 15</td>

<td>16GB  
32GB</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">42mm M.2  
NGFF</td>

<td rowspan="2">15.6 in  
(39.6 cm)</td>

<td rowspan="2">1366x768  
(16:9)  
1920x1080  
(16:9)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to RW_LEGACY</td>

</tr>

<tr>

<td rowspan="5">Mar 2015</td>

<td>C910 (EDU)  
Chromebook 15</td>

<td>1.5 GHz Intel Celeron 3205U  
2.00 GHz Intel Core i3-5005U  
2.2 GHz Intel Core i5-5200U</td>

<td>4GB DDR3</td>

<td>16GB SSD  
32GB SSD</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">[42mm M.2  
NGFF](https://www.reddit.com/r/chromeos/comments/3asc4f/no_physical_differences_beteen_acer_chromebook/)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to RW_LEGACY</td>

</tr>

<tr>

<td>Google</td>

<td>[Chromebook  
Pixel 2](/index.php/Chromebook_Pixel_2 "Chromebook Pixel 2")</td>

<td>2.2 GHz Intel Core i5-5200U  
2.4 GHz Intel Core i7-5500U</td>

<td>8GB DDR3  
16GB DDR3</td>

<td>32GB  
64GB</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>12.85 in  
(32.6 cm)</td>

<td>2560x1700  
(3:2)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Yes</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to RW_LEGACY</td>

</tr>

<tr>

<td>Lenovo</td>

<td>N21  
Chromebook</td>

<td>2.16 GHz Intel BayTrail-M N2840</td>

<td>2GB DDR3  
4GB DDR3</td>

<td rowspan="3">16GB eMMC</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td>11.6 in  
(29.5 cm)</td>

<td>1366x768  
(16:9)</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Requires writing  
SeaBIOS</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">Custom firmware script  
only writes to BOOT_STUB</td>

</tr>

<tr>

<td>Haier</td>

<td>HR-166R  
Chromebook 11</td>

<td rowspan="2">1.8 GHz Rockchip RK3288</td>

<td rowspan="2">2GB DDR3</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td rowspan="2">11.6 in  
(29.5 cm)</td>

<td rowspan="2">1366x768  
(16:9)</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable  
on ARM</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unsupported by  
Arch Linux ARM</td>

</tr>

<tr>

<td>Hisense</td>

<td>Chromebook C11</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">No</td>

<td style="background: #faa; color: inherit; vertical-align: middle; text-align: center;">Unavailable  
on ARM</td>

<td style="background: #afa; color: inherit; vertical-align: middle; text-align: center;">[Supported by  
Arch Linux ARM](http://archlinuxarm.org/platforms/armv7/rockchip/hisense-chromebook-c11)</td>

</tr>

</tbody>

</table>

</center>

Retrieved from "[https://wiki.archlinux.org/index.php?title=Chrome_OS_devices/Chromebook&oldid=408194](https://wiki.archlinux.org/index.php?title=Chrome_OS_devices/Chromebook&oldid=408194)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Laptops](/index.php/Category:Laptops "Category:Laptops")