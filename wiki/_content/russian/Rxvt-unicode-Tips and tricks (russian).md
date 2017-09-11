**Состояние перевода:** На этой странице представлен перевод статьи [rxvt-unicode/Tips and tricks](/index.php/Rxvt-unicode/Tips_and_tricks "Rxvt-unicode/Tips and tricks"). Дата последней синхронизации: 12 марта 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Rxvt-unicode/Tips_and_tricks&diff=0&oldid=425316).

Смотрите главную статью [rxvt-unicode](/index.php/Rxvt-unicode_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Rxvt-unicode (Русский)").

## Contents

*   [1 Улучшенное поведение как в Kuake, Openbox](#.D0.A3.D0.BB.D1.83.D1.87.D1.88.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D0.BF.D0.BE.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.B0.D0.BA_.D0.B2_Kuake.2C_Openbox)
    *   [1.1 Скриплеты](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D0.BB.D0.B5.D1.82.D1.8B)
    *   [1.2 urxvtq с табуляцией](#urxvtq_.D1.81_.D1.82.D0.B0.D0.B1.D1.83.D0.BB.D1.8F.D1.86.D0.B8.D0.B5.D0.B9)
        *   [1.2.1 Управление Tab](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_Tab)
    *   [1.3 Настройка Openbox](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Openbox)
    *   [1.4 Дальнейшая настройка](#.D0.94.D0.B0.D0.BB.D1.8C.D0.BD.D0.B5.D0.B9.D1.88.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [1.5 Связанные сценарии](#.D0.A1.D0.B2.D1.8F.D0.B7.D0.B0.D0.BD.D0.BD.D1.8B.D0.B5_.D1.81.D1.86.D0.B5.D0.BD.D0.B0.D1.80.D0.B8.D0.B8)
*   [2 Повышение производительности](#.D0.9F.D0.BE.D0.B2.D1.8B.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8)
    *   [2.1 Демон-клиент](#.D0.94.D0.B5.D0.BC.D0.BE.D0.BD-.D0.BA.D0.BB.D0.B8.D0.B5.D0.BD.D1.82)
        *   [2.1.1 Xinitrc](#Xinitrc)
        *   [2.1.2 systemd](#systemd)
*   [3 Расширенное управление вкладками](#.D0.A0.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B2.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0.D0.BC.D0.B8)
*   [4 Прозрачность](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [4.1 Настоящая прозрачность](#.D0.9D.D0.B0.D1.81.D1.82.D0.BE.D1.8F.D1.89.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
    *   [4.2 Родная прозрачность](#.D0.A0.D0.BE.D0.B4.D0.BD.D0.B0.D1.8F_.D0.BF.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
*   [5 Набор иконок](#.D0.9D.D0.B0.D0.B1.D0.BE.D1.80_.D0.B8.D0.BA.D0.BE.D0.BD.D0.BE.D0.BA)
*   [6 Используйте urxvt для запуска приложений](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B9.D1.82.D0.B5_urxvt_.D0.B4.D0.BB.D1.8F_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
*   [7 Xterm escape sequences](#Xterm_escape_sequences)

## Улучшенное поведение как в Kuake, Openbox

Это первоначально разместил Xyne, на форуме [[1]](https://bbs.archlinux.org/viewtopic.php?pid=550380), и опирается на [xdotool](https://www.archlinux.org/packages/?name=xdotool) найденный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

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

Вы также можете использовать мышь для переключения вкладок щелкая по желаемой, и создавать новую вкладку, нажав на *[NEW].\\*

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

## Повышение производительности

*   Избегайте использования XFT шрифтов. Если есть необходимость в использовании XFT шрифтов, задайте занчени добавив `:antialias=false`.[[2]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod#Can_I_speed_up_Xft_rendering_somehow)
*   Соберите rxvt-unicode с отключением ненужных функций, `--disable-xft` и в частности `--disable-unicode3`.
*   Ограничьте количество `saveLines` (опция `-sl`)в буфере прокрутки, чтобы уменьшить использование памяти. [[4]](http://pod.tst.eu/http://cvs.schmorp.de/rxvt-unicode/doc/rxvt.7.pod#Isn_t_rxvt_unicode_supposed_to_be_sm)
    *   Используйте tmux для прокрутки буфера и установит saveLines в 0
*   [Отключите Perl](#.D0.9E.D1.82.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D1.88.D0.B8.D1.80.D0.B5.D0.BD.D0.B8.D0.B9_Perl)
*   Пользуйтесь демоном `urxvtd` запуская клиенты `urxvtc`.

### Демон-клиент

#### Xinitrc

Смотрите раздел *Примеры* в [urxvtd(1)](http://jlk.fjfi.cvut.cz/arch/manpages/man/urxvtd.1). Это предпочтительный вариант.

**Совет:** Добавьте в ваш `~/.xinitrc` строку:
```
urxvtd -q -f -o &

```

Перед строкой запуска вашего Окружения рабочего стола/Оконного менеджера. Перезапустите Х сервер.

Теперь запустите urxvt в качестве клиента, командой `urxvtc`

#### systemd

**Примечание:** Обычные пользователи не могут выполнять команды systemctl для управления питанием (reboot (перезагрузка), poweroff (выключение), и т.п.) когда вход в urxvt клиент/демон выполняется через systemd, так как клиент не является частью [cессии](/index.php/Session "Session"). По этой причине, запуск urxvt через Systemd не рекомендуется.

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
urxvtd@*username*.service

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
WantedBy=*MyTarget*.target

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

## Расширенное управление вкладками

Установите пакет [urxvt-tabbedex](https://aur.archlinux.org/packages/urxvt-tabbedex/) из [AUR](/index.php/AUR "AUR"), затем добавьте `tabbedex` значение в `URxvt.perl-ext-common` X resource в вашем `~/.Xresources`:

```
URxvt.perl-ext-common: ...,tabbedex,...

```

**Примечание:** Если вы ранее использовали `tabbed` расширение Perl и определили `tabbed` значение для `URxvt.perl-ext-common` X resource, пожалуйста, удалите `tabbed` первое значение, чтобы избежать конфликта с `tabbedex`.

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

**Примечание:** Переназначенные горячие клавиши, используемые для пользовательских команд, не будет отключать сопоставление по умолчанию, для этого вы должны установить X resource `no-tabbedex-keys`. Однако это значение, в настоящее время не входит в пакет [urxvt-tabbedex](https://aur.archlinux.org/packages/urxvt-tabbedex/). Вместо него, рассмотрите возможность использования пакета [urxvt-tabbedex-git](https://aur.archlinux.org/packages/urxvt-tabbedex-git/):
```
URxvt.tabbed.no-tabbedex-keys: true

```

## Прозрачность

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

**Примечание:** Для того, чтобы эти настройки были универсальны для всех форм URxvt, вы можете добавить символ подстановки "*". Например, `URxvt.depth` станет `URxvt*.depth`.

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

**Примечание:** Избегайте использования затенения (shading), если у вас набор `URxvt.tintColor`. Используйте вместо `tintColor` другой.

## Набор иконок

**Примечание:** Из-за сообщений и жалоб в отчете об ошибке [FS#34862](https://bugs.archlinux.org/task/34862), что в пакете [rxvt-unicode](https://www.archlinux.org/packages/?name=rxvt-unicode) много зависимостей, теперь для того, чтобы использовать опцию `iconFile`, вы должны установить пакет [rxvt-unicode-pixbuf](https://aur.archlinux.org/packages/rxvt-unicode-pixbuf/)

По умолчанию URxvt не имеет значка на панели задач. Тем не менее, это можно легко изменить путем добавления строки, указывающей на нужную иконку, в файл `~/.Xresources`:

```
URxvt.iconFile:    /usr/share/icons/Clarity/scalable/apps/terminal.svg

```

## Используйте urxvt для запуска приложений

urxvt может быть использован в качестве легкой альтернативы для запуска приложений, таких как [gmrun](https://www.archlinux.org/packages/?name=gmrun). Запустите urxvt со следующей опцией вида и поведения запуска приложения, или назначьте команду в псевдониме:

```
$ urxvt -geometry 80x3 -name 'bashrun' -e sh -c "/bin/bash -i -t"

```

## Xterm escape sequences

It is possible for rxvt-unicode to mimic the [Xterm](/index.php/Xterm "Xterm") escape sequences. These can be found for arbitrary key combinations by running `cat -v` inside *xterm*, then bound in *urxvt* using keysyms.

Take this word by word movement binding as an example:

 `~/.Xresources` 
```
!Xterm escapes, word by word movement
URxvt.keysym.Control-Left:    \033[1;5D
URxvt.keysym.Control-Right:    \033[1;5C

```

For more information, see ascii(7) and the keysym section of the urxvt(1) man page.