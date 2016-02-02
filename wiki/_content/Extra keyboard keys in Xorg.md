# Extra keyboard keys in Xorg

## Contents

*   [1 Mapping keysyms to actions](#Mapping_keysyms_to_actions)
    *   [1.1 Third-party tools](#Third-party_tools)
        *   [1.1.1 sxhkd](#sxhkd)
        *   [1.1.2 keytouch](#keytouch)
        *   [1.1.3 actkbd](#actkbd)
        *   [1.1.4 xbindkeys](#xbindkeys)

## Mapping keysyms to actions

When we are in a graphical environment we may want to execute a command when certain key combination is pressed. There are multiple ways to do that:

*   The most portable way using low level tools, such as [acpid](/index.php/Acpid "Acpid"). Not all keys are supported, but configuration in uniform way is possible for keyboard keys, power adapter connection and even headphone jack (un)plugging events. It is also difficult to run programs inside X session correctly.
*   The universal way using [Xorg](/index.php/Xorg "Xorg") utilities (e.g. [xbindkeys](/index.php/Xbindkeys "Xbindkeys")) and eventually your desktop environment or window manager tools.
*   The quicker way using a third-party program to do everything in GUI, such as the Gnome Control Center or [Keytouch](/index.php/Keytouch "Keytouch").

### Third-party tools

#### sxhkd

A simple X hotkey daemon with a powerful and compact configuration syntax. See [sxhkd](/index.php/Sxhkd "Sxhkd") for details.

#### keytouch

KeyTouch is a program which allows you to easily configure the extra function keys of your keyboard. This means that you can define, for every individual function key, what to do if it is pressed.

See the main article: [keytouch](/index.php/Keytouch "Keytouch").

#### actkbd

From [actkbd home page](http://users.softlab.ece.ntua.gr/~thkala/projects/actkbd/):

	[actkbd](https://aur.archlinux.org/packages/actkbd/)<sup><small>AUR</small></sup> (available in [AUR](/index.php/AUR "AUR")) is a simple daemon that binds actions to keyboard events. It recognises key combinations and can handle press, repeat and release events. Currently it only supports the linux-2.6 evdev interface. It uses a plain-text configuration file which contains all the bindings.

A sample configuration and guide is available [here](http://users.softlab.ece.ntua.gr/~thkala/projects/actkbd/latest/README).

#### xbindkeys

[xbindkeys](/index.php/Xbindkeys "Xbindkeys") allows advanced mapping of keysyms to actions independently of the Desktop Environment.

**Tip:** If you find `xbindkeys` difficult to use, try the graphical manager [xbindkeys_config](https://aur.archlinux.org/packages/xbindkeys_config/)<sup><small>AUR</small></sup><sup>[[broken link](/index.php/ArchWiki:Requests#Broken_package_links "ArchWiki:Requests"): archived in [aur-mirror](http://pkgbuild.com/git/aur-mirror.git/tree/xbindkeys_config)]</sup> from the [AUR](/index.php/AUR "AUR").

Retrieved from "[https://wiki.archlinux.org/index.php?title=Extra_keyboard_keys_in_Xorg&oldid=392110](https://wiki.archlinux.org/index.php?title=Extra_keyboard_keys_in_Xorg&oldid=392110)"