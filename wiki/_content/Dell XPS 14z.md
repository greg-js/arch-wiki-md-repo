# Dell XPS 14z

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

## Contents

*   [1 Hardware state](#Hardware_state)
*   [2 System Settings](#System_Settings)
*   [3 System Setup](#System_Setup)
    *   [3.1 Graphics](#Graphics)
        *   [3.1.1 Nvidia card](#Nvidia_card)
        *   [3.1.2 Intel card](#Intel_card)
    *   [3.2 Power management](#Power_management)
    *   [3.3 Special trick for acpid](#Special_trick_for_acpid)
    *   [3.4 Other](#Other)

## Hardware state

<table class="wikitable">

<tbody>

<tr>

<th width="160" style="border-bottom: 2px solid;">Device</th>

<th width="120" style="border-bottom: 2px solid">Status</th>

</tr>

<tr>

<th style="border-bottom: 1px solid; border-right: 1px solid">Network</th>

<th style="background: green; border-bottom: 1px solid">Works</th>

</tr>

<tr>

<th style="border-bottom: 1px solid; border-right: 1px solid">Wireless</th>

<th style="background: green; border-bottom: 1px solid">Works</th>

</tr>

<tr>

<th style="border-bottom: 1px solid; border-right: 1px solid">Sound</th>

<th style="background: green; border-bottom: 1px solid">Works</th>

</tr>

<tr>

<th style="border-bottom: 1px solid; border-right: 1px solid">Bluetooth</th>

<th style="background: green; border-bottom: 1px solid">Works</th>

</tr>

<tr>

<th style="border-bottom: 1px solid; border-right: 1px solid">Touchpad</th>

<th style="background: green; border-bottom: 1px solid">Works</th>

</tr>

<tr>

<th style="border-bottom: 1px solid; border-right: 1px solid">Graphics</th>

<th style="background: #FF7F00; border-bottom: 1px solid">Modify</th>

</tr>

<tr>

<th style="border-bottom: 1px solid; border-right: 1px solid">USB 3.0</th>

<th style="background: #FFFFFF; border-bottom: 1px solid">Not tested</th>

</tr>

<tr>

<th style="border-bottom: 1px solid; border-right: 1px solid">Webcam</th>

<th style="background: green; border-bottom: 1px solid">Works</th>

</tr>

</tbody>

</table>

## System Settings

 `lspci` 

```
00:00.0 Host bridge: Intel Corporation 2nd Generation Core Processor Family DRAM Controller (rev 09)
00:01.0 PCI bridge: Intel Corporation Xeon E3-1200/2nd Generation Core Processor Family PCI Express Root Port (rev 09)
00:02.0 VGA compatible controller: Intel Corporation 2nd Generation Core Processor Family Integrated Graphics Controller (rev 09)
00:16.0 Communication controller: Intel Corporation 6 Series/C200 Series Chipset Family MEI Controller #1 (rev 04)
00:1b.0 Audio device: Intel Corporation 6 Series/C200 Series Chipset Family High Definition Audio Controller (rev 04)
00:1c.0 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 1 (rev b4)
00:1c.2 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 3 (rev b4)
00:1c.3 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 4 (rev b4)
00:1c.5 PCI bridge: Intel Corporation 6 Series/C200 Series Chipset Family PCI Express Root Port 6 (rev b4)
00:1d.0 USB controller: Intel Corporation 6 Series/C200 Series Chipset Family USB Enhanced Host Controller #1 (rev 04)
00:1f.0 ISA bridge: Intel Corporation HM67 Express Chipset Family LPC Controller (rev 04)
00:1f.2 SATA controller: Intel Corporation 6 Series/C200 Series Chipset Family 6 port SATA AHCI Controller (rev 04)
00:1f.3 SMBus: Intel Corporation 6 Series/C200 Series Chipset Family SMBus Controller (rev 04)
01:00.0 VGA compatible controller: nVidia Corporation Device 1050 (rev ff)
07:00.0 Ethernet controller: Atheros Communications AR8151 v2.0 Gigabit Ethernet (rev c0)
08:00.0 Network controller: Intel Corporation Centrino Advanced-N 6230 (rev 34)
09:00.0 Unassigned class [ff00]: Realtek Semiconductor Co., Ltd. RTS5116 PCI Express Card Reader (rev 01)
0f:00.0 USB controller: Texas Instruments Device 8241 (rev 02)

```

## System Setup

### Graphics

#### Nvidia card

Initially, both the Intel integrated graphics and the Nvidia card will be active, consuming a lot of power, so you probably want to install [bumblebee and bbswitch](/index.php/Bumblebee "Bumblebee"). With this laptop, the packages nvidia, bumblebee-git and bbswitch-git are working fine.

#### Intel card

From the [xps 15z](/index.php/Dell_XPS_15z "Dell XPS 15z"), wiki page, it is reported that using the Intel card without any modifications can result in poor video performance. A quick fix that does not make things worse for the 14z is to edit `/boot/grub/menu.lst`, and append the following to the `kernel` section

```
kernel /boot/vmlinuz... **i915.semaphores=1**

```

### Power management

Classical power saving tricks should apply for this laptop. See the dedicated pages of [acpid](/index.php/Acpid "Acpid"), [laptop-mode](/index.php/Laptop_Mode_Tools "Laptop Mode Tools") and [cpufreq](/index.php/Cpufreq "Cpufreq").

First try to install [pm-utils](https://www.archlinux.org/packages/?name=pm-utils).

and see if the following command works successfully:

```
# pm-suspend

```

Normally it should.

### Special trick for acpid

If you wish to use acpid for handling the event for plugging/unplugging the ac adapter, you should know that the script does not handle it properly. For some reason, acpi_listen does not report a second argument in AC|ACAD|ADP0 but ACPI0003:00\. In `/etc/acpi/handler.sh`, you can modify these lines:

```
   ac_adapter)
       case "$2" in
           AC|ACAD|ADP0)
           ...

```

in

```
   ac_adapter)
       case "$2" in
           AC|ACAD|ADP0|ACPI0003:00)
           ...

```

If this does not solve your problem, you should be able to see what event is triggered by plugging/unplugging the laptop using acpi_listen.

### Other

USB 3.0 has not been tested but should be working. The USB 3.0 driver in the Linux kernel is located in:

```
Device Drivers -> USB Support -> xHCI HCD (USB 3.0) support (EXPERIMENTAL)
SYMBOL: USB_XHCI_HCD

```

Retrieved from "[https://wiki.archlinux.org/index.php?title=Dell_XPS_14z&oldid=384008](https://wiki.archlinux.org/index.php?title=Dell_XPS_14z&oldid=384008)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Dell](/index.php/Category:Dell "Category:Dell")