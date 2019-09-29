Ссылки по теме

*   [pacman (Русский)](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Pacman (Русский)")

**Состояние перевода:** На этой странице представлен перевод статьи [Pkgfile](/index.php/Pkgfile "Pkgfile"). Дата последней синхронизации: 27 сентября 2019\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Pkgfile&diff=0&oldid=581214).

**pkgfile** — инструмент для поиска файлов в пакетах из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

**Совет:** В [pacman](https://www.archlinux.org/packages/?name=pacman) есть схожая [встроенная функциональность](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Поиск_пакета_по_названию_файла "Pacman (Русский)").

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Использование](#Использование)
*   [3 Команда не найдена](#Команда_не_найдена)
*   [4 Автоматические обновления](#Автоматические_обновления)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [pkgfile](https://www.archlinux.org/packages/?name=pkgfile). В качестве альтернативы можно установить пакет [pkgfile-git](https://aur.archlinux.org/packages/pkgfile-git/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)").

Чтобы синхронизировать базу данных *pkgfile*, выполните команду:

```
# pkgfile -u

```

## Использование

Найти пакет, которому принадлежит файл `makepkg`:

 `$ pkgfile makepkg`  `core/pacman` 

Показать все файлы пакета [archlinux-keyring](https://www.archlinux.org/packages/?name=archlinux-keyring):

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

Последняя команда похожа на команду `pacman -Ql` (подробности можно найти в статье [pacman (Русский)#Запросы к базам данных пакетов](/index.php/Pacman_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Запросы_к_базам_данных_пакетов "Pacman (Русский)")), но позволяет искать файлы пакетов, которые ещё не установлены в систему и находятся в удалённых (remote) репозиториях.

## Команда не найдена

Изучите статьи [Bash (Русский)#Команда не найдена](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Команда_не_найдена "Bash (Русский)"), [Zsh (Русский)#Обработчик неизвестных команд](/index.php/Zsh_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Обработчик_неизвестных_команд "Zsh (Русский)") и [Fish (Русский)#Хук "command not found"](/index.php/Fish_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Хук_"command_not_found" "Fish (Русский)").

## Автоматические обновления

**pkgfile** поставляется вместе со службой [systemd](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)") и [таймером](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)/Timers_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Systemd (Русский)/Timers (Русский)") для автоматической синхронизации базы данных. Для запуска автоматического обновления [включите](/index.php/%D0%92%D0%BA%D0%BB%D1%8E%D1%87%D0%B8%D1%82%D0%B5 "Включите") таймер `pkgfile-update.timer`.

По умолчанию, база данных обновляется ежедневно. Чтобы изменить график обновлений, [отредактируйте файл юнитов](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#Редактирование_предоставленных_пакетами_файлов_юнитов "Systemd (Русский)").