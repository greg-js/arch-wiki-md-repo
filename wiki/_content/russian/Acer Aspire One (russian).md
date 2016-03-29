Эта страница содержит информацию об установке Arch Linux на Acer Aspire One.

Обсуждение установки Arch Linux на нетбуке Acer Aspire One [на форуме](http://archlinux.org.ru/arch_forum/viewtopic.php?f=9&t=1360).

## Contents

*   [1 Прежде чем начать установку](#.D0.9F.D1.80.D0.B5.D0.B6.D0.B4.D0.B5_.D1.87.D0.B5.D0.BC_.D0.BD.D0.B0.D1.87.D0.B0.D1.82.D1.8C_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D1.83)
    *   [1.1 SSD](#SSD)
*   [2 Минимальная установка для работы в текстовом режиме](#.D0.9C.D0.B8.D0.BD.D0.B8.D0.BC.D0.B0.D0.BB.D1.8C.D0.BD.D0.B0.D1.8F_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_.D0.B2_.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.BE.D0.B2.D0.BE.D0.BC_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5)
    *   [2.1 Подготовка загрузочной флешки](#.D0.9F.D0.BE.D0.B4.D0.B3.D0.BE.D1.82.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B7.D0.BE.D1.87.D0.BD.D0.BE.D0.B9_.D1.84.D0.BB.D0.B5.D1.88.D0.BA.D0.B8)
    *   [2.2 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
    *   [2.3 Первый старт. Подключение к Internet](#.D0.9F.D0.B5.D1.80.D0.B2.D1.8B.D0.B9_.D1.81.D1.82.D0.B0.D1.80.D1.82._.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA_Internet)
    *   [2.4 Подключение SDHC карты в левый кардридер](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_SDHC_.D0.BA.D0.B0.D1.80.D1.82.D1.8B_.D0.B2_.D0.BB.D0.B5.D0.B2.D1.8B.D0.B9_.D0.BA.D0.B0.D1.80.D0.B4.D1.80.D0.B8.D0.B4.D0.B5.D1.80)
    *   [2.5 Настройка pacman и yaourt](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_pacman_.D0.B8_yaourt)
    *   [2.6 Создание пользователя](#.D0.A1.D0.BE.D0.B7.D0.B4.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
    *   [2.7 Wi-Fi](#Wi-Fi)
        *   [2.7.1 Поднятие беспроводного интерфейса](#.D0.9F.D0.BE.D0.B4.D0.BD.D1.8F.D1.82.D0.B8.D0.B5_.D0.B1.D0.B5.D1.81.D0.BF.D1.80.D0.BE.D0.B2.D0.BE.D0.B4.D0.BD.D0.BE.D0.B3.D0.BE_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D1.84.D0.B5.D0.B9.D1.81.D0.B0)
        *   [2.7.2 Настройка WPA](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_WPA)
        *   [2.7.3 Скрипт для управления подключением к сети](#.D0.A1.D0.BA.D1.80.D0.B8.D0.BF.D1.82_.D0.B4.D0.BB.D1.8F_.D1.83.D0.BF.D1.80.D0.B0.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D1.8F_.D0.BF.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5.D0.BC_.D0.BA_.D1.81.D0.B5.D1.82.D0.B8)
    *   [2.8 Настройка аудио](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B0.D1.83.D0.B4.D0.B8.D0.BE)
    *   [2.9 Настройка графической системы](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
        *   [2.9.1 Установка фреймбуфера](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.84.D1.80.D0.B5.D0.B9.D0.BC.D0.B1.D1.83.D1.84.D0.B5.D1.80.D0.B0)
    *   [2.10 Ещё немного про оптимизацию](#.D0.95.D1.89.D1.91_.D0.BD.D0.B5.D0.BC.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE_.D0.BE.D0.BF.D1.82.D0.B8.D0.BC.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8E)
        *   [2.10.1 Выключение кнопкой](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.BE.D0.B9)
    *   [2.11 Программы для работы в текстовом режиме](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B_.D0.B4.D0.BB.D1.8F_.D1.80.D0.B0.D0.B1.D0.BE.D1.82.D1.8B_.D0.B2_.D1.82.D0.B5.D0.BA.D1.81.D1.82.D0.BE.D0.B2.D0.BE.D0.BC_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.D0.B5)
        *   [2.11.1 Установка универсального проигрывателя](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D1.83.D0.BD.D0.B8.D0.B2.D0.B5.D1.80.D1.81.D0.B0.D0.BB.D1.8C.D0.BD.D0.BE.D0.B3.D0.BE_.D0.BF.D1.80.D0.BE.D0.B8.D0.B3.D1.80.D1.8B.D0.B2.D0.B0.D1.82.D0.B5.D0.BB.D1.8F)
*   [3 Установка графической оболочки](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B9_.D0.BE.D0.B1.D0.BE.D0.BB.D0.BE.D1.87.D0.BA.D0.B8)
    *   [3.1 GNOME](#GNOME)
        *   [3.1.1 Установка GNOME](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_GNOME)
        *   [3.1.2 Настройка Wi-Fi](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Wi-Fi)
            *   [3.1.2.1 Настройка VPN](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_VPN)
            *   [3.1.2.2 Использование коммуникатора с WM для выхода в Internet](#.D0.98.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D0.BE.D0.B2.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BE.D0.BC.D0.BC.D1.83.D0.BD.D0.B8.D0.BA.D0.B0.D1.82.D0.BE.D1.80.D0.B0_.D1.81_WM_.D0.B4.D0.BB.D1.8F_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4.D0.B0_.D0.B2_Internet)
            *   [3.1.2.3 Системный монитор](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D0.B9_.D0.BC.D0.BE.D0.BD.D0.B8.D1.82.D0.BE.D1.80)
*   [4](#)
    *   [4.1 Улучшение производительности графической системы](#.D0.A3.D0.BB.D1.83.D1.87.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BF.D1.80.D0.BE.D0.B8.D0.B7.D0.B2.D0.BE.D0.B4.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D0.BE.D1.81.D1.82.D0.B8_.D0.B3.D1.80.D0.B0.D1.84.D0.B8.D1.87.D0.B5.D1.81.D0.BA.D0.BE.D0.B9_.D1.81.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D1.8B)
*   [5](#_2)
*   [6 Дополнительные функциональные клавиши](#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.84.D1.83.D0.BD.D0.BA.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8)
*   [7 Выключение кнопкой](#.D0.92.D1.8B.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.BE.D0.B9_2)
*   [8 Различные приятные мелочи](#.D0.A0.D0.B0.D0.B7.D0.BB.D0.B8.D1.87.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.B8.D1.8F.D1.82.D0.BD.D1.8B.D0.B5_.D0.BC.D0.B5.D0.BB.D0.BE.D1.87.D0.B8)
    *   [8.1 Подключение телефона и выход в интернет](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.82.D0.B5.D0.BB.D0.B5.D1.84.D0.BE.D0.BD.D0.B0_.D0.B8_.D0.B2.D1.8B.D1.85.D0.BE.D0.B4_.D0.B2_.D0.B8.D0.BD.D1.82.D0.B5.D1.80.D0.BD.D0.B5.D1.82)
        *   [8.1.1 Через USB](#.D0.A7.D0.B5.D1.80.D0.B5.D0.B7_USB)
        *   [8.1.2 Через Bluetooth](#.D0.A7.D0.B5.D1.80.D0.B5.D0.B7_Bluetooth)
*   [9 Установка нового ядра](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.BE.D0.B2.D0.BE.D0.B3.D0.BE_.D1.8F.D0.B4.D1.80.D0.B0)
*   [10 Примеры конфигураций](#.D0.9F.D1.80.D0.B8.D0.BC.D0.B5.D1.80.D1.8B_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.B9)
    *   [10.1 /etc/fstab](#.2Fetc.2Ffstab)
    *   [10.2 /etc/rc.local](#.2Fetc.2Frc.local)
    *   [10.3 fdisk -l](#fdisk_-l)
    *   [10.4 /etc/X11/xorg.conf](#.2Fetc.2FX11.2Fxorg.conf)
    *   [10.5 Original Linpus Xorg.conf](#Original_Linpus_Xorg.conf)
    *   [10.6 Lines from rc.conf (kernel >=2.6.27)](#Lines_from_rc.conf_.28kernel_.3E.3D2.6.27.29)
    *   [10.7 /etc/acerfand.conf](#.2Fetc.2Facerfand.conf)
    *   [10.8 /etc/modprobe.d/sound](#.2Fetc.2Fmodprobe.d.2Fsound)
*   [11 Программое обеспечение](#.D0.9F.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D0.BE.D0.B5_.D0.BE.D0.B1.D0.B5.D1.81.D0.BF.D0.B5.D1.87.D0.B5.D0.BD.D0.B8.D0.B5)
    *   [11.1 Офисные программы](#.D0.9E.D1.84.D0.B8.D1.81.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)
    *   [11.2 Системные программы](#.D0.A1.D0.B8.D1.81.D1.82.D0.B5.D0.BC.D0.BD.D1.8B.D0.B5_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B)
    *   [11.3 Игры и программы для общения](#.D0.98.D0.B3.D1.80.D1.8B_.D0.B8_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.BC.D1.8B_.D0.B4.D0.BB.D1.8F_.D0.BE.D0.B1.D1.89.D0.B5.D0.BD.D0.B8.D1.8F)
*   [12 Черновик](#.D0.A7.D0.B5.D1.80.D0.BD.D0.BE.D0.B2.D0.B8.D0.BA)
    *   [12.1 Настройка внешнего порта VGA](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D0.B2.D0.BD.D0.B5.D1.88.D0.BD.D0.B5.D0.B3.D0.BE_.D0.BF.D0.BE.D1.80.D1.82.D0.B0_VGA)
    *   [12.2 Обновление ядра](#.D0.9E.D0.B1.D0.BD.D0.BE.D0.B2.D0.BB.D0.B5.D0.BD.D0.B8.D0.B5_.D1.8F.D0.B4.D1.80.D0.B0)
*   [13 Советы](#.D0.A1.D0.BE.D0.B2.D0.B5.D1.82.D1.8B)
    *   [13.1 Настройка Internet Connection Sharing на сетевую плату](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Internet_Connection_Sharing_.D0.BD.D0.B0_.D1.81.D0.B5.D1.82.D0.B5.D0.B2.D1.83.D1.8E_.D0.BF.D0.BB.D0.B0.D1.82.D1.83)
    *   [13.2 Настройка Internet Connection Sharing на WiFi](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Internet_Connection_Sharing_.D0.BD.D0.B0_WiFi)
    *   [13.3 Не загружается после установки](#.D0.9D.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
*   [14 Автоматизация](#.D0.90.D0.B2.D1.82.D0.BE.D0.BC.D0.B0.D1.82.D0.B8.D0.B7.D0.B0.D1.86.D0.B8.D1.8F)
*   [15 Установка настроенного ArchLinux из образа SSD](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BD.D0.BD.D0.BE.D0.B3.D0.BE_ArchLinux_.D0.B8.D0.B7_.D0.BE.D0.B1.D1.80.D0.B0.D0.B7.D0.B0_SSD)
*   [16 От автора](#.D0.9E.D1.82_.D0.B0.D0.B2.D1.82.D0.BE.D1.80.D0.B0)
*   [17 Полезные ссылки](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Прежде чем начать установку

Желательно ознакомиться со статьёй [Руководство для новичков](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%B4%D0%BB%D1%8F_%D0%BD%D0%BE%D0%B2%D0%B8%D1%87%D0%BA%D0%BE%D0%B2 "Руководство для новичков") и [Руководство по установке](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B5 "Руководство по установке").

### SSD

Вобщем-то это руководство по установке на версию нетбука с твердотельным накопителем (SSD).

Твердотельные накопители - это флешпамять, которая имеет высокую скорость чтения и незначительную скорость записи. В отличии от традиционного жесткого диска (HDD) накопитель SSD имеет ограниченное количество циклов записи (порядка миллиона раз) в одну ячейку. Тем не менее, применительно к AAO, если выполнить ряд мер, можно существенно продлить жизнь накопителя SSD. Для этого следует:

*   Отказаться от использования на SSD журналируемой файловой системы;
*   Отказаться от использования раздела подкачки (swap) на SSD (если только вы не хотите использовать спящий режим);
*   Монтировать на SSD "noatime" разделы;
*   Не сохранять логи и сообщения на SSD;
*   Если требуется часто писать что-то в файлы, эти файлы размещать на флешке из левого кардридера.

## Минимальная установка для работы в текстовом режиме

### Подготовка загрузочной флешки

Скачиваем дистрибутив ArchLinux через BitTorrent Download [Core ISOs: i686](https://www.archlinux.org/download/).

Надо сделать загрузочную флешку. Подойдёт любая флешка, размером от 512 мегабайт.

Открываем Мой компьютер и кликаем правую кнопку мышки над флешкой. Выбираем Форматировать.

Скачиваем программу [unetbootin](https://ru.wikipedia.org/wiki/UNetbootin). Текущая версия, на момент написания руководства, [http://downloads.sourceforge.net/unetbootin/unetbootin-windows-312.exe](http://downloads.sourceforge.net/unetbootin/unetbootin-windows-312.exe)

Запускаем unetbootin. Ставим галочку **Образ**. Справа кликаем по кнопке и находим образ дистрибутива ArchLinux.

Внизу окошка выбираем Тип - USB-накопитель и Диск - вашу флешку.

Жмём ОК и ждём минуты три...пять, пока unetbootin сделает загрузочную флешку.

### Установка

Вставляем флешку в нетбук и включаем питание. Успеваем нажать F12 Попадаем в Boot menu. Здесь надо выбрать с какого устройства будет идти загрузка операционной системы. Меню может выглядеть, например, вот так

```
1\. IDE 0: SSDPAMM0008G1
2\. USB HDD: Generic USB
3\. Network Boot: LEGACY PCI DEVICE

```

Загрузочная флешка с ArchLinux стоит второй строкой. Выбрать и нажать Enter.

В загрузчике unetbootin загружаемся по первой строке default.

После загрузки операционки набираем `**root**` Далее набираем `**/arch/setup**`

1\. Выбираем источник. Это будет CD-ROM or OTHER SOURCE

2\. Время. Здесь всё интуитивно понятно как надо сделать. Жмём 8(Европа) - 39(Россия) - 2(Москва) и соглашаемся, соглашаемся.

3\. Prepare Hard Drive. То есть препарируем жесткий наш диск.

Пропускаем Auto-Prepare.

Выбираем Partition Hard Drive.

Здесь вот бывает как получится. Внутренний диск определяется то как /dev/sda, то как /dev/sdb/

Это не страшно. Главное, запомнить тот, который 7GiB (если у вас 8 гиговый) или 15GiB(если 16 гиговый SSD).

Второй диск - это загрузочная флешка.

Например

```
Available Disks

/dev/sda:  488 MiB (0 GiB)  - это флешка
**/dev/sdb**:  7695 MiB (7 GiB) - это **SSD**

```

Далее надо установщику указать диск **SSD** нетбука. Выбираете. В нашем случае это /dev/sdb. Запустится утилитка, в которой можно поудалять все существующие разделы и сделать два раздела. Нетбук поставляется с 8 или 16 гигабайтным SSD. 8, а тем более, 16 гигабайт вы забьёте программами весьма нескоро. Если забьёте. Посему можно сразу же, на этапе установки, часть памяти отдать будущему пользователю. Например на 8 гигабайтном SSD 6 гиг отдать системе, а 2 - вывести в отдельный раздел. Для 16 гигового: 6 на систему и 10 пользователю. То есть в нашем случае создаём два раздела: sdb1 и sdb2.

Диск размечен, теперь можно выйти. Выбираем DONE.

3\. Set Filesystem Mountpoints

При выборе Set Filesystem Mountpoints установщик напоминает нам где есть какие диски.

```
Select the partition to use as swap

```

Своп на SSD нам не нужен. Потому выбираем NONE.

```
Select the partition to mount as /

```

Выбираем раздел для **/**. Это /dev/sdb1 в нашем случае (у вас может быть /dev/sda1).

```
Select a file system for /dev/sdb1

```

Выбираем тип файловой системы Ext2.

На вопрос

```
Would you like to create a filesystem on /dev/sdb1?

```

Выбираем `Yes`.

```
Select any additional partitions to mount under your new root...

```

Выбираем DONE

```
Would you like to create and mount the filesystem like this? 
Syntax
------

DEVICE:TYPE:MOUNTPOINT:FORMAT

/dev/sdb1:ext2:/:yes

```

Выбираем YES

```
Partition were successfully mounted.

```

Ну и отлично. Жмём OK

И возвращаемся к главному меню.

4\. Select Packages

Выбираем и **base**, и **base devel**. Также обязательно надо выбрать строчку с **pptpclient**. Без этого мы не сможем подключиться далее к Internet. Ну и ещё можновыбрать wireless_tools. Чтобы не скачивать его при настройке Wi-Fi.

5\. Install Packages

Устанавливаем пакеты. Установка длится чуть больше 5 минут. Жмём Continue.

6\. Configure System

Выберите редактор **nano**

Управление nano:

```
Сохранить изменение в файле **Ctrl+o**
Выйти из редактора **Ctrl+x**

```

Попадаем в окошко **Configuration**

Здесь надо выбрать каждую строчку, отредактировать конфиг, сохранить изменения в файле и выйти. Ниже жирным шрифтом выделено то, что надо изменить или добавить.

**/etc/rc.conf** System Config

```
#------------
#LOCALIZATION
#------------

LOCALE="**ru_RU.UTF-8**"
HARDWARECLOCK="**localtime**"
USEDIRECTISA="no"
TIMEZONE="**Europe/Moscow**"   #потом смените часовой пояс, если потребуется
KEYMAP="**ru**"
CONSOLEFONT="**ruscii_8x16**"
CONSOLEMAP=""
USECOLOR="yes"

#------------
#HARDWARE
#------------

MODULES=(**!memstick !snd-pcsp acpi_cpufreq ath5k pciehp r8169 uvcvideo**)

#------------
#NETWORKING
#------------
**eth0="dhcp"**
INTERFACE=(eth0) 

```

**/etc/fstab** Filesystem Moutpoints

Исправляем по-аналогии:

```
# 
# /etc/fstab: static file system information
#
# <file system>        <dir>         <type>    <options>          <dump> <pass>
none                   /dev/pts      devpts    defaults            0      0
none                   /dev/shm      tmpfs     defaults            0      0

#/dev/cdrom            /media/cd     auto      ro,user,noauto,inhide 0     0 
#/dev/dvd              /media/dvd    auto      ro,user,noauto,inhide 0     0
#/dev/fd0              /media/fl     auto      user,noauto           0     0

UUID=61fa45ba-14cb-42c8-92ea-770ed5faa221 / ext2 defaults**,noatime,errors=remount-ro** 0  1

#монтируем директории /var/log, /tmp, /var/tmp в оперативную память
**none                   /var/log      tmpfs     defaults,size=10M   0      0**
**none                   /tmp          tmpfs     defaults,size=100M  0      0**
**none                   /var/tmp      tmpfs     defaults,size=20M   0      0**

```

UUID=61fa45ba-14cb-42c8-92ea-770ed5faa221 - это уникальный идентификатор и у вас будет он выглядеть иначе. Между "defaults,noatime,errors=remount-ro" не должно быть пробелов! Писать символ-за_символом.

Пропускаем пока

**/etc/mkinitcpio.conf** Initramfs Config

**/etc/modprobe.d/modprobe.conf** Kernel Modules

Редактируем **/etc/resolv.conf** DNS Servers

```
#
# /etc/resolv.conf
#

#search<yourdomain.tld>

#У воронежского билайна DNS 194.186.60.107 и 194.186.60.108

**nameserver 194.186.60.107**
**nameserver 194.186.60.108**

```

Пропускаем

**/etc/hosts** Network Hosts

**/etc/hosts.deny** Denied Network Services

**/etc/hosts.allow** Allowed Network Services

**/etc/hosts.allow** Allowed Network Services

Правим **/etc/locale** Glibc Locales

```
#закомментариваем строчки 
#en_US.UTF-8 UTF-8 
#en_US ISO-8859-1

#убираем символ комментария со строчки
ru_RU.UTF-8   UTF-8

```

Пропускаем

**/etc/pacman.d/mirrorlist** Pacman Mirror List

Устанавливаем пароль суперпользователя

Root-Password Set the root password

И возвращаемся в главное меню. Return Return to Main Menu

Начинается Rebuilding initcpio image. Ждём минуты полторы.

Устанавливаем загрузчик (Install Bootloader).

Выбираем GRUB.

В редакторе открывается /mnt/boot/grub/menu.lst По умолчанию таймаут ожидания выбора загружаемого ядра 5 секунд. Уменьшим до 1 секунды.

```
# general configuration
timeout   **1**
default   0

```

В нашем случае SSD определился как sdb, поэтому в этом файле надо подправить

```
# (0) Arch Linux
title Arch Linux
root  (hd**0**,0)

```

и

```
# (1) Arch Linux
title Arch Linux Fallsback
root  (hd**0**,0)

```

Выбираем устройство, где будет установлен GRUB. В нашем случае это будет /dev/sdb

```
Do you have your system installed on software raid?

```

Жмём No.

```
GRUB was successfully installed.

```

OK

Выбираем Exit Install.

И набираем в консоли **poweroff**.

После выключения вытаскиваем флешку из USB.

Система установлена. =) Это самый минимум, с которым уже можно работать. Теперь будем окультуривать нетбук, подгоняя Арча под свои нужды. =)

### Первый старт. Подключение к Internet

Если нетбук не загружается - смотреть [здесь](#.D0.9D.D0.B5_.D0.B7.D0.B0.D0.B3.D1.80.D1.83.D0.B6.D0.B0.D0.B5.D1.82.D1.81.D1.8F_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8). Если всё равно не загружается - всё-таки начинаем читать [Руководство для новичков](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%B4%D0%BB%D1%8F_%D0%BD%D0%BE%D0%B2%D0%B8%D1%87%D0%BA%D0%BE%D0%B2 "Руководство для новичков") и [Руководство по установке](/index.php/%D0%A0%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE_%D1%83%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B5 "Руководство по установке").

Если загрузился - вводим логин `root` и пароль, который задали при установке.

В дальнейших манипуляциях с Арчем нам потребуется соединение с Internet.

Настройка VPN:

[http://ru.posix.wikia.com/wiki/PPTP](http://ru.posix.wikia.com/wiki/PPTP)

### Подключение SDHC карты в левый кардридер

Настало время подключить флешку в левом кардридере.

Создём файл `**/etc/modprobe.d/options**` и вписываем в него строку

```
options sdhci debug_quirks=1

```

В файле `**/etc/fstab**` добавляем строку:

```
/dev/mmcblk0p1  /home   ext2     defaults,noatime     0       1

```

Перегружаем нетбук.

В командной строке пишем: `**reboot**`

Теперь папка /home привязана к флешке из левого кардридера. Забудьте про неё и более оттуда не вытаскивайте. Ну как минимум до тех пор, пока не станете с Арчем на "ты". ))

Если же вытащите, то сможете заходить в систему лишь как root.

Если карточка новая - можно сразу её отформатировать. В консоли делаем:

`**mkfs.ext2 /dev/mmcblk0p1**`

и назначить метку

`**e2label /dev/mmcblk0p1 "SD_HOME"**`

### Настройка pacman и yaourt

Определим каталог кеша для pacman. Это будет на флешке расширения (левый кардридер) - то есть в каталоге **/home**. Создаём каталог **/home/cache/pacman/pkg**

`**mkdir /home/cache**`

`**mkdir /home/cache/pacman**`

`**mkdir /home/cache/pacman/pkg**`

Правим конфиг пакмана: `nano /etc/pacman.conf`

```
CacheDir     = /home/cache/pacman/pkg/
LogFile      = /var/log/pacman.log

```

А в самом низу пропишем сервер французский с репо (было подсказано <pride> в конфе arch@conference.jabber.ru)

```
 [archlinuxfr]
Server = [http://repo.archlinux.fr/i686](http://repo.archlinux.fr/i686)

```

Это нам весьма облегчит жизнь при настройке ArchLinux позже.

Если интернет у вас уже работает в нетбуке, то установим из французского репозитория **yaourt**.

`**pacman -S yaourt**`

Правим конфиг yaourt: `nano /etc/yaourtrc`

```
TmpDirectory     = /home/cache/yaourt

```

И создаём папку:

`**mkdir /home/cache/yaourt**`

### Создание пользователя

Постоянно пребывать в системе как root не очень хорошо для безопасности. Карту расширения мы установили, посему настало время создать обычного пользователя.

Например заводим пользователя **masha** с паролем **mAsha**

Это делаем двумя командами

```
`**useradd -m -G users,network,audio,video,wheel masha**`

`**passwd masha**`

Введите новый пароль UNIX: *mAsha*
Повторите ввод нового пароля UNIX: *mAsha*
passwd: пароль успешно обновлён

```

### Wi-Fi

#### Поднятие беспроводного интерфейса

[Настройка беспроводного соединения в Archlinux](/index.php/Wireless_Setup_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Wireless Setup (Русский)")

*Примечание:* для Atheros AR2425, возможно, вместо ath5k лучше использовать madwifi с новым HAL:

```
yaourt -S madwifi-newhal-svn

```

Итак, сперва установим wireless-tools

`**pacman -S wireless_tools**`

Перенастраиваем [ISC](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_Internet_Connection_Sharing_.D0.BD.D0.B0_WiFi) на десктопном компьютере.

Проверяем

`**iwconfig**`

Должно быть нечто наподобие:

```
wlan0    IEEE 802.11bg  ESSID:""  
         Mode:Managed  Frequency:2.412 GHz  Access Point: Not-Associated   
         Tx-Power=27 dBm   
         Retry min limit:7   RTS thr:off   Fragment thr=2352 B   
         Encryption key:off
         Power Management:off
         Link Quality:0  Signal level:0  Noise level:0
         Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
         Tx excessive retries:0  Invalid misc:0   Missed beacon:0

```

Далее в консоли набираем

`**ifconfig eth0 down**`

`**ifconfig wlan0 up**`

И можем посмотреть близлежащие Точки Доступа:

`**iwlist wlan0 scan**`

Нетбук нашел точку доступа "HOMEWIFI":

```
wlan0    Scan completed :
         Cell 01 - Address: 00:B1:8C:20:93:2D
                   ESSID:"HOMEWIFI"
                   Mode:Master
                   Channel:1
                   Frequency:2.412 GHz (Channel 1)
                   Quality=92/100  Signal level:-42 dBm  Noise level=-101 dBm
                   Encryption key:on
                   IE: Unknown: 000567313333
                   IE: Unknown: 010651248B967843086C
                   IE: Unknown: 069101
                   IE: Unknown: 2A6144
                   IE: Unknown: 78940C563260
                   IE: WPA Version 1
                       Group Cipher : TKIP
                       Pairwise Ciphers (1) : TKIP
                       Authentication Suites (1) : PSK
                   IE: Unknown: DD45780C4301065350
                   Bit Rates:1 Mb/s; 2 Mb/s; 5.5 Mb/s; 11 Mb/s; 9 Mb/s
                             18 Mb/s; 36 Mb/s; 54 Mb/s; 6 Mb/s; 12 Mb/s
                             24 Mb/s; 48 Mb/s
                   Extra:tsf=00000000a68fc61e
                   Extra: Last beacon: 983ms ago

```

Используя выведенные данные, скажите своему устройству, какую точку использовать. В нашем случае:

`**iwconfig wlan0 essid HOMEWIFI**`

Затем, настройте интерфейс как обычно. Например, если на вашем десктопе запущен DHCP сервер, так:

`**dhcpcd wlan0**`

Ну или статически

`**ifconfig wlan0 192.168.0.3**`

Пробуем пингануть: ping -c5 archlinux.org

```
PING archlinux.org (66.211.213.17) 56(84) bytes of data.
64 bytes from gerolde.archlinux.org (66.211.213.17): icmp_seq=1 ttl=49 time=199 ms
64 bytes from gerolde.archlinux.org (66.211.213.17): icmp_seq=2 ttl=49 time=189 ms
64 bytes from gerolde.archlinux.org (66.211.213.17): icmp_seq=3 ttl=49 time=198 ms
64 bytes from gerolde.archlinux.org (66.211.213.17): icmp_seq=4 ttl=49 time=186 ms
64 bytes from 66.211.213.17: icmp_seq=5 ttl=49 time=190 ms   

--- archlinux.org ping statistics ---
5 packets transmitted, 5 received, 0% packet loss, time 4004ms
rtt min/avg/max/mdev = 186.967/193.076/199.659/5.214 ms

```

Примерно такое у вас?

Если нет, проверьте ещё раз по тексту то, что вводили - может где ошиблись. Убедитесь, что точка доступа не имеет шифрации.

Если да - идём дальше.

Пропишем в конце файла **/etc/rc.local**

```
ifconfig eth0 down
ifconfig wlan0 up

```

Ибо проводное соединение нам уже понадобится нескоро.

Точка доступа не имеет шифрации и соединение открытое, что чревато неприятностями. Настройка WEP рассматриваться не будет, в силу непригодности для домашнего применения. Ниже рассмотрим настройку Wi-Fi с WPA шифрацией.

#### Настройка WPA

[Настройка WPA в ArchLinux](/index.php/WPA_Supplicant_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "WPA Supplicant (Русский)")

Хотя и с WPA вашу безпроводную сеть можно расколоть.

За дополнительной информацией отсылаю к гуглу. Например [вот](http://www.google.ru/search?hl=ru&newwindow=1&q=%D0%B2%D0%B7%D0%BB%D0%BE%D0%BC+%D1%81%D0%B5%D1%82%D0%B8+wi+fi&btnG=%D0%9F%D0%BE%D0%B8%D1%81%D0%BA&lr=&aq=f&oq=).

#### Скрипт для управления подключением к сети

### Настройка аудио

Настройку аудио смотреть [здесь](/index.php/ALSA_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ALSA (Русский)"). Канал PCM в AAO отсутствует, поэтому сообщение об ошибке при вводе команды

`**amixer set PCM 85% unmute**`

пусть вас не волнует.

Рекомендуется использовать ядро >= 2.6.28\. Для нормальной работы внутреннего микрофона добавьте строчку в файл **/etc/modprobe.d/modprobe.conf**:

```
options snd-hda-intel model=acer

```

### Настройка графической системы

Чипсет AAO работает с драйвером xf86-video-intel

Необходимо установить следущие пакеты:

*   xf86-video-intel
*   xf86-input-synaptics

В консоли набираем:

`**pacman -S xf86-video-intel**`

`**pacman -S xf86-input-synaptics**`

#### Установка фреймбуфера

Здесь нам надо установить фреймбуфер разрешением 1024х600 при 32-х битном цвете. Почитайте [Uvesafb](/index.php/Uvesafb "Uvesafb") для начала. Но можно просто сделать то, что описано ниже и всё заработает.

*   Устанавливаем v86d;
*   Устанавливаем 915resolution-static из AUR.

Устанавливаем v86d

`**pacman -S v86d**`

Устанавливаем 915resolution-static

`**yaourt -S 915resolution-static**` Внимательно читайте то, что спрашивает установщик **yaourt**.

По окончании компиляции и установки правим **/etc/modprobe.d/uvesafb.conf** вот так:

```
options uvesafb mode_option=1024x600-32 scroll=ywrap

```

Правим **/lib/initcpio/hooks/915resolution** вот так:

```
run_hook ()
{
  msg -n ":: Patching the VBIOS..."
  /usr/sbin/915resolution -c 945GM 5c **1024 600**
  msg "done."
}

```

Добавляем **915resolution** и **v86d** в список хуков в **/etc/mkinitcpio.conf**:

```
HOOKS="base udev 915resolution v86d ..."

```

И запускаем

`**mkinitcpio -p kernel26**`

### Ещё немного про оптимизацию

Чтобы аккумулятор разряжался медленнее, следует кое-что поднастроить.

Для динамического изменения частоты процессора в зависимости от нагрузки, следует прописать в файле **/etc/rc.local** пару строк:

```
echo ondemand > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
echo ondemand > /sys/devices/system/cpu/cpu1/cpufreq/scaling_governor

```

Увеличиваем интервал времени между записями dirty (изменённой) памяти на SSD. В командной строке набираем:

```
echo "1500" > /proc/sys/vm/dirty_writeback_centisecs

```

#### Выключение кнопкой

Выключается компьютер подачей команды `poweroff`. Перезагрузка компьютера: `reboot`.

Назначим команду "Выключить" кнопке питания.

Установим пакет с демоном acpid

```
pacman -S acpid

```

Можем сразу же его запустить без перезагрузки. В командной строке пишем:

```
/etc/rc.d/acpid start

```

Чтобы демон acpid стартовал при загрузке сделаем следущее:

*   Если у вас прописан запуск демона hal в rc.conf - более ничего делать не надо. Потому что hal запустит acpid автоматически.
*   Если вы не используете hal - вам надо добавить acpid в строке DAEMONS в файле rc.conf

А теперь в командной строке пишем:

```
echo "event=button/power.*" > /etc/acpi/events/power
echo "action=/sbin/poweroff" >> /etc/acpi/events/power

```

Нажмите и отпустите кнопку питания. Если удерживать кнопку питания слишком долго (секунды две) - нетбук будет просто выключен, без корректной процедуры завершения.

### Программы для работы в текстовом режиме

В текстовом режиме можно редактировать текст - vi ( [Vim](/index.php/Vim_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Vim (Русский)") обычно уже установлен в базовом варианте), отправлять и принимать почту - , слушать музыку и смотреть видео - mplayer (его установку см. [здесь](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)")), серфить - [lynx](http://ru.wikipedia.org/wiki/Lynx) (установка: `pacman -S lynx`), работать в файл менеджером - mc (установка [Midnight Commander](http://ru.wikipedia.org/wiki/Midnight_Commander): `pacman -S mc`).

#### Установка универсального проигрывателя

Загрузим пакет музыкального проигрывателя Mplayer и установим его по [инструкции](/index.php/MPlayer_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "MPlayer (Русский)").

А именно - набрать `pacman -S mplayer codecs`. Будет установлен и проигрыватель, и кодеки к нему.

Для воспроизведения музыки или видео достаточно войти в папку, где у вас лежат мультимедийные файлы, и подать команду `mplayer *`. Будут воспроизводиться все по очереди. Или, если какой-то конкретный файл воспроизвести `mplayer filename`. Esc - выйти из проигрывателя. Space - пауза/воспроизведение. Другие горячие клавиши управления проигрывателем смотреть `man mplayer`. Конфиги плеера в `/etc/mplayer/`

Для воспроизведения потокового аудио следует ввести следущую команду:

```
mplayer [mms://mms.online.ru/c16_13_128](mms://mms.online.ru/c16_13_128)

```

Будет воспроизводиться этот поток [http://101.ru/?an=chan_popplay&uid=44192&bit=128](http://101.ru/?an=chan_popplay&uid=44192&bit=128)

```
mplayer [mms://mms.online.ru/c17_2_128](mms://mms.online.ru/c17_2_128)

```

А это поспокойнее ;) [http://101.ru/?an=chan_popplay&uid=46761&bit=128](http://101.ru/?an=chan_popplay&uid=46761&bit=128)

Битрейты потоков в примерах 128к. Адрес потока можно подсмотреть внутри asx-файла.

Этот проигрыватель будет у вас работать и в графической оболочке GNOME.

## Установка графической оболочки

Устанавливаем [Xorg](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)")

### GNOME

Про Гнома: [http://library.gnome.org/misc/release-notes/2.24/](http://library.gnome.org/misc/release-notes/2.24/)

#### Установка GNOME

Читаем прежде [здесь](/index.php/GNOME_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0 "GNOME (Русский)")

#### Настройка Wi-Fi

Как и положено в оконно-мышечной концепции, подключаемся к различным сетевым ресурсам без консоли. То есть методом тыка.

[Устанавливаем](/index.php/Network_Manager "Network Manager") Network Manager. После установки, там где часы, появится иконка - кликаем по ней и выбираем сеть.

##### Настройка VPN

Устанавливаем [плагин](https://aur.archlinux.org/packages.php?ID=23279) для Network Manager из AUR.

```
yaourt -S networkmanager-pptp-0.7

```

##### Использование коммуникатора с WM для выхода в Internet

На примере использования коммуникатора [HTC3300](http://www.mobile-review.com/phonemodels/htc/htc-p3300.shtml).

##### Системный монитор

Чтобы на десктопе отображалась всякая полезная информация - устанавливаем conky

```
#pacman -S conky

```

Описание здесь [http://starl1te.wordpress.com/2007/01/01/conky-howto/](http://starl1te.wordpress.com/2007/01/01/conky-howto/)

#### Улучшение производительности графической системы

Чтобы улучшить производительность 2D графики следует добавить следующие строки в раздел Driver Section файла **xorg.conf**

```
Option "AccelMethod" "exa"
Option "MigrationHeuristic" "greedy"

```

Замечание: Установка опции "MigrationHeuristic" в "greedy" может приводить к искажениям иконок трея в KDE 4.1, как описано здесь [http://bugs.kde.org/show_bug.cgi?id=170283](http://bugs.kde.org/show_bug.cgi?id=170283) и здесь [http://bugs.freedesktop.org/show_bug.cgi?id=19059](http://bugs.freedesktop.org/show_bug.cgi?id=19059)

Для увеличения производительности 3D, добавить в **/etc/profile**

```
export INTEL_BATCH=1

```

Смотреть также [Intel](/index.php/Intel "Intel").

## Дополнительные функциональные клавиши

## Выключение кнопкой

## Различные приятные мелочи

### Подключение телефона и выход в интернет

#### Через USB

...

#### Через Bluetooth

...

## Установка нового ядра

## Примеры конфигураций

Все конфиги упакованы в [архив](http://depositfiles.com/files/25ss4b3fi). Распакуйте архив как есть. Все файлы разместятся в требуемых каталогах и вам потребуется или подправить имеющиеся строки, или переименовать файл.

### /etc/fstab

```
 # 
 # /etc/fstab: static file system information
 #
 # <file system>        <dir>         <type>    <options>          <dump> <pass>
 none                   /dev/pts      devpts    defaults            0      0
 none                   /dev/shm      tmpfs     defaults            0      0
 UUID=510b26a4-d407-4707-8ed9-d3b1d0632024 /boot ext2 noatime 0 1
 UUID=61fa45ba-14cb-42c8-92ea-770ed5faa221 / ext3 defaults,noatime,errors=remount-ro,commit=15	01
 /dev/mmcblk0p1  /home   xfs     defaults,noatime     0       1
 #LABEL=HD-Home
 #UUID=FFFF-FFFF /media/right    vfat    users,rw,uid=1000,gid=100,fmask=0133,dmask=0002 0       0
 UUID=7ee58355-644f-46fb-a557-202d2b968161 swap swap defaults 0 0
 none    /var/log        tmpfs   defaults,size=10M       0       0
 none    /tmp    tmpfs   defaults,size=100M      0       0
 none    /var/tmp        tmpfs   defaults,size=20M       0       0

```

### /etc/rc.local

```
 #!/bin/bash
 #
 # /etc/rc.local: Local multi-user startup script.
 #
 # Change CPU governors and writeback-time (as suggested by powertop)
 echo ondemand > /sys/devices/system/cpu/cpu0/cpufreq/scaling_governor
 echo ondemand > /sys/devices/system/cpu/cpu1/cpufreq/scaling_governor
 echo 1500 > /proc/sys/vm/dirty_writeback_centisecs
 # Make the right SD-slot visible, as suggested by the Debian wiki
 setpci -d 197b:2381 AE=47
 # Set up the wifi-key
 /usr/bin/setkeycodes e055 159
 /usr/bin/setkeycodes e056 158
 # Set up the function keys
 /usr/bin/setkeycodes e025 130
 /usr/bin/setkeycodes e026 131
 /usr/bin/setkeycodes e027 132
 /usr/bin/setkeycodes e029 122
 /usr/bin/setkeycodes e071 134
 /usr/bin/setkeycodes e072 135

```

### fdisk -l

```
 Disk /dev/sda: 8069 MB, 8069677056 bytes
 255 heads, 63 sectors/track, 981 cylinders
 Units = cylinders of 16065 * 512 = 8225280 bytes
 Disk identifier: 0xb7d8b185
    Device Boot      Start         End      Blocks   Id  System
 /dev/sda1               1          32      257008+  83  Linux
 /dev/sda2              33         908     7036470   83  Linux
 /dev/sda3             909         981      586372+  82  Linux swap / Solaris

```

### /etc/X11/xorg.conf

This is for Xorg >= 7.4 and synaptics >= 0.99.

Note that:

*   autodetection of input devices is disabled here by the <tt>AutoAddDevices</tt> option.
*   scrolling on the touchpad is disabled here with by the <tt>HorizEdgeScroll</tt> and <tt>VertEdgeScroll</tt> options.

```
Section "ServerLayout"
       Identifier     "Default Layout"
       Screen      0  "Screen0" 0 0
       InputDevice    "Synaptics Mouse" "AlwaysCore"
       InputDevice    "Keyboard0" "CoreKeyboard"
       InputDevice    "USB Mouse" "CorePointer"
EndSection

Section "ServerFlags"
       Option "AllowMouseOpenFail"  "true"
       Option "AutoAddDevices" "False"
EndSection

Section "Module"
       Load "synaptics"
EndSection

Section "Files"
       ModulePath   "/usr/lib/xorg/modules"
       FontPath     "/usr/share/fonts/misc:unscaled"
       FontPath     "/usr/share/fonts/misc"
       FontPath     "/usr/share/fonts/75dpi:unscaled"
       FontPath     "/usr/share/fonts/75dpi"
       FontPath     "/usr/share/fonts/100dpi:unscaled"
       FontPath     "/usr/share/fonts/100dpi"
       FontPath     "/usr/share/fonts/PEX"
# Additional fonts: Locale, Gimp, TTF...
       FontPath     "/usr/share/fonts/cyrillic"
#       FontPath     "/usr/share/lib/X11/fonts/latin2/75dpi"
#       FontPath     "/usr/share/lib/X11/fonts/latin2/100dpi"
# True type and type1 fonts are also handled via xftlib, see /etc/X11/XftConfig!
       FontPath     "/usr/share/fonts/Type1"
       FontPath     "/usr/share/fonts/ttf/western"
       FontPath     "/usr/share/fonts/ttf/decoratives"
       FontPath     "/usr/share/fonts/truetype"
       FontPath     "/usr/share/fonts/truetype/openoffice"
       FontPath     "/usr/share/fonts/truetype/ttf-bitstream-vera"
       FontPath     "/usr/share/fonts/latex-ttf-fonts"
       FontPath     "/usr/share/fonts/defoma/CID"
       FontPath     "/usr/share/fonts/defoma/TrueType"
       FontPath     "/usr/share/fonts/artwiz-fonts"
       FontPath     "/usr/share/fonts/local"
EndSection

Section "InputDevice"
       Identifier  "Keyboard0"
       Driver      "keyboard"
       Option      "CoreKeyboard"
       Option "XkbRules" "xorg"
       Option "XkbModel" "pc105"
       Option "XkbLayout" "no"
# Option "XkbVariant" "nodeadkeys"
EndSection

Section "InputDevice"
       Identifier "Synaptics Mouse"
       Driver     "synaptics"
       Option     "Device" "/dev/psaux"
       Option     "Protocol" "auto-dev"
       Option     "LeftEdge"  "1700"
       Option  "RightEdge"     "5300"
       Option  "TopEdge"       "1700"
       Option  "BottomEdge"    "4200"
       Option  "FingerLow"     "25"
       Option  "FingerHigh"    "30"
       Option  "MaxTapTime"    "180"
       Option  "MaxTapMove"    "220"
       Option  "VertScrollDelta" "100"
       Option  "MinSpeed"      "0.09"
       Option  "MaxSpeed"      "0.18"
       Option  "AccelFactor"   "0.0015"
       Option  "SHMConfig"     "on"
# new in synaptics 0.99
       Option  "ClickFinger1"  "1"
       Option  "ClickFinger2"  "0"
       Option  "ClickFinger3"  "0"
       Option  "HorizTwoFingerScroll"  "0"
       Option  "VertTwoFingerScroll"   "0"
       Option  "HorizScrollDelta"      "100"
       Option  "PressureMotionMinZ"    "10"
       Option  "FingerPress"   "256"
       Option  "PalmDetect"    "0"
       Option  "PalmMinWidth"  "10"
       Option  "PalmMinZ"      "200"
       Option  "MaxTapMove"    "220"
       Option  "MaxTapTime"    "180"
       Option  "MaxDoubleTapTime"      "200"
       Option  "TapButton1"    "1"
       Option  "TapButton2"    "0"
       Option  "TapButton3"    "0"
       Option  "RTCornerButton"        "2"
       Option  "RBCornerButton"        "3"
       Option  "LTCornerButton"        "0"
       Option  "LBCornerButton"        "0"
# Circular scrolling is uber-cool, but it's not for everyone. Check out "gsynaptics" as well.
       Option  "CircularScrolling"     "0"
# Scrolling with the right and bottom side can be fun... or incredibly annoying. Use "1" to enable.
       Option  "HorizEdgeScroll"       "0"
       Option  "VertEdgeScroll"        "0"
EndSection

Section "InputDevice"
       Identifier      "USB Mouse"
       Driver          "mouse"
       Option          "Device"                "/dev/input/mice"
       Option          "SendCoreEvents"        "true"
       Option          "Protocol"              "IMPS/2"
       Option          "ZAxisMapping"          "4 5"
       Option          "Buttons"               "5"
EndSection

Section "Monitor"
       Identifier  "Monitor0"
       Modeline  "1024x600" 48.96 1024 1064 1168 1312 600 601 604 622 -HSync +VSync
       DisplaySize 346 203 # 75 DPI @ 1024x600
EndSection

Section "Device"
       Identifier  "Videocard0"
       Driver      "intel"
       Option      "Clone" "true"
       Option      "MonitorLayout"     "LVDS,VGA"
       BusID       "PCI:0:2:0"
       Option      "MigrationHeuristic" "greedy"
       Option      "AccelMethod" "EXA"
EndSection

Section "Screen"
       Identifier "Screen0"
       Device     "Videocard0"
       Monitor     "Monitor0"
       DefaultDepth     24
       SubSection "Display"
               Viewport   0 0
               Depth     24
               Modes    "1024x600" "800x600" "640x480"
               Virtual 1920 1800
       EndSubSection
EndSection

Section "DRI"
       Mode 0666
EndSection

```

### Original Linpus Xorg.conf

```
# Xorg configuration created by system-config-display

Section "ServerFlags"
  Option "DontZap" "yes"
  Option "DontVTSwitch" "yes"
EndSection

Section "ServerLayout"
  Identifier "Default Layout"
  Screen 0 "Screen0" 0 0
  InputDevice "Mouse0" "CorePointer"
  InputDevice "Synaptics Mouse" "AlwaysCore"
  InputDevice "Keyboard0" "CoreKeyboard"
EndSection

Section "InputDevice"
  Identifier "Keyboard0"
  Driver "kbd"
  Option "XkbModel" "pc105"
  Option "XkbLayout" "gb,us"
  Option "XkbVariant" "euro"
  Option "XkbOptions" "grp:alt_shift_toggle"
EndSection

Section "InputDevice"
  Identifier "Synaptics Mouse"
  Driver "synaptics"
  Option "Device" "/dev/psaux"
  Option "Protocol" "auto-dev"
  Option "LeftEdge" "1700"
  Option "RightEdge" "5300"
  Option "TopEdge" "1700"
  Option "BottomEdge" "4200"
  Option "FingerLow" "25"
  Option "FingerHigh" "30"
  Option "MaxTapTime" "180"
  Option "MaxTapMove" "220"
  Option "VertScrollDelta" "100"
  Option "MinSpeed" "0.09"
  Option "MaxSpeed" "0.18"
  Option "AccelFactor" "0.0015"
  Option "SHMConfig" "on"
EndSection

Section "InputDevice"
  Identifier "Mouse0"
  Driver "mouse"
  Option "Protocol" "IMPS/2"
  Option "Device" "/dev/input/mice"
  Option "ZAxisMapping" "4 5"
  Option "Emulate3Buttons" "no"
EndSection

Section "Monitor"
  Identifier "Monitor0"
  Modeline "1024x600" 50.40 1024 1048 1184 1344 600 600 619 625
  # Option "Above" "Monitor1"
EndSection

Section "Device"
  Identifier "Videocard0"
  Driver "intel"
  # Option "monitor-LVDS" "Monitor0"
  # Option "monitor-VGA" "Monitor1"
  Option "Clone" "true"
  Option "MonitorLayout" "LVDS,VGA"
  vBusID "PCI:0:2:0"
  # Screen 0
EndSection

Section "Screen"
  Identifier "Screen0"
  Device "Videocard0"
  Monitor "Monitor0"
  DefaultDepth 24
  SubSection "Display"
    Viewport 0 0
    Depth 24
    Modes "1024x600" "800x600" "640x480"
    Virtual 1024 600
  EndSubSection
EndSection

```

### Lines from rc.conf (kernel >=2.6.27)

```
 MODULES=(r8169 acpi_cpufreq ath5k !wlan !ath_hal !ath_pci snd-mixer-oss snd-pcm-oss snd-hwdep snd-page-alloc snd-pcm snd-timer snd snd-hda-intel soundcore !pcspkr !uvcvideo !videodev !v4l1_compat !video !memstick pciehp acer-wmi)
 NETWORKS=(wpa.example)
 DAEMONS=(@acpid @laptop-mode cpufreq syslog-ng !netfs !crond dbus @hal @network @net-profiles gdm)

```

### /etc/acerfand.conf

```
INTERVAL=5
FANOFF=52
FANAUTO=62

```

### /etc/modprobe.d/sound

```
options snd-hda-intel model=acer-aspire

```

## Программое обеспечение

### Офисные программы

...

### Системные программы

...

### Игры и программы для общения

A list of games working on your One and configuration tips for those can be found under [Acer Aspire One Games List](/index.php/Acer_Aspire_One_Games_List "Acer Aspire One Games List").

## Черновик

### Настройка внешнего порта VGA

Внешний порт VGA работает без дополнительных модификаций конфига, если внешний монитор подключен до загрузки ArchLinux. Если подключение случилось позже, то порт VGA активизируется настройками в xrandr. Смотреть секцию [Дополнительные функциональные клавиши](/index.php/Acer_Aspire_One_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.94.D0.BE.D0.BF.D0.BE.D0.BB.D0.BD.D0.B8.D1.82.D0.B5.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D1.84.D1.83.D0.BD.D0.BA.D1.86.D0.B8.D0.BE.D0.BD.D0.B0.D0.BB.D1.8C.D0.BD.D1.8B.D0.B5_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8 "Acer Aspire One (Русский)").

### Обновление ядра

Читаем как устанавливать из репозитория пользовательских пакетов (AUR) [здесь](/index.php/AUR_%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE_%D0%BF%D0%BE%D0%BB%D1%8C%D0%B7%D0%BE%D0%B2%D0%B0%D1%82%D0%B5%D0%BB%D1%8F "AUR руководство пользователя").

Инструкция:

Идём сюда [https://aur.archlinux.org/packages.php?ID=22794](https://aur.archlinux.org/packages.php?ID=22794) и качаем вот это:

[Архив](https://aur.archlinux.org/packages/kernel26-one-dev/kernel26-one-dev.tar.gz) :: Файлы :: PKGBUILD

Копируем архив в любое место в нетбуке. Например вот сюда /home/krnl/

`**mkdir /home/krnl**`

Разворачиваем архив: `**tar -xvvzf kernel26-one-dev.tar.gz**`

Заходим в создавшуюся директорию `**cd /home/krnl/kernel26-one-dev**`

Пишем команду `makepkg`

Если есть подключение к интернету - makepkg скачает все необходимые модули сам.

Если интернета нет - нужно положить в директорию /home/krnl/kernel26-one-dev все файлы, перечисленные в

**Исходники**

[ath5k-patch1.patch](https://aur.archlinux.org/packages/kernel26-one-dev/kernel26-one-dev/ath5k-patch1.patch)

[ath5k-patch2.patch](https://aur.archlinux.org/packages/kernel26-one-dev/kernel26-one-dev/ath5k-patch2.patch)

[config](https://aur.archlinux.org/packages/kernel26-one-dev/kernel26-one-dev/config)

[ftp://ftp.kernel.org/pub/linux/kernel/v2.6/testing/linux-2.6.29-rc5.tar.bz2](ftp://ftp.kernel.org/pub/linux/kernel/v2.6/testing/linux-2.6.29-rc5.tar.bz2)

[http://kernel.org/pub/linux/kernel/v2.6/snapshots/patch-2.6.29-rc5-git4.bz2](http://kernel.org/pub/linux/kernel/v2.6/snapshots/patch-2.6.29-rc5-git4.bz2)

Сборка ядра занимает минут 30.

Результатом сборки имеем пакет kernel26-one-dev-2.6.29rc5git4-1-i686.pkg.tar.gz

Его нужно установить в системе командой

`**pacman -U kernel26-one-dev-2.6.29rc5git4-1-i686.pkg.tar.gz**`

Здесь выдаётся ошибка: не удалось корректно выполнить скрипт

Тем не менее ядро установилось.

Идём в директорию /boot/grub и правим файл меню menu.lst

`**nano /boot/grub/menu.lst**`

Приводим файл вот к такому виду:

```
# general configuration:
timeout   1
**default   2   #по-умолчанию будет загружаться новое ядро**
color light-blue/black light-cyan/blue

# boot sections follow
# each is implicitly numbered from 0 in the order of appearance below
#
# TIP: If you want a 1024x768 framebuffer, add "vga=773" to your kernel line.
#
#-*  

# (0) Arch Linux
title  Arch Linux
root   (hd0,0)
kernel /boot/vmlinuz26 root=/dev/disk/by-uuid/f055dd4b-5df0-4118-bb9d-2e6ff30d753a ro
initrd /boot/kernel26.img

# (1) Arch Linux
title  Arch Linux Fallback
root   (hd0,0)
kernel /boot/vmlinuz26 root=/dev/disk/by-uuid/f055dd4b-5df0-4118-bb9d-2e6ff30d753a ro
initrd /boot/kernel26-fallback.img 

**# (2) Arch Linux Acer Aspire One**
**title  Arch Linux Acer Aspire One**
**root   (hd0,0)**
**kernel /boot/vmlinuz-one-dev root=/dev/sda ro**

```

**C ЭТОЙ ВЕРСИЕЙ СБОРКИ ЯДРА НЕОБХОДИМО ПОДПРАВИТЬ НЕКОТОРЫЕ КОНФИГИ**

/etc/rc.conf System Config

Удаляем модули

```
#------------
#HARDWARE
#------------
# приводим вот к такому виду
**MODULES=(!memstick)**

```

/etc/fstab Filesystem Moutpoints

Если есть в левом кардридере флешка (что очень желательно) - подключаем её.

```
# 
# /etc/fstab: static file system information
#
# <file system>        <dir>         <type>    <options>          <dump> <pass>
none                   /dev/pts      devpts    defaults            0      0
none                   /dev/shm      tmpfs     defaults            0      0

#/dev/cdrom            /media/cd     auto      ro,user,noauto,inhide 0     0 
#/dev/dvd              /media/dvd    auto      ro,user,noauto,inhide 0     0
#/dev/fd0              /media/fl     auto      user,noauto           0     0

UUID=61fa45ba-14cb-42c8-92ea-770ed5faa221 / ext2 defaults,noatime,errors=remount-ro 0  1

#монтируем директории /var/log, /tmp, /var/tmp в оперативную память
none                   /var/log      tmpfs     defaults,size=10M   0      0
none                   /tmp          tmpfs     defaults,size=100M  0      0
none                   /var/tmp      tmpfs     defaults,size=20M   0      0

**/dev/mmcblk0           /home         ext2      defaults,noatime,errors=remount-ro 0  1**

```

Зарубежные арчелюбители предлагают вместо [Ext2](http://ru.wikipedia.org/wiki/Ext2) пользовать [XFS](http://ru.wikipedia.org/wiki/XFS).

Перезагрузить нетбук, набрав в командной строке: `reboot`

После перезагрузки, если карточка новая - можно сразу же её отформатировать. В консоли пишем:

`**mkfs.ext2 /dev/mmcblk0p1**`

и назначаем метку

`**e2label /dev/mmcblk0p1 "SD_HOME"**`

## Советы

### Настройка Internet Connection Sharing на сетевую плату

### Настройка Internet Connection Sharing на WiFi

### Не загружается после установки

Если при загрузке системы загрузчик выдал сообщение типа:

```
  Booting 'Arch Linux'
root   (hd1,0)
Error 21: Selected disk does not exist
Press any key to continue...

```

Жмите пробел и далее выбираете строчку и нажимаете клавишу 'e'. Попадаете в редактор меню загрузки. Выбираете строчку root (hd1,0) и опять жмете 'e'. Теперь попробуйте заменить единичку на ноль, чтобы стало вот так: root (hd0,0). Теперь жмите Энтер. Теперь клавишу 'b'. Система может загрузиться. Если не загрузилась - придётся гуглить. Если система загрузилась, входите как root с паролем, затем пишите:

`**nano /boot/grub/menu.lst**`

находите строчки root (hd1,0) и заменяете 1 на 0\. Сохраняете Ctrl+o. При следующей перезагрузке всё будет хорошо. =)

## Автоматизация

Для ленивых

## Установка настроенного ArchLinux из образа SSD

Что есть в образе:

## От автора

Данная статья является переводом статьи [Acer Aspire One](/index.php/Acer_Aspire_One "Acer Aspire One") с небольшими изменениями и дополнениями.

## Полезные ссылки

*   [Обсуждение установки ArchLinux на AAO](http://archlinux.org.ru/arch_forum/viewtopic.php?f=9&t=1360)
*   [Русскоязычное сообщество Arch Linux](http://archlinux.org.ru/arch_forum/index.php)
*   [Всё для acer aspire one](http://aspire1.ru/forum/)
*   [Awesome 3 configuration (Russian)](http://awesome.naquadah.org/wiki/index.php?title=Awesome_3_configuration_(Russian))