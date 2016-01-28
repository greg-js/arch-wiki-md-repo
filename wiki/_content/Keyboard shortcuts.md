# Keyboard shortcuts

From ArchWiki

Jump to: [navigation](#column-one), [search](#searchInput)

This article provides a list of (not commonly known) default keyboard shortcuts and provides information about user customization.

## Contents

*   [1 Standard shortcuts](#Standard_shortcuts)
    *   [1.1 Kernel](#Kernel)
    *   [1.2 Terminal](#Terminal)
        *   [1.2.1 Virtual console](#Virtual_console)
        *   [1.2.2 Readline](#Readline)
    *   [1.3 X11](#X11)
*   [2 User customization](#User_customization)
    *   [2.1 Readline](#Readline_2)
    *   [2.2 X11](#X11_2)
    *   [2.3 Firefox](#Firefox)
    *   [2.4 Key binding for X-selection-paste](#Key_binding_for_X-selection-paste)
*   [3 Tips and tricks](#Tips_and_tricks)
*   [4 See also](#See_also)

## Standard shortcuts

### Kernel

There are several low level shortcuts that are implemented in the kernel which can be used for debugging and recovering from an unresponsive system. Whenever possible, it is recommended that you use these shortcuts instead of doing a hard shutdown (holding down the power button to completely power off the system).

To use these, they must first be activated with either `sysctl kernel.sysrq=1` or `echo "1" > /proc/sys/kernel/sysrq`. If you wish to have it enabled during boot, edit `/etc/sysctl.d/99-sysctl.conf` and set `kernel.sysrq = 1`.

A common idiom to remember this is "**R**eboot **E**ven **I**f **S**ystem **U**tterly **B**roken" (also referred to as "REISUB"). Alternatively, think of it as "BUSIER" backwards.

<table class="wikitable">

<tbody>

<tr>

<th>Keyboard Shortcut</th>

<th>Description</th>

</tr>

<tr>

<td>`Alt+SysRq+r` **Unraw**</td>

<td>Take control of keyboard back from X.</td>

</tr>

<tr>

<td>`Alt+SysRq+e` **Terminate**</td>

<td>Send SIGTERM to all processes, allowing them to terminate gracefully.</td>

</tr>

<tr>

<td>`Alt+SysRq+i` **Kill**</td>

<td>Send SIGKILL to all processes, forcing them to terminate immediately.</td>

</tr>

<tr>

<td>`Alt+SysRq+s` **Sync**</td>

<td>Flush data to disk.</td>

</tr>

<tr>

<td>`Alt+SysRq+u` **Unmount**</td>

<td>Unmount and remount all filesystems read-only.</td>

</tr>

<tr>

<td>`Alt+SysRq+b` **Reboot**</td>

<td>Reboot</td>

</tr>

</tbody>

</table>

**Tip:**

*   If you are using a [display manager](/index.php/Display_manager "Display manager") and after `Alt+SysRq+e` you are presented with the login screen (or full desktop if autologin is enabled), it is most likely caused by `Restart=always` directive in the relevant [service file](/index.php/Systemd "Systemd"). If necessary, [edit the unit](/index.php/Systemd#Editing_provided_units "Systemd"), however this should not prevent the "REISUB" sequence from working.
*   If all the above combinations work except `Alt+SysRq+b`, try using the contralateral `Alt` key.
*   On laptops that use `Fn` key to differentiate `SysRq` from `PrtScrn`, it may not actually be necessary to use the `Fn` key (i.e., `Alt+PrtSc+_letter_` could work).
*   You may need to press `Ctrl` along with `Alt`. So for example, full key shortcut would be `Ctrl+Alt+SysRq+b`.

See [Magic SysRq key - Wikipedia](https://en.wikipedia.org/wiki/Magic_SysRq_key "wikipedia:Magic SysRq key") for more details.

### Terminal

#### Virtual console

<table class="wikitable">

<tbody>

<tr>

<th>Keyboard Shortcut</th>

<th>Description</th>

</tr>

<tr>

<td>`Ctrl+Alt+Del`</td>

<td>Reboots Computer (specified by the symlink `/usr/lib/systemd/system/ctrl-alt-del.target`)</td>

</tr>

<tr>

<td>`Alt+F1`, `F2`, `F3`, ...</td>

<td>Switch to _n_-th virtual console</td>

</tr>

<tr>

<td>`Alt+ ←`</td>

<td>Switch to previous virtual console</td>

</tr>

<tr>

<td>`Alt+ →`</td>

<td>Switch to next virtual console</td>

</tr>

<tr>

<td>`Scroll Lock`</td>

<td>When Scroll Lock is activated, input/output is locked</td>

</tr>

<tr>

<td>`Shift+PgUp`/`PgDown`</td>

<td>Scrolls console buffer up/down</td>

</tr>

<tr>

<td>`Ctrl+c`</td>

<td>Kills current task</td>

</tr>

<tr>

<td>`Ctrl+d`</td>

<td>Inserts an EOF</td>

</tr>

<tr>

<td>`Ctrl+z`</td>

<td>Pauses current Task</td>

</tr>

</tbody>

</table>

#### Readline

GNU readline is a commonly used library for line-editing; it is used for example by Bash, FTP, and many more (see the details of [readline](https://www.archlinux.org/packages/?name=readline) package under "Required By" for more examples). readline is also customizable (see man page for details).

<table class="wikitable">

<tbody>

<tr>

<th>Keyboard Shortcut</th>

<th>Description</th>

</tr>

<tr>

<td>`Ctrl+l`</td>

<td>Clear the screen</td>

</tr>

<tr>

<td colspan="2" align="center">**Cursor Movement**</td>

</tr>

<tr>

<td>`Ctrl+b`</td>

<td>Move cursor one character to the left</td>

</tr>

<tr>

<td>`Ctrl+f`</td>

<td>Move cursor one character to the right</td>

</tr>

<tr>

<td>`Alt+b`</td>

<td>Move cursor one word to the left</td>

</tr>

<tr>

<td>`Alt+f`</td>

<td>Move cursor one word to the right</td>

</tr>

<tr>

<td>`Ctrl+a`</td>

<td>Move cursor to start of the line</td>

</tr>

<tr>

<td>`Ctrl+e`</td>

<td>Move cursor to end of the line</td>

</tr>

<tr>

<td colspan="2" align="center">**Copy & Paste**</td>

</tr>

<tr>

<td>`Ctrl+u`</td>

<td>Cut everything from line start to cursor</td>

</tr>

<tr>

<td>`Ctrl+k`</td>

<td>Cut everything from the cursor to end of the line</td>

</tr>

<tr>

<td>`Alt+d`</td>

<td>Cut the current word after the cursor</td>

</tr>

<tr>

<td>`Ctrl+w`</td>

<td>Cut the current word before the cursor</td>

</tr>

<tr>

<td>`Ctrl+y`</td>

<td>Paste the previous cut text</td>

</tr>

<tr>

<td>`Alt+y`</td>

<td>Paste the second latest cut text</td>

</tr>

<tr>

<td>`Alt+Ctrl+y`</td>

<td>Paste the first argument of the previous command</td>

</tr>

<tr>

<td>`Alt+.`/`_`</td>

<td>Paste the last argument of the previous command</td>

</tr>

<tr>

<td colspan="2" align="center">**History**</td>

</tr>

<tr>

<td>`Ctrl+p`</td>

<td>Move to the previous line</td>

</tr>

<tr>

<td>`Ctrl+n`</td>

<td>Move to the next line</td>

</tr>

<tr>

<td>`Ctrl+s`</td>

<td>Search</td>

</tr>

<tr>

<td>`Ctrl+r`</td>

<td>Reverse search</td>

</tr>

<tr>

<td>`Ctrl+j`</td>

<td>End search</td>

</tr>

<tr>

<td>`Ctrl+g`</td>

<td>Abort search (restores original line)</td>

</tr>

<tr>

<td>`Alt+r`</td>

<td>Restores all changes made to line</td>

</tr>

<tr>

<td colspan="2" align="center">**Completion**</td>

</tr>

<tr>

<td>`Tab`</td>

<td>Auto-complete a name</td>

</tr>

<tr>

<td>`Alt+?`</td>

<td>List all possible completions</td>

</tr>

<tr>

<td>`Alt+*`</td>

<td>Insert all possible completions</td>

</tr>

</tbody>

</table>

### X11

<table class="wikitable">

<tbody>

<tr>

<th>Keyboard Shortcut</th>

<th>Description</th>

<th>Notes</th>

</tr>

<tr>

<td>`Ctrl+Alt+F1`, `F2`, `F3`, ...</td>

<td>Switch to _n_-th virtual console</td>

</tr>

<tr>

<td>`Shift+Insert`  
`Mouse Button 2`</td>

<td>Paste text from the [PRIMARY buffer](/index.php/Clipboard "Clipboard")</td>

<td>By default, Qt maps `Shift+Insert` to CLIPBOARD instead of the PRIMARY buffer (see e.g. [[1]](http://doc.qt.io/qt-5/qlineedit.html#details)).</td>

</tr>

</tbody>

</table>

## User customization

### Readline

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

[![Tango-two-arrows.png](/images/7/72/Tango-two-arrows.png)](/index.php/File:Tango-two-arrows.png)

**This article or section is a candidate for merging with [Readline](/index.php/Readline "Readline").**

**Notes:** This section duplicates content of the main article. (Discuss in [Talk:Keyboard shortcuts#](https://wiki.archlinux.org/index.php/Talk:Keyboard_shortcuts))

This example adds keys that allow (in _vi-mode_) to search backward through the history for the string of characters between the start of the current line and the point. This is a non-incremental search.

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

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

[![Tango-emblem-important.png](/images/c/c8/Tango-emblem-important.png)](/index.php/File:Tango-emblem-important.png)

**The factual accuracy of this article or section is disputed.**

**Reason:** The shortcuts presented here are mixed up or outdated: `F12` in Firefox toggles the developer tools [[2]](https://support.mozilla.org/en-US/kb/keyboard-shortcuts-perform-firefox-tasks-quickly?redirectlocale=en-US&redirectslug=Keyboard+shortcuts#w_tools) and `Shift+Insert` pastes the PRIMARY buffer. (Discuss in [Talk:Keyboard shortcuts#](https://wiki.archlinux.org/index.php/Talk:Keyboard_shortcuts))

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

Retrieved from "[https://wiki.archlinux.org/index.php?title=Keyboard_shortcuts&oldid=412643](https://wiki.archlinux.org/index.php?title=Keyboard_shortcuts&oldid=412643)"

[Categories](/index.php/Special:Categories "Special:Categories"):

*   [Keyboards](/index.php/Category:Keyboards "Category:Keyboards")
*   [X server](/index.php/Category:X_server "Category:X server")
*   [Accessibility](/index.php/Category:Accessibility "Category:Accessibility")

Hidden categories:

*   [Pages or sections flagged with Template:Merge](/index.php/Category:Pages_or_sections_flagged_with_Template:Merge "Category:Pages or sections flagged with Template:Merge")
*   [Pages or sections flagged with Template:Accuracy](/index.php/Category:Pages_or_sections_flagged_with_Template:Accuracy "Category:Pages or sections flagged with Template:Accuracy")