Some Apple keyboard models may have swapped keys or missing functionality. This article describes how to change the settings for the keyboard so that it behaves as expected.

## Contents

*   [1 Numlock is on](#Numlock_is_on)
*   [2 Repeating keys on a wireless keyboard](#Repeating_keys_on_a_wireless_keyboard)
*   [3 Function keys do not work](#Function_keys_do_not_work)
*   [4 < and > have changed place with § and ½](#.3C_and_.3E_have_changed_place_with_.C2.A7_and_.C2.BD)
*   [5 < and > have changed place with ^ and ° (or @ and #, or ` and ~)](#.3C_and_.3E_have_changed_place_with_.5E_and_.C2.B0_.28or_.40_and_.23.2C_or_.60_and_.7E.29)
*   [6 PrintScreen and SysRq](#PrintScreen_and_SysRq)
*   [7 Treating Apple keyboards like regular keyboards](#Treating_Apple_keyboards_like_regular_keyboards)
    *   [7.1 Change the Behavior Without Reboot](#Change_the_Behavior_Without_Reboot)
*   [8 See also](#See_also)

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

Apple Keyboards have an `F13` key instead of a `PrintScreen`/`SysRq` key. This means that [Alt+SysRq sequences](/index.php/Keyboard_shortcuts#Kernel "Keyboard shortcuts") do not work, and application actions associated with `PrintScreen` (such as taking screenshots in many games that work under [Wine](/index.php/Wine "Wine")) do not work. To fix this, you can add `setxkbmap -option "apple:alupckeys"` to your `.xinitrc`. This will map `PrintScreen`/`SysRq` to `F13`, as well as `Scroll lock` to `F14` and `Pause` to `F15`.

Alternatively, follow the [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes") article to map the `F13` scancode to the `PrintScreen`/`SysRq` keycode, where 458856 (0x0**70068**) is the scancode of `F13`, and `sysrq` is the keycode of `PrintScreen`/`SysRq`.

## Treating Apple keyboards like regular keyboards

**Warning:** Another package [un-apple-keyboard](https://aur.archlinux.org/packages/un-apple-keyboard/) also provides similar functionality, but is no longer actively maintained. Thus it is advised to use the following package.

While the original `hid-apple` module doesn't have options to further customize the keyboard, like swapping `Fn` and left `Ctrl` keys or having `Alt` on the left side of `Super`, there is a [patch](https://github.com/free5lot/hid-apple-patched) adding this functionality to the module. To install the patch, [install](/index.php/Install "Install") the [hid-apple-patched-git-dkms](https://aur.archlinux.org/packages/hid-apple-patched-git-dkms/) package.

In addition to the patched kernel module, a configuration file is also provided by the package at `/etc/modprobe.d/hid_apple_pclayout.conf`, which enables PC-like layout by default:

*   Top-row keys are normally function keys, switchable to media keys by holding Fn key, as in [#Function keys do not work](#Function_keys_do_not_work).
*   Four keys at the lower left corner act as `Ctrl`, `Fn`, `Super`, `Alt`, in this order.
*   `Super` and `Alt` keys on the right are swapped.
*   If you have an `Ejectcd` key, it will act as `Delete` key.

Please refer to [https://github.com/free5lot/hid-apple-patched#configuration](https://github.com/free5lot/hid-apple-patched#configuration) for exact meaning of each configuration options and tweaking the configuration file to suit your need.

**Note:** Don't forget to include the configuration file in *initramfs* otherwise it won't work automatically after boot. Refer to [Mkinitcpio#BINARIES and FILES](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio") or [Mkinitcpio#Hooks](/index.php/Mkinitcpio#Hooks "Mkinitcpio") (the hook you might need is called `modconf`) about how to do that.

After installation the change is not picked up by the kernel immediately. The simplest way is to just reboot your system and the new behavior should be in effect.

### Change the Behavior Without Reboot

**Warning:** If the builtin keyboard and touch pad are the only input device, beware that doing so might leave your computer in an inoperable state unless hard reboot when the second command failes.

To reload the kernel module without reboot, run `sudo rmmod hid_apple && sudo modprobe hid_apple`.

## See also

*   [https://help.ubuntu.com/community/AppleKeyboard](https://help.ubuntu.com/community/AppleKeyboard)
*   [https://github.com/hlechner/xmodmap-aluminium-pt-br](https://github.com/hlechner/xmodmap-aluminium-pt-br)
*   [https://github.com/free5lot/hid-apple-patched](https://github.com/free5lot/hid-apple-patched)