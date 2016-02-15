**Состояние перевода:** На этой странице представлен перевод статьи [Tox](/index.php/Tox "Tox"). Дата последней синхронизации: 2015-07-29\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Tox&diff=0&oldid=382499).

С домашней страницы [проекта](https://tox.chat/ru):

	_Tox - это распределённый безопасный мессенджер с возможностью общения по аудио и видео._

## Установка

Ядро Tox и его клиентская часть разрабатываются раздельно. Вам потребуется установить пакет [toxcore](https://www.archlinux.org/packages/?name=toxcore) и любой из [клиентов Tox](https://wiki.tox.chat/clients):

*   **µTox (uTox)** — Облегченный клиент Tox

	[https://wiki.tox.chat/UTox](https://wiki.tox.chat/UTox) || [utox-git](https://aur.archlinux.org/packages/utox-git/)

*   **qTox** — Мощный Tox клиент, написанный на QT

	[https://wiki.tox.chat/clients/qtox](https://wiki.tox.chat/clients/qtox) || [qtox-git](https://aur.archlinux.org/packages/qtox-git/)

*   **Toxic** — Интерфейс командной строки на базе Ncurses

	[https://wiki.tox.chat/clients/toxic](https://wiki.tox.chat/clients/toxic) || [toxic-git](https://aur.archlinux.org/packages/toxic-git/)

*   **Ratox** — Клиент на базе именованного канала

	[https://wiki.tox.chat/Ratox](https://wiki.tox.chat/Ratox) || [ratox-git](https://aur.archlinux.org/packages/ratox-git/)

*   **gTox** — Tox клиент в GTK3 стиле

	[https://github.com/KoKuToru/gTox/](https://github.com/KoKuToru/gTox/) || [gtox-git](https://aur.archlinux.org/packages/gtox-git/)

**Важно:** Такого клиента нет в списке [клиентов](https://wiki.tox.chat/users/clients)

*   **Blight** — Cross-platform graphical user interface for Tox

	[https://wiki.tox.chat/Blight](https://wiki.tox.chat/Blight) || Not in AUR

*   **Плагин протокола Tox для Pidgin** — плагин для Pidgin, который позволяет использовать протокол Tox в Pidgin

	[https://wiki.tox.chat/Tox_Pidgin_Protocol_Plugin](https://wiki.tox.chat/Tox_Pidgin_Protocol_Plugin) || [tox-prpl-git](https://aur.archlinux.org/packages/tox-prpl-git/)

## Подключение к узлу

Чтобы подключиться к другим, сначала Tox должен подключиться к [DHT ноде](https://wiki.tox.chat/users/nodes). Все DHT ноды соединены между собой, и когда все подключены хотя бы к одной DHT ноде, вы можете подключаться к другим тем или иным путём.

 `/etc/conf.d/tox_bootstrap` 

```
cmdline="--ipv4"

# открытый узел, взятый с [https://wiki.tox.chat/users/nodes](https://wiki.tox.chat/users/nodes) DHT
ip="IP_узла"
port="порт_узла"
key="ключ_узла"
```

_IP_узла_, _порт_узла_ и _ключ_узла_ возьмите с [https://wiki.tox.chat/users/nodes](https://wiki.tox.chat/users/nodes).

**Важно:** Берите адреса **только** с официальной Вики Tox - они защищены от изменений третьими лицами, в отличие от ArchWiki

Создайте service файл.

 `/etc/systemd/system/tox_bootstrap.service` 

```
[Unit]
Description=Tox DHT Bootstrap Daemon
After=network.target

[Service]
Type=simple
EnvironmentFile=/etc/conf.d/tox_bootstrap
WorkingDirectory=/etc/tox
ExecStart=/usr/bin/DHT_bootstrap ${cmdline} ${ip} ${port} ${key}
User=tox
Group=tox

[Install]
WantedBy=multi-user.target
```

Создайте пользователя для запуска демона и настройте папку.

```
# useradd --no-create-home --shell /bin/false --user-group tox
# mkdir --verbose /etc/tox
# chown --recursive --verbose tox:tox /etc/tox

```

Перезапустите _systemd_ для сканирования новых юнитов:

```
# systemctl daemon-reload

```

[Включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") и запустите tox_bootstrap сервис и убедитесь, что он запущен и что порт был назначен:

 `# ss --listening --numeric --processes | grep _порт_узла_`  `udp        0      0 *:_порт_узла_                 *:*                                 576/DHT_bootstrap`