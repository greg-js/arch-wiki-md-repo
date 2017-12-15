Ссылки по теме

*   [Ремастеринг установочного ISO-образа](/index.php/%D0%A0%D0%B5%D0%BC%D0%B0%D1%81%D1%82%D0%B5%D1%80%D0%B8%D0%BD%D0%B3_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BE%D1%87%D0%BD%D0%BE%D0%B3%D0%BE_ISO-%D0%BE%D0%B1%D1%80%D0%B0%D0%B7%D0%B0 "Ремастеринг установочного ISO-образа")
*   [PXE (Русский)](/index.php/PXE_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "PXE (Русский)")
*   [Archboot (Русский)](/index.php/Archboot_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Archboot (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Archiso](/index.php/Archiso "Archiso"). Дата последней синхронизации: 24 ноября 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Archiso&diff=0&oldid=498359).

**Archiso** - набор bash скриптов, предназначенных для создания полностью функциональных Live-CD/DVD и Live-USB на базе Arch Linux. Это тот же инструмент, который используется для создания официальных образов, но поскольку он довольно гибкий инструмент, который может быть использован как для создания дисков восстановления или установочных, так и для специализированных live-CD/DVD/USB систем. Центр Archiso - *mkarchiso*. Для получения подробного описания всех его опций достаточно вызвать его без параметров, так что здесь будет описанно только создание live диска своими руками.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка Live носителя](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Live_.D0.BD.D0.BE.D1.81.D0.B8.D1.82.D0.B5.D0.BB.D1.8F)
    *   [2.1 Установка пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
        *   [2.1.1 Пользовательский локальный репозиторий](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D0.B9_.D0.BB.D0.BE.D0.BA.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B9_.D1.80.D0.B5.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BE.D1.80.D0.B8.D0.B9)
        *   [2.1.2 Предотвращение установки пакетов, принадлежащих базовой группе](#.D0.9F.D1.80.D0.B5.D0.B4.D0.BE.D1.82.D0.B2.D1.80.D0.B0.D1.89.D0.B5.D0.BD.D0.B8.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2.2C_.D0.BF.D1.80.D0.B8.D0.BD.D0.B0.D0.B4.D0.BB.D0.B5.D0.B6.D0.B0.D1.89.D0.B8.D1.85_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D0.BE.D0.B9_.D0.B3.D1.80.D1.83.D0.BF.D0.BF.D0.B5)
        *   [2.1.3 Установка пакетов из multilib](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2_.D0.B8.D0.B7_multilib)
    *   [2.2 Добавление файлов в образ](#.D0.94.D0.BE.D0.B1.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.B2_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7)
    *   [2.3 Загрузчик](#.D0.97.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D1.87.D0.B8.D0.BA)
    *   [2.4 Вход в систему](#.D0.92.D1.85.D0.BE.D0.B4_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [2.5 Изменение автоматического входа в систему](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
*   [3 Создание ISO](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_ISO)
    *   [3.1 Пересоздание ISO](#.D0.9F.D0.B5.D1.80.D0.B5.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_ISO)
*   [4 Использование ISO](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_ISO)
*   [5 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.1 Установка без подключения к Интернету](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B1.D0.B5.D0.B7_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BA_.D0.98.D0.BD.D1.82.D0.B5.D1.80.D0.BD.D0.B5.D1.82.D1.83)
        *   [5.1.1 Установка archiso в новый корень](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_archiso_.D0.B2_.D0.BD.D0.BE.D0.B2.D1.8B.D0.B9_.D0.BA.D0.BE.D1.80.D0.B5.D0.BD.D1.8C)
        *   [5.1.2 Chroot и настройка базовой системы](#Chroot_.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B1.D0.B0.D0.B7.D0.BE.D0.B2.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
            *   [5.1.2.1 Восстановление конфигурации журнала](#.D0.92.D0.BE.D1.81.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D0.B6.D1.83.D1.80.D0.BD.D0.B0.D0.BB.D0.B0)
            *   [5.1.2.2 Удаление особых правил udev](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.81.D0.BE.D0.B1.D1.8B.D1.85_.D0.BF.D1.80.D0.B0.D0.B2.D0.B8.D0.BB_udev)
            *   [5.1.2.3 Отключение и удаление служб, созданных archiso](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B8_.D1.83.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BB.D1.83.D0.B6.D0.B1.2C_.D1.81.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_archiso)
            *   [5.1.2.4 Удаление особых скриптов Live среды](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BE.D1.81.D0.BE.D0.B1.D1.8B.D1.85_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.BE.D0.B2_Live_.D1.81.D1.80.D0.B5.D0.B4.D1.8B)
            *   [5.1.2.5 Импорт ключей archlinux](#.D0.98.D0.BC.D0.BF.D0.BE.D1.80.D1.82_.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.B9_archlinux)
            *   [5.1.2.6 Настройка системы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
            *   [5.1.2.7 Включение графического входа (Опционально)](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.28.D0.9E.D0.BF.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.29)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)
    *   [6.1 Документация и учебные пособия](#.D0.94.D0.BE.D0.BA.D1.83.D0.BC.D0.B5.D0.BD.D1.82.D0.B0.D1.86.D0.B8.D1.8F_.D0.B8_.D1.83.D1.87.D0.B5.D0.B1.D0.BD.D1.8B.D0.B5_.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D0.B8.D1.8F)
    *   [6.2 Примеры шаблонов настройки](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D1.88.D0.B0.D0.B1.D0.BB.D0.BE.D0.BD.D0.BE.D0.B2_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)

## Установка

**Примечание:**

*   Чтобы использовать Archiso, вы должны работать на платформе x86_64[[1]](https://projects.archlinux.org/archiso.git/tree/docs/README.build#n67). В противном случае, скорее всего, возможны проблемы, решение которых будет рассмотрено дальше.
*   Рекомендуется действовать под суперпользователем на всех последующих этапах. В противном случае, скорее всего, возможны проблемы, с ложными разрешениями позже.

Для начала нужно установить пакет [archiso](https://www.archlinux.org/packages/?name=archiso) или [archiso-git](https://aur.archlinux.org/packages/archiso-git/).

Archiso поставляется с двумя "профилями": *releng* и *baseline*.

*   Если вы хотите создать полностью индивидуальную версию Arch Linux, предварительно установленной со всеми вашими любимыми программами и конфигурациями, используйте профиль *releng*.
*   Если вы просто хотите создать оптимальную для существования, без предварительно установленных пакетов и минимальной конфигурацией, используйте *baseline*.

Теперь скопируйте профиль на Ваш выбор, в каталог, в котором вы можете вносить корректировки (мы будем использовать `~/archlive`). Выполните следующую команду, заменив `**profile**` на `releng` или `baseline`.

```
# cp -r /usr/share/archiso/configs/**profile**/* *archlive*

```

*   Если вы используете `releng` профиль, создавая полностью индивидуальный образ, вы можете переходить к [настройке Live носителя](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Live_.D0.BD.D0.BE.D1.81.D0.B8.D1.82.D0.B5.D0.BB.D1.8F).
*   Если вы используете `baseline` профиль для создания голого образа, у вас не будет времени на настройку и можно переходить к [созданию ISO](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_ISO).

## Настройка Live носителя

В этом разделе подробно описывается настройка создаваемого вами образа, определение пакетов и конфигурации, которые вы хотите, чтобы ваш live image содержал.

Внутри каталога `*archlive*`, созданного в [#Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0), есть ряд файлов и каталогов; мы рассмотрим лишь несколько из них, в основном:

*   `packages.*` - это где вы перечисляете построчно пакеты, которые вы хотите установить, и
*   `airootfs` каталог - это каталог выступает в качестве оверлея, это где вы делаете все настройки.

Как правило, любые административные задачи, которые вы обычно делаете после новой установки, могут быть выполнены в скрипте `*archlive*/airootfs/root/customize_airootfs.sh`, за исключением установки пакетов. Скрипт должен быть написан с точки зрения новой среды, поэтому `/` в скрипте означает корень ISO-образа, который создается.

### Установка пакетов

[Отредактируйте](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A0.D0.B5.D0.B4.D0.B0.D0.BA.D1.82.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.B5.D0.B4.D0.BE.D1.81.D1.82.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B0.D0.BC.D0.B8_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)") списки пакетов в `packages.i686`, `packages.x86_64` или `packages.both` чтобы указать, какие пакеты должны быть установлены на live носителе. Суффикс здесь указывает, в какой архитектуре доступны пакеты.

**Примечание:** Если вы хотите использовать [оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер") в Live CD, то вы должны добавить необходимые и правильные [видео драйвера](/index.php/Video_drivers "Video drivers"), или WM может зависнуть при загрузке.

#### Пользовательский локальный репозиторий

Вы также можете [создать пользовательский локальный репозиторий](/index.php/Custom_local_repository "Custom local repository") в целях подготовки пакетов из [AUR](/index.php/AUR "AUR") или [ABS](/index.php/ABS "ABS"). При этом пакеты для обеих архитектур, должны следовать в определенном порядке каталогов, чтобы не столкнуться с проблемами.

Например:

*   `~/customrepo`
    *   `~/customrepo/x86_64`
        *   `~/customrepo/x86_64/foo-x86_64.pkg.tar.xz`
        *   `~/customrepo/x86_64/customrepo.db.tar.gz`
        *   `~/customrepo/x86_64/customrepo.db` (symlink created by `repo-add`)
    *   `~/customrepo/i686`
        *   `~/customrepo/i686/foo-i686.pkg.tar.xz`
        *   `~/customrepo/i686/customrepo.db.tar.gz`
        *   `~/customrepo/i686/customrepo.db` (symlink created by `repo-add`)

Затем вы можете добавить ваш репозиторий внеся изменения в файле `~/archlive/pacman.conf`, поставив его над другой записью репозитория (для более высшего приоритета):

```
# пользовательский репозиторий
[customrepo]
SigLevel = Optional TrustAll
Server = file:///home/**user**/customrepo/$arch

```

Таким образом, скрипты сборки просто ищут соответствующие пакеты.

Если это не так, вы столкнетесь с сообщениями об ошибках, подобными этому:

```
error: failed to prepare transaction (package architecture is not valid)
:: package foo-i686 does not have a valid architecture

```

#### Предотвращение установки пакетов, принадлежащих базовой группе

По умолчанию `/usr/bin/mkarchiso`, скрипт, который используется `~/archlive/build.sh`, вызывает один из [arch-install-scripts](https://www.archlinux.org/packages/?name=arch-install-scripts) с именем `pacstrap` без флага `-i`, что заставляет [Pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") не ждать ввода пользователя во время процесса установки.

При внесении в черный список базовых групповых пакетов путем добавления их в строку `IgnorePkg` в файле `~/archlive/pacman.conf`, [Pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)") спрашивает, должны ли они все еще быть установлены, а это значит, что при входе пользователя пропускаются. Чтобы избавиться от этих пакетов существует несколько вариантов:

*   **"Грязный" способ**: добавьте флаг `-i` в каждую строку, вызывающую `pacstrap` в `/usr/bin/mkarchiso`.

*   **"Чистый"**: Создайте копию `/usr/bin/mkarchiso` , в которую вы добавляете флаг и адаптируете `~/archlive/build.sh`, так чтобы он вызывал измененную версию скрипта mkarchiso.

*   **Расширенный способ**: создайте функцию для `~/archlive/build.sh`, которая явно удаляет пакеты после базовой установки. Это принесет вам удовольствие от того, что не приходится столько вводить во время процесса установки.

#### Установка пакетов из multilib

Чтобы установить пакеты из репозитория [multilib](/index.php/Multilib_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Multilib (Русский)"), вам необходимо создать два файла конфигурации pacman: один для x86_64 и другой для i686\. Скопируйте файл `pacman.conf` в `pacmanx86_64.conf` и `pacmani686.conf`. Раскомментируйте следующие строки, чтобы включить *multilib* в `pacmanx86_64.conf`:

 `pacmanx86_64.conf` 
```
[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
```

Затем отредактируйте файл `build.sh` с помощью редактора. Замените следующие строки:

 `build.sh` 
```
run_once make_pacman_conf

# сделать все вещи для каждого airootfs
for arch in i686 x86_64; do
    run_once make_basefs
    run_once make_packages
done

run_once make_packages_efi

for arch in i686 x86_64; do
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

```

with:

 `build.sh` 
```
cp -v releng/pacmanx86_64.conf releng/pacman.conf
run_once make_pacman_conf

# сделать все вещи для каждого airootfs
for arch in x86_64; do
    run_once make_basefs
    run_once make_packages
    run_once make_packages_efi
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

echo make_pacman_conf i686
cp -v releng/pacmani686.conf releng/pacman.conf
cp -v releng/pacmani686.conf ${work_dir}/pacman.conf

for arch in i686; do
    run_once make_basefs
    run_once make_packages
    run_once make_packages_efi
    run_once make_setup_mkinitcpio
    run_once make_customize_airootfs
done

```

Таким образом, пакеты для x86_64 и i686 будут установлены со своим собственным конфигурационным файлом pacman.

### Добавление файлов в образ

**Примечание:** Для этого вы должны быть суперпользователем, не изменяйте права собственности на какой-либо из файлов, которые вы копируете, **все** в каталоге airootfs должно принадлежать суперпользователю. Соответствующие владельцы будут отсортированы в ближайшее время.

Каталог airootfs действует как оверлей, считая его корневым каталогом '/' в вашей текущей системе, поэтому любые файлы, которые вы размещаете в этом каталоге, будут скопированы при загрузке.

Поэтому, если у вас есть набор скриптов iptables в вашей текущей системе, которые вы хотите использовать на вашем live образey, скопируйте их как таковые:

```
# cp -r /etc/iptables ~/archlive/airootfs/etc

```

Размещение файлов в домашнем каталоге пользователей немного отличается. Не помещайте их в `airootfs/home`, но вместо этого создайте каталог skel внутри `airootfs/` и разместите их там. Затем мы добавим соответствующие команды в `customize_airootfs.sh`, которые мы собираемся использовать для их копирования при загрузке и выяснять разрешения.

Сначала создайте каталог skel:

```
# mkdir ~/archlive/airootfs/etc/skel

```

Теперь скопируйте 'home' файлы в каталог skel, например для `.bashrc`:

```
# cp ~/.bashrc ~/archlive/airootfs/etc/skel/

```

Когда выполняется `~/archlive/airootfs/root/customize_airootfs.sh`, и создается новый пользователь, файлы из каталога skel будут автоматически скопированы в новую домашнюю папку, а разрешения будут установлены правильно.

Аналогичным образом, требуется обратить внимание на особые файлы конфигурации, которые находятся где-то внизу по иерархии. В качестве примера конфигурационный файл `/etc/X11/xinit/xinitrc` находится на пути, который может быть перезаписан путем установки пакета. Чтобы поместить файл конфигурации, следует поместить пользовательский `xinitrc` в `~/archlive/airootfs/etc/skel/`, а затем изменить `customize_airootfs.sh`, чтобы переместить его соответствующим образом.

### Загрузчик

Файл по умолчанию должен работать нормально, поэтому вам не нужно прикасаться к нему.

Из-за модульной природы isolinux вы можете использовать множество дополнений, так как все *.c32 файлы копируются и доступны вам. Взгляните на [официальный сайт syslinux](http://syslinux.zytor.com/wiki/index.php/SYSLINUX) и на [archiso git repo](https://projects.archlinux.org/archiso.git/tree/configs/syslinux-iso/boot-files). Используя указанные аддоны, можно сделать визуально привлекательные и сложные меню. Смотрите [здесь](http://syslinux.zytor.com/wiki/index.php/Comboot/menu.c32).

### Вход в систему

Запуск X при загрузке выполняется путем включения службы [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") менеджера входа в систему. Если вы знаете, какой файл .service нуждается в программной ссылке: Отлично. Если нет, то вы можете легко узнать в случае, если вы используете одну и ту же программу в системе, в которой вы строите свой iso. Просто используйте:

```
$ ls -l /etc/systemd/system/display-manager.service

```

Теперь создайте ту же самую программную ссылку в `~/archlive/airootfs/etc/systemd/system`. Для LXDM:

```
# ln -s /usr/lib/systemd/system/lxdm.service ~/archlive/airootfs/etc/systemd/system/display-manager.service

```

Это позволит запустить LXDM при загрузке системы в вашей live системе.

В качестве альтернативы вы можете просто включить службу в `airootfs/root/customize_airootfs.sh` вместе с другими службами, которые там включены.

Если вы хотите, чтобы графическая среда фактически запускалась автоматически во время загрузки, обязательно отредактируйте `airootfs/root/customize_airootfs.sh` и замените

```
systemctl set-default multi-user.target

```

на

```
systemctl set-default graphical.target

```

### Изменение автоматического входа в систему

Конфигурация автоматического входа в систему getty находится по адресу `airootfs/etc/systemd/system/getty@tty1.service.d/autologin.conf`.

Вы можете отредактировать этот файл для изменения автоматического входа пользователя в систему:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty --autologin **isouser** --noclear %I 38400 linux

```

Или удалите его, чтобы отключить автоматический вход в систему.

## Создание ISO

Теперь вы готовы превратить ваши файлы в .iso, которые вы можете записать на CD или USB:

Сначала создайте каталог `out/`,

```
# mkdir ~/archlive/out/

```

Затем внутри `~/archlive` выполнить:

```
# ./build.sh -v

```

Теперь скрипт загрузит и установит пакеты, которые вы указали в `work/*/airootfs`, создайте ядро и запустите образы, примените свои настройки и, наконец, создайте iso в `out/`.

### Пересоздание ISO

Восстановление iso после модификаций официально не поддерживается. Однако это легко осуществить, применив два шага. Сначала вам нужно удалить файлы блокировки в рабочем каталоге:

```
# rm -v work/build.make_*

```

Кроме того, требуется отредактировать скрипт `airootfs/root/customize_airootfs.sh`, и добавить команду `id` в начале строки `useradd`, как показано здесь. В противном случае восстановление останавливается в этот момент, потому что пользователь, который должен быть добавлен, уже существует [[2]](https://bugs.archlinux.org/task/41865).

```
! id arch && useradd -m -p "" -g users -G "adm,audio,floppy,log,network,rfkill,scanner,storage,optical,power,wheel" -s /usr/bin/zsh arch

```

Также удалите постоянные данные, например созданные пользователями или символические ссылки, такие как `/etc/sudoers`.

Пересоздание можно немного ускорить, отредактировав скрипт pacstrap (расположенный в /bin/pacstrap) и изменив следующее в строке 361:

До:

```
if ! pacman -r "$newroot" -Sy "${pacman_args[@]}"; then

```

После:

```
if ! pacman -r "$newroot" -Sy --needed "${pacman_args[@]}"; then

```

Это увеличивает скорость первоначальной загрузки,так как не нужно загружать и устанавливать какие-либо из базовых пакетов, которые уже установлены.

## Использование ISO

Смотрите раздел [Category:Getting and installing Arch (Русский)#Способы установки](/index.php/Category:Getting_and_installing_Arch_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.BF.D0.BE.D1.81.D0.BE.D0.B1.D1.8B_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8 "Category:Getting and installing Arch (Русский)") для различных параметров.

## Советы и хитрости

### Установка без подключения к Интернету

Если вы хотите установить archiso (например, [официальный ежемесячный выпуск](https://www.archlinux.org/download/)) без подключения к Интернету, или, если вы не хотите загружать пакеты снова:

Сначала следуйте инструкциям [руководства по установке](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Installation guide (Русский)"), а потом пропусктите разделы с [Соединение с Интернетом](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A1.D0.BE.D0.B5.D0.B4.D0.B8.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81_.D0.98.D0.BD.D1.82.D0.B5.D1.80.D0.BD.D0.B5.D1.82.D0.BE.D0.BC "Installation guide (Русский)") до раздела [Установка основных пакетов](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Installation guide (Русский)").

#### Установка archiso в новый корень

Вместо того, чтобы устанавливать пакеты с помощью `pacstrap` (которые будут пытаться загрузить из удаленных репозиториев), скопируйте *все* в live среду в новый корень:

```
# time cp -ax / /mnt

```

**Примечание:** Опция (`-x`) исключает некоторые специальные каталоги, так как они не должны копироваться в новый корень.

Затем скопируйте образ ядра в новый корень, чтобы сохранить целостность новой системы:

```
# cp -vaT /run/archiso/bootmnt/arch/boot/$(uname -m)/vmlinuz /mnt/boot/vmlinuz-linux

```

После этого сгенерируйте fstab, как описано в [руководстве по установке#Fstab](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Fstab "Installation guide (Русский)").

#### Chroot и настройка базовой системы

Далее, сделать операцию chroot в вашей вновь установленной системы:

```
# arch-chroot /mnt /bin/bash

```

**Примечание:** Перед выполнением других шагов [руководства по установке#Настройка системы](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B "Installation guide (Русский)") (например, локаль, раскладка клавиатуры и т.д.) необходимо избавиться от следов Live среды (другими словами, настройка archiso, которая не соответствует Live среде).

##### Восстановление конфигурации журнала

[Эта настройка archiso](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/root/customize_airootfs.sh#n19) приведет к сохранению системного журнала в ОЗУ, а это означает, что журнал после перезагрузки будет недоступен:

```
# sed -i 's/Storage=volatile/#Storage=auto/' /etc/systemd/journald.conf

```

##### Удаление особых правил udev

[Это правило udev](https://projects.archlinux.org/archiso.git/tree/configs/releng/airootfs/etc/udev/rules.d/81-dhcpcd.rules) автоматически запускает dhcpcd, если есть какие-либо проводные сетевые интерфейсы.

```
# rm /etc/udev/rules.d/81-dhcpcd.rules

```

##### Отключение и удаление служб, созданных archiso

Некоторые служебные файлы создаются для Live среды, отключите службы и удалите файл, поскольку они не нужны для новой системы:

```
# systemctl disable pacman-init.service choose-mirror.service
# rm -r /etc/systemd/system/{choose-mirror.service,pacman-init.service,etc-pacman.d-gnupg.mount,getty@tty1.service.d}
# rm /etc/systemd/scripts/choose-mirror

```

##### Удаление особых скриптов Live среды

Есть некоторые скрипты, которые установлены в live системе скриптами archiso, которые не нужны для новой системы:

```
# rm /etc/systemd/system/getty@tty1.service.d/autologin.conf
# rm /root/{.automated_script.sh,.zlogin}
# rm /etc/mkinitcpio-archiso.conf
# rm -r /etc/initcpio

```

##### Импорт ключей archlinux

Чтобы использовать официальные репозитории, нам нужно импортировать главные ключи archlinux ([pacman/Package signing (Русский)#Инициализация связки ключей](/index.php/Pacman/Package_signing_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D0.BD.D0.B8.D1.86.D0.B8.D0.B0.D0.BB.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F_.D1.81.D0.B2.D1.8F.D0.B7.D0.BA.D0.B8_.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.B9 "Pacman/Package signing (Русский)")). Этот шаг обычно делается с помощью pacstrap, но может быть достигнут с помощью

```
# pacman-key --init
# pacman-key --populate archlinux

```

**Примечание:** Клавиатура или мышь должны быть подключенными для генерации энтропии и ускорения первого шага

##### Настройка системы

Теперь вы можете выполнить пропущенные шаги раздела [руководства по установке#Настройка системы](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B "Installation guide (Русский)") (установка локали, часовой пояс, имя хоста и т.д.) и завершить установку, создав исходный ramdisk, как описано в [руководстве по установке#Initramfs](/index.php/Installation_guide_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Initramfs "Installation guide (Русский)").

##### Включение графического входа (Опционально)

Если вы используете менеджер входа, такой как GDM, вы можете изменить параметр по умолчанию systemd multi-user.target на тот, который позволяет графический вход в систему.

```
# systemctl disable multi-user.target
# systemctl enable graphical.target

```

## Смотрите также

### Документация и учебные пособия

*   [Страница проекта Archiso](https://projects.archlinux.org/archiso.git)
*   [Official Официальная документация](https://projects.archlinux.org/archiso.git/tree/docs)

### Примеры шаблонов настройки

*   [Live DJ дистрибутив, основанный на ArchLinux и созданный с помощью Archiso](http://easy.open.and.free.fr/didjix/)