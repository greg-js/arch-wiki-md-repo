Ссылки по теме

*   [Uswsusp](/index.php/Uswsusp "Uswsusp")
*   [TuxOnIce](/index.php/TuxOnIce "TuxOnIce")
*   [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)")
*   [Power management](/index.php/Power_management "Power management")

**Состояние перевода:** На этой странице представлен перевод статьи [Power management/Suspend and hibernate](/index.php/Power_management/Suspend_and_hibernate "Power management/Suspend and hibernate"). Дата последней синхронизации: 22 июля 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Power_management/Suspend_and_hibernate&diff=0&oldid=482651).

В настоящее время существует три метода приостановки работы компьютера: **suspend to RAM** обычно называемая просто **suspend**(приостановка, ждущий режим, сон, STR, S3 ), **suspend to disk** известный как **hibernate**( гибернация, спящий режим, STD, S4 ), и **hybrid suspend**( гибридная приостановка, гибридный спящий режим, иногда применяется название **suspend to both**):

*   **Suspend to RAM** отключает питание большинства частей компьютера, кроме ОЗУ, что требуется для восстановления состояния машины. Из-за большой экономии энергии рекомендуется, чтобы ноутбуки автоматически входили в этот режим, когда компьютер работает от батарей, и крышка закрыта или пользователь неактивен в течение некоторого времени.

