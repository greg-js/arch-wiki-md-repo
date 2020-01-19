Ссылки по теме

*   [Зеркала](/index.php/%D0%97%D0%B5%D1%80%D0%BA%D0%B0%D0%BB%D0%B0 "Зеркала")
*   [Pacman (Русский)](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")

[Reflector](http://xyne.archlinux.ca/projects/reflector/) — скрипт, который автоматизирует процесс настройки зеркал, включающий в себя загрузку свежего списка зеркал со страницы [Mirror Status](https://www.archlinux.org/mirrors/status/), фильтрацию из них наиболее обновленных, сортировку по скорости и сохранение в `/etc/pacman.d/mirrorlist`.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
    *   [2.1 Примеры](#Примеры)
        *   [2.1.1 Пример 1](#Пример_1)
        *   [2.1.2 Пример 2](#Пример_2)
        *   [2.1.3 Пример 3](#Пример_3)
*   [3 Автоматизация](#Автоматизация)
    *   [3.1 Pacman hook](#Pacman_hook)
    *   [3.2 Служба systemd](#Служба_systemd)
    *   [3.3 Таймер systemd](#Таймер_systemd)
    *   [3.4 Пакет Reflector-timer](#Пакет_Reflector-timer)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [reflector](https://www.archlinux.org/packages/?name=reflector), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Использование

**Важно:**

*   Обязательно сделайте резервную копию файла `/etc/pacman.d/mirrorlist`:

```
# cp -vf /etc/pacman.d/mirrorlist /etc/pacman.d/mirrorlist.backup

```

*   После обновления `/etc/pacman.d/mirrorlist`, взгляните на содержимое файла и убедитесь, что он не содержит подозрительных зеркал перед тем, как выполнять синхронизацию базы данных пакетов [pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)").

Чтобы увидеть список всех доступных опций, наберите

```
# reflector --help

```

### Примеры

#### Пример 1

Следующая команда отфильтрует пять зеркал с поддержкой https, отсортирует их по скорости и обновит файл mirrorlist:

```
# reflector --verbose -l 5 -p https --sort rate --save /etc/pacman.d/mirrorlist

```

#### Пример 2

Эта команда подробно выведет список 200 наиболее недавно обновленных HTTPS-зеркал, отсортирует их по скорости загрузки и обновит mirrorlist:

```
# reflector --verbose -l 200 -p https --sort rate --save /etc/pacman.d/mirrorlist

```

#### Пример 3

То же, что и в предыдущем примере, но будут взяты только зеркала, расположенные в Соединенных Штатах:

```
# reflector --verbose --country 'United States' -l 200 -p https --sort rate --save /etc/pacman.d/mirrorlist

```

## Автоматизация

### Pacman hook

Вы можете создать [хук pacman](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Хуки "Pacman (Русский)"), который будет запускать *reflector* и удалять файл *.pacnew* после каждого обновления [pacman-mirrorlist](https://www.archlinux.org/packages/?name=pacman-mirrorlist).

 `/etc/pacman.d/hooks/mirrorupgrade.hook` 
```
[Trigger]
Operation = Upgrade
Type = Package
Target = pacman-mirrorlist

[Action]
Description = Обновление списка зеркал с помощью reflector и удаление pacnew файла...
When = PostTransaction
Depends = reflector
Exec = /bin/sh -c "reflector --country 'United States' --protocol https --latest 10 --age 24 --sort rate --save /etc/pacman.d/mirrorlist;  rm -f /etc/pacman.d/mirrorlist.pacnew"

```

Удостоверьтесь, что подставили необходимые вам аргументы.

### Служба systemd

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

```

Теперь запуск `# systemctl start reflector` разово обновит ваш mirrorlist.

Для обновления списка зеркал при каждой загрузке системы, используйте следующий файл юнита:

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update
Requires=network.target
After=network.target

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol https --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

[Install]
RequiredBy=network.target

```

И [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `reflector.service`.

Для того, чтобы она работала, цель `network.target` должна правильно означать, что установлено интернет-соединение.

### Таймер systemd

Если вы хотите запускать `reflector.service`, скажем, раз в неделю:

 `/etc/systemd/system/reflector.timer` 
```
[Unit]
Description=Run reflector weekly

[Timer]
OnCalendar=weekly
AccuracySec=12h
Persistent=true

[Install]
WantedBy=timers.target

```

Сохраните файл и [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") таймер:

```
# systemctl enable reflector.timer

```

### Пакет Reflector-timer

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [reflector-timer](https://aur.archlinux.org/packages/reflector-timer/), который будет запускать *reflector* раз в неделю.

Настройки по умолчанию, которые могут быть изменены под нужды пользователя:

 `/usr/share/reflector-timer/reflector.conf` 
```
AGE=6
COUNTRY='United States'
LATEST=30
NUMBER=20
SORT=rate
### Удалите те протоколы, которые не хотите использовать
PROTOCOL1='-p http'
PROTOCOL2='-p https'
PROTOCOL3='-p ftp'
PROTOCOL4='-p rsync'
```

Затем [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") таймер `reflector.timer`.