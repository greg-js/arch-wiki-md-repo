## Contents

*   [1 Предговор](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B3.D0.BE.D0.B2.D0.BE.D1.80)
*   [2 Подкарване на програмата под Arch Linux](#.D0.9F.D0.BE.D0.B4.D0.BA.D0.B0.D1.80.D0.B2.D0.B0.D0.BD.D0.B5_.D0.BD.D0.B0_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.B0.D1.82.D0.B0_.D0.BF.D0.BE.D0.B4_Arch_Linux)
    *   [2.1 Сваляне](#.D0.A1.D0.B2.D0.B0.D0.BB.D1.8F.D0.BD.D0.B5)
    *   [2.2 Необходими пакети](#.D0.9D.D0.B5.D0.BE.D0.B1.D1.85.D0.BE.D0.B4.D0.B8.D0.BC.D0.B8_.D0.BF.D0.B0.D0.BA.D0.B5.D1.82.D0.B8)
    *   [2.3 Компилация и инсталация](#.D0.9A.D0.BE.D0.BC.D0.BF.D0.B8.D0.BB.D0.B0.D1.86.D0.B8.D1.8F_.D0.B8_.D0.B8.D0.BD.D1.81.D1.82.D0.B0.D0.BB.D0.B0.D1.86.D0.B8.D1.8F)
    *   [2.4 Преди да рестартирате](#.D0.9F.D1.80.D0.B5.D0.B4.D0.B8_.D0.B4.D0.B0_.D1.80.D0.B5.D1.81.D1.82.D0.B0.D1.80.D1.82.D0.B8.D1.80.D0.B0.D1.82.D0.B5)
    *   [2.5 Финални настройки](#.D0.A4.D0.B8.D0.BD.D0.B0.D0.BB.D0.BD.D0.B8_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8)
    *   [2.6 Използване на програмата](#.D0.98.D0.B7.D0.BF.D0.BE.D0.BB.D0.B7.D0.B2.D0.B0.D0.BD.D0.B5_.D0.BD.D0.B0_.D0.BF.D1.80.D0.BE.D0.B3.D1.80.D0.B0.D0.BC.D0.B0.D1.82.D0.B0)

# Предговор

Засега няма официален драйвър за мишките на Razer под Linux. Michael Buesch е създал програма за мишките на Razer под under Linux. В момента следните мишки имат следните статуси: Razer DeathAdder и Razer Krait са Stable, Razer Lachesis е с либсващи свойства/тестов, Razer Copperhead и Razer Boomslang са без поддръжка.

# Подкарване на програмата под Arch Linux

Инструкции в README-то трябва да се модивицират за да тръгне програмата под Arch Linux. Аз използвах Razer Lachesis за тестове.

## Сваляне

Свалете програмата от [уеб-страницата](http://www.bu3sch.de/joomla/index.php/razer-nextgen-config-tool) на автора. Понастоящем, най-новата версия е 0.06.

## Необходими пакети

Нужно е да свалите тези пакети за да работи програмата:

```
# pacman -S cmake qt4 python python-qt4 libusb

```

## Компилация и инсталация

Разархивирайте пакета и след това го компилирайте и инсталирайте по следния начин:

```
$ cmake .
$ make
# make install
# ldconfig

```

След това, копирайте daemon-а:

```
# cp razerd.initscript /etc/rd.d/razerd

```

## Преди да рестартирате

Преди да рестартирате е нужно да редактирате файла **xorg.conf** и да премахнете сегашните настройки на мишката. Лично аз само ги коментирах и добавих следното както авторът препоръчва:

```
Section "InputDevice"
   Identifier	"Mouse"
   Driver	"mouse"
   Option	"Device" "/dev/input/mice"
EndSection

```

Важно е да пише "Mouse" а не "Mouse№" в **xorg.conf**.

След това е нужно да се копира библиотеката, понеже Arch не я намира по подразбиране:

```
# cp /usr/local/lib/librazer.so /usr/lib/librazer.so

```

## Финални настройки

Рестартирайте компютъра и вкарайте следната команда:

```
# udevadm control --reload-rules

```

За да пуснете daemon-а, вкарайте следната команда:

```
# /etc/rc.d/razerd start

```

Ако всичко е наред, не би трябвало да получите грешки.

## Използване на програмата

Програмата се намира в **/usr/local/bin/razercfg** и **/usr/local/bin/qrazercfg**. Вторият адрес е графичната версия.