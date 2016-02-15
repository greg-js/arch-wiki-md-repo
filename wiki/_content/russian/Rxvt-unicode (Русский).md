**Состояние перевода:** На этой странице представлен перевод статьи [Rxvt-unicode](/index.php/Rxvt-unicode "Rxvt-unicode"). Дата последней синхронизации: 14 ноября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Rxvt-unicode&diff=0&oldid=409102).

[rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) это очень настраиваемый [эмулятор терминала](https://en.wikipedia.org/wiki/ru:%D0%AD%D0%BC%D1%83%D0%BB%D1%8F%D1%82%D0%BE%D1%80_%D1%82%D0%B5%D1%80%D0%BC%D0%B8%D0%BD%D0%B0%D0%BB%D0%B0 "wikipedia:ru:Эмулятор терминала") ответвлённый от [rxvt](https://en.wikipedia.org/wiki/Rxvt "wikipedia:Rxvt"). Обычно известный как `urxvt`, rxvt-unicode может быть [демон](/index.php/Daemon_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Daemon (Русский)")изирован для запуска клиентов в рамках одного [процесса](https://en.wikipedia.org/wiki/ru:%D0%9F%D1%80%D0%BE%D1%86%D0%B5%D1%81%D1%81_(%D0%B8%D0%BD%D1%84%D0%BE%D1%80%D0%BC%D0%B0%D1%82%D0%B8%D0%BA%D0%B0) "wikipedia:ru:Процесс (информатика)") для того, чтобы свести к минимуму использование системных ресурсов. Некоторые из наиболее выдающихся особенностей rxvt-Unicode включают международную языковую поддержку через [Юникод](https://en.wikipedia.org/wiki/ru:%D0%AE%D0%BD%D0%B8%D0%BA%D0%BE%D0%B4 "wikipedia:ru:Юникод"), способность отображать различные типы шрифтов и поддержку расширений [Perl](https://en.wikipedia.org/wiki/ru:Perl "wikipedia:ru:Perl"). Разработан Марк Леманном и сообществом разработчиков.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [2.1 Создание ~/.Xresources](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.7E.2F.Xresources)
    *   [2.2 Настоящая прозрачность](#.D0.9D.D0.B0.D1.81.D1.82.D0.BE.D1.8F.D1.89.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [2.3 Родная прозрачность](#.D0.A0.D0.BE.D0.B4.D0.BD.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [2.4 Полоса прокрутки](#.D0.9F.D0.BE.D0.BB.D0.BE.D1.81.D0.B0_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8)
    *   [2.5 Позиция полосы прокрутки](#.D0.9F.D0.BE.D0.B7.D0.B8.D1.86.D0.B8.D1.8F_.D0.BF.D0.BE.D0.BB.D0.BE.D1.81.D1.8B_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8)
    *   [2.6 Прокрутка буфера в дополнительном экране](#.D0.9F.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B0_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0_.D0.B2_.D0.B4.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D0.BC_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.B5)
    *   [2.7 Методы декларации шрифта](#.D0.9C.D0.B5.D1.82.D0.BE.D0.B4.D1.8B_.D0.B4.D0.B5.D0.BA.D0.BB.D0.B0.D1.80.D0.B0.D1.86.D0.B8.D0.B8_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0)
    *   [2.8 Набор иконок](#.D0.9D.D0.B0.D0.B1.D0.BE.D1.80_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA)
    *   [2.9 Установить как оболочку входа](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.B8.D1.82.D1.8C_.D0.BA.D0.B0.D0.BA_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D1.83_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0)
    *   [2.10 Используйте urxvt для запуска приложений](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B9.D1.82.D0.B5_urxvt_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [2.11 Расстояние шрифта](#.D0.A0.D0.B0.D1.81.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D0.B5_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0)
*   [3 Perl расширения](#Perl_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.1 Кликабельные ссылки (URL-адреса)](#.D0.9A.D0.BB.D0.B8.D0.BA.D0.B0.D0.B1.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8_.28URL-.D0.B0.D0.B4.D1.80.D0.B5.D1.81.D0.B0.29)
    *   [3.2 Yankable URL'ы (без мыши)](#Yankable_URL.27.D1.8B_.28.D0.B1.D0.B5.D0.B7_.D0.BC.D1.8B.D1.88.D0.B8.29)
    *   [3.3 Простые вкладки](#.D0.9F.D1.80.D0.BE.D1.81.D1.82.D1.8B.D0.B5_.D0.B2.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8)
    *   [3.4 Расширенное управление вкладками](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0.D0.BC.D0.B8)
    *   [3.5 Полноэкранный](#.D0.9F.D0.BE.D0.BB.D0.BD.D0.BE.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.B9)
    *   [3.6 Поддержка колеса прокрутки](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BB.D0.B5.D1.81.D0.B0_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8)
    *   [3.7 Изменение размера шрифта на лету](#.D0.98.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D0.B7.D0.BC.D0.B5.D1.80.D0.B0_.D1.88.D1.80.D0.B8.D1.84.D1.82.D0.B0_.D0.BD.D0.B0_.D0.BB.D0.B5.D1.82.D1.83)
    *   [3.8 Отключение расширений Perl](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D0.B9_Perl)
*   [4 Цвета](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0)
    *   [4.1 Цвета как в Xterm](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0_.D0.BA.D0.B0.D0.BA_.D0.B2_Xterm)
*   [5 Повышение производительности](#.D0.9F.D0.BE.D0.B2.D1.8B.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.1 Демон-клиент](#.D0.94.D0.B5.D0.BC.D0.BE.D0.BD-.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82)
        *   [5.1.1 Xinitrc](#Xinitrc)
        *   [5.1.2 systemd](#systemd)
*   [6 Вырезать и вставить](#.D0.92.D1.8B.D1.80.D0.B5.D0.B7.D0.B0.D1.82.D1.8C_.D0.B8_.D0.B2.D1.81.D1.82.D0.B0.D0.B2.D0.B8.D1.82.D1.8C)
    *   [6.1 Клавиши по умолчанию](#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
    *   [6.2 Пользовательские сочетания клавиш](#.D0.9F.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8C.D1.81.D0.BA.D0.B8.D0.B5_.D1.81.D0.BE.D1.87.D0.B5.D1.82.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
    *   [6.3 Управление буфером обмена](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.BE.D0.BC_.D0.BE.D0.B1.D0.BC.D0.B5.D0.BD.D0.B0)
    *   [6.4 Сценарий автоматического управления](#.D0.A1.D1.86.D0.B5.D0.BD.D0.B0.D1.80.D0.B8.D0.B9_.D0.B0.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B3.D0.BE_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
*   [7 Улучшенное поведение как в Kuake, Openbox](#.D0.A3.D0.BB.D1.83.D1.87.D1.88.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D0.BF.D0.BE.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.B0.D0.BA_.D0.B2_Kuake.2C_Openbox)
    *   [7.1 Скриплеты](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D0.BB.D0.B5.D1.82.D1.8B)
    *   [7.2 urxvtq с табуляцией](#urxvtq_.D1.81_.D1.82.D0.B0.D0.B1.D1.83.D0.BB.D1.8F.D1.86.D0.B8.D0.B5.D0.B9)
        *   [7.2.1 Управление Tab](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_Tab)
    *   [7.3 Настройка Openbox](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Openbox)
    *   [7.4 Дальнейшая настройка](#.D0.94.D0.B0.D0.BB.D1.8C.D0.BD.D0.B5.D0.B9.D1.88.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [7.5 Связанные сценарии](#.D0.A1.D0.B2.D1.8F.D0.B7.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D1.81.D1.86.D0.B5.D0.BD.D0.B0.D1.80.D0.B8.D0.B8)
*   [8 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [8.1 Настройки ~/.Xresources не применяются](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.7E.2F.Xresources_.D0.BD.D0.B5_.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D0.BD.D1.8F.D1.8E.D1.82.D1.81.D1.8F)
    *   [8.2 Прозрачность не работает после обновления, начиная с версии 9.09](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BE.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F.2C_.D0.BD.D0.B0.D1.87.D0.B8.D0.BD.D0.B0.D1.8F_.D1.81_.D0.B2.D0.B5.D1.80.D1.81.D0.B8.D0.B8_9.09)
    *   [8.3 Удаленные хосты](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.B5_.D1.85.D0.BE.D1.81.D1.82.D1.8B)
    *   [8.4 Использование rxvt-Unicode в качестве терминала gmrun (Gnome Completion-Run)](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_rxvt-Unicode_.D0.B2_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.B0_gmrun_.28Gnome_Completion-Run.29)
    *   [8.5 Моя цифровая клавиатура действует странно и производит странный вывод (например, в VIM)](#.D0.9C.D0.BE.D1.8F_.D1.86.D0.B8.D1.84.D1.80.D0.BE.D0.B2.D0.B0.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D0.B0_.D0.B4.D0.B5.D0.B9.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.BD.D0.BE_.D0.B8_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82_.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.28.D0.BD.D0.B0.D0.BF.D1.80.D0.B8.D0.BC.D0.B5.D1.80.2C_.D0.B2_VIM.29)
    *   [8.6 pseudo-tty](#pseudo-tty)
    *   [8.7 Горячие клавиши не работают](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D1.8E.D1.82)
    *   [8.8 Низкая производительность при рисовании глифов](#.D0.9D.D0.B8.D0.B7.D0.BA.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D1.8C_.D0.BF.D1.80.D0.B8_.D1.80.D0.B8.D1.81.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B8_.D0.B3.D0.BB.D0.B8.D1.84.D0.BE.D0.B2)
*   [9 Внешние ресурсы](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D1.80.D0.B5.D1.81.D1.83.D1.80.D1.81.D1.8B)

## Установка

[rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) доступен в [официальных репохиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") и содержит поддержку 256 цветов.

[rxvt-unicode-patched](https://aur.archlinux.org/packages/rxvt-unicode-patched/) доступен в [AUR](/index.php/AUR "AUR") и включает в себя исправление ошибки ширины шрифта.

## Настройка

Смотрите [rxvt-unicode страницу справки](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) для полного списка доступных настроек и значений.

### Создание ~/.Xresources

Внешний вид, ощущения и функциональность rxvt-unicode контролируются аргументами (параметрами) командной строки и/или [ресурсами Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х"). X resources может быть задан при помощи `~/.Xresources` и _xrdb_ ([xorg-xrdb](https://www.archlinux.org/packages/?name=xorg-xrdb)). Для получения дополнительной информации смотрите статью [Ресурсы Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х").

Добавьте прокомментированный список всех "ресурсов (параметров)" _rxvt_ в ваш файл `~/.Xresources`:

```
 urxvt --help 2>&1| sed -n '/:  /s/^ */! URxvt*/gp' >> ~/.Xresources

```

Либо, чтобы помимо комментариев в файле были и полезные описания:

 `TERM=rxvt-unicode-256color command man -Pcat urxvt | sed -n '/depth: b/,/^BA/p'|sed '$d'|sed '/^       [a-z]/s/^ */^/g'|sed -e :a -e 'N;s/\n/@@/g;ta;P;D'|sed 's,\^\([^@]\+\)@*[\t ]*\([^\^]\+\),! \2\n! URxvt*\1\n\n,g'|sed 's,@@\(  \+\),\n\1,g'|sed 's,@*$,,g'|sed '/^[^!]/d'|tr -d "'\`" >> ~/.Xresources` 
**Обратите внимание:** Аргументы командной строки переопределяют настройки ресурсов и имеют над ними приоритет

### Настоящая прозрачность

Чтобы использовать настоящую прозрачность, вы должны использовать [оконный менеджер](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") с поддержкой композитинга, или отдельное приложение для композитинга.

Из командной строки:

```
$ urxvt -depth 32 -bg rgba:3f00/3f00/3f00/dddd

```

Используя файл настроек:

 `~/.Xresources` 

```
URxvt.depth: 32
URxvt.background: rgba:1111/1111/1111/dddd

```

или

 `~/.Xresources` 

```
URxvt.depth: 32
URxvt.background: [95]#000000

```

где '95' является уровень непрозрачности в процентах и '#000000' цвет фона.

Чтобы использовать цвет #302351 т.е. с rgba:rrrr/gggg/bbbb/aaaa синтаксисом это будет rgba:3000/2300/5100/ee00\. "ee00" (значение альфа) ятобы сделать его красиво прозрачным.

**Обратите внимание:** Для того, чтобы эти настройки были универсальны для всех форм URxvt, вы можете добавить символ подстановки "*". Например, `URxvt.depth` станет `URxvt*.depth`.

### Родная прозрачность

Если нет необходимости в настоящей прозрачности, или если композитинг использует слишком много ресурсов на вашей системе, вы можете получить прозрачность следующим образом:

 `~/.Xresources` 

```
! Xresources file

URxvt*.transparent: true
! URxvt*.shading: 0 to 99 darkens, 101 to 200 lightens
URxvt*.shading: 110

```

Использование установки URxvt*background подтверждает пример выше, URxvt*.shading также будет работать.

**Обратите внимание:** Избегайте использования затенения (shading), если у вас набор `URxvt.tintColor`. Используйте вместо `tintColor` другой.

### Полоса прокрутки

Внешний вид полосы прокрутки может быть выбраны через эту запись в `~/.Xresources`:

```
! стиль полосы прокрутки - rxvt (по умолчанию), plain (самый компактный), next, или xterm
URxvt.scrollstyle: rxvt

```

Полоса прокрутки может быть полностью отключена:

```
URxvt.scrollBar: false

```

### Позиция полосы прокрутки

По умолчанию, когда появляется вывод оболочки, вид прокрутки автоматически переходит к нижней части буфера для отображения нового вывода. Если вы хотите, увидеть предыдущий выход (например, сообщения компилятора), установите следующие параметры в `~/.Xresources`:

```
! Не прокручивать при выводе
URxvt*scrollTtyOutput: false

! прокручивать по отношению к буферу (прокрутка мышью или Shift+Page Up)
URxvt*scrollWithBuffer: true

! прокрутка по нажатию клавиши
URxvt*scrollTtyKeypress: true

```

### Прокрутка буфера в дополнительном экране

Когда вы прокручиваете постранично во _вторичном экране_ (например `less` без опции`**-X**`), будет хорошей идеей отключить прокрутку буфера, чтобы иметь возможность прокручивать _именно_ постранично _вторичный экран_, а не буфер терминала: это неизменено по умолчанию в терминалах на основе vte. Чтобы отключить буфер прокрутки _второго_ экрана в _urxvt_:

```
URxvt.secondaryScreen: 1
URxvt.secondaryScroll: 0

```

Эта настройка работает как и ожидалось, за исключением прокрутки колесом мыши. Когда вы листаете постранично "вторичный экран" колесом мыши - и там было что-то в буфере прокрутки - вместо страницы _вторичного экрана_ колесом мыши будет прокручиватся буфер прокрутки. Чтобы решить эту проблему, необходимо ввести новый параметр в rxvt-unicode[[1]](https://bbs.archlinux.org/viewtopic.php?id=132150). Патченный rxvt-unicode доступен в пакете [rxvt-unicode-better-wheel-scrolling](https://aur.archlinux.org/packages/rxvt-unicode-better-wheel-scrolling/). После его установки добавьте следующие строки в файл настроек:

```
URxvt.secondaryWheel: 1

```

**Обратите внимание:** Пожалуйста, не используйте эту опцию с расширением Perl [vtwheel](#.D0.9F.D0.BE.D0.B4.D0.B4.D0.B5.D1.80.D0.B6.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BB.D0.B5.D1.81.D0.B0_.D0.BF.D1.80.D0.BE.D0.BA.D1.80.D1.83.D1.82.D0.BA.D0.B8): это приведёт к беспорядку

### Методы декларации шрифта

```
URxvt.font: 9x15

```

Тоже самое что и:

```
URxvt.font: -misc-fixed-medium-r-normal--15-140-75-75-c-90-iso8859-1

```

И, для того же шрифта bold (толстый):

```
URxvt.font: 9x15bold

```

Тоже самое что и:

```
URxvt.font: -misc-fixed-bold-r-normal--15-140-75-75-c-90-iso8859-1

```

Полный список коротких имен для основных шрифтов Х может быть найден в `/usr/share/fonts/misc/fonts.alias` (также есть файлы fonts.alias в некоторых других подкаталогах `/usr/share/fonts/`, но они упакованы отдельно от реальных шрифтов, и могут перечислять шрифты которые на самом деле не установлены). Стоит отметить, что эти короткие псевдонимы выбираются для версии ISO-8859-1 а не версии ISO-10646-1 (Юникод), и скорее версии 75 DPI чем 100 DPI, так что лучше избегать их, и вместо них выбирать шрифты по полному имени.

**Обратите внимание:** Пункт выше только для растровых шрифтов. Другие шрифты могут быть использованы через Xft, используя следующий формат:

```
URxvt.font: xft:monaco:size=10

```

Или

```
URxvt.font: xft:monaco:bold:size=10

```

**Обратите внимание:**

*   Если есть дефис (-) в имени шрифта Xft, он должен быть экранирован двойным (\). Как в этом примере:

```
URxvt*font: xft:Inconsolata\\-\\dz for Powerline:size=12

```

Это отличается от использования варианта опции urxvt -fn которая возвращает результат fc-list, где (\) указан только один раз.

*   Вы увидите новый шрифт только при перезапуске сервера Х.

Хороший способ для тестирования шрифтов прямо в терминале до совершения изменений в файле настроек, является вывод escape-кодов в терминале, например:

```
$ printf '\e]710;%s\007' "xft:Terminus:pixelsize=12"

```

### Набор иконок

**Обратите внимание:** Из-за сообщений и жалоб в отчете об ошибке [FS#34862](https://bugs.archlinux.org/task/34862), что в пакете [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) много зависимостей, теперь для того, чтобы использовать опцию `iconFile`, вы должны установить пакет [rxvt-unicode-pixbuf](https://aur.archlinux.org/packages/rxvt-unicode-pixbuf/)

По умолчанию URxvt не имеет значка на панели задач. Тем не менее, это можно легко изменить путем добавления строки, указывающей на нужную иконку, в файл `~/.Xresources`:

```
URxvt.iconFile:    /usr/share/icons/Clarity/scalable/apps/terminal.svg

```

### Установить как оболочку входа

Это заставляет оболочку (shell) запускаться как оболочку входа (login shell), как вариант `-ls`.

```
URxvt*loginShell: true

```

### Используйте urxvt для запуска приложений

urxvt может быть использован в качестве легкой альтернативы для запуска приложений, таких как [gmrun](https://www.archlinux.org/packages/?name=gmrun). Запустите urxvt со следующей опцией вида и поведения запуска приложения, или назначьте команду в псевдониме:

```
$ urxvt -geometry 80x3 -name 'bashrun' -e sh -c "/bin/bash -i -t"

```

### Расстояние шрифта

По умолчанию, расстояние между символами слишком широкое. Это контролируется параметром:

 `~/.Xresources` 

```
URxvt.letterSpace: -1

```

Здесь `-1` уменьшается расстояние от одного пикселя, при необходимости можно регулировать.

## Perl расширения

Вы можете включить расширения perl в URxvt, следующей строкой:

```
URxvt.perl-ext-common: имя_расширения_1,имя_расширения_2,...

```

Обратите внимание, что между именами расширения **не** должно быть пробелов.

### Кликабельные ссылки (URL-адреса)

Вы можете сделать URL-адреса в терминале кликабельными , используя расширение matcher. Например, для открытия ссылок в [Firefox](/index.php/Firefox "Firefox") добавьте следушее в`.Xresources`:

```
URxvt.perl-ext-common: default,matcher
URxvt.url-launcher: /usr/bin/firefox
URxvt.matcher.button: 1

```

С rxvt-unicode 9.14, также можно использовать matcher для открытия списка последних (в настоящее время ограничено до 10) URL-адресов с помощью клавиатуры:

```
URxvt.keysym.C-Delete: perl:matcher:last
URxvt.keysym.M-Delete: perl:matcher:list

```

Соответствующие ссылки могут быть окрашены с помощью [#Цвета](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0) переднего плана (foreground) или фона (background), например, в синий:

```
URxvt.matcher.rend.0: Uline Bold fg5

```

В качестве альтернативы, используйте `colorUL` для цвета #RRGGBB. Это, окрасит весь подчеркнутый текст, только для ссылок matches:

```
URxvt.colorUL: #4682B4

```

### Yankable URL'ы (без мыши)

Кроме того, вы можете выбрать и открыть URL, в веб-браузере, не используя мышь. Установите пакет [urxvt-perls](https://www.archlinux.org/packages/?name=urxvt-perls) из [официальных репозиторий](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)") и настройте как надо `.Xresources`. Пример показан ниже:

```
URxvt.perl-ext: default,url-select
URxvt.keysym.M-u: perl:url-select:select_next
URxvt.url-select.launcher: /usr/bin/xdg-open
URxvt.url-select.underline: true

```

**Обратите внимание:** Это расширение заменяет расширение Clickable URLs упомянутых выше, так `matcher` могут быть удалены из списка `URxvt.perl-ext`.

**Основные команды:**

| Клавиша | Описание |
| Alt+u | Вход в режим выбора. Будет выбран последний URL на вашем экране. Вы можете повторить `Alt+u` для выбора следующего upward URL. |
| k | Select next upward URL |
| j | Select next downward URL |
| Return | Открыть выбранный URL в браузере и выйти из режима выбора |
| o | Открыть выбранный URL в браузере без выхода из режима выбора |
| y | Скопировать (yank) выбранные URL выйти из режима выбора |
| Esc | Отменить режим выбора URL |

### Простые вкладки

Чтобы добавить вкладки в urxvt, добавьте следующую строку в ваш `~/.Xresources`:

```
URxvt.perl-ext-common: ...,tabbed,...

```

Для управления вкладками, используйте:

| Клавиши | Описание |
| Shift+Down | Новая вкладка |
| Shift+Left | Перейти к левой вкладке |
| Shift+Right | Перейти к правой вкладке |
| Ctrl+Left | Переместить вкладку влево |
| Ctrl+Right | Переместить вкладку вправо |
| Ctrl+d | Закрыть вкладку |

Вы можете изменить цвета вкладок, следующими значениями:

```
URxvt.tabbed.tabbar-fg: 2
URxvt.tabbed.tabbar-bg: 0
URxvt.tabbed.tab-fg: 3
URxvt.tabbed.tab-bg: 0

```

### Расширенное управление вкладками

Установите пакет [urxvt-tabbedex](https://aur.archlinux.org/packages/urxvt-tabbedex/) из [AUR](/index.php/AUR "AUR"), затем добавьте `tabbedex` значение в `URxvt.perl-ext-common` X resource в вашем `~/.Xresources`:

```
URxvt.perl-ext-common: ...,tabbedex,...

```

**Обратите внимание:** Если вы ранее использовали `tabbed` расширение Perl и определили `tabbed` значение для `URxvt.perl-ext-common` X resource, пожалуйста, удалите `tabbed` первое значение, чтобы избежать конфликта с `tabbedex`.

По умолчанию, кнопка "[NEW]" (которая редко используется и используется только с помощью мыши) отключена при tabbedex. Вы можете снова включить эту функцию, задав `new-button`:

```
URxvt.tabbed.new-button: true

```

Вкладки можно назвать с помощью `Shift+ ↑` (чтобы подтвердить `Enter`, и `Escape` для отмены).

Чтобы автоматически скрывать панель вкладок, когда присутствует только одна вкладка, включите следующий ресурс:

```
URxvt.tabbed.autohide: true

```

Для предотвращения закрытия последней вкладки Urxvt, включите следующий ресурс:

```
URxvt.tabbed.reopen-on-close: yes

```

Чтобы начать новую вкладку или цикл с помощью вкладок, используйте следующие команды пользователя: `tabbedex:(new|next|prev)_tab`. Пример отображения:

```
URxvt.keysym.Control-t: perl:tabbedex:new_tab
URxvt.keysym.Control-Tab: perl:tabbedex:next_tab
URxvt.keysym.Control-Shift-Tab: perl:tabbedex:prev_tab

```

Чтобы определить свои собственные горячие клавиши для переименования вкладки или перемещения вкладки вправо или влево, используйте следующие команды: `tabbedex:move_tab_(left|right)` и `tabbedex:rename_tab`. Пример отображения:

```
URxvt.keysym.Control-Shift-Left: perl:tabbedex:move_tab_left
URxvt.keysym.Control-Shift-Right: perl:tabbedex:move_tab_right
URxvt.keysym.Control-Shift-R: perl:tabbedex:rename_tab

```

**Обратите внимание:** Переназначенные горячие клавиши, используемые для пользовательских команд, не будет отключать сопоставление по умолчанию, для этого вы должны установить X resource `no-tabbedex-keys`. Однако это значение, в настоящее время не входит в пакет [urxvt-tabbedex](https://aur.archlinux.org/packages/urxvt-tabbedex/). Вместо него, рассмотрите возможность использования пакета [urxvt-tabbedex-git](https://aur.archlinux.org/packages/urxvt-tabbedex-git/):

```
URxvt.tabbed.no-tabbedex-keys: true

```

### Полноэкранный

Вы можете установить [AUR](/index.php/AUR "AUR") пакет [urxvt-fullscreen](https://aur.archlinux.org/packages/urxvt-fullscreen/), а затем назначить клавишу (или сочетание клавиш), чтобы привести urxvt в полноэкранный режим.

 `~/.Xresources` 

```
...
URxvt.perl-ext-common: ..., fullscreen, ...
URxvt.keysym.F11: perl:fullscreen:switch
...

```

### Поддержка колеса прокрутки

Установите [urxvt-vtwheel](https://aur.archlinux.org/packages/urxvt-vtwheel/) из [AUR](/index.php/AUR "AUR") и добавьте его в ваше расширение Perl внутри `~/.Xresources`:

```
 URxvt.perl-ext-common:  ...,vtwheel,...

```

### Изменение размера шрифта на лету

Установите [urxvt-resize-font-git](https://aur.archlinux.org/packages/urxvt-resize-font-git/) из [AUR](/index.php/AUR "AUR"), и добавьте его в ваше расширение Perl внутри `~/.Xresources`

```
 URxvt.perl-ext-common:  ...,resize-font,...

```

и добавьте некоторые горячие клавиши, например, как эти:

```
 URxvt.resize-font.smaller: C-Down
 URxvt.resize-font.bigger: C-Up

```

Для назначения работы Ctrl+Shift, по умолчанию необходимо отключить назначение (binding)(обсуждение см [здесь](http://wilmer.gaa.st/blog/archives/36-rxvt-unicode-and-ISO-14755-mode.html)):

```
 URxvt.iso14755: false
 URxvt.iso14755_52: false

```

### Отключение расширений Perl

Если вы не используете функции расширения Perl, вы можете улучшить безопасность и скорость, отключив расширения Perl полностью.

```
URxvt.perl-ext:
URxvt.perl-ext-common:

```

**Обратите внимание:** Если вы используете несколько возможностей расширения Perl, вы можете перечислить их в последовательности, разделяя запятыми: `URxvt.perl-ext-common:default,matcher,tabbed.`

## Цвета

По умолчанию, rxvt-unicode собран с поддержкой цвета. В дополнении к стандартным цветам переднего плана и цвету фона, rxvt может отображать до 256 цветов (плюс high-intensity bold/blinking/underlined (высокоинтенсивный жирный/мигающий/подчёркнутый) и любое сочетание из них).

Образец `~/.Xresources` для urxvt терминала с цветами по умолчанию, белые шрифты на чёрном фоне написаны как и следует:

 `~/.Xresources` 

```
! Background color
URxvt*background: black

! Цвет шрифта
URxvt*foreground: white

! Другие цвета
URxvt*color0: black
URxvt*color1: red3
URxvt*color2: green3
URxvt*color3: yellow3
URxvt*color4: blue2
URxvt*color5: magenta3
URxvt*color6: cyan3
URxvt*color7: gray90
URxvt*color8: grey50
URxvt*color9: red
URxvt*color10: green
URxvt*color11: yellow
URxvt*color12: blue
URxvt*color13: magenta
URxvt*color14: cyan
URxvt*color15: white
```

Также можно указать значения цветов foreground (передний план/шрифт), background (фон), cursorColor (цвет курсора), cursorColor2 (цвет курсора2), colorBD, colorUL как число 0-15, - удобное сокращение ссылки на цвет color0-color15\. Смотрите [#Создание ~/.Xresources](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.7E.2F.Xresources) для создания комментированного файла `~/.Xresources` для `urxvt`.

### Цвета как в Xterm

По умолчанию `urxvt` использует те же цвета `xterm` кроме одного. Добавьте следующую строку в конце вашего `~/.Xresources` для цветов как в xterm:

 `~/.Xresources` 

```
...
URxvt*color12: rgb:5c/5c/ff
```

а затем объедините его содержимое с текущей настройкой X resources:

```
xrdb -merge ~/.Xresources

```

и перезапустите `urxvt`.

## Повышение производительности

*   Избегайте использования XFT шрифтов. Если есть необходимость в использовании XFT шрифтов, задайте занчени добавив `:antialias=false`.[[2]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod#Can_I_speed_up_Xft_rendering_somehow)
*   Соберите rxvt-unicode с отключением ненужных функций, `--disable-xft` и в частности `--disable-unicode3`.
*   Ограничьте количество `saveLines` (опция `-sl`)в буфере прокрутки, чтобы уменьшить использование памяти. [[4]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod#Isn_t_rxvt_unicode_supposed_to_be_sm)
    *   Используйте tmux для прокрутки буфера и установит saveLines в 0
*   [Отключите Perl](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D0.B9_Perl)
*   Пользуйтесь демоном `urxvtd` запуская клиенты `urxvtc`.

### Демон-клиент

#### Xinitrc

Смотрите раздел _Примеры_ в `man urxvtd`. Это предпочтительный вариант.

**Совет:** Добавьте в ваш `~/.xinitrc` строку:

```
urxvtd -q -f -o &

```

Перед строкой запуска вашего Окружения рабочего стола/Оконного менеджера. Перезапустите Х сервер.

Теперь запустите urxvt в качестве клиента, командой `urxvtc`

#### systemd

**Обратите внимание:** Обычные пользователи не могут выполнять команды systemctl для управления питанием (reboot (перезагрузка), poweroff (выключение), и т.п.) когда вход в urxvt клиент/демон выполняется через systemd, так как клиент не является частью [cессии](/index.php/Session "Session"). По этой причине, запуск urxvt через Systemd не рекомендуется.

Системная служба:

 `/etc/systemd/system/urxvtd@.service` 

```
[Unit]
Description=RXVT-Unicode Daemon

[Service]
User=%i
ExecStart=/usr/bin/urxvtd -q -o

[Install]
WantedBy=multi-user.target

```

Передайте имя пользователя [запустив службу](/index.php/Systemd_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D1.8E.D0.BD.D0.B8.D1.82.D0.BE.D0.B2 "Systemd (Русский)"):

```
urxvtd@_username_.service

```

Для службы [systemd/User](/index.php/Systemd/User "Systemd/User"), поместите следующие файлы секций, в `~/.config/systemd/user`:

 `urxvtd.service` 

```
[Unit]
Description=Urxvt Terminal Daemon
Requires=urxvtd.socket

[Service]
ExecStart=/usr/bin/urxvtd -o -q
Environment=RXVT_SOCKET=%t/urxvtd-%H

[Install]
WantedBy=_MyTarget_.target

```

 `urxvtd.socket` 

```
[Unit]
Description=urxvt daemon (socket activation)
Documentation=man:urxvtd(1) man:urxvt(1)

[Socket]
ListenStream=%t/urxvtd-%H

[Install]
WantedBy=sockets.target

```

## Вырезать и вставить

**Обратите внимание:** При использовании терминального мультиплексора, urxvt (или любой эмулятор терминала) интеграция `CLIPBOARD` не будет эффективной, поскольку будет невозможно выбрать весь нужный текст в прямом режиме или вообще, в некоторых случаях (например, когда активный мультиплексированный терминал меняется на другой, а затем происходит возврат к первоначальному, и один выбирает текст сверх того, что можно видеть, что вызывает текст из другого терминала, который будет отображаться). Очевидно, что это связано с тем, что эмулятор терминала не способен различать мультиплексированные терминалы. Таким образом, было бы излишне эффективно для тех, кто всегда использует терминальный мультиплексор, способный прокручивать буфер прокрутки и интеграцию с `CLIPBOARD` (например [tmux](/index.php/Tmux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Tmux (Русский)") c [индивидуальными горячими клавишами](/index.php/Tmux_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9A.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F "Tmux (Русский)")) для интеграции `CLIPBOARD` с urxvt.

Для пользователей, незнакомых с методами передачи данных [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)"), обмен информацией из rxvt-unicode может стать обузой. Достаточно сказать, что rxvt-unicode использует путь буфера который обычно загружается в текущем `PRIMARY` выборе по умолчанию. [[5]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod#THE_SELECTION_SELECTING_AND_PASTING_) Пользователи призывают пересмотреть [Wikipedia:X Window selection](https://en.wikipedia.org/wiki/X_Window_selection "wikipedia:X Window selection") для получения дополнительной информации.

### Клавиши по умолчанию

Горячие клавиши по умолчанию, всё равно будут работать для копирования и вставки. После выбора текста, для копирования воспользуйтесь Ctrl+Insert или Ctrl+Alt+C, для вставки Shift+Insert или Ctrl+Alt+V.

### Пользовательские сочетания клавиш

Для включения копировать/вставить по Ctrl+Shift+c/Ctrl+Shift+v, или аналогичных, вы должны отредактировать ваш .Xresources. Сначала добавьте расширение:

```
URxvt.perl-ext-common: default,clipboard

```

Затем отключите iso14755:

```
URxvt.iso14755: False

```

И назначьте клавиши:

```
URxvt.keysym.Shift-Control-C: perl:clipboard:copy
URxvt.keysym.Shift-Control-V: perl:clipboard:paste

```

При использовании xsel (который по умолчанию), используйте:

```
URxvt.clipboard.copycmd:  xsel -ib
URxvt.clipboard.pastecmd: xsel -ob

```

Эти две настройки могут быть изменены для других менеджеров буфера обмена, таких как Xclip.

### Управление буфером обмена

Смотрите [Clipboard#List of clipboard managers](/index.php/Clipboard#List_of_clipboard_managers "Clipboard")

### Сценарий автоматического управления

**Обратите внимание:** Начиная с версии 9.20, [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) поставляется с новым расширением `selection-to-clipboard`(выделение-в-буфер обмена) который заменяет сценарии ниже. Включите его, как и любое друге расширение.

Skottish [[6]](https://bbs.archlinux.org/viewtopic.php?pid=506845#p506845) создал скрипт на Perl, который автоматически копирует в буфер обмена Х любое выделение в rxvt-Unicode. Сохраните его как `/usr/lib/urxvt/perl/clipboard`:

```
#! /usr/bin/perl

sub on_sel_grab {
    my $query=quotemeta $_[0]->selection;
    $query=~ s/\n/\\n/g;
    $query=~ s/\r/\\r/g;
    system( "echo -en " . $query . " | xsel -i -b -p" );
}

```

Участник Xyne также создал свой собственный вариант сценария Skottish по имени [urxvt-clipboard](https://aur.archlinux.org/packages/urxvt-clipboard/) который доступен в [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)"), позволяющий пользователю вставлять выделение вместо `Ctrl+V` по щелчку средней кнопки мыши:

```
#! /usr/bin/perl

sub on_sel_grab
{
  my $query = $_[0]->selection;
  open (my $pipe,'|-','xsel -ib') or die;
  print $pipe $query;
  close $pipe;
  open (my $pipe,'|-','xsel -ip') or die;
  print $pipe $query;
  close $pipe;
}

```

Он также требует [xsel](https://www.archlinux.org/packages/?name=xsel) и должен быть включен в поле `*perl-ext-common` или `*perl-ext` `~/.Xresources`. Например:

```
URxvt.perl-ext-common: default,clipboard

```

[AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") пакет [urxvt-perls-git](https://aur.archlinux.org/packages/urxvt-perls-git/) это еще один вариант которым можно воспользоватся. [urxvt-perls-git](https://aur.archlinux.org/packages/urxvt-perls-git/) включает в себя такую же функциональность как [urxvt-clipboard](https://aur.archlinux.org/packages/urxvt-clipboard/), в дополнение к расширениям Perl keyboard-select и url-select.

## Улучшенное поведение как в Kuake, Openbox

Это первоначально разместил Xyne, на форуме [[7]](https://bbs.archlinux.org/viewtopic.php?pid=550380), и опирается на [xdotool](https://www.archlinux.org/packages/?name=xdotool) найденный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

### Скриплеты

Сохраните этот скриплет для `urxvtc` где-то на вашей системе как `urxvtc` (например в `~/.config/openbox`):

```
#!/bin/sh

urxvtc "$@"
if [ $? -eq 2 ]; then
   urxvtd -q -o -f
   urxvtc "$@"
fi

```

и сохраните этот скриплет как `urxvtq`:

```
#!/bin/bash

wid=$(xdotool search --classname urxvtq)
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 80x28
  wid=$(xdotool search --classname urxvtq | head -1)
  xdotool windowfocus "$wid"
  xdotool key Control_L+l
else
  if [ -z "$(xdotool search --onlyvisible --classname urxvtq 2>/dev/null)" ]; then
    xdotool windowmap "$wid"
    xdotool windowfocus "$wid"
  else
    xdotool windowunmap "$wid"
  fi
fi

```

Предыдущая версия [xdotool](https://www.archlinux.org/packages/?name=xdotool) выдавала ошибку, которая отключала признание видимых окон и, таким образом, привела некоторых пользователей к использованию следующего скриптлета на месте предыдущего. В этом больше нет необходимости, как и в [xdotool](https://www.archlinux.org/packages/?name=xdotool) >= 1.20100416.2809, но он был оставлен здесь для дальнейшего использования.'

```
#!/bin/bash

wid=$(xprop -name urxvtq | grep 'WM_COMMAND' | awk -F ',' '{print $3}' | awk -F '"' '{print $2}')
if [ -z "$wid" ]; then
  /path/to/urxvtc -name urxvtq -geometry 200x28
  wid=$(xprop -name urxvtq | grep 'WM_COMMAND' | awk -F ',' '{print $3}' | awk -F '"' '{print $2}')
  xdotool windowfocus "$wid"
  xdotool key Control_L+l
else
  if [ -z "$(xprop -id "$wid" | grep 'window state: Normal' 2>/dev/null)" ]; then
    xdotool windowmap "$wid"
    xdotool windowfocus "$wid"
  else
    xdotool windowunmap "$wid"
  fi
fi

```

Убедитесь, что вы измените `/путь/к/urxvtc` к фактическому путю скриптлета `urxvtc`, что вы сохранили выше. Мы будем использовать `urxvtc` чтобы запустить как обычные экземпляры `urxvt` и экземпляр как kuake.

### urxvtq с табуляцией

Если вы хотите, чтобы вкладки были как в kuake `urxvtc` (здесь называется `urxvtq`) просто замените третью строчку в `urxvtq`:

```
wid=$(xdotool search --name urxvtq)

```

на:

```
wid=$(xdotool search --name urxvtq | grep -m 1 "" )

```

Для активации поддержки вкладок, вы можете либо заменить пятую строку вашего `urxvtq`:

```
/path/to/urxvtc -name urxvtq -geometry 80x28

```

на:

```
/path/to/urxvtc -name urxvtq -pe tabbed -geometry 80x28

```

или заменить эту строку вашего файла `~/.Xresources`:

```
URxvt.perl-ext-common: default,matcher

```

на

```
URxvt.perl-ext-common: default,matcher,tabbed

```

#### Управление Tab

| Горячие клавиши | Описание |
| Shift+Left | Переход на вкладку слева от текущей |
| Shift+Right | Переход на вкладку справа от текущей |
| Shift+Down | Создать новую вкладку |

Вы также можете использовать мышь для переключения вкладок щелкая по желаемой, и создавать новую вкладку, нажав на _[NEW].\\_

Чтобы закрыть вкладку, введите `exit` как будто вы нормально закрыли терминал.

### Настройка Openbox

Теперь добавьте следующие строки в раздел `<applications>` файла `~/.config/openbox/rc.xml`:

```
<application name="urxvtq">
   <decor>no</decor>
   <position force="yes">
     <x>center</x>
     <y>0</y>
   </position>
   <desktop>all</desktop>
   <layer>above</layer>
   <skip_pager>yes</skip_pager>
   <skip_taskbar>yes</skip_taskbar>
   <maximized>Horizontal</maximized>
</application>
```

и добавьте эти строки в разделе `<keyboard>`:

```
<keybind key="W-t">
  <action name="Execute">
    <command>/path/to/urxvtc</command>
  </action>
</keybind>
<keybind key="W-grave">
  <action name="Execute">
    <execute>/path/to/urxvtq</execute>
  </action>
</keybind>
```

Здесь тоже необходимо изменить строку `/path/to/*` (/путь/к/*) чтобы указать на сценарии, которые вы сохранили ранее. Сохраните файл, а затем перенастройте Openbox. Теперь вы можете запускать urxvt с `Super+T`, и переключать как консоль kuake с `Super+**`**` (ковычка на клавише "ё").

### Дальнейшая настройка

Преимущество этой настройки через скрипт Perl urxvt kuake, в том что Openbox предоставляет больше возможностей, привязки клавиш-модификаторов. Сценарий kuake захватывает все физические клавиши, независимо от любой комбинации модификаторов. Для полного диапазона возможностей прочтите [Openbox bindings documentation](http://openbox.org/wiki/Help:Bindings).

[Openbox per-app settings](http://openbox.org/wiki/Help:Applications) могут быть использованы для дальнейшей настройки поведения как консоль kuake (например, положение экрана, слой и т.д.). Вам возможно потребуется изменить параметр "geometry" в скриплете `urxvtq` для регулировки высоты консоли.

### Связанные сценарии

*   hbekel опубликовал обобщенную версию из `urxvtq` [here](https://bbs.archlinux.org/viewtopic.php?pid=550380#p550380) которая может быть использована для переключения любого приложения, используя [xdotool](https://www.archlinux.org/packages/?name=xdotool).
*   [http://www.jukie.net/~bart/blog/20070503013555](http://www.jukie.net/~bart/blog/20070503013555) - Сценарий для открытия URL-адреса с помощью клавиатуры, а не мыши.

## Решение проблем

### Настройки ~/.Xresources не применяются

В некоторых случаях, когда _urxvt_ не признаёт `~/.Xresources`, вы можете добавить строку `xrdb -merge ~/.Xresources` в ваш файл `~/.xinitrc`. Для получения дополнительной информации смотрите статью [Ресурсы Х](/index.php/%D0%A0%D0%B5%D1%81%D1%83%D1%80%D1%81%D1%8B_%D0%A5 "Ресурсы Х").

### Прозрачность не работает после обновления, начиная с версии 9.09

Разработчики rxvt-Unicode удалили код совместимости для многих нестандартных установщиков обоев с этим обновлением. Использование несовместимых установщиков обоев, ломает поддержку прозрачности. Рекомендуемые установщики обоев:

*   [feh](/index.php/Feh "Feh")
*   hsetroot
*   esetroot

Для того, чтобы работала истинная прозрачность, убедитесь что закомментированы URxvt.tintColor и URxvt.inheritPixmap.

### Удаленные хосты

Если вы заходите на удаленный хост, вы можете столкнуться с проблемами при запуске программ в текстовм режиме под rxvt-Unicode. Это может быть исправлено путем установки [rxvt-unicode-terminfo](https://www.archlinux.org/packages/?name=rxvt-unicode-terminfo) на удаленном хосте или с помощью копирования, `/usr/share/terminfo/r/rxvt-unicode` с локального компьютера на ваш хост в `~/.terminfo/r/rxvt-unicode`; тоже самое для rxvt-unicode-256color.

Некоторые удаленные системы не изменяют название автоматически, если вы не укажете TERM=xterm. Чтобы решить этот вопрос, добавьте на удалённой машине в .bashrc строку:

```
PROMPT_COMMAND='echo -ne "\033]0;${USER}@${HOSTNAME}:${PWD}\007"'

```

### Использование rxvt-Unicode в качестве терминала gmrun (Gnome Completion-Run)

В отличие от некоторых других терминалов, urxvt ожидает аргументы `-e` определённые отдельно, а не сгруппированные вместе с кавычками. Это вызывает проблемы с [gmrun](/index.php/Gmrun "Gmrun"), который предполагает противоположное поведение. Это можно обойти, указав "eval" перед значением терминала в `.gmrunrc`:

```
Terminal = eval urxvt
TermExec = ${Terminal} -e

```

(gmrun использует `/bin/sh` чтобы выполнять команды, так что "eval" здесь понимается.) "eval" имеет побочный эффект "разрыва" аргументов `-e` таким же образом, что `$@` делает в [Bash](/index.php/Bash "Bash"), что делает команды понятными для urxvt.

### Моя цифровая клавиатура действует странно и производит странный вывод (например, в VIM)

Кажется есть проблема у некоторых пользователей Debian GNU/Linux, хотя никаких конкретных подробностей не сообщалось до сих пор. Вполне возможно, что это вызвано установкой неправильного TERM, хотя подробностей как это может произойти неизвестно, как TERM=rxvt должен предложить совместимую раскладку. Смотрите ответ на предыдущий вопрос, и, пожалуйста, сообщите если это помогло.

Тем не менее, с помощью программы _xmodmap_ ([xorg-xmodmap](https://www.archlinux.org/packages/?name=xorg-xmodmap)), вы можете переназначить клавиши цифровой клавиатуры обратно.

1\. Проверьте, что ваш keycode цифровой клавиатры (numpad) генерируется с поомщью программы `xev`.

*   Запустите программу `xev`
*   Нажмите цифру на вашей цифровой клавиатуре, смотрите _... keycode xxx ..._ в выводе `xev`. Например, клавиша 1 на моей клавиатуре также известна как калавиша "End", что имеет '**keycode 87'**.

2\. Создайте или измените ваш файл xmodmap, обычно `~/.Xmodmap`, с содержимым, представляющим свой код клавиш.

Пример Xmodmap файла с номером keycode:

```
keycode 63 = KP_Multiply
keycode 79 = Home KP_7
keycode 80 = Up KP_8
keycode 81 = Prior KP_9
keycode 82 = KP_Subtract
keycode 83 = Left KP_4
keycode 84 = KP_5
keycode 85 = Right KP_6
keycode 86 = KP_Add
keycode 87 = End KP_1
keycode 88 = Down KP_2
keycode 89 = Next KP_3
keycode 90 = Insert KP_0
keycode 91 = Delete KP_Decimal
keycode 112 = Prior
keycode 117 = Next
```

3\. Загрузите ваш файл xmodmap при запуске X сессии.

Например добавьте в файл `~/.xinitrc`:

```
...
xmodmap ~/.Xmodmap
...

```

### pseudo-tty

Следующая ошибка, скорее всего, вызвана `/dev/pts`, будучи смонтированным с неправильными опциями.

```
urxvt: cannot initialize pseudo-tty, aborting.

```

Удалите `/dev/pts` из `/etc/fstab` и исправьте текущие опции монтирования на:

```
sudo mount -o remount,gid=5,mode=620 /dev/pts

```

Смотрите также [[8]](https://mailman.archlinux.org/pipermail/arch-dev-public/2013-August/025332.html), [FS#36548](https://bugs.archlinux.org/task/36548), и [[9]](https://bbs.archlinux.org/viewtopic.php?pid=1318127).

### Горячие клавиши не работают

Смотрите [Get Alt key to work in terminal](http://vim.wikia.com/wiki/Get_Alt_key_to_work_in_terminal?useskin=monobook).

### Низкая производительность при рисовании глифов

Некоторые программы, такие как alsamixer и xprop не хорошо выполняются с некоторыми графическими драйверами, и как следствие перерисовывают очень медленно. Опция "skipBuiltinGlyphs" в `~/.Xresources` или параметр командной строки `-sbg` может это исправить. Одним из возможных решений является добавление следующей строки в `~/.Xresources`:

```
URxvt*skipBuiltinGlyphs:    true

```

## Внешние ресурсы

*   [rxvt-unicode](http://software.schmorp.de/pkg/rxvt-unicode.html) - Официальный сайт
*   [Source Code](http://cvs.schmorp.de/rxvt-unicode/) - Browseable CVS
*   [rxvt-unicode FAQ](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod) - Оффициальные ЧАВО
*   [rxvt-unicode Reference](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.1.pod) - Официальная страница руководства
*   [urxvtperl](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/src/urxvt.pm) - Официальная справка расширений Perl