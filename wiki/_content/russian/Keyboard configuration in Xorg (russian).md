**Состояние перевода:** На этой странице представлен перевод статьи [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg"). Дата последней синхронизации: 22 ноября 2017\. Вы можете [помочь](/index.php/ArchWiki_Translation_Team_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "ArchWiki Translation Team (Русский)") синхронизировать перевод, если в английской версии произошли [изменения](https://wiki.archlinux.org/index.php?title=Keyboard_configuration_in_Xorg&diff=0&oldid=497914).

Ссылки по теме

*   [Конфигурация клавиатуры в консоли](/index.php/%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D0%B0%D1%82%D1%83%D1%80%D1%8B_%D0%B2_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D0%B8 "Конфигурация клавиатуры в консоли")
*   [Дополнительные клавиши](/index.php/%D0%94%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D1%88%D0%B8 "Дополнительные клавиши")
*   [Xorg (Русский)](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xorg (Русский)")
*   [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension")

Цель этой статьи описать основные настройки клавиатуры в Xorg. Для расширенных тем, таких как изменение раскладки клавиатуры или дополнительные сопоставления клавиш, смотрите статьи [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension") или [Дополнительные клавиши](/index.php/%D0%94%D0%BE%D0%BF%D0%BE%D0%BB%D0%BD%D0%B8%D1%82%D0%B5%D0%BB%D1%8C%D0%BD%D1%8B%D0%B5_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D1%88%D0%B8 "Дополнительные клавиши") соответственно.

## Contents

*   [1 Обзор](#.D0.9E.D0.B1.D0.B7.D0.BE.D1.80)
*   [2 Просмотр настроек клавиатуры](#.D0.9F.D1.80.D0.BE.D1.81.D0.BC.D0.BE.D1.82.D1.80_.D0.BD.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B5.D0.BA_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [2.1 Сторонние утилиты](#.D0.A1.D1.82.D0.BE.D1.80.D0.BE.D0.BD.D0.BD.D0.B8.D0.B5_.D1.83.D1.82.D0.B8.D0.BB.D0.B8.D1.82.D1.8B)
*   [3 Настройка раскладки клавиатуры](#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BA.D0.B8_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [3.1 Через setxkbmap](#.D0.A7.D0.B5.D1.80.D0.B5.D0.B7_setxkbmap)
    *   [3.2 Через конфигурационные файлы X](#.D0.A7.D0.B5.D1.80.D0.B5.D0.B7_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B_X)
        *   [3.2.1 С помощью localectl](#.D0.A1_.D0.BF.D0.BE.D0.BC.D0.BE.D1.89.D1.8C.D1.8E_localectl)
*   [4 Часто используемые опции XKB](#.D0.A7.D0.B0.D1.81.D1.82.D0.BE_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC.D1.8B.D0.B5_.D0.BE.D0.BF.D1.86.D0.B8.D0.B8_XKB)
    *   [4.1 Переключение раскладок клавиатуры](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.80.D0.B0.D1.81.D0.BA.D0.BB.D0.B0.D0.B4.D0.BE.D0.BA_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D0.B0.D1.82.D1.83.D1.80.D1.8B)
    *   [4.2 Завершение Xorg по сочетанию клавиш Ctrl+Alt+Backspace](#.D0.97.D0.B0.D0.B2.D0.B5.D1.80.D1.88.D0.B5.D0.BD.D0.B8.D0.B5_Xorg_.D0.BF.D0.BE_.D1.81.D0.BE.D1.87.D0.B5.D1.82.D0.B0.D0.BD.D0.B8.D1.8E_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88_Ctrl.2BAlt.2BBackspace)
    *   [4.3 Блокировка клавиши Caps Lock нажатием левого Control](#.D0.91.D0.BB.D0.BE.D0.BA.D0.B8.D1.80.D0.BE.D0.B2.D0.BA.D0.B0_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_Caps_Lock_.D0.BD.D0.B0.D0.B6.D0.B0.D1.82.D0.B8.D0.B5.D0.BC_.D0.BB.D0.B5.D0.B2.D0.BE.D0.B3.D0.BE_Control)
    *   [4.4 Включение кнопок мышки](#.D0.92.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BE.D0.BA_.D0.BC.D1.8B.D1.88.D0.BA.D0.B8)
    *   [4.5 Configuring compose key](#Configuring_compose_key)
        *   [4.5.1 Сочетания клавиш](#.D0.A1.D0.BE.D1.87.D0.B5.D1.82.D0.B0.D0.BD.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88)
    *   [4.6 Значки валют на других кнопках](#.D0.97.D0.BD.D0.B0.D1.87.D0.BA.D0.B8_.D0.B2.D0.B0.D0.BB.D1.8E.D1.82_.D0.BD.D0.B0_.D0.B4.D1.80.D1.83.D0.B3.D0.B8.D1.85_.D0.BA.D0.BD.D0.BE.D0.BF.D0.BA.D0.B0.D1.85)
    *   [4.7 Переключение состояния сразу после нажатия клавиши Caps Lock](#.D0.9F.D0.B5.D1.80.D0.B5.D0.BA.D0.BB.D1.8E.D1.87.D0.B5.D0.BD.D0.B8.D0.B5_.D1.81.D0.BE.D1.81.D1.82.D0.BE.D1.8F.D0.BD.D0.B8.D1.8F_.D1.81.D1.80.D0.B0.D0.B7.D1.83_.D0.BF.D0.BE.D1.81.D0.BB.D0.B5_.D0.BD.D0.B0.D0.B6.D0.B0.D1.82.D0.B8.D1.8F_.D0.BA.D0.BB.D0.B0.D0.B2.D0.B8.D1.88.D0.B8_Caps_Lock)
        *   [4.7.1 Временное решение](#.D0.92.D1.80.D0.B5.D0.BC.D0.B5.D0.BD.D0.BD.D0.BE.D0.B5_.D1.80.D0.B5.D1.88.D0.B5.D0.BD.D0.B8.D0.B5)
*   [5 Adjusting typematic delay and rate](#Adjusting_typematic_delay_and_rate)
    *   [5.1 Using xset](#Using_xset)
    *   [5.2 Using XServer startup options](#Using_XServer_startup_options)
    *   [5.3 Using XServer options](#Using_XServer_options)
*   [6 See also](#See_also)

## Обзор

The Xorg server uses the [X KeyBoard extension](/index.php/X_KeyBoard_extension "X KeyBoard extension") (XKB) to define keyboard layouts. Optionally, [xmodmap](/index.php/Xmodmap "Xmodmap") can be used to access the internal keymap table directly, although this is not recommended for complex tasks. Also [systemd](/index.php/Systemd "Systemd")'s *localectl* can be used to define the keyboard layout for both the Xorg server and the virtual console.

**Примечание:** XKB options can be overridden by the tools provided by some desktop environments such as [GNOME (XkbOptions)](/index.php/GNOME#XkbOptions_keyboard_options "GNOME") and [KDE (set keyboard)](/index.php/KDE#Set_keyboard "KDE").

## Просмотр настроек клавиатуры

Вы можете использовать следующую команду, чтобы просмотреть настройки XKB:

 `$ setxkbmap -print -verbose 10` 
```
Setting verbose level to 10
locale is C
Applied rules from evdev:
model:      evdev
layout:     us
options:    terminate:ctrl_alt_bksp
Trying to build keymap using the following components:
keycodes:   evdev+aliases(qwerty)
types:      complete
compat:     complete
symbols:    pc+us+inet(evdev)+terminate(ctrl_alt_bksp)
geometry:   pc(pc104)
xkb_keymap {
        xkb_keycodes  { include "evdev+aliases(qwerty)" };
        xkb_types     { include "complete"      };
        xkb_compat    { include "complete"      };
        xkb_symbols   { include "pc+us+inet(evdev)+terminate(ctrl_alt_bksp)"    };
        xkb_geometry  { include "pc(pc104)"     };
};

```

### Сторонние утилиты

Здесь приведены некоторые "неофициальные" утилиты, которые позволяют выводить специфичную информацию о используемой в настоящее время раскладке клавиатуры.

*   [xkb-switch-git](https://aur.archlinux.org/packages/xkb-switch-git/):

 `$ xkb-switch`  `us` 

*   [xkblayout-state](https://aur.archlinux.org/packages/xkblayout-state/):

 `$ xkblayout-state print "%s"`  `de` 

## Настройка раскладки клавиатуры

Раскладку клавиатуры можно настроить разными способами в Xorg. Вот объяснение используемых параметров:

*   `XkbModel` устанавливает модель клавиатуры. Это влияет только на некоторые дополнительные клавиши. Для большиства клавиатур подходят модели `pc104` или `pc105`. Но, например, ноутбуки обычно имеют дополнительные клавиши, чтобы заставить их работать иногда достаточно только выбрать правильную модель клавиатуры.
*   `XkbLayout` устанавливает раскладку клавиатуры. Несколько раскладок могут быть указаны в списке, разделенном запятыми, если, например, вам нужно быстро переключаться между ними.
*   `XkbVariant` устанавливает специфичое расположение клавиш для раскладки. Например, вариант по умолчанию для `sk` - `qwertz`, но его можно изменить вручную на другой, например, `qwerty`.
*   `XkbOptions` устанавливает некоторые дополнительные опции. Используется для указания клавиш для смены раскладки, уведомления светодиодом, режима compose и др. Смотрите раздел [#Часто используемые опции XKB](#.D0.A7.D0.B0.D1.81.D1.82.D0.BE_.D0.B8.D1.81.D0.BF.D0.BE.D0.BB.D1.8C.D0.B7.D1.83.D0.B5.D0.BC.D1.8B.D0.B5_.D0.BE.D0.BF.D1.86.D0.B8.D0.B8_XKB) для примеров.

**Примечание:** Необходимо указывать варианты для каждой установленной раскладки. Если вам нужен стандартный вариант, укажите пустую строку, как вариант (запятая должна оставаться). Например, имеется первичная стандартная раскладка `us` и вторичная раскладка `us` с вариантом расположения клавиш `dvorak`, тогда укажите `us,us` как `XkbLayout` и `,dvorak` как `XkbVariant`.

Имя раскладки, как правило, состоиз из [2-буквенного кода страны](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2#Officially_assigned_code_elements "wikipedia:ISO 3166-1 alpha-2"). Чтобы посмотреть полный список моделей клавиатур, раскладок, вариантов и опций вместе с коротким описанием, откройте файл `/usr/share/X11/xkb/rules/base.lst`. Кроме того, вы можете использовать одну из следующих команд для просмотра раскладки и т.д., но без описания:

*   `localectl list-x11-keymap-models`
*   `localectl list-x11-keymap-layouts`
*   `localectl list-x11-keymap-variants [*layout*]`
*   `localectl list-x11-keymap-options`

Примеры в следующих подразделах будут делать одно и то же. Они устанавливают модель клавиатуры `pc105`, первичной раскладкой `us`, `ru` - вторичной раскладкой, вариант расположения клавиш `dvorak` для раскладки `us` и комбинацию клавиш `Alt+Shift` для переключения между раскладками. Для получения дополнительной информации смотрите [xkeyboard-config(7)](https://jlk.fjfi.cvut.cz/arch/manpages/man/xkeyboard-config.7).

### Через setxkbmap

*setxkbmap* настраивает раскладку клавиатуры только для текущей сессии X, но ее можно сделать постоянной в [xinitrc](/index.php/Xinitrc_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xinitrc (Русский)") или [xprofile](/index.php/Xprofile_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9) "Xprofile (Русский)"). Это переопределяет общесистемные настройки, указанные в [#Через конфигурационные файлы X](#.D0.A7.D0.B5.D1.80.D0.B5.D0.B7_.D0.BA.D0.BE.D0.BD.D1.84.D0.B8.D0.B3.D1.83.D1.80.D0.B0.D1.86.D0.B8.D0.BE.D0.BD.D0.BD.D1.8B.D0.B5_.D1.84.D0.B0.D0.B9.D0.BB.D1.8B_X).

Используйте следующим образом (смотрите [setxkbmap(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/setxkbmap.1)):

```
$ setxkbmap [-model *xkb_model*] [-layout *xkb_layout*] [-variant *xkb_variant*] [-option *xkb_options*]

```

Чтобы изменить раскладку введите (`-layout` - стандартный флаг):

```
$ setxkbmap *xkb_layout*

```

Для нескольких настроек:

```
$ setxkbmap -model pc105 -layout us,ru -variant dvorak, -option grp:alt_shift_toggle

```

### Через конфигурационные файлы X

**Примечание:** `xorg.conf` анализируется X-сервером при запуске. Чтобы применить изменения, перезапустите X.

Синтакс конфигурационных файлов X объяснен в [Xorg (Русский)#Настройка](/index.php/Xorg_(%D0%A0%D1%83%D1%81%D1%81%D0%BA%D0%B8%D0%B9)#.D0.9D.D0.B0.D1.81.D1.82.D1.80.D0.BE.D0.B9.D0.BA.D0.B0 "Xorg (Русский)"). Этот способ создает постоянные общесистемные настройки.

Вот пример:

 `/etc/X11/xorg.conf.d/00-keyboard.conf` 
```
Section "InputClass"
        Identifier "system-keyboard"
        MatchIsKeyboard "on"
        Option "XkbLayout" "us,ru"
        Option "XkbModel" "pc105"
        Option "XkbVariant" "dvorak,"
        Option "XkbOptions" "grp:alt_shift_toggle"
EndSection

```

#### С помощью localectl

Для удобства можно использовать инструмент *localectl* вместо ручного редактирования конфигурационных файлов X. Он сохраняет настройки в файл `/etc/X11/xorg.conf.d/00-keyboard.conf`, который не следует редактировать вручную, потому что *localectl* перепишет его при следующем запуске.

Используйте следующим образом:

```
$ localectl [--no-convert] set-x11-keymap *раскладка* [*модель* [*вариант* [*опции*]]]

```

Чтобы установить *модель*, *вариант* или *опции*, нужно указать все эти поля, но их можно пропустить, передав пустую строку `""`. Если параметр `--no-convert` не передан, тогда указанная клавиатура преобразуется в ближайшую соответствующую раскладку для консоли и прописывается в [настройках консоли](/index.php/%D0%9A%D0%BE%D0%BD%D1%84%D0%B8%D0%B3%D1%83%D1%80%D0%B0%D1%86%D0%B8%D1%8F_%D0%BA%D0%BB%D0%B0%D0%B2%D0%B8%D0%B0%D1%82%D1%83%D1%80%D1%8B_%D0%B2_%D0%BA%D0%BE%D0%BD%D1%81%D0%BE%D0%BB%D0%B8 "Конфигурация клавиатуры в консоли") в файле `vconsole.conf`. Для получения дополнительной информации смотрите [localectl(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/localectl.1).

Чтобы создать файл `/etc/X11/xorg.conf.d/00-keyboard.conf`, как указано выше:

```
$ localectl --no-convert set-x11-keymap us,ru pc105 dvorak, grp:alt_shift_toggle

```

## Часто используемые опции XKB

### Переключение раскладок клавиатуры

To be able to easily switch keyboard layouts, first specify multiple layouts between which you want to switch (the first one is the default). Then specify a key (or key combination), which will be used for switching. For example, to switch between a US and a Swedish layout using the `CapsLock` key, use `us,se` as an argument of `XkbLayout` and `grp:caps_toggle` as an argument of `XkbOptions`.

You can use other key combinations than `CapsLock`, they are listed in `/usr/share/X11/xkb/rules/base.lst`, start with `grp:` and end with `toggle`. To get the full list of available options, run the following command:

```
$ grep "grp:.*toggle" /usr/share/X11/xkb/rules/base.lst

```

### Завершение Xorg по сочетанию клавиш Ctrl+Alt+Backspace

By default, the key combination `Ctrl+Alt+Backspace` is disabled. You can enable it by passing `terminate:ctrl_alt_bksp` to `XkbOptions`. This can also be done by binding a key to `Terminate_Server` in `xmodmap` (which undoes any existing `XkbOptions` setting). In order for either method to work, one also needs to have `DontZap` set to "off" in `ServerFlags`; however, from at least version R6.8.0 (year 2004) [[1]](https://www.x.org/archive/X11R6.8.0/doc/xorg.conf.5.html) this is the default.

### Блокировка клавиши Caps Lock нажатием левого Control

To swap Caps Lock with Left Control key, add `ctrl:swapcaps` to `XkbOptions`. Run the following command to see similar options along with their descriptions:

```
$ grep -E "(ctrl|caps):" /usr/share/X11/xkb/rules/base.lst

```

### Включение кнопок мышки

[Mouse keys](https://en.wikipedia.org/wiki/Mouse_keys "w:Mouse keys") is disabled by default and has to be manually enabled by passing `keypad:pointerkeys` to `XkbOptions`. This will make the `Shift+NumLock` shortcut toggle mouse keys.

See also [X KeyBoard extension#Mouse control](/index.php/X_KeyBoard_extension#Mouse_control "X KeyBoard extension") for advanced configuration.

### Configuring compose key

Though typically not on traditional keyboards, a [Compose key](https://en.wikipedia.org/wiki/Compose_key "wikipedia:Compose key") can be configured to an existent key.

The `Compose` key begins a keypress sequence that involves (usually two) additional keypresses. Usage is typically either for entering characters in a language that the keyboard was not designed for, or for other less-used characters that are not covered with the `AltGr` modifier. For example, pressing `Compose` `'` `e` produces `é`, or `Compose` `-` `-` will produce an "em dash": `—`.

Though a few more eccentric keyboards feature a `Compose` key, its availability is usually through substituting an already existing key to it. For example, to make the `Menu` key a `Compose` key use the [Desktop environment](/index.php/Desktop_environment "Desktop environment") configuration, or pass `compose:menu` to `XkbOptions` (or [setxkbmap](#Using_setxkbmap): `setxkbmap -option compose:menu`). Allowed key substitutions are defined in `/usr/share/X11/xkb/rules/base.lst`:

```
$ grep "compose:" /usr/share/X11/xkb/rules/base.lst

```

If the desired mapping is not found in that file, an alternative is to use [xmodmap](/index.php/Xmodmap "Xmodmap") to map the desired key to the `Multi_key` keysym, which acts as a compose key by default (note that *xmodmap* settings are reset by *setxkbmap*).

#### Сочетания клавиш

The default combinations for the compose keys depend on the [locale](/index.php/Locale "Locale") configured for the session and are stored in `/usr/share/X11/locale/*used_locale*/Compose`, where `*used_locale*` is for example `en_US.UTF-8`.

You can define your own compose key combinations by copying the default file to `~/.XCompose` and editing it. The compose key works with any of the thousands of valid Unicode characters, including those outside the Basic Multilingual Plane.

However, GTK does not use [XIM](https://en.wikipedia.org/wiki/X_Input_Method "wikipedia:X Input Method") by default and therefore does not follow `~/.XCompose` keys. This can be fixed by forcing GTK to use XIM by adding `export GTK_IM_MODULE=xim` and/or `export XMODIFIERS="@im=none"` to `~/.xprofile`.

**Tip:** XIM is very old, you might have better luck with other input methods: [SCIM](/index.php/SCIM "SCIM"), [UIM](/index.php/UIM "UIM"), [IBus](/index.php/IBus "IBus"), etc. See [Internationalization#Input methods in Xorg](/index.php/Internationalization#Input_methods_in_Xorg "Internationalization") for details.

**Note:** XIM will prevent insertion of Unicode characters with the `Ctrl+Shift+u` combination.

### Значки валют на других кнопках

Most European keyboards have a Euro sign (€) printed on on the `5` key. For example, to access it with `Alt+5`, use the `lv3:lalt_switch` and `eurosign:5` options.

The Rupee sign (₹) can be used the same way with `rupeesign:4`.

### Переключение состояния сразу после нажатия клавиши Caps Lock

Those who prefer typing capital letters with the Caps Lock key may experience a short delay when Caps Lock state is switched, resulting in two or more capital letters (e.g. *THe*, *ARch LInux*). This behaviour [stems from typewriters](https://en.wikipedia.org/wiki/Caps_lock#History "wikipedia:Caps lock").

Some more popular operating systems have removed this behaviour, either voluntarily (as it can be confusing to some) or by mistake, however this is a question of preference. Bug reports have been filed on the Xserver bug tracker, as there is currently no easy way to switch to the behaviour reflected by those other operating systems. For anyone who would like to follow up the issue, bug reports and latest working progress can be found at [[2]](https://bugs.freedesktop.org/show_bug.cgi?id=27903) and [[3]](https://bugs.freedesktop.org/show_bug.cgi?id=56491).

#### Временное решение

First, export your keyboard configurations to a file:

```
$ xkbcomp -xkb $DISPLAY xkbmap

```

In the file *xkbmap*, locate the Caps Lock section which begins with *key <CAPS>*:

```
 key <CAPS> {         [       Caps_Lock ] };

```

and replace whole section with the following code:

```
key <CAPS> {
    repeat=no,
    type[group1]="ALPHABETIC",
    symbols[group1]=[ Caps_Lock, Caps_Lock],
    actions[group1]=[ LockMods(modifiers=Lock), Private(type=3,data[0]=1,data[1]=3,data[2]=3)]
};

```

Save and reload keyboard configurations:

```
$ xkbcomp -w 0 xkbmap $DISPLAY

```

Consider making it a service launching after X starts, since reloaded configurations do not survive a system reboot.

## Adjusting typematic delay and rate

The *typematic delay* indicates the amount of time (typically in miliseconds) a key needs to be pressed and held in order for the repeating process to begin. After the repeating process has been triggered, the character will be repeated with a certain frequency (usually given in Hz) specified by the *typematic rate*. Note that these settings are configured seperately for Xorg and [for the virtual console](/index.php/Keyboard_configuration_in_console#Adjusting_typematic_delay_and_rate "Keyboard configuration in console").

### Using xset

The tool *xset* can be used to set the typematic delay and rate for an active X server, certain actions during runtime tho may cause the XServer to reset these changes and revert instead to its *seat defaults*.

Usage:

```
$ xset r rate *delay* [*rate*]

```

For example to set a typematic delay to 200ms and a typematic rate to 30Hz, use the following command (use [xinitrc](/index.php/Xinitrc "Xinitrc") to make it permanent):

```
$ xset r rate 200 30

```

Issuing the command without specifying the delay and rate will reset the typematic values to their respective defaults; a delay of 660ms and a rate of 25Hz:

```
$ xset r rate

```

### Using XServer startup options

A more resistant way to set the typematic delay and rate is to make them the *seat defaults* by passing the desired settings to the X server on its startup using the following options:

*   `-ardelay *miliseconds*` - sets the autorepeat delay (length of time in milliseconds that a key must be depressed before autorepeat starts).
*   `-arinterval *miliseconds*` - sets the autorepeat interval (length of time in milliseconds that should elapse between autorepeat-generated keystrokes).

See [Xserver(1)](https://jlk.fjfi.cvut.cz/arch/manpages/man/Xserver.1) for a full list of X server options and refer to your [display manager](/index.php/Display_manager "Display manager") for information about how to pass these options.

### Using XServer options

Add this line to `/etc/X11/xorg.conf.d/00-keyboard.conf`:

```
Option "AutoRepeat" "*delay* *rate*"

```

## See also

*   [Madduck guide](http://madduck.net/docs/extending-xkb/) on extending XKB