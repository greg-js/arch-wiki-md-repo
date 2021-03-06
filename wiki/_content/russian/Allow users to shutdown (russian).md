<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 События нажатия кнопки питания и закрытия крышки ноутбука](#События_нажатия_кнопки_питания_и_закрытия_крышки_ноутбука)
*   [2 Используя systemd-logind](#Используя_systemd-logind)
*   [3 Используя sudo](#Используя_sudo)
    *   [3.1 Ограничение привилегий sudo](#Ограничение_привилегий_sudo)
*   [4 Создание псевдонимов](#Создание_псевдонимов)

## События нажатия кнопки питания и закрытия крышки ноутбука

События нажатия кнопок ждущего режима, выключения и режима гибернации, а также закрытия крышки ноутбука обрабатываются *logind*, как описано на странице [Power management#ACPI events](/index.php/Power_management#ACPI_events "Power management").

## Используя systemd-logind

Если вы используете [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") и установили [polkit](https://www.archlinux.org/packages/?name=polkit), пользователи через локальный сеанс могут вызывать команды управления режимами электропитания, пока сеанс [не будет нарушен](/index.php/General_troubleshooting_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Разрешения_сессии "General troubleshooting (Русский)").

Чтобы убедиться, что ваш сеанс активен, наберите:

```
$ loginctl show-session $XDG_SESSION_ID --property=Active

```

Пользователь может использоать команды *systemctl* в командной строке, или добавить их в меню окружения рабочего стола:

```
$ systemctl poweroff
$ systemctl reboot

```

Другие команды, такие как `systemctl suspend` и `systemctl hibernate` также могут быть использованы. Смотрите раздел *System Commands* в справочном руководстве [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1).

## Используя sudo

[Установите](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Установка_отдельных_пакетов "Pacman (Русский)") [sudo](https://www.archlinux.org/packages/?name=sudo) и [добавьте](/index.php/Sudo_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Примеры_настроек "Sudo (Русский)") текущего пользователя в список `sudoers`. После этого, текущий пользователь сможет вызывать *systemctl* через sudo из командной строки или меню окружения рабочего стола:

```
$ sudo systemctl poweroff
$ sudo systemctl reboot

```

Другие команды, такие как `systemctl suspend` и `systemctl hibernate` также могут быть использованы. Смотрите раздел *System Commands* в справочном руководстве [systemctl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/systemctl.1).

### Ограничение привилегий sudo

Если пользователю следует разрешить только, например, использовать команду выключения, добавьте следующее в конец файла `/etc/sudoers`, используя команду `visudo`:

```
*имя_пользователя* *название_хоста*=NOPASSWD: /usr/bin/systemctl poweroff,/usr/bin/systemctl halt,/usr/bin/systemctl reboot

```

Название хоста вы можете не указывать (или указать `localhost`). Теперь пользователь сможет выключить компьютер используя `sudo systemctl poweroff` или `sudo systemctl halt`, и перезагрузить его с помощью `sudo systemctl reboot` без ввода пароля. Удалите `NOPASSWD:`, если вы хотите, чтобы у пользователя запрашивался его пароль перед продолжением.

## Создание псевдонимов

Для удобства, вы можете добавить эти [псевдонимы](/index.php/Bash#Aliases "Bash") в пользовательский `~/.bashrc` или системный `/etc/bash.bashrc` файл инициализации командной оболочки:

```
alias reboot="sudo systemctl reboot"
alias poweroff="sudo systemctl poweroff"
alias halt="sudo systemctl halt"

```

То же самое вы можете сделать, установив [systemd-sysvcompat](https://www.archlinux.org/packages/?name=systemd-sysvcompat), который создаст символические ссылки на *systemctl* с соответствующими именами.