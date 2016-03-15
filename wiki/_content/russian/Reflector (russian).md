[Reflector](http://xyne.archlinux.ca/projects/reflector/) — скрипт, который автоматизирует процесс настройки зеркал, включающий в себя загрузку свежего списка зеркал со страницы [Mirror Status](https://www.archlinux.org/mirrors/status/), фильтрацию из них наиболее обновленных, сортировку по скорости и сохранение в `/etc/pacman.d/mirrorlist`.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
    *   [2.1 Примеры](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B)
        *   [2.1.1 Пример 1](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_1)
        *   [2.1.2 Пример 2](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_2)
        *   [2.1.3 Пример 3](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80_3)
        *   [2.1.4 Служба systemd](#.D0.A1.D0.BB.D1.83.D0.B6.D0.B1.D0.B0_systemd)
        *   [2.1.5 Таймер systemd](#.D0.A2.D0.B0.D0.B9.D0.BC.D0.B5.D1.80_systemd)

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

Следующая команда отфильтрует пять зеркал, отсортирует их по скорости и обновит файл mirrorlist:

```
# reflector --verbose -l 5 --sort rate --save /etc/pacman.d/mirrorlist

```

#### Пример 2

Эта команда подробно выведет список 200 наиболее недавно обновленных HTTP-зеркал, отсортирует их по скорости загрузки и обновит mirrorlist:

```
# reflector --verbose -l 200 -p http --sort rate --save /etc/pacman.d/mirrorlist

```

#### Пример 3

То же, что и в предыдущем примере, но будут взяты только зеркала, расположенные в Соединенных Штатах:

```
# reflector --verbose --country 'United States' -l 200 -p http --sort rate --save /etc/pacman.d/mirrorlist

```

#### Служба systemd

 `/etc/systemd/system/reflector.service` 
```
[Unit]
Description=Pacman mirrorlist update

[Service]
Type=oneshot
ExecStart=/usr/bin/reflector --protocol http --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

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
ExecStart=/usr/bin/reflector --protocol http --latest 30 --number 20 --sort rate --save /etc/pacman.d/mirrorlist

[Install]
RequiredBy=network.target

```

И [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") службу `reflector.service`.

Для того, чтобы она работала, цель `network.target` должна правильно означать, что установлено интернет-соединение.

#### Таймер systemd

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