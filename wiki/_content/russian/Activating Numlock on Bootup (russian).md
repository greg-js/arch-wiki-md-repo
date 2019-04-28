<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 TTY (Teletype) Консоль 1-6](#TTY_(Teletype)_Консоль_1-6)
*   [2 X.org](#X.org)
    *   [2.1 KDM](#KDM)
    *   [2.2 Пользователям KDE](#Пользователям_KDE)
    *   [2.3 GDM](#GDM)
    *   [2.4 SLiM](#SLiM)

## TTY (Teletype) Консоль 1-6

Для активации numlock при обычной загрузке в консоль TTY (tty1 -> tty6), добавьте следующую строку в `/etc/rc.local`:

```
for tty in /dev/tty?; do /usr/bin/setleds -D +num < "$tty"; done

```

примечание: Виртуальные Консоли vc/1 -> vc/6 были заменены на tty1 -> tty6 с 2009-08-02.

## X.org

Если Вы используете startx для запуска вашей сессии X, просто установите пакет numlockx и добавьте его в Ваш файл `~/.xinitrc`.

Установите `numlockx`:

```
# pacman -S numlockx

```

Добавьте в `~/.xinitrc` до `exec`:

```
#!/bin/sh
#
# ~/.xinitrc
#
# Executed by startx (run your window manager from here)
#

numlockx &

exec ваш_оконный_менеджер

```

### KDM

Если Вы используете для входа KDM добавьте :

```
numlockx on

```

в файл `/usr/share/config/kdm/Xsetup`, или в `/opt/kde/share/config/kdm/Xsetup`, если Вы используете KDM3.

Обратите внимание на то, что этот файл не входит в "зону внимания" pacman'a, поэтому при апгрейде системы может быть перезаписан без предупреждений или создания .pacnew-файла. Чтобы предотвратить это, добавьте в ваш `/etc/pacman.conf` следующую строку:

```
NoUpgrade = usr/share/config/kdm/Xsetup

```

Заметьте, что **/** в начале не ставится.

Стоит отметить, что все эти настойки дают возможность включить требуемую опцию только *после* загрузки. Для того же, чтобы включать NumLock еще "до" загрузки KDM, следует отредактировать `/usr/share/config/kdm/kdmrc`. Это - файл конфигурации KDM, все опции там выставлены по умолчанию и закомментированы. Нам нужно найти секцию, отвечающую за включение NumLock, снять комментарий и изменить значение опции:

```
NumLock = On

```

### Пользователям KDE

Можно добавить скрипт в директорию ~/.kde/Autostart:

```
$ nano ~/.kde/Autostart/numlockx

```

Добавляем:

```
#!/bin/sh
numlockx on

```

И разрешаем выполнять запуск:

```
$ chmod +x ~/.kde/Autostart/numlockx

```

**Примечание:** Есть также вариант включения numlock при запуске kde в kcontrol (kde3) и системных настройках (kde4). Но он на данный момент не работает, так как никто не берется починить эту ошибку (вроде как починили уже).

### GDM

Убедитесь, что пакет numlockx установлен. Теперь, добавьте следующий код в файл `/etc/gdm/Init/Default`:

```
if [ -x /usr/bin/numlockx ]; then
      /usr/bin/numlockx on
fi

```

### SLiM

В файле `/etc/slim.conf` найдите строку:

```
#numlock             on

```

и удалите символ комментария - "#".