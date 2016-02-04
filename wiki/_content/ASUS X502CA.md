# ASUS X502CA

This laptop has some hardware that does not work well out of-the-box. With some extra effort it should work on Arch Linux with the possible exception of the wireless interface. For those that are considering this laptop for Linux use: Reconsider, there are Asus laptops that are probably better suited for Linux.

## Contents

*   [1 Ethernet interface](#Ethernet_interface)
*   [2 Wireless interface:](#Wireless_interface:)
*   [3 Graphics interface](#Graphics_interface)
*   [4 Booting](#Booting)
*   [5 Touchpad](#Touchpad)

## Ethernet interface

The initial install was not smooth. The built-in Atheros Ethernet interface did not work during installation. During my installation I used the wireless interface that works very poorly with the native kernel driver. After installation the ethernet interface works OK. At the time of writing following is needed: [https://bbs.archlinux.org/viewtopic.php?pid=1331741](https://bbs.archlinux.org/viewtopic.php?pid=1331741)

## Wireless interface:

The native kernel support is very poor. If the wifi is very strong it might connect but the connection is unreliable. When the field is weak do not bother. An alternative is to try [rt3290sta-dkms](https://aur.archlinux.org/packages/rt3290sta-dkms/) instead. This works better. But I have experienced that the connections stops working maybe about once an hour. Everything seems fine but no data is transmitted. The connection works after disconnect - connect.

## Graphics interface

This works mostly well. I had to add a kernel parameter to get brightness control working: "!Windows 2012" Yes, the parameter must contain the "-characters. I added it to my uefi-boot:

```
# efibootmgr -v -c -L "Arch Linux acpi_osi_not_windows" -l /vmlinuz-linux -u 'root=/dev/sda2 rw initrd=/initramfs-linux.img cpi_osi="!Windows 2012"'

```

The relevant discussion can be found here: [https://bbs.archlinux.org/viewtopic.php?id=164928](https://bbs.archlinux.org/viewtopic.php?id=164928)

Sometimes not very often the screen shows some corrupted lines when scrolling. I have no idea what is the cause for this. The problem disappears after a reboot.

## Booting

I am satisfied with the UEFI-boot method. It works as expected and booting is very fast. I have only Linux so I do not know how dual booting with Windows is working.

## Touchpad

I have tried to configure this. I am not really satisfied with the huge touchpad and my configuration so I will not post my configuration. Useful information should be found here:

*   [Touchpad Synaptics](/index.php/Touchpad_Synaptics "Touchpad Synaptics")
*   [http://askubuntu.com/questions/128023/synaptics-touchpad-sensitivity-issue](http://askubuntu.com/questions/128023/synaptics-touchpad-sensitivity-issue)

Retrieved from "[https://wiki.archlinux.org/index.php?title=ASUS_X502CA&oldid=356042](https://wiki.archlinux.org/index.php?title=ASUS_X502CA&oldid=356042)"