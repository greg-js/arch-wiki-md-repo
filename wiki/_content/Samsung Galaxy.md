# Samsung Galaxy

Here are the steps to mount a Samsung Galaxy SII from command line:

From the smart phone: Go to settings > Wireless and network > USB utilities.

Click on the "Connect storage to PC" icon.

Now, Plug the cable into the phone and to the computer.

You will get a new screen that says "USB Connected". Click the "Connect USB storage" icon.

You will get a new colored andoid screen showing that the USB mass storage is active.

Su or sudo to root.

```
mount /dev/sdb /mnt/usb

```

You will now be able to transfer your files back and forth from command line.

reverse out your steps when you unmount.

**If you have some troubles, install go-mtpfs from** [AUR](https://wiki.archlinux.org/index.php/Arch_User_Repository). For more detail, check [go-mtpfs](https://wiki.archlinux.org/index.php/MTP#go-mtpfs).

Retrieved from "[https://wiki.archlinux.org/index.php?title=Samsung_Galaxy&oldid=248663](https://wiki.archlinux.org/index.php?title=Samsung_Galaxy&oldid=248663)"