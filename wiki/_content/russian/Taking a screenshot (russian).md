## Contents

*   [1 import](#import)
*   [2 gimp](#gimp)
*   [3 xwd](#xwd)
*   [4 scrot](#scrot)
*   [5 KDE](#KDE)
*   [6 GNOME](#GNOME)
*   [7 Виртуальная консоль](#.D0.92.D0.B8.D1.80.D1.82.D1.83.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D0.BA.D0.BE.D0.BD.D1.81.D0.BE.D0.BB.D1.8C)

## import

Простым способом сделать скриншот является использование команды import:

```
import -window root screenshot.jpg

```

import часть пакета imagemagick.

В случае, если вам нужно получить скриншот отдельного окна, вы можете использовать xwininfo для нахождения id окна. Просто выполните нижеприведённую команду и щёлкните мышкой по окну, скриншот которого надо получить.

```
import -window `xwininfo |grep 'Window id:' |cut -d" " -f4` screenshot.jpg

```

Если вы используете twinview или dualhead, просто сделайте скриншот дважды и используйте imagemagick для их совмещения:

```
import -window root -display :0.0 -screen /tmp/0.png
import -window root -display :0.1 -screen /tmp/1.png
convert +append /tmp/0.png /tmp/1.png screenshot.png
rm /tmp/{0,1}.png

```

## gimp

Вы так-же можете делать скриншоты при помощи gimp (File -> Acquire -> Screenshot ...(Файл -> Создать -> Снимок экрана...)).

## xwd

xwd часть пакета xorg-apps.

Пример скриншота основного окна:

```
xwd -root -out screenshot.xwd

```

## scrot

Scrot, доступен в [extra](/index.php/Official_repositories_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#extra "Official repositories (Русский)") и позволяет получить скриншот, находясь в консоли, так-же поддерживает несколько полезных свойств типа определяемого пользователем таймера. Если не указанно другое, он сохраняет скриншот в директорию, в которой находился пользователь, когда запустил команду

```
scrot -t 20 -d 5

```

Сохраняет скриншот в .PNG файл, в имени которого присутствует дата скриншота. Так-же сохраняется миниатюра (20% от оригинального расширения) для удобного размещения в сети. Скриншот делается после пятисекундной задержки.

## KDE

Если вы пользуетесь KDE, удобней всего будет использовать ksnapshot, который может быть запущен через системное меню, либо нажатием <Prt Scr>.

## GNOME

Нажмите <Prt Scr> или запустите Apps->Accessories->Take Screenshot.

**Примечание:** Если при нажатии <Prt Scr> система говорит, что не может найти gnome-screenshot или в меню системы отсутствует "Take Screenshot", установите[gnome-utils](https://www.archlinux.org/packages/?name=gnome-utils).

## Виртуальная консоль

Установите [framebuffer](/index.php/Framebuffer "Framebuffer") и используйте [fbgrab](https://www.archlinux.org/packages/?name=fbgrab) для получения скриншота. Другой способ, использовать [fbshot](https://www.archlinux.org/packages/?name=fbshot), но оно искажает цвета.