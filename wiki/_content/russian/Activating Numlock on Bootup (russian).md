**Состояние перевода:** На этой странице представлен перевод статьи [Activating Numlock on Bootup](/index.php/Activating_Numlock_on_Bootup "Activating Numlock on Bootup"). Дата последней синхронизации: 13 сентября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Activating_Numlock_on_Bootup&diff=0&oldid=582086).

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Консоль](#Консоль)
    *   [1.1 Отдельная служба](#Отдельная_служба)
    *   [1.2 Расширение getty@.service](#Расширение_getty@.service)
    *   [1.3 Bash](#Bash)
*   [2 X.org](#X.org)
    *   [2.1 startx](#startx)
    *   [2.2 MATE](#MATE)
    *   [2.3 KDE Plasma](#KDE_Plasma)
    *   [2.4 GDM](#GDM)
    *   [2.5 GNOME](#GNOME)
    *   [2.6 Xfce](#Xfce)
    *   [2.7 SDDM](#SDDM)
    *   [2.8 SLiM](#SLiM)
    *   [2.9 OpenBox](#OpenBox)
    *   [2.10 LightDM](#LightDM)
    *   [2.11 LXDM](#LXDM)
    *   [2.12 LXQt](#LXQt)

## Консоль

### Отдельная служба

**Совет:** Данные шаги можно автоматизировать, [установив](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [systemd-numlockontty](https://aur.archlinux.org/packages/systemd-numlockontty/) и [включив](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `numLockOnTty`.

Для начала создайте скрипт включения Num Lock в необходимых TTY:

 `/usr/local/bin/numlock` 
```
#!/bin/bash

for tty in /dev/tty{1..6}
do
    /usr/bin/setleds -D +num < "$tty";
done

```

Затем создайте и [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу systemd:

 `/etc/systemd/system/numlock.service` 
```
[Unit]
Description=numlock

[Service]
ExecStart=/usr/local/bin/numlock
StandardInput=tty
RemainAfterExit=yes

[Install]
WantedBy=multi-user.target
```

### Расширение getty@.service

Это более простой способ, так как в нём не используется отдельная служба и не привязываются номера определённых виртуальных терминалов. Создайте [drop-in сниппет](/index.php/Drop-in_%D1%81%D0%BD%D0%B8%D0%BF%D0%BF%D0%B5%D1%82 "Drop-in сниппет") для `getty@.service`, который будет применяться поверх оригинальной службы:

 `/etc/systemd/system/getty@.service.d/activate-numlock.conf` 
```
[Service]
ExecStartPre=/bin/sh -c 'setleds -D +num < /dev/%I'
```

**Примечание:** В случае каких-либо проблем, замените `ExecStartPre` на `ExecStartPost` и/или отключите подсказку, как описано ниже.

Чтобы отключить подсказку активации Num Lock на экране входа, [отредактируйте](/index.php/%D0%9E%D1%82%D1%80%D0%B5%D0%B4%D0%B0%D0%BA%D1%82%D0%B8%D1%80%D1%83%D0%B9%D1%82%D0%B5 "Отредактируйте") `getty@tty1.service` и добавьте `--nohints` к аргументам *agetty*:

```
[Service]
ExecStart=
ExecStart=-/sbin/agetty '-p -- \\u' --nohints --noclear %I $TERM

```

### Bash

Добавьте `setleds -D +num` в `~/.bash_profile`. Заметьте, что в отличие от других методов, изменения не вступят в силу до входа в аккаунт.

## X.org

### startx

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [numlockx](https://www.archlinux.org/packages/?name=numlockx) и добавьте его в файл `~/.xinitrc` перед `exec`:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

numlockx &

exec оконный_менеджер

```

### MATE

По умолчанию MATE сохраняет последнее состояние перед выходом и восстанавливает его при следующем входе. Чтобы включать Num Lock при каждом входе, измените следующие значения DCONF:

```
dconf write org.mate.peripherals-keyboard remember-numlock-state false
dconf write org.mate.peripherals-keyboard numlock-state 'on'

```

### KDE Plasma

Перейдите в *Параметры системы > Устройства ввода > Клавиатура* и выберите необходимое поведение Num Lock в секции *Режим NumLock при запуске Plasma*.

### GDM

**Примечание:** GDM больше не выполняет скрипты из `/etc/gdm/Init`.

Убедитесь, что пакет [numlockx](https://www.archlinux.org/packages/?name=numlockx) установлен, а затем добавьте следующий код в файл [~/.xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)"):

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### GNOME

Если вы не используете экранный менеджер GDM, numlockx можно запускать при загрузке GNOME.

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [numlockx](https://www.archlinux.org/packages/?name=numlockx), а затем добавьте команду запуска `numlockx`.

```
$ gnome-session-properties

```

Данная команда откроет приложение **Startup Applications Preferences**. Нажмите на ***Add*** и введите следующее:

| Name: | *Numlockx* |
| Command: | */usr/bin/numlockx on* |
| Comment: | *Turns on numlock.* |

**Примечание:** Это не общесистемная настройка, соответственно данную процедуру необходимо повторить для каждого пользователя, которому необходимо включать Num Lock после входа.

### Xfce

Убедитесь, что следующим параметрам задано значение `true` в файле `~/.config/xfce4/xfconf/xfce-perchannel-xml/keyboards.xml`:

```
<property name="Numlock" type="bool" value="true"/>
<property name="RestoreNumlock" type="bool" value="true"/>

```

**Примечание:** Если файл не существует, откройте *Настройки > Клавиатура*, а затем проверьте и снимите галочку с опции `Restore num lock state on startup`, что создаст файл `keyboards.xml`.

### SDDM

Задайте параметру *Numlock* значение *on* в секции `[General]` файла `/etc/sddm.conf`:

```
[General]
...
Numlock=on

```

### SLiM

Найдите следующую строку в файле `/etc/slim.conf` и раскомментируйте её (уберите символ `#`):

```
#numlock             on

```

### OpenBox

Добавьте следующую строку в файл `~/.config/openbox/autostart`:

```
numlockx &

```

А затем сохраните файл.

### LightDM

См. раздел [LightDM (Русский)#NumLock включен по умолчанию](/index.php/LightDM_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#NumLock_включен_по_умолчанию "LightDM (Русский)").

### LXDM

Задайте следующий параметр в файле `/etc/lxdm/lxdm.conf`:

```
numlock=1

```

### LXQt

Задайте следующий параметр в файле `~/.config/lxqt/session.conf`:

```
[Keyboard]
numlock=true

```