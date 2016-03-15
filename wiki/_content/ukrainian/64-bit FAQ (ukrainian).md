Нижче наведений список запитання що часто задаються про Arch Linux на x86_64 сумісних процесорах.

## Contents

*   [1 Як мені визначити чи мій процесор сумісний з x86_64?](#.D0.AF.D0.BA_.D0.BC.D0.B5.D0.BD.D1.96_.D0.B2.D0.B8.D0.B7.D0.BD.D0.B0.D1.87.D0.B8.D1.82.D0.B8_.D1.87.D0.B8_.D0.BC.D1.96.D0.B9_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D0.BE.D1.80_.D1.81.D1.83.D0.BC.D1.96.D1.81.D0.BD.D0.B8.D0.B9_.D0.B7_x86_64.3F)
    *   [1.1 Користувачі GNU/Linux](#.D0.9A.D0.BE.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.B2.D0.B0.D1.87.D1.96_GNU.2FLinux)
    *   [1.2 Користувачі Windows](#.D0.9A.D0.BE.D1.80.D0.B8.D1.81.D1.82.D1.83.D0.B2.D0.B0.D1.87.D1.96_Windows)
*   [2 Яку версію Arch мені слід використовувати, 32 чи 64?](#.D0.AF.D0.BA.D1.83_.D0.B2.D0.B5.D1.80.D1.81.D1.96.D1.8E_Arch_.D0.BC.D0.B5.D0.BD.D1.96_.D1.81.D0.BB.D1.96.D0.B4_.D0.B2.D0.B8.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D1.82.D0.BE.D0.B2.D1.83.D0.B2.D0.B0.D1.82.D0.B8.2C_32_.D1.87.D0.B8_64.3F)
*   [3 Як я можу встановити Arch64?](#.D0.AF.D0.BA_.D1.8F_.D0.BC.D0.BE.D0.B6.D1.83_.D0.B2.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D0.B8_Arch64.3F)
*   [4 Наскільки повноцінний порт?](#.D0.9D.D0.B0.D1.81.D0.BA.D1.96.D0.BB.D1.8C.D0.BA.D0.B8_.D0.BF.D0.BE.D0.B2.D0.BD.D0.BE.D1.86.D1.96.D0.BD.D0.BD.D0.B8.D0.B9_.D0.BF.D0.BE.D1.80.D1.82.3F)
*   [5 Чи будуть доступними всі пакети до яких я звик з мого 32-бітного Arch'у?](#.D0.A7.D0.B8_.D0.B1.D1.83.D0.B4.D1.83.D1.82.D1.8C_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.BD.D0.B8.D0.BC.D0.B8_.D0.B2.D1.81.D1.96_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B8_.D0.B4.D0.BE_.D1.8F.D0.BA.D0.B8.D1.85_.D1.8F_.D0.B7.D0.B2.D0.B8.D0.BA_.D0.B7_.D0.BC.D0.BE.D0.B3.D0.BE_32-.D0.B1.D1.96.D1.82.D0.BD.D0.BE.D0.B3.D0.BE_Arch.27.D1.83.3F)
*   [6 Чому 64-bit?](#.D0.A7.D0.BE.D0.BC.D1.83_64-bit.3F)
*   [7 Як я можу повідомити про баги?](#.D0.AF.D0.BA_.D1.8F_.D0.BC.D0.BE.D0.B6.D1.83_.D0.BF.D0.BE.D0.B2.D1.96.D0.B4.D0.BE.D0.BC.D0.B8.D1.82.D0.B8_.D0.BF.D1.80.D0.BE_.D0.B1.D0.B0.D0.B3.D0.B8.3F)
*   [8 Які репозиторії повинен використовувати pacman?](#.D0.AF.D0.BA.D1.96_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D1.96.D1.97_.D0.BF.D0.BE.D0.B2.D0.B8.D0.BD.D0.B5.D0.BD_.D0.B2.D0.B8.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D1.82.D0.BE.D0.B2.D1.83.D0.B2.D0.B0.D1.82.D0.B8_pacman.3F)
*   [9 Як змінити існуючі PKGBUILDи для використанні в Arch64?](#.D0.AF.D0.BA_.D0.B7.D0.BC.D1.96.D0.BD.D0.B8.D1.82.D0.B8_.D1.96.D1.81.D0.BD.D1.83.D1.8E.D1.87.D1.96_PKGBUILD.D0.B8_.D0.B4.D0.BB.D1.8F_.D0.B2.D0.B8.D0.BA.D0.BE.D1.80.D0.B8.D1.81.D1.82.D0.B0.D0.BD.D0.BD.D1.96_.D0.B2_Arch64.3F)
*   [10 Чого мені не вистачатиме у Arch64?](#.D0.A7.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D1.96_.D0.BD.D0.B5_.D0.B2.D0.B8.D1.81.D1.82.D0.B0.D1.87.D0.B0.D1.82.D0.B8.D0.BC.D0.B5_.D1.83_Arch64.3F)
*   [11 Чи зможу я запустити 32-бітні програми на Arch64?](#.D0.A7.D0.B8_.D0.B7.D0.BC.D0.BE.D0.B6.D1.83_.D1.8F_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D1.82.D0.B8.D1.82.D0.B8_32-.D0.B1.D1.96.D1.82.D0.BD.D1.96_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.B8_.D0.BD.D0.B0_Arch64.3F)
*   [12 Чи можна зібрати 32-бітні пакети для i686 в Arch64?](#.D0.A7.D0.B8_.D0.BC.D0.BE.D0.B6.D0.BD.D0.B0_.D0.B7.D1.96.D0.B1.D1.80.D0.B0.D1.82.D0.B8_32-.D0.B1.D1.96.D1.82.D0.BD.D1.96_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B8_.D0.B4.D0.BB.D1.8F_i686_.D0.B2_Arch64.3F)
    *   [12.1 Репозиторій multilib - Multilib_Project](#.D0.A0.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D1.96.D0.B9_multilib_-_Multilib_Project)
*   [13 Чи можу я оновити/змінити мою систему з i686 на x86_64 без перевстановлення?](#.D0.A7.D0.B8_.D0.BC.D0.BE.D0.B6.D1.83_.D1.8F_.D0.BE.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D0.B8.2F.D0.B7.D0.BC.D1.96.D0.BD.D0.B8.D1.82.D0.B8_.D0.BC.D0.BE.D1.8E_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83_.D0.B7_i686_.D0.BD.D0.B0_x86_64_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.B5.D1.80.D0.B5.D0.B2.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8F.3F)

## Як мені визначити чи мій процесор сумісний з x86_64?

### Користувачі GNU/Linux

Виконати наступну команду:

```
$ less /proc/cpuinfo

```

Шукати значення `flags`. Якщо присутній `lm` - значить твій процесор x86_64-сумісний.

Або можна просто виконати цю команду:

```
$ grep -q "^flags.*\blm\b" /proc/cpuinfo && echo "x86_64" || echo "not x86_64"

```

### Користувачі Windows

Використавши безкоштовну програму [CPU-Z](http://www.cpuid.com/cpuz.php) можна визначити чи твій процесор x86_64 сумісний. Центральні процесори AMD з позначкою "AMD64" або процесори Intel з "EM64T" повинні бути сумісними з x86_64 випусками і бінарними пакетами.

## Яку версію Arch мені слід використовувати, 32 чи 64?

Якщо твій процесор [x86_64](https://en.wikipedia.org/wiki/X86-64 "wikipedia:X86-64")-сумісний, слід використовувати Arch64.

## Як я можу встановити Arch64?

Просто використай наші [офіційні інсталяційні образи дисків](https://www.archlinux.org/download/).

## Наскільки повноцінний порт?

Порт готовий для щоденного використання на домашніх або серверних комп'ютерах.

## Чи будуть доступними всі пакети до яких я звик з мого 32-бітного Arch'у?

Репозиторії повністю портовані і все повинно працювати як очікується.

Рідко зустрічаються старі пакунки з [AUR](/index.php/Arch_User_Repository "Arch User Repository") які описані тільки як `'i686'`, але зазвичай вони працюють і для 64-бітних систем також. Просто спробуй додати `'x86_64'`.

## Чому 64-bit?

У більшості випадків він швидший і по суті безпечніший завдяки природі [Address space layout randomization (ASLR)](https://en.wikipedia.org/wiki/Address_space_layout_randomization "wikipedia:Address space layout randomization") в комбінації з [Position-independent code (PIC)](https://en.wikipedia.org/wiki/Position-independent_code "wikipedia:Position-independent code") і [NX Bit](https://en.wikipedia.org/wiki/NX_Bit "wikipedia:NX Bit") які не є доступними в ядрі i686 через відключене PAE. Якщо твій комп'ютер має 4 ГБ або більше оперативної пам'яті, рекомендується використовувати 64-бітний випуск оскільки 32-бітні операційні системи не можуть розпізнати будь-яку додаткову оперативну пам'ять. Більше деталей можна дізнатись у наших [звітах відмінностей](https://www.archlinux.org/packages/differences/). Це список в якому наведено порівняння версій 32-/64-бітних пакетів.

## Як я можу повідомити про баги?

Просто використовуй [Flyspray](https://bugs.archlinux.org/) але вибирай x86_64 в полі "Architecture" якщо ти думає що ця проблема має відношення до портування.

## Які репозиторії повинен використовувати pacman?

Всі репозиторії підтримуються портом.

## Як змінити існуючі PKGBUILDи для використанні в Arch64?

Додати наступну змінну до всіх портованих пакетів:

```
arch=('i686' 'x86_64') 

```

Внести зміни прямо у секції що відповідають за вихідний код і md5-суми і використати інший вихідний код:

```
[ "$CARCH" = "x86_64" ] && source=(${source[@]} 'other source')
[ "$CARCH" = "x86_64" ] && md5sums=(${md5sums[@]} 'other md5sum')

```

Для невеликих змін внеси в секцію build:

```
[ "$CARCH" = "x86_64" ] && (patch -Np0 -i ../foo_x86_64.patch)

```

Або коли потрібно більше змін:

```
if [ "$CARCH" = "x86_64" ]; then
    configure/patch/sed      # for x86_64
  else configure/patch/sed   # for i686
fi

```

## Чого мені не вистачатиме у Arch64?

Нічого, справді. Практично всі програми зараз підтримують 64-bit або перебувають у стадії розробки сумісності з 64-bit.

Найбільшою проблемою є або пакети з закритим вихідним кодом або які мають x86-специфічну структуру, яка надто громіздка для портування на 64-bit (типово для емуляторів).

Ці програми раніше були проблематичними, проте зараз доступні в [AUR](/index.php/Arch_User_Repository "Arch User Repository") і чудово працюють:

*   Acrobat Reader не має 64-бітної версії, але можна запустити 32-бітну в режимі сумісності. Також існує багато альтернативних програм з відкритим вихідним кодом для перегляду pdf-файлів.

Все інше повинно працювати цілком нормально. Якщо бракує якогось Arch32-пакету в нашому порті і тобі відомо що він компілюється на x86_64 (наприклад ти знайшов цей пакет у іншому 64-bit дистрибутиві), просто зв'яжись з розробниками або зроби запит про новий пакет на форумах.

## Чи зможу я запустити 32-бітні програми на Arch64?

Так!

*   Можна встановити `lib32-*` бібліотеки з [multilib] репозиторію. Щоб використовувати цей репозиторій, потрібно додати наступні рядки до `/etc/pacman.conf`:

```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

Зараз (Грудень 2011), [multilib] включає Wine і Skype. Крім того, там знаходиться мультибібліотечний компілятор gcc-multilib.

*   Або можна створити інший chroot з 32-бітною системою (детальніше в [Arch64 Install bundled 32bit system](/index.php/Arch64_Install_bundled_32bit_system "Arch64 Install bundled 32bit system")):

Завантажитись в Arch64, запустити Xorg(команда startx), відкрити термінал.

```
$ xhost +local:
$ su
# mount /dev/sda1 /mnt/arch32
# mount --bind /proc /mnt/arch32/proc
# chroot /mnt/arch32
# su ім'я_32_бітного_користувача
$ /usr/bin/command-you want # or eg: /opt/mozilla/bin/firefox

```

Деякі 32-бітні програми (наприклад OpenOffice) можуть вимагати додаткових звязків. Наступні рядки потрібно додати в `/etc/rc.local` щоб забезпечити все що потрібно 32-бітним програмам (припускається що `/mnt/arch32` монтується в `/etc/fstab`):

```
mount --bind /dev /mnt/arch32/dev
mount --bind /dev/pts /mnt/arch32/dev/pts
mount --bind /dev/shm /mnt/arch32/dev/shm
mount --bind /proc /mnt/arch32/proc
mount --bind /proc/bus/usb /mnt/arch32/proc/bus/usb
mount --bind /sys /mnt/arch32/sys
mount --bind /tmp /mnt/arch32/tmp
#закоментувати наступний рядок якщо не використовується спільний домашній каталог
mount --bind /home /mnt/arch32/home

```

Потім можна набрати в терміналі:

```
$ xhost +localhost
$ sudo chroot /mnt/arch32 su ім'я_32_бітного_користувача /opt/openoffice/program/soffice

```

## Чи можна зібрати 32-бітні пакети для i686 в Arch64?

Так. Можна використати:

*   multilib-верісії відповідних пакунків з репозиторію [multilib] або
*   i686 chroot.

### Репозиторій multilib - [Multilib_Project](/index.php/Multilib_Project "Multilib Project")

Щоб використовувати [multilib] репозиторій, потрібно внести зміни в `/etc/pacman.conf` і розкоментувати наступні рядки:

```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist

```

оновити систему `pacman -Syu` і встановити пакет [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib).

**Note:** Якщо система має встановлену групу пакунків `base-devel`, користувачі повинні замінити версії з [extra] на версії [mutlilib] як показано нижче.

**Note:** [gcc-multilib](https://www.archlinux.org/packages/?name=gcc-multilib) може збирати 64-бітний і 32-бітний вихідний код. Можна безпечно встановити `multilib-devel` щоб замінити пакети показані нижче, проте `base-devel` потрібен через ініші пакети які в нього включені. Дивись [https://bbs.archlinux.org/viewtopic.php?id=102828](https://bbs.archlinux.org/viewtopic.php?id=102828) для більш детальної інформації.

```
# pacman -S gcc-multilib
resolving dependencies...
warning: dependency cycle detected:
warning: lib32-gcc-libs will be installed before its gcc-libs-multilib dependency
looking for inter-conflicts...
:: gcc-libs-multilib and gcc-libs are in conflict. Remove gcc-libs? [y/N] y
:: binutils-multilib and binutils are in conflict. Remove binutils? [y/N] y
:: gcc-multilib and gcc are in conflict. Remove gcc? [y/N] y
:: libtool-multilib and libtool are in conflict. Remove libtool? [y/N] y

Remove (4): gcc-libs-4.6.1-1  binutils-2.21.1-1  gcc-4.6.1-1  libtool-2.4-4

Total Removed Size:   87.65 MB

Targets (7): lib32-glibc-2.14-4  lib32-gcc-libs-4.6.1-1  gcc-libs-multilib-4.6.1-1  binutils-multilib-2.21.1-1
             gcc-multilib-4.6.1-1  lib32-libtool-2.4-2  libtool-multilib-2.4-2

Total Download Size:    25.04 MB
Total Installed Size:   108.27 MB

Proceed with installation? [Y/n]

```

Компіляція пакетів на x86_64 для i686 вимагає лише заміни наступних значень у файлі (наприклад `~/.makepkg.i686.conf`)

```
CARCH="i686"
CHOST="i686-pc-linux-gnu"
CFLAGS="-m32 -march=i686 -mtune=generic -O2 -pipe -fstack-protector --param=ssp-buffer-size=4 -D_FORTIFY_SOURCE=2"
CXXFLAGS="${CFLAGS}"

```

і виклику makepkg наступною командою:

```
$ linux32 makepkg -src --config ~/.makepkg.i686.conf

```

## Чи можу я оновити/змінити мою систему з i686 на x86_64 без перевстановлення?

Так. Існує стаття на [форумі](https://bbs.archlinux.org/viewtopic.php?id=64485) в якій покроково описується процес необхідний для успішної міграції встановленої 32-бітної системи на 64-бітну без втрати конфігураційних файлів/налаштувань/інформації. Зауважте: Великий зовнішній жорсткий диск був використаний для перенесення.

Однак, можна запустити Arch64 з інсталяційного диску, змонтувати диск, зберегти все що необхідно і не є 32-бітним бінарним пакетом (наприклад: `/home` & `/etc`), і встановити систему.

Також може знадобитись [Migrating Between Architectures Without Reinstalling](/index.php/Migrating_Between_Architectures_Without_Reinstalling "Migrating Between Architectures Without Reinstalling").