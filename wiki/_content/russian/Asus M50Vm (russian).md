## Contents

*   [1 Введение](#.D0.92.D0.B2.D0.B5.D0.B4.D0.B5.D0.BD.D0.B8.D0.B5)
*   [2 Описание лептопа](#.D0.9E.D0.BF.D0.B8.D1.81.D0.B0.D0.BD.D0.B8.D0.B5_.D0.BB.D0.B5.D0.BF.D1.82.D0.BE.D0.BF.D0.B0)
*   [3 Установка](#.D0.A3.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B0)
*   [4 Настройка WiFi](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_WiFi)
*   [5 Проблемы в процессе настройки и установки](#.D0.9F.D1.80.D0.BE.D0.B1.D0.BB.D0.B5.D0.BC.D1.8B_.D0.B2_.D0.BF.D1.80.D0.BE.D1.86.D0.B5.D1.81.D1.81.D0.B5_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B8_.D0.B8_.D1.83.D1.81.D1.82.D0.B0.D0.BD.D0.BE.D0.B2.D0.BA.D0.B8)
    *   [5.1 WiFi](#WiFi)
    *   [5.2 Xorg](#Xorg)
    *   [5.3 amarok 2.2](#amarok_2.2)
    *   [5.4 Hibernate (Спящий режим)](#Hibernate_.28.D0.A1.D0.BF.D1.8F.D1.89.D0.B8.D0.B9_.D1.80.D0.B5.D0.B6.D0.B8.D0.BC.29)
    *   [5.5 Сканер отпечатков](#.D0.A1.D0.BA.D0.B0.D0.BD.D0.B5.D1.80_.D0.BE.D1.82.D0.BF.D0.B5.D1.87.D0.B0.D1.82.D0.BA.D0.BE.D0.B2)
*   [6 Полезные ссылки](#.D0.9F.D0.BE.D0.BB.D0.B5.D0.B7.D0.BD.D1.8B.D0.B5_.D1.81.D1.81.D1.8B.D0.BB.D0.BA.D0.B8)

## Введение

В этом документе описывается установка и настройка ArchLinux x86_64 на ноутбуке Asus M50Vm.

## Описание лептопа

```
Производитель:	ASUSTeK Computer Inc.
Маркировка:	ASUS M50Vm
Тип оборудования:	портативный игровой ноутбук
Диагональ дисплея:	15.4" (39.1 см) Color-Shine
Тип дисплея:	TFT, широкоформатный 16:10, с технологией ASUS Splendid Video Intelligent
Разрешение экрана:	WXGA (1280 x 800)
Корпус:	специальное покрытие Scatchproof - защита от царапин
Чипсет:	Mobile Intel® PM45 Express Chipset +ICH9M
Процессор:	Intel Core 2 Duo P8600 (TDP - 25W)
Количество ядер:	2
Тактовая частота:	2.40 ГГц
Ядро:	Penryn (45 нм)
Частота системной шины:	1066МГц FSB
Кэш память:	3Мб кэш L2
Тип памяти:	2 слота DDR2-800/667
Объём памяти:	4 Гб DDR2-800
Жесткий диск:	320Гб SATA, 5400rpm/8Мб
Оптический привод:	Blu-Ray DVD Combo
Видеокарта:	NVIDIA® GeForce® 9600M GS 1Gb VRAM
Шина видео:	PCI Express 2.0
Звук:	HD Audio
Сеть, коммуникации:	- модем 56Кб/с 
 - сеть проводная Gigabit Ethernet LAN 
 - сеть беспроводная Intel Wireless WiFi Link 5100 
 - модуль Bluetooth 2.0+EDR
Порты, разъёмы:	4 x USB, i.Link (IEEE 1394), VGA-out, HDMI, TV-out (S-Video), Mic-In, Head-Out (совмещён с SPDIF), Express Card slot
Дополнительно:	- веб-камера 1.3 Мп (поворотная) 
 - расширенная клавиатура с цифровым блоком 
 - cканер отпечатков пальцев
Устройство чтения карт памяти:	8-in-1 Card Reader (MMC/ SD/ Mini-SD/ Memory Stick/ MS Pro/ MS-Duo/MS-Pro-Duo)

```

## Установка

Без особых проблем, все делал по документации, никаких проблем не возникло.

## Настройка WiFi

Дома WiFi роутер с WPA2-PSK (TKIP). Для настройки подключения использовал wpa_supplicant (+dhcpcd).

После третьей перезагрузки, устав руками запускать wpa_supplicant и dhcpcd, добавил их в rc.local:

```
sudo wpa_supplicant -Dwext -iwlan0 -c/etc/wpa_supplicant.conf -B
sudo dhcpcd wlan0

```

## Проблемы в процессе настройки и установки

Здесь приведены различные проблемы (в порядке вспоминания, а не встречи с ними), с которыми я столкнулся в процессе установки и настройки.

### WiFi

WiFi интерфейс отказался подниматься (**ifconfig wlan0 up**) с невнятным сообщением (уже не воспроизведу... :( ). **dmesg | tail** показал:

```
kernel: iwlagn 0000:03:00.0: firmware: requesting iwlwifi-5000-2.ucode
kernel: iwlagn 0000:03:00.0: firmware: requesting iwlwifi-5000-1.ucode
firmware.sh[2183]: Cannot find  firmware file 'iwlwifi-5000-2.ucode'
firmware.sh[2189]: Cannot find  firmware file 'iwlwifi-5000-1.ucode'
kernel: iwlagn 0000:03:00.0: firmware: requesting iwlwifi-5000-2.ucode
kernel: iwlagn 0000:03:00.0: firmware: requesting iwlwifi-5000-1.ucode
firmware.sh[13594]: Cannot find  firmware file 'iwlwifi-5000-2.ucode'
firmware.sh[13607]: Cannot find  firmware file 'iwlwifi-5000-1.ucode'

```

Выяснилось, что почему-то не был установлен пакет firmware:

```
pacman -S iwlwifi-5000-ucode

```

### Xorg

1.  Первый запуск X закончился перезагрузкой с конпки Power - не работала клавиатура, получил просто серый экран.
    *   Решение: Очень удивился, не обнаружив hal в зависимостях - **pacman -S hal**. (Без hal клавиатура и тачпад не работают - подробнее [Xorg](/index.php/Xorg "Xorg")). (Не забываем добавить hal в DAEMONS в /etc/rc.conf).
2.  При первом удачном запуске обнаружил очень странные шрифты (расползшиеся вширь).
    *   Проблема оказалась в DPI: в KDE System Settings пришлось выставить Force fonts DPI: 120 dpi (System Settings/Appearance/Fonts).

PS. Мой xorg.conf:

```
Section "ServerLayout"
   Identifier     "Layout0"
   Screen      0  "Screen0"
EndSection

```

```
Section "Files"
   FontPath    "/usr/share/fonts/"
EndSection

```

```
Section "Device"
   Identifier     "Device0"
   Driver         "nvidia"
   VendorName     "NVIDIA Corporation"
   Option      "RenderAccel"   "True"
   Option      "TripleBuffer"  "True"
EndSection

```

```
Section "Screen"
   Identifier     "Screen0"
   Device         "Device0"
EndSection

```

```
Section "Module"
   Load "glx" 
   Load "ddc"  # Эти два модуля нужны для автоопределения
   Load "i2c"   # настроек монитора
EndSection

```

### amarok 2.2

Очень удивился, обнаружив Amarok не играющим ничего. Оказалось:

1.  Не была установлена Alsa. Инструкция здесь: [ALSA](/index.php/ALSA "ALSA")
2.  Не было плагинов к gstreamer (gstreamer - бек-энд по умолчанию в Phonon). Вылечилось:

```
pacman -S gstreamer0.10-good-plugins gstreamer0.10-base-plugins 

```

### Hibernate (Спящий режим)

Сначала просто не работал, почитал [KDE](/index.php/KDE "KDE") - узнал, что надо добавить себя в группу power. Добавил - все вроде стало хорошо, уснул... Но при включении - сеанс не восстановился, лаптоп грузился как будто я его выключил кнопкой - с проверкой дисков и руганью на ошибки.

Лечится добавлением строки resume=/dev/swap как опции загрузки ядра в grub (где swap - девайс свопа).

### Сканер отпечатков

Все что нужно:

```
sudo pacman -S fprint

```

Добавляем себя в группу scanner (для того чтобы иметь доступ к девайсу):

```
sudo gpasswd -a username scanner

```

И регистрируем свои пальчики:

```
sudo pam_fprint_enroll

```

Дальше идем сюда: [Thinkfinger](/index.php/Thinkfinger "Thinkfinger"), ищем секции по включению аутентификации по пальцам и имя модуля везде с pam_thinkfinger заменяем на pam_fprint. Все!

## Полезные ссылки

Ссылки, использованные в процессе установки и настройки:

*   [ALSA](/index.php/ALSA "ALSA")
*   [Регулировка частоты процессора](/index.php/Cpufrequtils "Cpufrequtils")
*   [Xorg](/index.php/Xorg "Xorg")