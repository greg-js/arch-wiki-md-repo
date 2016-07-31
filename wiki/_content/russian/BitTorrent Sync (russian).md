[BitTorrent Sync](https://www.getsync.com/) (BTSync) это система обмена файлами, который использует протокол [BitTorrent](https://en.wikipedia.org/wiki/Bittorrent "wikipedia:Bittorrent"). Вместо того, чтобы иметь центральный сервер, который архивирует каждый файл, этот метод синхронизации использует соединения децентрализованных равноправных узлов между самими устройствами, поэтому не существует никаких ограничений по хранению данных и/или скорости передачи данных. Данные пользователя хранятся исключительно на устройствах, которые выбрал пользователь, следовательно, пользователь должен иметь по меньшей мере два устройства, или «узла», которые должны быть в сети. Если многие устройства подключены одновременно, файлы распределяются между ними в топологии ячеистой сети.

## Contents

*   [1 Безопасность](#.D0.91.D0.B5.D0.B7.D0.BE.D0.BF.D0.B0.D1.81.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
*   [2 Cинхронизация](#C.D0.B8.D0.BD.D1.85.D1.80.D0.BE.D0.BD.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
*   [3 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [4 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)

## Безопасность

Весь трафик между устройствами шифруется с помощью AES-128 в режиме счетчика, с помощью уникального ключа. Этот ключ является производным от «тайного», который сам по себе является случайной генерации 21-байтого ключа base32-алгоритма. Путем передачи секретного ключа, файлы и папки могут быть синхронизированы с другими пользователями.

## Cинхронизация

Когда устройство добавляет папку для синхронизации, генерируется секретный ключ. С этого момента, каждое устройство, которое хочет синхронизировать эту папку должен знать секретный ключ.

Синхронизация не имеет скорости или размера ограничений, до тех пор, как оба устройства имеют достаточно дискового пространства.

## Установка

[btsync](https://aur.archlinux.org/packages/btsync/) может быть установлен из [AUR (Русский)](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"). Пакет включает в себя [systemd (Русский)](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)")-сервис для управления btsync демона. По умолчанию, этот пакет создает /etc/btsync.conf для системы / корневой операции. Внесите необходимые изменения (например, Логин ID и пароль) в этих файлах до включения сервис-файл с systemctl.

В качестве альтернативы, голый 'tar.gz' упаковывают исполняемый файл может быть загружен с официального сайта. Остальная часть этого руководства предполагает, что вы используете пакет btsync из AUR.

## Использование

Клиент Linux из BTSync не использует типичный GUI, вместо этого он настраивает сервер WebUI доступный на localhost:8888\. Общие папки можно также настроить статически в файле конфигурации, но при этом отключает WebGUI.

После установки, вы будете в первую очередь необходимо создать конфигурационный файл в `~/.config /btsync/btsync.conf` см. [#Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F). Вам также необходимо создать каталог `путь_папки`. Когда это будет сделано, и начать (если вы хотите, чтобы начать при загрузке системы) включите службы:

```
$ systemctl --user start btsync
$ systemctl --user enable btsync

```

Служба будет работать как пользователь, ссылающегося команду. Обратите внимание, что приведенная выше команда *не* запускается как root-пользователь: это может привести к ошибке, что D-Bus отказал в соединении.

**Note:** Важно, чтобы убедиться, что, когда `btsync` запускается в качестве пользователя, файл `btsync.conf` и каталог, в котором `btsync.pid` файл будет располагаться иметь правильные разрешения пользователя, т.е. принадлежат пользователю, ссылающегося команду. Несоблюдение этого правила позволит предотвратить службу от запуска. Если права доступа пользователей являются правильными, но btsync по-прежнему не запускается после того, как включен, перезагрузите систему.

**Note:** Если после запуска `btsync` на обезглавленный сервере, позволяют сохраняющиеся начать `btsync` и сохранить это работает вне сеансов пользователей: [systemd/User (Русский)#Автоматический запуск пользовательского экземпляра systemd](/index.php/Systemd/User_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D1.8D.D0.BA.D0.B7.D0.B5.D0.BC.D0.BF.D0.BB.D1.8F.D1.80.D0.B0_systemd "Systemd/User (Русский)")

Вы также можете запустить его в качестве пользователя системы `btsync`, просто оставьте `--user` часть из:

```
# systemctl enable btsync
# systemctl start btsync

```

Конфигурация для этого пользователя находится в `/etc/btsync.conf`, и метаданные сохраняются в `/var/lib/btsync/` по умолчанию. Необходимо просмотреть параметры конфигурации, особенно пользователя и пароль, смотрите ниже.