**Состояние перевода:** На этой странице представлен перевод статьи [Remmina](/index.php/Remmina "Remmina"). Дата последней синхронизации: 6 октября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Remmina&diff=0&oldid=584503).

[Remmina](https://remmina.org/) — клиент удалённого рабочего стола, созданный проектом [FreeRDP](http://www.freerdp.com/) с использованием GTK. Поддерживаются следующие протоколы: SSH, VNC, RDP, NX и XDMCP.

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [remmina](https://www.archlinux.org/packages/?name=remmina).

Установите пакет [libvncserver](https://www.archlinux.org/packages/?name=libvncserver), если необходима поддержка VNC.

Также установите [freerdp](https://www.archlinux.org/packages/?name=freerdp) или [remmina-plugin-rdesktop](https://aur.archlinux.org/packages/remmina-plugin-rdesktop/), если необходима поддержка RDP. Обратите внимание, что:

*   Если опция подключения по RDP недоступна в выпадающем меню Remmina после установки [freerdp](https://www.archlinux.org/packages/?name=freerdp), полностью завершите выполнение программы (например, выполните `killall remmina`) и снова запустите её, после чего опция с RDP должна появиться.
*   По состоянию на Remmina 1.2.0, некоторые пользователи сообщают, что RDP-соединения с использованием FreeRDP часто прерываются и соединения с использованием rdesktop более надёжны.
*   Сохранение паролей зависит от [GNOME Keyring](/index.php/GNOME/Keyring "GNOME/Keyring").

## Использование

Выполните следующую команду, чтобы открыть предварительно сохранённый профиль соединений:

```
$ remmina -c ~/.remmina/название-файла.remmina

```

Ниже представлен скрипт, который переименовывает файлы профиля соединений, основываясь на свойстве `name=`, что делает их более удобными для восприятия:

```
#!/bin/bash
cd ~/.remmina
ls -1 *.remmina | while read a; do
       N=`grep '^name=' "$a" | cut -f2 -d=`;
       [ "$a" == "$N.remmina" ] || mv "$a" "$N".remmina;
done

```

Чтобы при запуске программа была свёрнута в трей, используйте опцию командной строки `-i`.

## Смотрите также

*   [Репозиторий Remmina на GitLab](https://gitlab.com/Remmina/Remmina)
*   [FreeRDP Wiki](https://github.com/FreeRDP/FreeRDP/wiki)