## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Использование libnotify](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_libnotify)
    *   [2.1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
        *   [2.2.1 Gnome](#Gnome)
        *   [2.2.2 Xfce4](#Xfce4)
*   [3 Советы и подсказки](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D0.BF.D0.BE.D0.B4.D1.81.D0.BA.D0.B0.D0.B7.D0.BA.D0.B8)

## Введение

**Libnotify** - это простой способ отображения уведомлений и информации в маленьком диалоговом окне. Он используется во многих программах с открытым исходным кодом, например [evolution](/index.php/Evolution "Evolution"), [pidgin](/index.php/Pidgin_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pidgin (Русский)") и т.д., и поддерживает как **Gtk+**, так и **Qt**. Кроме этого, **libnotify** не зависит от используемого оконного менеджера.

## Использование libnotify

### Установка

Для установки **libnotify** выполните команду:

```
pacman -S [libnotify](https://www.archlinux.org/packages/?name=libnotify)

```

### Настройка

Далее описывается, как настроить **libnotify** для работы с **Gnome** и **Xfce4**.

#### Gnome

Выполните

```
pacman -S [notification-daemon](https://www.archlinux.org/packages/?name=notification-daemon)

```

Установите также **gconf-editor**, если его у вас пока что нет:

```
pacman -S [gconf-editor](https://www.archlinux.org/packages/?name=gconf-editor)

```

Запустите **gconf-editor** и выберите `/apps/notification-daemon/`. Теперь вы можете настроить виджет уведомлений.

#### Xfce4

Выполните

```
pacman -S xfce4-notifyd
pacman -S xfconf 

```

Для выполнения настройки запустите

```
xfce4-notifyd-config

```

## Советы и подсказки

Вы можете легко отображать сообщения **libnotify** из программы на **python** или любом другом языке.

**Обратите внимание:** Вам понадобится обвязка **libnotify** для **python**:

```
pacman -S python-notify

```

Вот простой "hello world" пример на python:

```
#!/usr/bin/env python
import subprocess
info = "Hello world!"
subprocess.call(['notify-send', info])

```

```
#!/usr/bin/python
import subprocess
import commands    
# версия ядра
uname = commands.getoutput('uname -r')
head = "All the info about your system:"
msg = "Your kernel version: "+ uname +"\n"       
# отображение уведомления
subprocess.call(['notify-send', head, msg])

```

Вместо **python** вы можете использовать любимый **bash**:

```
# отправка уведомления "hello world"
notify-send "hello world"

```