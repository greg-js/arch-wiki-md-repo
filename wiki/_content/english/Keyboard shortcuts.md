This article provides a list of (not commonly known) default keyboard shortcuts and provides information about user customization.

<input type="checkbox" role="button" id="toctogglecheckbox" class="toctogglecheckbox" style="display:none">

## Contents

<label class="toctogglelabel" for="toctogglecheckbox"></label>

*   [1 Standard shortcuts](#Standard_shortcuts)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Virtual console](#Virtual_console)
    *   [1.3 Xorg and Wayland](#Xorg_and_Wayland)
*   [2 Customization](#Customization)
    *   [2.1 Readline](#Readline)
    *   [2.2 Zsh](#Zsh)
    *   [2.3 Xorg](#Xorg)
        *   [2.3.1 sxhkd](#sxhkd)
        *   [2.3.2 actkbd](#actkbd)
        *   [2.3.3 xbindkeys](#xbindkeys)
    *   [2.4 Desktop environments](#Desktop_environments)
    *   [2.5 Windows managers](#Windows_managers)
    *   [2.6 Key binding for X-selection-paste](#Key_binding_for_X-selection-paste)
        *   [2.6.1 XMonad Window Manager](#XMonad_Window_Manager)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 See also](#See_also)

## Standard shortcuts

### Kernel

There are several low level shortcuts that are implemented in the kernel which can be used for debugging and recovering from an unresponsive system. Whenever possible, it is recommended that you use these shortcuts instead of doing a hard shutdown (holding down the power button to completely power off the system).

To use these, they must first be activated with either `sysctl kernel.sysrq=1` or `echo "1" > /proc/sys/kernel/sysrq`. If you wish to have it enabled during boot, add `kernel.sysrq = 1` to your [sysctl configuration](/index.php/Sysctl#Configuration "Sysctl"). If you want to make sure it will be enabled even before the partitions are mounted and in the initrd, then add `sysrq_always_enabled=1` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

A common idiom to remember this is "**R**eboot **E**ven **I**f **S**ystem **U**tterly **B**roken" (also referred to as "REISUB"). Alternatively, think of it as "BUSIER" backwards.

| Keyboard Shortcut | Description |
| `Alt+SysRq+r` Unraw | Take control of keyboard back from X. |
| `Alt+SysRq+e` Terminate | Send SIGTERM to all processes, allowing them to terminate gracefully. |
| `Alt+SysRq+i` Kill | Send SIGKILL to all processes, forcing them to terminate immediately. |
| `Alt+SysRq+s` Sync | Flush data to disk. |
| `Alt+SysRq+u` Unmount | Unmount and remount all filesystems read-only. |
| `Alt+SysRq+b` Reboot | Reboot |

**Tip:**

*   If you are using a [display manager](/index.php/Display_manager "Display manager") and after `Alt+SysRq+e` you are presented with the login screen (or full desktop if autologin is enabled), it is most likely caused by `Restart=always` directive in the relevant [service file](/index.php/Systemd "Systemd"). If necessary, [edit the unit](/index.php/Edit_the_unit "Edit the unit"), however this should not prevent the "REISUB" sequence from working.
*   If all the above combinations work except `Alt+SysRq+b`, try using the contralateral `Alt` key.
*   On laptops that use `Fn` key to differentiate `SysRq` from `PrtScrn`, it may not actually be necessary to use the `Fn` key (i.e., `Alt+PrtSc+*letter*` could work).
*   On Lenovo laptops `SysRq` is often configured as `Fn+S`. To use it press and hold `Alt` then press `Fn+s`, **release** `Fn` and `s` still holding `Alt` followed by the keys above.
*   You may need to press `Ctrl` along with `Alt`. So for example, full key shortcut would be `Ctrl+Alt+SysRq+b`.

See [Wikipedia:Magic SysRq key](https://en.wikipedia.org/wiki/Magic_SysRq_key "wikipedia:Magic SysRq key") for more details.

### Virtual console

See [Linux console#Keyboard shortcuts](/index.php/Linux_console#Keyboard_shortcuts "Linux console").

### Xorg and Wayland

| Keyboard Shortcut | Description | Notes |
| `Ctrl+Alt+F1`, `F2`, `F3`, ... | Switch to *n*-th virtual console | If it does not work, try `Ctrl+Fn+Alt+F…`. |
| `Shift+Insert`
`Mouse Button 2` | Paste text from the [PRIMARY buffer](/index.php/Clipboard "Clipboard") | By default, Qt maps `Shift+Insert` to CLIPBOARD instead of the PRIMARY buffer (see e.g. [[1]](http://doc.qt.io/qt-5/qlineedit.html#details)) and `Ctrl+Shift+Insert` is mapped to the PRIMARY buffer. |

## Customization

### Readline

[Readline](/index.php/Readline "Readline") is a commonly used library for line-editing; it is used for example by [Bash](/index.php/Bash "Bash"), FTP, and many more (see the details of [readline](https://www.archlinux.org/packages/?name=readline) package under "Required By" for more examples). It has [Emacs](/index.php/Emacs "Emacs")-like and [vi](/index.php/Vi "Vi")-like editing modes which can be customized with escape sequences. Default key bindings are listed in the [Info documentation](https://tiswww.cwru.edu/php/chet/readline/rluserman.html).

### Zsh

[Zsh](/index.php/Zsh "Zsh") uses [ZLE](/index.php/Zsh#Key_bindings "Zsh") to link shortcuts to widgets, scripts and commands.

### Xorg

See [Xorg/Keyboard configuration#Frequently used XKB options](/index.php/Xorg/Keyboard_configuration#Frequently_used_XKB_options "Xorg/Keyboard configuration") for some common shortcuts, that are disabled by default.

When we are in a graphical environment we may want to execute a command when certain key combination is pressed (i.e. bind a command to a *keysym*). There are multiple ways to do that:

*   The most portable way using low level tools, such as [acpid](/index.php/Acpid "Acpid"). Not all keys are supported, but configuration in uniform way is possible for keyboard keys, power adapter connection and even headphone jack (un)plugging events. It is also difficult to run programs inside X session correctly.
*   The universal way using [Xorg](/index.php/Xorg "Xorg") utilities (e.g. [xbindkeys](/index.php/Xbindkeys "Xbindkeys")) and eventually your desktop environment or window manager tools.
*   The quicker way using a third-party program to do everything in GUI, such as the Gnome Control Center.

#### sxhkd

A simple X hotkey daemon with a powerful and compact configuration syntax. See [sxhkd](/index.php/Sxhkd "Sxhkd") for details.

#### actkbd

From [actkbd home page](http://users.softlab.ece.ntua.gr/~thkala/projects/actkbd/):

	[actkbd](https://aur.archlinux.org/packages/actkbd/) (available in [AUR](/index.php/AUR "AUR")) is a simple daemon that binds actions to keyboard events. It recognises key combinations and can handle press, repeat and release events. Currently it only supports the linux-2.6 evdev interface. It uses a plain-text configuration file which contains all the bindings.

A sample configuration and guide is available [here](http://users.softlab.ece.ntua.gr/~thkala/projects/actkbd/latest/README).

#### xbindkeys

[xbindkeys](/index.php/Xbindkeys "Xbindkeys") allows advanced mapping of keysyms to actions independently of the Desktop Environment.

**Tip:** If you find `xbindkeys` difficult to use, try the graphical manager [xbindkeys_config-gtk2](https://aur.archlinux.org/packages/xbindkeys_config-gtk2/) from the [AUR](/index.php/AUR "AUR").

### Desktop environments

*   [LXDE#Bindings](/index.php/LXDE#Bindings "LXDE")
*   [Xfce#Keyboard_Shortcuts](/index.php/Xfce#Keyboard_Shortcuts "Xfce")

### Windows managers

*   [Fluxbox#Hotkeys](/index.php/Fluxbox#Hotkeys "Fluxbox")
*   [Openbox#Keybinds](/index.php/Openbox#Keybinds "Openbox")

### Key binding for X-selection-paste

Users who prefer to work with the keyboard rather than the mouse may benefit from a key binding to the paste operation of the middle mouse button. This is especially useful in a keyboard-centered environment. A workflow example is:

1.  In Firefox, select a string you want to google for (with the mouse).
2.  Hit `Ctrl+k` to enter the "search engine" field.
3.  Hit `F9` to paste the buffer, instead of moving the mouse pointer to the field and middle-click to paste.

**Note:** `Shift+Insert` has a similar yet different functionality, see [#Xorg](#Xorg): `Shift+Insert` inserts the clipboard buffer, not the x-selection-paste buffer. In some applications, these two buffers are mirrored.

The method suggested here uses the following three packages::

*   [xsel](https://www.archlinux.org/packages/?name=xsel) to give access to the x-selection-buffer content.
*   [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") to bind a key-stroke to an action.
*   [xvkbd](https://aur.archlinux.org/packages/xvkbd/) to pass the buffer string to the application by emulating keyboard input.

This example binds the x-selection-paste operation to the `F9` key:

 `.xbindkeysrc` 
```
"xvkbd -no-jump-pointer -xsendevent -text "\D1`xsel`" 2>/dev/null"
    F9

```

The `"\D1"` code prefixes a 100 ms pause to inserting the selection buffer (see the [xvkbd home page](http://t-sato.in.coocan.jp/xvkbd/)).

**Note:** Depending on your X configuration, you may need to drop the `-xsendevent` argument to xvkbd.

The key codes for keys other than `F9` can be determined using `xbindkeys -k`.

References:

*   [Pasting X selection (not clipboard) contents with keyboard](http://unix.stackexchange.com/questions/11889/pasting-x-selection-not-clipboard-contents-with-keyboard)
*   [xvkbd home page](http://homepage3.nifty.com/tsato/xvkbd/)

#### XMonad Window Manager

In the [xmonad](https://www.archlinux.org/packages/?name=xmonad) window manager there is a built-in function to paste the x-selection-buffer content. In order to bind that function to a key-stroke (here `Insert` key) the following configuration can be used:

 `xmonad.hs` 
```
import XMonad.Util.Paste
...
  -- X-selection-paste buffer
  , ((0,                     xK_Insert), pasteSelection) ]

```

## Tips and tricks

*   If you like a keyboard-centered workflow, you might also appreciate a [tiling window manager](/index.php/Window_manager#Tiling_window_managers "Window manager").

## See also

*   [The Linux Magic System Request Key - Kernel documentation](https://www.kernel.org/doc/html/v4.11/admin-guide/sysrq.html)
*   [Linux Newbie Administrator Guide - Shortcuts and Commands](http://lnag.sourceforge.net/lnag_html/node5.html)
*   [The Linux keyboard and console HOWTO](http://tldp.org/HOWTO/Keyboard-and-Console-HOWTO.html)