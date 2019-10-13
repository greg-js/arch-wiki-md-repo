Related articles

*   [Advanced Linux Sound Architecture (Русский)](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)")
*   [Desktop notifications](/index.php/Desktop_notifications "Desktop notifications")

**Состояние перевода:** На этой странице представлен перевод статьи [Volnoti](/index.php/Volnoti "Volnoti"). Дата последней синхронизации: 21 ноября 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Volnoti&diff=0&oldid=495356).

[Volnoti](https://github.com/davidbrazdil/volnoti) - это, в соответствии с описанием на странице Github,

	"*Легковесный демон сообщений об уровне громкости для GNU/Linux и иных POSIX операционных систем. Он использует GTK+ и D-Bus и должен работать с любым оконным менеджером. Основной целью было создание демона сообщений уровня громкости для легковесных оконных менеджеров таких как LXDE или XMonad. Известно, что он работает с большим списком оконных менеджеров, включая GNOME, KDE, Xfce, LXDE, XMonad, i3 и многими другими*"

Volnoti может быть полезен для проверки изменения уровня громкости, если вы используете легковесный оконный менеджер, такой как [Openbox](/index.php/Openbox_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Openbox (Русский)"), который обычно не поставляется вместе с демоном сообщений, особенно в комбинации с медиаклавишами ноутбука/клавиатуры.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Установка](#Установка)
*   [2 Настройка и использование](#Настройка_и_использование)
    *   [2.1 Запуск Volnoti](#Запуск_Volnoti)
    *   [2.2 Настройка для Xbindkeys](#Настройка_для_Xbindkeys)
    *   [2.3 Настройки для i3](#Настройки_для_i3)

## Установка

Установите пакет [volnoti](https://aur.archlinux.org/packages/volnoti/) из [AUR](/index.php/Arch_User_Repository_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Arch User Repository (Русский)").

## Настройка и использование

### Запуск Volnoti

Для запуска демона выполните команду

```
$ volnoti

```

Volnoti будет запущен в фоновом режиме. Для того чтобы Volnoti запускался автоматически при запуске вашего оконного менеджера, добавьте команду в файл автозапуска (например, `~/.config/openbox/autostart`, если вы используете Openbox). Проверить запущена ли программа можно командой в терминале

```
$ volnoti-show 20

```

В результате должен отобразиться полупрозрачный квадрат по центру экрана, показывающий уровень громкости 25%. Далее вам следует настроить Volnoti для отображения сообщения, каждый раз как изменится уровень громкости.

### Настройка для Xbindkeys

Настройки, приведенные ниже, используют Volnoti, [Alsa](/index.php/Advanced_Linux_Sound_Architecture_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Advanced Linux Sound Architecture (Русский)") и [Xbindkeys](/index.php/Xbindkeys_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xbindkeys (Русский)") для отображения изменения уровня громкости при нажатии горячих клавиш. Этот пример рассчитан на то, что Xbindkeys уже установлен и настроен как описано на его странице.

Откройте `~./xbindkeysrc` в текстовом редакторе и добавьте следующий код перед строкой `# End of xbindkeys configuration`:

```
# Увеличить громкость
"amixer set Master 5%+ && volnoti-show $(amixer get Master | grep -Po "[0-9]+(?=%)" | tail -1)"
   XF86AudioRaiseVolume

# Уменьшить громкость
"amixer set Master 5%- && volnoti-show $(amixer get Master | grep -Po "[0-9]+(?=%)" | tail -1)"
   XF86AudioLowerVolume

# Выключить/включить звук
"amixer set Master toggle; if amixer get Master | grep -Fq "[off]"; then volnoti-show -m; else volnoti-show $(amixer get Master | grep -Po "[0-9]+(?=%)" | tail -1); fi"
   XF86AudioMute

```

Первые две команды увеличат или уменьшат уровень громкости, когда будут нажаты соответствующие специальные клавиши, считают новое значение громкости и отправят его как аргумент в `volnoti-show`. Третья команда выключит/включит звук и отобразит сообщение Volnoti об этом (был ли звук включен или выключен).

Теперь вы можете перезапустить Xbindkeys с помощью команды `kill -1 $(pidof xbindkeys)` (или перезагрузить ПК, после того как убедитесь, что и Volnoti и Xbindkeys прописаны в файле автозапуска) и проверить ваши настройки.

### Настройки для i3

Добавьте следующие 3 строки в ваш файл конфигурации i3 (~/.i3/config или ~/.config/i3/config по умолчанию)

```
 bindsym XF86AudioRaiseVolume exec --no-startup-id "amixer set Master 2%+ && volnoti-show $(amixer get Master | grep -Po '[0-9]+(?=%)' | head -1)"
 bindsym XF86AudioLowerVolume exec --no-startup-id "amixer set Master 2%- && volnoti-show $(amixer get Master | grep -Po '[0-9]+(?=%)' | head -1)"
 bindsym XF86AudioMute exec --no-startup-id "amixer set Master toggle && if amixer get Master | grep -Fq '[off]'; then volnoti-show -m; else volnoti-show $(amixer get Master | grep -Po '[0-9]+(?=%)' | head -1); fi"

```