*   **Suspend to disk** метод сохраняет состояние машины на диске [Swap (Русский)](/index.php/Swap_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Swap (Русский)") и полностью отключает компьютер, потребления электроэнергии нет. Когда устройство включается, состояние восстанавливается.

*   **Suspend to both** сохраняет состояние машины на диске в свопе, но не выключает ее. Вместо этого выполняется обычная приостановка в ОЗУ. Поэтому, если батарея не разряжена, система может возобновиться из ОЗУ. Если батарея разряжена, система может быть возобновлена с диска, что намного медленнее, чем возобновление работы из ОЗУ, но состояние машины не будет потеряно.

Существует несколько низкоуровневых интерфейсов, обеспечивающих базовые функции, а также некоторые интерфейсы высокого уровня, обеспечивающие трюки для обработки проблемных аппаратных драйверов / модулей ядра (например, повторная инициализация видеокарты).

## Contents

*   [1 Низкоуровневые интерфейсы](#.D0.9D.D0.B8.D0.B7.D0.BA.D0.BE.D1.83.D1.80.D0.BE.D0.B2.D0.BD.D0.B5.D0.B2.D1.8B.D0.B5_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B)
    *   [1.1 kernel (swsusp)](#kernel_.28swsusp.29)
    *   [1.2 uswsusp](#uswsusp)
*   [2 Интерфейсы высокого уровня](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B_.D0.B2.D1.8B.D1.81.D0.BE.D0.BA.D0.BE.D0.B3.D0.BE_.D1.83.D1.80.D0.BE.D0.B2.D0.BD.D1.8F)
    *   [2.1 systemd](#systemd)
*   [3 Гибернация](#.D0.93.D0.B8.D0.B1.D0.B5.D1.80.D0.BD.D0.B0.D1.86.D0.B8.D1.8F)
    *   [3.1 Про размер раздела/файла подкачки](#.D0.9F.D1.80.D0.BE_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80_.D1.80.D0.B0.D0.B7.D0.B4.D0.B5.D0.BB.D0.B0.2F.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BF.D0.BE.D0.B4.D0.BA.D0.B0.D1.87.D0.BA.D0.B8)
    *   [3.2 Необходимые параметры ядра](#.D0.9D.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D1.8B.D0.B5_.D0.BF.D0.B0.D1.80.D0.B0.D0.BC.D0.B5.D1.82.D1.80.D1.8B_.D1.8F.D0.B4.D1.80.D0.B0)
        *   [3.2.1 Гибернация в файл подкачки](#.D0.93.D0.B8.D0.B1.D0.B5.D1.80.D0.BD.D0.B0.D1.86.D0.B8.D1.8F_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB_.D0.BF.D0.BE.D0.B4.D0.BA.D0.B0.D1.87.D0.BA.D0.B8)
    *   [3.3 Настройка initramfs](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_initramfs)
*   [4 Исправление проблем](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [4.1 ACPI_OS_NAME](#ACPI_OS_NAME)
    *   [4.2 Пользователям VAIO](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F.D0.BC_VAIO)
    *   [4.3 Ждущий/Спящий режим не работает или сбоит](#.D0.96.D0.B4.D1.83.D1.89.D0.B8.D0.B9.2F.D0.A1.D0.BF.D1.8F.D1.89.D0.B8.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.B8.D0.BB.D0.B8_.D1.81.D0.B1.D0.BE.D0.B8.D1.82)
    *   [4.4 Wake-on-LAN](#Wake-on-LAN)
    *   [4.5 Instantaneous wakeups from suspend](#Instantaneous_wakeups_from_suspend)

## Низкоуровневые интерфейсы

Хотя эти интерфейсы могут использоваться напрямую, рекомендуется использовать какой-либо из [#Интерфейсы высокого уровня](#.D0.98.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D1.8B_.D0.B2.D1.8B.D1.81.D0.BE.D0.BA.D0.BE.D0.B3.D0.BE_.D1.83.D1.80.D0.BE.D0.B2.D0.BD.D1.8F) для ждущего / спящего режима. Использование низкоуровневых интерфейсов напрямую существенно быстрее, чем использование любого интерфейса высокого уровня, поскольку запуск всех хуков перед и после режима приостановки требует времени, но хуки могут правильно устанавливать аппаратные часы, восстанавливать беспроводное соединение и т.д.

### kernel (swsusp)

Самый простой подход для входа в режим сна заключается в прямом информировании встроенного программного кода ядра (swsusp); точный метод и состояние зависят от уровня аппаратной поддержки. В современных ядрах основным механизмом переключения режимов является запись соответствующих значений в `/sys/power/state`.

Cмотрите [документацию](https://www.kernel.org/doc/Documentation/power/states.txt) для подробностей.

### uswsusp

Uswsusp ('Userspace Software Suspend') представляет собой оболочку ядерного механизма приостановки в ОЗУ, которая выполняет некоторые манипуляции с графическим адаптером из пользовательского пространства перед приостановкой и после возобновления.

Смотрите основную статью [Uswsusp](/index.php/Uswsusp "Uswsusp").

## Интерфейсы высокого уровня

Конечной целью этих пакетов является предоставление программ( двоичных файлов/скриптов), которые могут быть вызваны для выполнения приостановки компьютера. Фактическая привязка их к кнопкам питания, щелчкам меню или событиям крышки ноутбука обычно предоставляется другим инструментам. Чтобы автоматически приостановить работу при определенных событиях, таких как закрытие крышки ноутбука или процент истощения батареи, вам может потребоваться запустить [Acpid](/index.php/Acpid "Acpid").

### systemd

[systemd](/index.php/Systemd "Systemd") предоставляет собственные команды для ждущего, спящего и гибридного режима приостановки, смотрите [Power management#Power management with systemd](/index.php/Power_management#Power_management_with_systemd "Power management") для деталей. Это интерфейс по умолчанию, используемый в Arch Linux. Смотрите [Power management#Sleep hooks](/index.php/Power_management#Sleep_hooks "Power management") для получения дополнительной информации о настройке хуков режимов сна. Также смотрите [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1), [systemd-sleep(8)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd-sleep.8) и [systemd.special(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemd.special.7).

## Гибернация

Чтобы использовать спящий режим, вам нужно создать [swap](/index.php/Swap "Swap") раздел или файл. Вам нужно будет указать ядру на своп, используя параметр `resume=`, который настраивается через загрузчик. Вам также понадобится [настроить initramfs](#Configure_the_initramfs). Это говорит ядру попытаться возобновить работу с указанного свопа в раннем пользовательском пространстве. Эти три этапа подробно описаны ниже.

### Про размер раздела/файла подкачки

Даже если ваш раздел подкачки меньше ОЗУ, у вас все еще есть большая вероятность успешно перейти в спящий режим. Согласно [ядерной документации](https://www.kernel.org/doc/Documentation/power/interface.txt):

*`/sys/power/image_size` управляет размером образа, создаваемого механизмом приостановки на диск. Это может быть строка, представляющая неотрицательное целое число, которое будет использоваться в качестве верхнего предела размера образа в байтах. Механизм приостановки сделает все возможное, чтобы размер образа не превышал это число. Однако, если это окажется невозможным, он попытается приостановить все равно, используя наименьший возможный размер образа. В частности, если в этот файл записать «0», размер образа будет настолько мал на сколько это возможно. Чтение из этого файла отображает текущее ограничение размера образа, которое по умолчанию установлено на 2/5 доступного ОЗУ.*

Вы можете либо уменьшить значение `/sys/power/image_size`, чтобы сделать образ как можно меньшим (для небольших разделов подкачки) или увеличить его, чтобы ускорить процесс гибернации.

### Необходимые параметры ядра

Должен быть использован параметр ядра `resume=*swap_partition*`. Либо имя, назначенное ядром для раздела, либо его [UUID](/index.php/UUID "UUID"), можно использовать как `*swap_partition*`. Например:

*   `resume=/dev/sda1`
*   `resume=UUID=4209c845-f495-4c43-8a03-5363dd433153`
*   `resume=/dev/mapper/archVolumeGroup-archLogicVolume` -- если используется LVM

В общем, метод именования, используемый для параметра `resume`, должен быть таким же, как и для параметра `root`. Конфигурация зависит от используемого [boot loader](/index.php/Boot_loader "Boot loader"), обратитесь к [Kernel parameters](/index.php/Kernel_parameters "Kernel parameters") за деталями.

#### Гибернация в файл подкачки

**Важно:** [Btrfs](/index.php/Btrfs#Swap_file "Btrfs") не поддерживает файлы подкачки. Несоблюдение этого предупреждения может привести к повреждению файловой системы. В то же время когда файл подкачки монтируется через устройство `/dev/loop` его можно использовать и на Btrfs, но это приведет к значительному ухудшению производительности подкачки.

Использование файла вместо раздела подкачки требует дополнительного параметра для ядра `resume_offset=*swap_file_offset*`.

Значение `*swap_file_offset*` можно получить запустив `filefrag -v *swap_file*`, требуемое значение расположено в столбце `physical_offset` первого ряда таблицы выводимой командой. Например:

 `# filefrag -v /swapfile` 
```
Filesystem type is: ef53
File size of /swapfile is 4294967296 (1048576 blocks of 4096 bytes)
 ext:     logical_offset:        physical_offset: length:   expected: flags:
   0:        0..       0:      38912..     38912:      1:            
   1:        1..   22527:      38913..     61439:  22527:             unwritten
   2:    22528..   53247:     899072..    929791:  30720:      61440: unwritten
...

```

В этом примере значение `*swap_file_offset*` это первое число `38912` с двумя точками.

Значение `*swap_file_offset*` так же может быть получено с помощью `swap-offset *swap_file*`. Файл команды *swap-offset* предоставляется пакетом [uswsusp-git](https://aur.archlinux.org/packages/uswsusp-git/).

**Примечание:**

*   Параметр ядра `resume` определяет устройство, раздел которого содержит файл подкачки, а не сам файл подкачки. О местонахождении файла подкачки на утройстве возобновления систему информирует параметр `resume_offset`. Перед первой гибернацией требуется перезагрузка для их активации.
*   Если вы используете [uswsusp](/index.php/Uswsusp "Uswsusp"), то эти два параметра должны быть представлены в `/etc/suspend.conf` с помощью ключей `resume device` и `resume offset`. В этом случае перезагрузка не требуется.

**Совет:** Возможно, вы захотите уменьшить [Swap#Swappiness](/index.php/Swap#Swappiness "Swap") для вашего файла подкачки, если единственная цель способность обеспечить спящий режим, а не расширение ОЗУ.

### Настройка initramfs

*   Когда используется [initramfs](/index.php/Initramfs "Initramfs") с хуком `base`, а по умолчанию это так, хук `resume` требуется в `/etc/mkinitcpio.conf`. Будь то по метке или по UUID раздел подкачки ссылается на файл устройства создаваемый udev, поэтому хук `resume` должен идти «после» хука `udev`. Этот пример был сделан на основе конфигурации хуков по умолчанию:

	 `HOOKS="base udev **resume** autodetect modconf block filesystems keyboard fsck"` 

	Не забудьте [пересобрать образ initramfs](/index.php/Mkinitcpio#Image_creation_and_activation "Mkinitcpio") чтобы эти изменения вступили в силу.

**Примечание:** [LVM](/index.php/LVM "LVM") пользователи должны добавить `resume` хук после `lvm2`.

*   Когда используется initramfs с хуком `systemd`, механизм возобновления уже предоставлен и дополнительные хуки не нужны.

## Исправление проблем

### ACPI_OS_NAME

Возможно, вы захотите настроить свою **таблицу DSDT**, чтобы заставить ее работать. Смотрите статью [DSDT](/index.php/DSDT "DSDT")

### Пользователям VAIO

Добавьте **acpi_sleep=nonvs** параметр ядра в ваш загрузчик и возьмите себе с полки пирожок!

### Ждущий/Спящий режим не работает или сбоит

There have been many reports about the screen going black without easily viewable errors or the ability to do anything when going into and coming back from suspend and/or hibernate. These problems have been seen on both laptops and desktops. This is not an official solution, but switching to an older kernel, especially the LTS-kernel, will probably fix this.

Sometimes the screen goes black due to device initialization from within the initramfs. Removing any modules you might have in [Mkinitcpio#MODULES](/index.php/Mkinitcpio#MODULES "Mkinitcpio") and rebuilding the initramfs, can possibly solve this issue, specially graphics drivers for [early KMS](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting"). Initializing such devices before resuming can cause inconsistencies that prevents the system resuming from hibernation. This does not affect resuming from RAM. Also, check this [article](https://01.org/blogs/rzhang/2015/best-practice-debug-linux-suspend/hibernate-issues) for the best practices to debug suspend/hibernate issues.

For Intel graphics drivers, enabling early KMS may help to solve the blank screen issue. Refer to [Kernel mode setting#Early KMS start](/index.php/Kernel_mode_setting#Early_KMS_start "Kernel mode setting") for details.

### Wake-on-LAN

If [Wake-on-LAN](/index.php/Wake-on-LAN "Wake-on-LAN") is active, the network interface card will consume power even if the computer is hibernated.

### Instantaneous wakeups from suspend

For some Intel Haswell systems with the LynxPoint and LynxPoint-LP chipset, instantaneous wakeups after suspend are reported. They are linked to erroneous BIOS ACPI implementations and how the `xhci_hcd` module interprets it during boot. As a work-around reported affected systems are added to a blacklist (named `XHCI_SPURIOUS_WAKEUP`) by the kernel case-by-case.[[1]](https://bugzilla.kernel.org/show_bug.cgi?id=66171#c6)

Instantaneous resume may happen, for example, if a USB device is plugged during suspend and ACPI wakeup triggers are enabled. A viable work-around for such a system, if it is not on the blacklist yet, is to disable the wakeup triggers. An example to disable wakeup through USB is described as follows.[[2]](https://bbs.archlinux.org/viewtopic.php?pid=1575617)

To view the current configuration:

 `$ cat /proc/acpi/wakeup` 
```
Device  S-state   Status   Sysfs node
...
EHC1      S3    *enabled  pci:0000:00:1d.0
EHC2      S3    *enabled  pci:0000:00:1a.0
XHC       S3    *enabled  pci:0000:00:14.0
...

```

The relevant devices are `EHC1`, `EHC1` and `XHC` (for USB 3.0). To toggle their state you have to echo the device name to the file as root.

```
# echo EHC1 > /proc/acpi/wakeup
# echo EHC2 > /proc/acpi/wakeup
# echo XHC > /proc/acpi/wakeup

```

This should result in suspension working again. However, this settings are only temporary and would have to be set at every reboot. To automate this take a look at [systemd#Writing unit files](/index.php/Systemd#Writing_unit_files "Systemd"). See [BBS thread](https://bbs.archlinux.org/viewtopic.php?pid=1575617#p1575617) for a possible solution and more information.