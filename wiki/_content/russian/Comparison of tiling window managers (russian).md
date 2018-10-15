**Состояние перевода:** На этой странице представлен перевод статьи [Comparison of tiling window managers](/index.php/Comparison_of_tiling_window_managers "Comparison of tiling window managers"). Дата последней синхронизации: 5 января 2016\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Comparison_of_tiling_window_managers&diff=0&oldid=414427).

Эта статья предусматривает объективное сравнение наиболее популярных *тайловых* [оконных менеджеров](/index.php/Window_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Window manager (Русский)") (в отличие от *плавающих* оконных менеджеров).

## Contents

*   [1 Таблица сравнения](#.D0.A2.D0.B0.D0.B1.D0.BB.D0.B8.D1.86.D0.B0_.D1.81.D1.80.D0.B0.D0.B2.D0.BD.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [1.1 Стиль управления](#.D0.A1.D1.82.D0.B8.D0.BB.D1.8C_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [1.2 Слои](#.D0.A1.D0.BB.D0.BE.D0.B8)
    *   [1.3 Назначение клавиш](#.D0.9D.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
*   [2 Внешние ссылки](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Таблица сравнения

Для краткого обзора в таблице перечислены наиболее популярные тайловые оконные менеджеры, с примечательными особенностями.

<caption>Сравнение тайловых оконных менеджеров</caption>
| Оконный менеджер (WM) | Написан на | Настраивается с помощью | Стиль управления | Поддержка системного трея | Перезагрузка на лету | Информационный бар | Композитность | Слои по умолчанию | Pixel usage | Внешнее управление | Библиотека | Многомониторный (n) режим | ICCCM/EWMH Совместимый | Состояние |
| [alopex](/index.php/Alopex "Alopex") | C | C (recompile) | Гибридный | Нет | Нет | Встроенный; Вызов сценария / программы в качестве первого аргумента | внешний | max, h-stack, v-stack, h-tab | Variable borders; titles in-statusbar | Xlib | шесть меток, два вида, доступные по умолчанию | Активный |
| [Awesome](/index.php/Awesome_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Awesome (Русский)") | C | Lua | Динамический | Встроенный | Да | Встроенный, изображения и текст | внешний | max, nh-stack (and invert), nv-stack (and invert), free | variable borders, optional h-tab titles | dbus (если включен) | XCB | n-tags (рабочие пространства). По-умолчанию включено 9\. [Example](https://awesome.naquadah.org/images/6mon.medium.png) | Да | Активный |
| [bspwm](/index.php/Bspwm_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Bspwm (Русский)") | C | Anything | Гибридный | Нет | Да | Can write internal state to a FIFO | внешний | v-split, h-split | Variable borders | via `bspc` | XCB | Рабочие столы привязаны к мониторам | Да | Активный |
| [catwm](/index.php/Catwm "Catwm") | C | C (recompile) | Динамический | Нет | Нет | Нет | Нет | v-stack, max | 1-pix borders | Xlib | Заброшенный |
| dswm | Lisp | Lisp | Ручной | Нет | Да | Да | Нет | Активный |
| [dwm](/index.php/Dwm "Dwm") | C | C (recompile) | Динамический | Дополнительный патч | [Optional](/index.php/Dwm#Restart_dwm_without_logging_out_or_closing_programs "Dwm") | Built-in, reads from root window name | внешний | v-stack, max | Xlib | n regions, 9 workspaces fixed to each region | Активный |
| [echinus](/index.php/Echinus "Echinus") | C | Text | Динамический | Нет | Да | [ourico](https://aur.archlinux.org/packages/ourico/) | внешний | v-stack, b-stack, max | Variable borders & optional titles | Xlib | Да | Неизвестно |
| euclid-wm | C | Text | Гибридный | Нет | Да | внешний([dzen](/index.php/Dzen "Dzen")) | строки, столбцы | 1-pix borders | Xlib | Бездействующий |
| [FrankenWM](/index.php/FrankenWM "FrankenWM") | C | C (recompile) | Динамический | Нет | Нет | No, outputs information to stdout, which can easily be parsed and displayed by an внешний monitor or panel (dzen2, conky, etc) | внешний | v-stack (and invert), h-stack (and invert), dual-v/h-stack, grid, fibonacci (vh-stack), строки, столбцы, max, free | Variable borders | XCB | Активный |
| [herbstluftwm](/index.php/Herbstluftwm "Herbstluftwm") | C | Text | Ручной | Нет | Да | строки, столбцы | 1-pix borders | commands via herbstclient | Xlib and Glib | n regions, 9 workspaces visible in any region | Активный |
| [i3](/index.php/I3_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "I3 (Русский)") | C | Text | Динамический | i3bar | Да(Layout is preserved) | text piped to i3bar (`i3status`/`conky` and others can be used) | внешний | tree, v-split, h-split, stacked, tabbed, max, can be nested infinitely | none, 1-pix or 2-pix, optional titlebars, can hide edge borders | commands via ipc (or i3-msg, which uses ipc) | XCB | n regions | Да | Активный |
| [Ion3](/index.php/Ion3 "Ion3") | C | Lua | Ручной | trayion | Да | configurable | ? | h-tab, max | Заброшенный |
| [monsterwm](/index.php/Monsterwm "Monsterwm") | C | C (recompile) | Динамический | Нет | Optional, but windows are lost | No, outputs information to stdout, which can easily be parsed and displayed by an внешнийmonitor or panel (`dzen2`, `conky`, etc) | внешний | h-stack, v-stack, grid, max | supports `_NET_Активный_WINDOW`, so внешнийcontrol can be supplied by `xdotool` and similar tools | [Xlib primary and XCB fork](/index.php/Monsterwm#Installation "Monsterwm") | n workspaces per monitor | Активный |
| [Musca](/index.php/Musca "Musca") | C | Text, own command set, C(recompile) | Ручной | Нет | No, but allows running of musca commands on the fly | Нет | Нет | h-split, v-split, max | commands, hooks | Xlib | Заброшенный |
| [Notion](/index.php/Notion "Notion") | C, Lua | Lua, compatible with Ion3 configs | Ручной | trayion, stalonetray | Да | configurable | ? | h-tab, max | Configurable borders and titlebars/tabs | EWMH, arbitrary Lua scripts which have access to the rich internal API | Xlib | n workspaces on each monitor. Supports on-the-fly changes in topology | Активный |
| [qtile](/index.php/Qtile "Qtile") | Python | Python | Динамический | Да | Да | Да | внешний | tree, v-split, h-split, stacked, tabbed, max | Нетborders, although customizable | Hooks, Server mode | XCB | Активный |
| [Ratpoison](/index.php/Ratpoison "Ratpoison") | C | Text | Ручной | Нет | Да | Да | внешний | max | Нет | Активный |
| [Snapwm](/index.php/Snapwm "Snapwm") | C | Reloadable Text | Динамический | Нет | Да | Built-in, reads from root window name | внешний | nVertical, Fullscreen, nHorizontal, Grid, Center Stacking | variable borders, Нетtitles | Xlib | Number of desktops distributed evenly between monitors | Активный |
| [Spectrwm](/index.php/Spectrwm "Spectrwm") | C | Text | Динамический | Нет | Да | Built-in, reads from user script | Нет | nv-stack, nh-stack, max | 1-pix borders, Нетtitles | XCB | n regions, 10 workspaces visible in any region | Да | Активный |
| [Stumpwm](/index.php/Stumpwm "Stumpwm") | Lisp | Lisp | Ручной | Нет | Да | Да | Нет | Нет | Активный |
| [subtle](/index.php/Subtle "Subtle") | C | Ruby | Ручной | Built-in | Да | Built-in (Ruby), внешнийcan be used as well | внешний | Variable grid | Variable borders, Нетtitles | Hooks (Ruby), subtler (CLI), subtlext (Ruby extension) | Xlib | One workspace (view) per monitor (screen), placement on views via tags and per runtime | Да | Активный |
| [Wingo](/index.php/Wingo "Wingo") | Go | Text | Динамический | Нет | Да | Нет | внешний | floating, nv-stack, nh-stack, max | title bars in floating, skinny borders in tiling | via [wingo-cmd](https://github.com/BurntSushi/wingo/blob/master/HOWTO-COMMANDS) or UNIX sockets in any programming language | [X Go Binding](https://github.com/BurntSushi/xgb) | n regions, workspaces visible in any region | Да | Активный |
| [WMFS](/index.php/WMFS "WMFS") | C | Text | Динамический | Built-in | Да | Built-in, set with command, color text, images | внешний | nh-stack (and invert), nv-stack (and invert), mirror-v, mirror-h, grid, free, max | variable borders, titles or Нетtitles | commands | Xlib | Up to 36 tags(workspaces) per screen | Да | Активный |
| [wmii](/index.php/Wmii "Wmii") | C | Anything | Ручной | witray | Да | Встроенный | внешний | столбцы, max, v-tab | titles | [9P filesystem](http://9p.cat-v.org) | one big region | Да | Активный |
| [xmonad](/index.php/Xmonad_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xmonad (Русский)") | Haskell | Haskell | Динамический | Нет | Да | Нет | Да, с xmonad-contrib и внешним менеджером | nv-stack, nh-stack, max | variable borders, Нетtitles | via [XMonad-Hooks-ServerMode](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-ServerMode.html) | Xlib | n regions, 9 workspaces visible in any region | Да/ ? | Активный |
| Оконный менеджер (WM) | Написан на | Настраивается с помощью | Стиль управления | Поддержка системного трея | Перезагрузка на лету | Информационный бар | Композитность | Слои по умолчанию | Pixel usage | Внешнее управление | Библиотека | Многомониторный (n) режим | ICCCM/EWMH compliant | Состояние |

**Совет:** Внешний контроль может быть достигнут с помощью таких программ, как [xdotool](https://www.archlinux.org/packages/?name=xdotool) имитирующих нажатие клавиш.

### Стиль управления

Динамическое управление выделяет лёгкость и скорость автоматического управления оконных слоёв. Ручное управление выделяет ручную регулировку расположения и размера окна. Более точный контроль, и большую трату времени на перемещение и изменение размеров окна.

### Слои

Ряд общих типов компоновки доступен в нескольких тайловых WM, хотя терминология может несколько меняться.

*   **max**: Показать одно коно во весь экран (с или без статус баром, заголовком и границами). Также: monocle(dwm, monsterwm).
*   **h-stack**: Основная область в верхней половине, другие окна располагаются горизонтально в нижней половине.

Основная область может быть изменяемого размера. Может быть инвертирована вверх-вниз (wmfs). Также: bottom stack (dwm), bstack(monsterwm).

*   **v-stack**: Основная область в левой половине, другие окна располагаются вертикально в правой половине. Основная область может быть изменяемого размера. Может быть инвертирована влево-вправо(wmfs). Aka: tile (dwm, monsterwm).
*   **nh-stack**: h-stack позволяет >=1 окно(а) в мастер-области. Также: nbstack (dwm).
*   **nv-stack**: v-stack позволяет >=1 окно(а) в мастер-области. Также: ntile (dwm).
*   **mirror-h**: nh-stack со стеками выше и ниже главной области.
*   **mirror-v**: nv-stack со стеками слева и справа от главной области.
*   **h-tab**: одно окно показано на весь экран, со всеми названиями окон, указанными по горизонтали (как вкладки браузера).
*   **v-tab**: одно окно показано на весь экран, со всеми названиями окон, указанными по вертикали. Также: stack (wmii).
*   **h-split**: назначенным сочетанием клавиш разбивается окно по горизонтали, создавая пространство для другого.
*   **v-split**: назначенным сочетанием клавиш разбивается окно по вертикали, создавая пространство для другого.
*   **columns**: ручной стиль слоёв, который воспринимает окна как столбцы по вертикали.
*   **rows**: ручной стиль слоёв, который воспринимает окна как горизонтальные ряды.
*   **grid**: размеры и позиции окон, основанные на регулярной сетке NxM. Может быть автоматическим (как в wmfs, monsterwm) или ручным (как в Subtle).

### Назначение клавиш

Тайловые оконные менеджеры ориентированы, как правило, на использование исключительно с клавиатурой или с клавиатурой и мышкой. Для быстроты и простоты использования оконного менеджера, используются горячие клавиши (мышкой результат будет достигнут медленней). Разумные назначения горячих клавиш делают работу быстрой и эффективной. Некоторые сочетания клавиш по умолчанию хороши, но их можно изменить под свои нужды.

## Внешние ссылки

*   [Comparison of extensible window managers](http://sawfish.wikia.com/wiki/Comparison_of_extensible_window_managers) compares WMs "extensible" by scripting, like Xmonad and Sawfish.