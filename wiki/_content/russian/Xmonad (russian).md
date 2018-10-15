Ссылки по теме

*   [Оконный менеджер](/index.php/%D0%9E%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Оконный менеджер")
*   [Сравнение тайловых оконных менеджеров](/index.php/%D0%A1%D1%80%D0%B0%D0%B2%D0%BD%D0%B5%D0%BD%D0%B8%D0%B5_%D1%82%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D1%8B%D1%85_%D0%BE%D0%BA%D0%BE%D0%BD%D0%BD%D1%8B%D1%85_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%BE%D0%B2 "Сравнение тайловых оконных менеджеров")
*   [Экранный менеджер](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер")
*   [Функциональность файлового менеджера](/index.php/%D0%A4%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%B0%D0%BB%D1%8C%D0%BD%D0%BE%D1%81%D1%82%D1%8C_%D1%84%D0%B0%D0%B9%D0%BB%D0%BE%D0%B2%D0%BE%D0%B3%D0%BE_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80%D0%B0 "Функциональность файлового менеджера")

**Состояние перевода:** На этой странице представлен перевод статьи [xmonad](/index.php/Xmonad "Xmonad"). Дата последней синхронизации: 14 сентября 2015\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Xmonad&diff=0&oldid=399821).

[xmonad](http://xmonad.org/) это тайловый оконный менеджер для X. Окна автоматически располагаются плиткой на экране без пробелов или перекрытия, максимально используя экранное место.

xmonad написан, настроен и расширяем на [Haskell](http://haskell.org/). Пользовательские алгоритмы компоновки, назначения клавиш и другие расширения могут быть написаны пользователем в файлах настройки.

Применение динамических шаблонов, на каждом рабочем столе можно использовать различные схемы. Xinerama полностью поддерживается, что позволяет размещать окна на нескольких физических экранах.

Для большей информации, пожалуйста посетите сайт xmonad: [http://xmonad.org/](http://xmonad.org/)

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск xmonad](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_xmonad)
    *   [2.1 С установленным Экранным менеджером](#.D0.A1_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D1.8B.D0.BC_.D0.AD.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D1.8B.D0.BC_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.BE.D0.BC)
    *   [2.2 Без установленного экранного менеджера](#.D0.91.D0.B5.D0.B7_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)
*   [3 Настройка](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0)
    *   [3.1 Базовая настройка Рабочего Стола](#.D0.91.D0.B0.D0.B7.D0.BE.D0.B2.D0.B0.D1.8F_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.A0.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D0.A1.D1.82.D0.BE.D0.BB.D0.B0)
*   [4 Выход xmonad](#.D0.92.D1.8B.D1.85.D0.BE.D0.B4_xmonad)
*   [5 Советы и приемы](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D0.BF.D1.80.D0.B8.D0.B5.D0.BC.D1.8B)
    *   [5.1 X-Selection-Paste](#X-Selection-Paste)
    *   [5.2 Горячие клавиши](#.D0.93.D0.BE.D1.80.D1.8F.D1.87.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
        *   [5.2.1 Основные комбинации клавиш](#.D0.9E.D1.81.D0.BD.D0.BE.D0.B2.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BE.D0.BC.D0.B1.D0.B8.D0.BD.D0.B0.D1.86.D0.B8.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
    *   [5.3 Дополнительные приложения](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [5.4 Увеличение числа рабочих столов](#.D0.A3.D0.B2.D0.B5.D0.BB.D0.B8.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.87.D0.B8.D1.81.D0.BB.D0.B0_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B8.D1.85_.D1.81.D1.82.D0.BE.D0.BB.D0.BE.D0.B2)
    *   [5.5 Создание комнаты для Conky или приложений из трея](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.BD.D0.B0.D1.82.D1.8B_.D0.B4.D0.BB.D1.8F_Conky_.D0.B8.D0.BB.D0.B8_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.D0.B8.D0.B7_.D1.82.D1.80.D0.B5.D1.8F)
    *   [5.6 Использование xmobar с xmonad](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_xmobar_.D1.81_xmonad)
        *   [5.6.1 Быстрый, менее гибкий](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9.2C_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B5_.D0.B3.D0.B8.D0.B1.D0.BA.D0.B8.D0.B9)
        *   [5.6.2 Подробные настройки](#.D0.9F.D0.BE.D0.B4.D1.80.D0.BE.D0.B1.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
        *   [5.6.3 Проверка настройки XMobar](#.D0.9F.D1.80.D0.BE.D0.B2.D0.B5.D1.80.D0.BA.D0.B0_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_XMobar)
    *   [5.7 Управление xmonad внешними скриптами](#.D0.A3.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_xmonad_.D0.B2.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.BC.D0.B8_.D1.81.D0.BA.D1.80.D0.B8.D0.BF.D1.82.D0.B0.D0.BC.D0.B8)
    *   [5.8 Запуск другого оконного менеджера с xmonad](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.B3.D0.BE_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0_.D1.81_xmonad)
    *   [5.9 KDE и xmonad](#KDE_.D0.B8_xmonad)
    *   [5.10 IM слой для Skype](#IM_.D1.81.D0.BB.D0.BE.D0.B9_.D0.B4.D0.BB.D1.8F_Skype)
    *   [5.11 Примеры настроек](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA)
*   [6 Решение проблем](#.D0.A0.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [6.1 GNOME 3 и xmonad](#GNOME_3_.D0.B8_xmonad)
        *   [6.1.1 Композитный Xmonad и Gnome](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BD.D1.8B.D0.B9_Xmonad_.D0.B8_Gnome)
    *   [6.2 Xfce 4 и xmonad](#Xfce_4_.D0.B8_xmonad)
    *   [6.3 Отсутствует xmonad-i386-linux или xmonad-x86_64-linux](#.D0.9E.D1.82.D1.81.D1.83.D1.82.D1.81.D1.82.D0.B2.D1.83.D0.B5.D1.82_xmonad-i386-linux_.D0.B8.D0.BB.D0.B8_xmonad-x86_64-linux)
    *   [6.4 Проблемы с приложениями Java](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F.D0.BC.D0.B8_Java)
    *   [6.5 Пустое пространство в нижней части окон gVim или терминалов](#.D0.9F.D1.83.D1.81.D1.82.D0.BE.D0.B5_.D0.BF.D1.80.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D1.81.D1.82.D0.B2.D0.BE_.D0.B2_.D0.BD.D0.B8.D0.B6.D0.BD.D0.B5.D0.B9_.D1.87.D0.B0.D1.81.D1.82.D0.B8_.D0.BE.D0.BA.D0.BE.D0.BD_gVim_.D0.B8.D0.BB.D0.B8_.D1.82.D0.B5.D1.80.D0.BC.D0.B8.D0.BD.D0.B0.D0.BB.D0.BE.D0.B2)
    *   [6.6 Chromium/Chrome не работает полноэкранно](#Chromium.2FChrome_.D0.BD.D0.B5_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D0.B0.D0.B5.D1.82_.D0.BF.D0.BE.D0.BB.D0.BD.D0.BE.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.D0.BD.D0.BE)
    *   [6.7 Multitouch / touchegg](#Multitouch_.2F_touchegg)
    *   [6.8 Назначение клавиш с раскладкой клавиатуры azerty](#.D0.9D.D0.B0.D0.B7.D0.BD.D0.B0.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_.D1.81_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.BE.D0.B9_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B_azerty)
    *   [6.9 GNOME 3 mod4+p изменение настройки отображения вместо запуска dmenu](#GNOME_3_mod4.2Bp_.D0.B8.D0.B7.D0.BC.D0.B5.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B2.D0.BC.D0.B5.D1.81.D1.82.D0.BE_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA.D0.B0_dmenu)
    *   [6.10 Проблемы с фокусировкой границы окна в VirtualBox](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D1.81_.D1.84.D0.BE.D0.BA.D1.83.D1.81.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.BE.D0.B9_.D0.B3.D1.80.D0.B0.D0.BD.D0.B8.D1.86.D1.8B_.D0.BE.D0.BA.D0.BD.D0.B0_.D0.B2_VirtualBox)
    *   [6.11 Игры из Steam (Half-Life, Left 4 Dead, …) и xmonad](#.D0.98.D0.B3.D1.80.D1.8B_.D0.B8.D0.B7_Steam_.28Half-Life.2C_Left_4_Dead.2C_.E2.80.A6.29_.D0.B8_xmonad)
    *   [6.12 LibreOffice - фокус перескакивает между главным окном и диалогом](#LibreOffice_-_.D1.84.D0.BE.D0.BA.D1.83.D1.81_.D0.BF.D0.B5.D1.80.D0.B5.D1.81.D0.BA.D0.B0.D0.BA.D0.B8.D0.B2.D0.B0.D0.B5.D1.82_.D0.BC.D0.B5.D0.B6.D0.B4.D1.83_.D0.B3.D0.BB.D0.B0.D0.B2.D0.BD.D1.8B.D0.BC_.D0.BE.D0.BA.D0.BD.D0.BE.D0.BC_.D0.B8_.D0.B4.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3.D0.BE.D0.BC)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

[Установите](/index.php/Install "Install") пакет [xmonad](https://www.archlinux.org/packages/?name=xmonad), и [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) для использования разнообразных алгоритмов компоновки, настройки, скриптов, и т.д.

Как вариант, установите [xmonad-git](https://aur.archlinux.org/packages/xmonad-git/), разрабатываемая версия, с некоторыми дополнительными зависимостями; а также [xmonad-contrib-git](https://aur.archlinux.org/packages/xmonad-contrib-git/) если хотите.

## Запуск xmonad

### С установленным Экранным менеджером

Выберите *Xmonad* из меню ссессий [Экранного менеджера](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)").

### Без установленного экранного менеджера

Если установлен только Xmonad, без использования экранного менеджера (такого как KDE, Gnome и т.д.). Добавьте `exec xmonad` в ваш [~/.xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") файл а затем начните сеанс, выполнив *startx* .

**Примечание:** По умолчанию, xmonad не устанавливает курсор X, поэтому обычно отоброжается "крест" вместо курсора. Чтобы установить привычный курсор (стрелочка показывающая влево-вверх), добавьте следующую строку в ваш `~/.xinitrc` (или `~/.xprofile` если вы используете оконный менеджер): `xsetroot -cursor_name left_ptr`

В итоге (ссылаясь на вышописанное), рекомендуем добавить в `~/.xinitrc`

```
setxkbmap -layout "us,ru" # Установит раскладки **us** и **ru**
setxkbmap -option "grp:caps_toggle,grp_led:scroll"
xsetroot -cursor_name left_ptr &
export PATH=~/bin:$PATH
exec xmonad

```

## Настройка

Создайте каталог `~/.xmonad` и файл `~/.xmonad/xmonad.hs`, после чего отредактируйте этот файл, как описано ниже. После изменений, сделанных в `~/.xmonad/xmonad.hs`, нажмите `Mod+q`, чтобы изменения вступили в силу.

**Примечание:** По умолчанию клавиша `Mod` - это `Alt`

**Совет:** Настройка по умолчанию для *xmonad* вполне удобна и полностью работает без файла `xmonad.hs`

Поскольку файл настройки *xmonad* написан на [Haskell](/index.php/Haskell "Haskell"), не-программистам, возможно, будет сложно настраивать параметры. Для получения более подробных руководств и примеров настроек вы можете обратиться к следующим ресурсам:

*   [xmonad wiki](http://wiki.haskell.org/Xmonad)
*   [xmonad configuration archive](http://wiki.haskell.org/Xmonad/Config_archive)
*   [xmonad FAQ](http://wiki.haskell.org/Xmonad/Frequently_asked_questions)
*   Arch Linux [forum thread](https://bbs.archlinux.org/viewtopic.php?id=40636)

Лучше всего помешать свои изменения и настройки только в `~/.xmonad/xmonad.hs` и записывать все неустановленные параметры из файла настроек по умолчанию (defaultConfig).

Это делается путем записи в `xmonad.hs`:

```
 import XMonad

 main = xmonad defaultConfig
     { terminal    = "urxvt"
     , modMask     = mod4Mask
     , borderWidth = 3
     }

```

Это установит терминал по умолчанию (terminal = "urxvt") и ширину рамки в 3 пикселя (borderWidth = 3), оставляя все остальные настройки по умолчанию (унаследовав из XConfig значения defaultConfig (настроек по умолчанию)).

**Примечание:** Чтобы использовать urxvt, его нужно поставить: pacman -S rxvt-unicode

Это может быть удобно, когда используются сложные вещи, чтобы вызвать параметры настроек по имени функции внутри главной функции, и определить их отдельно в своих разделах вашего `~/.xmonad/xmonad.hs`. Это расширит настройки вашей планировки и сделает сохранение, визуализацию и управление хуками легче.

Простой `xmonad.hs` можно было записать так:

```
 import XMonad

 main = do
   xmonad $ defaultConfig
     { terminal    = myTerminal
     , modMask     = myModMask
     , borderWidth = myBorderWidth
     }

 myTerminal    = "urxvt"
 myModMask     = mod4Mask -- Win клавиша (или Super_L)
 myBorderWidth = 3

```

Кроме того, установленные выше (main, myTerminal, myModMask и т.д.), в пределах {} не имеют значения в Haskell, пока не импортируются в первую очередь.

Ниже берется шаблон файла настроек 0.9\. Этот пример из наиболее распространенных функций можно определить в свой основной блок (main = do).

```
 {
   terminal           = myTerminal,
   focusFollowsMouse  = myFocusFollowsMouse,
   borderWidth        = myBorderWidth,
   modMask            = myModMask,
   -- numlockMask deprecated in 0.9.1
   -- numlockMask        = myNumlockMask,
   workspaces         = myWorkspaces,
   normalBorderColor  = myNormalBorderColor,
   focusedBorderColor = myFocusedBorderColor,

   -- key bindings
   keys               = myKeys,
   mouseBindings      = myMouseBindings,

   -- hooks, layouts
   layoutHook         = myLayout,
   manageHook         = myManageHook,
   handleEventHook    = myEventHook,
   logHook            = myLogHook,
   startupHook        = myStartupHook
 }

```

Сам пакет также включает в себя `xmonad.hs`, последний использует официальный пример `xmonad.hs`, который поставляется с модулем Haskell *'xmonad'* в качестве примера того, как всё это реализовать. Его не рекомендуется использоваться в качестве шаблона настроек, но он подойдёт в качестве примера. Можете взять часть кода для использования в собственной настройке. Он расположен в (зависит от версии архитектуры) каталоге `/usr/share/` (или выполните для поиска `find /usr/share -name xmonad.hs`).

### Базовая настройка Рабочего Стола

В [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) лучшая настройка по умолчанию для обычных пользователей. Он также помогает с проблемами в некоторых современных программах, такие как Chromium

Добавьте это:

```
 import XMonad
 import XMonad.Config.Desktop

 baseConfig = desktopConfig

 main = xmonad baseConfig
     { terminal    = "urxvt"
     , modMask     = mod4Mask
     }

```

## Выход xmonad

Для завершения текущей сессии xmonad session, нажмите `Mod+Shift+Q`.

## Советы и приемы

### X-Selection-Paste

Центральное управление клавиатурой в Xmonad может дополнительно поддерживать горячие клавиши [X-Selection-Paste](/index.php/Keyboard_shortcuts#Key_binding_for_X-selection-paste "Keyboard shortcuts").

Кроме того, существует функция "pasteSelection" в XMonad.Util.Paste которая может быть связана с клавишей, используя строку:

 `xmonad.hs` 
```
  -- X-selection-paste buffer
  , ((0, xK_Insert), pasteSelection)
```

Нажатие клавиши "Insert" теперь будет вставлять "буфер мыши" в активном окне.

### Горячие клавиши

Если вы используете Xmonad в качестве самостоятельного менеджера окон, вы можете редактировать `xmonad.hs` чтобы добавить горячие клавиши. Вам просто нужно найти имя клавиши XF86 (например как XF86PowerDown) посмотрите его в `/usr/include/X11/XF86keysym.h`. Это даст вам код клавиши (вроде 0x1008FF2A) который вы можете использовать, чтобы добавить строку, как в следующем разделе комбинации клавиш с вашим `xmonad.hs`:

```
((0,               0x1008FF2A), spawn "sudo pm-suspend")

```

#### Основные комбинации клавиш

**Примечание:** Если вы не переназначили Mod-клавишу. то (как говорилось выше) по умолчанию это Alt

```
Mod+Shift+Enter — запустить новый терминал.
Mod+Число — переключиться на N’ый рабочий стол.
Mod+Shift+Число — перенести окно на N’ый рабочий стол.
Mod+C — закрыть текущее окно.
Mod+Пробел — переключение между компоновками окон.
Mod+Shift+Пробел — использовать компоновку по умолчанию.
Mod+Enter — поменять местами текущее окно и первое (всегда главное).
Mod+Запятая — увеличить количество главных окон.
Mod+Точка — уменьшить количество главных окон.
Mod+H — уменьшить размер главной части.
Mod+L — увеличить размер главной части.
Mod+P — dmenu (удобный запуск программ).
Mod+Shift+P — gmrun (менее удобная альтернатива dmenu).
Mod+Tab или Mod+J — сделать активным следующее окно.
Mod+K — сделать активным предыдущее окно.
Mod+Shift+J — поменять местами текущее окно и следующее.
Mod+Shift+K — поменять местами текущее окно и предыдущее.
Mod+ЛКМ — перемещение окна с помощью мыши.
Mod+ПКМ — изменение размера окна с помощью мыши.
Mod+T — вернуть плавающее окно в мозаику.
Mod+Q — перезапустить Xmonad.
Mod+Shift+Q — закрыть Xmonad.

```

### Дополнительные приложения

Есть ряд дополнительных приложений, которые хорошо работают с xmonad. Наиболее распространенные из них:

*   **[xmobar](/index.php/Xmobar "Xmobar")** — Лёгкая строка состояния, написанная на Haskell.

	[http://projects.haskell.org/xmobar/](http://projects.haskell.org/xmobar/) || [xmobar](https://www.archlinux.org/packages/?name=xmobar), [xmobar-git](https://aur.archlinux.org/packages/xmobar-git/)

*   **xmonad-log-applet** — [https://github.com/alexkay/xmonad-log-applet](https://github.com/alexkay/xmonad-log-applet)

	Апплет для GNOME, MATE или xfce панели. || [xmonad-log-applet-xfce4-git](https://aur.archlinux.org/packages/xmonad-log-applet-xfce4-git/), [xmonad-log-applet-gnome-git](https://aur.archlinux.org/packages/xmonad-log-applet-gnome-git/)

### Увеличение числа рабочих столов

По умолчанию, xmonad использует 9 рабочих столов. Вы можете увеличить это значение до 14 расширяя следующую строку:

 `xmonad.hs` 
```
-- (i, k) <- zip (XMonad.workspaces conf) [xK_1, xK_2, xK_3, xK_4, xK_5, xK_6, xK_7, xK_8, xK_9]
(i, k) <- zip (XMonad.workspaces conf) [xK_grave, xK_1, xK_2, xK_3, xK_4, xK_5, xK_6, xK_7, xK_8, xK_9, xK_0, xK_minus, xK_equal, xK_BackSpace]
```

### Создание комнаты для Conky или приложений из трея

Оберните ваши макеты с avoidStruts из XMonad.Hooks.ManageDocks для автоматического dock/panel/trayer интервала:

```
 import XMonad
 import XMonad.Hooks.ManageDocks

 main=do
   xmonad $ defaultConfig
     { ...
     , layoutHook=avoidStruts $ layoutHook defaultConfig
     , manageHook=manageHook defaultConfig <+> manageDocks
     , ...
     }

```

Если вы хотите переключать интервалы, это действие можно добавить в клавиатурных назначениях:

```
,((modMask x, xK_b     ), sendMessage ToggleStruts)

```

### Использование xmobar с xmonad

**[xmobar](/index.php/Xmobar "Xmobar")** это легкий и минималистичный текстовый бар, предназначенный для работы с xmonad. Для использования xmobar с xmonad, вам понадобятся два пакета, в дополнении к пакету [xmonad](https://www.archlinux.org/packages/?name=xmonad). Эти пакеты [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) и [xmobar](https://www.archlinux.org/packages/?name=xmobar) из [официальных репозиториев](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)"), или воспользуйтесь [xmobar-git](https://aur.archlinux.org/packages/xmobar-git/) из [AUR](/index.php/AUR_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "AUR (Русский)") вместо официального пакета [xmobar](https://www.archlinux.org/packages/?name=xmobar).

Запустим xmobar внутри xmonad. Который перезагружает xmobar, когда вы запускаете xmonad. Откройте `~/.xmonad/xmonad.hs` в вашем любимом текстовом редакторе и выберите один из двух следующих вариантов:

#### Быстрый, менее гибкий

**Примечание:** Существует также [dzen2](https://www.archlinux.org/packages/?name=dzen2) который можно заменить на [xmobar](https://www.archlinux.org/packages/?name=xmobar).

Общий импорт:

```
import XMonad
import XMonad.Hooks.DynamicLog

```

Xmobar запускает xmobar c изменёнными настройками, которые включает все варианты, описанные в [#Подробные настройки](#.D0.9F.D0.BE.D0.B4.D1.80.D0.BE.D0.B1.D0.BD.D1.8B.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8).

```
main = xmonad =<< xmobar defaultConfig { modMask = mod4Mask {- или любая другая настройка здесь ... -}}

```

#### Подробные настройки

В xmonad(-contrib) 0.9, есть новая функция [XMonad.Hooks.DynamicLog](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-DynamicLog.html) в [statusBar](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-DynamicLog.html#v%3AstatusBar). Она позволяет использовать свои настройки:

*   Команда вывода в бар
*   PP определяющий, что написано в бар
*   Сочетание клавиш для переключения/изменения промежутков бара

Ниже приведен пример как ей воспользоваться:

 `~/.xmonad/xmonad.hs` 
```
-- Импорт.
import XMonad
import XMonad.Hooks.DynamicLog

-- Основная функция.
main = xmonad =<< statusBar myBar myPP toggleStrutsKey myConfig

-- Команда для запуска бара.
myBar = "xmobar"

-- Настройте пользовательские PP как вам нравится. Они определяют то, что пишется в бар..
myPP = xmobarPP { ppCurrent = xmobarColor "#429942" "" . wrap "<" ">" }

-- Назначение клавиш для переключения промежутков бара.
toggleStrutsKey XConfig {XMonad.modMask = modMask} = (modMask, xK_b)

-- Главная настройка. Переопределите значения по умолчанию на свой вкус.
myConfig = defaultConfig { modMask = mod4Mask }

```

#### Проверка настройки XMobar

Шаблон xmobarrc по умолчанию содержит это. Откройте `~/.xmobarrc` и убедитесь, что у вас есть `StdinReader` в шаблоне, и запустите плагин, например:

 `~/.xmobarrc` 
```
Config { ...
       , commands = [ Run StdinReader .... ]
         ...
       , template = " %StdinReader% ... "
       }

```

Теперь, все что вам придется сделать, - это запустить, или перезапустить xmonad.

**Совет:** Для перезапуска xmonad, выполните `xmonad --restart`

### Управление xmonad внешними скриптами

Вот несколько способов сделать это:

*   Воспользуйтесь расширением для xmonad [XMonad.Hooks.ServerMode](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-ServerMode.html).

*   Эмулируйте нажатия клавиш, используя [xdotool](https://www.archlinux.org/packages/?name=xdotool) или аналогичные программы. Смотрите тут [Ubuntu forums thread](http://ubuntuforums.org/archive/index.php/t-658040.html). Следующая команда будет имитировать нажатие `Super+n`:

```
xdotool key Super+n

```

*   [wmctrl](https://www.archlinux.org/packages/?name=wmctrl) -Если у вас есть desktopConfig или написан EwmhDesktops, то это очень простая в использовании стандартная утилита.

### Запуск другого оконного менеджера с xmonad

Если вы используете [xmonad-git](https://aur.archlinux.org/packages/xmonad-git/), с Января 2011, вы можете перезапустить xmonad с другим оконным менеджером. Вам просто нужно написать небольшой скрипт и добавить в `~/.xmonad/xmonad.hs`. Вот этот скрипт:

 `~/bin/obtoxmd` 
```
#!/bin/sh
openbox
xmonad

```

А вот поправки, которые нужно добавить к вашему `~/.xmonad/xmonad.hs`:

 `~/.xmonad/xmonad.hs` 
```
import XMonad
--You need to add this import
import XMonad.Util.Replace

main do
    -- And this "replace"
    replace
    xmonad $ defaultConfig
    {
    --Add the usual here
    }

```

Также нужно добавить привязку клавиш:

 `~/xmonad/xmonad.hs` 
```
--Add a keybinding as follows:
((modm .|. shiftMask, xK_o     ), restart "/home/abijr/bin/obtoxmd" True)

```

Только не забудьте добавить запятую перед или после, а также изменить путь к реальному пути скрипта. Нажмите `Mod+q` (перезапустите *xmonad* с обновлёнными настройками), затем `Mod+Shift+o`, и вы должны получить работающий Openbox с теми же открытыми окнами, что и в *xmonad*. Чтобы вернуться к *xmonad*, просто выйдите из Openbox. Вот ссылка на файл `~/.xmonad/xmonad.hs` от adamvo, который использует эту установку: [Adamvo's xmonad.hs](http://wiki.haskell.org/Xmonad/Config_archive/adamvo%27s_xmonad.hs).

### KDE и xmonad

В Вики xmonad есть инструкции о том, как [запустить xmonad внутри KDE](https://wiki.haskell.org/Xmonad/Using_xmonad_in_KDE)

Будет хорошей идеей установить глобальное сочетание клавиш KDE при запущенном xmonad, в случае, если он случайно будет закрыт или "убит".

### IM слой для Skype

Чтобы создать IM слой для новой версии skype, используйте следующий код:

 `xmonad.hs` 
```
myIMLayout = withIM (1%7) skype Grid
    where
      skype = And (ClassName "Skype") (Role "")

```

### Примеры настроек

Ниже приведены несколько примеров настроек от пользователей xmonad. Не стесняйтесь добавлять ссылки на свои файлы настроек.

*   brisbin33 :: simple, useful, readable :: [config](https://github.com/pbrisbin/xmonad-config) [screenshot](http://files.pbrisbin.com/screenshots/current_desktop.png)
*   jelly :: Configuration with prompt, different layouts, twinview with xmobar :: [xmonad.hs](http://github.com/jelly/dotfiles/tree/master/.xmonad/xmonad.hs)
*   MrElendig :: Simple configuration, with xmobar :: [xmonad.hs](http://github.com/MrElendig/dotfiles-alice/blob/master/.xmonad/xmonad.hs), [.xmobarrc](http://github.com/MrElendig/dotfiles-alice/blob/master/.xmobarrc), [screenshot](http://arch.har-ikkje.net/gfx/ss/2010-09-05-163305_2960x1050_scrot.png).
*   thayer :: A minimal mouse-friendly config ideal for netbooks :: [configs](http://wiki.haskell.org/Xmonad/Config_archive/Thayer_Williams%27_xmonad.hs) [screenshot](http://wiki.haskell.org/Image:Thayer-xmonad-20110511.png)
*   vicfryzel :: Beautiful and usable xmonad configuration, along with xmobar configuration, xinitrc, dmenu, and other scripts that make xmonad more usable. :: [git repository](https://github.com/vicfryzel/xmonad-config), [screenshot](https://github.com/vicfryzel/xmonad-config/raw/master/screenshot.png).
*   vogt :: Check out adamvo's config and many others in the official [Xmonad/Config archive](http://wiki.haskell.org/Xmonad/Config_archive)
*   wulax :: Example of using xmonad inside Xfce. Contains two layouts for GIMP. :: [xmonad.hs](https://gist.github.com/jsjolund/94f6821b248ff79586ba), [screenshot](https://i.imgur.com/at9AbOl.png).

## Решение проблем

### GNOME 3 и xmonad

С выпуском GNOME 3 [custom GNOME sessions](/index.php/GNOME#Custom_GNOME_sessions "GNOME") потребуются дополнительные действия, чтобы сделать из GNOME и xmonad конфетку.

Либо установите [xmonad-gnome3](https://aur.archlinux.org/packages/xmonad-gnome3/) из AUR, или вручную:

Добавьте сессию xmonad в файл используемый gnome-session (`/usr/share/gnome-session/sessions/xmonad.session`):

```
[GNOME Session]
Name=Xmonad session
RequiredComponents=gnome-panel;gnome-settings-daemon;
RequiredProviders=windowmanager;notifications;
DefaultProvider-windowmanager=xmonad
DefaultProvider-notifications=notification-daemon
```

Создайте файл для рабочего стола GDM (`/usr/share/xsessions/xmonad-gnome-session.desktop`):

```
[Desktop Entry]
Name=Xmonad GNOME
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=gnome-session --session=xmonad
Type=XSession
```

Создайте или отредактируйте этот файл (`/usr/share/applications/xmonad.desktop`):

```
[Desktop Entry]
Type=Application
Encoding=UTF-8
Name=Xmonad
Exec=xmonad
NoDisplay=true
X-GNOME-WMName=Xmonad
X-GNOME-Autostart-Phase=WindowManager
X-GNOME-Provides=windowmanager
X-GNOME-Autostart-Notify=false
```

В конце концов, установите [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) и создайте или отредактируйте `~/.xmonad/xmonad.hs` со следующим содержимым:

```
import XMonad
import XMonad.Config.Gnome

main = xmonad gnomeConfig
```

Теперь Xmonad должен появиться в списке сеансов GDM, а также будет работать с gnome-session.

#### Композитный Xmonad и Gnome

Некоторые приложения выглядят лучше (например GNOME Do) когда включен композитный режим. Это, однако, не задействовано в оконном менеджере Xmonad по умолчанию. Чтобы включить его, добавьте дополнительный .desktop файл `/usr/share/xsessions/xmonad-gnome-session-composite.desktop`:

```
[Desktop Entry]
Name=Xmonad GNOME (Composite)
Comment=Tiling window manager
TryExec=/usr/bin/gnome-session
Exec=/usr/sbin/gnome-xmonad-composite
Type=XSession
```

И создайте `/usr/sbin/gnome-xmonad-composite` и `chmod +x /usr/sbin/gnome-xmonad-composite`:

```
xcompmgr &
gnome-session --session=xmonad
```

Теперь выберите "Xmonad GNOME (Composite)" в списке сеансов, во время входа в систему. Посмотрите [xcompmgr(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xcompmgr.1) для дополнительных настроек "радующих глаз".

### Xfce 4 и xmonad

Используйте `xfceConfig` вместо `defaultConfig` после импорта `XMonad.Config.Xfce` в `~/.xmonad/xmonad.hs`, например адаптируем минимальную настройку свыше:

```
import XMonad
import XMonad.Config.Xfce

```

```
main = xmonad xfceConfig
    { terminal    = "urxvt"
    , modMask     = mod4Mask
    }

```

Также добавьте запись в *Настройки > Session and Startup > Application Autostart* чтобы выполнить `xmonad --replace`.

### Отсутствует xmonad-i386-linux или xmonad-x86_64-linux

Xmonad автоматически создаёт `xmonad-i386-linux` файл (в `~/.xmonad/`). Если это не так, возьмите файл настройки из [xmonad wiki](http://wiki.haskell.org/Xmonad/Config_archive) или создайте свой [own](http://wiki.haskell.org/Xmonad/Config_archive/John_Goerzen's_Configuration). Положите `.hs` и все другие файлы в `~/.xmonad/` и запустите эту команду из папки:

```
xmonad --recompile

```

Теперь вы должны увидеть файл.

**Примечание:** Вы можете получить сообщение об ошибке, что xmonad-x86_64-linux не найден потому что [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib) не установлен.

### Проблемы с приложениями Java

Если у вас есть проблемы, с приложениями Java, - окна не меняют размер, или меню сразу закрывается после вызова, смотрите [Java#Приложения не изменяют размер с WM, меню сразу закрывается](/index.php/Java_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Java (Русский)").

### Пустое пространство в нижней части окон gVim или терминалов

Решение, меняющее цвет пространства на цвет фона, можно найти в разделе [Vim (Русский)#Пустое пространство в нижней части окон gVim](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9F.D1.83.D1.81.D1.82.D0.BE.D0.B5_.D0.BF.D1.80.D0.BE.D1.81.D1.82.D1.80.D0.B0.D0.BD.D1.81.D1.82.D0.B2.D0.BE_.D0.B2_.D0.BD.D0.B8.D0.B6.D0.BD.D0.B5.D0.B9_.D1.87.D0.B0.D1.81.D1.82.D0.B8_.D0.BE.D0.BA.D0.BE.D0.BD_gVim "Vim (Русский)").

В случае с [rxvt-unicode](/index.php/Rxvt-unicode_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Rxvt-unicode (Русский)") можно воспользоватся пакетом [rxvt-unicode-patched](https://aur.archlinux.org/packages/rxvt-unicode-patched/).

Также можно заставить xmonad соблюдать размер, но из-за этого может появиться зазор. Смотрите [документацию по Xmonad.Layout.LayoutHints](http://www.eng.uwaterloo.ca/~aavogt/xmonad/docs/xmonad-contrib/XMonad-Layout-LayoutHints.html).

### Chromium/Chrome не работает полноэкранно

Если Chromium/Chrome не может перейти в полноэкранный режим по нажатию `F11`, воспользуйтесь [XMonad.Hooks.EwmhDesktops](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-EwmhDesktops.html) расширением из пакета [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib). Просто добавьте `import` строчку в ваш `~/.xmonad/xmonad.hs`:

```
import XMonad.Hooks.EwmhDesktops

```

а затем добавьте `handleEventHook = fullscreenEventHook` в соответствующее место; например:

```
...
        xmonad $ defaultConfig
            { modMask            = mod4Mask
            , handleEventHook    = fullscreenEventHook
            }
...

```

После перекомпиляции / перезагрузки xmonad, Chromium теперь должен ответить на `F11` (полноэкранный режим) как положено.

### Multitouch / touchegg

Touchégg polls the window manager for the `_NET_CLIENT_LIST` (in order to fetch a list of windows it should listen for mouse events on.) По умолчанию, xmonad не поддерживает это свойство. Чтобы это включить, воспользуйтесь [XMonad.Hooks.EwmhDesktops](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-EwmhDesktops.html) расширением из пакета [xmonad-contrib](https://www.archlinux.org/packages/?name=xmonad-contrib).

### Назначение клавиш с раскладкой клавиатуры azerty

Пользователи использующие клавиатуру с раскладкой "azerty" могут столкнуться с проблемами при использовании сочетаний клавиш. Воспользуйтесь [XMonad.Config.Azerty](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Config-Azerty.html) модулем для решения проблемы.

### GNOME 3 mod4+p изменение настройки отображения вместо запуска dmenu

Если вам не нужна возможность переключения "display-setup" в "gnome-control-center", просто выполните

 `dconf write /org/gnome/settings-daemon/plugins/xrandr/active false` 

в качестве пользователя, чтобы отключить плагин, который захватывает Super+p.

### Проблемы с фокусировкой границы окна в VirtualBox

Известная проблема с Virtualbox ([Ticket #6479](https://www.virtualbox.org/ticket/6479)) может вызвать проблемы с фокусировкой границы окна. Решение может быть найдено путем установки композитного менеджера, как [xcompmgr](/index.php/Xcompmgr "Xcompmgr") который отменяет некорректное поведение.

### Игры из Steam (Half-Life, Left 4 Dead, …) и xmonad

Бывают проблемы с играми на движке "Source" (например Half-Life). Если они не запускаются или зависли с черным экраном, - обойдите эту проблему, запустив игру в оконном режиме: щелкните правой кнопкой мыши на игре в вашей библиотеке и выберите "свойства". Нажмите на параметры запуска и введите: [[1]](http://steamcommunity.com/app/221410/discussions/0/864960353968561426/)

```
-windowed

```

Другим решением является плавающее окно игры с помощью хука управления. Например, следующая строка может быть использована для Half-Life:

```
 className =? "hl_linux" --> doFloat

```

Это также может работать, обратив внимание XMonad на EWMH, и в том числе полноэкранным хуком: [[2]](http://xmonad.org/xmonad-docs/xmonad-contrib/XMonad-Hooks-EwmhDesktops.html)

```
  main = xmonad $ ewmh defaultConfig{ handleEventHook =
           handleEventHook defaultConfig <+> fullscreenEventHook }

```

Это даёт несколько другой эффект, и делает его поведение больше похожим на полноэкранное приложение в других оконных менеджерах.

### LibreOffice - фокус перескакивает между главным окном и диалогом

По умолчанию пользовательский интерфейс LibreOffice использует "движок" gtk в обход окружения рабочего стола. Это может вызвать проблемы с некоторыми настройками xmonad. Такие настройки приводят к быстро скачущему фокусу между главным окном LibreOffice и любым открытым окном диалога LibreOffice, эффективно "запирая" приложение... В этом случае переменная среда SAL_USE_VCLPLUGIN может заставить LibreOffice использовать другую тему пользовательского интерфейса, как указано в [LibreOffice#Theme](/index.php/LibreOffice#Theme "LibreOffice") Например:

```
  export SAL_USE_VCLPLUGIN=gen lowriter

```

Использует общий (QT) UI.

## Смотрите также

Cтатьи на Русском:

*   [xmonad: функциональный оконный менеджер](https://ro-che.info/docs/xmonad/)
*   [XMonad + XMobar = ❤](http://habrahabr.ru/post/242351/)

Cтатьи на Английском:

*   [xmonad](http://xmonad.org/) - Официальный сайт xmonad
*   [xmonad.hs](http://wiki.haskell.org/Xmonad/Config_archive/Template_xmonad.hs_(0.9)) - шаблоны xmonad.hs
*   [xmonad: экскурсия](http://xmonad.org/tour.html)
*   [dzen](/index.php/Dzen "Dzen") - General purpose messaging and notification program
*   [dmenu](/index.php/Dmenu "Dmenu") - Dynamic X menu for the quick launching of programs
*   [Share your xmonad desktop!](https://bbs.archlinux.org/viewtopic.php?id=94969)
*   [xmonad hacking thread](https://bbs.archlinux.org/viewtopic.php?id=40636)