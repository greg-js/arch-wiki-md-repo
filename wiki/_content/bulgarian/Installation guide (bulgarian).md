Тази страница е ръководство за исталирането на [Arch Linux](/index.php/Arch_Linux "Arch Linux") от “живия“ диск зареден от официалния инсталационен образ. Преди инсталиране е препорачително да погледнете [често задаваните въпроси](/index.php/FAQ "FAQ"). За нормите използвани в този документ вижте [Help:Reading](/index.php/Help:Reading "Help:Reading"). В частност , примери форматирани с `*курсив*` трябва да бъдат заменени.

За по обстойни иструкции вижте съответните [ArchWiki](/index.php/ArchWiki "ArchWiki") страници или [man page](/index.php/Man_page "Man page") ръководства на самите програми, връзки и за двете от които са налични на тази страница. При нужда от помощ може да се обърнете към [чат-а](/index.php/IRC_channel "IRC channel") или да оставите своите въпроси във [форума](https://bbs.archlinux.org/).

Arch Linux би трябвало да работи на всяка [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64") съвместима машина с поне 512 MB RAM. Основна инсталация с всички пакети от група [base](https://www.archlinux.org/groups/x86_64/base/) може да заеме по-малко от 800 MB of дисково пространство. Тъй като инсталационният процес трябва да вземе пакети от външни хранилища, това ръководство приема, че е налична работеща интернет връзка.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Преди инсталацията](#Преди_инсталацията)
    *   [1.1 Verify signature](#Verify_signature)
    *   [1.2 Включете живата среда](#Включете_живата_среда)
    *   [1.3 Изберете клавиатурна подредба](#Изберете_клавиатурна_подредба)
    *   [1.4 Проверете boot режима](#Проверете_boot_режима)
    *   [1.5 Свързване с интернет](#Свързване_с_интернет)
    *   [1.6 Обновяване на системния часовник](#Обновяване_на_системния_часовник)
    *   [1.7 Разделяне на дялове](#Разделяне_на_дялове)
    *   [1.8 Форматиране на дяловете](#Форматиране_на_дяловете)
    *   [1.9 Включване на файловите системи](#Включване_на_файловите_системи)
*   [2 Инсталиране](#Инсталиране)
    *   [2.1 Избиране на източник](#Избиране_на_източник)
    *   [2.2 Инсталиране на основни пакети](#Инсталиране_на_основни_пакети)
*   [3 Настройване на системата](#Настройване_на_системата)
    *   [3.1 Fstab](#Fstab)
    *   [3.2 Chroot](#Chroot)
    *   [3.3 Времева зона](#Времева_зона)
    *   [3.4 Локализиране](#Локализиране)
    *   [3.5 Настройване на мрежи](#Настройване_на_мрежи)
    *   [3.6 Initramfs](#Initramfs)
    *   [3.7 Root парола](#Root_парола)
    *   [3.8 Boot loader](#Boot_loader)
*   [4 Рестартиране](#Рестартиране)
*   [5 След инсталиране](#След_инсталиране)

## Преди инсталацията

Ще откриете инсталационния диск и съпътстващите го [GnuPG](/index.php/GnuPG "GnuPG") подписи на [Download](https://archlinux.org/download/) страницата.

### Verify signature

Преди да използвате диска е препоръчетелно да проверите подписите му, особено когато е свален от *HTTP mirror*, изтеглянията ог който могат да бъдат [промеменени](http://www.cs.arizona.edu/stork/packagemanagersecurity/attacks-on-package-managers.html#explanation).

On a system with [GnuPG](/index.php/GnuPG "GnuPG") installed, do this by downloading the *PGP signature* (under *Checksums*) to the ISO directory, and [verifying](/index.php/GnuPG#Verify_a_signature "GnuPG") it with `gpg --keyserver pgp.mit.edu --keyserver-options auto-key-retrieve --verify archlinux-<version>-x86_64.iso.sig`.

Alternatively, run `pacman-key -v archlinux-<version>-x86_64.iso.sig` from an existing Arch Linux installation as root.

**Note:**

*   The signature itself could be manipulated if it is downloaded from a mirror site, instead of from [archlinux.org](https://archlinux.org/download/) as above. In this case, ensure that the public key, which is used to decode the signature, is signed by another, trustworthy key. The `gpg` command will output the fingerprint of the public key.
*   Another method to verify the authenticity of the signature is to ensure that the public key's fingerprint is identical to the key fingerprint of the [Arch Linux developer](https://www.archlinux.org/people/developers/) who signed the ISO-file. See [Wikipedia:Public-key_cryptography](https://en.wikipedia.org/wiki/Public-key_cryptography "wikipedia:Public-key cryptography") for more information on the public-key process to authenticate keys.

### Включете живата среда

„Живата“ среда може да бъде включена от [USB флашка](/index.php/USB_flash_installation_media "USB flash installation media"), [компакт диск](/index.php/Optical_disc_drive#Burning "Optical disc drive") или по мрежа с [PXE](/index.php/PXE "PXE"). За други инсталационни начини, вижте [Category:Installation process](/index.php/Category:Installation_process "Category:Installation process").

*   За да изберете носителя с Arch, вероятно трябва да натиснете клавиш по време на [автоматичения тест при включване](https://en.wikipedia.org/wiki/Power-on_self_test "w:Power-on self test"). Погледнете ръководството на дънната платка на компютъра Ви за повече информация.
*   Щом се появи менюто на Arch, изберете *Boot Arch Linux* и натиснете `Enter` за да влезете в инсталационната среда.
*   Вижте [README.bootparams](https://projects.archlinux.org/archiso.git/tree/docs/README.bootparams) за списък с [boot параметри](/index.php/Kernel_parameters#Configuration "Kernel parameters"), и [x86_64](https://git.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) за списък с включените пакети.

Ще бъдете логнати в първата [виртуална конзола](https://en.wikipedia.org/wiki/Virtual_console "wikipedia:Virtual console") като root потребител със [Zsh](/index.php/Zsh "Zsh") шел.

За да смените с друга конзола — например, за да видите това ръководство с [ELinks](/index.php/ELinks "ELinks") по време на инсталацията — натиснете [клавишната комбинация](/index.php/Keyboard_shortcuts#Virtual_console "Keyboard shortcuts") `Alt+*стрелка*`. За да [редактирате](/index.php/Textedit "Textedit") конфигурационни файлове, използвайте [nano](/index.php/Nano#Usage "Nano"), [vi](https://en.wikipedia.org/wiki/vi "wikipedia:vi") или [vim](/index.php/Vim#Usage "Vim").

### Изберете клавиатурна подредба

Първоначално избраната [конзолна клавиатурна подредба](/index.php/Console_keymap "Console keymap") е [US](https://en.wikipedia.org/wiki/File:KB_United_States-NoAltGr.svg "wikipedia:File:KB United States-NoAltGr.svg"). Други достъпни оформления могат да бъдат изброени с:

```
# ls /usr/share/kbd/keymaps/**/*.map.gz

```

За да промените клавиатурата добавете името на файла ѝ към [loadkeys(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/loadkeys.1), пропускайки пътя и разширението. Например, за да изберете [германска](https://en.wikipedia.org/wiki/File:KB_Germany.svg "wikipedia:File:KB Germany.svg") клавиатурна подредба:

```
# loadkeys de-latin1

```

[Конзолните шрифтове](/index.php/Console_fonts "Console fonts") се намират в `/usr/share/kbd/consolefonts/` и се избират със [setfont(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setfont.8).

### Проверете boot режима

Ако е избран UEFI режим на [UEFI](/index.php/UEFI "UEFI") дънна платка, [Archiso](/index.php/Archiso "Archiso") ще [включи](/index.php/Boot "Boot") Arch Linux чрез [systemd-boot](/index.php/Systemd-boot "Systemd-boot"). За да проверите това, проверете [efivars](/index.php/UEFI#UEFI_variables "UEFI") директорията:

```
# ls /sys/firmware/efi/efivars

```

Ако директорията не съществува, системата може да зареди в [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") или CSM режим. Проверете ръководството на дънната ви платка за детайли.

### Свързване с интернет

Инсталационният образ включва [dhcpcd](/index.php/Dhcpcd "Dhcpcd") за [жична връзка](https://git.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) при включване. Връзката може да бъде потвърдена с [ping](https://en.wikipedia.org/wiki/ping_(networking_utility) "wikipedia:ping (networking utility)"):

```
# ping archlinux.org

```

Ако връзка не е достъпна, [stop](/index.php/Stop "Stop") *dhcpcd* със `systemctl stop dhcpcd@*interface*` където `*interface*` може да бъде [tab-completed](https://en.wikipedia.org/wiki/Command-line_completion "wikipedia:Command-line completion"). Продължете с настройването на мрежата според [Network configuration](/index.php/Network_configuration "Network configuration").

### Обновяване на системния часовник

Използвайте [timedatectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/timedatectl.1) за да се уверите, че системният часовник е точен:

```
# timedatectl set-ntp true

```

За да проверите състоянието на услугата, използвайте `timedatectl status`.

### Разделяне на дялове

Разпознатите от системата твърдите дискове са показани като `/dev/sda` или `/dev/nvme0n1` ([block устройства](https://en.wikipedia.org/wiki/Device_file#Naming_conventions "wikipedia:Device file")). За да ги видите използвайте [lsblk](/index.php/Lsblk "Lsblk") или *fdisk*.

```
# fdisk -l

```

Резултати завършващи на `rom`, `loop` или `airoot` могат да бъдат игнорирани.

Следните *дялове* са **необходими** за избраното устройство:

*   Един дял за root директорията `/`.
*   Ако [UEFI](/index.php/UEFI "UEFI") е включено, и [системен дял](/index.php/EFI_system_partition "EFI system partition").

**Note:** [Swap](/index.php/Swap "Swap") може да бъде отделен дял или [файл](/index.php/Swap_file "Swap file").

За да промените *таблицата на дяловете*, използвайте [fdisk](/index.php/Fdisk "Fdisk") или [parted](/index.php/Parted "Parted").

```
# fdisk /dev/*sda*

```

Вижте [Partitioning](/index.php/Partitioning "Partitioning") за повече информация.

**Note:** Ако искате да създадете устройство за [LVM](/index.php/LVM "LVM"), [disk encryption](/index.php/Disk_encryption "Disk encryption") или [RAID](/index.php/RAID "RAID"), направете това сега.

### Форматиране на дяловете

Щом дяловете са създадени, всеки трябва да бъде форматиран в съответната [файлова система](/index.php/File_system "File system"). Например, за да форматирате дяла root на `/dev/*sda1*` с `*ext4*`, използвайте:

```
# mkfs.*ext4* /dev/*sda1*

```

Ако създадохте дял за swap (например `/dev/*sda3*`), включете го с *mkswap*:

```
# mkswap /dev/*sda3*
# swapon /dev/*sda3*

```

Вижте [Създаване на файлова система](/index.php/File_systems#Create_a_file_system "File systems") за детайли.

### Включване на файловите системи

[Включете](/index.php/Mount "Mount") файловата система на дяла root към `/mnt`, например:

```
# mount /dev/*sda1* /mnt

```

Създайте точки на качване за други дялове и ги включете подобаващо:

```
# mkdir /mnt/*boot*
# mount /dev/*sda2* /mnt/*boot*

```

[genfstab](https://git.archlinux.org/arch-install-scripts.git/tree/genfstab.in) ще открие качени файлови системи и суап място.

## Инсталиране

### Избиране на източник

Исталационните пакети трябва да бъдат изтеглени от [mirror сървъри](/index.php/Mirrors "Mirrors"), които са описани в `/etc/pacman.d/mirrorlist`. На “живата“ система, всички източници са включени и подредени по скорост и времето необходимо за синхронизирането им, когато е бил създаден инсталационният образ.

Колкото по-високо в списъка е източник, толкова по-скоро ще бъде използван при сваляне на пакет. Вероятно бихте искали да редактирате файла, като преместите географски по-близките източници най-горе в списъка, въпреки че и други фактори могат да повлият.

По-късно този файл ще бъде копиран от *pacstrap*, затова е добре да ги подредите правилно.

### Инсталиране на основни пакети

Използвайте скрипта [pacstrap](https://projects.archlinux.org/arch-install-scripts.git/tree/pacstrap.in) за да инсталирате групата [base](https://www.archlinux.org/groups/x86_64/base/) пакети:

```
# pacstrap /mnt base

```

Тази група не включва всичко налично на “живата“ инсталация, като [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs) или определени безжични фърмуеари; вижте [включените пакети](https://projects.archlinux.org/archiso.git/tree/configs/releng/packages.x86_64) за сравнение.

За да [инсталирате](/index.php/Install "Install") пакети и други групи като [base-devel](https://www.archlinux.org/groups/x86_64/base-devel/), добавете имената им след *pacstrap* (разделени с интервал) или с индивидуални [pacman](/index.php/Pacman "Pacman") команди след стъпката [#Chroot](#Chroot).

## Настройване на системата

### Fstab

Генерирайте [fstab](/index.php/Fstab "Fstab") файл (използвайте `-U` или `-L` за [UUID](/index.php/UUID "UUID") или надпис):

```
# genfstab -U /mnt >> /mnt/etc/fstab

```

След това проверете съдържанието на изходящия файл в `/mnt/etc/fstab` и редактирайте в случай на грешка.

### Chroot

[Change root](/index.php/Change_root "Change root") в новата система:

```
# arch-chroot /mnt

```

### Времева зона

Настройте [времевата зона](/index.php/Time_zone "Time zone") с:

```
# ln -sf /usr/share/zoneinfo/*Region*/*City* /etc/localtime

```

Използвайте [hwclock(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hwclock.8) за да създадете `/etc/adjtime`:

```
# hwclock --systohc

```

Тази команда очаква часовника на устройството да бъде [UTC](https://en.wikipedia.org/wiki/UTC "wikipedia:UTC"). Вижте [System time#Time standard](/index.php/System_time#Time_standard "System time") за детайли.

### Локализиране

Махнете `#` пред `en_US.UTF-8 UTF-8`, както и от други нужни [локализации](/index.php/Localization "Localization") в `/etc/locale.gen` и ги създайте с командата:

```
# locale-gen

```

Настройте [променливата](/index.php/Variable "Variable") `LANG` в [locale.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/locale.conf.5), например:

 `/etc/locale.conf`  `LANG=*en_US.UTF-8*` 

Ако сте променили подредбата на [конзолната клавиатура](#Изберете_клавиатурна_подредба), може да направите промените постоянни във [vconsole.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/vconsole.conf.5):

 `/etc/vconsole.conf`  `KEYMAP=*de-latin1*` 

### Настройване на мрежи

Създайте [hostname](/index.php/Hostname "Hostname") файла:

 `/etc/hostname` 
```
*моето-хост-име*

```

Добавете го и в [hosts(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/hosts.5) файла:

 `/etc/hosts` 
```
127.0.0.1	localhost
::1		localhost
127.0.1.1	*моето-хост-име*.localdomain	*моето-хост-име*

```

Ако системата е с постоянен IP адрес, то той трябва да бъде използван вместо `127.0.1.1`.

Завършете [мрежовото настройване](/index.php/Network_configuration "Network configuration") на току що инсталираната среда.

### Initramfs

Съдаването на нов *initramfs* обикновено не е необходимо, защото [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio") е бил задействан от инсталирането на пакета [linux](https://www.archlinux.org/packages/?name=linux) при извършването на *pacstrap* скрипта.

При специални случай, променете [mkinitcpio.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/mkinitcpio.conf.5) файла и създайте initramfs образ с командата:

```
# mkinitcpio -p linux

```

### Root парола

Създайте root [парола](/index.php/Password "Password") с:

```
# passwd

```

### Boot loader

Linux-съвместим boot loader трябва да бъде инталиран за да включите Arch Linux. Вижте [Arch boot process#Boot loader](/index.php/Arch_boot_process#Boot_loader "Arch boot process") за да изберете някой от предоставените.

Ако разполагате с Intel или AMD процесор, включете [microcode](/index.php/Microcode "Microcode") обновления.

## Рестартиране

Напуснете chroot средата като напишете `exit` или като натиснете `Ctrl+D`.

Също така може да изключите всички дялове с `umount -R /mnt`: това позволява да забележите "заети" дялове, ако има такива и да намерите причината за това с командата [fuser(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/fuser.1).

Накрая рестартирайте машината като напишете `reboot`: всеки все още включен дял ще бъде автоматично изключен от *systemd*. Не забравяйте да извадите инсталационния носител, след което се впишете в новата система с root потребителя.

## След инсталиране

Вижте [основни препоръки](/index.php/General_recommendations "General recommendations") за насоки в поддръжка и след инсталационни ръководства (като включване на графична среда, звук или тъчпад).

За списък с програми, които биха ви заинтересовали, вижте [List of applications](/index.php/List_of_applications "List of applications").