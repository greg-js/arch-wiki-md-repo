## Contents

*   [1 Введение](#Введение)
*   [2 Использование libnotify](#Использование_libnotify)
    *   [2.1 Установка](#Установка)
    *   [2.2 Настройка](#Настройка)
        *   [2.2.1 Gnome](#Gnome)
        *   [2.2.2 Xfce4](#Xfce4)
*   [3 Советы и подсказки](#Советы_и_подсказки)

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

**Примечание:** Вам понадобится обвязка **libnotify** для **python**:
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
msg = "Your kernel version: "+ uname +"
"       
# отображение уведомления
subprocess.call(['notify-send', head, msg])

```

Вместо **python** вы можете использовать любимый **bash**:

```
# отправка уведомления "hello world"
notify-send "hello world"

```