**Обратите внимание:** Эта статья является дополнением к основной: [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)").

Эта wiki страница призвана помочь пользователям в настройке Openbox в Arch Linux. В статье описывается как можно настроить темы, системные иконки, итп. А так же тут содержится краткий обзор панелей, трея и вспомогательных программ.

## Contents

*   [1 Внешний вид и темы](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B9_.D0.B2.D0.B8.D0.B4_.D0.B8_.D1.82.D0.B5.D0.BC.D1.8B)
    *   [1.1 Темы Openbox](#.D0.A2.D0.B5.D0.BC.D1.8B_Openbox)
    *   [1.2 Внешний вид в среде X11](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B9_.D0.B2.D0.B8.D0.B4_.D0.B2_.D1.81.D1.80.D0.B5.D0.B4.D0.B5_X11)
    *   [1.3 X11 курсоры мыши](#X11_.D0.BA.D1.83.D1.80.D1.81.D0.BE.D1.80.D1.8B_.D0.BC.D1.8B.D1.88.D0.B8)
    *   [1.4 Темы GTK](#.D0.A2.D0.B5.D0.BC.D1.8B_GTK)
        *   [1.4.1 GTK2/ GTK+](#GTK2.2F_GTK.2B)
        *   [1.4.2 GTK1](#GTK1)
        *   [1.4.3 Шрифты GTK](#.D0.A8.D1.80.D0.B8.D1.84.D1.82.D1.8B_GTK)
        *   [1.4.4 Иконки GTK](#.D0.98.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_GTK)
    *   [1.5 Иконки рабочего стола](#.D0.98.D0.BA.D0.BE.D0.BD.D0.BA.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
    *   [1.6 Обои рабочего стола](#.D0.9E.D0.B1.D0.BE.D0.B8_.D1.80.D0.B0.D0.B1.D0.BE.D1.87.D0.B5.D0.B3.D0.BE_.D1.81.D1.82.D0.BE.D0.BB.D0.B0)
*   [2 Рекомендуемые программы](#.D0.A0.D0.B5.D0.BA.D0.BE.D0.BC.D0.B5.D0.BD.D0.B4.D1.83.D0.B5.D0.BC.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)
    *   [2.1 Менеджеры входа в систему (login managers)](#.D0.9C.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83_.28login_managers.29)
    *   [2.2 Композитные менеджеры](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.BE.D0.B7.D0.B8.D1.82.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B)
    *   [2.3 Панели, Трей, Пейджеры](#.D0.9F.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8.2C_.D0.A2.D1.80.D0.B5.D0.B9.2C_.D0.9F.D0.B5.D0.B9.D0.B4.D0.B6.D0.B5.D1.80.D1.8B)
        *   [2.3.1 Панели](#.D0.9F.D0.B0.D0.BD.D0.B5.D0.BB.D0.B8)
        *   [2.3.2 Трей](#.D0.A2.D1.80.D0.B5.D0.B9)
        *   [2.3.3 Пейджеры](#.D0.9F.D0.B5.D0.B9.D0.B4.D0.B6.D0.B5.D1.80.D1.8B)
    *   [2.4 Файловые менеджеры](#.D0.A4.D0.B0.D0.B9.D0.BB.D0.BE.D0.B2.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80.D1.8B)
    *   [2.5 Быстрый запуск приложения (Application launchers)](#.D0.91.D1.8B.D1.81.D1.82.D1.80.D1.8B.D0.B9_.D0.B7.D0.B0.D0.BF.D1.83.D1.81.D0.BA_.D0.BF.D1.80.D0.B8.D0.BB.D0.BE.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F_.28Application_launchers.29)
        *   [2.5.1 Dmenu](#Dmenu)
        *   [2.5.2 Gmrun](#Gmrun)
        *   [2.5.3 Bashrun2](#Bashrun2)
        *   [2.5.4 Kupfer](#Kupfer)
        *   [2.5.5 Launchy](#Launchy)
        *   [2.5.6 Gnome-panel](#Gnome-panel)
    *   [2.6 Менеджер буфера обмена](#.D0.9C.D0.B5.D0.BD.D0.B5.D0.B4.D0.B6.D0.B5.D1.80_.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0_.D0.BE.D0.B1.D0.BC.D0.B5.D0.BD.D0.B0)
    *   [2.7 Аплеты управления звуком](#.D0.90.D0.BF.D0.BB.D0.B5.D1.82.D1.8B_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.B7.D0.B2.D1.83.D0.BA.D0.BE.D0.BC)
        *   [2.7.1 Gvolwheel, gvtray](#Gvolwheel.2C_gvtray)
        *   [2.7.2 Obmixer, PNMixer](#Obmixer.2C_PNMixer)
        *   [2.7.3 Volti](#Volti)
        *   [2.7.4 Volumeicon, volwheel](#Volumeicon.2C_volwheel)
    *   [2.8 Батарея & CPU](#.D0.91.D0.B0.D1.82.D0.B0.D1.80.D0.B5.D1.8F_.26_CPU)
        *   [2.8.1 Trayfreq](#Trayfreq)
    *   [2.9 Индикаторы раскладки клавиатуры](#.D0.98.D0.BD.D0.B4.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D1.80.D1.8B_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
        *   [2.9.1 Fbxkb, xxkb, axkb](#Fbxkb.2C_xxkb.2C_axkb)
        *   [2.9.2 xneur](#xneur)
    *   [2.10 Диалог выхода из сеанса](#.D0.94.D0.B8.D0.B0.D0.BB.D0.BE.D0.B3_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B0_.D0.B8.D0.B7_.D1.81.D0.B5.D0.B0.D0.BD.D1.81.D0.B0)

## Внешний вид и темы

В дополнение к статье о темах Openbox, эта статья нацелена на пользователей, которые используют Openbox как самостоятельное рабочее окружение, без содействия с другими окружениями (GNOME, KDE или Xfce).

### Темы Openbox

Темы в Openbox отвечают за внешний вид краёв окна декоратора, в том числе декорации заголовков и кнопки расположенные на них. Так же темы контролируют внешний вид мею приложений и всплывающих сообщений (в случае, если прорисовкой приложение не занимается самостоятельно)

Дополнительные темы доступны в стандартных репозиториях:

```
# pacman -S openbox-themes

```

Данный пакет с темами не вмещает в себе все возможные темы. Дополнительно вы можете скачать больше других тем на разнообразных ресурсах, например:

*   [box-look.org](http://www.box-look.org/index.php?xcontentmode=7402)
*   [customize.org](http://customize.org/browse/tags/openbox)
*   [http://www.minuslab.net/themes/](http://www.minuslab.net/themes/)
*   [http://celo.wordpress.com/themes/](http://celo.wordpress.com/themes/)
*   [http://vault.openmonkey.com/pages/openbox](http://vault.openmonkey.com/pages/openbox)
*   [http://hewphoria.com/?p=submission&type=theme&cat=7](http://hewphoria.com/?p=submission&type=theme&cat=7)

Скачаные темы должны быть распакованы в директорию по пути `~/.themes` так-же вы можете установить данные темы с помощью утилиты ObConf.

Создание собственных тем весьма не сложно. Подробные инструкции доступны на странице проекта [well-documented](http://openbox.org/wiki/Help:Themes)

Для создания и редактирования тем по средством графического интерфейса (GUI), можно воспользоваться редактором тем, который доступен по адресу [ObTheme](http://xyne.archlinux.ca/info/obtheme).

### Внешний вид в среде X11

Если вы используете Openbox как самостоятельное окружение, вы должны провести конфигурацию файла .Xdefaults Сохраните и сделайте копию в директорию ~/.Xdefaults и /root/.Xdefaults, для окон, запущенных от пользователя Root.

Xdefaults это конфигурационный файл, вносящий изменения для каждого пользователя отдельно. По-умолчанию он располагается в корне домашней директории (~/.Xdefaults). Параметры, указанные в файле, перечитываются программой xrdb (Xorg resource database), которая является частью программы Xorg, и это действие происходит во время старта последнего. В возможности конфигурации входит:

*   определение цветов в терминале
*   изменение настроек терминала
*   определение параметров для шрифтов в X (DPI, сглаживание, хинтинг(hinting))
*   изменение темы системного курсора
*   определение темы xscreensaver
*   альтернативные настройки для низкоуровневых программ для X (xclock, xpdf,итп.)

Xdefaults Arch WiKi [https://wiki.archlinux.org/index.php/Xdefaults](https://wiki.archlinux.org/index.php/Xdefaults)

### X11 курсоры мыши

Распакуйте и поместите желаемую тему либо по пути `/usr/share/icons` (для доступа со всей системы) или `~/.icons` (только локально доступная тема для вашего пользователя) Так же некоторое количество тем доступно в репозиториях, их можно установить по средством pacman.

Добавьте эту строку в `~/.Xdefaults`:

```
Xcursor.theme:   [name-of-cursor-theme]

```

где `[name-of-cursor-theme]` название директории темы. Например:

```
Xcursor.theme:	Vanilla-DMZ-AA

```

Для изменения размера:

```
Xcursor.size: [size]

```

Иногда необходимо создание символьной ссылки к системной директории с необходимой темой (её папкой) и нужной папкой в директории пользователя:

```
$ mkdir ~/.icons
$ ln -s /usr/share/icons/[name-of-cursor-theme] ~/.icons/default

```

Для более подробной информации ознакомьтесь с более подробной страницей Arch WiKi [https://wiki.archlinux.org/index.php/X11_Cursors](https://wiki.archlinux.org/index.php/X11_Cursors)

### Темы GTK

#### GTK2/ GTK+

Первым делом раcпакуйте и разместите желанные темы в `/usr/share/themes` (для доступа со всей системы) или `~/.themes` (только локально доступная тема для вашего пользователя), после чего:

Темами GTK+ можно легко управлять с помощью программ, таких как **[lxappearance](/index.php/LXDE "LXDE")**, **gtk-chtheme**, or **switch2**. Для их установки, выполните в терминале:

```
# pacman -S lxappearance

```

и\или

```
# pacman -S gtk-chtheme

```

и\или

```
# pacman -S gtk-theme-switch2

```

Теперь запустите `lxappearance`, `gtk-chtheme` или `switch2` для выбора и установки желаемой темы.

Если у вас установлен и используется `gnome-settings-daemon`, вы можете испытать трудности в изменении темы GTK, в виду того, что он возвращает вид к оригинальной теме GTK. По-умолчанию autostart.sh имеет возможность запуска `gnome-settings-daemon`. Потому убедитесь, что данное приложение у вас не запущенно.

#### GTK1

Для обратной совместимости с темами GTK1, установите пакет **gtk-theme-switch**:

```
# pacman -S gtk-theme-switch

```

После чего запустите `switch` для выбора желаемой темы..

#### Шрифты GTK

Для редактирования темы и размера шрифтов, добавьте в `~/.gtkrc.mine` секцию вида:

```
style "user-font"
{
font_name = "[font-name] [size]"
}
widget_class "*" style "user-font"
gtk-font-name = "[font-name] [size]"

```

где `[font-name] [size]` необходимый шрифт и его размер. Пример:

```
style "user-font"
{
font_name = "DejaVu Sans 8"
}
widget_class "*" style "user-font"
gtk-font-name = "DejaVu Sans 8"

```

Оба поля `font_name` и `gtk-font-name` обеспечивают обратную совместимость.

Таже можно воспользоваться утилитами **gtk-chtheme** или **lxappearance** для настройки GTK шрифта.

#### Иконки GTK

Для начала разпакуйте выбранные темы в `/usr/share/icons` (для доступа со всей системы) или `~/.icons` (только локально доступная тема для вашего пользователя), после чего:

Добавте\отредактируйте строку в файле `~/.gtkrc.mine`:

```
gtk-icon-theme-name = "[name-of-icon-theme]"

```

где `[name-of-icon-theme]` имя директории с темой иконок. Пример:

```
gtk-icon-theme-name = "Tango"

```

Убедитесь что бы `~/.gtkrc-2.0` использовал параметры с `~/.gtkrc.mine`:

```
# ~/.gtkrc-2.0
# -- THEME AUTO-WRITTEN DO NOT EDIT
include "/usr/share/themes/Rezlooks-Gilouche/gtk-2.0/gtkrc"
include "/home/username/.gtkrc.mine"
# -- THEME AUTO-WRITTEN DO NOT EDIT

```

Так-же для изменений тем иконок можно воспользоваться **lxappearance**. Как альтернативой, можно воспользоваться [lxappearance2-git](https://aur.archlinux.org/packages.php?ID=39339) с пользовательских репозиториев AUR для управления и настройки темами мыши, темами GTK, и темами иконок.

### Иконки рабочего стола

По-умолчанию Openbox не поддерживает функции отображения иконок рабочего стола. Для достижения этой функции можно воспользоваться программами, которые способны это реализовать: Xfdesktop, PcmanFM, [ROX](http://rox.sourceforge.net), [iDesk](/index.php/Idesk "Idesk"), или даже Nautilus (и gnome-settings-daemon)

ROX и PCmanFM имеют дополнительное преимущество в поддержке функции легковесных файловых менеджеров.

### Обои рабочего стола

По-умолчанию Openbox не имеет функции смены обоев рабочего стола. Реализовать этот функционал можно с помощью таких программ как [Feh](/index.php/Feh "Feh") и [Nitrogen](/index.php/Nitrogen "Nitrogen"). Другие возможности реализованы так же в ImageMagick, hsetroot и xsetbg. Стоит еще сообщить о возможности реализации этой возможности по средством Pcmanfm и Xfdesktop.

Вы можете выключить функцию управления и загрузки обоев в gnome-settings-daemon:

```
$ gconftool-2 --set /apps/gnome_settings_daemon/plugins/background/active --type bool False

```

В Gnome 3 используйте:

```
$ gsettings set org.gnome.desktop.background draw-background false

```

## Рекомендуемые программы

**Обратите внимание:** The <u>main</u> [Openbox](/index.php/Openbox "Openbox") основная статья по установке Openbox.

В этой <u>справочной</u> части wiki рассматриваются программы, которые вы можете использовать для реализации дополнительного функционала, после установки Openbox.

Смотрите статью [Список приложений](/index.php/%D0%A1%D0%BF%D0%B8%D1%81%D0%BE%D0%BA_%D0%BF%D1%80%D0%B8%D0%BB%D0%BE%D0%B6%D0%B5%D0%BD%D0%B8%D0%B9 "Список приложений"), в которой перечислено в том числе легковесное программное обеспечение, прекрасно подходящее для работы в Openbox.

### Менеджеры входа в систему (login managers)

[SLiM](http://slim.berlios.de/) легковесный менеджер входа в систему. Он предназначен для использования при использовании Openbox как самостоятельное окружение. Пройдите по ссылке Arch's [SLiM](/index.php/SLiM "SLiM") wiki для более подробных деталей.

[Qingy](http://qingy.sourceforge.net/) легковесный, гибкий в настройках менеджер входа в систему. Поддерживает вход в систему как через X так и через терминал. Он использует [DirectFB](http://www.directfb.org). Qingy не запускает X-сессию пока вы не выберете сессию (окружение), которое будет использовать X. Дополнительная информация доступна по ссылке [Qingy](/index.php/Qingy "Qingy") в Arch wiki.

### Композитные менеджеры

[Xcompmgr](/index.php/Xcompmgr_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xcompmgr (Русский)") легковесный композитный менеджер, способный прорисовывать тени, анимацию затухания, и прозрачность в среде Openbox и других оконных менеджеров. (Стоит отметить что xcompmgr больше не поддерживается и не развивается. Потому любые возникшие с ним проблемы наврядли будут когда-либо исправлены) (Работая вместе с запущенным tint2 0.9, иконки из трея могут отображаться не корректно или не отображаться вовсе)

[Cairo Composite Manager](/index.php/Cairo_Compmgr "Cairo Compmgr") -- Универсальный и расширяемый композитный менеджер, технология работы, которого, использует для работы cairo.

### Панели, Трей, Пейджеры

Некоторые программы, реализующие панели, системный трей, итп.:

#### Панели

| 

  [Avant window navigator](/index.php/Avant_Window_Navigator "Avant Window Navigator")
  [BMPanel](http://nsf.110mb.com/bmpanel/)
  [Cairo-Dock](/index.php/Cairo-Dock "Cairo-Dock")
  [Fbpanel](http://fbpanel.sourceforge.net)
  [Fspanel](http://freshmeat.net/projects/fspanel/)

 | 

    [Gnome-panel](http://live.gnome.org/GnomePanel/)
    [LXPanel](http://www.gnomefiles.org/app.php/LXPanel)
    [Pancake](http://www.failedprojects.de/pancake/)
    [PerlPanel](http://freshmeat.net/projects/perlpanel/)
    [PyPanel](/index.php/PyPanel "PyPanel")

 | 

      [Screenlets](http://www.screenlets.org/)
      [Tint2](/index.php/Tint2 "Tint2")
      [Wbar](http://code.google.com/p/wbar/)
      [Xfce4-panel](http://www.xfce.org/projects/xfce4-panel/)

 |

#### Трей

*   [Stalonetray](/index.php/Stalonetray "Stalonetray")
*   [Trayer](http://download.gna.org/fvwm-crystal/trayer/1.0/)

#### Пейджеры

  [IPager](http://useperl.ru/ipager/index.en.html)
  [Neap](http://code.google.com/p/neap/)
  [Netwmpager](https://aur.archlinux.org/packages.php?ID=17563)
  [pager-multihead](https://aur.archlinux.org/packages.php?ID=51536)

### Файловые менеджеры

Два популярных и легковесных файловых менеджера:

*   [Thunar](/index.php/Thunar "Thunar")  Thunar поддерживает автомонтирование и его функционал может раcширяться плагинами.

```
# pacman -S thunar

```

*   [ROX](http://rox.sourceforge.net) ROX имеет возможность отображения значков на рабочем столе.

```
# pacman -S rox

```

*   [PCManFM](http://pcmanfm.sourceforge.net) легковесный файловый менеджер.

```
# pacman -S pcmanfm   #  PcManFM так же умеет отображать значки на рабочем столе.
# pacman -S ntfs-3g   #  Этот пакет позволяет PCManFM получать доступ и читать NTFS разделы.

```

Для еще большей легковесности системы можно использовать For even lighter options, consider [Gentoo](http://www.obsession.se/gentoo/) или [emelFM2.](http://emelfm2.net/). Эти программы реализованы в классическом двухпанельном виде. Другие менеджеры: [xfe](http://sourceforge.net/projects/xfe/) и [muCommander.](http://www.mucommander.com/)

Как альтернативу, вы можете использовать Nautilus из окружения GNOME. Этот менеджер тяжелее и медленней чем вышеназванные менеджеры, но Nautilus поддерживает [виртуальные файловые системы,](http://en.wikipedia.org/wiki/Virtual_file_system) и умеет реализовывать доступ к папкам по средствам SSH, FTP и Samba. Ето его преимущество, перед другими менеджерами файлов.

### Быстрый запуск приложения (Application launchers)

#### Dmenu

Настройте программу следую инструкциям по ссылке [dmenu](/index.php/Dmenu "Dmenu"). После этого добавте\отредактируйте следующую секцию <keyboard> в `~/.config/openbox/rc.xml` для привязки комбинации клавиш к запуску dmenu:

```
   <keybind key="W-space">
     <action name="Execute">
       <execute>dmenu_run</execute>
     </action>
   </keybind>

```

#### [Gmrun](/index.php/Gmrun "Gmrun")

[gmrun](http://sourceforge.net/projects/gmrun) реализует превосходную работу Диалога быстрого запуска, повторяя возможности программ из окружения Gnome и KDE, запускаемые в них по комбинации Alt+F2:

```
# pacman -S gmrun

```

Для справки - ознакомьтесь с страницей Gmrun [здесь](/index.php/Gmrun "Gmrun") и настройте запуск по комбинации Alt+F2, через файл `~/.config/openbox/rc.xml`:

```
<keybind key="A-F2">
<action name="execute"><execute>gmrun</execute></action>
</keybind>

```

#### Bashrun2

[bashrun2](http://bashrun.sourceforge.net) реализует альтернативную панель быстрого запуска приложений, по средствам запуска диалога через маленькое окно xterm. Программа доступна в репозитории [AUR](https://aur.archlinux.org/packages.php?ID=43465) и пожет стартовать по Alt+F2 через добавление в секцию из файла `~/.config/openbox/rc.xml` следующего текста:

```
   <application name="bashrun2-run-dialog">
     <desktop>all</desktop>
     <decor>no</decor>  # switch to yes if you prefer a bordered window
     <focus>yes</focus>
     <skip_pager>yes</skip_pager>
     <layer>above</layer>
   </application>

```

#### Kupfer

[Kupfer](https://aur.archlinux.org/packages.php?ID=27896) еще одна программа запуска приложений, написан на Python.

#### Launchy

[Launchy](http://www.launchy.net/) основой есть подход с политикой минимализма. копирует функционал Gnome Do.

```
# pacman -S launchy

```

Для быстрого запуска использует комбинацию клавиш Ctrl+Space.

#### Gnome-panel

Диалог запуска при установленном окружением GNOME:

```
gnome-panel-control --run-dialog

```

### Менеджер буфера обмена

Вы можете попробовать установить менеджер буфера обмена.

**xfce4-clipman-plugin, parcellite,** или **glipper-old** могут быть установлены через pacman. Добавьте выбранный менеджер в **`autostart.sh`.**

### Аплеты управления звуком

#### Gvolwheel, gvtray

[gvolwheel](https://aur.archlinux.org/packages/gvolwheel/) - аудиомикшер, который интегрируется в системный трей. Форк *gvolwheel* - [gvtray](https://aur.archlinux.org/packages/gvtray/).

#### Obmixer, PNMixer

Obmixer написан на C. Хорошая альтернатива другим миксерам звука. [obmixer](https://aur.archlinux.org/packages.php?ID=31131) в AUR. Obmixer больше не поддерживается.

PNMixer форк Obmixer. [PNMixer](https://aur.archlinux.org/packages.php?ID=48899) в AUR.

#### Volti

Volti это приложение на GTK+ для управления громкостью звука, через системный трей. [volti](https://aur.archlinux.org/packages.php?ID=33525) в AUR.

#### Volumeicon, volwheel

Volumeicon миксер звука в трее. [volumeicon](https://www.archlinux.org/packages/?name=volumeicon) в AUR.

Volwheel интегрируется в трей, позволяет управлять звуком. [volwheel](https://www.archlinux.org/packages/community/any/volwheel/) в AUR.

### Батарея & CPU

#### Trayfreq

[Trayfreq](/index.php/Trayfreq "Trayfreq") легковесный монитор состояния заряженности батареи.

### Индикаторы раскладки клавиатуры

#### Fbxkb, xxkb, axkb

Индикатор и управляющая программа [fbxkb](https://aur.archlinux.org/packages/fbxkb/) в AUR.

Индикатор раскладки [xxkb](https://www.archlinux.org/packages/community/i686/xxkb/) в AUR.

Индикатор написаный на QT4 [axkb](https://aur.archlinux.org/packages.php?ID=25555) в AUR.

#### xneur

X neural switcher это анализатор текста. Программа анализирует язык вводимого текста, и меняет раскладку, если это необходимо. [aneur](https://aur.archlinux.org/packages.php?ID=9750) в AUR.

### Диалог выхода из сеанса

*   [exitx](https://aur.archlinux.org/packages/exitx/)
*   [exitx-polkit](https://aur.archlinux.org/packages/exitx-polkit/)
*   [obshutdown](https://aur.archlinux.org/packages/obshutdown/)

Альтернативой может быть реализация выхода и выключения средствами самой системы.

Примером может быть реализация `exit-menu` в Exit (используя PolicyKit/Dbus):

```
<menu id="exit-menu" label="Exit">
	<item label="Log Out">
		<action name="Execute">
			<command>openbox --exit</command>
		</action>
	</item>
	<item label="Shutdown">
		<action name="Execute">
			<command>dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Stop</command>
		</action>
	</item>
	<item label="Restart">
		<action name="Execute">
			<command>dbus-send --system --print-reply --dest="org.freedesktop.ConsoleKit" /org/freedesktop/ConsoleKit/Manager org.freedesktop.ConsoleKit.Manager.Restart</command>
		</action>
	</item>
	<item label="Suspend">
		<action name="Execute">
		<command>dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Suspend</command>
		</action>
	</item>
	<item label="Hibernate">
		<action name="Execute">
		<command>dbus-send --system --print-reply --dest="org.freedesktop.UPower" /org/freedesktop/UPower org.freedesktop.UPower.Hibernate</command>
		</action>
	</item>
</menu>

```

Добавьте это в ваш menu.xml, и добавьте в ваше меню выов:

```
<menu id="exit-menu"/>

```

Если вы желаете привязать это к комбинации клавиш, добавьте этот текст в ваш rc.xml:

```
<keybind key="XF86PowerOff">
  <action name="ShowMenu">
      <menu>exit-menu</menu>
  </action>
</keybind>

```

Это привяжет действие к кнопке выключения компьютера, если вы хотите другую клавишу, измените XF86PowerOff на вашу клавишу.