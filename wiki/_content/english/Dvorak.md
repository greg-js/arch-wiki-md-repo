This is a quick blurb for setting or converting your keymaps to dvorak instead of qwerty.

## Contents

*   [1 Setting dvorak layout](#Setting_dvorak_layout)
*   [2 For international users](#For_international_users)
    *   [2.1 Swedish](#Swedish)
    *   [2.2 Spanish](#Spanish)
*   [3 Typing tutors](#Typing_tutors)

## Setting dvorak layout

See [Keyboard configuration in console](/index.php/Keyboard_configuration_in_console "Keyboard configuration in console") or [Keyboard configuration in Xorg](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") for configuration details.

These variants are available in both console and Xorg:

*   `dvorak`, standard dvorak layout
*   `dvorak-l`, left-handed dvorak layout
*   `dvorak-r`, right-handed dvorak layout

**Note:** For console, these are standalone keymaps, but for Xorg these are variants of the `us` layout, you need to pass them to `XkbVariant` variable. See [Keyboard configuration in Xorg#Setting keyboard layout](/index.php/Keyboard_configuration_in_Xorg#Setting_keyboard_layout "Keyboard configuration in Xorg") for an explanation.

The following variants are available only in Xorg:

*   `dvorak-intl`, international layout with dead keys

## For international users

### Swedish

Swedish people interested in trying dvorak can find the swedish "version", called svorak, at [aoeu.info](http://www.aoeu.info)! To convert to svorak in X you do not need to download any additional files from www.aoeu.info.

### Spanish

In console, specify `dvorak-es` instead of `dvorak` to use the Spanish dvorak variant.

In Xorg, specify `es` as `XkbLayout` and `dvorak` as `XkbVariant`.

## Typing tutors

	Console

*   [DvorakNG](https://aur.archlinux.org/packages/DvorakNG/)

	GUI

*   [kdeedu-ktouch](https://www.archlinux.org/packages/?name=kdeedu-ktouch) (includes Dvorak lessons in English, French, German & Spanish)
*   [klavaro](https://www.archlinux.org/packages/?name=klavaro) Dvorak lessons: (BG; BR; DE_neo2; EO; FR; FR_bépo; TR; UK; US; US_BR; US_ES; US_SE)