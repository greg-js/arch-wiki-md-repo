Ця стаття описує процес встановлення і налаштування [Arch Linux](/index.php/Arch_Linux "Arch Linux") за допомогою [Arch Install Scripts](https://github.com/falconindy/arch-install-scripts). Перед встановленням, рекомендується переглянути [FAQ](/index.php/FAQ "FAQ"). Команда підтримки [Arch Wiki](/index.php/Main_page "Main page") є відмінним ресурсом і шукайте допомогу з усіх питань першочергово тут. [IRC](https://en.wikipedia.org/wiki/IRC "wikipedia:IRC")-канал ([irc://irc.freenode.net/#archlinux](irc://irc.freenode.net/#archlinux)), та [форум](https://bbs.archlinux.org/) також доступні, якщо відповідь не може бути знайдена в іншому місці. Крім того, переконайтеся, що немає відповіді на ваше питання на `man`-сторінках для будь-якої команди; які можна викликати `man *command*`.

## Contents

*   [1 Завантаження](#.D0.97.D0.B0.D0.B2.D0.B0.D0.BD.D1.82.D0.B0.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F)
*   [2 Встановлення](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F)
    *   [2.1 Розкладка клавіатури](#.D0.A0.D0.BE.D0.B7.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D1.96.D0.B0.D1.82.D1.83.D1.80.D0.B8)
    *   [2.2 Створення розділів](#.D0.A1.D1.82.D0.B2.D0.BE.D1.80.D0.B5.D0.BD.D0.BD.D1.8F_.D1.80.D0.BE.D0.B7.D0.B4.D1.96.D0.BB.D1.96.D0.B2)
    *   [2.3 Форматування розділів](#.D0.A4.D0.BE.D1.80.D0.BC.D0.B0.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.80.D0.BE.D0.B7.D0.B4.D1.96.D0.BB.D1.96.D0.B2)
    *   [2.4 Монтування розділів](#.D0.9C.D0.BE.D0.BD.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.80.D0.BE.D0.B7.D0.B4.D1.96.D0.BB.D1.96.D0.B2)
    *   [2.5 Підключення до мережі Інтернет](#.D0.9F.D1.96.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.BD.D1.8F_.D0.B4.D0.BE_.D0.BC.D0.B5.D1.80.D0.B5.D0.B6.D1.96_.D0.86.D0.BD.D1.82.D0.B5.D1.80.D0.BD.D0.B5.D1.82)
*   [3 Бездротове з'єднання =](#.D0.91.D0.B5.D0.B7.D0.B4.D1.80.D0.BE.D1.82.D0.BE.D0.B2.D0.B5_.D0.B7.27.D1.94.D0.B4.D0.BD.D0.B0.D0.BD.D0.BD.D1.8F_.3D)
    *   [3.1 Встановлення базової системи](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D0.BE.D1.97_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B8)
    *   [3.2 Встановлення завантажувача](#.D0.92.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.B7.D0.B0.D0.B2.D0.B0.D0.BD.D1.82.D0.B0.D0.B6.D1.83.D0.B2.D0.B0.D1.87.D0.B0)
        *   [3.2.1 GRUB](#GRUB)
        *   [3.2.2 Syslinux](#Syslinux)
    *   [3.3 Налаштування системи](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B8)
    *   [3.4 Розмонтування розділів та перезавантаження](#.D0.A0.D0.BE.D0.B7.D0.BC.D0.BE.D0.BD.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.80.D0.BE.D0.B7.D0.B4.D1.96.D0.BB.D1.96.D0.B2_.D1.82.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.B7.D0.B0.D0.B2.D0.B0.D0.BD.D1.82.D0.B0.D0.B6.D0.B5.D0.BD.D0.BD.D1.8F)
*   [4 Дії після встановлення базової системи](#.D0.94.D1.96.D1.97_.D0.BF.D1.96.D1.81.D0.BB.D1.8F_.D0.B2.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D0.BE.D1.97_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B8)
    *   [4.1 Керування користувачами](#.D0.9A.D0.B5.D1.80.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.B2.D0.B0.D1.87.D0.B0.D0.BC.D0.B8)
    *   [4.2 Керування пакунками](#.D0.9A.D0.B5.D1.80.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D0.BF.D0.B0.D0.BA.D1.83.D0.BD.D0.BA.D0.B0.D0.BC.D0.B8)
    *   [4.3 Керування службами](#.D0.9A.D0.B5.D1.80.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.D0.B0.D0.BC.D0.B8)
    *   [4.4 Звук](#.D0.97.D0.B2.D1.83.D0.BA)
    *   [4.5 Відео-драйвер](#.D0.92.D1.96.D0.B4.D0.B5.D0.BE-.D0.B4.D1.80.D0.B0.D0.B9.D0.B2.D0.B5.D1.80)
    *   [4.6 Графічний сервер](#.D0.93.D1.80.D0.B0.D1.84.D1.96.D1.87.D0.BD.D0.B8.D0.B9_.D1.81.D0.B5.D1.80.D0.B2.D0.B5.D1.80)
    *   [4.7 Шрифти](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D0.B8)
*   [5 Додатково](#.D0.94.D0.BE.D0.B4.D0.B0.D1.82.D0.BA.D0.BE.D0.B2.D0.BE)

## Завантаження

Завантажити новий iso-образ Arch Linux можна зі [сторінки завантаження Arch Linux](https://www.archlinux.org/download/).

*   В один iso-образ включені i686 і x86_64 живі системи для установки Arch Linux по мережі. Середовища, що містять [core] репозиторій більше не надаються.
*   Образи встановлення підписані і настійно рекомендуємо перевірити свої підписи перед використанням. В Arch Linux, це можна зробити за допомогою `pacman-key -v <iso-file>.sig` 
*   Образ може бути записаний на компакт-диск, змонтований у вигляді файлу ISO, або на USB флеш-накопичувач за допомогою утиліти `dd`. Даний iso-образ призначений тільки для нових встановлень, в існуючих системах Arch Linux завжди можна оновитись за допомогою `pacman -Syu`.

## Встановлення

### Розкладка клавіатури

Для більшості країн і видів клавіатур вже доступні відповідні розкладки, яка може бути обрана командою `loadkeys uk`. Інші розкладки можна знайти в `/usr/share/kbd/keymaps/` (ви повинні ввести повний шлях і розширення файлу при використанні loadkeys).

### Створення розділів

Докладніше дивись [partitioning](/index.php/Partitioning "Partitioning").

При потребі не забудьте створити [LVM](/index.php/LVM "LVM"), [LUKS](/index.php/LUKS "LUKS"), чи [RAID](/index.php/RAID "RAID") пристрої.

### Форматування розділів

Докладніше дивись [File Systems](/index.php/File_systems#Step_2:_create_the_new_file_system "File systems").

Якщо ви використовуєте (U)EFI, вам, швидше за все, потрібен ще один розділ для розміщення розділів UEFI системи.

Читай [Create an UEFI System Partition in Linux](/index.php/Unified_Extensible_Firmware_Interface#Create_an_UEFI_System_Partition_in_Linux "Unified Extensible Firmware Interface").

### Монтування розділів

Тепер ми повинні змонтувати кореневий розділ в {ic|/mnt}}.

```
# mount /dev/sda2 /mnt

```

Якщо ви хочете створити будь-які інші розділи, які будуть автоматично монтуватись скриптом `genfstab`, треба створити теки та змонтувати їх, наприклад для розділів `/boot`, `/home`

```
# mkdir /mnt/boot && mount /dev/sda1 /mnt/boot
# mkdir /mnt/home && mount /dev/sda3 /mnt/home

```

### Підключення до мережі Інтернет

Служба DHCP вже включена для всіх доступних пристроїв. Якщо вам необхідно встановити статичний IP або використовувати інструменти управління, такі як [Netcfg](/index.php/Netcfg#Configuration "Netcfg"), ви повинні зупинити цю службу: `systemctl stop dhcpcd.service`. Для додаткової інформації дивіться розділ [configuring network](/index.php/Configuring_network "Configuring network").

## Бездротове з'єднання =

Виконайте `wifi-menu` для налаштування вашої бездротової мережи. Докладніше дивись [Wireless network configuration](/index.php/Wireless_network_configuration "Wireless network configuration") та [Netcfg](/index.php/Netcfg#Configuration "Netcfg").

### Встановлення базової системи

Перед початком встановлення, ви, можливо, захочете відредагувати `/etc/pacman.d/mirrorlist` для вибору відповідного дзеркала.

Для України рекомендуються наступні дзеркала в UA-IX:

```
# Server = [http://ftp.linux.kiev.ua/pub/Linux/ArchLinux/$repo/os/$arch](http://ftp.linux.kiev.ua/pub/Linux/ArchLinux/$repo/os/$arch)
# Server = [http://mirrors.mithril.org.ua/linux/archlinux/$repo/os/$arch](http://mirrors.mithril.org.ua/linux/archlinux/$repo/os/$arch)

```

Копія файлу буде також встановлена в вашу систему за допомогою `pacstrap`.

Скрипт [pacstrap](https://github.com/falconindy/arch-install-scripts/blob/master/pacstrap.in) встановить базову систему. Група пакунків *base-devel* також повинна бути встановлена, якщо ви плануєте компілювати програми з [AUR](/index.php/AUR "AUR") або [ABS](/index.php/ABS "ABS").

```
# pacstrap /mnt base base-devel

```

Також можна встановити і інші пакунки, додавши їх назви, розділені пробілами, до команди вище.

### Встановлення завантажувача

#### [GRUB](/index.php/GRUB "GRUB")

*   Для BIOS

```
# arch-chroot /mnt pacman -S grub-bios

```

*   Для EFI (в рідкісних випадках вам буде потрібно `grub-efi-i386` замість `grub-efi-x86_64`)

```
# arch-chroot /mnt pacman -S grub-efi-x86_64

```

*   Встановити GRUB після chroot'інга (див. розділ [Налаштування системи](#.D0.9D.D0.B0.D0.BB.D0.B0.D1.88.D1.82.D1.83.D0.B2.D0.B0.D0.BD.D0.BD.D1.8F_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.B8)).

#### [Syslinux](/index.php/Syslinux "Syslinux")

```
# arch-chroot /mnt pacman -S syslinux

```

### Налаштування системи

Створіть [fstab](/index.php/Fstab "Fstab") наступною командою. (Якщо ви хочете використовувати UUID або мітки, використовуйте опції `-U` і `-L` відповідно.)

```
# genfstab -p /mnt >> /mnt/etc/fstab

```

Далі перейдіть в свою встановлену систему за допомогою [chroot](/index.php/Chroot "Chroot").

```
# arch-chroot /mnt

```

*   Вкажіть ім'я хоста у файлі `/etc/hostname`.
*   Створіть посилання `/etc/localtime` на `/usr/share/zoneinfo/Zone/SubZone`. Де `Zone` і `Subzone` змініть на ваш часовий пояс. Наприклад

```
# ln -s /usr/share/zoneinfo/Europe/Kiev /etc/localtime

```

*   Також можливо ви захочете налаштувати [locale](/index.php/Locale#Setting_the_system_locale "Locale") в `/etc/locale.conf`.
*   Налаштуйте [розкладку консолі та шрифти](/index.php/KEYMAP "KEYMAP") в `/etc/vconsole.conf`
*   Розкоментуйте(приберіть знак 'гратки', що стоїть на початку рядка) потрібні рядки [locales](/index.php/Locale "Locale") в `/etc/locale.gen` і згенеруйте `locale-gen`.
*   Налаштуйте `/etc/mkinitcpio.conf` для ваших потреб (читай [mkinitcpio](/index.php/Mkinitcpio "Mkinitcpio")) і створіть ramdisk:

```
# mkinitcpio -p linux

```

*   Налаштування завантажувача: звернутися до відповідної статті в розділі установки завантажувача.
*   Встановіть root пароль `passwd`.

### Розмонтування розділів та перезавантаження

Якщо ви все ще в chroot оточенні введіть `exit` або натисніть `Ctrl+D`. Ми змонтували розділи в `/mnt`. Тепер розмонтуємо їх.

```
# umount /mnt/{boot,home,}

```

Тепер перезавантажтеся і увійдіть в нову систему з облікового запису root.

## Дії після встановлення базової системи

### Керування користувачами

Обов'язково створіть, щонайменше, одного користувача, як описано в [User management](/index.php/Users_and_groups#User_management "Users and groups"). Це погана практика використання облікового запису суперкористувача(root) для постійної роботи, і не використовуйте його через [SSH](/index.php/SSH "SSH") на сервері. Обліковий запис суперкористувача повинен використовуватися тільки для адміністративних завдань.

### Керування пакунками

Читайте [pacman](/index.php/Pacman_(%D0%A3%D0%BA%D1%80%D0%B0%D1%97%D0%BD%D1%81%D1%8C%D0%BA%D0%B0) "Pacman (Українська)") та [FAQ#Package management](/index.php/FAQ#Package_management "FAQ") для отримання інформації про встановлення, оновлення та керування пакунками.

### Керування службами

Arch Linux використовує [systemd](/index.php/Systemd "Systemd") як систему ініціалізації та менеджер служб для Linux. Для кращого розуміння Arch Linux, було б непогано навчитися основам [systemd](/index.php/Systemd "Systemd"). Взаємодія з systemd здійснюється через `systemctl` команди. Читайте [systemd#Basic systemctl usage](/index.php/Systemd#Basic_systemctl_usage "Systemd") для отримання докладнішої інформації.

### Звук

[ALSA](/index.php/ALSA "ALSA") як правило, працює 'з коробки'. Встановить [alsa-utils](https://www.archlinux.org/packages/?name=alsa-utils) (який містить `alsamixer`) і дотримуйтесь [цих](/index.php/Advanced_Linux_Sound_Architecture#Unmuting_the_channels "Advanced Linux Sound Architecture") інструкцій. ALSA включений в ядро і є рекомендованим. Якщо він не працює, [OSS](/index.php/OSS "OSS") є життєздатною альтернативою. Якщо у вас є підвищені вимоги до аудіо, подивіться [Sound system](/index.php/Sound_system "Sound system") для огляду різних статей.

### Відео-драйвер

Ядро Linux включає в себе відкриті відео-драйвера і підтримку апаратного прискорення кадровим буфером. Підтримка для OpenGL та 2D-прискорення в X11.

Якщо ви не знаєте, який відео-чипсет доступний на вашій машині, запустіть:

```
$ lspci | grep VGA

```

Для отримання повного списку відкритих відеодрайверів, шукайте у базі даних пакетів:

```
$ pacman -Ss xf86-video | less

```

Драйвер `vesa` генерує режим налаштування драйверів, який буде працювати практично зі всіма GPU, але не буде надавати 2D або 3D прискорення. Якщо кращий драйвер не може бути знайдений або не вдається завантажити, Xorg повернеться до vesa. Для його встановлення:

```
# pacman -S xf86-video-vesa

```

Щоб працювало прискорення відео у всіх режимах, оберіть відповідний драйвер відео:

| Brand | Type | Driver | [Multilib](/index.php/Multilib "Multilib") Package
(for 32-bit applications on Arch x86_64) | Documentation |
| **AMD/ATI** | Open source | [xf86-video-ati](https://www.archlinux.org/packages/?name=xf86-video-ati) | [lib32-ati-dri](https://www.archlinux.org/packages/?name=lib32-ati-dri) | [ATI](/index.php/ATI "ATI") |
| Proprietary | [catalyst-dkms](https://aur.archlinux.org/packages/catalyst-dkms/) | [lib32-catalyst-utils](https://aur.archlinux.org/packages/lib32-catalyst-utils/) | [AMD Catalyst](/index.php/AMD_Catalyst "AMD Catalyst") |
| **Intel** | Open source | [xf86-video-intel](https://www.archlinux.org/packages/?name=xf86-video-intel) | [lib32-intel-dri](https://www.archlinux.org/packages/?name=lib32-intel-dri) | [Intel graphics](/index.php/Intel_graphics "Intel graphics") |
| **Nvidia** | Open source | [xf86-video-nouveau](https://www.archlinux.org/packages/?name=xf86-video-nouveau) | [lib32-nouveau-dri](https://www.archlinux.org/packages/?name=lib32-nouveau-dri) | [Nouveau](/index.php/Nouveau "Nouveau") |
| [xf86-video-nv](https://aur.archlinux.org/packages/xf86-video-nv/) | – | (legacy driver) |
| Proprietary | [nvidia](https://www.archlinux.org/packages/?name=nvidia) | [lib32-nvidia-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-utils) | [NVIDIA](/index.php/NVIDIA "NVIDIA") |
| [nvidia-304xx](https://www.archlinux.org/packages/?name=nvidia-304xx) | [lib32-nvidia-304xx-utils](https://www.archlinux.org/packages/?name=lib32-nvidia-304xx-utils) |

### Графічний сервер

X Window System (X11, або X) є мережевим і графічним протоколом, який забезпечує роботу віконної системи на дисплеї. Це стандарт де-факто для побудови графічного інтерфейсу користувача. Докладніше - [Xorg](/index.php/Xorg "Xorg"). [Wayland](/index.php/Wayland "Wayland"), новий протокол графічного сервера з композитним менеджером Weston, доступний для використання. Дуже мало підтримується додатків на цій ранній стадії розвитку.

### Шрифти

Ви можете встановити набір TrueType шрифтів, бо тільки растрові шрифти включені за замовчуванням. DejaVu являє собою набір високої якості, загального призначення з хорошими шрифтами [Юнікоду](https://en.wikipedia.org/wiki/%D0%AE%D0%BD%D1%96%D0%BA%D0%BE%D0%B4 "wikipedia:Юнікод"):

```
# pacman -S ttf-dejavu

```

Зверніться до [Font configuration](/index.php/Font_configuration "Font configuration") за інформацією, як налаштувати рендерінг шрифтів і [Fonts](/index.php/Fonts "Fonts") за інструкціями по встановленню.

## Додатково

Список програм, які, можливо, вас зацікавлять, дивиться [List of applications](/index.php/List_of_applications "List of applications").

Читайте [General recommendations](/index.php/General_recommendations "General recommendations") для подальшої установки, підручники для створення сенсорної панелі або рендерінга шрифтів.