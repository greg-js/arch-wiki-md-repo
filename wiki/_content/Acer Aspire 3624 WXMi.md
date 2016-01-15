# Acer Aspire 3624 WXMi

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-emblem-symbolic-link.png](/images/f/f9/Tango-emblem-symbolic-link.png)](/index.php/File:Tango-emblem-symbolic-link.png)

[![Tango-emblem-symbolic-link.png](/images/f/f9/Tango-emblem-symbolic-link.png)](/index.php/File:Tango-emblem-symbolic-link.png)

**This article is being considered for redirection to [Laptop](/index.php/Laptop "Laptop").**

**Notes:** Info in this page is out of data and should redirect to [Laptop](/index.php/Laptop "Laptop"). (Discuss in [Talk:Acer Aspire 3624 WXMi#](https://wiki.archlinux.org/index.php/Talk:Acer_Aspire_3624_WXMi))

Article based on [Acer Aspire 1652 ZWLMi](/index.php?title=Acer_Aspire_1652_ZWLMi&action=edit&redlink=1 "Acer Aspire 1652 ZWLMi (page does not exist)"), which in turn was based on [Acer Aspire 1691 WLMi](/index.php/Acer_Aspire_1691_WLMi "Acer Aspire 1691 WLMi").

## lspci

```
00:00.0 Host bridge: Intel Corporation Mobile 915GM/PM/GMS/910GML Express Processor to DRAM Controller (rev 03)
00:02.0 VGA compatible controller: Intel Corporation Mobile 915GM/GMS/910GML Express Graphics Controller (rev 03)
00:02.1 Display controller: Intel Corporation Mobile 915GM/GMS/910GML Express Graphics Controller (rev 03)
00:1d.0 USB Controller: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) USB UHCI #1 (rev 03)
00:1d.1 USB Controller: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) USB UHCI #2 (rev 03)
00:1d.2 USB Controller: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) USB UHCI #3 (rev 03)
00:1d.3 USB Controller: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) USB UHCI #4 (rev 03)
00:1d.7 USB Controller: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) USB2 EHCI Controller (rev 03)
00:1e.0 PCI bridge: Intel Corporation 82801 Mobile PCI Bridge (rev d3)
00:1e.2 Multimedia audio controller: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) AC'97 Audio Controller (rev 03)
00:1e.3 Modem: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) AC'97 Modem Controller (rev 03)
00:1f.0 ISA bridge: Intel Corporation 82801FBM (ICH6M) LPC Interface Bridge (rev 03)
00:1f.1 IDE interface: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) IDE Controller (rev 03)
00:1f.3 SMBus: Intel Corporation 82801FB/FBM/FR/FW/FRW (ICH6 Family) SMBus Controller (rev 03)
06:05.0 Ethernet controller: Atheros Communications, Inc. AR2413 802.11bg NIC (rev 01)
06:07.0 Ethernet controller: Realtek Semiconductor Co., Ltd. RTL-8139/8139C/8139C+ (rev 10)
06:09.0 CardBus bridge: ENE Technology Inc CB1410 Cardbus Controller (rev 01)

```

# Installing Arch Linux

# Xorg

The intel driver doesn't like to set the DPI according to forced physical dimensions, so there is a trick to get the desired DPI (81x81). In the user's ~/.bashrc the following line was added:

```
alias xinit='xinit -- -dpi 81'

```

So that when issuing the xinit command, it will always use that DPI resolution.

Retrieved from "[https://wiki.archlinux.org/index.php?title=Acer_Aspire_3624_WXMi&oldid=415198](https://wiki.archlinux.org/index.php?title=Acer_Aspire_3624_WXMi&oldid=415198)"

[Category](/index.php/Special:Categories "Special:Categories"):

*   [Acer](/index.php/Category:Acer "Category:Acer")

Hidden category:

*   [Pages flagged with Template:Redirect](/index.php/Category:Pages_flagged_with_Template:Redirect "Category:Pages flagged with Template:Redirect")