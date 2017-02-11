Some Apple keyboard models may have swapped keys or missing functionality. This article describes how to change the settings for the keyboard so that it behaves as expected.

## Contents

*   [1 Numlock is on](#Numlock_is_on)
*   [2 Repeating keys on a wireless keyboard](#Repeating_keys_on_a_wireless_keyboard)
*   [3 Function keys do not work](#Function_keys_do_not_work)
*   [4 < and > have changed place with § and ½](#.3C_and_.3E_have_changed_place_with_.C2.A7_and_.C2.BD)
*   [5 < and > have changed place with ^ and ° (or @ and #, or ` and ~)](#.3C_and_.3E_have_changed_place_with_.5E_and_.C2.B0_.28or_.40_and_.23.2C_or_.60_and_.7E.29)
*   [6 PrintScreen and SysRq](#PrintScreen_and_SysRq)
*   [7 Treating Apple keyboards like regular keyboards](#Treating_Apple_keyboards_like_regular_keyboards)
*   [8 Swap the Alt key and Command key (Meta/Super)](#Swap_the_Alt_key_and_Command_key_.28Meta.2FSuper.29)
*   [9 Swap the Fn key and Left Ctrl key](#Swap_the_Fn_key_and_Left_Ctrl_key)
*   [10 See also](#See_also)

## Numlock is on

You may find that the numlock is on. The symptoms are that only the physical keys 7,8,9,u,i,o,j,k,l and surrounding keys work and output numbers. To fix this hit `Fn`+`F6` twice.

Alternatively, set the keycodes manually using [xmodmap](/index.php/Xmodmap "Xmodmap") to avoid use Numlock:

```
keycode  90 = KP_0 KP_0 KP_0 KP_0 KP_0 KP_0
keycode  87 = KP_1 KP_1 KP_1 KP_1 KP_1 KP_1
keycode  88 = KP_2 KP_2 KP_2 KP_2 KP_2 KP_2
keycode  89 = KP_3 KP_3 KP_3 KP_3 KP_3 KP_3
keycode  83 = KP_4 KP_4 KP_4 KP_4 KP_4 KP_4
keycode  84 = KP_5 KP_5 KP_5 KP_5 KP_5 KP_5
keycode  85 = KP_6 KP_6 KP_6 KP_6 KP_6 KP_6
keycode  79 = KP_7 KP_7 KP_7 KP_7 KP_7 KP_7
keycode  80 = KP_8 KP_8 KP_8 KP_8 KP_8 KP_8
keycode  81 = KP_9 KP_9 KP_9 KP_9 KP_9 KP_9

```

## Repeating keys on a wireless keyboard

Unpair the keyboard and then re-pair it. The trick is to hold down the power button throughout the entire pairing process.

## Function keys do not work

If your `F<num>` keys do not work, this is probably because the kernel driver for the keyboard has defaulted to using the media keys and requiring you to use the `Fn` key to get to the `F<num>` keys. To change the behavior temporarily, [append](/index.php/Help:Reading#Append.2C_add.2C_create.2C_edit "Help:Reading") `2` to `/sys/module/hid_apple/parameters/fnmode`. To make the change permanent, [set](/index.php/Kernel_modules#Setting_module_options "Kernel modules") the `hid_apple` `fnmode` option to 2.

## < and > have changed place with § and ½

If the **<** and **>** are switched with the **§** and **½** keys, [set the xkb option](/index.php/Keyboard_configuration_in_Xorg "Keyboard configuration in Xorg") `apple:badmap`, for instance by running the following command in your graphical environment:

```
$ setxkbmap -option apple:badmap

```

Alternatively, set the keycodes manually using [xmodmap](/index.php/Xmodmap "Xmodmap"):

```
keycode  49 = less greater less greater bar brokenbar
keycode  94 = section degree section degree notsign notsign

```

If you use a Canadian multilingual layout (where the "ù" and the "/" is switch) use this:

```
keycode  94 = slash backslash slash backslash bar brokenbar
keycode  49 = ugrave Ugrave ugrave Ugrave notsign notsign

```

## < and > have changed place with ^ and ° (or @ and #, or ` and ~)

With German layout, circumflex/degree symbol and </> are exchanged. With French layout, @/# are exchanged. With the US layout, `/~ and </> are exchanged.

To change the behavior temporarily, [append](/index.php/Help:Reading#Append.2C_add.2C_create.2C_edit "Help:Reading") `0` to `/sys/module/hid_apple/parameters/iso_layout`. To make the change permanent, [set](/index.php/Kernel_modules#Setting_module_options "Kernel modules") the `hid_apple` `iso_layout` option to 0.

## PrintScreen and SysRq

Apple Keyboards have an `F13` key instead of a `PrintScreen`/`SysRq` key. This means that [Alt+SysRq sequences](/index.php/Keyboard_shortcuts#Kernel "Keyboard shortcuts") do not work, and application actions associated with `PrintScreen` (such as taking screenshots in many games that work under [Wine](/index.php/Wine "Wine")) do not work. To fix this, [map the `F13` scancode to the `PrintScreen`/`SysRq` keycode](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes"), where 458856 (0x070068) is the scancode of `F13`, and 99 is the keycode of `PrintScreen`/`SysRq`.

## Treating Apple keyboards like regular keyboards

If you want to use your Apple keyboard like a regular US-layout keyboard, with `Alt` on the left side of `Meta`, you can use the [AUR](/index.php/AUR "AUR") package [un-apple-keyboard](https://aur.archlinux.org/packages/un-apple-keyboard/). Currently it only works for the aluminium USB model. The package does the following things:

*   Adds a `/etc/modprobe.d/hid_apple.conf` file which enables the `F<num>` keys by default, as in [#Function keys do not work](#Function_keys_do_not_work).
*   Uses keyfuzz to remap `F13-15` to `PrintScreen`/`SysRq`, `Scroll Lock`, and `Pause`, respectively.
*   Swaps the ordering of the `Alt` and `Meta` (`Command`) keys to match all other keyboards, again using `/etc/modprobe.d/hid_apple.conf`, as in [#Swap the Alt key and Command key (Meta/Super)](#Swap_the_Alt_key_and_Command_key_.28Meta.2FSuper.29).
*   Applies these changes automatically when you plug in your keyboard, with a [udev](/index.php/Udev "Udev") rule.

You will need to add `/etc/modprobe.d/hid_apple.conf` to FILES in [mkinitcpio.conf](/index.php/Mkinitcpio.conf "Mkinitcpio.conf"). Otherwise if you boot your computer with the Apple keyboard plugged in, the the `F<num>` keys will not work by default.

## Swap the Alt key and Command key (Meta/Super)

To change the behavior temporarily, [append](/index.php/Help:Reading#Append.2C_add.2C_create.2C_edit "Help:Reading") `1` to `/sys/module/hid_apple/parameters/swap_opt_cmd`. To make the change permanent, [set](/index.php/Kernel_modules#Setting_module_options "Kernel modules") the `hid_apple` `swap_opt_cmd` option to 1.

## Swap the Fn key and Left Ctrl key

While the original `hid-apple` module doesn't have an option to swap the fn and left control keys, there is a [patch](https://github.com/free5lot/hid-apple-patched) adding this functionality to the module. To install the patch, [install](/index.php/Install "Install") the [hid-apple-patched-git](https://aur.archlinux.org/packages/hid-apple-patched-git/) package.

To change the behavior temporarily, [append](/index.php/Help:Reading#Append.2C_add.2C_create.2C_edit "Help:Reading") `1` to `/sys/module/hid_apple/parameters/swap_fn_leftctrl`. To make the change permanent, [set](/index.php/Kernel_modules#Setting_module_options "Kernel modules") the `hid_apple` `swap_fn_leftctrl` option to 1.

**Note:**

*   The default configuration provided in [hid-apple-patched-git](https://aur.archlinux.org/packages/hid-apple-patched-git/) also swaps the left option and command keys so you don't have to follow [#Swap the Alt key and Command key (Meta/Super)](#Swap_the_Alt_key_and_Command_key_.28Meta.2FSuper.29) to do that.
*   This [hid-apple-patched-git](https://aur.archlinux.org/packages/hid-apple-patched-git/) also provides an option to use ejectcd key as the missing delete key on Apple keyboard. It is enabled by default through the `ejectcd_as_delete=1` option.

## See also

*   [https://help.ubuntu.com/community/AppleKeyboard](https://help.ubuntu.com/community/AppleKeyboard)
*   [https://github.com/hlechner/xmodmap-aluminium-pt-br](https://github.com/hlechner/xmodmap-aluminium-pt-br)