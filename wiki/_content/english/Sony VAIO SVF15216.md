This wiki entry describes some tips of Installation of ArchLinux on a Sony VAIO SVF15216 laptop.

## Wifi

Our SVF15216 comes with BCM43142 an its a little problematic with some distros, but no in Arch x86_64 (if you chose de correct package). You can use the BCM43142 by using the "broadcom-wl-dkms" package. There is also a PKGBUILD available in [AUR](https://aur.archlinux.org/packages/broadcom-wl-dkms/)

## Fan Speed

You can control the fan speed by using the **vaiofand** daemon that you can find on this address : [http://vaio-utils.org/fan/](http://vaio-utils.org/fan/) There is also a PKGBUILD available in [AUR](https://aur.archlinux.org/packages.php?ID=38826).

## Power Saving

You can automatically turn of some device like the bluetooth, the firewire port, the cd/dvd drive or the audio card by using the **vaiopower** daemon that you can find on this address : [http://vaio-utils.org/power/](http://vaio-utils.org/power/) There is also a PKGBUILD available in [AUR](https://aur.archlinux.org/packages/vaiopower/).