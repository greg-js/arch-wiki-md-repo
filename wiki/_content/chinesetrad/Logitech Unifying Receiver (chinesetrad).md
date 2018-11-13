[羅技 Unifying 接收器](http://www.logitech.com/zh-tw/promotions/6072)是無線裝置的接收器，可同時連接最多六個相容滑鼠及鍵盤。 和該接收器一組的輸入裝置已預先配對，並能隨插即用。而針對額外的輸入裝置，羅技僅提供 Windows 軟體以供配對。 不過 [Benjamin Tissoires](http://goo.gl/eG4q9) 在 kernel mailing list 發表了一支程式，令 Linux 下也有其功能。

## Contents

*   [1 編譯 unifying_pair](#編譯_unifying_pair)
*   [2 相容裝置配對](#相容裝置配對)
*   [3 Known Problems](#Known_Problems)
    *   [3.1 Keyboard Layout via xorg.conf](#Keyboard_Layout_via_xorg.conf)

## 編譯 unifying_pair

此程式亦可於 [AUR](https://aur.archlinux.org/packages.php?ID=58261) 找到。

首先確定系統已安裝了 C 編譯器。

```
# pacman -S gcc 

```

將下列程式碼複制到檔案並命名，假設名為 *unifying_pair.c*。

```
/*
* Copyright 2011 Benjamin Tissoires 
*
* This program is free software: you can redistribute it and/or modify
* it under the terms of the GNU General Public License as published by
* the Free Software Foundation, either version 3 of the License, or
* (at your option) any later version.
*
* This program is distributed in the hope that it will be useful,
* but WITHOUT ANY WARRANTY; without even the implied warranty of
* MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
* GNU General Public License for more details.
*
* You should have received a copy of the GNU General Public License
* along with this program.  If not, see .
*/

#include <linux/input.h>
#include <linux/hidraw.h>
#include <sys/ioctl.h>
#include <fcntl.h>
#include <unistd.h>
#include <stdio.h>
#include <errno.h>

#define USB_VENDOR_ID_LOGITECH                  (__u32)0x046d
#define USB_DEVICE_ID_UNIFYING_RECEIVER         (__s16)0xc52b
#define USB_DEVICE_ID_UNIFYING_RECEIVER_2       (__s16)0xc532

int main(int argc, char **argv)
{
       int fd;
       int res;
       struct hidraw_devinfo info;
       char magic_sequence[] = {0x10, 0xFF, 0x80, 0xB2, 0x01, 0x00, 0x00};

       if (argc == 1) {
               errno = EINVAL;
               perror("No hidraw device given");
               return 1;
       }

       /* Open the Device with non-blocking reads. */
       fd = open(argv[1], O_RDWR|O_NONBLOCK);

       if (fd < 0) {
               perror("Unable to open device");
               return 1;
       }

       /* Get Raw Info */
       res = ioctl(fd, HIDIOCGRAWINFO, &info);
       if (res < 0) {
               perror("error while getting info from device");
       } else {
               if (info.bustype != BUS_USB ||
                   info.vendor != USB_VENDOR_ID_LOGITECH ||
                   (info.product != USB_DEVICE_ID_UNIFYING_RECEIVER &&
                    info.product != USB_DEVICE_ID_UNIFYING_RECEIVER_2)) {
                       errno = EPERM;
                       perror("The given device is not a Logitech "
                               "Unifying Receiver");
                       return 1;
               }
       }

       /* Send the magic sequence to the Device */
       res = write(fd, magic_sequence, sizeof(magic_sequence));
       if (res < 0) {
               printf("Error: %d
", errno);
               perror("write");
       } else if (res == sizeof(magic_sequence)) {
               printf("The receiver is ready to pair a new device.
"
               "Switch your device on to pair it.
");
       } else {
               errno = ENOMEM;
               printf("write: %d were written instead of %ld.
", res,
                       sizeof(magic_sequence));
               perror("write");
       }
       close(fd);
       return 0;
}

```

將原始碼編譯成可執行檔 *unifying_pair*：

```
$ gcc -o unifying_pair unifying_pair.c 

```

## 相容裝置配對

下一步需要尋找接收器裝置的位置，因此觀察下列命令的輸出

```
$ cat /sys/class/hidraw/hidraw**X**/device/uevent |grep NAME

```

(你必須把 **X** 替換成系統上存在的整數) 直到找到 *Logitech USB Receiver* 為止(在此假設 X 恰為 **0**)

```
$ cat /sys/class/hidraw/hidraw0/device/uevent |grep NAME
  HID_NAME=Logitech USB Receiver

```

如果想要配對的裝置現在是開著時，關掉並執行適才編譯過的程式，以合適的裝置做為其參數：

```
# ./unifying_pair /dev/hidraw0

```

若順利該程式會告知你打開欲配對的裝置，且該裝置應該也會正常運作。

## Known Problems

### Keyboard Layout via xorg.conf

With kernel 3.2 the Unifying Receiver got its own kernel module *hid_logitech_dj* which does not work flawlessly together with keyboard layout setting set via [xorg.conf](/index.php/Xorg#Keyboard_settings "Xorg"). A temporary workaround is to use [xorg-setxkbmap](https://www.archlinux.org/packages/?name=xorg-setxkbmap) and set the layout manually. For example for a German layout with no deadkeys one has to execute:

```
$ setxkbmap -layout de -variant nodeadkeys

```

To automate this process one could add this line to [xinitrc](/index.php/Xinitrc "Xinitrc").