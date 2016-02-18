## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Установка mkinitcpio](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_mkinitcpio)
    *   [2.1 Из текущего репозитория](#.D0.98.D0.B7_.D1.82.D0.B5.D0.BA.D1.83.D1.89.D0.B5.D0.B3.D0.BE_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D1.8F)
    *   [2.2 Из git](#.D0.98.D0.B7_git)
*   [3 Создание загрузочного образа](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0)
*   [4 Редактирование файлов конфигурации](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [4.1 MODULES](#MODULES)
    *   [4.2 BINARIES and FILES](#BINARIES_and_FILES)
    *   [4.3 HOOKS](#HOOKS)
        *   [4.3.1 Build hooks](#Build_hooks)
        *   [4.3.2 Runtime hooks](#Runtime_hooks)
        *   [4.3.3 Доступные хуки](#.D0.94.D0.BE.D1.81.D1.82.D1.83.D0.BF.D0.BD.D1.8B.D0.B5_.D1.85.D1.83.D0.BA.D0.B8)
        *   [4.3.4 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
    *   [4.4 Изменение переменной MODULES](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE.D0.B9_MODULES)
    *   [4.5 Настройка BINARIES и FILES](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_BINARIES_.D0.B8_FILES)
*   [5 Создание образа](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0)
    *   [5.1 Пересоздание предопределенного образа / использование предустановок](#.D0.9F.D0.B5.D1.80.D0.B5.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B5.D0.B4.D0.BE.D0.BF.D1.80.D0.B5.D0.B4.D0.B5.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_.2F_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B5.D0.B4.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BE.D0.BA)
    *   [5.2 Вручную](#.D0.92.D1.80.D1.83.D1.87.D0.BD.D1.83.D1.8E)
        *   [5.2.1 Перегенерация fallback-образа](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B3.D0.B5.D0.BD.D0.B5.D1.80.D0.B0.D1.86.D0.B8.D1.8F_fallback-.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0)
*   [6 Изменения строки параметров ядра](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D1.8F.D0.B4.D1.80.D0.B0)
    *   [6.1 Вход в безотказный режим](#.D0.92.D1.85.D0.BE.D0.B4_.D0.B2_.D0.B1.D0.B5.D0.B7.D0.BE.D1.82.D0.BA.D0.B0.D0.B7.D0.BD.D1.8B.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC)
    *   [6.2 Запрет обработчиков](#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82_.D0.BE.D0.B1.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.87.D0.B8.D0.BA.D0.BE.D0.B2)
    *   [6.3 Запрет загрузки модулей](#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B8_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B5.D0.B9)
    *   [6.4 Использование raid](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_raid)
    *   [6.5 Использование net](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_net)
    *   [6.6 Использование lvm](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_lvm)
    *   [6.7 Использование шифрования на корневом разделе](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.88.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BD.D0.B0_.D0.BA.D0.BE.D1.80.D0.BD.D0.B5.D0.B2.D0.BE.D0.BC_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B5)
        *   [6.7.1 Использование LUKS томов](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_LUKS_.D1.82.D0.BE.D0.BC.D0.BE.D0.B2)
        *   [6.7.2 Использование legacy cryptsetup томов](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_legacy_cryptsetup_.D1.82.D0.BE.D0.BC.D0.BE.D0.B2)
        *   [6.7.3 Использование loop-aes томов](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_loop-aes_.D1.82.D0.BE.D0.BC.D0.BE.D0.B2)
*   [7 Использование спящего режима (на диск)](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81.D0.BF.D1.8F.D1.89.D0.B5.D0.B3.D0.BE_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B0_.28.D0.BD.D0.B0_.D0.B4.D0.B8.D1.81.D0.BA.29)
    *   [7.1 swsusp](#swsusp)
    *   [7.2 µswsusp](#.C2.B5swsusp)
    *   [7.3 suspend2](#suspend2)
    *   [7.4 Примеры конфигурационных файлов загрузчиков](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D1.8B.D1.85_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA.D0.BE.D0.B2)
        *   [7.4.1 GRUB](#GRUB)
        *   [7.4.2 LILO](#LILO)
*   [8 Возможные проблемы](#.D0.92.D0.BE.D0.B7.D0.BC.D0.BE.D0.B6.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B)
    *   [8.1 piix ide контролер и ядро beyond](#piix_ide_.D0.BA.D0.BE.D0.BD.D1.82.D1.80.D0.BE.D0.BB.D0.B5.D1.80_.D0.B8_.D1.8F.D0.B4.D1.80.D0.BE_beyond)
        *   [8.1.1 Проблема](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D0.B0)
        *   [8.1.2 Решение](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5)
*   [9 Я параноик!](#.D0.AF_.D0.BF.D0.B0.D1.80.D0.B0.D0.BD.D0.BE.D0.B8.D0.BA.21)
    *   [9.1 Предупреждение о cpio](#.D0.9F.D1.80.D0.B5.D0.B4.D1.83.D0.BF.D1.80.D0.B5.D0.B6.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE_cpio)
    *   [9.2 Использование bsdtar для извлечения](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_bsdtar_.D0.B4.D0.BB.D1.8F_.D0.B8.D0.B7.D0.B2.D0.BB.D0.B5.D1.87.D0.B5.D0.BD.D0.B8.D1.8F)

## Введение

mkinitcpio это Bash скрипт используемый для создания начального загрузочного диска системы. Из [mkinitcpio man page](https://projects.archlinux.org/mkinitcpio.git/tree/man/mkinitcpio.8.txt):

	*The initial ramdisk is in essence a very small environment (early userspace) which loads various kernel modules and sets up necessary things before handing over control to init. This makes it possible to have, for example, encrypted root file systems and root file systems on a software RAID array. mkinitcpio allows for easy extension with custom hooks, has autodetection at runtime, and many other features.*

Традиционно ядро отвечает за обнаружение всего оборудования и выполняет задачи на ранних этапах [процесса загрузки](/index.php/Boot_process "Boot process") до монтирования корневой файловой системы.

В настоящее время корневая файловая система может быть на широком диапазоне аппаратных средств от SCSI до SATA и USB дисков, управляемых различными контроллерами от разных производителей. Кроме того корневая файловая система может быть зашифрована или сжата, находиться в RAID массиве или группе логических томов. Простой способ справиться с этой сложностью является передача управления в пользовательском пространстве: начальный загрузочный диск.

Смотрите также: [/dev/brain0 » Blog Archive » Early Userspace in Arch Linux](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/).

mkinitcpio является модульным инструментом для построения initramfs CPIO образа, предлагая много преимуществ по сравнению с альтернативными методами. Эти преимущества включают в себя:

*   Использование [BusyBox](http://www.busybox.net/), чтобы обеспечить легкость базы для раннего userspace'a.
*   Поддержка **[udev](/index.php/Udev "Udev")** для автоматического обнаружения оборудования, предотвращая загрузку ненужных модулей.
*   Использование расширяемого hook-based скрипта с поддержкой пользовательских хуков, которые могут быть включены в состав пакетов и устанавливаться с помощью [pacman](/index.php/Pacman "Pacman").
*   Поддержка **LVM2**, **dm-crypt** как и LUKS томов, **mdadm**, и **swsusp**, и **suspend2** для использования спящего режимаи загрузки с USB носителей.
*   Предоставляет много возможностей для настройки из командной строки ядра без необходимости пересборки образа.

mkinitcpio создан разработчиками Arch Linux и вкладами сообщества. Смотрите [public Git repository](https://projects.archlinux.org/mkinitcpio.git/).

## Установка mkinitcpio

### Из текущего репозитория

**mkinitcpio** находится в репозитории current. Вы можете установить его командой

```
# pacman -S mkinitcpio

```

### Из git

Последнюю development версию **mkinitcpio**, можно получить из git командой

```
# git clone [git://projects.archlinux.org/mkinitcpio.git](git://projects.archlinux.org/mkinitcpio.git)

```

## Создание загрузочного образа

По умолчанию mkinitcpio генерирует два образа после установки или обновления ядра: `/boot/initramfs-linux.img` and `/boot/initramfs-linux-fallback.img`. *fallback* образ создается с точно таким же конфигурационным файлом за исключением хука **autodetect**, что позволяет включить в него все модули. Хук **autodetect** обнаруживает нужные модули необходимые для оборудования и включает их в initramfs.

Можно создать любое количество initramfs с различными конфигурациями. Необходимый initramfs должен быть прописан в [конфигурационном файле загрузчика](/index.php/Boot_Loader#Configuration_files "Boot Loader"). После изменения конфигурационного файла initramfs должен быть пересобран. Для стандартного ядра Arch Linux, [linux](https://www.archlinux.org/packages/?name=linux):

```
# mkinitcpio -p linux

```

Параметр `-p` (сокращение от *preset*) указывает на использование preset файла из `/etc/mkinitcpio.d` (т.е. `/etc/mkinitcpio.d/linux.preset` для `linux`). preset файл определяет параметры сборки initramfs образа вместо указания файла конфигурации и выходной файл каждый раз.

**Warning:** *preset* файлы используются для автоматической пересборки initramfs после обновления ядра; вудьте внимательны при редактировании их.

Пользователи могут вручную создать образ с помощью альтернативного конфигурационного файла. Например, следующее будет генерировать initramfs образ в соответствии с `/etc/mkinitcpio-custom.conf` и сохранит его в `/boot/linux-custom.img`.

```
# mkinitcpio -c /etc/mkinitcpio-custom.conf -g /boot/linux-custom.img

```

Если необходимо создать образ с ядром отличным от загруженного.Доступные версии ядер можно посмотреть в `/usr/lib/modules`.

```
# mkinitcpio -g /boot/linux.img -k 3.3.0-ARCH

```

## Редактирование файлов конфигурации

`/etc/mkinitcpio.conf` - основной конфигурационный файл **mkinitcpio**. Кроме того, в каталоге `/etc/mkinitcpio.d` располагаются preset файлы (e.g. `/etc/mkinitcpio.d/linux.preset`).

**Warning:** **lvm2**, **mdadm**, и **encrypt** **НЕ ВКЛЮЧЕНЫ** по умолчанию. Прочитайте эту страницу чтобы узнать как их включить и настроить.

**Note:** Если у вас более одного контроллера дисков использующих одно пространство имен устройств (например 2 SCSI/SATA или IDE контроллера) и они требуют разных модулей, укажите правильный порядок в `MODULES` в файле `/etc/mkinitcpio.conf`, иначе устройства могут поменяться местами и вы получите kernel panic при загрузке. Более правильный путь - использовать [persistent block device naming](/index.php/Persistent_block_device_naming "Persistent block device naming"), чтобы быть уверенным, что вы смонтировали действительно то, что хотели.

**Note:** **PS/2 keyboard users**: Для того, чтобы получить ввод с клавиатуры в начале загрузки, если он не работает, необходимо добавить **keyboard** хук в `HOOKS`. На некоторых материнских платах (в основном древних, но и некоторых новых), контроллер i8042 не может быть определен автоматически. Вы можете обнаружить эту ситуацию заранее. Если у вас есть порт PS/2 и появляется сообщение `i8042: PNP: No PS/2 controller found. Probing ports directly`, добавьте **atkbd** в `MODULES`.

Можно изменять шесть переменных в конфигурационном файле:

	`MODULES`

	Модули ядра, которые будут загружены до выполнения хуков.

	`BINARIES`

	Дополнительные исполняемые файлы, которые необходимо включить в initramfs.

	`FILES`

	Дополнительные файлы, которые необходимо включить в initramfs.

	`HOOKS`

	Hooks - скрипты, выполняемые в initramfs.

	`COMPRESSION`

	Тип используемого сжатия initramfs.

	`COMPRESSION_OPTIONS`

	Дополнительные опции архиваторов. Использование этого параметра не рекомендуется. mkinitcpio будет обрабатывать особые требования к архиваторам (например `--check=crc32` для xz), что может привести к невозможности запуска системы.

### MODULES

Указывает какие модули ядра должны быть загружены прежде чем что-либо будет сделано.

Для модулей с суффиксом `?` не будет выводиться ошибка, если они не будут найдены. Это может быть полезно для пользовательских ядер.

### BINARIES and FILES

Указывают какие файлы необходимо добавить в initramfs. `BINARIES` и `FILES` будут добавлены до запуска хуков и использоваться для переопределения файлов использаемых хуками. `BINARIES` - бинарные файлы из `PATH`, необходимые для работы библиотеки будут автоматически добавлены. `FILES` добавляет файлы как есть. Например:

```
FILES="/etc/modprobe.d/modprobe.conf"

```

```
BINARIES="kexec"

```

И в `BINARIES`, и в `FILES` может быть добавлено несколько файлов с пробелом в качестве разделителя.

### HOOKS

Параметр `HOOKS` наиболее важный в файле настроек. Хуки - это небольшие скрипты, которые описывают что будет добавлено к образу, а также дополнительные действия, выполняемые при загрузке системы. Хуки указываются по имени и выполняются по порядку.

The default `HOOKS` setting should be sufficient for most simple, single disk setups. For root devices which are stacked or multi-block devices such as [LVM](/index.php/LVM "LVM"), [mdadm](/index.php/Software_RAID_and_LVM "Software RAID and LVM"), or [dm-crypt](/index.php/Dm-crypt "Dm-crypt"), see the respective wiki pages for further necessary configuration.

#### Build hooks

Build hooks - хуки сборки. Располагаются в `/usr/lib/initcpio/install`. Эти файлы используются mkinitcpio во время сборки initramfs. Должны содержать две функции: `build` и `help`. Функция `build` перечисляет модули, файлы, исполняемые файлы, которые добавляются в образ. Функция `help` содержит описание действий хука.

Для получения списка всех доступных хуков:

```
$ mkinitcpio -L

```

Используйте опцию `-H` для вывода информации о конкретном хуке:

```
$ mkinitcpio -H udev

```

#### Runtime hooks

Runtime hooks - хуки выполняемые в initramfs. Располагаются в `/usr/lib/initcpio/hooks`. Для любого runtime хука существует хук сборки с таким же именем, в котором имеется вызов `add_runscript`, указывающий на добавление runtime хука в образ. Они запускаются по порядку записи в `HOOKS` за исключением cleanup хуков. Runtime хуки могут содержать несколько функций:

`run_earlyhook`: Functions of this name will be run once the API file systems have been mounted and the kernel command line has been parsed. This is generally where additional daemons, such as udev, which are needed for the early boot process are started from.

`run_hook`: Functions of this name are run shortly after the early hooks. This is the most common hook point, and operations such as assembly of stacked block devices should take place here.

`run_latehook`: Functions of this name are run after the root device has been mounted. This should be used, sparingly, for further setup of the root device, or for mounting other file systems, such as `/usr`.

`run_cleanuphook`: Functions of this name are run as late as possible, and in the reverse order of how they are listed in the `HOOKS` setting in the config file. These hooks should be used for any last minute cleanup, such as shutting down any daemons started by an early hook.

#### Доступные хуки

Таблица стандартных хуков и как они влияют на создание и выполнение образа. Обратите внимание, что эта таблица не является полной, так как пакеты могут предоставлять свои хуки.

| Hook | При установке | Во время выполнения |
| **base** | Устанавливает все начальные каталоги, базовые утилиты и библиотеки. Всегда ставьте этот хук первым, за исключением случаев, когда вы действительно знаете, что делаете. | -- |
| **systemd** | Запуск systemd в initramfs. Замена хукам *base*, *usr* и *udev*. Несовместим с некоторыми хуками (например encryption). Необходимо использовать аналоги с префиксом "sd-*". | -- |
| **btrfs** | Включает необходимые модули для использования [Btrfs](/index.php/Btrfs "Btrfs") в качестве корневой файловой системы. | Запуск `btrfs device scan` для сборки нескольких устройств Btrfs в корневую файловую систему при отсутвии хука udev. Требуется пакет [btrfs-progs](https://www.archlinux.org/packages/?name=btrfs-progs). |
| **udev** | Добавляет udev в образ ram-диска | Udev автоматически создает файл устройства для корня и загружает необходимые модули для его работы. Рекомендуется использовать. |
| **autodetect** | Уменьшает размер initramfs пытаясь определить какие модули вам нужны. Проверьте список модулей которые он добавил. Он должен запускаться раньше других подсистем. Все обработчики выполняемые до него будут включать все модули. | -- |
| **modconf** | Добавляет конфигурационные файлы modprobe `/etc/modprobe.d` и `/usr/lib/modprobe.d` | -- |
| **block** | Добавляет все модули блочных устройств, ранее предоставляемые другими хуками (*fw*, *mmc*, *pata*, *sata*, *scsi*, *usb*, *virtio*). | -- |
| **pcmcia** | Добавляет pcmcia модули. Требует наличия pcmciautils. | Загружает модули pcmcia. |
| **net** | Добавляет поддержку сети. Для PCMCIA устройств добавьте хук **pcmcia**. | Требуется для корневой файловой системы через NFS. |
| **dmraid** | Поддержка корневой файловой системы на fakeRAID массивах. Необходимо установить пакет [dmraid](https://www.archlinux.org/packages/?name=dmraid). Обратите внимание, что необходимо использовать `mdadm` с хуком **mdadm_udev** с fakeRAID если ваш контроллер поддерживает это. | Находит и монтирует fakeRAID блочные устройства используя `dmraid`. |
| **mdadm** | Обеспечивает поддержку для сборки RAID массивов из `/etc/mdadm.conf`, или автоопределеним во время загрузки. Необходимо установить пакет [mdadm](https://www.archlinux.org/packages/?name=mdadm). Вместо этого хука предпочтительнее использовать хук **mdadm_udev** . | Находит и собирает программные RAID блочные устройства с помощью `mdassemble`. |
| **mdadm_udev** | Обеспечивает поддержку для сборки RAID массивов с помощью udev. Необходимо установить пакет [mdadm](https://www.archlinux.org/packages/?name=mdadm). Если вы используете этот крючок с массивом FakeRAID, рекомендуется включить `mdmon` в секции BINARIES и добавить хук **shutdown** чтобы избежать восстановления массива при перезагрузке. | Находит и собирает программные RAID блочные устройства с помощь `udev` и `mdadm`.Это предпочтительный метод использования mdadm (заменяет хук *mdadm*). |
| **keyboard** | Добавляет модули необходимые для работы клавиатур. Используйте этот хук, если необходимо использовать USB клавиатуру на ранней стадии загрузки (в initramfs). | -- |
| **keymap** | Добавляет в initramfs раскладки указанные `/etc/vconsole.conf`. | Загружает раскладки указанные в `/etc/vconsole.conf`. |
| **consolefont** | Добавляет в initramfs консольный шрифт указанный `/etc/vconsole.conf`. | Загружает шрифт указанный в `/etc/vconsole.conf`. |
| **sd-vconsole** | Добавляет в initramfs раскладки и консольный шрифт указанные в `/etc/vconsole.conf`. Используется с хуком systemd. | Загружает раскладки и шрифт указанные в `/etc/vconsole.conf`. |
| **encrypt** | Добавляет dm-crypt модуль и программу cryptsetup. Требует установленный пакет cryptsetup. | Определяет и разблокирует зашифрованый корневой раздел. См. секцию [Изменение строки параметров ядра](/index.php/Configuring_mkinitcpio#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D0.BE.D0.B2_.D1.8F.D0.B4.D1.80.D0.B0 "Configuring mkinitcpio"). |
| **sd-encrypt** | Позволяет шифровать корневую файловую систему в initramfs с хуком systemd.

Смотрите доступные параметры загрузки ядра в man systemd-cryptsetup-generator(8). В качестве альтернативы, если файл `/etc/crypttab.initramfs` существует, он будет добавлен в initramfs как `/etc/crypttab`. для получения дополнительной информации о синтаксисе crypttab см. man crypttab(5).

 | -- |
| **lvm2** | Добавляет поддержку lvm. Требует установленного пакета lvm2\. | Включает поддержку lvm. |
| **fsck** | Добавляет исполняемый вайл fsck и необходимые обработчики файловых систем. Если стоит после хука **autodetect**, то будут добавлены только обработчики для Вашей корневой файловой системы. Использование этого крючка настоятельно рекомендуется и **обязательно** с отдельным `/usr` разделом. | Запускает fsck для корневой файловой системы (и раздела `/usr`) до монтирования. |
| **resume** | -- | Необходим для работы спящего режима (suspend to disk). Работает с *swsusp* и *[TuxOnIce](/index.php/TuxOnIce "TuxOnIce")*. См. [Hibernation](/index.php/Hibernation "Hibernation"). Работает только совместно с хуком `base`. Хук `systemd` использует свои механизмы resume. |
| **filesystems** | Включает в образ модули необходимых файловых систем. Этот хук **обязателен**, если Вы не указываете модули файловых систем в MODULES. | -- |
| **shutdown** | Переход в initramfs при выключении. Рекомендуется до mkinitcpio 0.16 версии при использовании отдельного раздела `/usr` или шифровании корня. Начиная с mkinitcpio 0.16 [не требуется](https://mailman.archlinux.org/pipermail/arch-dev-public/2013-December/025742.html). | Размонтирование и отключение устройств при выключении. |
| **usr** | Добавляет поддержку отделного `/usr` раздела. | Монтирует раздел `/usr` после монтирования корневой файловой системы. |

#### Примеры

Эта конфигурация будет работать для большинства пользователей:

```
HOOKS="base udev autodetect ide scsi sata filesystems"

```

Если вы хотите загружать систему на разных машинах используйте:

```
HOOKS="base udev ide scsi sata filesystems"

```

Вы можете использовать зашифрованные тома на lvm2:

```
HOOKS="base udev autodetect ide scsi sata lvm2 encrypt filesystems"

```

### Изменение переменной MODULES

MODULES содержит список модулей для включения в образ и загрузки. Например это нужно если вы не хотите использовать **udev** или **modload**. Тогда можно добавить все нужные модули вручную:

```
MODULES="piix ide_disk reiserfs"
HOOKS="base autodetect ide filesystems"

```

NOTE: Если вам нужен **reiser4**, вы ДОЛЖНЫ добавить его в список модулей.

### Настройка BINARIES и FILES

Эти опции добавляют в образ указанные файлы. Разница только в том, что BINARIES проверяет зависимости от библиотек, в то время как FILES просто копирует файлы.

Пример:

```
FILES="/etc/modprobe.d/modprobe.conf"

```

```
BINARIES="/usr/bin/somefile"

```

## Создание образа

### Пересоздание предопределенного образа / использование предустановок

Если вы хотите перегенерировать образы, используйте команду

```
# mkinitcpio -p linux

```

Это пример для пакета *linux*, но вы можете выполнить аналогичную команду и для других ядер.

Если вы хотите изменить настройки образов, отредактируйте `/etc/mkinitcpio.d/linux.preset` (для пакета linux). **Эти *.preset* файлы также будут использованы при обновлении ядра, не испортите их!**

### Вручную

Создайте образ командой:

```
mkinitcpio -g /boot/kernel26.img

```

Она создаст образ для текущего ядра в файле **/boot/kernel26.img**, который является образом для ядра из пакета **kernel26**. Пользователи **kernel26beyond** должны написать:

```
mkinitcpio -g /boot/kernel26beyond.img

```

Если вы хотите сгенерировать образ для ядра, которое в данный момент не загружено, используйте:

```
mkinitcpio -g /boot/kernel26.img -k 2.6.16-ARCH

```

#### Перегенерация fallback-образа

*Замечание:* Нижеследующий текст предназначен для создания образа для текущего ядра. Для других ядер используйте ключ -k.

Fallback образ должен быть уже создан если вы установили **kernel26** или **kernel26beyond**, но в случае если вы хотите его пересоздать используйте:

```
mkinitcpio -c /boot/mkinitcpio.d/kernel26-fallback.conf -g /boot/kernel26.img

```

для beyond ядер

```
mkinitcpio -c /boot/mkinitcpio.d/kernel26beyond-fallback.conf -g /boot/kernel26beyond.img

```

См. **mkinitcpio -h** чтобы увидеть другие опции.

Не забудьте добавить запись в загрузчик. Просто скопируйте старую запись и измените путь к initrd. Будьте аккуратны, всегда имейте провереный вариант загрузки в списке загрузчика. Вы можете использовать mkinitcpio с любыми вариантами ядер (kernel26, kernel26-beyond...).

## Изменения строки параметров ядра

Не зависимо от наличия initramfs некоторые опции приходится передавать через строку параметров ядра, как например корневое устройство. Некоторые из обработчиков mkinitcpio имеют специальные опции. Они и обсуждаются в этой главе.

Если вы не знаете, что такое строка параметров ядра, читайте документацию по [GRUB](/index.php/GRUB "GRUB") или [LILO](/index.php/LILO "LILO").

### Вход в безотказный режим

Если Вы добавите опцию

```
break=y

```

в строку параметров ядра, то init остановится после инициализации и вы получите *dash* шелл. Это может быть использовано, чтобы проверить, что все хорошо. После выхода загрузка продолжится в обычном режиме.

### Запрет обработчиков

Вы можете запретить обработчики при помощи параметра *disablehooks* в строке параметров ядра:

```
disablehooks=hook1,hook2,hook2

```

например,

```
disablehooks=resume

```

### Запрет загрузки модулей

Вы можете запретить загрузку некоторых модулей добавив параметр *disablemodules* в строку параметров ядра:

```
disablemodules=mod1,mod2,mod3

```

например,

```
disablemodules=ata_piix

```

### Использование raid

Добавьте обработчик raid в список HOOKS в /etc/mkinitcpio.conf

**Параметры ядра:** Укажите md массивы с помощью: md= parameter: (см. ниже). Простого добавления вашего raid массива достаточно.

```
 Пример: md=0,/dev/sda3,/dev/sda4 md=1,/dev/hda1,/dev/hdb1

```

Затем добавьте следующее в строку kernel в **grub/menu.lst**:

```
 Пример: md=0,/dev/sda3,/dev/sda4 md=1,/dev/hda1,/dev/hdb1

```

Т.е. это будет выглядеть так:

```
 kernel /vmlinuz26beyond root=/dev/md0 ro md=0,/dev/sda1,/dev/sdb1

```

Эта строка создает два md массива с постоянными суперблоками

**Настройка:**

```
 - для старых raid массивов без постоянных суперблоков:
    md=<номер устройства md>,<уровень raid>,<chunk size factor>,<fault level>,dev0,dev1
 - для raid массивом с постоянными суперблоками:
    md=<номер устройства md>,dev0,dev1,...,devn
 - для сборки partitionable массивов:
    md=d<md device no.>,dev0,dev1,...,devn

```

**Параметры:**

```
 - <номер устройства md> = номер устройства:
    0 значит md0, 1 значит md1, ...
 - <уровень raid> = -1 линейный режим, 0 striped режим
    другие режимы поддерживаются только с постоянным суперблоком
 - <chunk size factor> = (только для raid-0 и raid-1):
    Установить chunk size as 4k << n.
 - <fault level> = игнорируется
 - <dev0-devn>: т.е. /dev/hda1,/dev/hdc1,/dev/sda1,/dev/sdb1

```

### Использование net

**Параметры ядра:**

**ip=**

Описание интерфейса может быть в короткой форме, которая состоит просто из имени интерфейса (eth0 или какой либо еще), или в длинной форме. Длинная форма содержит семь элементов, разделенных двоеточием:

```
 ip=<client-ip>:<server-ip>:<gw-ip>:<netmask>:<hostname>:<device>:<autoconf>
 nfsaddrs= это алиас для ip= и может использоваться также.

```

*Разъяснение параметров:*

```
 <client-ip>   IP адрес клиента. Если пустой, то автоматически назначается
               протоколом RARP/BOOTP/DHCP. Какой протокол используется
               зависит от параметра <autoconf>. Если его значение не пустое,
               то autocnf работает корректно.

 <server-ip>   IP адрес NFS сервера. Если используется RARP для определения
               адреса клиента и этот параметр не пуст, то принимаются ответы
               только от указанного сервера.
               Для использования разных RARP и NFS серверов,
               укажите ваш RARP сервер здесь (или оставьте пустым), и
               укажите ваш NFS сервер в параметре `nfsroot'
               (см. выше). Если тут пусто, будет использован сервер, ответивший
               на RARP/BOOTP/DHCP запрос.

 <gw-ip>       IP адрес шлюза если сервер в другой подсети. Если тут пусто,
               предполагается, что сервер находится в одной подсети, если значение
               не получено по BOOTP/DHCP.

 <netmask>     Маска подсети для локального интерфейса. Если тут пусто,
               используется маска по умолчанию в зависимости от класса IP,
               если конечно не переопределена значением из BOOTP/DHCP ответа.

 <hostname>    Имя машины клиента. Если пусто, используется IP адрес в виде ASCII
               строки, или значение полученное по BOOTP/DHCP.

 <device>      Имя сетевого устройства. Если тут пусто, все устройства будут использованы
               для RARP/BOOTP/DHCP запросов, и все настройки будут получены из первого
               пришедшего ответа. Если вы имеете только одно сетевое устройство, можно спокойно
               оставить поле пустым.

 <autoconf>	Какой метод использовать для автонастройки: 'rarp', 'bootp', или 'dhcp'.
               Если значение 'both', 'all' или пусто, все протоколы будут использованы.
               'off', 'static' или 'none' означают запрет автонастройки.

```

*Примеры:*

```
 ip=127.0.0.1:::::lo:none  --> Разрешить lo интерфейс.
 ip=192.168.1.1:::::eth2:none --> Статический eth2 интерфейс.
 ip=:::::eth0:dhcp --> Разрешить dhcp протокол для настройки интерфейса eth0.

```

**nfsroot=**

Если параметр 'nfsroot' НЕ передан, будет использовано значение по умолчанию "/tftpboot/%s".

```
 nfsroot=[<server-ip>:]<root-dir>[,<nfs-options>]

```

*Описание параметров:*

```
 <server-ip>   IP адрес NFS сервера. Если параметр отсутствует
               адрес по умолчанию определяется по переменной
               `ip' (см. ниже). Одно из применений этого параметра -
               использование разных серверов для 
               RARP и NFS. Обычно можете оставить этот параметр пустым.

 <root-dir>    Путь к директории, которая будет корневой на клиенте. Если тут
               написано "%s", то оно будет заменено на ASCII представление IP
               клиента.

 <nfs-options> Стандартные опции NFS. Все опции разделены запятыми.
               Если опция отсутствует будут использованы следующие значения по умолчанию:
                       port            = как скажет portmap демон на сервере
                       rsize           = 1024
                       wsize           = 1024
                       timeo           = 7
                       retrans         = 3
                       acregmin        = 3
                       acregmax        = 60
                       acdirmin        = 30
                       acdirmax        = 60
                       flags           = hard, nointr, noposix, cto, ac

```

**root=/dev/nfs**

```
 Если вы не используете параметр nfsroot=, вам нужно установить root=/dev/nfs 
 для загрузки с автонастройкой корня в nfs.

```

### Использование lvm

Если ваш корень находится на lvm, вы должны добавить обработчик **lvm2**. Также, вы должны передать имя корневого устройства ядру в формате

```
root=/dev/mapper/<имя-группы-томов>-<логическое-имя-тома>

```

например

```
root=/dev/mapper/myvg-root

```

### Использование шифрования на корневом разделе

Если ваш корневой раздел зашифрован, вы должны добавить обработчик **encrypt**. Затем укажите ядру корневой раздел также, как если бы он не был зашифрован.

Например для sata/scsi:

```
root=/dev/sda5

```

или для зашифрованного lvm:

```
root=/dev/mapper/myvg-root

```

Корневое устройство автоматически поменяется на */dev/mapper/root*.

#### Использование LUKS томов

Если вы используете LUKS для шифрования дисков, скрипт инициализации поймет это автоматически, если вы указали обработчик **encrypt**. Он спросит пароль для разблокирования тома.

Если этого не происходит, попробуйте добавить filesystem-module в список модулей в фале /etc/mkinitcpio.conf если он не вкомпилирован в ядро.

#### Использование legacy cryptsetup томов

Если вы используете legacy cryptsetup том, вы должны указать все опции, необходимые для его разблокировки в строке параметров ядра. Опции формата

```
crypto=hash:cipher:keysize:offset:skip

```

представляют опции cryptsetup: --hash, --cipher, --keysize, --offset и --skip. Если вы пропустите опцию, будет использовано значение по умолчанию, т.е. вы можете написать просто

```
crypto=::::

```

если вы создали том с настройками по умолчанию.

**ЗАМЕЧАНИЕ:** По техническим причинам невозможно проверить корректность пароля для legacy cryptsetup тома. Если вы ошибетесь, у вас просто не получится его смонтировать. Рекомендуется использовать LUKS вместо legacy cryptsetup.

#### Использование loop-aes томов

**mkinitcpio** пока не поддерживает loop-aes.

## Использование спящего режима (на диск)

Если вы хотите, чтобы ваш компьютер засыпал на диск, вы должны добавить обработчик **resume**.

#### swsusp

*TODO*

#### µswsusp

µswsusp пока не поддерживается.

#### suspend2

Если вы используете [suspend2](/index.php/Suspend_to_Disk "Suspend to Disk"), вы должны указать обработчик *resume2* в параметрах ядра. Если вы используете запись в своп, пишите:

```
resume2=swap:/dev/hda3

```

где */dev/hda3* ваш своп раздел. Если вы пишите память в файл, используйте

```
resume2=file:/dev/hda2:0x123456

```

где */dev/hda2* раздел с файлом (обычно корневой раздел) и *0x123456* - смещение до файла. Вы можете получить его с помощью команд:

```
echo "/suspend2_file" > /proc/suspend2/filewriter_target
cat /proc/suspend2/resume2

```

где /suspend2_file - путь к файлу, куда записывается образ памяти. Это (естественно) работает и для томов lvm. Также можно использовать и зашифрованные разделы

```
resume2=file:/dev/mapper/root:0x123456

```

где *0x123456* снова смещение. Восстановление с зашифрованного своп раздела не поддерживается.

### Примеры конфигурационных файлов загрузчиков

Если Вы используете beyond kernel, замените имена фалов *kernel26.img* и *kernel26-fallback.img* на *kernel26beyond.img* и *kernel26beyond-fallback.img* соответственно. Так же замените "vmlinuz26" на "vmlinuz26beyond".

#### GRUB

Для тех у кого /boot на отдельном разделе диска:

```
# (0) Arch Linux
title Arch Linux
root   (hd0,3)
kernel /vmlinuz26 root=/dev/hda4 vga=791 ro
initrd /kernel26.img

title Arch Linux Fallback
root   (hd0,3)
kernel /vmlinuz26 root=/dev/hda4 vga=791 ro
initrd /kernel26-fallback.img

```

Для тех у кого /boot **не** на отдельном разделе диска:

```
# (0) Arch Linux
title Arch Linux
root   (hd0,3)
kernel /boot/vmlinuz26 root=/dev/hda4 vga=791 ro
initrd /boot/kernel26.img

title Arch Linux Fallback
root   (hd0,3)
kernel /boot/vmlinuz26 root=/dev/hda4 vga=791 ro
initrd /boot/kernel26-fallback.img

```

#### LILO

Если Вы используете загрузчик LILO, то рекомендуется использовать *append="root=/dev/XYZ"* вместо *root=/dev/XYZ*. Если у Вас уже есть глобальная опция *append*, тогда используйте *addappend*.

```
boot=/dev/hdX 
default = ArchLinux
timeout=50 
vga=791
lba32
prompt

# для образа автоопределения железа
image=/boot/vmlinuz26
label=ArchLinux
append="root=/dev/hdXY"
initrd=/boot/kernel26.img
read-only

# fallback image если другие образы не работают (Will most prob. never be used)
image=/boot/vmlinuz26
label=ArchLinuxFallBack
append="root=/dev/hdXY"
initrd=/boot/kernel26-fallback.img
read-only

```

## Возможные проблемы

### piix ide контролер и ядро beyond

#### Проблема

Если mkinitcpio не хочет определять ваш жесткий диск выдавая ошибки вида "Can't find device dev(0,0)" при переключении kinit, то это скорее всего из-за конфликта между драйвером ata_piix и piix. Ядро beyond содержит несколько патчей libata которые вызывают *конфликт* ata_piix с piix.

#### Решение

Измените /etc/mkinitcpio.conf так, чтобы он содержал только одну запись: или ide, или sata, или scsi, в зависимости от того откуда вы хотите загружать систему.

## Я параноик!

Если вам действительно нужно знать, что включено в initrd, вы можете вытаскивать и класть внутрь образа файлы. Это просто cpio архив, но...

### Предупреждение о cpio

Использование cpio для извлечения опасно (от root'а), так как оно пытается извлечь файлы в /, ломая существующую систему загрузки. Для исправления, вам придется переставить все пакеты, файлы которых были перезаписаны с помощью pacman.static. Список файлов выдаст команда bsdtar -t -f kernel26.img

### Использование bsdtar для извлечения

bsdtar извлекает файлы в текущий каталог.

Используйте команду:

```
 bsdtar -x -f /boot/kernel26.img

```