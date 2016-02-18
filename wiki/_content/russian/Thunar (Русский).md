Thunar - это новый файловый менеджер, создаваемый как быстрый, легковесный и простой в использовании. Является частью окружения рабочего стола Xfce4, но может быть использован с другими оконными менеджерами. Это делает Thunar весьма привлекательным для пользователей [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)") и [Awesome3](/index.php/Awesome3_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome3 (Русский)")

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Подключаемые модули и дополнения](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B0.D0.B5.D0.BC.D1.8B.D0.B5_.D0.BC.D0.BE.D0.B4.D1.83.D0.BB.D0.B8_.D0.B8_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [2.1 Менеджер томов Thunar](#.D0.9C.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80_.D1.82.D0.BE.D0.BC.D0.BE.D0.B2_Thunar)
        *   [2.1.1 Системные требования](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D0.B5_.D1.82.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
        *   [2.1.2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_2)
        *   [2.1.3 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.2 Дополнение архиватора Thunar](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D1.80.D1.85.D0.B8.D0.B2.D0.B0.D1.82.D0.BE.D1.80.D0.B0_Thunar)
    *   [2.3 Дополнения тегов мультимедиа](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F_.D1.82.D0.B5.D0.B3.D0.BE.D0.B2_.D0.BC.D1.83.D0.BB.D1.8C.D1.82.D0.B8.D0.BC.D0.B5.D0.B4.D0.B8.D0.B0)
    *   [2.4 Эскизы Thunar](#.D0.AD.D1.81.D0.BA.D0.B8.D0.B7.D1.8B_Thunar)
    *   [2.5 Общий доступ Thunar](#.D0.9E.D0.B1.D1.89.D0.B8.D0.B9_.D0.B4.D0.BE.D1.81.D1.82.D1.83.D0.BF_Thunar)
        *   [2.5.1 Установка дополнения](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
        *   [2.5.2 Настройка дополнения](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
*   [3 Советы и подсказки](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D0.BF.D0.BE.D0.B4.D1.81.D0.BA.D0.B0.D0.B7.D0.BA.D0.B8)
    *   [3.1 Запуск Thunar как демона](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Thunar_.D0.BA.D0.B0.D0.BA_.D0.B4.D0.B5.D0.BC.D0.BE.D0.BD.D0.B0)
    *   [3.2 Исправление отображения русских букв](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D1.80.D1.83.D1.81.D1.81.D0.BA.D0.B8.D1.85_.D0.B1.D1.83.D0.BA.D0.B2)
    *   [3.3 Не работает автомонтирование,нет корзины](#.D0.9D.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.2C.D0.BD.D0.B5.D1.82_.D0.BA.D0.BE.D1.80.D0.B7.D0.B8.D0.BD.D1.8B)
*   [4 Устранение конфликтов](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.84.D0.BB.D0.B8.D0.BA.D1.82.D0.BE.D0.B2)
    *   [4.1 Блокировка в hal-mtab](#.D0.91.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B2_hal-mtab)
    *   [4.2 Автоматическое монтирование с помощью udev](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_udev)
*   [5 Ссылки и руководства](#.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8_.D0.B8_.D1.80.D1.83.D0.BA.D0.BE.D0.B2.D0.BE.D0.B4.D1.81.D1.82.D0.B2.D0.B0)

## Установка

Чтобы установить Thunar, наберите команду:

```
# pacman -S thunar

```

Если вы используете Xfce4, то скорее всего Thunar у вас уже есть.

## Подключаемые модули и дополнения

Большинство дополнений для Thunar входят в группу `xfce4-goodies`, и если вы её загружали, то считайте, что все дополнения уже установлены.

### Менеджер томов Thunar

Thunar может автоматически монтировать и размонтировать съёмные устройства, а Менеджер томов Thunar обеспечивает дополнительные возможности, такие как автозапуск команд или открытие окна Thunar для подмонтированного устройства.

#### Системные требования

Учтите, что для правильной работы Менеджер томов Thunar требует запущенный Dbus.

**Обратите внимание:** В связи со заменой HAL на udev, автомонтирование не работает. Посмотрите раздел [автомонтирование с udev](/index.php/Thunar_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B5_.D0.BC.D0.BE.D0.BD.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.81_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_udev "Thunar (Русский)")

#### Установка

Менеджер томов Thunar можно установить так:

```
# pacman -S thunar-volman

```

#### Конфигурация

Менеджер томов можно настроить на выполнение определённых действий, например когда подключена фотокамера или аудиоплеер. Для этого нужно установить дополнения:

1.  Запустите Thunar и откройте Настройки.
2.  Во вкладке Дополнительно отметьте флажок 'Включить управление томами'.
3.  Щёлкните 'Настроить' и внесите необходимые изменения (пример см. ниже).

Например, вам нужно заставить Amarok проигрывать Audio CD:

```
Multimedia - Audio CDs: `amarok --cdplay %d`

```

### Дополнение архиватора Thunar

Дополнение архиватора Thunar - это фронтэнд к вашей программе-архиватору, например File Roller, Ark или Xarchiver. Он нужен, чтобы предоставить простой интерфейс для открытия и распаковки архивов.

Дополнение можно установить так:

```
# pacman -S thunar-archive-plugin

```

### Дополнения тегов мультимедиа

Если вы хотите, чтобы Thunar отображал подробную информацию о файлах мультимедиа, установите thunar-media-tags-plugin. Это дополнение поддерживает ID3 (формат MP3) и теги Ogg/Vorbis. Кроме того, в него включена функция массового переименования файлов и редактирования тегов мультимедиа.

Дополнение можно установить так:

```
# pacman -S thunar-media-tags-plugin

```

### Эскизы Thunar

Цель проекта Эскизы Thunar - создать генерацию эскизов для мультимедиа форматов, неподдерживаемых другими генераторами эскизов. Если вы хотели бы видеть эскизы и поддержку форматов мультимедиа, с которыми не работают другие генераторы эскизов, используйте Эскизы Thunar. Чтобы узнать полный список поддерживаемых форматов, посмотрите [страницу проекта](http://goodies.xfce.org/projects/thunar-plugins/thunar-thumbnailers/).

Дополнение можно установить из пакета [thunar-thumbnailers](https://www.archlinux.org/packages/?name=thunar-thumbnailers).

### Общий доступ Thunar

Дополнение oбщего доступа позволит вам быстро открыть общий доступ к папке из Thunar, используя [Samba](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)"). При этом вам не понадобится доступ от имени суперпользователя.

#### Установка дополнения

Установите пакет [thunar-shares-plugin](https://aur.archlinux.org/packages/thunar-shares-plugin/).

#### Настройка дополнения

Выполните описанные ниже действия от имени суперпользователя.

This marks the named objects for automatic export to the environment of subsequently executed commands:

```
export USERSHARES_DIR="/var/lib/samba/*usershares*"
export USERSHARES_GROUP="*sambashare*"

```

Создайте папку общих файлов впользователя в `/var/lib/samba`:

```
mkdir -p ${USERSHARES_DIR}

```

Создайте группу `sambashare`:

```
groupadd ${USERSHARES_GROUP}

```

Смените владельца папки и группы, которые вы только что создали:

```
chown root:${USERSHARES_GROUP} ${USERSHARES_DIR}

```

Измените разрешения папки с общими файлами так, чтобы пользователи в группе *sambashare* могли читать, писать и выполнять файлы:

```
chmod 01770 ${USERSHARES_DIR}

```

Откройте свой любимый текстовый редактор (например, [Nano](/index.php/Nano_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Nano (Русский)")) и создайте файл `/etc/samba/smb.conf`:

```
 ##This is the main Samba configuration file. You should read the
 ##smb.conf(5) manual page in order to understand the options listed
 ##here. Samba has a huge number of configurable options (perhaps too
 ##many!) most of which are not shown in this example
 ##
 ##For a step to step guide on installing, configuring and using samba, 
 ## read the Samba-HOWTO-Collection. This may be obtained from:
 ##  [http://www.samba.org/samba/docs/Samba-HOWTO-Collection.pdf](http://www.samba.org/samba/docs/Samba-HOWTO-Collection.pdf)
 ##
 ## Many working examples of smb.conf files can be found in the 
 ## Samba-Guide which is generated daily and can be downloaded from: 
 ##  [http://www.samba.org/samba/docs/Samba-Guide.pdf](http://www.samba.org/samba/docs/Samba-Guide.pdf)
 ##
 ## Any line which starts with a ; (semi-colon) or a # (hash) 
 ## is a comment and is ignored. In this example we will use a #
 ## for commentry and a ; for parts of the config file that you
 ## may wish to enable
 ##
 ## NOTE: Whenever you modify this file you should run the command "testparm"
 ## to check that you have not made any basic syntactic errors. 
 ##
 #[global]
 #  workgroup = WORKGROUP
 #  security = share
 #  server string = My Share
 #  load printers = yes
 #  log file = /var/log/samba/%m.log
 #  max log size = 50
 #  usershare path = /var/lib/samba/usershares
 #  usershare max shares = 100
 #  usershare allow guests = yes
 #  usershare owner only = yes
 #  
 #
 # #Windows Internet Name Serving Support Section:
 #
 # #WINS Support - Tells the NMBD component of Samba to enable it's WINS Server
 #;   wins support = yes
 #
 ## WINS Server - Tells the NMBD components of Samba to be a WINS Client
 ##	Note: Samba can be either a WINS Server, or a WINS Client, but NOT both
 #;   wins server = w.x.y.z
 #
 ##WINS Proxy - Tells Samba to answer name resolution queries on
 ## behalf of a non WINS capable client, for this to work there must be
 ## at least one	WINS Server on the network. The default is NO.
 #;   wins proxy = yes

```

Сохраните файл. Затем добавьте вашего пользователя в группу *sambashares*:

```
gpasswd -a *имя пользователя* ${USERSHARES_GROUP}

```

Перезапустите Samba:

```
/etc/rc.d/samba restart

```

Выйдите из системы и войдите снова. Теперь у вас есть возможность щёлкнуть правой кнопкой на любой папке и открыть к ней доступ из сети.

Для того, чтобы samba запускалась во время загрузки компьютера, добавьте *samba* в список демонов в файл `/etc/rc.conf`.

Если вы хотите узнать больше, загляните на страницу [Samba](/index.php/Samba_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Samba (Русский)")

## Советы и подсказки

### Запуск Thunar как демона

Thunar может запускаться как демон. Это даёт несколько преимуществ, включая более быстрый запуск Thunar и его выполнение в фоне.

Одно из решений - запускать Thunar автоматически через файл `~/.xinirc` или скрипт автозапуска (так, в [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)") это `autostart`).

Чтобы запустить Thunar как демона, просто добавьте в свой скрипт автозапуска или запустите из терминала:

```
thunar --daemon &

```

### Исправление отображения русских букв

В общесистемном `/etc/xdg/xfce4/mount.rc` или в пользовательском файле `~/.config/xfce4/mount.rc` добавьте *utf8=true* в секции файловых систем, с которыми имеет место проблема. Например:

```
[vfat]
uid=<auto>
shortname=winnt
utf8=true
# FreeBSD specific option
longnames=true

```

В этом файле определены правила для нескольких файловых систем:

*   **vfat** - FAT, флешки
*   **iso9660** - CDFS, компакт-диски CD
*   **udf** - UDF, обычно DVD
*   **ntfs** - собственно, NTFS
*   **ntfs-3g** - свободная реализация NTFS

### Не работает автомонтирование,нет корзины

Посетите статью про PCManFM все относится и к Thunar [[1]](https://wiki.archlinux.org/index.php/PCManFM_%28%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9%29)

## Устранение конфликтов

### Блокировка в hal-mtab

Если у вас одновременно работают hal и autofs, возможны блокировки в hal-mtab. Чтобы предотвратить это, используйте только один из них.

Если у вас не работает автоматическое монтирование при запуске вашего оконного менеджера через `~/.xinitrc`, вам, возможно, потребуется изменить строчку запуска для оконного менеджера с такой:

```
exec /usr/bin/dwm

```

### Автоматическое монтирование с помощью udev

Thunar и XFCE4 переходят на [udev](/index.php/Udev "Udev") для обнаружения и монтирования внешних мультимедиа устройств.

Установливайте Thunar как обычно, однако не забудьте добавить пользователя в группу 'storage' (`/etc/group`).

```
# usermod -a -G storage <user>

```

Если Вы используете [экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер") для запуска Вашего оконного менеджера, посмотрите документацию по настройке запуска с нужной [политикой доступа](/index.php/PolicyKit "PolicyKit"). Например, при использовании SLIM руководство [здесь](/index.php/Slim#PolicyKit "Slim").

## Ссылки и руководства

*   Страница [Thunar](http://thunar.xfce.org/index.html).
*   Страница [Thunar Volume Manager](http://goodies.xfce.org/projects/thunar-plugins/thunar-volman).
*   Страница [Thunar Archive Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-archive-plugin).
*   Страница [Thunar Media Tags Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-media-tags-plugin).
*   Страница [Thunar Thumbnailers](http://goodies.xfce.org/projects/thunar-plugins/thunar-thumbnailers/).
*   Страница [Thunar Shares Plugin](http://goodies.xfce.org/projects/thunar-plugins/thunar-shares-plugin/).
*   Список [модулей](http://goodies.xfce.org/projects/thunar-plugins/start).