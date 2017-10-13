#### Вопрос: Как я могу настроить прокрутку у колеса мыши в Xorg?

**Ответ:** Это можно сделать в конфигурационном файле: `/etc/X11/xorg.conf`. Для большинства мышей вам просто надо добавить:

```
Option "ZAxisMapping" "4 5"

```

в секцию Mouse. Например:

```
  Section "InputDevice"
    Identifier "Mouse"
    Driver "mouse"
    Option "Protocol" "ExplorerPS/2"
    Option "Device" "/dev/input/mice"
    Option "ZAxisMapping" "4 5"
  EndSection

```

Если колесо прокрутки не работает с этими настройками, попробуйте запустить `xev` и подвигать колёсико. В выводе программы будет показано, от каких кнопок пришли события. Если они иные, чем 4 и 5, то измените соответствующим образом секцию мыши в конфигурационном файле.

Для необычных мышей (несколько колёс, более трёх кнопок, с эмуляцией колеса и т. д.), возможно, стоит поискать способ настройки вашей мыши в статье [Get All Mouse Buttons Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working") или в гугле.

Например:

```
  Section "InputDevice"
    Identifier  "Mouse"
    Driver "mouse"
    Option "Protocol" "ExplorerPS/2"
    Option "Device" "/dev/input/mouse0"
    Option "Buttons" "6"
    Option "ZAxisMapping" "5 6"
    Option "Emulate3Buttons" "off"
    Option "EmulateWheel" "on"
    Option "EmulateWheelButton" "4"
  EndSection

```

для четырёхкнопочной мыши без колеса прокрутки.

Также прочитайте: [Установка и настройка Xorg](/index.php/%D0%A3%D1%81%D1%82%D0%B0%D0%BD%D0%BE%D0%B2%D0%BA%D0%B0_%D0%B8_%D0%BD%D0%B0%D1%81%D1%82%D1%80%D0%BE%D0%B9%D0%BA%D0%B0_Xorg "Установка и настройка Xorg")