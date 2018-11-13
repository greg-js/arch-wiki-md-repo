Тази страница обяснява как да приготви инсталационно USB (флашка) за ArchLinux. Крайният резултат е LiveCD от който можете да инсталирате.

## Contents

*   [1 Създаване под GNU/Linux](#Създаване_под_GNU/Linux)
    *   [1.1 Arch USB images](#Arch_USB_images)
    *   [1.2 С UNetBootin](#С_UNetBootin)
    *   [1.3 С Gujin](#С_Gujin)
*   [2 Създаване под Mac OS X](#Създаване_под_Mac_OS_X)
*   [3 Създавене под Windows](#Създавене_под_Windows)
    *   [3.1 С програмата Flashnul](#С_програмата_Flashnul)
    *   [3.2 Със Cygwin](#Със_Cygwin)
    *   [3.3 win32 disk imager](#win32_disk_imager)
    *   [3.4 С UNetBootin](#С_UNetBootin_2)
*   [4 Стар метод с ISO](#Стар_метод_с_ISO)
    *   [4.1 After booting from the USB stick:](#After_booting_from_the_USB_stick:)
    *   [4.2 Бележки:](#Бележки:)

## Създаване под GNU/Linux

### Arch USB images

При всички версии след 2010.05, iso файловете могат директно да бъдат записвани върху USB медии. Свалете ги от [[1]](https://archlinux.org/download/). Демонтирайте USB устройството и след това въведете следната команда:

```
$ dd if=image.iso of=/dev/sd[x]

```

*image.iso* е пътя към iso файла, а */dev/sd[x]* е USB устройството. ***Проверете че ползвате /dev/sdx а НЕ /dev/sdx1.*** **Това е често срещана грешка!**

Тази команда ще изтрие всичко на USB устройството.

### С UNetBootin

Друг начин да създадете boot USB е с програмата [UNetBootin](http://unetbootin.sourceforge.net/). Самата програма сваля дадената дистрибуция и я записва на флашката. UNetBootin не ползва най-новия Arch ISO, но за сметка на това можете да зададете собствен ISO файл.

След като Unetbootin приключи, трябва да модифицирате syslinux.cfg на root раздела на флашката преди да рестартирате. Поправете параметъра "archisolabel=" да ползва името на USB устройството, т.е.:

```
append initrd=/ubninit archisolabel=<label> tmpfs_size=75% locale=en_US.UTF-8

```

### С Gujin

A third method is to follow the instructions about [Booting multiple LiveCD's from a single USB stick](http://psychoticspoon.blogspot.com/2009/01/booting-multiple-livecds-from-single.html). In a nutshell, you create 2 partitions on your USB drive, copy the [Gujin](http://gujin.sourceforge.net/) boot loader image to the first partition, and copy Arch's ISO to the second.

## Създаване под Mac OS X

To be able to use dd on your usb device on a Mac you have to do some special maneuvers. First of all insert your usb device, OS X will automount it, and run

```
diskutil list

```

in Terminal.app. Figure out what your usb device is called - mine was called /dev/disk1\. (Just use the `mount` command or `sudo dmesg | tail`.) Now you run

```
diskutil unmountDisk /dev/disk1

```

to unmount the partitions on the device (i.e., /dev/disk1s1) while keeping the device proper (i.e., /dev/disk1). Now we can continue in accordance with the Linux instructions above (but use bs=8192 if you're using the OS X dd, the number comes from 1024*8).

```
 dd if=image.iso of=/dev/disk1 bs=8192
 20480+0 records in
 20480+0 records out
 167772160 bytes transferred in 220.016918 secs (762542 bytes/sec)

```

## Създавене под Windows

To write the USB image on Windows, you will need [flashnul](http://shounen.ru/soft/flashnul/) ([English version of the page](http://translate.google.com/translate?u=http%3A%2F%2Fshounen.ru%2Fsoft%2Fflashnul%2F&hl=en&ie=UTF8&sl=ru&tl=en)) or [Cygwin](http://www.cygwin.com/).

### С програмата Flashnul

From a command prompt, invoke flashnul with -p, and determine which device index is your USB drive. For example, my output looks like this:

```
C:\>flashnul -p

Avaible [sic] physical drives:
0       size = 200048565760 (186 Gb)
1       size = 400088457216 (372 Gb)
2       size = 400088457216 (372 Gb)
3       size = 4060086272 (3872 Mb)

```

In my case, with a 4 GB USB drive, it is device index 3.

When you have determined which device is the correct one, you can write the image to your drive, by invoking flashnul with the device index, -L, and the path to your image. In my case, it would be

```
C:\>flashnul 3 -L path\to\arch\usb.iso

```

As long as you are really sure you want to write the data, type yes, then wait a bit for it to write. If you get an access denied error, unplugging and re-attaching the drive worked for me.

If under Vista or Win7, you should open the console as administrator, or else flashnul will fail to open the stick as a block device and will only be able to write via the drive handle windows provides

**Note:** *I had to do "C:\flashnul\flashnul.exe **H:** -L c:\archlinux-2008.06-core-i686.img" for it to work. I kept getting access denied if i just used the number. -gejr*

**Note:** *The output of flashnul -p was considerably different for me. No numbers were returned or block information, just a list of logical drive mappings (C:, D:, etc..) so I just did flashnul -L archlinux.img E: --[Kahrn](/index.php?title=User:Kahrn&action=edit&redlink=1 "User:Kahrn (page does not exist)") 18:12, 28 April 2010 (EDT)*

**Note:** *Confirmed that you need to use drive letter as opposed to number. flashnul 1rc1, Windows 7 x64\. -bgalakazam*

### Със Cygwin

Make sure your cygwin installation contains the dd package. Or if you don't want to install Cygwin, you can simply download dd for windows from [http://www.chrysocome.net/dd](http://www.chrysocome.net/dd).

Place your image file in your home directory, in my case it is:

```
C:\cygwin\home\John\

```

Run cygwin as administrator (required for cygwin to access hardware). To write to your USB drive use the following command:

```
dd if=image.iso of=\\.\[x]:

```

where image.iso is the path to the iso-image file within the cygwin directory and \\.\[x]: is your USB device where x is the windows designated letter, in my case "\\.\d:".

**Note:** This will irrevocably delete all files on your USB stick, so make sure you don't have any important files on the stick before doing this.

### win32 disk imager

Download win32 disk imager from [http://launchpad.net/win32-image-writer](http://launchpad.net/win32-image-writer). Run the program. Select the arch image-file and usb stick. The Win32 Disk Imager's file browser assumes image files end with .img, so if the image-file you've selected ends with .iso, you will have to type its name in manually; this difference in suffixes is simply cosmetic however, the image will be written fine regardless. Click on the write button. Now you should be able to boot from the usb stick and install Arch Linux from it.

### С UNetBootin

Another way to make a USB drive bootable, is by using UNetBootin ([see above](#С_UNetBootin)).

## Стар метод с ISO

*   Prepare USB stick:

The arch-ftp.img is about 150 MB, so it should fit on a 256 MB USB stick. The arch-core.img is ~300 MB and should fit on a 512 MB stick.

1\. Partition the USB stick. Create one partition with FAT16 type, make it bootable. Remember its name, such as /dev/sd[x]1.

```
cfdisk /dev/sd[x]

```

2\. Make a FAT16 filesystem (you need dosfstools)

```
mkdosfs /dev/sd[x]1

```

3\. Get the arch-base install ISO from www.archlinux.org

4\. Mount the iso to an temporary directory

```
mkdir -p /mnt/archcd
mount -o loop /Path/to/iso /mnt/archcd

```

5\. Mount the USB Stick

```
mkdir -p /mnt/usb/
mount /dev/sd[x]1 /mnt/usb/

```

6\. Copy the .iso to the USB Stick

```
cp -ra /mnt/archcd/* /mnt/usb/

```

7\. Copy the boot data

```
cd /mnt/usb/isolinux/
cp vmlinuz /mnt/usb/
cp initrd.img /mnt/usb/
cp boot.* /mnt/usb/
cp isolinux.cfg /mnt/usb/syslinux.cfg

```

8\. Install MBR and syslinux

```
lilo -M /dev/sd[x] mbr
syslinux -s /dev/sd[x]1

```

### After booting from the USB stick:

Start the installation by logging in as root and invoke the command "/arch/setup".

The installer should mount the source media automatically. If it fails you can manually mount the source media on the stick to the /src directory with the following command:

```
mount /dev/sd[x] /src

```

### Бележки:

 Using lilo is not really needed because syslinux does the "floppy" loading stuff. But if you get some error like "Can't load operating system" you have to perform the lilo command.

 If you get "Cluster sizes larger than 16K not supported" error when booting this means you need to install more recent version of syslinux.

 Space not used on the USB stick can still be used for storing files... Use a utility like gparted and add a partition to the unused space.