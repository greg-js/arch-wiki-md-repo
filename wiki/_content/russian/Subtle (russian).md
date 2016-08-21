Со [страницы проекта Subtle](http://subforge.org/projects/subtle):

	*Subtle это фреймовый менеджер окон с ручным управлением с несколько нестандарнтым подходом к фреймам: вместо того, чтобы опираться на заранее поередённые раскладки, Subtle представляет экран в виде сетки с настраиваемыми изменяемыми ячейками (называемым гравитацией).*

Subtle настраивается при помощи [Ruby](/index.php/Ruby "Ruby") для [Xorg](/index.php/Xorg "Xorg").

**Note:** Эта статься описывает основы Subtle. Полная информация и руководства могут быть найдены на [странице проекта Subtle](http://subforge.org/projects/subtle).

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск Subtle](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_Subtle)
*   [3 Basic function](#Basic_function)
*   [4 Configuration](#Configuration)
*   [5 Sublets](#Sublets)
    *   [5.1 Installing sublets](#Installing_sublets)
    *   [5.2 Enabling sublets](#Enabling_sublets)
*   [6 See also](#See_also)

## Установка

[Установите](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0 "Установка") пакет [subtle-git](https://aur.archlinux.org/packages/subtle-git/).

## Запуск Subtle

Для запуска Subtle добавьте `exec subtle` в ваш `.xinitrc` файл и запустите Xorg. Помните, что Subtle не предоставляет иконок или меню, только предопределённое сочетание клавиш для открытия терминала -- `Super+Enter`, которое запустит [URxvt](/index.php/URxvt "URxvt"). Так что если у васт отсутствуетс URxvt, установите его или измените конфигурационный файл перед запуском. Если вам необходимо выйти из Subtle, нажмите `Super+Ctrl+q`.

## Basic function

When windows are opened they are matched against a set of user-defined rules to get proper position and size. The process of applying these rules can be broken down in three main parts:

*   View
*   Gravity
*   Tag

*Views* are the environment in which the windows will be placed. Much like ordinary desktop surfaces. Defining the actual rules for a window is accomplished with a *tag*. In tags you also determine the *gravity* to be used. Gravities control the size and position of windows.

**Note:** When configuring Subtle you actually need to declare these elements in reverse order. Gravity, tag then view.

## Configuration

Subtle will search for `subtle.rb` in your $XDG_CONFIG_HOME path. If it is non-existant it will load a default file from your $XDG_CONFIG_DIRS path. It is preferable to copy this file to your `$XDG_CONFIG_HOME/subtle` directory instead of using the default.

The default file will contain numerous gravities, tags and views. This is an excellent place to start when designing your own environment. Applications without matching tags will be placed on the view containing the default tag, if no view posses it, they are automatically placed on the first view.

To check your configuration file for potential errors, simply run the following command:

```
$ subtle -k

```

## Sublets

Sublets are tiny apps that appear in the Subtle panels. They can be used to control various applications and show system stats.

### Installing sublets

To install a sublet, type the following command in a terminal:

```
$ sur install <name of sublet>

```

For a list of sublets, go to the [sur website](http://sur.subforge.org).

**Note:** If you install a sublet as root, you will not be able to invoke the sublet as a regular user. Sublets used by non-root accounts must be installed under the user.

### Enabling sublets

By default all sublets are displayed in the top right corner. You can change this behavior in `subtle.rb` by removing `:sublets` from the screen config and adding your sublets like this:

```
screen 1 do
 top [ :title, :spacer, :views ]
 bottom [ :mpd, :wifi, :battery ]
end

```

Then just add the sublets name in the same fashion as the other ones, like this:

```
 bottom [ :mpd,  :<name of sublet>, :wifi, :battery ]

```

It can of course be inserted at a place by your own choice.

## See also

*   [Subtle project page](http://subforge.org/projects/subtle)
*   [Sublets archive](http://sur.subforge.org)
*   [The subtle thread](https://bbs.archlinux.org/viewtopic.php?id=71783)
*   [Share your Subtle desktop!](https://bbs.archlinux.org/viewtopic.php?id=112486)
*   [xinitrc](/index.php/Xinitrc "Xinitrc")
*   [Start X at login](/index.php/Start_X_at_login "Start X at login")
*   [Window manager](/index.php/Window_manager "Window manager")