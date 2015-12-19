# All Mouse Buttons Working (Русский)

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

[![Tango-preferences-desktop-locale.png](/images/d/dc/Tango-preferences-desktop-locale.png)](/index.php/File:Tango-preferences-desktop-locale.png)

**Эта страница нуждается в сопроводителе**

Статья не гарантирует актуальность информации. Помогите русскоязычному сообществу поддержкой подобных страниц. См. [Команда переводчиков ArchWiki](/index.php/%D0%9A%D0%BE%D0%BC%D0%B0%D0%BD%D0%B4%D0%B0_%D0%BF%D0%B5%D1%80%D0%B5%D0%B2%D0%BE%D0%B4%D1%87%D0%B8%D0%BA%D0%BE%D0%B2_ArchWiki "Команда переводчиков ArchWiki")

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

[![Tango-mail-mark-junk.png](/images/e/e7/Tango-mail-mark-junk.png)](/index.php/File:Tango-mail-mark-junk.png)

**Эта статья или раздел нуждается в улучшении грамматики, форматирования или стиля.**

**Причина:** пожалуйста, используйте первый аргумент шаблона для указания причины. (обсуждение: [Talk:All Mouse Buttons Working (Русский)#](https://wiki.archlinux.org/index.php/Talk:All_Mouse_Buttons_Working_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)))

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

Для необычных мышей (несколько колёс, более трёх кнопок, с эмуляцией колеса и т. д.), возможно, стоит поискать способ настройки вашей мыши в статье [Get_All_Mouse_Buttons_Working](/index.php/Get_All_Mouse_Buttons_Working "Get All Mouse Buttons Working") или в гугле.

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=All_Mouse_Buttons_Working_(Русский)&oldid=412721](https://wiki.archlinux.org/index.php?title=All_Mouse_Buttons_Working_(Русский)&oldid=412721)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Input devices (Русский)](/index.php/Category:Input_devices_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:Input devices (Русский)")
*   [X server (Русский)](/index.php/Category:X_server_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Category:X server (Русский)")
*   [Русский](/index.php/Category:%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9 "Category:Русский")