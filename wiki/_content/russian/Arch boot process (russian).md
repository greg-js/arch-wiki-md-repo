Ссылки по теме

*   [Fstab (Русский)](/index.php/Fstab_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fstab (Русский)")
*   [Автозапуск](/index.php/Autostarting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Autostarting (Русский)")

Эта статья призвана описать процесс загрузки Arch Linux и перечислить вовлеченные в процесс загрузки системные файлы, предоставляя ссылки на соответствующие статьи в вики там, где это потребуется. Arch славится своей приверженностью стилю загрузки [BSD](https://en.wikipedia.org/wiki/Berkeley_Software_Distribution "wikipedia:Berkeley Software Distribution"), в отличии более распространенного [SysV](https://en.wikipedia.org/wiki/UNIX_System_V "wikipedia:UNIX System V"). Это означает, что существует небольшое различие между уровнями выполнения([Wikipedia:runlevel](https://en.wikipedia.org/wiki/runlevel "wikipedia:runlevel")), поскольку система по умолчанию сконфигурирована использовать и запускать одни и те же модули и процессы на всех уровнях выполнения. Преимуществом такой схемы выступает то, что пользователю становится легче настроить процесс запуска (см. [rc.conf](/index.php/Rc.conf "Rc.conf")); с другой стороны, некоторые способы углубленного конфигурирования (какие были в SysV) потеряны. Тем, кого это не устраивает, будет полезно обратиться к статье [Adding Runlevels](/index.php/Adding_Runlevels "Adding Runlevels"). Чтобы узнать больше о различиях между стилями инициализации BSD и SysV см. [Wikipedia:Init](https://en.wikipedia.org/wiki/Init "wikipedia:Init")

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 До выполнения init](#До_выполнения_init)
*   [2 Пользовательские ловушки](#Пользовательские_ловушки)
    *   [2.1 Пример](#Пример)
*   [3 init: Идентификация в системе](#init:_Идентификация_в_системе)
*   [4 См. также](#См._также)

## До выполнения init

После подачи питания системе и завершения [POST](https://en.wikipedia.org/wiki/Power-on_self-test "wikipedia:Power-on self-test"), [BIOS](https://en.wikipedia.org/wiki/BIOS "wikipedia:BIOS") определяет с какого устройства необходимо начать загрузку и передает управление на [Master Boot Record](/index.php/Master_Boot_Record "Master Boot Record") этого устройства. На машине под управлением GNU/Linux в качестве загрузчика ОС чаще всего используют [GRUB](/index.php/GRUB "GRUB") или [LILO](/index.php/LILO "LILO"), который собственно и располагается в MBR. Загрузчик может предоставить пользователю выбор ОС для загрузки. Такая установка описана в статье [Windows and Arch Dual Boot (Русский)](/index.php/Windows_and_Arch_Dual_Boot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Windows and Arch Dual Boot (Русский)"). После выбора Arch Linux в качестве ОС для запуска, загрузчик размещает в памяти [ядро Linux](https://en.wikipedia.org/wiki/Linux_kernel "wikipedia:Linux kernel") (`vmlinuz-linux`) и образ первичной корневой файловой системы (`initramfs-linux.img`), затем загрузчик запускает ядро, передавая ему также параметры запуска, указанные в конфигурационном файле загрузчика.

Ядро выполняет роль прослойки между аппаратной частью и программами, которые используют ресурсы системы, необходимые им для работы. Для эффективного использования процессора в ядре имеется планировщик, который определяет какой задаче передать приоритет выполнения в любой конкретный момент времени, таким образом создавая иллюзию одновременного выполнения задач.

Также, после запуска, ядро распаковывает [initramfs](/index.php/Initramfs "Initramfs") (сокр. от initial RAM filesystem/первичная файловая система в ОЗУ), которая становится первичной корневой файловой системой. Затем ядро запускает на выполнение `/init`. Таким образом, init становится первым процессом [пространства пользователя](https://en.wikipedia.org/wiki/User_space "wikipedia:User space")

Конечной целью работы initramfs является получение доступа к корневой файловой системе с устройства (см. также [FHS](/index.php/FHS "FHS")). Для работы с устройствами IDE, SCSI, SATA, USB/FW (если загрузка происходит с внешнего носителя) требуются соответствующие модули, которые должны быть либо встроены в ядро, или непосредственно загружены из initramfs; как только подходящий модуль найден (с помощью программы/скрипта или через [udev](/index.php/Udev "Udev")), процесс загрузки продолжится. Для получения доступа к корневой файловой системе, initramfs не обязательно содержать все возможные модули, которые только могут потребоваться во время работы с устройствами хранения данных. Большинство остальных модулей устройств будут загружены позже, во время инициализации, с помощью udev.

На заключительной стадии *[раннего пространства пользователя](http://archlinux.me/brain0/2010/02/13/early-userspace-in-arch-linux/)* взамен первичной(инициализирующей) корневой файловой системы [монтируется](https://ru.wikipedia.org/wiki/%D0%9C%D0%BE%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%B8%D0%B5_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%BE%D0%B9_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D1%8B) ФС с устройства. И с неё запускается `/sbin/init`, подменяя собой временный `/init`.

## Пользовательские ловушки

Ловушки полезны, когда необходимо включить какой-либо код в различные места скриптов rc.* без их редактирования.

| Наименование ловушки | Момент исполнения |
| sysinit_start | В начале rc.sysinit |
| sysinit_udevlaunched | После запуска udev в rc.sysinit |
| sysinit_udevsettled | После получения uevents в rc.sysinit |
| sysinit_prefsck | Перед запуском fsck в rc.sysinit |
| sysinit_postfsck | После запуска fsck в rc.sysinit |
| sysinit_premount | Перед монтированием локальных файловых систем, но после того, как был монтирован корень(/) в режиме чтения-записи в rc.sysinit |
| sysinit_end | В конце rc.sysinit |
| multi_start | В начале rc.multi |
| multi_end | В конце rc.multi |
| single_start | В начале rc.single |
| single_prekillall | Перед убийством всех процессов в rc.single |
| single_postkillall | После убийства всех процессов в rc.single |
| single_udevlaunched | После запуска udev в rc.single |
| single_udevsettled | После получения uevents в rc.single |
| single_end | В конце rc.single |
| shutdown_start | В начале rc.shutdown |
| shutdown_prekillall | Перед убийством всех процессов в rc.shutdown |
| shutdown_postkillall | После убийства всех процессов в rc.shutdown |
| shutdown_poweroff | Непосредственно перед отключением питания в rc.shutdown |

Для объявления функции-ловушки создайте файл в `/etc/rc.d/functions.d` используя в качестве примера:

```
function_name() {
   ...
}
add_hook hook_name function_name

```

Файлы из `/etc/rc.d/functions.d` читаются скриптом `/etc/rc.d/functions`. Позволяется регистрировать как несколько функций-ловушек на один и тот же тип ловушки, так и несколько типов ловушек на одну и ту же функцию-ловушку. В этих файлах запрещается именовать функцию как add_hook или run_hook, поскольку функции с такими именами уже объявлены в `/etc/rc.d/functions`.

#### Пример

Добавление следующего файла отключает [кэш отложенной записи](https://ru.wikipedia.org/wiki/%D0%9A%D1%8D%D1%88#.D0.9F.D0.BE.D0.BB.D0.B8.D1.82.D0.B8.D0.BA.D0.B0_.D0.B7.D0.B0.D0.BF.D0.B8.D1.81.D0.B8_.D0.BF.D1.80.D0.B8_.D0.BA.D1.8D.D1.88.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8) на жестком диске *перед* стартом [сервисов](/index.php/Daemons_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemons (Русский)") (полезно для устройств, содержащих файлы MySQL InnoDB).

 `/etc/rc.d/functions.d/hd_settings` 
```
hd_settings() {
    /usr/bin/hdparm -W0 /dev/sdb
}
add_hook sysinit_udevsettled hd_settings
add_hook single_udevsettled  hd_settings

```

Сперва объявляется функция-ловушка hd_settings, затем она регистрируется на ловушки типа **single_udevsettled** и **sysinit_udevsettled**. Функция-ловушка будет вызываться незамедлительно после получения uevents в `/etc/rc.d/rc.sysinit` или `/etc/rc.d/rc.single`.

## init: Идентификация в системе

По умолчанию, после завершения всех скриптов запуска, программа `/sbin/agetty` просит вас представиться в системе. После ввода имени пользователя `/sbin/agetty` вызывает программу `/bin/login`, чтобы она запросила пароль.

Наконец, после успешного входа, программа `/bin/login` запускает командный интерпретатор (shell / оболочку) пользователя. Стандартный шелл а также [переменные среды](https://ru.wikipedia.org/wiki/%D0%9F%D0%B5%D1%80%D0%B5%D0%BC%D0%B5%D0%BD%D0%BD%D1%8B%D0%B5_%D1%81%D1%80%D0%B5%D0%B4%D1%8B) (environment variables) могут быть объявлены глобально, с помощью `/etc/profile`. Все переменные, объявленные в стартовых скриптах домашней директории пользователя, получают приоритет над переменными объявленными глобально в `/etc`. К примеру, если переменная с одним и тем же одним именем объявлена в `/etc/profile` и `~/.bashrc`, та, что находится в `~/.bashrc` будет иметь преимущественную силу.

Большинство пользователей, желающих запустить при старте оконную систему [X](/index.php/X_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "X (Русский)"), пожелают также установить графический менеджер входа в систему (см. [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")). Также, статья [Запуск X при входе](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA_X_%D0%BF%D1%80%D0%B8_%D0%B2%D1%85%D0%BE%D0%B4%D0%B5 "Запуск X при входе") охватывает методы, которые не требуют установки менеджера входа.

## См. также

*   [Boot Linux Grub Into Single User Mode](http://www.cyberciti.biz/faq/grub-boot-into-single-user-mode/)
*   [Boot with GRUB](http://www.linuxjournal.com/article/4622)
*   [Inside the Linux boot process](http://www.ibm.com/developerworks/linux/library/l-linuxboot/)
*   [Linux / Unix Command: sysctl.conf](http://linux.about.com/library/cmd/blcmdl5_sysctl.conf.htm)
*   [Search the forum for rc.local examples](https://bbs.archlinux.org/search.php?action=search&keywords=rc.local&search_in=topic&sort_dir=DESC&show_as=topics)
*   [Wikipedia:Linux startup process](https://en.wikipedia.org/wiki/Linux_startup_process "wikipedia:Linux startup process")
*   [Wikipedia:initrd](https://en.wikipedia.org/wiki/initrd "wikipedia:initrd")