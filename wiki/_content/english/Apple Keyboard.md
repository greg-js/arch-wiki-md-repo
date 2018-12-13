Related articles

*   [Extra keyboard keys](/index.php/Extra_keyboard_keys "Extra keyboard keys")

Some Apple keyboard models may have swapped keys or missing functionality. This article describes how to change the settings for the keyboard so that it behaves as expected.

## Contents

*   [1 Numlock is on](#Numlock_is_on)
*   [2 Repeating keys on a wireless keyboard](#Repeating_keys_on_a_wireless_keyboard)
*   [3 Function keys do not work](#Function_keys_do_not_work)
*   [4 Switching Cmd and Alt/AltGr](#Switching_Cmd_and_Alt/AltGr)
*   [5 < and > have changed place with § and ½](#<_and_>_have_changed_place_with_§_and_½)
*   [6 < and > have changed place with ^ and ° (or @ and #, or ` and ~)](#<_and_>_have_changed_place_with_^_and_°_(or_@_and_#,_or_`_and_~))
*   [7 PrintScreen and SysRq](#PrintScreen_and_SysRq)
*   [8 Treating Apple keyboards like regular keyboards](#Treating_Apple_keyboards_like_regular_keyboards)
    *   [8.1 Use a patch to hid-apple](#Use_a_patch_to_hid-apple)
    *   [8.2 Use un-apple-keyboard](#Use_un-apple-keyboard)
    *   [8.3 Change the Behavior Without Reboot](#Change_the_Behavior_Without_Reboot)
*   [9 Magic Keyboard does not connect](#Magic_Keyboard_does_not_connect)
*   [10 See also](#See_also)

## Numlock is on

You may find that the numlock is on. The symptoms are that only the physical keys `7`,`8`,`9`,`u`,`i`,`o`,`j`,`k`,`l` and surrounding keys work and output numbers. To fix this hit `Fn+F6` twice.

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

If your `F<num>` keys do not work, this is probably because the kernel driver for the keyboard has defaulted to using the media keys and requiring you to use the `Fn` key to get to the `F<num>` keys. To change the behavior temporarily, [append](/index.php/Append "Append") `2` to `/sys/module/hid_apple/parameters/fnmode`.

```
# echo 2 > /sys/module/hid_apple/parameters/fnmode

```

To make the change permanent, [set](/index.php/Kernel_modules#Setting_module_options "Kernel modules") the `hid_apple` `fnmode` option to 2:

 `/etc/modprobe.d/hid_apple.conf`  `options hid_apple fnmode=2` 

To apply the change to your initial ramdisk, in your [mkinitcpio configuration](/index.php/Mkinitcpio#Configuration "Mkinitcpio") (usually `/etc/mkinitcpio.conf`), make sure you either have `modconf` included in the `HOOKS` variable or `/etc/modprobe.d/hid_apple.conf` in the `FILES` variable. You would then need to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

## Switching Cmd and Alt/AltGr

This will switch the left `Alt` and `Cmd` key as well as the right `Alt`/`AltGr` and `Cmd` key.

Temporary and immediate solution:

```
# echo "1" > /sys/module/hid_apple/parameters/swap_opt_cmd

```

Permanent change, taking place at next reboot:

 `/etc/modprobe.d/hid_apple.conf`  `options hid_apple swap_opt_cmd=1` 

You then need to [regenerate the initramfs](/index.php/Regenerate_the_initramfs "Regenerate the initramfs").

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

To change the behavior temporarily, [overwrite](/index.php/Help:Reading#Append,_add,_create,_edit "Help:Reading") `/sys/module/hid_apple/parameters/iso_layout` with `0`. To make the change permanent, [set](/index.php/Kernel_modules#Setting_module_options "Kernel modules") the `hid_apple` `iso_layout` option to 0.

## PrintScreen and SysRq

Apple Keyboards have an `F13` key instead of a `PrintScreen`/`SysRq` key. This means that [Alt+SysRq sequences](/index.php/Keyboard_shortcuts#Kernel "Keyboard shortcuts") do not work, and application actions associated with `PrintScreen` (such as taking screenshots in many games that work under [Wine](/index.php/Wine "Wine")) do not work. To fix this, you can add `setxkbmap -option "apple:alupckeys"` to your `.xinitrc`. This will map `PrintScreen`/`SysRq` to `F13`, as well as `Scroll lock` to `F14` and `Pause` to `F15`.

Alternatively, follow the [Map scancodes to keycodes](/index.php/Map_scancodes_to_keycodes "Map scancodes to keycodes") article to map the `F13` scancode to the `PrintScreen`/`SysRq` keycode, where 458856 (0x0**70068**) is the scancode of `F13`, and `sysrq` is the keycode of `PrintScreen`/`SysRq`.

## Treating Apple keyboards like regular keyboards

Depending on the customisations you want to accomplish, there are two solutions available. You need to choose one of the other.

### Use a patch to hid-apple

While the original `hid-apple` module does not have options to further customize the keyboard, like swapping `Fn` and left `Ctrl` keys or having `Alt` on the left side of `Super`, there is a [patch](https://github.com/free5lot/hid-apple-patched) adding this functionality to the module. To install the patch, [install](/index.php/Install "Install") the [hid-apple-patched-git-dkms](https://aur.archlinux.org/packages/hid-apple-patched-git-dkms/) package.

In addition to the patched kernel module, a configuration file is also provided by the package at `/etc/modprobe.d/hid_apple_pclayout.conf`, which enables PC-like layout by default:

*   Top-row keys are normally function keys, switchable to media keys by holding Fn key, as in [#Function keys do not work](#Function_keys_do_not_work).
*   Four keys at the lower left corner act as `Ctrl`, `Fn`, `Super`, `Alt`, in this order.
*   `Super` and `Alt` keys on the right are swapped.
*   If you have an `Ejectcd` key, it will act as `Delete` key.

Please refer to [https://github.com/free5lot/hid-apple-patched#configuration](https://github.com/free5lot/hid-apple-patched#configuration) for exact meaning of each configuration options and tweaking the configuration file to suit your need.

**Note:** Do not forget to include the configuration file in *initramfs* otherwise it will not work automatically after boot. Refer to [Mkinitcpio#BINARIES and FILES](/index.php/Mkinitcpio#BINARIES_and_FILES "Mkinitcpio") or [Mkinitcpio#HOOKS](/index.php/Mkinitcpio#HOOKS "Mkinitcpio") (the hook you might need is called `modconf`) about how to do that.

After installation the change is not picked up by the kernel immediately. The simplest way is to just reboot your system and the new behavior should be in effect.

### Use un-apple-keyboard

If you do not need all of these customizations and you do not want to compile a new module manually or using dkms, there is an AUR package [un-apple-keyboard](https://aur.archlinux.org/packages/un-apple-keyboard/) which does not rely on a new kernel module, but rather just to mappings. It enables the following features:

*   The keyboard is considered as an ISO keyboard (e.g. `<` and `>` located at the right of the `Left Shift` key are working like expected).
*   The function keys are disabled by default. You need to press the `Fn` key in combination to trigger them. By default, the behavior are thus keys `F1` to `F12`
*   The `Alt` and `Cmd` keys are swapped.
*   `F13` is mapped to `SYSRQ`, `F14` to `Scroll Lock` and `F15` to `Pause`.

The first 3 aforementioned features are brought to you using the default linux kernel module `hid-apple`.

The last one is provided by providing a mapping to [keyfuzz](https://aur.archlinux.org/packages/keyfuzz/).

### Change the Behavior Without Reboot

**Warning:** If the builtin keyboard and touch pad are the only input device, beware that doing so might leave your computer in an inoperable state unless hard reboot when the second command failes.

To reload the kernel module without reboot, run `rmmod hid_apple && modprobe hid_apple`.

## Magic Keyboard does not connect

If you have a magic keyboard that will not connect to the system through the built in tools, such as the Gnome 3 bluetooth menu in settings, install [blueman](https://www.archlinux.org/packages/?name=blueman) and its dependencies and attempt to connect with it. If it still fails to connect, make sure you have bluetoothctl and hcitool installed.

## See also

*   [https://help.ubuntu.com/community/AppleKeyboard](https://help.ubuntu.com/community/AppleKeyboard)
*   [https://github.com/hlechner/xmodmap-aluminium-pt-br](https://github.com/hlechner/xmodmap-aluminium-pt-br)
*   [https://github.com/free5lot/hid-apple-patched](https://github.com/free5lot/hid-apple-patched)