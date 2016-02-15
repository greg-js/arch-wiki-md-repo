С официального сайта:

"_[awesome](http://awesome.naquadah.org/) - это полностью настраиваемый современный оконный менеджер для X. Он очень быстрый, расширяемый и распространяется под GNU GPLv2 лицензией._

_Ориентирован на опытных пользователей, разработчиков, людей, занимающихся вычислениями и на тех, кто желает иметь полный контроль над графической средой._"

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Запуск awesome](#.D0.97.D0.B0.D0.BF.D1.83.D1.81.D0.BA_awesome)
    *   [2.1 Без использования менеджера входа в систему](#.D0.91.D0.B5.D0.B7_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
    *   [2.2 С использованием менеджера входа в систему](#.D0.A1_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5.D0.BC_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)
        *   [2.2.1 GDM, LightDM и другие, использующие /usr/share/xsessions/](#GDM.2C_LightDM_.D0.B8_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D0.B5.2C_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D1.8E.D1.89.D0.B8.D0.B5_.2Fusr.2Fshare.2Fxsessions.2F)
        *   [2.2.2 KDM](#KDM)
*   [3 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
    *   [3.1 Создание файла конфигурации](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.2 Источники для файлов конфигурации](#.D0.98.D1.81.D1.82.D0.BE.D1.87.D0.BD.D0.B8.D0.BA.D0.B8_.D0.B4.D0.BB.D1.8F_.D1.84.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B8)
    *   [3.3 Отладка файла rc.lua при помощи Xephyr](#.D0.9E.D1.82.D0.BB.D0.B0.D0.B4.D0.BA.D0.B0_.D1.84.D0.B0.D0.B9.D0.BB.D0.B0_rc.lua_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_Xephyr)
*   [4 Темы оформления](#.D0.A2.D0.B5.D0.BC.D1.8B_.D0.BE.D1.84.D0.BE.D1.80.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [4.1 Установка обоев рабочего стола](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BE.D0.B1.D0.BE.D0.B5.D0.B2_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
        *   [4.1.1 Случайные фоновые изображения](#.D0.A1.D0.BB.D1.83.D1.87.D0.B0.D0.B9.D0.BD.D1.8B.D0.B5_.D1.84.D0.BE.D0.BD.D0.BE.D0.B2.D1.8B.D0.B5_.D0.B8.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
*   [5 Советы и хитрости](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B_.D0.B8_.D1.85.D0.B8.D1.82.D1.80.D0.BE.D1.81.D1.82.D0.B8)
    *   [5.1 Использование awesome в GNOME в качестве оконного менеджера](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_awesome_.D0.B2_GNOME_.D0.B2_.D0.BA.D0.B0.D1.87.D0.B5.D1.81.D1.82.D0.B2.D0.B5_.D0.BE.D0.BA.D0.BE.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D0.B0)
    *   [5.2 Эффект развертывания окон как в compiz](#.D0.AD.D1.84.D1.84.D0.B5.D0.BA.D1.82_.D1.80.D0.B0.D0.B7.D0.B2.D0.B5.D1.80.D1.82.D1.8B.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BE.D0.BA.D0.BE.D0.BD_.D0.BA.D0.B0.D0.BA_.D0.B2_compiz)
    *   [5.3 Скрыть/показать wibox в awesome](#.D0.A1.D0.BA.D1.80.D1.8B.D1.82.D1.8C.2F.D0.BF.D0.BE.D0.BA.D0.B0.D0.B7.D0.B0.D1.82.D1.8C_wibox_.D0.B2_awesome)
    *   [5.4 Снимки рабочего стола](#.D0.A1.D0.BD.D0.B8.D0.BC.D0.BA.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [5.5 Динамические теги](#.D0.94.D0.B8.D0.BD.D0.B0.D0.BC.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.B8.D0.B5_.D1.82.D0.B5.D0.B3.D0.B8)
    *   [5.6 Space Invaders](#Space_Invaders)
    *   [5.7 Naughty для всплывающих уведомлений](#Naughty_.D0.B4.D0.BB.D1.8F_.D0.B2.D1.81.D0.BF.D0.BB.D1.8B.D0.B2.D0.B0.D1.8E.D1.89.D0.B8.D1.85_.D1.83.D0.B2.D0.B5.D0.B4.D0.BE.D0.BC.D0.BB.D0.B5.D0.BD.D0.B8.D0.B9)
    *   [5.8 Контекстное меню](#.D0.9A.D0.BE.D0.BD.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.BD.D0.BE.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8E)
    *   [5.9 Еще виджеты для awesome](#.D0.95.D1.89.D0.B5_.D0.B2.D0.B8.D0.B4.D0.B6.D0.B5.D1.82.D1.8B_.D0.B4.D0.BB.D1.8F_awesome)
    *   [5.10 Прозрачность](#.D0.9F.D1.80.D0.BE.D0.B7.D1.80.D0.B0.D1.87.D0.BD.D0.BE.D1.81.D1.82.D1.8C)
        *   [5.10.1 ImageMagick](#ImageMagick)
    *   [5.11 Автозапуск программ](#.D0.90.D0.B2.D1.82.D0.BE.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC)
    *   [5.12 Передача информации виджетам при помощи awesome-client](#.D0.9F.D0.B5.D1.80.D0.B5.D0.B4.D0.B0.D1.87.D0.B0_.D0.B8.D0.BD.D1.84.D0.BE.D1.80.D0.BC.D0.B0.D1.86.D0.B8.D0.B8_.D0.B2.D0.B8.D0.B4.D0.B6.D0.B5.D1.82.D0.B0.D0.BC_.D0.BF.D1.80.D0.B8_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D0.B8_awesome-client)
    *   [5.13 Использование другой панели в awesome](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.B4.D1.80.D1.83.D0.B3.D0.BE.D0.B9_.D0.BF.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8_.D0.B2_awesome)
    *   [5.14 Запретить Nautilus'у отображать рабочий стол (Gnome3)](#.D0.97.D0.B0.D0.BF.D1.80.D0.B5.D1.82.D0.B8.D1.82.D1.8C_Nautilus.27.D1.83_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D1.82.D1.8C_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B8.D0.B9_.D1.81.D1.82.D0.BE.D0.BB_.28Gnome3.29)
    *   [5.15 Переход с GNOME 3](#.D0.9F.D0.B5.D1.80.D0.B5.D1.85.D0.BE.D0.B4_.D1.81_GNOME_3)
    *   [5.16 Не менять теги колесом мыши](#.D0.9D.D0.B5_.D0.BC.D0.B5.D0.BD.D1.8F.D1.82.D1.8C_.D1.82.D0.B5.D0.B3.D0.B8_.D0.BA.D0.BE.D0.BB.D0.B5.D1.81.D0.BE.D0.BC_.D0.BC.D1.8B.D1.88.D0.B8)
*   [6 Устранение неисправностей](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BD.D0.B5.D0.B8.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BD.D0.BE.D1.81.D1.82.D0.B5.D0.B9)
    *   [6.1 Кнопка Mod4](#.D0.9A.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0_Mod4)
        *   [6.1.1 Mod4 кнопка против пользователей IBM ThinkPad](#Mod4_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0_.D0.BF.D1.80.D0.BE.D1.82.D0.B8.D0.B2_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D0.B5.D0.B9_IBM_ThinkPad)
    *   [6.2 Исправление для Java приложений (серый интерфейс)](#.D0.98.D1.81.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D0.B4.D0.BB.D1.8F_Java_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9_.28.D1.81.D0.B5.D1.80.D1.8B.D0.B9_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.29)
    *   [6.3 Курсор мыши остается в режиме ожидания](#.D0.9A.D1.83.D1.80.D1.81.D0.BE.D1.80_.D0.BC.D1.8B.D1.88.D0.B8_.D0.BE.D1.81.D1.82.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.B2_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5_.D0.BE.D0.B6.D0.B8.D0.B4.D0.B0.D0.BD.D0.B8.D1.8F)
*   [7 Смотрите также](#.D0.A1.D0.BC.D0.BE.D1.82.D1.80.D0.B8.D1.82.D0.B5_.D1.82.D0.B0.D0.BA.D0.B6.D0.B5)

## Установка

Awesome доступен в community:

```
pacman -S awesome

```

Git-based версия также доступна в [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"), смотрите [awesome-git](https://aur.archlinux.org/packages/awesome-git/).

## Запуск awesome

### Без использования менеджера входа в систему

Для запуска awesome без логин менеджера просто добавьте `exec awesome` в ваш скрипт запуска графического окружения (например в ~/.xinitrc.) Подробнее смотрите [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)").

Также возможен автозапуск awesome после авторизации пользователя из виртуальной консоли. Смотрите [Запуск X при входе](/index.php/%D0%97%D0%B0%D0%BF%D1%83%D1%81%D0%BA_X_%D0%BF%D1%80%D0%B8_%D0%B2%D1%85%D0%BE%D0%B4%D0%B5 "Запуск X при входе").

### С использованием менеджера входа в систему

Для запуска awesome из логин менеджера смотрите [эту статью](/index.php/%D0%AD%D0%BA%D1%80%D0%B0%D0%BD%D0%BD%D1%8B%D0%B9_%D0%BC%D0%B5%D0%BD%D0%B5%D0%B4%D0%B6%D0%B5%D1%80 "Экранный менеджер").

#### GDM, LightDM и другие, использующие /usr/share/xsessions/

После установки awesome автоматически создаст конфигурационный файл для этих оконных менеджеров, дающий возможность выбрать awesome при входе в систему.

#### KDM

Создайте следующий файл:

 `/usr/share/apps/kdm/sessions/awesome.desktop` 

```
[Desktop Entry]
Name=Awesome
Comment=Tiling Window Manager
Type=Application
Exec=/usr/bin/awesome
TryExec=/usr/bin/awesome
```

## Конфигурация

Awesome неплохо работает «из коробки», но рано или поздно вы захотите изменить что-нибудь. Конфигурация на языке Lua находится в `~/.config/awesome/rc.lua`.

### Создание файла конфигурации

Во-первых, создайте новый каталог. В нем будет храниться файл конфигурации.

```
$ mkdir -p ~/.config/awesome/

```

Awesome попытается использовать конфигурацию, которая содержится в файле ~/.config/awesome/rc.lua. Он не создается автоматически, поэтому скопируйте шаблон:

```
$ cp /etc/xdg/awesome/rc.lua ~/.config/awesome/rc.lua

```

Синтаксис файла конфигурации часто изменяется при обновлении awesome. Поэтому повторите эту команду, если с awesome произошло что-то непонятное или же вы хотите изменить конфигурацию.

Чтобы получить дополнительную информацию о настройке awesome, посмотрите [Awesome 3 configuration wiki](https://awesome.naquadah.org/wiki/Awesome_3_configuration/ru)

### Источники для файлов конфигурации

**Обратите внимание:** Синтаксис конфигурации awesome регулярно меняется, поэтому Вам скорее всего придется изменить файл, который Вы скачаете.

Отличные примеры файлов rc.lua можно найти по следующим ссылкам:

*   [http://git.sysphere.org/awesome-configs/tree/](http://git.sysphere.org/awesome-configs/tree/) - конфигурации Awesome 3.4 от Adrian C. (anrxc)
*   [http://pastebin.com/f6e4b064e](http://pastebin.com/f6e4b064e) - конфигурация Darthlukan'а для awesome 3.4\.
*   [http://www.calmar.ws/dotfiles/dotfiledir/dot_awesomerc.lua](http://www.calmar.ws/dotfiles/dotfiledir/dot_awesomerc.lua)
*   [http://www.ugolnik.info/downloads/awesome/rc.lua](http://www.ugolnik.info/downloads/awesome/rc.lua) (screen) - Awesome 3 с маленькими строками заголовка и состояния.
*   [http://github.com/nblock/config/blob/master/.config/awesome/rc.lua](http://github.com/nblock/config/blob/master/.config/awesome/rc.lua)
*   Пользовательские конфигурационные файлы на [http://awesome.naquadah.org/wiki/User_Configuration_Files](http://awesome.naquadah.org/wiki/User_Configuration_Files)

### Отладка файла rc.lua при помощи Xephyr

Этот способ редактирования конфигурации предпочтителен, потому что он не изменяет текущий рабочий стол. Для начала скопируйте файл rc.lua в другой файл:

```
$ cp ~/.config/awesome/rc.lua ~/.config/awesome/rc.lua.new

```

Затем можете изменить его как Вам необходимо. Теперь запускайте новый экземпляр awesome в Xephyr (эта программа позволяет запускать вложенный Х-сервер, [screenshot](http://upload.wikimedia.org/wikipedia/commons/d/d7/Xephyr-IceWM-Fluxbox-LinuxMint.png)), используя файл конфигурации rc.lua.new:

```
$ Xephyr -ac -br -noreset -screen 1152x720 :1 &
$ DISPLAY=:1.0 awesome -c ~/.config/awesome/rc.lua.new

```

Преимущество такого подхода в том, что если изменить rc.lua.new, то не нарушится работа текущего экземпляра рабочего стола awesome (а также не потеряются все несохраненные данные, не закроются все экземпляры приложений и т.п.). Как только новые настройки Вас устроят, просто переместите новый файл с конфигурацией на место rc.lua:

```
$ cp ~/.config/awesome/rc.lua.new ~/.config/awesome/rc.lua

```

и перезапустите оконный менеджер.

## Темы оформления

[Beautiful](http://awesome.naquadah.org/wiki/Beautiful) — это библиотека lua, которая позволяет Вам задавать темы оформления для awesome из внешних файлов. С ее помощью весьма легко изменить «на лету» цвета или обои awesome без внесения изменений в файл rc.lua.

Тема по-умолчанию содержится в /usr/share/awesome/themes/default. Скопируйте ее и другие темы:

```
$ cp -r /usr/share/awesome/themes/ ~/.config/awesome/themes/

```

Затем измените путь к теме оформления в файле rc.lua:

```
$ nano ~/.config/awesome/rc.lua

```

Найдите строку beautiful.init('/usr/share/awesome/themes/default/theme.lua')

и замените путь на /home/$USER/.config/awesome/themes/default/theme.lua.

Подробности [здесь](http://awesome.naquadah.org/wiki/Beautiful).

Примеры тем [здесь](http://awesome.naquadah.org/wiki/Beautiful_themes).

### Установка обоев рабочего стола

Beautiful может управлять обоями рабочего стола. Это позволяет задать различные для каждой темы обои. Настройки темы содержатся в файле theme.lua.

Например, вы можете задать обои, изменив путь в строке

theme.wallpaper_cmd = { "awsetbg -f .config/awesome/themes/awesome-wallpaper.png" }

**Обратите внимание:** Чтобы команда awsetbg сработала, вам потребуется программа для установки обоев, например, **[Feh](/index.php/Feh "Feh")**.

#### Случайные фоновые изображения

Чтобы случайно менять фоновые изображения, просто закомментируйте строку из пункта выше и добавьте следующие строки в .xinitrc:

```
while true;
do
  awsetbg -r <path/to/the/directory/of/your/wallpapers>
  sleep 15m
done &

```

## Советы и хитрости

Не стесняйтесь добавлять советы и хитрости, которыми бы Вы хотели поделиться с другими пользователями.

### Использование awesome в GNOME в качестве оконного менеджера

Преимущество GNOME в том, что он сразу работает как нужно. Вы можете использовать awesome для отрисовки окон, а GNOME оставить всю "теневую" работу. За подробностями - в [awesome wiki](https://awesome.naquadah.org/wiki/Quickly_Setting_up_Awesome_with_Gnome).

### Эффект развертывания окон как в compiz

Развертывание представляет возможность увидеть все открытые в данный момент рабочие столы.

Подробная информация [здесь](http://awesome.naquadah.org/wiki/Revelation/ru).

### Скрыть/показать wibox в awesome

Чтобы привязать комбинацию Modkey + b для показа/скрытия строки состояния на активном рабочем столе (как в awesome 2.3), добавьте сочетание клавиш в rc.lua:

```
awful.key({ modkey }, "b", function ()
    mywibox[mouse.screen].visible = not mywibox[mouse.screen].visible
end),

```

### Снимки рабочего стола

Чтобы активировать функцию снимков рабочего стола в awesome, Вам нужна программа для захвата экрана. Для этой цели подойдет scrot - легкая в использовании утилита, которая доступна в репозиториях Arch.

Достаточно выполнить:

```
# pacman -S scrot

```

Также Вы можете установить необязательные пакеты, идущие вместе с этим пакетом, если необходимо.

Затем нужно узнать название клавиши PtrScr, обычно это "Print", но лучше убедиться в этом.

Запускаем:

```
# xev

```

Нажмите кнопку PtrScr, вывод программы будет выглядеть примерно так:

```
 KeyPress event ....
     root 0x25c, subw 0x0, ...
     state 0x0, keycode 107 (keysym 0xff61, **Print**), same_screen YES,
     ....

```

В нашем случае кнопка называется Print.

Теперь приступим к конфигурации awesome.

В блоке с назначениями клавиш (globalkeys) наберите:

```
 awful.key({ }, "Print", function () awful.util.spawn("scrot -e 'mv $f ~/screenshots/ 2>/dev/null'") end),

```

Неплохой идеей будет разместить эту строку ниже сочетания для открытия терминала.

```
 awful.util.spawn(terminal)

```

Эта функция сохраняет снимки рабочего стола в каталог ~/screenshots/, поэтому измените путь, если необходимо.

### Динамические теги

[Eminent](http://awesome.naquadah.org/wiki/Eminent/ru) - это маленькая lua библиотека, которая позволяет быстро привязывать окна к тегам в стиле оконного менеджера wmii. Однако, eminent нацелен на то, чтобы сделать привязку к тегам максимально простой. В действительности, Вам даже не придется менять ваш rc.lua файл, eminent сделает это за Вас.

[Shifty](http://awesome.naquadah.org/wiki/Shifty/ru) - это расширение для awesome 3, которое также осуществляет динамическую привязку к тегам. Вместе с самим расширением поставляется конфигурация, позволяющая ВАМ быть хозяином своего рабочего стола, изменив всего-то пару переменных в конфигурации и поменяв сочетания клавиш.

### Space Invaders

[Space Invaders](http://awesome.naquadah.org/wiki/Space_Invaders) - программа-демонстрация для иллюстрации возможностей Awesome Lua API.

Учтите, что этот пакет не поставляется вместе с пакетом Awesome с релиза 3.4-rc1.

### Naughty для всплывающих уведомлений

См. [awesome wiki](https://awesome.naquadah.org/wiki/Naughty).

### Контекстное меню

По-умолчанию, в awesome3 есть контектсное меню, и настроить его очень просто. Но если вы используете awesome версии 2.x, взгляните на _[awful.menu](http://awesome.naquadah.org/wiki/index.php?title=Awful.menu)_.

Пример конфигурации меню для awesome3:

```
myawesomemenu = {
   { "lock", "xscreensaver-command -activate" },
   { "manual", terminal .. " -e man awesome" },
   { "edit config", editor_cmd .. " " .. awful.util.getdir("config") .. "/rc.lua" },
   { "restart", awesome.restart },
   { "quit", awesome.quit }
}

mycommons = {
   { "pidgin", "pidgin" },
   { "OpenOffice", "soffice-dev" },
   { "Graphic", "gimp" }
}

mymainmenu = awful.menu.new({ items = { 
                                        { "terminal", terminal },
                                        { "icecat", "icecat" },
                                        { "Editor", "gvim" },
                                        { "File Manager", "pcmanfm" },
                                        { "VirtualBox", "VirtualBox" },
                                        { "Common App", mycommons, beautiful.awesome_icon },
                                        { "awesome", myawesomemenu, beautiful.awesome_icon }
                                       }
                             })
```

### Еще виджеты для awesome

_Виджеты в Awesome - это объекты, которые можно размещать на панелях и в заголовках окон, они могут предоставлять различную информацию о системе и очень полезны для получения доступа к этой информации прямо из оконного менеджера. Виджеты легко использовать и они обладают большой гибкостью._ -- источник [[Wiki:Widgets(rus)](https://awesome.naquadah.org/wiki/Widgets_in_awesome/ru)]

Библиотека виджетов **Wicked** (совместима с awesome вплоть до версии 3.4) добавляет новые виджеты, такие как [MPD](https://wiki.archlinux.org/index.php/Music_Player_Daemon_%28%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9%29) виджет, загрузка ЦП, использование оперативной памяти и т.д. Дополнительная информация на странице [Wicked](http://awesome.naquadah.org/wiki/index.php?title=Wicked).

В качестве альтернативы Wicked в awesome 3.4 можно использовать:

*   **[Vicious](http://awesome.naquadah.org/wiki/Vicious)**. Для vicious есть отличная [документация](http://git.sysphere.org/vicious/tree/README).
*   **[Obvious](http://awesome.naquadah.org/wiki/Obvious)**
*   **[Bashets](http://awesome.naquadah.org/wiki/Bashets)**
*   **[Blingbling](http://awesome.naquadah.org/wiki/Blingbling)**

### Прозрачность

У awesome есть поддержка эффекта прозрачности через xcompmgr. Учтите, что Вам вероятно понадобится git-версия xcompmgr, которую можно найти на [AUR](https://aur.archlinux.org/packages.php?ID=16554).

Добавьте эту строчку в ~/.xinitrc

```
exec xcompmgr &

```

Посмотрите _man xcompmgr_ или [xcompmgr](/index.php/Xcompmgr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xcompmgr (Русский)") для дополнительной информации.

В awesome версии 3.4, прозрачность окна можно установить динамически, используя сигналы. Например, файл rc.lua может содержать следующие строки:

```
client.add_signal("focus", function(c)
                              c.border_color = beautiful.border_focus
                              c.opacity = 1
                           end)
client.add_signal("unfocus", function(c)
                                c.border_color = beautiful.border_normal
                                c.opacity = 0.7
                             end)

```

**Если возникнет ошибка про add_signal, замените его на connect_signal.**

Учтите, что при использовании [conky](/index.php/Conky_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Conky (Русский)"), Вы должны указать, что он должен создавать собственное окно, а не использовать рабочий стол. Чтобы сделать это, отредкактируйте ~/.conkyrc:

```
own_window yes
own_window_transparent yes
own_window_type desktop

```

В противном случае можно пронаблюдать, как все окна станут полностью прозрачными.

Начиная с версии awesome 3.1, имеется встроенная поддержка псевдопрозрачности для wibox'ов. Чтобы ее включить, добавьте 2 шестнадцатеричные цифры к цветам в файле конфигурации Вашей темы (~/.config/awesome/themes/default ,обычно является копией /usr/share/awesome/themes/default), как показано в примере:

```
bg_normal = #000000AA

```

где "AA" - это значение прозрачности.

#### ImageMagick

У вас может возникнуть проблема при попытке установить обои командой _display_ из пакета imagemagick (не очень хорошо работает с xcompmgr). awsetbg будет использовать _display_, если не найдет ничего более подходящего. Установите habak, feh, hsetroot или что-нибудь другое (список можно посмотреть командой _grep -A 1 wpsetters /usr/bin/awsetbg_).

### Автозапуск программ

_См. также [страница автозапуска на Awesome wiki](https://awesome.naquadah.org/wiki/Autostart/ru)._

В awesome есть несколько функций для запуска программ (в качестве дополнения к стандартной библиотеке Lua `os.execute`). Чтобы иметь возможность запускать программы при старте, как в GNOME или KDE, установите [dex](https://www.archlinux.org/packages/?name=dex) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)"), а затем включите строку в Ваш файл rc.lua:

```
os.execute"dex -a"

```

Если Вам нужно просто задать список программ для запуска при старте awesome, создайте таблицу со всеми командами:

```
do
  local cmds = 
  { 
    "swiftfox",
    "mutt",
    "consonance",
    "linux-fetion",
    "weechat-curses",
    --and so on...
  }

  for _,i in pairs(cmds) do
    awful.util.spawn(i)
  end
end

```

(Вы также можете запускать программы с помощью `os.execute` с окончанием '`&`', но рациональней будет задать функцию для запуска.)

Чтобы запустить программу, если она еще не запущена, воспользуйтесь командой оболочки `pgrep`, которая запустит программу только в том случае, если не обнаружит процесса с таким же именем:

```
function run_once(prg)
  awful.util.spawn_with_shell("pgrep -u $USER -x " .. prg .. " || (" .. prg .. ")")
end

```

Таким образом, для запуска, например, `parcellite`, только если он уже не запущен:

```
run_once("parcellite")

```

### Передача информации виджетам при помощи awesome-client

Вы можете легко передать текст виджету. Для этого создайте новый виджет:

```
 mywidget = widget({ type = "textbox", name = "mywidget" })
 mywidget.text = "initial text"

```

Для обновления текста из внешнего источника, используйте awesome-client:

```
 echo -e 'mywidget.text = "new text"' | awesome-client

```

Не забудьте добавить виджет в раздел wibox Вашей конфигурации.

### Использование другой панели в awesome

Если вам нравится в awesome все, кроме того, как выглядит стандартная панель, то пришло время установить другую, например xfce4-panel:

```
sudo pacman -S xfce4-panel

```

Конечно, другие панели тоже подойдут. После установки добавьте в автозапуск в rc.lua (прочтите выше, как это сделать). Также можно закомментировать секцию, которая создает wibox'ы для каждого экрана (начинается с "mywibox[s] = awful.wibox({ position = "top", screen = s })"), однако это не обязательно. Не забудьте проверить rc.lua на наличие ошибок командой

```
awesome -k rc.lua

```

Если нужна сторонняя программа запуска, например, Xfrun4, bashrun, посмотрите секцию оконного менеджера [Openbox](/index.php/Openbox_Themes_and_Apps#Application_launchers "Openbox Themes and Apps"). Можно также сменить сочетание клавиш для него на "modkey+R". Не забудьте добавить

```
      properties = { floating = true } },
    { rule = { instance = "$yourapplicationlauncher" },

```

в rc.lua.

### Запретить Nautilus'у отображать рабочий стол (Gnome3)

Запустите dconf-editor. В разделе org->background снимите галочку с "draw-background" и "show-desktop-icons". Все.

Стоит также слинковать /usr/bin/nautilus со скриптом, который выполняет 'nautilus --no-desktop', пропуская все аргументы.

### Переход с GNOME 3

Запустите 'gnome-session-properties' и удалите ненужный программы (Bluetooth Manager, Login Sounds и т.д.).

Если вы хотите избавиться от GDM, убедитесь, что в /etc/rc.conf в секции DAEMONS есть "dbus" (и "cupsd", если у вас есть принтер). Рекомендуется поставить другой логин менеджер ([SLiM](https://wiki.archlinux.org/index.php/SLiM)). Если не хотите этого делать, убедитесь, что верно отредактировали [.xinitrc](https://wiki.archlinux.org/index.php/Udev) и поставьте что-нибудь типа devmon ([AUR](https://aur.archlinux.org/packages.php?ID=45842)).

Чтобы сохранить удобные апплеты в системном лотке, а также тему оформления GTK, добавьте в rc.lua:

```
function start_daemon(dae)
	daeCheck = os.execute("ps -eF | grep -v grep | grep -w " .. dae)
	if (daeCheck ~= 0) then
		os.execute(dae .. " &")
	end
end

```

```
procs = {"gnome-settings-daemon", "nm-applet", "kupfer", "gnome-sound-applet", "gnome-power-manager"}
for k = 1, #procs do
	start_daemon(procs[k])
end

```

### Не менять теги колесом мыши

В файле rc.lua, секцию Mouse Bindings замените на

```
-- {{{ Mouse bindings
root.buttons(awful.util.table.join(
    awful.button({ }, 3, function () mymainmenu:toggle() end)))
-- }}} 

```

## Устранение неисправностей

### Кнопка Mod4

По-умолчанию, кнопкой Mod4 является **Win**. Если по каким-то причинам она не работает, проверьте код Вашей кнопки Mod4:

```
$ xev

```

Должно быть 115 для левой кнопки Win. Затем включите строку в файл ~/.xinitrc:

```
xmodmap -e "keycode 115 = Super_L" -e "add mod4 = Super_L"
exec awesome

```

#### Mod4 кнопка против пользователей IBM ThinkPad

IBM ThinkPad не поставлялись с кнопкой Win (хотя компания Lenovo уже изменила этой традиции). Кнопка Alt по-умолчанию не используется в комбинациях, описанных в rc.lua. Это позволит Вам заменить ею кнопку Win. Чтобы сделать это, необходимо отредактировать rc.lua, заменив:

```
modkey = "Mod4"

```

на:

```
modkey = "Mod1"

```

**Обратите внимание:** В awesome используются несколько сочетаний клавиш типа Mod4 + буква на клавиатуре. Изменив Mod4 на Alt, Вы можете получить наложение некоторых сочетаний. Эти сочетания придется также перебросить на другие кнопки.

Если Вы не хотите менять стандартные сочетания для awesome, Вы можете использовать другую кнопку. Например, Caps Lock используется нечасто, поэтому можно использовать ее в качестве Mod4\. Измените ~/.Xmodmap:

```
clear lock 
add mod4 = Caps_Lock

```

и [(пере)загрузите](https://wiki.archlinux.org/index.php/Extra_Keyboard_Keys_in_Xorg_%28%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9%29) файл. Это действие изменит Caps Lock на кнопку Mod4 и Вы сможете воспользоваться стандартными настройками awesome. Вдобавок, это позволит использовать Caps Lock как Mod4 и в других X-приложениях.

### Исправление для Java приложений (серый интерфейс)

Взято с [[1]](https://bbs.archlinux.org/viewtopic.php?pid=450870).

1.  Установите [wmname](https://www.archlinux.org/packages/?name=wmname).
2.  Выполните следующую команду или добавьте ее в {Filename|.xinitrc}}: `wmname LG3D` 

### Курсор мыши остается в режиме ожидания

Иногда, после запуска программы с помощью _awful.util.spawn_ курсор мыши остаётся в занятом режиме/режиме часов. Такое может наблюдаться, например при создании скриншота программой scrot используя клаившу PrintScreen. Чтобы отключить такое поведение глобально, добавьте в конец вашего `~/.rc.lua` следующий код:

```
-- отключить уведомление загрузки глобально
local oldspawn = awful.util.spawn
awful.util.spawn = function (s)
  oldspawn(s, false)
end

```

Для подробностей, смотрите [[отключение уведомлений запуска](http://awesome.naquadah.org/wiki/Disable_startup-notification_globally/ru%7CГлобальное)]

## Смотрите также

*   [http://archlinux.org.ru/forum/topic/11748/](http://archlinux.org.ru/forum/topic/11748/) - Анатомия awesome
*   [http://archlinux.org.ru/forum/topic/15184/](http://archlinux.org.ru/forum/topic/15184/) - Установка Awesome 3.5.6 и доведение его до рабочего состояния
*   [https://awesome.naquadah.org/wiki/Main_Page/ru](https://awesome.naquadah.org/wiki/Main_Page/ru) - Русскоязычная wiki awesome
*   [http://awesome.naquadah.org/wiki/FAQ](http://awesome.naquadah.org/wiki/FAQ) - ЧаВо
*   [http://www.lua.org/pil/](http://www.lua.org/pil/) - Программирование на Lua
*   [http://awesome.naquadah.org/](http://awesome.naquadah.org/) - Официальный сайт awesome
*   [http://awesome.naquadah.org/wiki/FAQ/ru](http://awesome.naquadah.org/wiki/FAQ/ru) - страница awesome wiki
*   [http://www.penguinsightings.org/desktop/awesome/](http://www.penguinsightings.org/desktop/awesome/) - Обзор
*   [http://compsoc.tardis.ed.ac.uk/wiki/AwesomeWM_guide](http://compsoc.tardis.ed.ac.uk/wiki/AwesomeWM_guide) - Гайд по Awesome
*   [https://bbs.archlinux.org/viewtopic.php?id=88926](https://bbs.archlinux.org/viewtopic.php?id=88926) - поделитесь своим awesome!
*   [http://help.ubuntu.ru/wiki/awesome](http://help.ubuntu.ru/wiki/awesome) - Отличная русскоязычная документация