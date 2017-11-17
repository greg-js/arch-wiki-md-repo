This article provides a list of (not commonly known) default keyboard shortcuts and provides information about user customization.

## Contents

*   [1 Standard shortcuts](#Standard_shortcuts)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Terminal](#Terminal)
        *   [1.2.1 Virtual console](#Virtual_console)
        *   [1.2.2 Readline](#Readline)
    *   [1.3 X11 & Wayland](#X11_.26_Wayland)
*   [2 User customization](#User_customization)
    *   [2.1 Readline](#Readline_2)
    *   [2.2 X11](#X11)
    *   [2.3 Firefox](#Firefox)
    *   [2.4 Key binding for X-selection-paste](#Key_binding_for_X-selection-paste)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 See also](#See_also)

## Standard shortcuts

### Kernel

There are several low level shortcuts that are implemented in the kernel which can be used for debugging and recovering from an unresponsive system. Whenever possible, it is recommended that you use these shortcuts instead of doing a hard shutdown (holding down the power button to completely power off the system).

To use these, they must first be activated with either `sysctl kernel.sysrq=1` or `echo "1" > /proc/sys/kernel/sysrq`. If you wish to have it enabled during boot, edit `/etc/sysctl.d/99-sysctl.conf` and insert the text `kernel.sysrq = 1`. If you want to make sure it will be enabled even before the partitions are mounted and in the initrd, then add `sysrq_always_enabled=1` to your [kernel parameters](/index.php/Kernel_parameters "Kernel parameters").

A common idiom to remember this is "**R**eboot **E**ven **I**f **S**ystem **U**tterly **B**roken" (also referred to as "REISUB"). Alternatively, think of it as "BUSIER" backwards.

| Keyboard Shortcut | Description |
| `Alt+SysRq+r` Unraw | Take control of keyboard back from X. |
| `Alt+SysRq+e` Terminate | Send SIGTERM to all processes, allowing them to terminate gracefully. |
| `Alt+SysRq+i` Kill | Send SIGKILL to all processes, forcing them to terminate immediately. |
| `Alt+SysRq+s` Sync | Flush data to disk. |
| `Alt+SysRq+u` Unmount | Unmount and remount all filesystems read-only. |
| `Alt+SysRq+b` Reboot | Reboot |

**Tip:**

*   If you are using a [display manager](/index.php/Display_manager "Display manager") and after `Alt+SysRq+e` you are presented with the login screen (or full desktop if autologin is enabled), it is most likely caused by `Restart=always` directive in the relevant [service file](/index.php/Systemd "Systemd"). If necessary, [edit the unit](/index.php/Systemd#Editing_provided_units "Systemd"), however this should not prevent the "REISUB" sequence from working.
*   If all the above combinations work except `Alt+SysRq+b`, try using the contralateral `Alt` key.
*   On laptops that use `Fn` key to differentiate `SysRq` from `PrtScrn`, it may not actually be necessary to use the `Fn` key (i.e., `Alt+PrtSc+*letter*` could work).
*   On Lenovo laptops `SysRq` is often configured as `Fn+S`. To use it press and hold `Alt` then press `Fn+s`, **release** `Fn` and `s` still holding `Alt` followed by the keys above.
*   You may need to press `Ctrl` along with `Alt`. So for example, full key shortcut would be `Ctrl+Alt+SysRq+b`.

See [Magic SysRq key - Wikipedia](https://en.wikipedia.org/wiki/Magic_SysRq_key "wikipedia:Magic SysRq key") for more details.

Other kernel keyboard shortcuts include:

| Keyboard Shortcut | Description |
| `Alt+SysRq+D` | Display all existing file locks |
| `Alt+SysRq+F` | Summon the kernel [OOM](https://en.wikipedia.org/wiki/Out_of_memory "wikipedia:Out of memory") killer, which will kill a process to free up memory |
| `Alt+SysRq+K` | Kill everything running in the current virtual console (VT) |
| `Alt+SysRq+M` | Output the current memory information |
| `Alt+SysRq+O` | Shutdown the machine |
| `Alt+SysRq+T` | Display a list of current tasks |
| `Alt+SysRq+N` | Resets the nice level of high and real-time priority processes |

### Terminal

#### Virtual console

| Keyboard Shortcut | Description |
| `Ctrl+Alt+Del` | Reboots Computer (specified by the symlink `/usr/lib/systemd/system/ctrl-alt-del.target`) |
| `Alt+F1`, `F2`, `F3`, ... | Switch to *n*-th virtual console |
| `Alt+ ←` | Switch to previous virtual console |
| `Alt+ →` | Switch to next virtual console |
| `Scroll Lock` | When Scroll Lock is activated, input/output is locked |
| `Shift+PgUp`/`PgDown` | Scrolls console buffer up/down |
| `Ctrl+c` | Kills current task |
| `Ctrl+d` | Inserts an EOF |
| `Ctrl+z` | Pauses current Task |

#### Readline

GNU readline is a commonly used library for line-editing; it is used for example by Bash, FTP, and many more (see the details of [readline](https://www.archlinux.org/packages/?name=readline) package under "Required By" for more examples). readline is also customizable (see man page for details).

| Keyboard Shortcut | Description |
| `Ctrl+l` | Clear the screen |
| **Cursor Movement** |
| `Ctrl+b` | Move cursor one character to the left |
| `Ctrl+f` | Move cursor one character to the right |
| `Alt+b` | Move cursor one word to the left |
| `Alt+f` | Move cursor one word to the right |
| `Ctrl+a` | Move cursor to start of the line |
| `Ctrl+e` | Move cursor to end of the line |
| **Copy & Paste** |
| `Ctrl+u` | Cut everything from line start to cursor |
| `Ctrl+k` | Cut everything from the cursor to end of the line |
| `Alt+d` | Cut the current word after the cursor |
| `Ctrl+w` | Cut the current word before the cursor |
| `Ctrl+y` | Paste the previous cut text |
| `Alt+y` | Paste the second latest cut text |
| `Alt+Ctrl+y` | Paste the first argument of the previous command |
| `Alt+.`/`_` | Paste the last argument of the previous command |
| **History** |
| `Ctrl+p` | Move to the previous line |
| `Ctrl+n` | Move to the next line |
| `Ctrl+s` | Search |
| `Ctrl+r` | Reverse search |
| `Ctrl+j` | End search |
| `Ctrl+g` | Abort search (restores original line) |
| `Alt+r` | Restores all changes made to line |
| **Completion** |
| `Tab` | Auto-complete a name |
| `Alt+?` | List all possible completions |
| `Alt+*` | Insert all possible completions |

### X11 & Wayland

| Keyboard Shortcut | Description | Notes |
| `Ctrl+Alt+F1`, `F2`, `F3`, ... | Switch to *n*-th virtual console | If it does not work, try `Ctrl+Fn+Alt+F…`. |
| `Shift+Insert`
`Mouse Button 2` | Paste text from the [PRIMARY buffer](/index.php/Clipboard "Clipboard") | By default, Qt maps `Shift+Insert` to CLIPBOARD instead of the PRIMARY buffer (see e.g. [[1]](http://doc.qt.io/qt-5/qlineedit.html#details)) and `Ctrl+Shift+Insert` is mapped to the PRIMARY buffer. |

## User customization

### Readline

This example adds keys that allow (in *vi-mode*) to search backward through the history for the string of characters between the start of the current line and the point. This is a non-incremental search.

 `.inputrc` 
```
set editing-mode vi
set keymap vi-insert
"\C-r": history-search-backward
"\C-e": history-search-forward

```

### X11

See [Keyboard configuration in Xorg#Frequently used XKB options](/index.php/Keyboard_configuration_in_Xorg#Frequently_used_XKB_options "Keyboard configuration in Xorg") for some common shortcuts, that are disabled by default.

### Firefox

Use the [customizable-shortcuts](https://addons.mozilla.org/en-us/firefox/addon/customizable-shortcuts/) add-on.

### Key binding for X-selection-paste

Users who prefer to work rather with the keyboard than the mouse may benefit from a key binding to the paste operation of the **middle mouse button**. This is especially useful in a keyboard-centered environment. A workflow example is:

1.  In Firefox, select a string you want to google for (with the mouse).
2.  Hit `Ctrl+k` to enter the "Google search" field.
3.  Hit `F12` to paste the buffer, instead of moving the mouse pointer to the field and center-click to paste.

**Note:** `Shift+Insert` has a similar yet different functionality, see [#X11](#X11): `Shift+Insert` inserts the clipboard buffer, not the x-selection-paste buffer. In some applications, these two buffers are mirrored.

The method suggested here uses three packages available in the [official repositories](/index.php/Official_repositories "Official repositories"):

*   [xsel](https://www.archlinux.org/packages/?name=xsel) to give access to the x-selection-buffer content.
*   [Xbindkeys](/index.php/Xbindkeys "Xbindkeys") to bind a key-stroke to an action.
*   [xvkbd](https://www.archlinux.org/packages/?name=xvkbd) to pass the buffer string to the application by emulating keyboard input.

This example binds the x-selection-paste operation to the `F12` key:

 `.xbindkeysrc` 
```
"xvkbd -no-jump-pointer -xsendevent -text "\D1`xsel`" 2>/dev/null"
    F12

```

The `"\D1"` code prefixes a 100 ms pause to inserting the selection buffer (see the [xvkbd home page](http://homepage3.nifty.com/tsato/xvkbd/)).

**Note:** Depending on your X configuration, you may need to drop the `-xsendevent` argument to xvkbd.

The key codes for keys other than `F12` can be determined using `xbindkeys -k`.

**References:**

*   [Pasting X selection (not clipboard) contents with keyboard](http://unix.stackexchange.com/questions/11889/pasting-x-selection-not-clipboard-contents-with-keyboard)
*   [xvkbd home page](http://homepage3.nifty.com/tsato/xvkbd/)

**XMonad Window Manager**

In the [xmonad](https://www.archlinux.org/packages/?name=xmonad) window manager there is a built-in function to paste the x-selection-buffer content. In order to bind that function to a key-stroke (here `Insert` key) the following configuration can be used:

 `xmonad.hs` 
```
import XMonad.Util.Paste
...
  -- X-selection-paste buffer
  , ((0,                     xK_Insert), pasteSelection) ]

```

**Using xdotool** - command-line X11 automation tool

With the [xdotool](https://www.archlinux.org/packages/?name=xdotool) it is possible to create a short cut which actually pastes the content of the X-Selection buffer via triggering the middle mouse button. Instead of hit the text as separate key strokes. The command for the short cut is:

`xdotool getwindowfocus key --window %1 click 2`

The command get the window which has focus from the xserver and triggers a click of button 2 which is the middle mouse button.

## Tips and tricks

*   If you like a keyboard-centered workflow, you might also appreciate a [tiling window manager](/index.php/Window_manager#Tiling_window_managers "Window manager").

## See also

*   [The Linux Magic System Request Key - Kernel documentation](https://www.kernel.org/doc/Documentation/sysrq.txt)
*   [Linux Newbie Administrator Guide - Shortcuts and Commands](http://lnag.sourceforge.net/lnag_html/node5.html)
*   [The Linux keyboard and console HOWTO](http://tldp.org/HOWTO/Keyboard-and-Console-HOWTO.html)