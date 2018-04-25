Ссылки по теме

*   [Flatpak](/index.php/Flatpak "Flatpak")

[snapd](https://github.com/snapcore/snapd) это REST API демон для управления snap-пакетами ("snaps"). Пользователи могут взаимодействовать с ним с помощью *snap* клиента, входящего в тот же пакет.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
*   [3 Управление snap-пакетами](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_snap-.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B0.D0.BC.D0.B8)
    *   [3.1 Поиск](#.D0.9F.D0.BE.D0.B8.D1.81.D0.BA)
    *   [3.2 Установка пакетов](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [3.3 Обновление пакетов](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
    *   [3.4 Удаление пакетов](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2)
*   [4 Удаление](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
*   [5 Советы и рекомендации](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.80.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D0.B0.D1.86.D0.B8.D0.B8)
    *   [5.1 Classic snaps](#Classic_snaps)
*   [6 Помощь](#.D0.9F.D0.BE.D0.BC.D0.BE.D1.89.D1.8C)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [snapd](https://aur.archlinux.org/packages/snapd/) или его [git](/index.php/Git "Git") версию, [snapd-git](https://aur.archlinux.org/packages/snapd-git/).

В пакет входит `snapd` демон, а также *snap-confine*, который обеспечивает монтирование, изоляцию и запуск snap-пакетов.

**Tip:** `snapd` устанавливает скрипт в `/etc/profile.d/` для экспорта путей в исполняемым файлам, входящим в snap-пакеты. Для того чтобы эти изменения вступили в силу потребуется перезагрузка.

## Настройка

В пакет также входят несколько [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") unit файлов, которые обеспечивают возможность обновления всех установленных snap-пакетов, при выходе новой версии.

Для того чтобы `snapd` демон запускался, когда *snap* обращается к нему, запустите `snapd.socket`.

```
# systemctl start snapd.socket

```

Вы также можете активировать его при старте системы.

```
# systemctl enable snapd.socket

```

Для того чтобы автоматически обновлять пакеты активируйте `snapd.refresh.timer`:

```
# systemctl start snapd.refresh.timer

```

## Управление snap-пакетами

Для управления пакетами используется утилита *snap*.

### Поиск

Для поиска пакетов, доступных для установки используйте команду *find*:

```
$ snap find

```

Это выведет список всех доступных пакетов. Для поиска конкретного пакета используйте:

```
$ snap find *критерий_поиска*

```

### Установка пакетов

Установить snap-пакет можно с помощью команды:

```
# snap install *имя_пакета*

```

Установка требует root привилегий. Установка с правами пользователя на данный момент невозможна. При установке snap загружается в `/var/lib/snapd/snaps` и монтируется в `/snap/*имя_пакета*`.

Кроме того, создаются также юнит-файлы для каждого snap-пакета и добавляются в `/etc/systemd/system/multi-user.target.wants/`, для того чтобы snap-пакеты монтировались при каждом запуске системы. Вы можете просмотреть список установленных пакетов командой:

```
$ snap list

```

Вы также можете устанавливать snap-пакеты локально, с жесткого диска:

```
# snap install --devmode */path/to/snap*

```

### Обновление пакетов

Для того чтобы обновить snap-пакеты выполните:

```
# snap refresh

```

### Удаление пакетов

Для того чтобы удалить пакет выполните:

```
# snap remove *snapname*

```

## Удаление

Удаление пакета [snapd](https://aur.archlinux.org/packages/snapd/) не приводит к удалению всех каталогов и файлов, которые создаются при его использовании. Лучше всего удалить все snap-пакеты с помощью *snap remove*, перед тем как удалять сам пакет. Однако, на данный момент невозможно удалить snap-пакет *ubuntu-core*. Для того чтобы полностью удалить все файлы следуйте инструкции ниже.

1\. Отмонтируйте все активные snap-пакеты из `/snap`.

```
# umount $(mount | grep snap | awk '{print $3}')

```

2\. Удалите следующие каталоги:

```
# rm -rf /var/lib/snapd
# rm -rf /snap

```

3\. Удалите все файлы, отвечающие за монтирование snap-пакетов из `/var/lib/snapd/snaps` в `/snap` при загрузке.

```
# find /etc/systemd/system -name "snap-*.mount" -delete
# find /etc/systemd/system -name "snap.*.service" -delete
# find /etc/systemd/system/multi-user.target.wants -name "snap-*.mount" -delete
# find /etc/systemd/system/multi-user.target.wants -name "snap.*.service" -delete

```

## Советы и рекомендации

### Classic snaps

Some snaps (e.g. Skype and Pycharm) use classic confinement. However, classic confinement requires the `/snap` directory, which is not FHS-compliant. Therefore, the snapd package doesn't ship this directory. However, if the user wants to, he can manually create a symlink from `/snap` to `/var/lib/snapd/snap`, to allow the installation of classic snaps:

```
# ln -s /var/lib/snapd/snap /snap

```

## Помощь

Почтовая рассылка Arch Linux и другие официальные каналы поддержки Arch Linux не являются подходящим местом для запроса помощи по snap-пакетам на Arch Linux. Подходящим местом для запроса поддержки является [Snapcraft forum](https://forum.snapcraft.io).

## Смотрите также

*   [Official site](https://snapcraft.io/)
*   [GitHub repository](https://github.com/snapcore/snapd)
*   [arstechnica article](http://arstechnica.com/information-technology/2016/06/goodbye-apt-and-yum-ubuntus-snap-apps-are-coming-to-distros-everywhere/) (06/16) about Ubuntu snaps becoming available for Arch and other distros