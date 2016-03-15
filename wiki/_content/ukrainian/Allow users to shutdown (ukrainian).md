Якщо ви хочете дати користувачеві дати можливість вимикати і перезавантажувати систему, ви повинні змінити права (permissions) на команду `halt`. `reboot` - це символічне посилання (symlink) на `halt`, тому з цією командою нічого робити не треба. Виконайте від імені *root*

```
chmod +s /sbin/halt

```

**Тема на форумі:** [https://bbs.archlinux.org/viewtopic.php?t=2787](https://bbs.archlinux.org/viewtopic.php?t=2787)

* * *

Інший варіант реалізації - через `sudo`. Спочатку встановіть `sudo`:

```
# pacman -S sudo

```

Тоді, як *root*, додайте наступні рядки в кінець `/etc/sudoers` використовуючи команду `visudo`. Замініть *user* на ім'я користувача і *hostname* на ім'я хоста (прописане в `/etc/rc.conf` в секції `HOSTNAME`).

```
user hostname = NOPASSWD: /sbin/shutdown -h now
user hostname = NOPASSWD: /sbin/reboot

```

Тепер користувач може вимкнути систему командою `sudo shutdown -h now`, і перезавантажити `sudo reboot`.

Для XFCE потрібно модифікувати `/etc/sudoers`. Для всіх користувачів:

```
%users hostname=NOPASSWD:/usr/lib/xfce4/xfsm-shutdown-helper

```

Для певного користувача:

```
user hostname=NOPASSWD:/usr/lib/xfce4/xfsm-shutdown-helper

```

Це активує опції "Перезавантаження" та "Вимкнення" в діалозі виходу з системи менеджера сесій XFCE.