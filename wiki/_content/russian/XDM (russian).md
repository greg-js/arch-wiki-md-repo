Согласно [странице руководства XDM](http://www.xfree86.org/current/xdm.1.html):

*Xdm управляет набором X дисплеев, которые могут находиться на локальном компьютере или на удалённом сервере. [...] Xdm выполняет функции, похожие на те, что предоставляются утилитами init, getty и login для текстовых терминалов: предлагает ввести имя пользователя и пароль, проводит аутентификацию пользователя и запускает "сессию."*

XDM предоставляет простой и прямолинейный графический интерфейс для входа в систему.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Фоны для XDM](#.D0.A4.D0.BE.D0.BD.D1.8B_.D0.B4.D0.BB.D1.8F_XDM)
*   [3 Проблемы и решения](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D0.B8_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [3.1 XDM отображается повторно после входа в систему](#XDM_.D0.BE.D1.82.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D0.B2.D1.82.D0.BE.D1.80.D0.BD.D0.BE_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.B2.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.83)

## Установка

Установите пакет [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm), доступный в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Далее возможны два варианта:

Можно использовать скрипт **~/.xsession** Для этого нужно разрешить выполнение файла `~/.xsession`.

```
$ cp /etc/skel/.xsession /etc/skel/.xinitrc ~ # use default launch script

```

Или обойтись одной строкой (предположим, вы используете оконный менеджер 'openbox')

```
$ echo exec openbox > ~/.xsession
$ chmod 744 ~/.xsession

```

Если вы также хотите установить тему “Arch Linux” для XDM, вам поможет пакет [xdm-archlinux](https://www.archlinux.org/packages/?name=xdm-archlinux) (также доступен в официальном репозитории).

Дополнительная информация доступна здесь: [Display Manager](/index.php/Display_manager_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Display manager (Русский)").

## Фоны для XDM

Только что установленный XDM не блещет красотой и изяществом. К счастью, можно его украсить при помощи фоновых изображений:

*   Установите Quick Image Viewer:

 `# pacman -S qiv` 

*   Создайте директорию для хранения фонов (например, `/root/backgrounds` или `/usr/local/share/backgrounds`).

*   Поместите изображения во вновь созданную папку. Если у вас нет подходящих картинок, сходите на [[1]](http://www.digitalblasphemy.com/).

*   Отредактируйте `/etc/X11/xdm/Xsetup_0`. Измените команду `xconsole` на

/usr/bin/qiv -zr /root/backgrounds/* если /root/backgrounds – ваша папка с фоновыми изображениями.

*   Отредактируйте `/etc/X11/xdm/Xresources`. Добавьте или замените следующие строки:

```
xlogin*greetFont: -adobe-helvetica-bold-o-normal--20-*-*-*-*-*-iso8859-1
xlogin*font: -adobe-helvetica-medium-r-normal--14-*-*-*-*-*-iso8859-1
xlogin*promptFont: -adobe-helvetica-bold-r-normal--14-*-*-*-*-*-iso8859-1
xlogin*failFont: -adobe-helvetica-bold-r-normal--14-*-*-*-*-*-iso8859-1
xlogin*frameWidth: 1
xlogin*innerFramesWidth: 1
xlogin*logoPadding: 0
xlogin*geometry: 300x175-0-0

```

Закомментируйте строки, касающиеся логотипа:

```
#xlogin*logoFileName: /usr/X11R6/lib/X11/xdm/pixmaps/xorg.xpm
#xlogin*logoFileName: /usr/X11R6/lib/X11/xdm/pixmaps/xorg-bw.xpm

```

Чтобы узнать точное значение каждого параметра, обратитесь к man-странице xdm.

*   Обновите `/etc/pacman.conf` , чтобы сделанные изменения не были затёрты:

```
~NoUpgrade = etc/X11/xdm/Xsetup_0 etc/X11/xdm/Xresources

```

В реультате этих изменений будет отображен случайный фон, а панель логина будет смещена в крайний правый угол экрана.

## Проблемы и решения

### XDM отображается повторно после входа в систему

В текущую версию пакета [xorg-xdm](https://www.archlinux.org/packages/?name=xorg-xdm), доступную в [официальных репозиториях](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Official repositories (Русский)").

Также убедитесь, что ваш оконный менеджер вообще должен запускаться. Например, что соответствующая строка присутствует в файле`~/.xsession`. Сам `~/.xsession` должен иметь корректные права доступа: `774`.

Ошибка может происходить, если в домашней папке кончилось дисковое пространство.