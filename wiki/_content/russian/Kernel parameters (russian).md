Существует три способа передачи параметров ядру и контроля над ним:

1.  При сборке ядра. Полная информация [Kernel Compilation](/index.php/Kernel_Compilation "Kernel Compilation").
2.  При запуске ядра (через системный загрузчик).
3.  На этапе выполнения (через файлы в `/proc` и `/sys`). Более подробно смотрите документацию по утилите [sysctl](/index.php/Sysctl "Sysctl").

This page now explains in more detail the second method and shows a list of most used kernel parameters in Arch Linux.

## Contents

*   [1 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [1.1 Syslinux](#Syslinux)
    *   [1.2 GRUB](#GRUB)
    *   [1.3 GRUB Legacy](#GRUB_Legacy)
    *   [1.4 iPXE](#iPXE)
    *   [1.5 LILO](#LILO)
    *   [1.6 Gummiboot](#Gummiboot)
    *   [1.7 rEFInd](#rEFInd)
*   [2 Список параметров](#.D0.A1.D0.BF.D0.B8.D1.81.D0.BE.D0.BA_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2)
*   [3 Ссылки](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Настройка

**Примечание:** You can check the parameters your system was booted up with by running `$ cat /proc/cmdline` and see if it includes your changes.

Kernel parameters can be set either temporarily by editing the boot menu when it shows up, or by modifying the boot loader's configuration file.

Here we are adding the parameters `quiet` and `splash` to [Syslinux](/index.php/Syslinux "Syslinux"), [GRUB](/index.php/GRUB "GRUB"), [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy"), [LILO](/index.php/LILO "LILO"), [gummiboot (Русский)](/index.php/Gummiboot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Gummiboot (Русский)") and [rEFInd (Русский)](/index.php/REFInd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "REFInd (Русский)").

#### Syslinux

*   Press `Tab` when the menu shows up and add them at the end of the string:

	 `linux /boot/vmlinuz-linux root=/dev/sda3 initrd=/boot/initramfs-linux.img *quiet splash*` 

	Press `Enter` to boot with these parameters.

*   To make the change persistent after reboot, edit `/boot/syslinux/syslinux.cfg` and add them to the `APPEND` line:

	 `APPEND root=/dev/sda3 *quiet splash*` 

For more information on configuring Syslinux, see the [Syslinux](/index.php/Syslinux "Syslinux") article.

#### GRUB

*   Нажмите `e` в момент показа загрузочного меню и добавьте в строку, содержащую `linux`:

	 `linux /boot/vmlinuz-linux root=UUID=978e3e81-8048-4ae1-8a06-aa727458e8ff *quiet splash*` 

	Нажмите `b` для загрузки с этими параметрами.

*   To make the change persistent after reboot, while you *could* manually edit `/boot/grub/grub.cfg` with the exact line from above, for beginners it's recommended to:

	Edit `/etc/default/grub` and append your kernel options to the `GRUB_CMDLINE_LINUX_DEFAULT` line:

	 `GRUB_CMDLINE_LINUX_DEFAULT="*quiet splash*"` 

	And then automatically re-generate the `grub.cfg` file with:

	 `# grub-mkconfig -o /boot/grub/grub.cfg` 

Полная информация по настройке [GRUB](/index.php/GRUB "GRUB").

#### GRUB Legacy

*   Press `e` when the menu shows up and add them on the `kernel` line:

	 `kernel /boot/vmlinuz-linux root=/dev/sda3 *quiet splash*` 

	Press `b` to boot with these parameters.

*   To make the change persistent after reboot, edit `/boot/grub/menu.lst` and add them to the `kernel` line, exactly like above.

Полная информация по настройке [GRUB Legacy](/index.php/GRUB_Legacy "GRUB Legacy").

#### iPXE

```
#!ipxe

kernel http://mirror.yandex.ru/archlinux/iso/2014.11.01/arch/boot/x86_64/vmlinuz archiso_http_srv=http://mirror.yandex.ru/archlinux/iso/2014.11.01/ archisobasedir=arch checksum=y ip=dhcp
initrd http://mirror.yandex.ru/archlinux.iso/2014.11.01/arch/boot/x86_64/archiso.img
boot

```

Полная информация по настройке [iPXE - open source boot firmware](http://ipxe.org/).

#### LILO

*   Добавить `/etc/lilo.conf`:

```
image=/boot/vmlinuz-linux
        ...
        *quiet splash*
```

Полная информация по настройке [LILO](/index.php/LILO "LILO").

#### Gummiboot

*   Press `e` when the menu appears and add the parameters to the end of the string:

	 `initrd=\initramfs-linux.img root=/dev/sda2 rw *quiet splash*` 

	Press `Enter` to boot with these parameters.

**Примечание:** If you have not set a value for menu timeout, you will need to hold `Space` while booting for the Gummiboot menu to appear.

*   To make the change persistent after reboot, edit `/boot/loader/entries/arch.conf` (assuming you set up your [EFI System Partition](/index.php/Unified_Extensible_Firmware_Interface#EFI_System_Partition "Unified Extensible Firmware Interface") and configuration files according to the instructions in the [Beginners' Guide](/index.php/Beginners%27_guide#Gummiboot "Beginners' guide")) and add them to the `options` line:

	 `options root=/dev/sda2 rw *quiet splash*` 

Полная информация по настройке [gummiboot (Русский)](/index.php/Gummiboot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Gummiboot (Русский)").

#### rEFInd

*   To make the change persistent after reboot, edit `/boot/EFI/arch/refind_linux.conf` (ie. refind_linux.conf in the folder your kernel is located in) and append them to all/required lines, for example:

	 `"Boot to X"   "root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff ro rootfstype=ext4 quiet splash` 

*   If you've disabled auto-detection of OS's in rEFInd and are defining OS stanzas instead in `/boot/EFI/refind/refind.conf` to load your OS's, you can edit it like:

```
menuentry "Arch" {
	loader /EFI/arch/vmlinuz-arch.efi
	options "quiet splash ro root=PARTUUID=978e3e81-8048-4ae1-8a06-aa727458e8ff"
```

Полная информация по настройке [Менеджер загрузки rEFInd](http://www.rodsbooks.com/refind/linux.html)

## Список параметров

Parameters always come in `parameter` or `parameter=value`. All of these parameters are case-sensitive.

**Примечание:** Not all of the listed options are always available. Most are associated with subsystems and work only if the kernel is configured with those subsystems built in. They also depend on the presence of the hardware they are associated with.

| Параметр | Описание |
| root= | Корневая файловая система. |
| ro | При загрузке монтировать корневую ФС только в режиме чтения (default). |
| rw | При загрузке монтировать корневую ФС в режиме чтения/записи. |
| initrd= | Путь образа-инициализатора. |
| init= | Запустить процесс пользовательского режима `/sbin/init` (ссылка на [systemd](/index.php/Systemd "Systemd") в Arch). |
| init=/bin/sh | Boot to shell. |
| systemd.unit= |
| systemd.unit=multi-user | Boot to a specified runlevel. |
| systemd.unit=rescue | Загрузка в однопользовательском режиме (root). |
| nomodeset | Disable [Kernel Mode Setting](/index.php/Kernel_Mode_Setting "Kernel Mode Setting"). |
| zswap.enabled | Enable [Zswap](/index.php/Zswap "Zswap"). |

 [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") uses `ro` as default value when neither `rw` or `ro` is set by the [boot loader](/index.php/Boot_loaders "Boot loaders"). Boot loaders may set the value to use, for example GRUB uses `rw` by default (see [FS#36275](https://bugs.archlinux.org/task/36275) as a reference).

Полный список всех опций смотрите в [документации](https://www.kernel.org/doc/Documentation/kernel-parameters.txt).

## Ссылки

*   [Power saving#Kernel parameters](/index.php/Power_saving#Kernel_parameters "Power saving")
*   [List of kernel parameters with further explanation and grouped by similar options](http://files.kroah.com/lkn/lkn_pdf/ch09.pdf)
*   [iPXE - open source boot firmware](http://ipxe.org/)