**Состояние перевода:** На этой странице представлен перевод статьи [Zsh](/index.php/Zsh "Zsh"). Дата последней синхронизации: 7 февраля 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Zsh&diff=0&oldid=419352).

[Zsh](http://zsh.sourceforge.net/Intro/intro_1.html) является мощной современной оболочкой, которая работает как в интерактивном режиме, так и в качестве интерпретатора языка сценариев. Он совместим с [bash](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bash (Русский)") (не по умолчанию, только в режиме `emulate sh`), но имеет преимущества, такие как улучшенное [завершение](http://zsh.sourceforge.net/Guide/zshguide06.html) и [подстановка](http://zsh.sourceforge.net/Doc/Release/Expansion.html).

Еще больше причин, по которым стоит использовать Zsh, перечислено в [Zsh FAQ EN](http://zsh.sourceforge.net/FAQ/zshfaq01.html#l4).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [1.1 Первоначальная настройка](#.D0.9F.D0.B5.D1.80.D0.B2.D0.BE.D0.BD.D0.B0.D1.87.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [1.2 Установка Zsh в качестве оболочки по умолчанию](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Zsh_.D0.B2_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E)
*   [2 Файлы Запуска/Завершения](#.D0.A4.D0.B0.D0.B9.D0.BB.D1.8B_.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0.2F.D0.97.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D1.8F)
*   [3 Настройка Zsh](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Zsh)
    *   [3.1 Простой .zshrc](#.D0.9F.D1.80.D0.BE.D1.81.D1.82.D0.BE.D0.B9_.zshrc)
    *   [3.2 Настройка переменной $PATH](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D0.B5.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE.D0.B9_.24PATH)
    *   [3.3 Автозавершение команд](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4)
    *   [3.4 Хук "Команда не найдена"](#.D0.A5.D1.83.D0.BA_.22.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.B0_.D0.BD.D0.B5_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD.D0.B0.22)
    *   [3.5 Игнорирование повторяющихся строк в истории](#.D0.98.D0.B3.D0.BD.D0.BE.D1.80.D0.B8.D1.80.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.B2.D1.82.D0.BE.D1.80.D1.8F.D1.8E.D1.89.D0.B8.D1.85.D1.81.D1.8F_.D1.81.D1.82.D1.80.D0.BE.D0.BA_.D0.B2_.D0.B8.D1.81.D1.82.D0.BE.D1.80.D0.B8.D0.B8)
    *   [3.6 Команда ttyctl](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.B0_ttyctl)
    *   [3.7 Назначение клавиш](#.D0.9D.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
        *   [3.7.1 Назначение клавиш в оболочке](#.D0.9D.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_.D0.B2_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B5)
        *   [3.7.2 Назначение клавиши в ncurses](#.D0.9D.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.B2_ncurses)
        *   [3.7.3 Альтернативный путь назначения клавиш в ncurses](#.D0.90.D0.BB.D1.8C.D1.82.D0.B5.D1.80.D0.BD.D0.B0.D1.82.D0.B8.D0.B2.D0.BD.D1.8B.D0.B9_.D0.BF.D1.83.D1.82.D1.8C_.D0.BD.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_.D0.B2_ncurses)
        *   [3.7.4 Горячие клавиши в файловом менеджере](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_.D0.B2_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D0.BE.D0.BC_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B5)
    *   [3.8 История поиска](#.D0.98.D1.81.D1.82.D0.BE.D1.80.D0.B8.D1.8F_.D0.BF.D0.BE.D0.B8.D1.81.D0.BA.D0.B0)
    *   [3.9 Настройка строки приглашения (PROMPT)](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8_.D0.BF.D1.80.D0.B8.D0.B3.D0.BB.D0.B0.D1.88.D0.B5.D0.BD.D0.B8.D1.8F_.28PROMPT.29)
    *   [3.10 Настройка командной строки (PROMPT)](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.BD.D0.BE.D0.B9_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B8_.28PROMPT.29)
        *   [3.10.1 Цвета](#.D0.A6.D0.B2.D0.B5.D1.82.D0.B0)
        *   [3.10.2 Цветной вывод команд](#.D0.A6.D0.B2.D0.B5.D1.82.D0.BD.D0.BE.D0.B9_.D0.B2.D1.8B.D0.B2.D0.BE.D0.B4_.D0.BA.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4)
        *   [3.10.3 Пример](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80)
    *   [3.11 Стек Каталогов](#.D0.A1.D1.82.D0.B5.D0.BA_.D0.9A.D0.B0.D1.82.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.B2)
    *   [3.12 Команда Help](#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.B0_Help)
    *   [3.13 Подсветка синтаксиса как в Fish](#.D0.9F.D0.BE.D0.B4.D1.81.D0.B2.D0.B5.D1.82.D0.BA.D0.B0_.D1.81.D0.B8.D0.BD.D1.82.D0.B0.D0.BA.D1.81.D0.B8.D1.81.D0.B0_.D0.BA.D0.B0.D0.BA_.D0.B2_Fish)
    *   [3.14 Примеры файла .zshrc](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.zshrc)
    *   [3.15 Фреймворки настроек](#.D0.A4.D1.80.D0.B5.D0.B9.D0.BC.D0.B2.D0.BE.D1.80.D0.BA.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
    *   [3.16 Автозапуск приложений](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [3.17 Постоянный rehash](#.D0.9F.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.BD.D1.8B.D0.B9_rehash)
*   [4 Функции](#.D0.A4.D1.83.D0.BD.D0.BA.D1.86.D0.B8.D0.B8)
    *   [4.1 Распаковка архива](#.D0.A0.D0.B0.D1.81.D0.BF.D0.B0.D0.BA.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B0.D1.80.D1.85.D0.B8.D0.B2.D0.B0)
    *   [4.2 Упаковка в архив](#.D0.A3.D0.BF.D0.B0.D0.BA.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B2_.D0.B0.D1.80.D1.85.D0.B8.D0.B2)
*   [5 Удаление](#.D0.A3.D0.B4.D0.B0.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5)
*   [6 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Перед установкой вы можете посмотреть, какая оболочка используется в данный момент:

```
$ echo $SHELL

```

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%B8%D1%82%D0%B5 "Установите") пакет [zsh](https://www.archlinux.org/packages/?name=zsh). Чтобы значительно расширить возможности автодополнения команд, установите также пакет [zsh-completions](https://www.archlinux.org/packages/?name=zsh-completions).

### Первоначальная настройка

Убедитесь, что Zsh был установлен правильно, выполнив следующую команду в терминале:

```
$ zsh

```

После этого вы должны увидеть скрипт *zsh-newuser-install*, который проведет вас через некоторые основные настройки. Если вы хотите пропустить первичную настройку, нажмите `q`. Если скрипт не запустился, вы можете вызвать его вручную:

```
$ zsh /usr/share/zsh/functions/Newuser/zsh-newuser-install -f

```

### Установка Zsh в качестве оболочки по умолчанию

Смотрите раздел [Командная оболочка#Выбор оболочки по умолчанию](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%BD%D0%B0%D1%8F_%D0%BE%D0%B1%D0%BE%D0%BB%D0%BE%D1%87%D0%BA%D0%B0#.D0.92.D1.8B.D0.B1.D0.BE.D1.80_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8_.D0.BF.D0.BE_.D1.83.D0.BC.D0.BE.D0.BB.D1.87.D0.B0.D0.BD.D0.B8.D1.8E "Командная оболочка").

**Совет:** При замене [bash](https://www.archlinux.org/packages/?name=bash) пользователь может перенести некоторые участки кода из `~/.bashrc` в `~/.zshrc` (например, приглашение командной строки и [псевдонимы](/index.php/Bash_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.BB.D0.B8.D0.B0.D1.81.D1.8B "Bash (Русский)")), а также из `~/.bash_profile` в `~/.zprofile` (например, [код, который запускает оконную систему X](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_X_.D0.BF.D1.80.D0.B8_.D0.B2.D1.85.D0.BE.D0.B4.D0.B5_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83 "Xinitrc (Русский)"))

## Файлы Запуска/Завершения

**Совет:** Смотрите [Руководство пользователя Z-Shell](http://zsh.sourceforge.net/Guide/zshguide02.html), информацию о интерактивном входе в оболочку, и что включать в Ваш автозапуск.

**Примечание:**

*   Если `$ZDOTDIR` не определена, используется `$HOME` по умолчанию.
*   Если опция `RCS` не установлена ни в одном из файлов, файлы конфигурации не будут получены после этого файла.
*   Если опция `GLOBAL_RCS` не задана ни в одном из файлов, после этого файла не будут найдены глобальные конфигурационные файлы (`/etc/zsh/*`).

При запуске Zsh по умолчанию он будет загружать следующие файлы в этом порядке:

	`/etc/zsh/zshenv`

	Используется для установки общесистемных переменных [environment variables (Русский)](/index.php/Environment_variables_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Environment variables (Русский)"); Он не должен содержать команд, которые производят вывод, или предполагает, что shell подключен к tty. Этот файл ***всегда*** будет источником, это нельзя переопределить.

	`$ZDOTDIR/.zshenv`

	Используется для установки переменных среды пользователя; Он не должен содержать команд, которые производят вывод, или предполагает, что shell подключен к tty. Этот файл ***всегда*** будет источником.

	`/etc/zsh/zprofile`

	Используется для выполнения команд при запуске, будет вызван при запуске как ***login shell***. Обратите внимание, что в Arch Linux по умолчанию в нем содержится [одна строка](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh), в которой источником является `/etc/profile`.

	`/etc/profile`

	Этот файл должен быть загружен всеми Bourne-совместимыми оболочками при входе в систему: он устанавливает `$PATH` и другие переменные окружения и специфичные для приложения (`/etc/profile.d/*.sh`) при входе в систему.

	`$ZDOTDIR/.zprofile`

	Используется для выполнения пользовательских команд при запуске, будет вызван при запуске как ***login shell***.

	`/etc/zsh/zshrc`

	Используется для настройки интерактивной конфигурации оболочки и выполнения команд, будет вызван при запуске как ***interactive shell***.

	`$ZDOTDIR/.zshrc`

	Используется для настройки интерактивной конфигурации пользователя и выполнения команд, будет вызван при запуске как ***interactive shell***.

	`/etc/zsh/zlogin`

	Используется для выполнения команд при завершении прогресса инициализации, будет вызван при запуске как ***login shell***.

	`$ZDOTDIR/.zlogin`

	Используется для выполнения пользовательских команд при завершении начального прогресса, будет вызван при запуске как ***login shell***.

	`$ZDOTDIR/.zlogout`

	Будет получен, когда ***login shell*** **завершится**.

	`/etc/zsh/zlogout`

	Будет получен, когда ***login shell*** **завершится**.

**Примечание:**

*   Пути, используемые в пакете Arch [zsh](https://www.archlinux.org/packages/?name=zsh), отличаются от используемых по умолчанию в [man pages](/index.php/Man_page "Man page") ([FS#48992](https://bugs.archlinux.org/task/48992)).
*   `/etc/profile` не является частью обычного списка запускаемых файлов Zsh, но поступает из `/etc/zsh/zprofile` в пакете [zsh](https://www.archlinux.org/packages/?name=zsh). Пользователи должны принять во внимание, что `/etc/profile` устанавливает переменную `$PATH` которая перезапишет любую переменную `$PATH` установленную в `$ZDOTDIR/.zshenv`. Чтобы это предотвратить, установите переменную `$PATH` в `$ZDOTDIR/.zprofile`.

**Важно:** Не рекомендуется заменять стандартную [одну строку](https://projects.archlinux.org/svntogit/packages.git/tree/trunk/zprofile?h=packages/zsh) в `/etc/zsh/zprofile` с чем-то другим, это нарушит целостность других пакетов, которые предоставляют некоторые сценарии в `/etc/profile.d`.

## Настройка Zsh

Хотя Zsh может использоваться “из коробки”, он настроен не так, как хотело бы большинство пользователей. Из-за наличия огромных возможностей настройки, доступных в Zsh, этот процесс может оказаться сложным и трудоемким.

### Простой .zshrc

Ниже приведён пример файла настроек, который обеспечивает достойный набор опций по умолчанию, а также предоставляет примеры многих вариантов настройки Zsh. Для того, чтобы использовать этот пример, сохраните его в виде файла с именем `.zshrc`.

**Совет:** Чтобы применить изменения не завершая сеанс, выполните команду `source ~/.zshrc`

Вот простой `.zshrc`:

 `~/.zshrc` 
```
autoload -U compinit promptinit
compinit
promptinit

# Эта настройка установит тему walters для приглашения командной строки
prompt walters
```

### Настройка переменной $PATH

Информацию о настройке в *zsh* системных путей отдельно для каждого пользователя можно найти [на странице проекта](http://zsh.sourceforge.net/Guide/zshguide02.html#l24). Вкратце, добавьте в файл `~/.zshenv` следующие строки:

 `~/.zshenv` 
```
typeset -U path
path=(~/bin /other/things/in/path $path[@])
```

Смотрите также примечание в разделе [#Фреймворки настроек](#.D0.A4.D1.80.D0.B5.D0.B9.D0.BC.D0.B2.D0.BE.D1.80.D0.BA.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA).

### Автозавершение команд

Возможно, наиболее убедительной стороной Zsh является его передовые возможности автозавершения. Включите автозавершение в `.zshrc`. Добавив следующую строку в ваш `~/.zshrc`:

 `~/.zshrc` 
```
autoload -U compinit
compinit

```

Настройки выше включают в себя также ssh/scp/sftp завершения хостов, но для того, чтобы эта функция работала, пользователи должны предотвратить SSH от хеширования хостов имён в `~/.ssh/known_hosts`.

**Важно:** Это делает компьютер уязвимым для["Island-hopping" атак](http://blog.rootshell.be/2010/11/03/bruteforcing-ssh-known_hosts-files/). В этом случае, закоментируйте следующую строку или установите значение
```
`no`:

```
 `/etc/ssh/ssh_config`  `#HashKnownHosts yes` 

И поместите `~/.ssh/known_hosts` где-то еще, так что ssh создаст новый с un-hashed хостами (ранее известные хосты, таким образом, будут утеряны). Для получения более подробной информации смотрите тут [кэшированные-хосты](http://nms.lcs.mit.edu/projects/ssh/README.hashed-hosts).

Для автозавершения с использованием клавиши-стрелки, добавьте следующие строки в:

 `~/.zshrc`  `zstyle ':completion:*' menu select` 

	*Для активации меню нажмите TAB дважды.*

Для автозавершения командной строки для алиасов (псевдонимов), добавьте следующее:

 `~/.zshrc`  `setopt completealiases` 

Позволяем разворачивать сокращенный ввод, к примеру cd /u/sh в /usr/share

 `~/.zshrc`  `autoload -U compinit && compinit` 

### Хук "Команда не найдена"

Смотрите [pkgfile (Русский)#Команда не найдена](/index.php/Pkgfile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9A.D0.BE.D0.BC.D0.B0.D0.BD.D0.B4.D0.B0_.D0.BD.D0.B5_.D0.BD.D0.B0.D0.B9.D0.B4.D0.B5.D0.BD.D0.B0 "Pkgfile (Русский)").

### Игнорирование повторяющихся строк в истории

Чтобы игнорировать повторяющиеся строки в истории, используйте следующее:

 `~/.zshrc`  `setopt HIST_IGNORE_DUPS` 

Чтобы освободить историю от уже созданных дубликатов, запустите:

```
$ sort -t ";" -k 2 -u ~/.zsh_history | sort -o ~/.zsh_history

```

### Команда ttyctl

[[1]](http://zsh.sourceforge.net/Doc/Release/Shell-Builtin-Commands.html#index-tty_002c-freezing) описывает `ttyctl` команды в Zsh. Это можно применить для "замораживания / размораживания" терминала. Многие программы изменяют состояние терминала, и часто не восстанавливают настройки терминала нормально при выходе. Чтобы избежать необходимости вручную сбрасывать терминал, используйте следующее:

 `~/.zshrc`  `ttyctl -f` 

### Назначение клавиш

Zsh не использует Readline, вместо этого он использует свой собственный и более мощный ZLE. Т.е. не читает `/etc/inputrc` или `~/.inputrc`. Zle имеет [emacs](/index.php/Emacs "Emacs") режим и [vi](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Vim (Русский)") режим. По умолчанию, он пытается взять клавиши emacs или vi из переменной среды `$EDITOR`. Если она пуста, то по умолчанию будет Emacs. Измните это `bindkey -e` или `bindkey -v` соответственно в режиме Emacs или режиме VI.

Смотрите также [zshwiki: bindkeys](http://zshwiki.org/home/zle/bindkeys).

#### Назначение клавиш в оболочке

Настраиваем нормальное поведение клавиш (не как в vi и emacs). Для этого в ~/.zshrc добавьте следующее:

```
[[ -n "${key[Home]}"     ]]  && bindkey  "${key[Home]}"     beginning-of-line
[[ -n "${key[End]}"      ]]  && bindkey  "${key[End]}"      end-of-line
[[ -n "${key[Insert]}"   ]]  && bindkey  "${key[Insert]}"   overwrite-mode
[[ -n "${key[Delete]}"   ]]  && bindkey  "${key[Delete]}"   delete-char
[[ -n "${key[Up]}"       ]]  && bindkey  "${key[Up]}"       up-line-or-history
[[ -n "${key[Down]}"     ]]  && bindkey  "${key[Down]}"     down-line-or-history
[[ -n "${key[Left]}"     ]]  && bindkey  "${key[Left]}"     backward-char
[[ -n "${key[Right]}"    ]]  && bindkey  "${key[Right]}"    forward-char
[[ -n "${key[PageUp]}"   ]]  && bindkey  "${key[PageUp]}"   beginning-of-buffer-or-history
[[ -n "${key[PageDown]}" ]]  && bindkey  "${key[PageDown]}" end-of-buffer-or-history

```

**Примечание:** Рекомендуем сделать так, как указано в этом подразделе.

#### Назначение клавиши в ncurses

Bind a ncurses application to a keystoke, but it will not accept interaction. Use `BUFFER` variable to make it work. The following example lets users open ncmpcpp using `Alt+\`:

 `~/.zshrc` 
```
ncmpcppShow() { BUFFER="ncmpcpp"; zle accept-line; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

#### Альтернативный путь назначения клавиш в ncurses

Этот метод будет содержать всё, что вы ввели в строку перед вызовом приложения

 `~/.zshrc` 
```
ncmpcppShow() { ncmpcpp <$TTY; zle redisplay; }
zle -N ncmpcppShow
bindkey '^[\' ncmpcppShow
```

#### Горячие клавиши в файловом менеджере

Могут пригодится настройки клавиш использующиеся в графическом файловом менеджере. Первая комбинация показывает историю каталогов (Alt + Left), вторая позволяет пользователю перейти в родительский каталог (Alt + Up). Они также отображают содержимое каталогов.

 `~/.zshrc` 
```
cdUndoKey() {
  popd      > /dev/null
  zle       reset-prompt
  echo
  ls
  echo
}

cdParentKey() {
  pushd .. > /dev/null
  zle      reset-prompt
  echo
  ls
  echo
}

zle -N                 cdParentKey
zle -N                 cdUndoKey
bindkey '^[[1;3A'      cdParentKey
bindkey '^[[1;3D'      cdUndoKey

```

### История поиска

Добавьте эти строки в .zshrc

 `~/.zshrc` 
```
[[ -n "${key[PageUp]}"   ]]  && bindkey  "${key[PageUp]}"    history-beginning-search-backward
[[ -n "${key[PageDown]}" ]]  && bindkey  "${key[PageDown]}"  history-beginning-search-forward

```

Doing this, only past commands beginning with the current input would have been shown.

### Настройка строки приглашения (PROMPT)

Существует быстрый и легкий способ создать цветное приглашение в Zsh. Убедитесь что prompt установлен в autoload в файле `.zshrc`. Это может быть сделано путем добавления этих строк:

 `~/.zshrc` 
```
autoload -U promptinit
promptinit

```

Доступные цветовые схемы можно перечислить с помощью команды:

```
$ prompt -l

```

Для просмотра всех доступных тем (с примерами), используйте команду:

```
$ prompt -p

```

Например, чтобы использовать цветовую схему `bigfade`, введите:

```
$ prompt bigfade

```

Чтобы использовать цветовую схему с заданным цветом (если доступен в теме), введите:

```
$ prompt elite2 blue

```

### Настройка командной строки (PROMPT)

В отличие от bash zsh имеет два промта — левый и правый. Правый промт исчезает при вводе длинных команд, что делает его очень удобным для отображения не самой полезной информации, типа времени или текущего каталога. Промты настраиваются с помощью переменных PROMPT (левый) и RPROMPT (правый):

export PROMPT='%n@%m> ' export RPROMPT='[%~]'

Некоторые из специальных последовательностей, которые можно в них использовать: Последовательность - Описание %n - Имя пользователя %m - Имя компьютера (до первой точки) %M - Полное имя компьютера %~ - Путь к текущему каталогу относительно домашнего %d - Полный путь к текущей директории ($PWD) %T - Время в формате HH:MM %* - Время в формате HH:MM:SS %D - Дата в формате YY-MM-DD %B, %b - Начало и конец выделения жирным

По материалам [этой статьи](http://eax.me/zsh/)

#### Цвета

Zsh устанавливает цвета иначе, чем [Bash](/index.php/Color_Bash_Prompt "Color Bash Prompt"). Добавьте`autoload -U colors && colors` до `PROMPT=` в `.zshrc` чтобы воспользоваться. Usually you will want to put these inside `%{ [...] %}` so the cursor does not move.

`$fg[color]` будет установлен цвет текста (значения, подставляемые вместо “color”, к примеру: red, green, blue, и т.д.. - по умолчанию установлены в любом формате до текста)

| Команда | Описание |
| `%F{color} [...] %f` | фактически то же самое, что и предыдущий, но с меньшим набором. Можно также вставить префикс с номером F. |
| `$fg_no_bold[color]` | будет использоваться не толстый текст с заданным цветом. |
| `$fg_bold[color]` | будет использоваться толстый текст с заданным цветом. |
| `$reset_color` | сбросит цвет текста, на цвет по умолчанию. Не сбрасывает толщину текста. Используйте `%b` для отмены утолщения. Saves typing if it's just `%f` though. |
| `%K{color} [...] %k` | устанавливает цвет фона. Того же цвета, как цвет без текста полужирным. Prefixing with any single-digit number makes the bg black. |

| Возможные значения цвета |
| `black` или `0` | `red` или `1` |
| `green` или `2` | `yellow` или `3` |
| `blue` или `4` | `magenta` или `5` |
| `cyan` или `6` | `white` или `7` |

**Note:** Утолщённый текст не обязательно использовать тогоже цвета что и обычный. Например, `$fg['yellow']` выглядит коричневым или очень темно-желтым, в то время как `$fg_bold['yellow']` выглядит ярче или как обычный жёлтый.

#### Цветной вывод команд

Раскрашивание вывода команд при помощи скрипта grc. Поставьте пакет [grc](https://aur.archlinux.org/packages/grc/) (доступен для установки из репозитория [community]) И добавьте следующие строки в ваш `~/.zshrc`

```
if [ -f /usr/bin/grc ]; then
 alias gcc="grc --colour=auto gcc"
 alias irclog="grc --colour=auto irclog"
 alias log="grc --colour=auto log"
 alias netstat="grc --colour=auto netstat"
 alias ping="grc --colour=auto ping"
 alias proftpd="grc --colour=auto proftpd"
 alias traceroute="grc --colour=auto traceroute"
fi

```

#### Пример

Это пример двустороннего промта:

```
PROMPT="%{$fg[red]%}%n%{$reset_color%}@%{$fg[blue]%}%m %{$fg_no_bold[yellow]%}%1~ %{$reset_color%}%#"
RPROMPT="[%{$fg_no_bold[yellow]%}%?%{$reset_color%}]"

```

А вот как оно будет отображаться:

```
username@host ~ %                                                         [0]

```

### Стек Каталогов

Zsh можно настроить, чтобы он помнил DIRSTACKSIZE (последние посещённые каталоги). Это пригодится для более быстрой работы с *cd*. Вам нужно добавить несколько строк, в файл настройки:

 `.zshrc` 
```
DIRSTACKFILE="$HOME/.cache/zsh/dirs"
if [[ -f $DIRSTACKFILE ]] && [[ $#dirstack -eq 0 ]]; then
  dirstack=( ${(f)"$(< $DIRSTACKFILE)"} )
  [[ -d $dirstack[1] ]] && cd $dirstack[1]
fi
chpwd() {
  print -l $PWD ${(u)dirstack} >$DIRSTACKFILE
}

DIRSTACKSIZE=20

setopt autopushd pushdsilent pushdtohome

## Удалить повторяющиеся записи
setopt pushdignoredups

## Это Отменяет +/- операторы.
setopt pushdminus

```

Теперь используйте

```
dirs -v

```

Для вывода стека директорий. Используйте `cd -<NUM>` чтобы вернуться к посещённому каталогу. Используйте автозавершение (нажав `TAB`) после тире.

**Примечание:** Это не будет работать, если у вас открыто более одной сессии *zsh*, и использование `cd`, приведёт к конфликту в обоих ссессиях пишущих в тот же файл.

### Команда Help

В отличие от [bash](/index.php/Bash "Bash"), *zsh* не позволяет использовать встроенный в `help` команду для автодополнения. Чтобы использовать `help` в zsh, добавьте следующие строки в ваш

```
`zshrc`:

```

```
autoload -U run-help
autoload run-help-git
autoload run-help-svn
autoload run-help-svk
unalias run-help
alias help=run-help
```

### Подсветка синтаксиса как в Fish

[Fish](/index.php/Fish_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Fish (Русский)") обеспечивает очень мощную подсветку синтаксиса. Для использования в zsh, вы можете установить [zsh-syntax-highlighting](https://www.archlinux.org/packages/?name=zsh-syntax-highlighting) из официального репозитория и обязательно добавьте в ваш `~/.zshrc` строку:

 `source /usr/share/zsh/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh` 

### Примеры файла .zshrc

*   Пакет [grml-zsh-config](https://www.archlinux.org/packages/?name=grml-zsh-config), доступный в официальном репозитории взятый с [http://grml.org/zsh](http://grml.org/zsh) содержит zshrc файл, который включает в себя множество настроек для Zshell. Эта настройка используется по умолчанию для [ежемесячного ISO релиза](https://www.archlinux.org/download/).
*   Базовая настройка с динамической строкой приглашения (Prompt) и заголовком окна / Hardinfo => [http://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc](http://github.com/MrElendig/dotfiles-alice/blob/master/.zshrc);
*   [https://github.com/slashbeast/things/blob/master/configs/DOTzshrc](https://github.com/slashbeast/things/blob/master/configs/DOTzshrc) - zshrc с несколькими функциями, - смотрите комментарии в файле. Известные особенности: подтверждение выключения, если пользователь запустил poweroff, а также запрос подтверждения на reboot или hibernate, поддержка GIT в Prompt (сделано без vcsinfo), завершение по TAB с меню, вывод текущей выполняемой команды в заголовке окна, и многое другое.

### Фреймворки настроек

*   [oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh) управляемый сообществом, популярный фреймворк для настройки вашего Zsh. Он поставляется в комплекте с тонной полезных функций, помощников, плагинов, тем.
*   [Prezto - мгновенно прекрасный Zsh](https://github.com/sorin-ionescu/prezto) (доступен в [prezto-git](https://aur.archlinux.org/packages/prezto-git/)) настроенный фреймворк Zsh. Он поставляется с модулями, разумно расширяющих среду интерфейса командной строки (по умолчанию), псевдонимами (алиасами), функциями, атодополнением, и темами Prompt.
*   [Antigen](https://github.com/zsh-users/antigen) (дступен в [antigen-git](https://aur.archlinux.org/packages/antigen-git/)) - менеджер плагинов для zsh, вдохновлённый oh-my-zsh и vundle.

### Автозапуск приложений

**Примечание:** `$ZDOTDIR` по умолчанию `$HOME`

Zsh всегда выполняет `/etc/zsh/zshenv` и `$ZDOTDIR/.zshenv` так что не раздувайте эти файлы.

При входе в оболочку, читаются команды из `/etc/profile` а потом `$ZDOTDIR/.zprofile`. Затем, если оболочка является интерактивной, команды читаются из `/etc/zsh/zshrc` а потом `$ZDOTDIR/.zshrc`. Наконец, если в оболочку выполнен вход, читаются `/etc/zsh/zlogin` и `$ZDOTDIR/.zlogin`.

Смотрите также секцию *STARTUP/SHUTDOWN FILES* в [zsh(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/zsh.1).

### Постоянный rehash

Обычно compinit не находит новые исполняемые файлы в $PATH. Например после установки нового пакета, файлы в /usr/bin не сразу будут включены в автодополнение. Чтобы включить их в работу, выполните:

```
$ rehash

```

'rehash' может выполняться автоматически. Включите его в вашем `zshrc`:

 `~/.zshrc`  `zstyle ':completion:*' rehash true` 
**Примечание:** Эта фишка была найдена в PR для Oh My Zsh [[2]](https://github.com/robbyrussell/oh-my-zsh/issues/3440)

## Функции

Zsh позволяет пользователю определять собственные функции, которые могут выполняться точно также как и обычные программы. Функции выполняются в том же процессе, что и вызвавшая их программа. При вызове функции аргументы передаются как позиционные параметры.

### Распаковка архива

Чтобы распаковать архив не указывая тип распаковщика и его аркументы, а выполнив всего лишь команду вида `ex имя_архива.bz2` Добавьте следующий код в `~/.zshrc`

```
ex () {
 if [ -f $1 ] ; then
   case $1 in
     *.tar.bz2) tar xvjf $1   ;;
     *.tar.gz)  tar xvzf $1   ;;
     *.tar.xz)  tar xvfJ $1   ;;
     *.bz2)     bunzip2 $1    ;;
     *.rar)     unrar x $1    ;;
     *.gz)      gunzip $1     ;;
     *.tar)     tar xvf $1    ;;
     *.tbz2)    tar xvjf $1   ;;
     *.tgz)     tar xvzf $1   ;;
     *.zip)     unzip $1      ;;
     *.Z)       uncompress $1 ;;
     *.7z)      7z x $1       ;;
     *)         echo "'$1' Не может быть распакован при помощи >ex<" ;;
   esac
 else
   echo "'$1' не является допустимым файлом"
 fi
}

```

### Упаковка в архив

Упаковка в архив командой `pk 7z /что/мы/пакуем имя_файла.7z` - при этом архив будет в Домашней папке.

```
pk () {
if [ $1 ] ; then
case $1 in
tbz)       tar cjvf $2.tar.bz2 $2      ;;
tgz)       tar czvf $2.tar.gz  $2       ;;
tar)      tar cpvf $2.tar  $2       ;;
bz2)    bzip $2 ;;
gz)        gzip -c -9 -n $2 > $2.gz ;;
zip)       zip -r $2.zip $2   ;;
7z)        7z a $2.7z $2    ;;
*)         echo "'$1' не может быть упакован с помощью pk()" ;;
esac
else
echo "'$1' не является допустимым файлом"
fi
}

```

## Удаление

Измените оболочку по умолчанию перед удалением пакета [zsh](https://www.archlinux.org/packages/?name=zsh).

**Важно:** Несоблюдение процедуры ниже, может привести пользователя к невозможности получить доступ к рабочей оболочке .

Запустите следующую команду:

```
$ chsh -s /bin/bash *user*

```

Где *user* - имя пользователя.

Используйте эту команду для каждого пользователя с установленной оболочкой *zsh* (в том числе и root при необходимости). После, удалите пакет [zsh](https://www.archlinux.org/packages/?name=zsh).

Кроме того, изменить оболочку по умолчанию обратно в Bash, можно редактируя `/etc/passwd` от root.

**Важно:** Настоятельно рекомендуется использовать `vipw` когда редактируете `/etc/passwd` это помогает предотвратить неверные записи и/или ошибки синтаксиса.

Например, изменить следующие:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/zsh

```

На:

```
*username*:x:1000:1000:*Full Name*,,,:/home/*username*:/bin/**bash**

```

## Смотрите также

Рекомендуем обязательно обратится к следующим Русскоязычным статьям, для более полного и лучшего понимания.

*   [Делаем из Zsh мороженку](http://dobroserver.ru/delaem-iz-zsh-morozhenku)
*   [Советы по настройке Zsh](http://www.altlinux.org/DotFiles/Shells/Zsh/%D0%A1%D0%BE%D0%B2%D0%B5%D1%82%D1%8B#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8.D0.B3.D0.BB.D0.B0.D1.88.D0.B5.D0.BD.D0.B8.D1.8F)
*   [Cправочная карта Zsh (PDF)](http://alexott.net/ru/writings/zsh/zsh-refcard.pdf)

Статьи на Английском:

*   [A User's Guide to ZSH](http://zsh.sourceforge.net/Guide/zshguide.html)
*   [The Z Shell Manual](http://zsh.sourceforge.net/Doc/Release/index-frame.html) (different format available [here](http://zsh.sourceforge.net/Doc/))
*   [Zsh FAQ](http://zsh.sourceforge.net/FAQ/zshfaq01.html)
*   [zsh-lovers(1)](http://grml.org/zsh/zsh-lovers.html) (this is also available as [zsh-lovers](https://www.archlinux.org/packages/?name=zsh-lovers) in offical repository)
*   [Zsh Wiki](http://zshwiki.org/home/)
*   [Gentoo Wiki: Zsh/HOWTO](https://wiki.gentoo.org/wiki/Zsh/HOWTO)
*   [Bash2Zsh Reference Card](http://www.bash2zsh.com/zsh_refcard/refcard.pdf)