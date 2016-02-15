Remmina - это клиент удаленного рабочего стола, написанный на GTK+. Поддерживаются следующие протоколы:

*   SSH
*   VNC
*   RDP
*   NX
*   SFTP
*   XDMCP

## Установка

Установите пакет [remmina](https://www.archlinux.org/packages/?name=remmina). Если вам нужна поддержка RDP, также установите [freerdp](https://www.archlinux.org/packages/?name=freerdp).

**Обратите внимание:** Если после установки [freerdp](https://www.archlinux.org/packages/?name=freerdp) возможность выбора протокола RDP в меню Remmina отсутствует, убедитесь, что вы полностью завершили программу: выполните `killall remmina`. Когда вы вновь запустите Remmina, RDP появится.

## Командная строка

Чтобы открыть предварительно сохраненный профиль соединений, вы можете выполнить:

```
$ remmina -c ~/.remmina/file-name.remmina

```

Вот небольшой скрипт, который переименовывает файлы профиля соединений, основываясь на свойстве `name=`, что делает их более удобными для восприятия:

```
#!/bin/bash
cd ~/.remmina
ls -1 *.remmina | while read a; do
       N=`grep '^name=' "$a" | cut -f2 -d=`;
       [ "$a" == "$N.remmina" ] || mv "$a" "$N".remmina;
done

```

Чтобы при запуске программа была свернута в трей, используйте опцию командной строки `-i`.