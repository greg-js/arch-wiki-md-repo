**Состояние перевода:** На этой странице представлен перевод статьи [Pkgfile](/index.php/Pkgfile "Pkgfile"). Дата последней синхронизации: 2015-02-17\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Pkgfile&diff=0&oldid=361499).

**pkgfile** — это инструмент для поиска файлов внутри пакетов из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Использование](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5)
*   [3 Команда не найдена](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.B0_.D0.BD.D0.B5_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD.D0.B0)
    *   [3.1 Bash](#Bash)
    *   [3.2 Zsh](#Zsh)
    *   [3.3 Fish](#Fish)
*   [4 Автоматические обновления](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") [pkgfile](https://www.archlinux.org/packages/?name=pkgfile) из официальных репозиториев или [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

Для синхронизации базы данных *pkgfile* используйте команду:

```
# pkgfile -u

```

## Использование

Чтобы найти пакет, который владеет файлом `makepkg`:

 `$ pkgfile makepkg`  `core/pacman` 

Чтобы отобразить все файлы из пакета [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring):

 `$ pkgfile -l archlinux-keyring` 
```
core/archlinux-keyring usr/
core/archlinux-keyring usr/share/
core/archlinux-keyring usr/share/pacman/
core/archlinux-keyring usr/share/pacman/keyrings/
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-revoked
core/archlinux-keyring usr/share/pacman/keyrings/archlinux-trusted
core/archlinux-keyring usr/share/pacman/keyrings/archlinux.gpg
```

Это аналогично `pacman -Ql` (смотрите [pacman (Русский)#Запросы к базам данных пакетов](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.97.D0.B0.D0.BF.D1.80.D0.BE.D1.81.D1.8B_.D0.BA_.D0.B1.D0.B0.D0.B7.D0.B0.D0.BC_.D0.B4.D0.B0.D0.BD.D0.BD.D1.8B.D1.85_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.BE.D0.B2 "Pacman (Русский)")), за тем исключением, что не требует установки пакета.

## Команда не найдена

pkgfile добавляет хук "command not found" для [Bash](/index.php/Bash "Bash") и [Zsh](/index.php/Zsh "Zsh"), который автоматически выполняет поиск в официальных репозиториях, если была введена неизвестная команда:

 `$ abiword` 
```
abiword may be found in the following packages:
  extra/abiword 2.8.6-7 usr/bin/abiword

```

Чтобы это работало во всех дочерних оболочках, необходимо прописать этот хук в файле инициализации вашей командной оболочки.

### Bash

 `~/.bashrc`  `source /usr/share/doc/pkgfile/command-not-found.bash` 

### Zsh

 `~/.zshrc`  `source /usr/share/doc/pkgfile/command-not-found.zsh` 

### Fish

`pkgfile` не предоставляет хук специально для [Fish](/index.php/Fish_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fish (Русский)"), однако, вы можете создать собственную функцию `command-not-found`, которая будет запускаться каждый раз, когда Fish обнаруживает неизвестную команду:

 `~/.config/fish/functions/command-not-found.fish` 
```
function command-not-found
        set cmd $argv[2]
        set pkgs (pkgfile -b -v $argv  2>/dev/null)
        set pkgs_test (echo $pkgs[1] / xargs)   ## trim spaces and line feeds
        if test -n $pkgs_test
                echo "$cmd may be found in the following packages:"
                echo -e $pkgs"
"
                return 0
        else
                echo "Command not found in any package."
        end
        return 127
end

```

В строке 4 `/` заменить на `|`

## Автоматические обновления

**pkgfile** поставляется вместе со службой и [таймером](/index.php/Systemd/T%D0%B0%D0%B9%D0%BC%D0%B5%D1%80%D1%8B "Systemd/Tаймеры") [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") для автоматической синхронизации базы данных. Для включения автоматического обновления [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") таймер `pkgfile-update.timer`.

По умолчанию, база данных обновляется ежедневно. Чтобы это изменить, скопируйте `/usr/lib/systemd/system/pkgfile-update.timer` в `/etc/systemd/system/pkgfile-update.timer` и отредактируйте копию файла под ваши нужды.