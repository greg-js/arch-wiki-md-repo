**Note:** [GRUB Legacy](/index.php/GRUB_Legacy_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "GRUB Legacy (Русский)") заменён [GRUB](/index.php/GRUB "GRUB") и больше не используется в Arch Linux. См. новость [здесь](https://www.archlinux.org/news/grub-legacy-no-longer-supported/).

Пропатченная версия GRUB Legacy с поддержкой фонового изображения.

## Contents

*   [1 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [2 Конфигурация](#.D0.9A.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D1.8F)
*   [3 (Пере)Установка Grub](#.28.D0.9F.D0.B5.D1.80.D0.B5.29.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_Grub)
*   [4 Использование Фонового Изображения](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.A4.D0.BE.D0.BD.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D0.98.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D1.8F)
    *   [4.1 Требования](#.D0.A2.D1.80.D0.B5.D0.B1.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D1.8F)
    *   [4.2 Установка Новых Изображений](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.9D.D0.BE.D0.B2.D1.8B.D1.85_.D0.98.D0.B7.D0.BE.D0.B1.D1.80.D0.B0.D0.B6.D0.B5.D0.BD.D0.B8.D0.B9)
*   [5 Устранение проблем](#.D0.A3.D1.81.D1.82.D1.80.D0.B0.D0.BD.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC)
    *   [5.1 Черный экран, нет меню, мигающая строка](#.D0.A7.D0.B5.D1.80.D0.BD.D1.8B.D0.B9_.D1.8D.D0.BA.D1.80.D0.B0.D0.BD.2C_.D0.BD.D0.B5.D1.82_.D0.BC.D0.B5.D0.BD.D1.8E.2C_.D0.BC.D0.B8.D0.B3.D0.B0.D1.8E.D1.89.D0.B0.D1.8F_.D1.81.D1.82.D1.80.D0.BE.D0.BA.D0.B0)
*   [6 Внешние Ссылки](#.D0.92.D0.BD.D0.B5.D1.88.D0.BD.D0.B8.D0.B5_.D0.A1.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Установка

Пакет grub-gfx находится в репозитории community. Проверьте `/etc/[pacman.conf](/index.php/Pacman.conf "Pacman.conf")` и удостоверьтесь, что `[community]` раскоментирован.

```
[community]
# Add your preferred servers here, they will be used first
Include = /etc/pacman.d/mirrorlist

```

Сохраните текущую конфигурацию Grub. Хотя при установке пакета это происходит автоматически, предосторожность Вам не помешает.

```
cp /boot/grub/menu.lst /boot/grub/menu.lst.bak

```

Теперь загрузите и установите grub-gfx, он также удалит пакет grub, если тот был установлен.

```
pacman -S grub-gfx

```

После установки проверьте `/boot/grub/menu.lst`. Отредактируйте строки загрузки также, как было в сделанной Вами копии. Если Вы не создали резервную копию, тогда используйте `/boot/grub/menu.lst.pacsave`. Вы также можете просто скопировать свою резервную копию файла menu.lst поверх новой и приступить к следующему этапу конфигурации.

## Конфигурация

Единственное изменение в конфигурации - это добавление строки `splashimage`. По умолчанию /boot/grub/menu.lst выглядеть будет так:

```
# general configuration:
timeout   5
default   0
color light-blue/black light-cyan/blue
splashimage /boot/grub/arch.xpm.gz

```

В другом случае вы можете просто добавить последнюю строчку в существующий menu.lst. Otherwise you will simply be adding the last line to your existing menu.lst. Эта строка будет указывать на изображение, которое Вы хотите использовать в качестве фона во время загрузки экрана выбора операционной системы. Учитывайте, что **эта строка относит Grub к корневому разделу**. То есть, если у Вас свой раздел /boot, то тогда следует читать как:

```
splashimage /grub/arch.xpm.gz

```

## (Пере)Установка Grub

Теперь нам нужно будет установить Grub для перезаписи текущего Grub или другого загрузчика. Пожалуйста, ознакомьтесь с вики-страницами [Grub](/index.php/Grub "Grub") и [reinstalling GRUB](/index.php?title=Reinstalling_GRUB&action=edit&redlink=1 "Reinstalling GRUB (page does not exist)"), если Вы не делали этого раньше. "Стандартная" установка выполняется так:

```
grub-install /dev/sda

```

Но помните, что путь должен соответствовать Вашей системе.

## Использование Фонового Изображения

### Требования

Изображение должно быть файлом типа xpm.gz, иметь размер 640x480 и 14 цветов.

### Установка Новых Изображений

Просто поместите изображение в директорию grub, например, `/boot/grub/`. Теперь обновите `menu.lst`, указав путь к изображению. Нет необходимости переустанавливать Grub. Просто перезагрузитесь и Вы увидите новое изображение.

## Устранение проблем

### Черный экран, нет меню, мигающая строка

При загрузке компьютера вы должны иметь возможность выбора нужной вам операционной системы. Если этого не произошло, то вам необходимо загрузиться в систему Linux(например, с live-cd) и проверить ваш файл `menu.lst` на наличие ошибок. Путь к вашему splashimage должен быть корректным. Помните, строка splashimage должна быть указана относительно корневого раздела. Если у вас GRUB находится в отдельным разделе /boot, то строка splashimage будет иметь следующий вид: splashimage /grub/splashscreen.xpm.gz.

## Внешние Ссылки

[Коллекция изображений для Grub](http://www.schultz-net.dk/grub.html)

[Руководство по Изображениям для GRUB](http://ruslug.rutgers.edu/~mcgrof/grub-images/)

[Создание Изображений для Grub](http://gentoo-wiki.com/HOWTO_Splash_image_in_GRUB)