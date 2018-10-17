Ссылки по теме

*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [KDE (Русский)](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [SDDM](/index.php/SDDM "SDDM"). Дата последней синхронизации: 15 октября 2018\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=SDDM&diff=0&oldid=547492).

[Simple Desktop Display Manager](https://github.com/sddm/sddm/) (SDDM) – это предпочтительный [экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер") для [KDE](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "KDE (Русский)") Plasma.

Из [Википедии](https://en.wikipedia.org/wiki/ru:Simple_Desktop_Display_Manager "wikipedia:ru:Simple Desktop Display Manager"):

	*Simple Desktop Display Manager (SDDM) — это дисплейный менеджер (программа для графического логин скрина) для X11 . SDDM был написан с нуля на языке C++11 и поддерживает установку тем через QML. SDDM является заменой устаревшему KDE Display Manager и интегрируется в KDE Frameworks 5, KDE Plasma 5 и KDE Applications 5.*

**Примечание:** Протокол Wayland поддерживается не полностью [[1]](https://github.com/sddm/sddm/issues/440). Сеансы Wayland отображаются в списке, но сам SDDM использует X11.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Автоматический вход в систему](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B2.D1.85.D0.BE.D0.B4_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [2.2 Автоматическая разблокировка KDE Wallet при входе в систему](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B0.D1.8F_.D1.80.D0.B0.D0.B7.D0.B1.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_KDE_Wallet_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [2.3 Настройки темы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D1.82.D0.B5.D0.BC.D1.8B)
        *   [2.3.1 Текущая тема](#.D0.A2.D0.B5.D0.BA.D1.83.D1.89.D0.B0.D1.8F_.D1.82.D0.B5.D0.BC.D0.B0)
        *   [2.3.2 Редактирование тем](#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D0.BC)
        *   [2.3.3 Тестирование (предпросмотр) темы](#.D0.A2.D0.B5.D1.81.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.28.D0.BF.D1.80.D0.B5.D0.B4.D0.BF.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80.29_.D1.82.D0.B5.D0.BC.D1.8B)
        *   [2.3.4 Курсор мыши](#.D0.9A.D1.83.D1.80.D1.81.D0.BE.D1.80_.D0.BC.D1.8B.D1.88.D0.B8)
        *   [2.3.5 Аватар пользователя](#.D0.90.D0.B2.D0.B0.D1.82.D0.B0.D1.80_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
    *   [2.4 Numlock](#Numlock)
    *   [2.5 Поворот экрана](#.D0.9F.D0.BE.D0.B2.D0.BE.D1.80.D0.BE.D1.82_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
    *   [2.6 Настройки DPI](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_DPI)
    *   [2.7 Включение HiDPI](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_HiDPI)
*   [3 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [3.1 Долгая загрузка перед отображением экрана приветствия SDDM](#.D0.94.D0.BE.D0.BB.D0.B3.D0.B0.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.B4_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F_SDDM)
    *   [3.2 Зависания после входа](#.D0.97.D0.B0.D0.B2.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0)
    *   [3.3 SDDM запускается на tty1 вместо tty7](#SDDM_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BD.D0.B0_tty1_.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BE_tty7)
    *   [3.4 Один или более пользователей не отображаются на экране приветствия](#.D0.9E.D0.B4.D0.B8.D0.BD_.D0.B8.D0.BB.D0.B8_.D0.B1.D0.BE.D0.BB.D0.B5.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_.D0.BD.D0.B5_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D1.8E.D1.82.D1.81.D1.8F_.D0.BD.D0.B0_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B5_.D0.BF.D1.80.D0.B8.D0.B2.D0.B5.D1.82.D1.81.D1.82.D0.B2.D0.B8.D1.8F)
    *   [3.5 SDDM загружает только английскую (US) раскладку клавиатуры](#SDDM_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B6.D0.B0.D0.B5.D1.82_.D1.82.D0.BE.D0.BB.D1.8C.D0.BA.D0.BE_.D0.B0.D0.BD.D0.B3.D0.BB.D0.B8.D0.B9.D1.81.D0.BA.D1.83.D1.8E_.28US.29_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D1.83_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [3.6 Слишком низкое разрешение экрана](#.D0.A1.D0.BB.D0.B8.D1.88.D0.BA.D0.BE.D0.BC_.D0.BD.D0.B8.D0.B7.D0.BA.D0.BE.D0.B5_.D1.80.D0.B0.D0.B7.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B0)
    *   [3.7 Долгая загрузка с домашней директорией на autofs](#.D0.94.D0.BE.D0.BB.D0.B3.D0.B0.D1.8F_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BA.D0.B0_.D1.81_.D0.B4.D0.BE.D0.BC.D0.B0.D1.88.D0.BD.D0.B5.D0.B9_.D0.B4.D0.B8.D1.80.D0.B5.D0.BA.D1.82.D0.BE.D1.80.D0.B8.D0.B5.D0.B9_.D0.BD.D0.B0_autofs)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [sddm](https://www.archlinux.org/packages/?name=sddm). Опционально установите пакет [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm) для использования модуля [KCM](/index.php/KDE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#KCM "KDE (Русский)").

Теперь следуйте инструкциям из раздела [Экранный менеджер#Запуск экранного менеджера](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0 "Экранный менеджер"), чтобы запускать SDDM при загрузке.

## Настройка

Настройки SDDM по умолчанию хранятся в файле `/usr/lib/sddm/sddm.conf.d/default.conf`. Для каких-либо изменений создайте конфигурационный файл(ы) в директории `/etc/sddm.conf.d/`. Для получения полного списка настроек смотрите страницу справочного руководства [sddm.conf(5)](https://jlk.fjfi.cvut.cz/arch/manpages/man/sddm.conf.5).

Пакет [sddm-kcm](https://www.archlinux.org/packages/?name=sddm-kcm) (входящий в группу [plasma](https://www.archlinux.org/groups/x86_64/plasma/)) предлагает графический интерфейс для конфигурации SDDM в *Параметрах системы* KDE Plasma. Также в [AUR (Русский)](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") доступен редактор настроек [sddm-config-editor-git](https://aur.archlinux.org/packages/sddm-config-editor-git/) на основе [Qt (Русский)](/index.php/Qt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Qt (Русский)").

Всё должно работать "из коробки", так как Arch Linux использует [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") и SDDM по умолчанию использует `systemd-logind` для управления сессиями.

### Автоматический вход в систему

SDDM поддерживает автоматический вход. Для этого настройте конфигурационный файл, например:

 `/etc/sddm.conf.d/autologin.conf` 
```
[Autologin]
User=ivan
Session=plasma.desktop
```

Эта конфигурация позволит автоматически запускать KDE Plasma для пользователя `ivan` при загрузке системы. Все доступные сеансы доступны в директории `/usr/share/xsessions/`.

Также недоступна возможность автоматического входа в KDE Plasma с одновременной блокировкой сеанса [[2]](https://github.com/sddm/sddm/issues/306).

Вы можете добавить скрипт, который активирует скринсейвер KDE при автозапуске в качестве обходного пути:

```
#!/bin/sh
/usr/bin/dbus-send --session --type=method_call --dest=org.freedesktop.ScreenSaver /ScreenSaver org.freedesktop.ScreenSaver.Lock &

```

### Автоматическая разблокировка KDE Wallet при входе в систему

Смотрите [KDE Wallet#Unlock KDE Wallet automatically on login](/index.php/KDE_Wallet#Unlock_KDE_Wallet_automatically_on_login "KDE Wallet").

### Настройки темы

Настройки темы могут быть изменены в секции `[Theme]`. Также можно увидеть предпросмотр тем, если вы используете приложение *Параметры системы* в KDE Plasma.

Задайте значение `breeze` для стандартной темы KDE Plasma.

Также некоторые темы доступны в [AUR (Русский)](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"), например, [archlinux-themes-sddm](https://aur.archlinux.org/packages/archlinux-themes-sddm/).

#### Текущая тема

Установите текущую тему с помощью значения `Current`, например, `Current=archlinux-simplyblack`.

#### Редактирование тем

Каталогом тем для SDDM по умолчанию является `/usr/share/sddm/themes/`. Вы можете добавить свои собственные темы в отдельный подкаталог этой директории. Заметьте, что названия подкаталогов должны совпадать с названием самой темы. Изучите установленные файлы для их изменения или создания собственной темы.

#### Тестирование (предпросмотр) темы

В случае необходимости, вы можете предварительно просматривать тему SDDM. Это особенно полезно в случае, когда вы не уверены в том, как тема будет смотреться (в частности, после её редактирования) без необходимости выхода из аккаунта. Вы можете выполнить команду вроде следующей:

```
$ sddm-greeter --theme /usr/share/sddm/themes/breeze

```

Эта команда должна открыть новое окно с предварительным просмотром темы.

**Примечание:** Это лишь предварительный просмотр. В этом режиме не работают некоторые функции, например, выключение, переход в режим сна или вход в систему.

#### Курсор мыши

Чтобы задать тему для курсора мыши, установите `CursorTheme` на предпочитаемую вами тему курсора.

Допустимыми значениями для [Plasma (Русский)](/index.php/Plasma_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Plasma (Русский)") являются `breeze_cursors`, `Breeze_Snow` и `breeze-dark`.

#### Аватар пользователя

SDDM считывает иконку пользователя (аватар) как изображение PNG `~/.face.icon` для каждого пользователя. Также можно задать единую директорию для аватаров всех пользователей используя переменную `FacesDir` в файле конфигурации SDDM. Данный файл должен располагаться в `/etc/sddm.conf` или, лучше, в `/etc/sddm.conf.d/`, например, `/etc/sddm.conf.d/avatar.conf`.

Для использования функции `FacesDir`, разместите изображение PNG под названием `*username*.face.icon` в директории, указанной параметром `FacesDir` в файле конфигурации. По умолчанию используется директория `/usr/share/sddm/faces/`. Вы можете изменить стандартное значение `FacesDir`, например:

 `/etc/sddm.conf.d/avatar.conf` 
```
[Theme]
FacesDir=/var/lib/AccountsService/icons/
```

Также можно разместить PNG-изображение под названием `.face.icon` в корне вашей домашней директории. В таком случае не потребуется вносить какие-либо изменения в файл конфигурации SDDM. Тем не менее, вам нужно убедиться, что пользователь `sddm` имеет права на чтение аватаров.

**Примечание:** Во многих версиях KDE аватаром пользователя являются файлы `~/.face` и `~/.face.icon` (символическая ссылка на первый файл). Если аватары пользователя – это символические ссылки, вам потребуется задать корректные права доступа к исходному файлу.

Для [задания корректных прав](/index.php/Access_Control_Lists_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B0.D0.B2_ACL "Access Control Lists (Русский)"), выполните следующую команду:

```
$ setfacl -m u:sddm:x ~/
$ setfacl -m u:sddm:r ~/.face.icon

```

Вы можете [проверить права](/index.php/Access_Control_Lists_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.BF.D1.80.D0.B0.D0.B2_ACL "Access Control Lists (Русский)") с помощью данной команды:

```
$ getfacl ~/
$ getfacl ~/.face.icon

```

Смотрите [SDDM README: No User Icon](https://github.com/sgerbino/sddm#no-user-icon).

### Numlock

Если вы хотите, чтобы Numlock автоматически включался, пропишите `Numlock=on` в секции `[General]`.

### Поворот экрана

Смотрите [Xrandr (Русский)#Настройка](/index.php/Xrandr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0 "Xrandr (Русский)").

### Настройки DPI

Иногда требуется задать корректные настройки PPI вашего монитора на уровне экранного менеджера. Для этого нужно найти параметр `ServerArguments` в `sddm.conf` и добавить `-dpi *ваш_dpi*` в конце строки.

Например:

 `/etc/sddm.conf.d/dpi.conf` 
```
[X11]
ServerArguments=-nolisten tcp -dpi 94
```

### Включение HiDPI

Создайте следующий файл:

 `/etc/sddm.conf.d/hidpi.conf` 
```
[Wayland]
EnableHiDPI=true

[X11]
EnableHiDPI=true
```

## Решение проблем

### Долгая загрузка перед отображением экрана приветствия SDDM

Низкий уровень энтропии в системе может стать причиной долгой загрузки SDDM. Смотрите статью [Random number generation](/index.php/Random_number_generation "Random number generation") для идей по повышению уровня энтропии.

### Зависания после входа

Попробуйте удалить файл `~/.Xauthority` и перезайти в систему без перезагрузки. Перезагрузка до повторного входа в систему пересоздаст данный файл и проблема сохранится.

### SDDM запускается на tty1 вместо tty7

SDDM следует [конвенции systemd](http://0pointer.de/blog/projects/serial-console.html), в которой первая графическая сессия запускается на tty1\. Если вы предпочитаете старую конвенцию, в которой терминалы с первого по шестой зарезервированы для текстовых консолей, измените стандартное значение переменной `MinimumVT` в секции `[X11]`:

 `/etc/sddm.conf.d/tty.conf` 
```
[X11]
MinimumVT=7
```

### Один или более пользователей не отображаются на экране приветствия

**Важно:** Пользователи в меньшем или большем заданном диапазоном `UID`, как правило, не должны отображаться в [экранном менеджере](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)").

По умолчанию, SDDM отображает только тех пользователей, чей UID находится в диапазоне от 1000 до 65000\. Если UID нужных вам пользователей ниже данного значения, вам потребуется изменить этот диапазон. Например, для пользователя с UID равным 501 файл конфигурации будет выглядеть следующим образом:

 `/etc/sddm.conf.d/uid.conf` 
```
[Users]
HideShells=/sbin/nologin,/bin/false
# Скрытые пользователи. Это для того, если какие-либо системные пользователи попадают в ваш диапазон. Смотрите /etc/passwd в вашей системе.
HideUsers=git,sddm,systemd-journal-remote,systemd-journal-upload

# Максимальный user id для отображаемых пользователей
MaximumUid=65000

# Минимальный user id для отображаемых пользователей
MinimumUid=500 #Мой UID равен 501
```

### SDDM загружает только английскую (US) раскладку клавиатуры

SDDM загружает раскладку клавиатуры, заданную в файле `/etc/X11/xorg.conf.d/00-keyboard.conf`. Вы можете сгенерировать этот конфигурационный файл командой `localectl set-x11-keymap`. Смотрите [Keyboard configuration in Xorg (Русский)](/index.php/Keyboard_configuration_in_Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Keyboard configuration in Xorg (Русский)") для дополнительной информации.

Также SDDM может некорректно отображать раскладку как английскую, но моментально изменит её на правильную после начала ввода пароля [[3]](https://github.com/sddm/sddm/issues/202#issuecomment-76001543). Похоже, что это баг не SDDM, а [libxcb](https://www.archlinux.org/packages/?name=libxcb) (версии 1.13-1 по состоянию на 2018) [[4]](https://github.com/sddm/sddm/issues/202#issuecomment-133628462).

### Слишком низкое разрешение экрана

Проблема может быть вызвана использованием HiDPI с мониторами с повреждённой информацией [EDID](https://en.wikipedia.org/wiki/ru:Extended_display_identification_data "wikipedia:ru:Extended display identification data") [[5]](https://github.com/sddm/sddm/issues/692). Попробуйте отключить HiDPI, если он у вас [включён](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_HiDPI).

Если же решение выше не помогает, можно попробовать задать размер экрана в файле конфигурации Xorg. Например:

 `/etc/X11/xorg.conf.d/90-monitor.conf` 
```
Section "Monitor"
        Identifier      "<default monitor>"
        DisplaySize     345 194 # in millimeters
EndSection
```

### Долгая загрузка с домашней директорией на autofs

По умолчанию, SDDM пытается отобразить аватарки пользователей считывая файл `~/.face.icon`. Если ваша домашняя директория имеет тип файловой системы *autofs*, например, в случае использования [Dm-crypt (Русский)](/index.php/Dm-crypt_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Dm-crypt (Русский)"), придётся ждать 60 секунд, пока autofs не сообщит, что директория не может быть смонтирована.

Вы можете отключить отображение аватарок отредактировав `/etc/sddm.conf`:

 `/etc/sddm.conf` 
```
[Theme]
EnableAvatars=false
```